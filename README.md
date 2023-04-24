flux68k
=======

The flux68k is an adapter board that allows usage of Gotek floppy drive emulators running [FlashFloppy](https://github.com/keirf/flashfloppy) firmware with the Sharp X68000 line of computers.

Requirements
============

1. Two Gotek floppy emulators based on the AT32F435 with SFRKC30.AT4.35 PCB revision (sold as FlashFloppy+ compatible).

2. Two USB flash drives.

3. flux68k PCB.

4. DC +5V power supply with a 6x2.1mm center positive barrel jack.

5. Male to male DB37 cable.


Installation
============

1. Set the jumpers on each of the Gotek emulators to S0 and MOR.

2. Install the emulators into the flux68k PCB, being careful to line up the power connectors.

3. Plug in the +5V power supply and ensure that both emulators power on.

4. Build the following branch of FlashFloppy, and flash it to to the Gotek. https://github.com/keirf/flashfloppy/pull/781

5. Copy the [example FF.CFG](https://github.com/keirf/flashfloppy/blob/a0a06fc15bd6ab05d6b62a67390bd5e57fd1853e/examples/FF.CFG) to each of the USB sticks and change the pin02 line to:
``` ini
pin02 = in
```

6. Set the switch on the back of the flux68k to drives 2-3.

7. Plug in the DB37 cable between the X68000 and the flux68k.

Usage
=====

Copy floppy images to the USB flash drives and access or boot from them from the X68000. More detailed information on using FlashFloppy can be found at (FlashFloppy's documentation)[https://github.com/keirf/flashfloppy/wiki].

Notes
=====

* XDF images must be renamed to have the .img extension.

* Many applications do not boot correctly from drives 2-3. For these, the rear switch must be set to drives 0-1 and the physical drives of the X68000 must be disconnected (or a floppy swapper board used).

* The flux68k must be powered when attached to the X68000 or floppies may not read correctly.

* FlashFloppy currently ignores the motorized eject signal, so the floppy must be manually ejected (by pushing the rotary knob) if an application tries to automatically eject a floppy.
