---
layout: post
title:  "How to Concatenate MP3s Into a Single File"
date:   2020-10-27 4:08:00 -0600
categories: technology
tags: linux command-line
---

Before you proceed, run `ls *.mp3` to check that they're in the correct order. You may need to rename files to get the order right.

```
sudo apt-get install mp3wrap
mp3wrap output.mp3 *.mp3
```

