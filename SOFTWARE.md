# Software

## Drivers
The ESP32 cannot directly communicate over USB with your computer to reprogram itself. It [uses an onboard chip](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/establish-serial-connection.html) (specifically, SiLab's `CP2102`) to do so, which requires you to install a driver. You only need to install the `CP210X` driver for your appropriate operating system.

[Download the driver here](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

## Programs
I would recommend using the following software with this board:
* https://www.arduino.cc/en/Main/Software - The Arduino IDE, to program everything!
  * https://github.com/espressif/arduino-esp32 - Install board manager support for ESP32
  * https://github.com/me-no-dev/arduino-esp32fs-plugin - This Arduino IDE plugin makes it simple to upload .gifs to your ESP32
* If you'd prefer not to use the Arduino IDE, you should be able to use all the below libraries and sketches in [PlatformIO](https://platformio.org/) on [Visual Studio Code](https://platformio.org/platformio-ide) using [this board configuration](https://docs.platformio.org/en/latest/boards/espressif32/esp32doit-devkit-v1.html).
* Use your preferred image editor to make your animated .gifs! I used Photoshop, but you could also use GIMP or something!

## Libraries
You'll need to install (by downloading, renaming the folder to remove `-master`, and copying to `My Documents/Arduino/libraries`) a few libraries to drive your LED panels:
* https://github.com/pixelmatix/SmartMatrix/tree/teensylc
  * Please note, this is a specific branch of SmartMatrix. ESP32 support only exists in this branch.
* https://github.com/adafruit/Adafruit-GFX-Library
* https://github.com/marcmerlin/Framebuffer_GFX
* https://github.com/FastLED/FastLED
* https://github.com/marcmerlin/SmartMatrix_GFX

If you want to use Wifi, you will need to install additional libraries:
* https://github.com/me-no-dev/AsyncTCP
* https://github.com/me-no-dev/ESPAsyncWebServer

## GIFs
The gifs are loaded onto the ESP32's SPIFFS: an integrated filesystem that shares the same flash memory as your program.  You have 4MB shared between the GIFs and your program code. Edit your own gifs using Photoshop or some other editor, then use [this Arduino IDE plugin](https://github.com/me-no-dev/arduino-esp32fs-plugin) to upload .gifs to your ESP32 via the Arduino IDE!

## Example Sketches
Keep in mind you'll need to tweak some variables to match your LED panel's parameters:
* LED panel size - `kMatrixWidth = 32;`, `kMatrixHeight = 16;` replace with your width and height in pixels
* Scantype - `kPanelType = SMARTMATRIX_HUB75_16ROW_MOD8SCAN;` for 1/8 scan, or `SMARTMATRIX_HUB75_32ROW_MOD16SCAN` for 1/16 scan panels, or `SMARTMATRIX_HUB75_64ROW_MOD32SCAN` for 1/32 scan panels
* Pinout - `#define GPIOPINOUT ESP32_FORUM_PINOUT` place this somewhere near the top of your sketch!

Note: some ESP32 dev boards require you to hold the BOOT button for ~3s to connect during sketch upload. If you're using my PCB and you have attached the auto-bootloader capacitor, you don't need to worry about this!

If you're using my PCB, when uploading to the board via Arduino IDE, please use the board: `DOIT ESP32 DEVKIT V1`.

* [Project Mc2 LED Purse](https://github.com/rorosaurus/project-mc2-led-purse) - A small repository of a few basic sketches I've constructed to make your introduction as easy as possible! Works with a very cheap display.
  * [FeatureDemo](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/FeatureDemo) - The demo of SmartMatrix features, straight from the SmartMatrix example sketches! I've lightly modified it to remove a couple demos that get VERY bright and might use too much power. However there's still a couple that are pretty blinding - be careful!
  * [MultipleTextLayers](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/MultipleTextLayers) - Lightly modified example sketch from the SmartMatrix example library. Perfect for a minimal sketch that displays scrolling text!
  * [SimpleGifExample](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/SimpleGifExample) - This is the bare minimum Arduino sketch that will display a gif you specify on the display.  
  * [AnimatedGIFs](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/AnimatedGIFs) - This is a more complicated sketch that loops between all gifs in the specified folder on SPIFFS.
  * [WifiControlledGIFs](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/WifiControlledGIFs) - This builds on AnimatedGIFs sketch to add a simple wifi server to switch between gifs and control brightness! Note this requires more memory, so it might not work on larger displays (like 128x64.. sorry [Furret](https://github.com/rorosaurus/FurretTotem)!)
* [marcmerlin/AnimatedGIFs](https://github.com/marcmerlin/AnimatedGIFs) - This code is where I started. It's a good starting point for your program, if you don't like the simplified code in the LED Purse repository. It uses the above software and libraries to playback animated .gifs for you! You can easily adjust things like the time between switching .gifs. 
* [captive-wifi-remote](https://github.com/rorosaurus/captive-wifi-remote) - The basic guts of a simple webserver to control your panel.
* You can also find some example sketches for Wifi/Bluetooth/etc. in your Arduino IDE after installing ESP32 support and all your libraries! Example sketches are a great place to start to learn how to use some features!