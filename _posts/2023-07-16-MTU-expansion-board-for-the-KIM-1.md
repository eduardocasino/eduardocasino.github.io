---
title: MTU expansion board for the KIM-1
date: 2023-07-16 10:24:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mtu, k-1008, k-1013]     # TAG names should always be lowercase
---
This board follows the MTU standard for the KIM-1 expansion bus and enables to connect up to five cards, like the K-1008. Additionally, all signals of the KIM-1 are replicated on an edge connector to allow further expansions and also on a pin header for easy breadboarding:

![img-description](/assets/img/posts/2023-07-16-MTU-expansion-board-for-the-KIM-1/kim-1-mtu-expansion-card-comp.png)

The MTU bus connects 1 to 1 to the KIM-1 expansion connector with the exception of pins 2,3, 16, 17, 18, 19, 20 and X, because MTU boards use some of these pins for power and expanded 18 bit address bus.

Two pin connectors have to be wired to pins J (K7) and K (DECODE ENABLE) of the KIM-1 application connector. Like in the original MTU's bus motherboard, a five screw terminal block provides power connections for both the KIM-1 (GND, +5V and +12V regulated) and the expansion boards (+7.5V and +16V unregulated). Also as in the original, the +12V terminal is not really connected to anything.

And this is how an example setup with one K-1008 board would look like:

![img-description](/assets/img/posts/2023-07-16-MTU-expansion-board-for-the-KIM-1/kim-1-with-k-1008.png)

Design files at [my GitHub repository](https://github.com/eduardocasino/kim-1-mtu-expansion-card).

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
