# Software
I would recommend using the following software with this board:
* https://www.arduino.cc/en/Main/Software - The Arduino IDE, to program everything!
  * https://github.com/espressif/arduino-esp32 - Install board manager support for ESP32
  * https://github.com/me-no-dev/arduino-esp32fs-plugin - This Arduino IDE plugin makes it simple to upload .gifs to your ESP32
* https://github.com/marcmerlin/AnimatedGIFs - This code is a good starting point for your program. It uses the above software and libraries to playback animated .gifs for you! You can easily adjust things like the time between switching .gifs. You'll need to install (by downloading and copying to `My Documents/Arduino/libraries`) a few libraries that it uses:
  * https://github.com/pixelmatix/SmartMatrix/tree/teensylc
  * https://github.com/adafruit/Adafruit-GFX-Library
  * https://github.com/marcmerlin/Framebuffer_GFX
  * https://github.com/FastLED/FastLED
  * https://github.com/marcmerlin/SmartMatrix_GFX
* Use your preferred image editor to make your animated .gifs! I used Photoshop, but you could also use GIMP or something!


For a simple sketch that works with a cheap display, please see my [Project Mc2 LED Purse Project](https://github.com/rorosaurus/project-mc2-led-purse).