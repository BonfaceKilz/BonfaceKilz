+++
title = "Using Haskell in JupyterLab"
description = "using haskell in jupyterlab"
tags = ["programming", "functional programming"]
categories = ["software"]
date= "2018-08-09"
+++

I've come to appreciate the use of JupyterLab in interactive computing. It is by far the best scientific computing tool that I've used to date. I was pleasantly surprised that they have Emacs bindings too! So far, I've limited myself to using Matlab and Python3 in the notebooks. With Python, I used it to prototype an Automatic Number Plate Recognition(ANPR) system(A computer vision/ machine learning project) for my final year project before writing the release software. With Matlab, I've used it to implement BCH codes, convolution codes and some rudimentary lab work based on digital control systems. Needless to say, it's been an invaluable tool for my school work and personal projects.

In this article I briefly walk through how I installed the Haskell Kernel for the Jupyter Lab.

First, ensure you have the following dependencies: `python3-pip git libtinfo-dev libzmq3-dev libcairo2-dev libpango1.0-dev libmagic-dev libblas-dev liblapack-dev.`

Also, ensure you have stack, which is Haskell's cross-platform program for developing Haskell projects[0]. You can install it by running:

```
curl -sSL https://get.haskellstack.org/ | sh

# or

wget -qO- https://get.haskellstack.org/ | sh
```

Clone the IHaskell project and `cd` into it:

```
git clone https://github.com/gibiansky/IHaskell
cd IHaskell
```

Use pip to install the requirements. In our case, the requirements contains necessary jupyter extensions and the minimum release version of jupyter that is required for our project to work. After installing these requirements, use stack to install gtk2hs-buildtools which is a package that provides a set of helper programs necessary to build GUI applications in haskell[1]. In the next step, we build the project we downloaded from github. Notice we use the `--fast` flag to turn off optimisations. This is very important since this step consumes alot of time. Finally after building `ihaskell install --stack` which install ihaskell and inherits the environment from stack when it is installed. This whole process is as follows:

```
pip3 install -r requirements.txt
stack install gtk2hs-buildtools
stack install --fast
ihaskell install --stack
```

Finally we install the jupyterlab ihaskell to get syntax highlighting[2] extension by running:

```
jupyter labextension install ihaskell_labextension
```

References:
[0] https://docs.haskellstack.org/en/stable/README/
[1] https://hackage.haskell.org/package/gtk2hs-buildtools
[2] https://github.com/gibiansky/IHaskell
