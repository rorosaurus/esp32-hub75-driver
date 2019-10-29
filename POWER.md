# Powering your ESP32 and LED Panels
Let's figure out the best way to power your LED panel!

General note: The `5V` and `GND` from the Micro-USB is in parallel with the two screw terminals and the C1 capacitor. They all have the same trace width, which should support TODO:TBD amps, and can be used interchangeably. If you are ever confused about which pad recieves which signal, you can confirm with your multimeter in diode mode.

## Power your LED panel via Micro-USB on the ESP32
This is the easiest way to easy snag a `5V` power source to power your panel, however it is not ideal. **I would recommend only choosing this for small panels**, and not at max brightness! Plug in your Micro-USB cable to the ESP32, and then wire your LED panel to the `5V` and `GND` [screw terminals](https://www.aliexpress.com/item/32993227789.html) (or solder directly).

TODO: pic

I have tested this method with `2.1A` flowing through to the panels for over 2 hours. Many components got quite hot, including: the LDO, Serial-to-USB chip, VIN pin, and Micro-USB port. I measured temperatures as high as 90°C.

This is included as an option for small projects like my [Project Mc2 LED Purse](https://github.com/rorosaurus/project-mc2-led-purse) which doesn't use much power (5W at max brightness).

## Power your LED panel via the 4-pin molex connector, and share that with ESP32
**Recommended for medium or large panels.** In this setup, your panels are recieving power from the [power cable](https://www.aliexpress.com/item/32832930794.html) that was probably included with your panel. You then share that power with the ESP32: using the screw terminals or even the C1 capacitor pads.  Optionally, you could power your ESP32 separately off the Micro-USB port.

TODO: pic

In this configuration, all the high current is flowing through the larger diameter power cables for the panel. This reduces a lot of stress on the ESP32 board, which now only deals with approximately 0.2A flowing in for the ESP32 itself. Temperatures stabilize at around 30°C - much more reasonable, and doesn't risk damaging the LDO, Serial-to-USB chip, etc.

## General
If you haven't used the C1 pads for supplying some power, you can optionally attach and solder a [1000uF through-hole Electrolytic Capacitor](https://www.aliexpress.com/item/32812085542.html). Take note of the polarity! This capacitor will help prevent brownouts/restarts on your ESP32, caused by voltage sag when your panels light up bright suddenly.