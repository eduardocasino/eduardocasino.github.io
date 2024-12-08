---
title: All KIM-1 schematics are wrong!
date: 2023-03-23 20:07:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mos, commodore]     # TAG names should always be lowercase
---
I've just remembered that there is a mistake in the original KIM-1 schematic, the one included in the user manual, that has propagated to each and every one derived from it, since Ruud Baltissen's to latest replicas.

The values of resistors R18 to R23 and R41 to R46 are swapped. The former are pull-ups that should be 1K and the later are the base resistors, that should be 220R in early revisions or 100R from Rev. D and onwards.

On a side note, I've changed the license terms to my schematic and now it is CC BY 4.0, as it contains publicly available information and does not add any significant value. The "Non Commercial" restriction is now limited to the PCB.
