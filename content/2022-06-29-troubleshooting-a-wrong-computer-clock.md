+++
title = "Troubleshooting a Wrong Computer System Clock"
description = "Troubleshooting a time-relate error in my system"
date = 2022-06-29T14:18:00+03:00
tags = ["linux"]
draft = false
+++

I got this error sometime today after doing a system upgrade:

> Your Computer Clock is Wrong
>
> Your computer thinks it is 6/2/2022, which prevents Firefox from connecting securely. To visit www.youtube.com, update your computer clock in your system settings to the current date, time, and time zone, and then refresh www.youtube.com.
>
> www.youtube.com has a security policy called HTTP Strict Transport Security (HSTS), which means that Firefox can only connect to it securely. You can’t add an exception to visit this site.

I fixed it by running:

```txt
sudo timedatectl set-ntp true
```
