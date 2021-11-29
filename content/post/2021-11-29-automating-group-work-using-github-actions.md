+++
title = "Automating Group Work Using GitHub  Actions"
description = """
  Using Git to co-ordinate group assignments and automate PDF generation
  using GitHub Actions.
  """
date = 2021-11-29T17:57:00+03:00
publishDate = 2021-11-29T00:00:00+03:00
tags = ["latex", "typesetting"]
draft = false
+++

During our group assignment, my group was assigned to do a case study
of Netflix' business model; it's sustainability; and pricing.  I
realise that many people in my group are new to TeX, version control
and to some extent the desire to automate workflows.  As such, this
post presents a novel workflow that I proposed to my group-mates in a
bid to make things more efficient without diving deep into the arcanes
of programming.

First, everything is maintained in [Git](https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/).  In the main Git [repository](https://github.com/BonfaceKilz/dsa8201-group-netflix-group-work) we
have TeX files from which people will be making their contributions.
Contributions, at least to the main repository, are made either by
[creating an issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue) to the main repository, or by creating a [Pull Request](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository)
against the main repository.  Understandably, simple as this may seem
to your seasoned computer user, it's not obvious.  As such, the group
leader(not me!) maintains a parallel google docs sheet which hosts
group work content from the rest of the group.  Some volunteer would
thereafter have to spend some time to update the main TeX files to
reflect activities from google docs.

What we have so far is a repository with TeX files, and nothing more.
What else could we do further?  First, we could have a way of
compiling those files and exposing those files to GitHub; and later
send a copy to our Group's slack channel.  For that, we use
[GitHub Actions](https://github.com/features/actions).  [GitHub Actions](https://github.com/features/actions) provides a Linux environment from which
we could have TeX installed, and have a PDF generated.  This is shown
in this YAML configuration snippet:

```yaml
name: Generate pdf

# Run actions when pushing to the main branch or when you create a
# PR against it
on: push

jobs:
  build_latex:
    runs-on: ubuntu-latest
```

_Note that we run this action whenever we update (push to) the main
branch of the repository.  More of this later._

Next we checkout our repository:

```yaml
    - name: Set up Git repo
      uses: actions/checkout@v2
```

We thereafter generate the main file whilst specifying "main.tex" as our target.  This is akin to running a command like: `pdflatex main.tex` on the file (for the extra curious, a bib command is also run).

```yaml
    - name: Compile LaTex document
      uses: xu-cheng/latex-action@v2
      with:
        root_file: main.tex
```

The generated `main.pdf` file is our "artefact"; and we need to upload it so that we can store that data during the workflow.  Here is how that is done:

```yaml
    - name: Upload artifact
      uses: actions/upload-artifact@v2
      with:
        name: PDF
        path: main.pdf
```

We are almost there!  Now we need to make a release, which looks like
[this](https://github.com/BonfaceKilz/dsa8201-group-netflix-group-work/releases).  Before we go on, we need to answer an important question: **How
should releases be made?** Making a release on every single push is
noisy, and really not helpful.  For this particular case, I opted to
make a release based on git tagging.  The idea is that whenever we
make a some significant progress worth reviewing, we create a tag; and
whenever I push that tag to the main repository, a release is made.
Tags would look like: `v0.0.1-intro-wip`, `v0.0.1-intro-final`, etc.
Naming Conventions is something we can agree on as a group later.  The
snippet responsible for making a release based on a tag is:

```yaml
    - name: Release
      uses: softprops/action-gh-release@v1
      if: startsWith(github.ref, 'refs/tags/')
      with:
        files: main.pdf
```

Finally, we upload the work to Slack.  For this, note the we store our tokens using [encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets); and that looks like:

```yaml
    - name: Slack upload
      uses: adrey/slack-file-upload-action@master
      if: startsWith(github.ref, 'refs/tags/')
      with:
        token: ${{ secrets.SLACK_TOKEN }}
        path: main.pdf
        channel: netflix
```

And there you have it!  We make contributions in one central place,
and we automate the pdf generation and slack upload.  Extra steps,
depending on how active people are, would be to ping the lecturer on
Slack after every release.

Finally, the full configuration file:

```yaml
name: Generate pdf

# Run actions when pushing to the main branch or when you create a
# PR against it
on: push

jobs:
  build_latex:
    runs-on: ubuntu-latest
    steps:
    - name: Set up Git repo
      uses: actions/checkout@v2

    - name: Compile LaTex document
      uses: xu-cheng/latex-action@v2
      with:
        root_file: main.tex

    - name: Upload artifact
      uses: actions/upload-artifact@v2
      with:
        name: PDF
        path: main.pdf

    - name: Release
      uses: softprops/action-gh-release@v1
      if: startsWith(github.ref, 'refs/tags/')
      with:
        files: main.pdf

    - name: Slack upload
      uses: adrey/slack-file-upload-action@master
      if: startsWith(github.ref, 'refs/tags/')
      with:
        token: ${{ secrets.SLACK_TOKEN }}
        path: main.pdf
        channel: netflix
```