+++
title = "Notes on Using Mumi — Guix London Meet-Up 2024-08-20"
description = "My notes from today's meet-up."
date = 2024-08-29T22:08:00+03:00
publishDate = 2024-08-29T00:00:00+03:00

draft = false

[taxonomies]
tags = ["guix"]
+++

-   Check out guix toys.
-   Guix RDE makes the email set-up easy to work with.
    -   Check out:

        ```bash
        mumi search author:jgart
        mumi search submitter:jgart
        mumi search is:open
        mumi search date:2d..now
        mumi search date:2012-04-18..2022-04-18
        mumi search date:1m..today
        ```

-   Compose email:

    ```bash
    mumi compose
    mumi compose --close
    mumi compose --done
    ```

-   Current ticket:

    ```bash
    mumi current
    mumi current <ticket-number>
    ```

-   Mumi am:

    ```bash
    mumi current
    mumi am -- -S -s
    ```

-   Check deps:

    ```bash
    guix refresh -l foo
    ```

-   Consider setting up RDE.

-   Guix is a do-o-cracy.
