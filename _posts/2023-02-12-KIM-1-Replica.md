---
title: KIM-1 Replica
date: 2023-02-12 00:01:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mos, commodore]     # TAG names should always be lowercase
---
I'm making a 1:1 reproduction of a KIM-1 PCB, using the high resolution photos on Hans Oten's website, specially the ones of the Rev. D. I'm using KiCad together with Inkscape to reproduce the footprints of the components, circuit traces, logos and everything else as accurately as possible.

First step has been to redo the schematics in KiCad, so I can have a basis to compare the reproduction with. Next, a high resolution image of a KIM-1 was used as a template in Inkscape. The image was resized to scale using the IC footprints as a reference. Then, the rest of the footprints were placed and I'm starting to trace the tracks using bézier curves. I'm using a layer for each type of graphic components (footprints, tracks, copper zones, typography, ...)

I've recreated the logo using the original MOS logo and adding the commodore name with the Eurostile Extended 2 Bold font.

I'm using the Futura STD Bold font for component references and The Arial-like Aria font for other typography.

The inkscape image is imported from Kicad to an user layer and used as a template for placing the footprints. Then, the image with the tracks is being imported to the copper layer and converted to kicad tracks, so it will be possible to check the pcb against the schematic.

The logo and the typography were converted to footprints using the svg2shenzhen plugin.

This is the current status:

![img-description](/assets/img/posts/2023-02-12-KIM-1-Replica/kim-1-components.png)
![img-description](/assets/img/posts/2023-02-12-KIM-1-Replica/kim-1-front.png)
![img-description](/assets/img/posts/2023-02-12-KIM-1-Replica/kim-1-back.png)

Everything is available at my [GitHub repository](https://github.com/eduardocasino/kim-1).

Thanks to Hans Otten for the invaluable info at his site,http://retro.hansotten.nl

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
