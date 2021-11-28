+++
title = "Quick Navigation in i3 Using Focus"
description = "A productivity for quick navigation in i3"
tags = ["software", "linux"]
categories = ["linux"]
date = "2018-08-24"
+++

_This is a brief hack for quick navigation using the [i3 window manager](https://i3wm.org/)._

If you find yourself commonly using specific applications, you can bind `focus` to that application. Here's an example of binding firefox, emacs, and a terminal:

```
bindsym $mod+Shift+f [class="Firefox"] focus
bindsym $mod+Shift+x [class="Emacs"] focus
bindsym $mod+Shift+t [class="(?i)terminal"] focus
```

You can also create a focused mode from which you can hard code focus keybindings. Here's an example:

```
# ~/.config/i3/config
# Enter focused mode
bindsym $mod+n mode "focused"

mode "focused" {
    # hardcoded focus keybindings
    bindsym f [class="(?i)firefox"] focus
    bindsym t [class="(?i)terminal"] focus
    bindsym x [class="Emacs"] focus

    # keybindings for marking and jumping to clients
    # use this to either mark or go to a container you want by name
    bindsym a exec i3-input -F 'mark %s' -P 'Mark name: '
    bindsym g exec i3-input -F '[con_mark=%s] focus' -P 'Go to mark: '

    # Assign marks to keys 1-5
    bindsym Shift+1 mark mark1
    bindsym Shift+2 mark mark2
    bindsym Shift+3 mark mark3
    bindsym Shift+4 mark mark4
    bindsym Shift+5 mark mark5

    # Jump to clients marked 1-5
    bindsym 1 [con_mark="mark1"] focus
    bindsym 2 [con_mark="mark2"] focus
    bindsym 3 [con_mark="mark3"] focus
    bindsym 4 [con_mark="mark4"] focus
    bindsym 5 [con_mark="mark5"] focus

    # Exit to the default mode
    bindsym Return mode "default"
    bindsym Escape mode "default"
}
```
