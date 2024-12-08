---
title: MTU motherboard for the KIM-1
date: 2023-10-08 21:07:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mtu, k-1008, k-1013]     # TAG names should always be lowercase
---
OK, after some thinking (not much, this is a hobby anyway :stuck_out_tongue_winking_eye:) and some discussions in the [Forum64](https://forum64.de), I'm ditching the original idea for the [application and IO board]({% post_url 2023-09-25-Application-and-IO-board-for-the-KIM-1 %}) and going with this::

* Old style, through hole components, full motherboard. As suggested by forum member Natas, all CPU lines buffered, maybe optional bus termination. Same size and looks as the KIM-1 board.
* Power connector for +5V, +12V, GND and unregulated +7.5V and +16V
* Apart from the buffering logic, just RS-232 and audio connectors to keep things "legacy"
* On top of that, an I/O card with at least USB TTY, IEC and one or two VIAs.
