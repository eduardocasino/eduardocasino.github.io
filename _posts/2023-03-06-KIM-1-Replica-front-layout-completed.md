---
title: KIM-1 Replica front layout completed!
date: 2023-03-06 23:23:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mos, commodore]     # TAG names should always be lowercase
---
DRC against schematic passes. I finally came up with a solution for footprints that have pads with different shapes on front and back layers. The trick is using an SMD pad for the front, another for the back and a THT pad joining both sides. All three must have the same pad number.

![img-description](/assets/img/posts/2023-03-06-KIM-1-Replica-front-layout-completed/kim-1-components.png)
![img-description](/assets/img/posts/2023-03-06-KIM-1-Replica-front-layout-completed/kim-1-front.png)

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
