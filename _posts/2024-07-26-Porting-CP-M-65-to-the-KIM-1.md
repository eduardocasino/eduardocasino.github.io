---
title: Porting CP/M-65 to the KIM-1
date: 2024-07-26 00:00:00 +0100
last_modified_at: 2024-08-07 00:00:00 +0100
categories: [Software, KIM-1]
image:
  path: /assets/img/posts/2024-07-26-Porting-CP-M-65-to-the-KIM-1/preview.png
  alt: Photo by Michael Specht, CC BY-SA 3.0
tags: [kim-1, mtu, k-1013, cp/m, cpm, cp/m-65, iec]     # TAG names should always be lowercase
---
> **Update:** David Given has already merged my KIM-1 ports into [his repository](https://github.com/davidgiven/cpm65), so they are now part of the main branch.
{: .prompt-info }

It seems that everything related to CODOS 1.0, MTU's operating system that was meant to work along with the K-1013, is lost. Only images of CODOS 2.0 for the MTU-130 and MTU-140 exist and, although that computer also uses a K-1013, it has a more complex arqchitecture so that version is not compatible with the KIM.

So, that posed a question for my K-1013 replica project: **which software am i running with it?**

Then, I stumbled upon [Davis Given's CP/M-65](https://github.com/davidgiven/cpm65), a modern rewrite of the popular operating system that targets the 6502 CPU. It supported some popular machines, like the BBC Micro, the Apple ][ or even the PET, and was very well written and structured, so it seemed a very good candidate.

The K-1013 emulation in my Pico based [RAM/ROM/Video/FDC card]({% post_url 2024-05-24-A-fully-configurable-RAM-ROM-Video-disk-controller-card-for-the-KIM-1 %}) was also reasonably complete, so I just goy down to work. The most difficult part was to understand the complex, Python based, build system. Once I did, just created a new folder for the architecture dependent parts of the port, which are just the loader and the BIOS, had a good look at the other ports and started coding. A couple of days later, I got it running:

![img-description](/assets/img/posts/2024-07-26-Porting-CP-M-65-to-the-KIM-1/cpm-65-k1013.png)

This will make and excellent testbed for the real K-1013 when it is finished and will give it some utility, too. But not many people was going to benefit from that. Then, I saw Ryan Roth's implementation of a very [simple SD card interface](https://github.com/ryaneroth/sdcard6502) with the KIM. Adapting that to the existing port was a matter of a few hours, so that brought the OS to users of even less poerful systems, like the [PAL-1](https://www.tindie.com/products/kim1/pal-1-a-mos-6502-powered-computer-kit/):

![img-description](/assets/img/posts/2024-07-26-Porting-CP-M-65-to-the-KIM-1/cpm-65-sd.png)

The requirements are very simple:

* RAM expansion that fills the memory hole from 0x0400 to 0x13FF and provides at least 32K from 0x2000, but full expansion up to 0xFF00 is advisable.
* An SDHC card of any capacity (only 32MB are used) and a generic Arduino SD card adapter **with 5V to 3.3V conversion**. See Ryan's repository for detailed requisites and connection instructions.

And finally, David had already made a 1541 based port for the C-64 and I had the IEC routines for the KIM from the [xkim1541 project]({% post_url 2024-03-03-IEC-support-for-Corshams-xXIM-and-Microsoft-Basic %}), so it was just trivial to add that too. If you don't mind seeing your beard grow while it works, you can also run CP/M-65 on a KIM-1 or PAL-1 equiped with an IEC disk:

![img-description](/assets/img/posts/2024-07-26-Porting-CP-M-65-to-the-KIM-1/cpm-65-iec.png)

It has a few limitations, thugh:

* It only currently works for 1541 drives (or pi1541 with 1541 personality). Other drives or SDIEC are not supported.
* Did I say that it is slow as hell?

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
