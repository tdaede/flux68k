flux68k
=======

The flux68k is an adapter board that allows usage of Gotek floppy drive emulators running [FlashFloppy](https://github.com/keirf/flashfloppy) firmware with the Sharp X68000 line of computers.

Requirements
------------

1. Two Gotek floppy emulators based on the AT32F435 with SFRKC30.AT4.35 PCB revision (sold as FlashFloppy+ compatible).

2. Two USB flash drives.

3. flux68k PCB.

4. DC +5V power supply with a 6x2.1mm center positive barrel jack (unless using auto switch board)

5. Male to male DB37 cable.


Installation
------------

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
-----

Copy floppy images to the USB flash drives and access or boot from them from the X68000. More detailed information on using FlashFloppy can be found at (FlashFloppy's documentation)[https://github.com/keirf/flashfloppy/wiki].

Notes
-----

* XDF images must be renamed to have the .img extension.

* Many applications do not boot correctly from drives 2-3. For these, the rear switch must be set to drives 0-1, and the X68000's internal drives disconnected (unless the auto switch board is used, see below). On compact models, there is a switch on the back of the X68000 to switch the internal drive assigments to 2-3.

* The flux68k must be powered when attached to the X68000 or floppies may not read correctly.

* FlashFloppy currently ignores the motorized eject signal, so the floppy must be manually ejected (by pushing the rotary knob) if an application tries to automatically eject a floppy.

Auto switch board
=================

Optionally, a mod can be installed on non-compact models to automatically switch the internal floppy drive assignments. In addition, this board will also supply power to the external floppy emulators, so that an external power supply is not needed.

Requirements
------------

1. Auto switcher board

2. 34 pin IDC cable, at least 20cm Long

3. +5V internal power cable, either a [Molex to berg connector cable](https://www.crystalfontz.com/product/wrpwry12-four-pin-power-splitter-cable) or a custom made cable that attaches to one of the 3 pin berg connections for the floppy drives or HDD.

Installation
------------

1. Remove the left panel of the X68000.

2. Disconnect the SCSI cable from the external SCSI connector PCB, if present.

3. Disconnect the floppy cable from the external floppy connector PCB.

4. Unscrew and remove the SCSI/floppy connector module via the two plastic tapping screws holding it in place.

5. Remove the SCSI connector PCB from the module by removing the two machine screws holding it in place.

6. Remove the floppy connector PCB from the mdoule by removing the two machine screws holding it in place. Note the relative positions of the bracket and EMI shielding.

7. Attach the new 34 pin IDC cable to the "MB" connector on the auto switcher PCB.

8. Attach the +5V power cable to the swapper PCB.

9. Install the auto switcher PCB on the original metal bracket / EMI shield using the two machine screws.

10. Install the SCSI connector board (if present) on top of the swapper PCB with two machine screws.

11. Install the external connector module back into the X68000 using the two plastic tapping screws.

12. Attach the +5V cable to the appropriate location (the molex connector if using a molex to berg cable).

13. Connect the existing 34 pin floppy IDC cable coming off of the floppy drives to the "FD" connector on the swapper PCB.

14. Disconnect the other end of the existing 34 pin floppy IDC cable from the motherboard connector at the base of the X68000. Leave this disconnected inside the machine.

15. Connect the other end of the new 34 pin IDC cable (connected to the "MB" connector on the switcher PCB) to the motherboard connector at the base of the X68000.

16. Reinstall the left panel of the X68000.

Notes
-----

* The auto switcher PCB uses the previously unused pin 3 of the 37-pin connector as the switch signal. When left floating or high, it switches the internal drives to 0-1. When pulled low, it switches the internal drives to 2-3.

* The auto swticher PCB uses unused pins 18 and 19 of the 37-pin connector to send +5V power to the external floppy emulator. Each pin is protected by a 250mA PTC fuse.
