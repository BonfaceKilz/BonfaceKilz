## Introduction

This repository contains all the code for my [blog](https://bonfacemunyoki.com "my blog").  It primarily serves as a back up for my websites.  It also serves as a way for external parties(if interested) to make corrections to some of the articles I have written.

The website is powered by [Hugo](https://gohugo.io/ "hugo")-- a static site generator written in GoLang -- and uses a theme called [Cactus Plus](https://themes.gohugo.io/hugo-theme-cactus-plus/ "theme used").

## How to build

Make sure you have Hugo [installed](https://gohugo.io/getting-started/installing/ "how to install hugo").

To preview all the content, including the draft articles:

```
hugo server -D
```

To generate the website:

```
hugo
```

## For Emacsen :heart: users

For my current blog flow(started 2019), I don't directly edit the mark down files.  Instead I have all my blog articles in an org file as trees.  I use [ox-hugo](https://ox-hugo.scripter.co/) to export the tree entries individual mark down entries.  I then use [easy-hugo](https://github.com/masasam/emacs-easy-hugo) to run the hugo preview command.  Here's my setup

```
(setq easy-hugo-basedir "~/Public/BonfaceKilz/")
(setq easy-hugo-url "https://bonfacemunyoki.com")
(setq easy-hugo-sshdomain "myserver")
(setq easy-hugo-root "$HOME/bonfacemunyoki.com/")
(setq easy-hugo-previewtime "300")
(define-key global-map (kbd "C-c C-e") 'easy-hugo)
```

<noscript><a href="https://liberapay.com/BonfaceKilz/donate"><img alt="Donate using Liberapay" src="https://liberapay.com/assets/widgets/donate.svg"></a></noscript>
