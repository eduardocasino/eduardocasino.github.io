---
title: IEC support for Corsham's xXIM and Microsoft Basic
date: 2024-03-03 00:00:00 +0100
categories: [Software, KIM-1]
image: /assets/img/posts/2024-03-03-IEC-support-for-Corshams-xXIM-and-Microsoft-Basic/preview.png
tags: [kim-1, corsham, basic, kb9]     # TAG names should always be lowercase
---
I've been extending Dave McMurtrie's implementation of IEC disk support for the KIM-1 (from the ca65 port of Nils Andres, aka netzherpes). I've added long file names, sending arbitrary commands to the disk, directory listing, verify and add a jump-table based interface, and used that to add disk support to Corsham's xKIM monitor and Microsoft's KB9. Here is a video of it working:

{% include embed/youtube.html id='33Ilamfl38Y' %}

Code at my GitHub repository:

* **xkim1541:** [https://github.com/eduardocasino/xkim1541](https://github.com/eduardocasino/xkim1541)
* **xKIM with IEC support:** [https://github.com/eduardocasino/xKIM/tree/IEC_support](https://github.com/eduardocasino/xKIM/tree/IEC_support)
* **KB9 with disk support:** [https://github.com/eduardocasino/msbasic/tree/IEC_support](https://github.com/eduardocasino/msbasic/tree/IEC_support)

## Build

This is still experimental, use at your own risk!

### Requirements

* Expanded KIM-1 (or PAL-1) with RAM from 2000 to DFFF, ROM from E000 to FFFF and the IEC circuit based on Dave's design, like the one in Ralf's expansion or my own buffered motherboard.
* Linux, WSL or any unix-like system with git, bash, gmake and Python.
* Clone the xkim1541 repository and build using `make`. You'll need to have Python installed as there is a script that generates the include file depending on the base address. By default, the code is generated to be loaded at 0xF000. You can change it editing the `OFFSET` variable in the Makefile. I do not recommend modifying the other two variables: `ZPINIT` and `BSSINIT`, as they have been chosen to not interfere with either xKIM or KB9.

Clone the xXIM repository and switch to the IEC_support branch. Copy the `iecproto.inc` file generated in the previous step. Build using `make IEC_SUPPORT=1`. Burn the `xKIM-0.bin` file to a ROM at offset 0xE000

Clone the KB9 repository and switch to the IEC_support branch. Build with `make`. By default, it is assumed that xkim1541 starts at 0xF000. Modify the `defines_kimiec.s` file if you put it anywhere else. Binary and hex files are generated in the tmp directory, with offset 0x2000. You can build it at a different one editing the `PAGE` variable in the makefile. For example, I built mine at PAGE = 40 (0x4000) because I've got a Visual Memory Card at 0x2000. You can build a prg file with `make prg`, so you can add it to a disk image.

## Usage

Jump to xKIM at addr 0xE000. There are some modified or new commands:

```terminal
C ........... Send a command to the drive
D ........... Disk directory
R ........... Read PRG file from disk
V ........... Verify PRG file on disk
W xxxx xxxx . Write memory to PRG file
```

I f you are familiar with xKIM, they are self-explanatory. If not, see the video. When writing to disk, end address must actually be address of last byte + 1

If you can generate a physical or pi1541 or similar image, make one with `kb9v2.prg` and load using the `R` command. You'll see the address where the program is loaded to. Just jump (`J`) to that address to start MS Basic.

### New and modified BASIC tokens:

* `LOAD` and `SAVE` , without arguments, work the same as the originals: loads and saves the current program from/to tape.
* `LOAD "<FILE>"` and `SAVE "<FILE>"` will load and save file `<FILE>` from/to disk.
* `VERIFY "<FILE>"` will compare the current program in memory against the `<FILE>` program on disk.
* `DIR` will list disk directory contents to screen. The current program in memory is not changed.
* `DCMD "<CMD>"` will send command `<CMD>` to disk. Example:
`DCMD "S0:X*"` will delete (scratch) all files beginning with "X".
