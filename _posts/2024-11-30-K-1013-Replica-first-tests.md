---
title: K-1013 Replica first tests
date: 2024-11-30 02:21:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mtu, k-1013]     # TAG names should always be lowercase
---
First "dry" test: powered up without connecting to the Kim, nothing blew up, no magic smoke, chips cold except for the D765 and the prom, which are lukewarm. So far, so good! :sweat_smile:

![img-description](/assets/img/posts/2024-11-30-K-1013-Replica-first-tests/power.jpg)

The board is adjusted as instructed in the manual and I can send commands and receive responses from the controller with no disk attached.

RAM tests also OK. All ram passes, but it was not at first try, of course. :stuck_out_tongue_winking_eye: It happens that one of the RAM chips was bad. I ordered 15 of them but, as I have no means to test them, I had to pick one of the spares, expect for it to be good and start swapping chips one by one. Today seems to be my lucky day, as the bad chip was the very first I swapped :smiley:

I've also done very basic tests like reading the configurable switch, setting the system RAM as read-only or read-write and read the status register of the 765. All good.

I'll contiue with the tests as soon I receive a missing connector.
