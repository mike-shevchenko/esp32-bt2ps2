# Notes from Mike Shevchenko

---------------------------------------------------------------------------------------------------
## Introduction

These notes describe my successful story of building and flashing this firmware into ESP32.

ATTENTION: The original project was intended for ESP32 with 2MB flash. Its binary releases work
only on such devices. For devices with 4MB flash (like ESP32-WROOM-32), it must be rebuilt form
source.

---------------------------------------------------------------------------------------------------
## Build for ESP32-WROOM-32

To build this project for ESP32-WROOM-32 with 4MB flash (e.g. MH-ET DevKit board) on Windows,
install the Espressif IDF SDK for ESP:
```
REM Clone exactly the v5.3 tag (which is 5.3.0) - the project requires it.
git clone -b v5.3 --recursive https://github.com/espressif/esp-idf.git esp-idf-v5.3

cd esp-idf-v5.3
install.bat

REM Set up the environment variables for this session
export.bat
```

Then go to the project directory and run:
```
idf.py -p COM11 build flash monitor

REM Alternatively, set the port permanently:
export ESPPORT=COM11
```

Releases tested as working are committed to: `release/wroom32_<commit-hash>/`

---------------------------------------------------------------------------------------------------
## Connect to a PS/2 input

Mini-DIN-6 (PS/2) - view to socket:
         0     GND
       6 | 5   CLK  GPIO22
  +5  4  \__3  GND
        2 1    DAT  GPIO23

---------------------------------------------------------------------------------------------------
## Pair with a keyboard

To pair with the Logitech Keys-2-go 2, press and hold the pairing key, then watch the serial output
for a code, then type the code ending with ENTER on the keyboard.

To pair with the Apple A1314 keyboard (which does not support sending the code): press and hold the
Power button on the keyboard until the LED flashes twice in series, then wait for the serial output
to show that it found the keyboard and is waiting for the code, then type `123456 ENTER` on the
keyboard. If the keyboard was paired before, it may need to clear the pairing - remove the
batteries, hold Power for a few seconds, reinstall the batteries.
