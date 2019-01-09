# Fun with MicroPython on an ESP32 microcontroller

We are going to use the [official MicroPython] implementation, with no
extended libraries and trying to keep it as pure as possible. The whole idea
of MicroPython is to be essencially minimal, open to be extended at will, but
only when really needed. When the need raises, of course new extensions will
be coded or used according to the case.

The MicroPython docs can be found [here][MicroPython docs].


## The ESP32 boards

The ESP32 chips I currently have to play are development boards and have the
following specs:

```
$ esptool.py flash_id
esptool.py v2.5.1
Found 1 serial ports
Serial port /dev/ttyUSB0
Connecting....
Detecting chip type... ESP32
Chip is ESP32D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse
MAC: xx:xx:xx:xx:xx:xx
Uploading stub...
Running stub...
Stub running...
Manufacturer: ef
Device: 4016
Detected flash size: 4MB
Hard resetting via RTS pin...
```


## Tools and setup

I'm using a Linux machine (Debian Stretch) with Python installed. It can be
any modern version after 2.7 or 3.6. It should be no problem getting them
installed from the official repos.

Using `pip` we need to install `esptool.py` and `adafruit-ampy`. They will be
very useful interacting with the board:

    $ pip install --user esptool adafruit-ampy

To avoid running the commands as root all the time, add your own user to the
`dialout` group:

    $ sudo usermod -a -G dialout <username>

To connect to the board via REPL, `screen` is an option. The connection is
done by passing the board "port" (the TTY device) and the baud rate (normally
115200) using the following command (replace `X` by the port number):

    $ screen /dev/ttyUSBX 115200


## Flashing the ESP32

The MicroPython image used to flash this chip came from here:

http://micropython.org/resources/firmware/esp32-20190109-v1.9.4-773-gafecc124e.bin

Here is how to do it:

    $ esptool.py --port /dev/ttyUSB0 write_flash \
        --flash_size 4MB \
        --compress \
        0x1000 esp32-20190105-v1.9.4-773-gafecc124e.bin


[official MicroPython]: https://github.com/micropython/micropython
[MicroPython docs]: https://docs.micropython.org/en/latest/
