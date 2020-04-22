---
layout: post
title:  "How to Fix Bisq And Other Applications Not Appearing in Dmenu on Ubuntu"
date:   2020-04-22 4:08:00 -0600
categories: technology
tags: linux ubuntu command-line bisq bitcoin
---

I'm currently diving down the bitcoin rabbit hole. I played around with bitcoin a bit in college but didn't take the time to really understand it. This time around I'm hoping to truly embrace the decentralized benefits by keeping my wallet on my local machine, currently using [bitcoin-qt](https://bitcoin.org/en/download), and finding a decentralized way to get buy coins. [Bisq](https://bisq.network/) claims to offer such a decentralized marketplace.

I installed it this morning, but ran into a bit of a hiccup. When I typed `bisq` into [dmenu](https://wiki.archlinux.org/index.php/Dmenu), no options appeared.

I was immediately suspicious this was due to my usage of [i3 window manager](https://i3wm.org/) instead of [gnome 3](https://www.gnome.org/gnome-3/), Ubuntu's default desktop environment.

Sure enough, I logged out and back in using gnome and Bisq was available in the application launcher. I've run into this problem a few times with other applications, so I hope this guide can be useful to others.

To figure out where it was installed, I ran:
```
dpkg-query -L Bisq
```
Which revealed it is installed in: `/opt/Bisq/`

![opt/bisq](/assets/img/opt-bisq.png)

I got lucky guessing which file was the executable by running:

```
/opt/Bisq/Bisq
```


So I created a quick script in `~/.local/bin/` to run the program.

```
touch ~/.local/bin/bisq
```

Added the contents with `vim`

```
#!/bin/sh	

/opt/Bisq/Bisq &>/dev/null &
```

And finally, made it executable

```
chmod a+x ~/.local/bin/bisq
```

Then logged back in using i3 and reaped the rewards!	

