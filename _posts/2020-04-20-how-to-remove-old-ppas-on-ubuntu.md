---
layout: post
title:  "How to Remove Old PPAs on Ubuntu 18.04"
date:   2020-04-20 7:08:00 -0600
categories: technology
tags: linux ubuntu command-line ppa apt
---

I recently ran `sudo apt update` and was provided with the following message:

```
E: The repository 'http://ppa.launchpad.net/pmcenery/ppa/ubuntu bionic Release' does not have a Release file.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
```

I couldn't remember why I had added this source, but after a bit of digging I realized this was from a while back when I was trying to sync my old iPhone with Ubuntu - an project I've since given up on. This isn't the first time I've had this happen, so I thought I'd document the fix for humanity.

The removal of a PPA on Ubuntu 18.04 is simple:

```
sudo rm -i /etc/apt/sources.list.d/<your_ppa_name>.*
sudo apt update
```

So in my case, the solution was: 

```
sudo rm -i /etc/apt/sources.list.d/pmcenery-ubuntu-ppa-bionic.*
sudo apt update
```

Problem solved.
