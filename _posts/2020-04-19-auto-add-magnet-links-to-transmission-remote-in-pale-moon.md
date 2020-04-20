---
layout: post
title:  "How to Automatically Add Magnet Links to Transmission Daemon from Firefox/Pale Moon"
date:   2020-04-19 10:08:00 -0600
categories: technology
tags: linux ubuntu command-line transmission pale-moon firefox
---

As I run [Transmisison][1] at the user level, as opposed to the default as root, I'll be making my script in `~/.local/bin/`. If you run [Transmission][1] as root, you'll want to put your script in `/usr/local/bin/`.

1. Create your script file named `magnet` in your `bin` directory of choice.
```
touch ~/.local/bin/magnet
```
2. Add contents to the script that pass the magnet link to `transmission-remote`
```sh
#!/bin/sh
exec transmission-remote --add "$1"
```

3. Make it executable
```
sudo chmod a+x ~/.local/bin/magnet
```

4. Set the application preferences for the Content-Type magnet to use our new script
![pale-moon-application-content-type-magnet](/assets/img/pale-moon-application-content-type-magnet.png)

5. Profit

[1]:https://transmissionbt.com/
