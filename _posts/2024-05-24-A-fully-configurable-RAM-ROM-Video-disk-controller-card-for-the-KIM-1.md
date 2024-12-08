---
title: A fully configurable RAM/ROM/Video/Disk controller card for the KIM-1
date: 2024-05-24 00:00:00 +0100
last_modified_at: 2024-11-30 00:00:00 +0100
categories: [Hardware, KIM-1]
image:
  path: /assets/img/posts/2024-05-24-A-fully-configurable-RAM-ROM-Video-disk-controller-card-for-the-KIM-1/preview.png
  alt: Card prototype (not final version)
tags: [kim-1, mtu, ram, rom, k-1008, k-1013, raspberry, pico, picow]     # TAG names should always be lowercase
---
> **Update:** K-1013 functionallity implemented. Still in beta, but working reasonably well. Also, sent to hell the Python `memcfg` utility and rewrote it in plain C.
{: .prompt-info }

I'm working on a fully configurable RAM/ROM/Video (and soon disk controller) card for the KIM-1. The picture above is of my prototype. The current design is now corrected and does not need the bodge wires :wink:.

As you can see, it is based in a Raspberry Pi Pico W and has some cool features:

* Can emulate RAM and/or ROM at any address of the KIM-1 memory map and with byte granularity so you can individually enable, disable, mark as RW or RO each and every byte of the 64K address space. It can also take over the KIM-1 system RAM and ROM, so it can be used as a diagnostic tool or to relive a KIM-1 with dead RAM.
* A default memory map and data are stored in the Pico flash memory and it is available at boot time.
* Runs a configuration web server with a RESTish API so you can configure and read or write all or any part of memory contents over Wifi and on the fly.
* The board is powered by the KIM-1, but it can also be dual powered by the KIM-1 and the USB port. This is useful, for example, if you are developing a boot ROM: you can power off the KIM, modify the boot program over wifi and turn it on again to test your changes.
* It emulates an MTU K-1008 Visible Memory Card . It can be mapped to the same addresses as the real one (and change that mapping while running) and gives configurable composite NTSC or PAL output through the RCA connector. VGA output is planned but unimplemented at the moment.
* Planned, but not yet implemented: K-1013 floppy disk controller emulation, reading and writing to disk images into the SD card.

A ~~python~~ C utility, memcfg, is provided to configure the board and facilitate the communication with the REST API. This is an overview of its functionality:

* Generate configuration files ready to be flashed into the Pico: WiFi parameters, video format, disk controller and images and default memory map and contents.
* Get or modify the memory map.
* Read memory contents and generate output in different formats: hexdump, Intel hex, binary, prg and raw. The raw format is how the Pico stores the memory map. Each memory address contains a 16-bit integer. The least significant byte is the content and the most significant one is a bitmap that indicates if the memory is enabled or disabled and writeable or read-only.
* Write memory contents from file or command line. The file formats supported are Intel hex, binary, prg and raw. Also, binary and raw data can be specified as a string from the command line.
* Modify the base address for the K-1008 emulation

Everything is now available in my GitHub repository. There is also a pitiful YouTube video with a small demo:

{% include embed/youtube.html id='ikJZE_anK7o' %}
