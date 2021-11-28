+++
title = "How to Setup Docker in FreeBSD"
description = "A guide on how to run Docker in FreeBSD"
date = 2020-01-19T19:09:00+03:00
tags = ["freebsd", "docker", "howto"]
draft = false
+++

Right now, you can't run docker natively on FreeBSD. I understand that there are
arguably better alternatives to Docker in the FreeBSD universe like using jails,
but it's hard to adjust to this if you're coming from Linux. Also, for many
projects out here, Docker is the preferred containerisation method of use, so
rest assured, alot of READMEs out here have instructions for a Docker set-up,
not jails.

Some people would ask, why not build Docker from source? Well, that's not
possible for now because Docker uses some Linux Kernel features like namespaces
and cgroups which are absent in FreeBSD. To make this work natively in FreeBSD,
someone would have to work around this. This has been attempted [before](https://www.freshports.org/sysutils/docker-freebsd/) but the
project has been stale for some time now. The only practical solution left is
running Docker inside a Linux VM inside FreeBSD. In this post, we'll be using
`docker-machine` and `virtualbox` to do just that.

First, you need to install a docker-client, docker-machine and virtualbox by:

```bash
sudo pkg install docker docker-machine virtualbox-ose
```

After installing virtualbox, you need to load the `vboxdrv` kernel module by
adding `vboxdrv_load="YES"` in `/boot/loader.conf`. You should also add your
current user to your `vboxusers` group in order to use vbox:

```bash
sudo pw groupmod vboxuser -m <username>
```

Once you are done, reboot your workstation in order to load the virtualbox
kernel modules.

I decided to use docker-machine for setting up docker because it lets me easily
create Docker hosts on my computer by creating servers, installing docker on
them and configuring Docker client to talk to them [0] and it's painless to use:

```bash
# Create the virtual box host
docker-machine create -d virtualbox default

# List all the hosts present:
docker-machine ls
```

Now you should set up your environment variables, so that your docker client can
be able to use docker installed inside virtualbox:

```bash
eval "$(docker-machine env default)"
```

You can opt to stick that fella ^ in your `.bashrc` or `.zshrc` file. With that,
you can run docker in FreeBSD :)

[0] <https://github.com/docker/machine/>
