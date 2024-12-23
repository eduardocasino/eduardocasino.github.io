---
title: TI/National Bipolar PROM Programmer
date: 2024-09-28 19:03:00 +0100
last_modified_at: 2024-12-23 00:00:00 +0100
categories: [Hardware, Arduino]
image: /assets/img/posts/2024-09-28-TI-National-Bipolar-PROM-Programmer/preview.png
tags: [kim-1, mtu, k-1013, prom, programmer, arduino]     # TAG names should always be lowercase
math: true
---
> **Update:** Arduino sketch and programmer utility finished. The programmer is now completely functional.
{: .prompt-info }

The [K-1013 Floppy Disk Controller](/posts/K-1013-Replica-completed/) uses an optional (and obsolete) 256x8 bit, 20 pin PROM to be able to boot the OS from disk. There were many variants that were pin-compatible for reading, but that required different and incompatible programming methods that, however, have something in common: They are not supported by modern, cheap programmers.

I was able to find a few 74s471 on e-bay, but my search for a suitable programmer only yielded options that cost many hundreds of euros.

So, based on [this design of a PROM programmer](https://theoddys.com/acorn/replica_boards/tesla_prom_programmer_board/tesla_prom_programmer_board.html) for the ACORN by Chris Oddy, I designed a poor man's TI/National Semiconductor Bipolar PROM programmer shield for the Arduino Mega and should as well burn other 256x8 and 512x8 bit PROMs from TI and Tesla.

According to [the datasheet](/assets/files/posts/2024-09-28-TI-National-Bipolar-PROM-Programmer/National-Schottky-PROMs.pdf), the programming procedure is as follows:

1. Apply a supply voltage (V<sub>cc</sub>) of 5 V and address the word to be programmed.
2. Verify that the bit location needs to be programmed. If not, proceed to the next bit.
3. If the bit requires programming, disable the outputs by applying a high-logic-level voltage to the chip-select input(s).
4. Only one bit location is programmed at a time. Connect each output not being programmed to 5V through a 3.9 kΩ resistor and connect the output to be programmed to ground. Maximum current out of the programming output supply during programming is 150 mA.
5. Step V<sub>cc</sub> to 10.5 V nominal. Maximum supply current required during programming is 750 mA.
6. Apply a low-logic-level voltage to the chip·select input(s). This should occur between 10 μS and 1 ms after V<sub>cc</sub> has reached its 10.5 V level.
7. After the programming pulse time (1 to 10 ms) is reached, a high logic level is applied to the chip-select inputs to disable the outputs.
8. Within 10 μs to 1 ms after the chip-select input(s) reach a high logic level, V<sub>cc</sub> should be stepped down to 5 V, at which level veritication can be accomplished.
9. The chip-select input(s) may be taken to a low logic level (to permit program verification) 10 μS or more after V<sub>cc</sub> reaches its steady-state value of 5 V.
10. At a programming pulse duty cycle of 35% or less, repeat steps 1 through 8 for each output where it is desired to program a bit.

The 74s471 is supplied with all bit locatlons containing low logic level (0) and programming a bit changes the output of that bit to high logic level.

So, the programmer's hardware must be capable of:

* Powering on/off the prom.
* Addressing each of the prom's locations.
* Reading each location contents.
* Connecting each bit line to ground or to a 3.9 kΩ pullup.
* Controlling the prom's select line(s).
* Applying a 10.5V pulse to the prom's V<sub>cc</sub>.

![schematic-1](/assets/img/posts/2024-09-28-TI-National-Bipolar-PROM-Programmer/schematic-1.png){: width="250" .right }
Chris' design is very clever. It uses a boost converter which output voltage is set based on a voltage divider formed by R<sub>2</sub> and R<sub>3</sub> when the transistor Q<sub>1</sub> is off. According to the datasheet, $$ V_{out} = (\frac{R_{3}}{R_{2}} + 1)\times1.23 = 5.01 V $$. When the transistor is on, R<sub>4</sub> is added in parallel to R<sub>2</sub>, which yields an equivalent value of $$ R_{eq} = \frac{R_{2} \times R_{4}}{R_{2} + R_{4}} = 15.95 kΩ $$, so the new output voltage is $$ V_{out} = (\frac{R_{3}}{R_{eq}} + 1)\times1.23 = 10.48 V $$. This way, we can generate the programming pulse just controlling Q<sub>1</sub>.

The [rest of the circuit](https://github.com/eduardocasino/TI-Bipolar-PROM-programmer-shield/blob/main/hardware/docs/TI-Bipolar-PROM-programmer-shield.pdf) is very straightforward, with a mosfet controlling power on/off, eight transistors that connect each bit pin to ground or the 3.9 kΩ pullups, and a couple of open-collector buffers. I've opted for an SMD design, whith sizes big enough so they can be soldered manually:

![img-description](/assets/img/posts/2024-09-28-TI-National-Bipolar-PROM-Programmer/programmer.jpg)

The sketch for the firmware has been developed from scratch, following the PROM's datasheet. It implements basic one-letter commands through the serial inteface, which are controlled by the programmer's command line utility (sorry, only for Unix-like OS. On Windows, use the Windows Subsystem for Linux).

You can find everything to build your own, including the programmer utility, [in my GitHub repository](https://github.com/eduardocasino/TI-Bipolar-PROM-programmer-shield).

### Programmer's usage

> **Warning:** During programming, the power comsumption goes well over 5W. I had a lot of stability problems until I realised that the USB connection was not providing enough juice, so you need to supply at least 10W to the Arduino through the barrel connector. I'm using a 12V, 1A adapter that I had lying around.
{: .prompt-warning }

On WSL, first make sure that you [attach the USB device to the Linux susbsystem](https://learn.microsoft.com/en-us/windows/wsl/connect-usb#attach-a-usb-device).

```plaintext
Usage: prom [-h]
       prom DEVICE [-c NUM] -b
       prom DEVICE [-c NUM] -r [ADDRESS [-n COUNT] | -o FILE [-f FORMAT]]
       prom DEVICE [-c NUM] {-w|-s|-v} {ADDRESS -d STRING | -i FILE [-f FORMAT]}

Arguments:
   DEVICE                   Serial device.

Options:
   -h[elp]                  Show this help message and exit.
   -c[hip]      NUM         Chip to program: 0 == 74s471 (default), 1 == 74s472.
   -b[lank]                 Do a whole chip blank test.
   -r[ead]      [ADDRESS]   Read chip. If ADDRESS is specified, read just that
                            byte. If not, do a hexdump of the chip contents to
                            the screen or, if an output file name is provided,
                            dump the contents with the format specified by the
                            -format option.
   -n[um-bytes] [COUNT]     Number of bytes to read. Defaults to the whole chip
                            size.
   -w[rite]     [ADDRESS]   Program chip. If ADDRESS is provided, program
                            beginning at that location with data specified with
                            the -data option. If not, an input filename must be
                            specified.
   -s[imulate]  [ADDRESS]   Program simulation. Will success of fail as the write
                            command, but without actually burning the chip.
   -v[erify]    [ADDRESS]   Verify data. Same options as for -write|-simulate.
   -d[ata]      STRING      Binary string to program, simulate or verify. Can
                            contain hex and oct escaped binary chars.
   -i[nput]     FILE        File to read the data from.
   -o[utput]    FILE        File to save the data to.
   -f[ormat]    {bin,ihex}  File format. Defaults to bin.

Note: Long and short options, with single or dual '-' are supported
```
{: file="Usage" }

#### Blank test command

Makes a quick blank test of the whole chip.

Example:

```bash
$ prom /dev/ttyUSB0 -b
Connected to programmer, firmware V01.00.00.
Chip is not blank. Found non-zero data at address 0x0.
```
{: .nolineno }

#### Read command

`prom DEVICE -r`, without any more arguments, does a hexadecimal dump to the screen:

```bash
$ ./prom /dev/ttyUSB0 -r
Connected to programmer, firmware V01.00.00.
000  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff ff ff  |................|
010  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff ff ff  |................|
020  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff ff ff  |................|
030  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff ff ff  |................|
040  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff ff ff  |................|
050  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff ff ff  |................|
060  01 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
070  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
080  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
090  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
0A0  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
0B0  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
0C0  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
0D0  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
0E0  00 00 00 00 00 00 00 00  ff ff ff ff ff ff ff ff  |................|
0F0  ff ff ff ff ff ff ff ff  ff ff 1c 1c 00 ff 1f 1c  |................|
100
```
{: .nolineno }

If an address is provided, the content from that cell and onwards is printed to the screen:

```bash
$ ./prom /dev/ttyUSB0 -r 0xec
Connected to programmer, firmware V01.00.00.
0EC  ff ff ff ff ff ff ff ff  ff ff ff ff ff ff 1c 1c  |................|
0FC  00 ff 1f 1c                                       |....            |
```
{: .nolineno }

Finally, it is also possible to make a dump in binary or Intel HEX format with the `-o FILE` and `-f {bin|ihex}` options, If not specified, `bin` is the default:

```bash
$ ./prom /dev/ttyUSB0 -r -f ihex -o test.hex
Connected to programmer, firmware V01.00.00.
Writing contents to file `test.hex` in ihex format.

$ cat test.hex
:20000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF00
:20002000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFE0
:20004000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFC0
:2000600001000000000000000000000000000000000000000000000000000000000000007F
:20008000000000000000000000000000000000000000000000000000000000000000000060
:2000A000000000000000000000000000000000000000000000000000000000000000000040
:2000C000000000000000000000000000000000000000000000000000000000000000000020
:2000E0000000000000000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF1C1C00FF1F1CA0
:00000001FF
```
{: .nolineno }

#### Write and Simulate Write commands

`prom DEVICE -w ADDRESS -d DATA` programs the cells beginning at address `ADDRESS` with the `DATA` binary string:

```bash
$ ./prom /dev/ttyUSB0 -w 0x60 -d '\x01\x02'
Connected to programmer, firmware V01.00.00.
WARNING: Programming is irreversible. Are you sure? Type YES to confirm
YES
Writing
..
Success.
```
{: .nolineno }

`prom DEVICE -w -f {bin|ihex} -i FILE` programs the chip with the contents of the `FILE` file. Working with `bin` and `ihex` have different implications:

* If a binary file is specified, the chip is programmed starting at address `0x000` up to the size of the file or the chip, whichever is smaller.
* With an Intel HEX file, only the addresses specified in the file are programmed.

```bash
$ ./prom /dev/ttyUSB0 -w -i test.bin
Connected to programmer, firmware V01.00.00.
WARNING: Programming is irreversible. Are you sure? Type YES to confirm
YES
Writing
.........................................................................
.......................
Success.
```
{: .nolineno }

Command `-s` works exactly the same as `-w`, but without burning the chip. It is strongly suggested to execute first a simulation as it helps to catch errors beforehand:

```bash
$ ./prom /dev/ttyUSB0 -s -f bin -i test2.bin
Connected to programmer, firmware V01.00.00.
Performing a write simulation
..........................................................
Error writing (simulated) to prom address 0x039: Read == 0xff, expected == 0x03
```
{: .nolineno }

#### Verify command

The verify command just checks the contents of the PROM against the data provided. It has the same options as the Write and Simulate write commands:

```bash
$ ./prom /dev/ttyUSB0 -v -f bin -i test2.bin
Connected to programmer, firmware V01.00.00.
Verifying
..........................................................
Error verifying prom address 0x039: Read == 0xff, expected == 0x03

$ ./prom /dev/ttyUSB0 -v -f ihex -i test.ihex
Connected to programmer, firmware V01.00.00.
Verifying
.........................................................................
.........................................................................
.........................................................................
.....................................
Success.
```
{: .nolineno }

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
