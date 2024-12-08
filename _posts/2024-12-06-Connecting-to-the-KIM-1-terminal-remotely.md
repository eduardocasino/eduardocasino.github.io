---
title: Connecting to the KIM-1 terminal remotely
date: 2024-12-06 00:00:00 +0100
categories: [Hardware, KIM-1]
image:
  path: /assets/img/posts/2024-12-06-Connecting-to-the-KIM-1-terminal-remotely/preview.png
  alt: Foto by manny PANTOJA at Unsplash
tags: [kim-1, mtu, esp8266, wifi, telnet]     # TAG names should always be lowercase
---
A few weeks back, Ryan Roth made very interesting post in the [PAL 6502 computer group](https://groups.google.com/g/pal6502):

![img-description](/assets/img/posts/2024-12-06-Connecting-to-the-KIM-1-terminal-remotely/group-post.png)

And, as you see, he kinda challenged me! :wink:

I took the bait and, in a couple of hours, came up with this design:

![img-description](/assets/img/posts/2024-12-06-Connecting-to-the-KIM-1-terminal-remotely/kim-1-aux-card-esp.png)

Which I've just finished building and testing. Now I can connect to my KIM-1 terminal over WiFi and using telnet. Thanks, Ryan!

![img-description](/assets/img/posts/2024-12-06-Connecting-to-the-KIM-1-terminal-remotely/card-installed.jpg)
![img-description](/assets/img/posts/2024-12-06-Connecting-to-the-KIM-1-terminal-remotely/connected.png)

Everything at my [GitHub repository](https://github.com/eduardocasino/kim-1-mtu-motherboard)

This opens up an interesting possibility. With just a few mods, maybe I can remotely control the KIM (power supply, reset) so I can have fun with the real thing wherever I am... :smirk:
