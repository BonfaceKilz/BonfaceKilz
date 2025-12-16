+++

date = "2017-07-06T07:28:39+03:00"
description = "Finally fixing the kindle 4 NT"

title = "Debricking Kindle 4NT part II"

[taxonomies]
tags = ["Hardware & Gadgets"]
categories = ["Hardware & Gadgets"]
+++

*Definitions:* Kindle 4 is also known as K4NT, K4 Non-Touch, K4S(silver) of K4B(black). The words debrick and debricking can also be called unbrick, unbricking, recover, recovery, repair, repairing, restore, restoring, restoration, or brick fix.

Well, good news! I've recovered my goddamn kindle. My [brother](https://jnduli.co.ke/e ) deserves a huge credit for this though. I had plugged my kindle in his wall socket(in his room). Dude just came back from work last night and started diagnosing the hell out of it. All I did was run some diagnostic tool :)

Anyway, here's what we did(for anyone who might run into the same problems).

First, enter bootmode by:

1. Plugging the kindle to your computer via a USB cable.
2. Long pressing the power button(about 20 seconds) until the kindle 4NT turns off.
3. Long pressing the 5-way button down.

Next, download the `diags_kernel` from this [link](https://www.mobileread.com/forums/showthread.php?t=170929https://www.mobileread.com/forums/showthread.php?t=170929URL ). Unzip the file and run:

```
# replace the <unzippedfile> with the name of
# the file you unzipped
sudo ./fastboot flash diags <unzippedfile>.img
sudo ./fastboot setvar bootmode diags
sudo ./fastboot reboot
```

After following the above mentioned steps, my kindle rebooted to a grey/ black screen. I then used `MfgTool` to recover my kindle. From `MfgTool`, I selected the `main` bootmode profile from the drop-down menu then clicked on the `start` button in the UI. That did it for me. The kindle booted normally after this.


##### Useful Resources: #####
1. http://www.mobileread.mobi/forums/showthread.php?t=170929
