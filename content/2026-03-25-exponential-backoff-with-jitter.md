+++
title = "Exponential Backoff with Jitter: Retries"
description = "When services time out, retrying immediately usually makes things worse.  This post shows a better way: exponential backoff with jitter.  Simple, works for one client or a thousand.  Code example included."
date = 2026-03-25T02:42:01+03:00

draft = false

[taxonomies]
categories = ["sre"]
tags = ["sre"]
+++

Transient failures happen alot in production systems.  Transient failures can come from:

- Network instability
- Service overload
- Resource contention
- Dependency flakiness
- Timeouts

When an operation fails transiently, immediate retries can be tempting.  However, this (moreso repeatedly) can amplify load at the worst possible moment, turning a temporary disruption into a cascading failure.

Consider a script that queries a Virtuoso triple store.  Under heavy load, the database may start returning HTTP 504 (Gateway Timeout) errors.

A naive retry loop might look like this:

```python
for attempt in range(max_retries):
    try:
        return sparql.queryAndConvert()
    except HTTPError as e:
        if e.code == 504:
            continue  # retry immediately
```

If the server is already struggling, immediate retries only add more pressure, making recovery harder.  Even if you add a fixed delay, all retries from all clients (or even a single client) will occur at the same intervals, possibly colliding with the server’s own cooldown periods.

## Exponential Backoff

Exponential backoff increases the delay between retries exponentially.  For example:

- First retry: 2 seconds
- Second retry: 4 seconds
- Third retry: 8 seconds

This gives the server a growing window of relief.  But there’s still a problem: if the delays are deterministic, a single client’s retries may consistently land on a server state that’s still recovering.  Worse, multiple clients would retry in perfect synchrony.

## Exponential Backoff with Jitter

Jitter adds a small random value to each calculated delay. This:

- Prevents retries from aligning across clients (thundering herd)
- Avoids deterministic collisions with server‑side recovery windows
- Spreads the load more evenly

In a single‑client scenario, jitter still helps by avoiding the situation where you always retry at times that happen to coincide with the server’s internal cooldown cycles.

Here’s a function that implements exponential backoff with jitter for a SPARQL query.  It retries only on HTTP 504 errors and uses a configurable base delay and maximum retries.

```python
import time
import random
from typing import Optional, Dict
from SPARQLWrapper import SPARQLWrapper
from urllib.error import HTTPError

def fetch_with_retry(
    sparql: SPARQLWrapper,
    max_retries: int = 3,
    base_delay: float = 2.0
) -> Optional[Dict]:
    """Execute SPARQL query with retry logic and exponential backoff."""
    for attempt in range(max_retries):
        try:
            return sparql.queryAndConvert()
        except HTTPError as e:
            if e.code == 504 and attempt < max_retries - 1:
                # Exponential backoff with jitter
                delay = base_delay * (2 ** attempt) + random.uniform(0, 1)
                print(f"    Timeout (attempt {attempt + 1}/{max_retries}), retrying in {delay:.1f}s...")
                time.sleep(delay)
            else:
                raise
    return None
```

Key Elements: 
- Exponential factor: base_delay * (2 ** attempt)
  - Attempt 0 → 2 seconds
  - Attempt 1 → 4 seconds
  - Attempt 2 → 8 seconds
- Jitter: `+ random.uniform(0, 1)` - adds a random value between 0 and 1 second. This small variance is enough to break any undesired alignment.
- Selective retry: Only HTTP 504 triggers a retry. Other errors are raised immediately, as they likely require different handling.
- Retry limit: The loop stops after `max_retries`, ensuring the operation eventually fails instead of retrying forever.

Some pointers:
- Use jitter even for a single client - it avoids deterministic collisions with server recovery periods.
- Set a maximum number of retries - infinite retries can mask underlying failures.
- Retry only idempotent operations - repeating non‑idempotent actions (e.g., writes) may cause data corruption.
- Log retries - in production, log each attempt with the delay used to aid debugging.
- Match base delay to your service - 1-2 seconds is a common starting point, but adjust based on typical recovery times.
