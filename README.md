# Use a ESP32-DEVKIT-V1 to drive HUB75 LED panels using SmartMatrix library

## Features
* Connects all necessary pins to drive HUB75 panels using `ESP32_FORUM_PINOUT` from [MatrixHardware_ESP32_V0.h](https://github.com/pixelmatix/SmartMatrix/blob/teensylc/src/MatrixHardware_ESP32_V0.h)
* 2x screw terminals to allow you to share 5V from the microUSB to your panels.
  * Traces are wide enough to support 5V@3A total
* Optional room for 1x Electrolytic Capacitor (I use a 16V 1000uF) to smooth the 5V power
* 2x4 pins for additional GPIO use: 
  * 2x GND
  * 2x 3.3V
  * 4x GPIO with ADC functionality (for buttons, potentiometers, etc.)
* Only one 16 pin IDC output, but this should support multiple HUB75 panels daisy-chained in series

## Software
I would recommend using the following software with this board:
* https://github.com/espressif/arduino-esp32 - To program ESP32 boards using Arduino
* https://github.com/pixelmatix/SmartMatrix/tree/teensylc - The library that helps you talk to the LED panel
* https://github.com/marcmerlin/AnimatedGIFs - Marc worked hard to make it relatively simple to use SmartMatrix to output animated .gifs
* https://github.com/me-no-dev/arduino-esp32fs-plugin - This plugin makes it simple to upload .gifs to your ESP32
* Use your preferred image editor to make your animated .gifs!

## Design
![](gerber/esp32-hub75-driver.png)
