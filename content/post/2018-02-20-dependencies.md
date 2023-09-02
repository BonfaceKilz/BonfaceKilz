+++
title = "Sane Way of Handling Dependencies"
description = "A sane way of maintaining javascript repositories"
tags = [
    "programming",
    "javascript",
]
categories = ["coding"]
slug="managing-dependencies"
date = "2018-02-20"
+++

It's been very busy year this. I'm juggling work(yes I work nowadays), school, and my final year project(some ML stuff). This post is a simple reference for my future self on how to to handle dependencies in a sane way. I noticed that alot of fellas out there barely track dependencies on their project, and this is a very bad idea.

Here's a list of useful things to run on your root project folder:

1. Keep track of your currently available packages: `npm ls --depth=0`
2. See if you have unused `npm depcheck`
3. Check the download statistic of a given dependency to see if it's heavily used: `npm-stat`
4. Check if a dependency has a good, mature version release frequency with a large number of maintainers: `npm view <package name>`
5. Check for outdated dependencies: `npm outdated`. You can check for updates using a tool called `npm-check-updates`
