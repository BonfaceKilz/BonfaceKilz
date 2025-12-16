+++
date = "2017-03-01T19:18:46+03:00"

tags = [
    "lfs", 
    "linux", 
    ]
description = "Frustrations when building my LFS system"
title = "LFS(Linux From Scratch) Frustrations"

[taxonomies]
categories = ["All Things Coding, Life"]
+++

Well, today has been frustrating. Very frustrating. I've been working on the whole LFS project for over 13 hours now[Compiling can be a biaaaaachh wo0t!]. I reached section 6.10(Adjusting the Toolchain) [here](http://www.linuxfromscratch.org/lfs/view/stable/chapter06/adjusting.html ). This is where my problems began.

<iframe src="//giphy.com/embed/joxAlNcfXnRaE" width="480" height="310" frameBorder="0" class="giphy-embed" allowFullScreen></iframe> 

After executing the following snippets: 
```
mv -v /tools/bin/{ld,ld-old}
mv -v /tools/$(uname -m)-pc-linux-gnu/bin/{ld,ld-old}
mv -v /tools/bin/{ld-new,ld}
ln -sv /tools/bin/ld /tools/$(uname -m)-pc-linux-gnu/bin/ld
``` 
and  
```
gcc -dumpspecs | sed -e 's@/tools@@g'                   \
    -e '/\*startfile_prefix_spec:/{n;s@.*@/usr/lib/ @}' \
    -e '/\*cpp:/{n;s@$@ -isystem /usr/include@}' >      \
    `dirname $(gcc --print-libgcc-file-name)`/specs``
```
I encountered errors. One of them being something along the lines `_could not find ld_`. I figured out that I missed an `ld` file in my tools directory. Further investigations[via `history`] showed that I skipped some very 2 vital steps when compiling Binutils in section 5.9 [here](http://www.linuxfromscratch.org/lfs/view/stable/chapter05/binutils-pass2.html). I did not copy `ld` to `ld-new` in the `/tools/bin` directory. Consequences? I'll have to start the whole goddamn build process again tomorrow goddamnit!

<iframe src="//giphy.com/embed/l0HlDJhyI8qoh7Wfu" width="480" height="360" frameBorder="0" class="giphy-embed" allowFullScreen></iframe> 

Well, mistakes aside, I have learnt something about the linux file systems[All about +ve energy here] and working with the terminal. It's interesting how Linux is organised. Every directory has a specific purpose e.g.  the `etc` directory for configuration files, the `dev` directory for placing virtual FS etc etc etc[not the `etc` directory Lol!]. I've also come to appreciate the concept of users and groups in the 'grand scheme' of things.

On working on the terminal, here are some really neat things with braces[which when used with other commands can be quite useful]: 
```
// Truncating the contents of a variable
$ var="Savagetfs"
$ echo ${var%t*}
// Result:
$ Savage 
// Making substitutions similar to sed
$ var="I hate thee Luffy Dono"; echo ${var/hate/love}
// Result: 
$ I love thee Luffy Done
// Iterating over loops
$ echo {0..2}
// Result
$ 0 1 2
```

There's so much more you can do with this stuff. Here's a neat example. Say you want to create a file structure with the following tree structure
```
. ├── build  
│   ├── css  
│   ├── html  
│   ├── js  
│   └── scss  
└── src  
├── css  
├── html  
├── js  
└── scss
```
Any of the following would work[vis-a-vis the above]:

```
// Method 1
$ folders=( html css js scss)
$ for i in ${folders[@]}; do mkdir -pv build/$i; done
$ for i in ${folders[@]}; do mkdir -pv src/$i; done
$ unset folders

// Method 2
// A verbose way of doing this
$ mkdir -pv src/{html,css,js,scss} build{html,css,js,scss}

// Method 3
// The elegant way
$ mkdir -pv {src,build}/{html,css,js,scss}
```
Well, there are many other small neat things you could for example: 
```
// When editing config files 
// For example, backing up your files 
// which would involve sth like this: 
// mv /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.old
$ mv /etc/pacman.d/mirrorlist{,.old}
```
I'll resume the build process again tomorrow. I'll be more careful this time. My goal is to finish the whole LFS project before this coming Saturday[04 March '17] where there'll be a NAILUG event.
