---
title: Application and IO board for the KIM-1
date: 2023-09-25 20:04:00 +0100
last_modified_at: 2023-10-29 21:03:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mtu, k-1008, k-1013]     # TAG names should always be lowercase
---

> **Update:** Project ditched in favour of [this one]({% post_url 2023-10-29-MTU-motherboard-for-the-KIM-1-finished %})
{: .prompt-info }

I'm working on an expansion and IO board for the application connector of the KIM-1, which I'm shamelessly calling "KIM-1 Super I/O" :stuck_out_tongue_winking_eye:. It is meant to be a companion of the MTU expansion board I made recently, so MTU boards with dual connectors should fit. What is new about it is that I'm including serial to USB conversion in it using an FT230 chip. You can select between USB or RS-232 with a switch. The usual audio and power connectors are also there, as well as an IEC bus. I'm including the schematic in case someone may be interested or can spot any blatant mistake.

[kim-1-super-io.pdf](/assets/files/posts/2023-09-25-Application-and-IO-board-for-the-KIM-1/kim-1-super-io.pdf)

This is the current PCB design:

![img-description](/assets/img/posts/2023-09-25-Application-and-IO-board-for-the-KIM-1/kim-1-super-io.png)

As always, I'll make everything available on GitHub.

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
