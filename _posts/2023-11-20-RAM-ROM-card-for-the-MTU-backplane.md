---
title: RAM ROM card for the MTU backplane
date: 2023-11-20 00:00:00 +0100
last_modified_at: 2024-04-30 00:00:00 +0100
categories: [Hardware, KIM-1]
image:
  path: /assets/img/posts/2023-11-20-RAM-ROM-card-for-the-MTU-backplane/preview.png
  alt: EPROM image by yellowcloud from Germany, CC BY 2.0
tags: [kim-1, mtu, k-1008, k-1013, ram, rom]     # TAG names should always be lowercase
---
> **Update:** New corrected and enhanced version
{: .prompt-info }

For it to be minimally usable, I need memory for my KIM-1. So, I've designed what I believe to be the most flexible KIM-1 memory expansion available:

* Switchable 0000-03FF systen RAM replacement
* Switchable 0400-13FF RAM
* Switchable system ROM replacement (needs a small modification to the MTU boards to disable the DECEN line if not used with my MTU buffered motherboard)
* 4 selectable ROM sets
* Enough room to place a ZIF socket for the ROM
* Switchable 4K RAM/ROM areas from 2000 to FFFF
* Configurable interrupt vectors to the top of any of the 4K chunks.
* Max. 1 TTL load on the bus, so it will work nicely on unbuffered backplanes

![img-description](/assets/img/posts/2023-11-20-RAM-ROM-card-for-the-MTU-backplane/kim-1-RAM-ROM.png)

Everything available at this [GitHub repository](https://github.com/eduardocasino/kim-1-mtu-ram-rom)

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
