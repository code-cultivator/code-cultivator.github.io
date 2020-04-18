---
layout: post
title:  "How to Mount an ISO on Ubuntu from the Command Line"
date:   2020-04-18 10:08:00 -0600
categories: technology
tags: linux ubuntu command-line
---

On rare occasion, you gotta mount an ISO to get the job done. When I went looking for answers, most people suggested installing additional applications - but luckily for us, adding more bloat to our systems is not necessary. We can get this done with tools that already exist on our machines.


# First, create a directory to serve as the mount location

`sudo mkdir /media/iso`

# Then, mount the ISO in the target directory

`sudo mount -o loop path/to/iso/file/<your_iso_file>.iso /media/iso`

# Finally, unmount the ISO

`sudo umount /media/iso`

Easy as that!
