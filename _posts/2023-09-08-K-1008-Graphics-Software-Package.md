---
title: K-1008 Graphics Software Package
date: 2023-09-08 00:05:00 +0100
categories: [Software, KIM-1]
tags: [kim-1, mtu, k-1008, assembly]     # TAG names should always be lowercase
---
I've reproduced the manual that came with the K-1008 Graphics Software Package, typed in the assembly sources and listings of the programs, made 64tass versions of those sources and built binaries (in Intel HEX and MOS papertape formats) from them. The SWIRL and LIFE demos have been tested on real hardware, the SDTXT and VMSUP subroutines just on Hans' emulator (I still have not made a memory expansion)

The manual was reproduced with the help of the Tesseract OCR for the texts, but all the listings were typed in manually. Then it was formatted using Libre Office and exported to PDF. It aims to be a true, facsimile quality reproduction of the original and for that reason I haven't fixed any typo, bug or grammatical error.

Big thanks to Hans Otten , who proofread, tested and fixed some errors (thankfully not so many :wink:) He's also made TASM32 versions of the sources and integrated the subroutines with MS Basic for the KIM-1. You can check it out [at his site](http://retro.hansotten.nl/) or [at my GitHub](https://github.com/eduardocasino/k-1008-graphics-software-package)
