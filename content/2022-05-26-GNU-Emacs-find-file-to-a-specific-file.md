+++
title = "GNU Emacs find-file to a specific line"
description = "How to make find-file open and go a given line-number"
date = 2022-05-26T18:17:00+03:00

draft = false

[taxonomies]
tags = ["programming", "emacs"]
+++

In GNU Emacs, there's no way that I am aware of
making "find-file" to open a buffer/file and go to
a specific line number. With this useful [advice](https://www.gnu.org/software/emacs/manual/html_node/elisp/Advising-Functions.html),
you can achieve this:

```el
;; Open files and goto lines like we see from g++ etc. i.e. file:line#
;; (to-do "make `find-file-line-number' work for emacsclient as well")
;; (to-do "make `find-file-line-number' check if the file exists")
(defadvice find-file (around find-file-line-number
                             (filename &optional wildcards)
                             activate)
  "Turn files like file.cpp:14 into file.cpp and going to the 14-th line."
  (save-match-data
    (let* ((matched (string-match "^\\(.*\\):\\([0-9]+\\):?$" filename))
           (line-number (and matched
                             (match-string 2 filename)
                             (string-to-number (match-string 2 filename))))
           (filename (if matched (match-string 1 filename) filename)))
      ad-do-it
      (when line-number
        ;; goto-line is for interactive use
        (goto-char (point-min))
        (forward-line (1- line-number))))))
```

Now, you can go to a function by "C-x C-f"
"&lt;file-name&gt;:line-number"
