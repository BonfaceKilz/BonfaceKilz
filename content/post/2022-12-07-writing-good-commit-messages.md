+++
title = "Good Commit Messages"
description = "How to write good commit messages"
date = 2022-12-08T16:21:00+03:00
tags = ["git"]
draft = false
+++

Commit messages are an important part of the software development process, as they provide a way to document and communicate the changes made to a codebase.  Good commit messages make it easier to do some things like generating a comprehensive changelog; and also bisecting code for errors.  A good commit message should be clear, concise, and informative, and should provide context and information about the changes being made.  Here are some pointers for writing good commit messages:

-   Keep it short and to the point: A good commit message should be short and concise, and should avoid unnecessary details or jargon. Aim for a message that is no more than 50-70 characters long, and that clearly and briefly summarizes the changes being made.
-   Use the imperative mood: A good commit message should use the imperative mood, as if it is issuing a command.  For example, instead of "Adds a new feature", use "Add a new feature".  This makes the message more direct and actionable, and makes it easier for others to understand and follow the changes.  One good way to help with this is to try and fill this in: "If this commit is applied, it will ... &lt;Your message&gt;"
-   Describe the changes: A good commit message should describe the changes being made, and should provide enough information for others to understand the purpose and impact of the changes.  This may include details about the specific files or lines of code that were changed, the motivation for the changes, and any known or potential issues or limitations.
-   Use the subject-body format: A good commit message should use the subject-body format, with a short subject line followed by a more detailed body.  The subject line should be a brief and concise summary of the changes, while the body can provide additional context and information.  This format makes it easier to quickly scan and understand the commit message, and allows for more detailed and nuanced explanations of the changes.

Personally, I stick to the [ChangeLog commit style](https://www.conventionalcommits.org/en/v1.0.0/).  Another alternative is the [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/).  I prefer the former to the latter.  To illustrate "why", say we modified a python function with tho following commit (obtained from the conventionalcommits website):

```text
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z
Refs: #123
```

Here's how that would look like in a ChangeLog style:

```text
Prevent racing of requests

* app/process_requests.py (process_response):
Introduce request id and a reference to the latest
request. Dismiss incoming response other than
from the latest request.
(timeout_fn): Delete (obsolete).
```

With the above, I don't really have to look at the diffstat. To search for a change, it's easier to grep the commit messages than the changes; and you can feel this pain for a big project. Moreover, changelog commits, when done right, are easier to read - they can be brief (by reading the header and optional body), yet contain enough information to get a good feel for what's happening. Both are good and useful properties when doing bisects - they make the experience easier. Another thing I've observed is that IMHO I find changelogs are easier to read should a contributor opt to send mail patches.

Of course, take my opinions as just that, opinions. Take them with a pinch of salt. Best to stick with whatever convention your place of work or project demands. But for many GNU projects - GNU Guix, GNU/Linux, GNU Emacs, Many Guile projects, different GNU utils etc etc - it's useful to know that this is usually the default convention.

For Emacsen/Magit users, there's a default "magit-generate-changelog" which generates the log for you automatically for you in your commit buffer. I've appropriately bound this to "C-x c l"

Overall, a good commit message should be well-written, informative, and useful to others who may need to review or use the changes being made.  By following these tips and guidelines, you can write commit messages that are clear, concise, and effective, and that help to improve the quality and collaboration in your codebase.
