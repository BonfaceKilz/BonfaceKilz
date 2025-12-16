+++
title = "Sending Patches with Git: A Guide"
description = "Learn how to easily send patches from the command line using 'git send-email' and make interactive changes with 'git rebase -i'"
date = 2023-01-03T23:34:00+03:00
publishDate = 2022-12-21T00:00:00+03:00

draft = false

[taxonomies]
tags = ["email", "git", "guix", "command-line", "patches"]
+++

Are you tired of the tedious process of sending patches through your email client? Do you long for a simpler solution? Look no further! With just a few easy commands, you can send your patches straight from the command line.

First, install "guix install guix:send-email" and follow the example in [here](https://git-scm.com/docs/git-send-email) to set it up.

Once you've cloned your repository and created a branch with some new commits, use the command "git format-patch -&lt;N&gt; --base=master" to generate patches. N is the number of commits you've made - for example, use '-1' for one commit or '-2' for two. The '--base' option specifies the commit your changes apply to, but it's optional. You can also use the '--cover-letter' option to describe your changes in more detail. Type "git format-patch --help" for more information on this command.

This will produce patches with names like '0000-cover-letter.patch' and '0001-blabla.patch'. To send these patches, use the command "git send-email --to=guix-patches@gnu.org 0000-cover-letter.patch". Note that this assumes you used the '--cover-letter' option. You should receive a patch number assignment in your inbox if everything is set up correctly.

To send a single patch, use the command "git send-email --to=123456@debbugs.gnu.org 0001-blabla.patch". To send a patch set (multiple patches), use "git send-email --to=123456@debbugs.gnu.org 000?-\*.patch".

If you need to make changes to your patch after it has been reviewed, use "git rebase -i" to make interactive changes. Then, generate a new patch with "git format-patch -&lt;N&gt; -v2" (omitting the '--cover-letter' option this time). This will produce a patch with a name like 'v2-0001-blabla.patch', which you can send using the command "git send-email --to=123456@debbugs.gnu.org v2-0001-blabla.patch". Remember to keep the same patch number when sending revised patches.
