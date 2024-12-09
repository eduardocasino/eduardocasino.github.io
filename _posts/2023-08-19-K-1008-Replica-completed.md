---
title: K-1008 Replica completed
date: 2023-08-19 23:13:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mtu, k-1008]     # TAG names should always be lowercase
---
Board completed!

Time to do some tests and see if I got it right and how many of the MM5280 are fake.

I opted to install bridges instead of the 5V and 12v regulators and provide regulated power to the board, an option which the manual suggests and that Dave Plummer confirmed me that works great for his board.

![img-description](/assets/img/posts/2023-08-19-K-1008-Replica-completed/board-completed.jpg)

This is a picture of the test setup:

![img-description](/assets/img/posts/2023-08-19-K-1008-Replica-completed/test-setup.jpg)

The first tests do not not seem to indicate that there is any fundamental problem with the board :smiley:

All the memory is accessible and passes the memory tests by ["The Glitch Works"](https://github.com/glitchwrks/kim1_memtest). It's been running a few passes now without errors, so this clears two of my fears: the level shifter with the replacement transistors is working and the MM5280 chips seem legit!

At first, I couldn't get a clear picture. It had a lot of "color" artifacts and it moved constantly:

![img-description](/assets/img/posts/2023-08-19-K-1008-Replica-completed/bender.jpg)

It turned out that it was because I was using a crappy Chinese video converter and it did not sync very well. User Tobias of the [Forum64 forum](https://www.forum64.de/) suggested that an old professional broadcast monitor like the [Sony LMD-1420](https://pro.sony/support/res/manuals/2593/e9a36f991c95d8994f4fbff71237f169/25932771M.pdf) could be the solution and...

![img-description](/assets/img/posts/2023-08-19-K-1008-Replica-completed/success.jpg)

Success! Clean and stable image.

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
