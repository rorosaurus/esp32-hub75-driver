# Software

## Drivers
The ESP32 cannot directly communicate over USB with your computer to reprogram itself. It [uses an onboard chip](https://docs.espressif.com/projects/esp-idf/en/latest/get-started/establish-serial-connection.html) (specifically, SiLab's `CP2102`) to do so, which requires you to install a driver. You only need to install the `CP210X` driver for your appropriate operating system. This step might not be necessary on Windows 10.

[Download the driver here](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

## Programs
I would recommend using the following software with this board:
* [Arduino IDE](https://www.arduino.cc/en/Main/Software) to code and program everything!
  * [Follow the instructions here](https://github.com/espressif/arduino-esp32) to install board manager support for ESP32!
* If you'd prefer not to use the Arduino IDE, you should be able to use all the below libraries and sketches in [PlatformIO](https://platformio.org/) on [Visual Studio Code](https://platformio.org/platformio-ide) using [this board configuration](https://docs.platformio.org/en/latest/boards/espressif32/esp32doit-devkit-v1.html).

## Making animated .gifs
Use your preferred image editor to make your animated .gifs! I used Photoshop, but you could also use GIMP or something! I can also recommend [Aseprite](https://www.aseprite.org/)! In a pinch, you can use websites to convert things to a .gif, but you have much less control over things like compression, color tables, etc.

## Libraries
You'll need to install (by downloading, renaming the folder to remove `-master`, and copying to `My Documents/Arduino/libraries`) a few libraries to drive your LED panels:
* https://github.com/pixelmatix/SmartMatrix/tree/teensylc
  * Please note: This is a specific branch of SmartMatrix. ESP32 support *only exists* in this branch.
* https://github.com/adafruit/Adafruit-GFX-Library
* https://github.com/marcmerlin/Framebuffer_GFX
* https://github.com/FastLED/FastLED
* https://github.com/marcmerlin/SmartMatrix_GFX

If you want to use Wifi, you will need to install additional libraries:
* https://github.com/me-no-dev/AsyncTCP
* https://github.com/me-no-dev/ESPAsyncWebServer

## Uploading .gifs
The gifs are loaded onto the ESP32's SPIFFS: an integrated filesystem that shares the same flash memory as your program.  You have 4MB shared between the GIFs and your program code. Edit your own gifs using Photoshop or some other editor, then use [this Arduino IDE plugin](https://github.com/me-no-dev/arduino-esp32fs-plugin) to upload .gifs to your ESP32 via the Arduino IDE!

Install that plugin by following the instructions from that repository page. You'll need to **make sure Serial Monitor is closed** before you upload using this, or you'll get an error.

Keep in mind that SPIFFS can't handle long-ish filenames. If a file fails to get bundled and appear on your ESP32, first shorten the filename and try again. Still not working? Is the file too large? Did you resize it properly for the display? Sometimes I forget to do that too. :)

## Uploading Sketches
Some ESP32 dev boards require you to hold the BOOT button for ~3s to connect during sketch upload. If you're using my PCB and you have attached the auto-bootloader capacitor, you don't need to worry about this!

If you're using my PCB, when uploading to the board via Arduino IDE, please use the board: `DOIT ESP32 DEVKIT V1` and use this programmer: `USBtinyISP`. You could also use the generic `ESP32 Dev Module` if you want to partition more space for SPIFFS.

**Make sure you use a data+charging USB cable to program your ESP32! A charging-only cable won't work!**

## Important Sketch Variables
Keep in mind, at a minimum you'll need to tweak some variables to match your LED panel's parameters:
* In `neomatrix_config.h`:
  * LED panel size - `kMatrixWidth = 32;`, `kMatrixHeight = 16;` replace with your width and height in pixels
  * Scantype - `kPanelType = SMARTMATRIX_HUB75_16ROW_MOD8SCAN;` for 1/8 scan, or `SMARTMATRIX_HUB75_32ROW_MOD16SCAN` for 1/16 scan panels, or `SMARTMATRIX_HUB75_64ROW_MOD32SCAN` for 1/32 scan panels
  * Pinout - `#define GPIOPINOUT ESP32_FORUM_PINOUT` place this somewhere near the top of your sketch!
* In `animatedgif_config.h`:
  * GIF size - `#define gif_width 32`, `#define gif_height 16` replace with your maximum size for GIF decoding

You might need to adjust some other options as well for your specific use case. I recommend reading [SmartMatrix's official documentation](http://docs.pixelmatix.com/SmartMatrix/library.html) for all the options available to you. Sometimes I have found this documentation to be lacking or out-of-date, in which case I would encourage you to look at the source code for SmartMatrix itself to see what methods are available for you to use.

For example, if you search the source code, you can find references to "rotation" in `SmartMatrix_Impl.h`. There on line 354 you can see that we can rotate the display by calling `matrix->setRotation(rotation90);` or similar.

## Example Sketches
* [Project Mc2 LED Purse](https://github.com/rorosaurus/project-mc2-led-purse) - A small repository of a few basic sketches I've constructed to make your introduction as easy as possible! Works with a very cheap display.
  * [FeatureDemo](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/FeatureDemo) - The demo of SmartMatrix features, straight from the SmartMatrix example sketches! I've lightly modified it to remove a couple demos that get VERY bright and might use too much power. However there's still a couple that are pretty blinding - be careful!
  * [MultipleTextLayers](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/MultipleTextLayers) - Lightly modified example sketch from the SmartMatrix example library. Perfect for a minimal sketch that displays scrolling text!
  * [SimpleGifExample](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/SimpleGifExample) - This is the bare minimum Arduino sketch that will display a gif you specify on the display.  
  * [AnimatedGIFs](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/AnimatedGIFs) - This is a more complicated sketch that loops between all gifs in the specified folder on SPIFFS.
  * [WifiControlledGIFs](https://github.com/rorosaurus/project-mc2-led-purse/tree/master/WifiControlledGIFs) - This builds on AnimatedGIFs sketch to add a simple wifi server to switch between gifs and control brightness! Note this requires more memory, so it might not work on larger displays (like 128x64.. sorry [Furret](https://github.com/rorosaurus/FurretTotem)!)
* [marcmerlin/AnimatedGIFs](https://github.com/marcmerlin/AnimatedGIFs) - This code is where I started. It's a good starting point for your program, if you don't like the simplified code in the LED Purse repository. It uses the above software and libraries to playback animated .gifs for you! You can easily adjust things like the time between switching .gifs. 
* [captive-wifi-remote](https://github.com/rorosaurus/captive-wifi-remote) - The basic guts of a simple webserver to control your panel.
* You can also find some example sketches for Wifi/Bluetooth/etc. in your Arduino IDE after installing ESP32 support and all your libraries! Example sketches are a great place to start to learn how to use some features!

## Daisy Chaining LED Panels
You can daisy-chain HUB75 LED panels by plugging an output connector into the next panel's input. Copying SmartMatrix's README below for your convenience.

New with SmartMatrix Library 3.0, you can chain several panels together to create a wider or taller display than one panel would allow.  Set `kMatrixWidth` and `kMatrixHeight` to the overall width and height of your display.  If your display is more than one panel high, set `kMatrixOptions` to how you tiled your panels:  

* Panel Order - By default, the first panel of each row starts on the same side, so you need a long ribbon cable to go from the last panel of the previous row to the first panel of the next row.  `SMARTMATRIX_OPTIONS_C_SHAPE_STACKING` inverts the panel on each row to minimize the length of the cable going from the last panel of each row the first panel of the other row.  
* Panel Direction - By default the first panel is on the top row.  To stack panels the other way, use `SMARTMATRIX_OPTIONS_BOTTOM_TO_TOP_STACKING`.  
* To set multiple options, use the bitwise-OR operator e.g. C-shape Bottom-to-top stacking: `const uint8_t kMatrixOptions = (SMARTMATRIX_OPTIONS_C_SHAPE_STACKING | SMARTMATRIX_OPTIONS_BOTTOM_TO_TOP_STACKING);`

## DMA-capable memory
The number of pixels you can drive is limited primarily by the amount of DMA-capable memory on your ESP32. This affects the size of your display(s) you can drive effectively, their color palette, how long animations can be, etc. There does not appear to be an exact science to this, or I would offer an easy formula for you.

Note: Wifi also uses some amount of DMA-capable memory.

At any time in your program, you can check how much DMA-capable memory is free using this code snippet:

````
Serial.print("8-bit/DMA Memory Available: ");
Serial.println(heap_caps_get_free_size(MALLOC_CAP_DMA));
````
