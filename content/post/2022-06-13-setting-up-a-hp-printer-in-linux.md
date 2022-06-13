+++
title = "Setting up a HP Printer in Linux"
description = "Setting up a HP printer in Linux"
date = 2022-06-13T20:47:00+03:00
publishDate = 2022-06-13T00:00:00+03:00
tags = ["linux", "howto"]
draft = false
+++

I have a "HP DeskJet Ink Advantage 4535" printer
in the house. I'll be doing a lot of printing in
the house given that I am committed to reading
more papers more consistently---I'm growing to
prefer physical media to virtual media. That said,
here are the steps I took to set-up my printer
over my home network:

-   First, install all the necessary packages from
    ArchLinux:

```text
sudo pacman -S cups avahi nss-mdns
```

-   Next, edit `/etc/cups/cupsd.conf` with the
    following specific edits:

    ```cfg
      [...]
      # Only listen for connections from the local machine.
      Port 631
      Listen /run/cups/cups.sock

      [...]

      # Restrict access to the server...
      <Location />
        Order allow,deny
        Allow @LOCAL
      </Location>

      # Restrict access to the admin pages...
      <Location /admin>
        AuthType Default
        Require valid-user
        Order allow,deny
        Allow @LOCAL
      </Location>

      [...]
    ```

-   Next make sure that the relevant services are
    enabled/started:

```text
sudo pacman systemctl enable cups avahi-daemon.service
```

-   Thereafter, scan for the printer:

```text
lpinfo --include-schemes dnssd -v
```

-   Use the url found in the previous step to add
    the printer using the web-interface at
    "localhost:673"


## Useful Links {#useful-links}

-   [Set up CUPS Print Server in Ubuntu 20.04](https://linuxhint.com/cups_print_server_ubuntu/)
-   [Using Network Printers](http://localhost:631/help/network.html)
-   [Host Name Resolution in Avahi](https://wiki.archlinux.org/title/Avahi#Hostname_resolution)
-   [CUPS---ArchWiki](https://wiki.archlinux.org/title/CUPS)
