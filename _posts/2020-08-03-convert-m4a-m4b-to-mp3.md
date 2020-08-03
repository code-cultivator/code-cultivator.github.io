---
layout: post
title:  "How to Convert m4a and m4b to mp3 with ffmpeg"
date:   2020-08-03 4:08:00 -0600
categories: technology
tags: linux command-line
---
Since I use an old SanDisk Sasnsa Clip+, I'm often converting m4a and m4b formatted audio to mp3s. Note that this drastically increases filesize.

```
ffmpeg -i input_file.m4[ab] -acodec libmp3lame output_file.mp3
```

