# Grids

To flash using the Ardiono UNO as ISP (with the ISP sketch), have to manually wire the pins to the ISP connector so that the RESET pin in also connected. Use the makefile in the Vagrant environment to build the `hex` files.

First time: flash the fuses like this:

```sh
avrdude -b 19200 -V -p m328p -c avrisp -P /dev/arduino-uno-r3 -B 10 -e -u -U efuse:w:0x05:m -U hfuse:w:0xd8:m -U lfuse:w:0xff:m -U lock:w:0x2f:m
```

then flash the actual firmware like this:

```sh
avrdude -B 1 -V -p m328p -c avrisp -P /dev/arduino-uno-r3  -b 19200 -U flash:w:build/grids/grids.hex:i -U flash:w:build/grids_bootloader/grids_bootloader.hex:i -U lock:w:0x2f:m
```

Maybe next time the bootloader can be used and no programmer is needed ?
