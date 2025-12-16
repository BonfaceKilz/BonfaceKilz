+++
title = "Troubleshooting Tmux"
description = "Troubleshooting Tmux"
date = 2022-01-10T16:51:00+03:00
tags = ["linux"]
draft = false
+++

For a while now, whenever I ran Tmux in my EXWM session, I always got
this annoying warning message:

```txt
/usr/lib/Xorg.wrap: Only console users are allowed to run the X serve
```

The problem lay in my `.zlogin` file where I had:

```txt
startx
```

I replaced the above with:

```txt
[ -z "$DISPLAY" ] && [ $XDG_VTNR -eq 1 ] && exec startx
```

And now I got rid of the above error message.