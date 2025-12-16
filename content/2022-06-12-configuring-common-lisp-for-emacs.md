+++
title = "Configuring Common Lisp for Emacs"
date = 2022-12-06T15:52:00+03:00
publishDate = 2022-12-06T00:00:00+03:00
tags = ["emacs"]
draft = false
+++

[Credits: [configuring slime](https://gist.github.com/jteneycke/7947353)]

-   First install sbcl:
    ```sh
      sudo pacman -S sbcl

      cd /tmp/
      curl -O http:/beta.quicklisp.org/quicklisp.lisp
      sbcl --load quicklisp.lisp
    ```

-   Within sbcl's context:

<!--listend-->

```lisp
(quicklisp-quickstart:install)
(ql:quickload "quicklisp-slime-helper")
```

-   Finally, add this to your .emacs configuration:

<!--listend-->

```el
(use-package slime
  :ensure t
  :mode ("\\.lisp\\'")
  :init
  (load (expand-file-name "~/quicklisp/slime-helper.el"))
  :custom
  (inferior-lisp-program "sbcl")
  :hook ((lisp-mode-hook . (lambda () (slime-mode t)))
	 (inferior-lisp-mode-hook . (lambda () (inferior-slime-mode t)))))
```
