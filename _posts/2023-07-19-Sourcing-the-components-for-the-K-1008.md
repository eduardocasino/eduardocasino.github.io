---
title: Sourcing the components for the K-1008
date: 2023-07-19 11:38:00 +0100
categories: [Hardware, KIM-1]
tags: [kim-1, mtu, k-1008]     # TAG names should always be lowercase
---
The boards have already been sent to fabrication and I'm starting to source the components. There are a few obsolete components that are either difficult to find and/or expensive to get, so I'm using up to date replacements when possible:

* There are no modern substitutes for the MM5280 memory chips, but it is still possible to find them as they were widely used for arcade machines. Even the slower MM5280-5 variant should work as they are within the 300ns access/470ns cycle specs for the board (they are 270/470 vs 200/400 for the faster version)
* All the logic ICs are also still manufactured, except for the 74ls13, but it is still in stock in some places. I'm using HCT variants when available to keep power consumption low.
* I'll probably left the regulators unpopulated (bridged) and use regulated 5V and 12V, but the LM340T5 is still in production and the LM342P12 can be replaced by the LM340T12.
* The 2N3904/2N3906 pair seems like a good replacement for the 2N3646/2N9416 in the level shifters. Will have to adjust the base resistor, though. The TO106 package is not made anymore, I'll go with TO92.
* And, finally, a low Vf Schottky, like the BAT86, will be a perfect replacement for the Ge 1N270 diode to simulate an open-collector gate for the VECTOR_FETCH (K7) signal.
