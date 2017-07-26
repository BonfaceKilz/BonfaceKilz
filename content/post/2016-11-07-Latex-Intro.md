+++
title = "Latex- Introduction"
description = "A short introduction to Latex"
date = "2016-11-07"
tags = [
    "latex", 
    "typesetting",
]
categories = [
    "coding",
    ]
slug = "introduction-to-latex"
+++

<img style="width:100%;display:inline-block;max-width:300px; min-width:200px; margin:0 auto;margin-left:25%;" src="/img/funnywp.jpg" alt="Latex"/>

LATEX is a typesetting program. You use LATEX to create beautiful documents for other people to read. It is similar to MS Word in this regard, but the similarities end here.

So why LATEX. And where and how did it come to be?

LATEX is a precursor to Tex. Tex is an open-source typesetting system designed and mostly written by Donald Knuth -the guy who wrote The Art of Computer Programming (Knuth is considered the “Father” of algorithms which by no means is a small thing). TEX was designed with two main goals in mind: to allow anybody to produce high-quality books using minimal effort, and to provide a system that would give exactly the same results on all computers, at any point in time.

Preparing a document with LATEX typically involves editing a file with a ___.tex___ extension using your favorite text editor (Emacs, Vim, Notepad++, Sublime, texMaker etc etc ) and then later converting that file to a PDF (or another document interchange format like postscript).

Unlike word processing software(like Microsoft Word or LibreOffice), LATEX  is not a WYSIWYG i.e. it does not necessarily come with a gui. You have to work with syntax:

![LATEX vs WYSIWG editor](/img/drawing-1.png)

So, why go out of your way to learn some syntax?

1) ___Superior Typography.___  
LATEX  was designed to abstract typography(kerning, choosing fonts etc) so that you could focus more on the content. LATEX  has excellent built-in fonts, good algorithms for automatic spacing, and the ability to fine-tune the spacing arbitrarily. This is how a typical LATEX document looks like: 

![Beautiful Typography](/img/drawing-2.png)

2) ___Mathematical TypeSetting.___  
LATEX is by far the best at writing mathematical formula. Good luck doing this on any [MS] Word processor:

![Example of Latex Equations](/img/latex_demo.png)

3) ___Modularisation of Work.___  
What is modularisation? Modularisation means splitting your work into chunks. LATEX gives you the ability to divide your document into smaller sections and work on them separately.  

Where the main files reside:
![Where the main files reside](/img/Screenshot-from-2016-09-13-20-05-14.png)

Where the subsections reside:
![Where the subsections reside](/img/Screenshot-from-2016-09-13-20-05-17.png)

4) __Portability.___  
LATEX runs on virtually any operating system in existence.

5) ___Document longevity.___  
You can work with a document that was written 10 years ago in LATEX. How I wish the same could be said about other word processing software.

6) ___Support from other tools.___
Many other tools support tex. Stuff like org-mode in emacs, matlab, and pandoc, to mention just a few are able to work with tex in very interesting ways.

LATEX is a powerful tool which you can incorporate either directly or indirectly in your workflow. I use it to write my lab reports[in my final years of university] and also to write any documents that would need to be exported to pdf. Prior to find the amazing 'Ya-snippet' mode in Emacs, I wrote my own tex-pdf generator [here](https://github.com/BonfaceKilz/latexmk)
