---
title: Choosing the right transistors for the K-1008
date: 2023-08-08 11:01:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mtu, k-1008]     # TAG names should always be lowercase
---
Populating the real thing. Still awaiting for the obsolete parts (74LS13, 74LS55 and the memories) and also need to get some old school ceramic discs of reasonable size to mantain the vintage look. I have a VC20 and couple of C64 boards (no chips, used for repairs) with at least part of the required ones:

![img-description](/assets/img/posts/2023-08-08-Choosing-the-right-transistors-for-the-K-1008/board-progress.jpg)

The 2N3904 is not a suitable replacement for the 2N3646 in the level shifters. A transistor capable of very fast switching under saturation like the PN2369A should be a good match, as it has extreme low turn-on, turn-off and storage times. At first, I thought that the requirements for the PNP should not be as critical and a 2N3906 would do, as the speed-up capacitor would help to turn it on quickly enough and the fast turn-on time of the 2369 should compensate for the high storage time of the 3906:

![img-description](/assets/img/posts/2023-08-08-Choosing-the-right-transistors-for-the-K-1008/level-shifter.png)

But, it turned out it was not the case. The PN2369A is fast enough and the fall time for the CE waveform is acceptable, about 30ns (K-1008 documentation says a minimum of 25ns, but the MM5280 datasheet says between 10 and 40ns). The 2N3906, on the other hand, is terribly slow. The PN2907, used in the video generator, performs a bit better and I get a rise time just over 40ns, still a bit too much.

Searching through datasheets, I've found the 2N4403, which has better turn-on figures. Adjusted a bit the resistors and speed-up capacitors and.. Got it! 12V amplitude and transition from Vss+2V to Vdd-2V between 10ns-40ns, as required in the MM5280 datasheet (with my old scope, I estimate about 25-30ns)

![img-description](/assets/img/posts/2023-08-08-Choosing-the-right-transistors-for-the-K-1008/ce_waveform7.jpg)
