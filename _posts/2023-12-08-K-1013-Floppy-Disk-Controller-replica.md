---
title: K-1013 Floppy Disk Controller replica
date: 2023-12-08 19:11:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mtu, k-1013]     # TAG names should always be lowercase
---
I'm working on an as accurate as possible replica of the MTU K-1013 Floppy Disk Controller for the KIM-1. This card used the ubiquitous NEC uPD765 IC and supported 5.25 and 8 inch, double side, dual density floppy drives. It has 16k of onboard RAM, it supports DMA transfers and is supposed to be reasonably fast.

The version I'm reproducing is a later revision, that was used as part of the MTU-130 and MTU-140 computers, although is basically the same card with some corrections and a couple of enhancements and it is fully compatible with the KIM-1.

This is a picture of the card from [David Williams' MTU-130](https://www.trailingedge.com/) that he kindly sent me:

![img-description](/assets/img/posts/2023-12-08-K-1013-Floppy-Disk-Controller-replica/MTU-FDC-Front.jpg)

I've now completed the first version of the schematics and I'm starting with the PCB. I'll be sharing my progress in this blog.

I have to thank Dave Williams, Dave Plummer and Hans Otten for their help to make this possible.

As always, everything is available at my [GitHub repository](https://github.com/eduardocasino/k-1013-floppy-disk-controller-replica).

<script src="https://giscus.app/client.js"
        data-repo="eduardocasino/eduardocasino.github.io"
        data-repo-id="R_kgDONX03Cg"
        data-category="General"
        data-category-id="DIC_kwDONX03Cs4ClErs"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="es"
        crossorigin="anonymous"
        async>
</script>
