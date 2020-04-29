---
layout: post
title:  "How to Add Content Types to Mailcap in Mutt"
date:   2020-04-29 4:08:00 -0600
categories: technology
tags: linux ubuntu command-line mutt email
---

I've grown fond of using ![mutt]() as my email client and have been slowly optimizing it for my use over time.

I was sent an XLSX file this week, and when I attempted to open it, I was prompted with them message:
```
mailcap entry for type application/vnd.openxmlformats-officedocument.spreadsheetml.sheet not found
```
Luckily, the solution was quite simple.

First, create the config file
```
mkdir .config/mailcap
vim .config/mailcap/config
```

Then add the content type to the file, followed by `;`, then the command you want to run
```
application/vnd.openxmlformats-officedocument.spreadsheetml.sheet; libreoffice
```

Finally, reference the `mailcap_path` to  muttrc
```
vim .config/mutt/muttrc
```
and add
```
set mailcap_path = ~/.config/mailcap/config
```

And live happily ever after.
