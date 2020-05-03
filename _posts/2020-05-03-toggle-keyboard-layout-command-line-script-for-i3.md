---
layout: post
title:  "How to Toggle Keyboard Layout from a Command Line Script for i3"
date:   2020-05-03 4:08:00 -0600
categories: technology
tags: linux ubuntu command-line i3 keyboard bash scripting
---

I'm a fan of ergonomics and [dvorak keyboard layout](https://en.wikipedia.org/wiki/Dvorak_keyboard_layout), and as such, years ago I purchased a [Kinesis Advantage2 QD Keyboard](https://kinesis-ergo.com/shop/advantage2-dvorak/). I love using it, but it is a bit peculiar - it is capable of switching between qwerty and dvorak without the use of any software, as a result, when I plug my keyboard into my laptop, I must switch the keyboard layout on my machine to standard US layout, and use the Dvorak layout built into the keyboard itself, this means switching layouts whenever I plug or unplug my keyboard. 

I'd love to one day figure out how to toggle the proper layout automatically when the device is plugged in, but so far my attempts have been unsuccessful. I have however bound a `kbtoggle` script to `Super+F2` in [i3](https://i3wm.org/).

# Getting the Current Keyboard Layout

To begin writing a script to toggle the layout, first we must determine what layout we are already in. For whatever reason, on initial login, the layout is not just `us`, but `us,us`. We'll address this in a few steps.

```
[user@computer ~]$ setxkbmap -query
rules:      evdev
model:      pc105
layout:     us,us
variant:    dvorak,
```
A bit more output than we need, we can pipe the output to `grep` to get only the line containing the text `layout`

```
[user@computer ~]$ setxkbmap -query | grep layout
layout:     us,us
```
To remove the `layout: ` we can use `awk` to get only the second column of data

```
[user@computer ~]$ setxkbmap -query | grep layout | awk '{print $2}'
us,us
```
Finally, we can fix this inital issue of `us,us` by using `sed` to remove anything after the `,`

```
[user@computer ~]$ setxkbmap -query | grep layout | awk '{print $2}' | sed "s/\,.*//"
us
```

# Writing the Toggle Script

Now let's create a script file in `~/.local/bin` called `kbtoggle` and store our new layout in a variable, and toggle the layout based on the current layout

```
#!/bin/sh

current_layout=$(setxkbmap -query | grep layout | awk '{print $2}' | sed "s/\,.*//")

set_layout() {
	setxkbmap -layout "$1";
}

case "$current_layout" in
	us) set_layout "dvorak";;
	dvorak) set_layout "us";;
esac
```

# i3 Keybind

Now we can bind our script to a keyboard shortcut in i3 to easily change the layout.

Add this to your `~/.config/i3/config`
```
bindsym $mod+F2         exec --no-startup-id kbtoggle
```
