---
title: TI/National Bipolar PROM Programmer
date: 2024-09-28 19:03:00 +0100
categories: [Hardware, Arduino]
image: /assets/img/posts/2024-09-28-TI-National-Bipolar-PROM-Programmer/preview.png
tags: [kim-1, mtu, k-1013, prom, programmer, arduino]     # TAG names should always be lowercase
---
Based on [this design of a PROM programmer](https://theoddys.com/acorn/replica_boards/tesla_prom_programmer_board/tesla_prom_programmer_board.html) for the ACORN by Chris Oddy, I've designed this poor man's TI/National Semiconductor TTL PROM programmer shield for the Arduino Mega. It should be able to program the 74s471 (256x8 bit) I've just acquired, as well as other 256x8 and 512x8 bit PROMs from TI and Tesla.

The Arduino sketch is still WIP, currently just reads PROMS.

![img-description](/assets/img/posts/2024-09-28-TI-National-Bipolar-PROM-Programmer/programmer.jpg)

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
