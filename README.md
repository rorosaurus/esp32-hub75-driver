# Drive HUB75 LED panels using an ESP32-DEVKIT-V1 and SmartMatrix library
[![Demo](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/demo.gif)](https://www.youtube.com/watch?v=UengvMiGzF8)

# [Buy this PCB on Tindie! ![I sell on Tindie](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/tindie.png)](https://www.tindie.com/products/18357/)

## Features

* Compatible with [SmartMatrix](https://github.com/pixelmatix/SmartMatrix/tree/teensylc) and [FastLED](https://github.com/FastLED/FastLED) libraries!
  * Play animated .gifs on your LED panel using [Marc Merlin's AnimatedGIFs sketch](https://github.com/marcmerlin/AnimatedGIFs)!
  * Animate scrolling text (and more!) using [SmartMatrix's FeatureDemo](https://github.com/pixelmatix/SmartMatrix/tree/teensylc/examples/FeatureDemo)!
* ESP32 provides 2.4GHz Wifi/Bluetooth capability, and is Arduino compatible!
* The PCB connects all 16 pins needed to drive HUB75 panels using [`ESP32_FORUM_PINOUT`](https://github.com/pixelmatix/SmartMatrix/blob/teensylc/src/MatrixHardware_ESP32_V0.h#L37) from SmartMatrix library.
  * Compatible with 1/8, 1/16, and 1/32 scan type HUB75 panels.
  * Supports multiple HUB75 panels daisy-chained in series!
  * There is no logic level shifter, so this is only compatible with 3.3V tolerant LED panels. (I haven't found a panel that doesn't work yet!)
* [Two different ways to connect to your LED panel](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/ASSEMBLY.md#step-1-mount-output-connector-onto-the-pcb):
  * Output Mode 0: directly plug this PCB into your LED panel using 2x8 female pin headers.
  * Output Mode 1: connect this PCB to your LED panel via 16 pin IDC socket (ribbon cable not included).
* 3x5 = 15 pins broken out for additional use: 
  * 3x `GND`
  * 3x `3.3V`
  * 9x GPIO pins (8 with ADC!): for buttons, potentiometers, sensors, etc.!
* Optional two screw terminals to manage `5V` power flow between ESP32 and your LED panels.
* Optional pads for one through-hole Electrolytic Capacitor (I use 1000uF) to smooth the `5V` power.
* Optional pads for one 1206 SMD Ceramic Capacitor (I use 10uF) to enable the automatic bootloader. No need to press buttons to upload new firmware!

## Example Projects
* [FurretTotem](https://ravefurret.com/): HE WALK! This cute little guy just keeps on walking.
* [Project Mc2 LED Purse](https://github.com/rorosaurus/project-mc2-led-purse): Cheap children's toy you can harvest a good beginner panel from!

## Assembly Instructions
Some assembly required! (Soldering ~46 pins.) Full assembly instructions and more detailed information can be found here: [`ASSEMBLY.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/ASSEMBLY.md)

## Hardware (BOM)
For a list of required and optional components, please see [`HARDWARE.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/HARDWARE.md)

## Software
For links to software I recommend using with this board, please see [`SOFTWARE.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/SOFTWARE.md)

Please note: my shield works with [SmartMatrix](https://github.com/pixelmatix/SmartMatrix/tree/teensylc) library, not [PxMatrix](https://github.com/2dom/PxMatrix).

## Powering your project
To find out the best way to power your ESP32 and LED panels, please head over to my power document: [`POWER.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/POWER.md)!

## PCB Design
Latest board revision is v1.1.

See [`CHANGELOG.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/CHANGELOG.md) for information about board revisions and high resolution renders of the board.

Schematic download (EasyEDA source): [`/gerber/esp32-hub75-driver-schem.json`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/gerber/esp32-hub75-driver-schem.json)

Gerber file download: [`/gerber/esp32-hub75-driver.zip`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/gerber/esp32-hub75-driver.zip)

## FAQ
I plugged everything in, and I don't see anything on my LED panel!
* Is your code configured correctly? Right pinout? Right panel size, scantype, etc.?
* Is the PCB plugged into the panel correctly?  It's possible to accidently plug in 1 pin too high or too low on the panel input. Check it is properly inserted and each pin aligns properly.
