# Software

## Programs
I would recommend using the following software with this board:
* https://www.arduino.cc/en/Main/Software - The Arduino IDE, to program everything!
  * https://github.com/espressif/arduino-esp32 - Install board manager support for ESP32
  * https://github.com/me-no-dev/arduino-esp32fs-plugin - This Arduino IDE plugin makes it simple to upload .gifs to your ESP32
* Use your preferred image editor to make your animated .gifs! I used Photoshop, but you could also use GIMP or something!

## Libraries
You'll need to install (by downloading, renaming the folder to remove `-master`, and copying to `My Documents/Arduino/libraries`) a few libraries to drive the LED panel:
* https://github.com/pixelmatix/SmartMatrix/tree/teensylc
  * Please note, this is a specific branch of SmartMatrix. ESP32 support only exists in this branch.
* https://github.com/adafruit/Adafruit-GFX-Library
* https://github.com/marcmerlin/Framebuffer_GFX
* https://github.com/FastLED/FastLED
* https://github.com/marcmerlin/SmartMatrix_GFX

If you want to use Wifi, you will need to install additional libraries:
* https://github.com/me-no-dev/AsyncTCP
* https://github.com/me-no-dev/ESPAsyncWebServer

## Sketches
Keep in mind you'll need to tweak some variables to match your LED panel size, scanrate, etc.
* https://github.com/rorosaurus/project-mc2-led-purse - A small repository of a few basic sketches I've constructed to make your introduction as easy as possible! Works with a very cheap display.
* https://github.com/marcmerlin/AnimatedGIFs - This code is a good starting point for your program. It uses the above software and libraries to playback animated .gifs for you! You can easily adjust things like the time between switching .gifs. 
* https://github.com/rorosaurus/captive-wifi-remote - The basic guts of a simple webserver to control your panel.