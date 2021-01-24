---
layout: post
title:  "How to Fix Brasero Ejecting Disk Before Burning on Ubuntu 18.04"
date:   2020-10-27 4:08:00 -0600
categories: technology
tags: linux command-line
---

This issue arrises from brasero not having access to the cd drive. To resolve:

```
sudo chmod 4711 /usr/bin/wodim; sudo chmod 4711 /usr/bin/cdrdao
```

