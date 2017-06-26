+++
categories = ["productivity"]
date = "2017-06-25T16:01:59+03:00"
description = "How to share and download files over LAN"
tags = ["fundamentals", "productivity", "software"]
title = "Quickly sharing files over a Local Area Network"

+++
I do this(sharing files over LAN) all the time at home so I figured I'd just write about it. Sharing files over LAN avoids the constant hurdle of looking for a flash drive or some external medium to share files.

First off, you need to start a server on the machine you want to get the files from. I usually rely on python's `simpleHTTPServer` for this. To start it up, just run:

```
python3 -m http.server
```

Something important to note is that you need to run this in the directory you want to share. Now that you have the server running, you can view the files in a browser on another machine in the LAN. The `simpleHTTPServer` usually gives you an address. It may look something like this: `192.168.0.101:8000/`. You can save files from the URL using your browser. This is however redundant and time consuming if you decide to use the browser. You can use `Curl` or `wget` to download files. Assuming you navigated to `191.168.0.101:8000/movies` and the listed files were:
```

    [HorribleSubs] One-Punch Man - 01 [480p].mkv
    [HorribleSubs] One-Punch Man - 02 [480p].mkv
    [HorribleSubs] One-Punch Man - 03 [480p].mkv
    [HorribleSubs] One-Punch Man - 04 [480p].mkv
    [HorribleSubs] One-Punch Man - 05 [480p].mkv
    [HorribleSubs] One-Punch Man - 06 [480p].mkv
    [HorribleSubs] One-Punch Man - 07 [480p].mkv
    [HorribleSubs] One-Punch Man - 08 [480p].mkv
    [HorribleSubs] One-Punch Man - 09 [480p].mkv
    [HorribleSubs] One-Punch Man - 10 [480p].mkv
    [HorribleSubs] One-Punch Man - 11 [480p].mkv
    [HorribleSubs] One-Punch Man - 12 [480p].mkv

```
You could run the following `wget` command to retrieve all the files:

```
# -r                : recursive download
# -nc, --no-clobber : Skip download if file exists
# -nd               : download all files to the current directory
# -np               : don't follow links to parent dirs
# -k                : make links in downloaded HTML of CSS point to local files
# -e                : ignore robots.txt files

wget -r -nc -nd -np -k -e 191.168.0.101:8000/movies
```

What if you wanted to download files with a given file extension only? Well, you simply add the `-A` flag like so:

```
wget -r -nc -nd -k -e -A pdf 191.168.101:8000/docs
```

In conclusion, sharing files over a LAN can be convenient. Supplementing this with some tools(like wget and curl) are really useful in everyday tasks.
