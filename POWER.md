# General Power Notes
These LED panels can demand multiple (sometimes up to 5!) Amps of current at 5V. Please make sure you have a beefy 5V power supply and thick cables if you want to avoid problems.

The `5V` and `GND` from the Micro-USB on the ESP32 board is in parallel with the two screw terminals and the C1 capacitor. They all have the same trace width and can be used interchangeably to supply or provide power to the ESP32. If you are ever confused about which pad recieves which signal, you can confirm with your multimeter in diode mode and probing when the circuit is disconnected from power.

# Mobile Power Notes
It is possible to power your panel off USB battery packs (although it is unlikely you can safely do anywhere near maximum brightness on anything besides tiny 32x16 panels). If you want to try this, I would recommend making sure your battery pack can do 5V/3A. This is the maximum current typically allowed for USB-A connectors. You might be able to find some USB-C battery packs that can do more.

Note that some battery packs will turn off after a while if they are not supplying a good deal of current. You probably don't need to worry about this, unless you have a very small panel at very low brightnesses.

Your LED panel and my PCB are not equipped to take full advantage of USB-PD or QC3.0 battery packs. If you plug into those, they should only provide the basic 5V/3A.

Start testing with a very low brightness (like 20/255 [some extremely low brightnesses might not display anything at all, FYI]) to ensure you do not pull too many Amps. Be sure to test how many Amps you are pulling (a USB multimeter makes this easy!) and set a reasonable brightness limit in your sketch, so you never exceed 3A! I actually set my maximum brightness to around 2.5A just to be safe.

Make sure your USB cable is also thick enough to handle that current. I recommend at least 22AWG thickness. I personally cannibalized [these cables](https://smile.amazon.com/gp/product/B011KMSNXM/) with good success. I cut them and soldered them to the 4-pin power cable provided with my panels. Try not to make your cable unnecessarily long, if you can avoid it.

![USB 4-pin power cable](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/power/usb-4-pin-power-cable.jpg)

# Power Options
Let's discuss the best way to power your LED panels and ESP32!

In general I would recommend Option 2 if possible. Then Option 0, which introduces some risk of brownouts/restarts. Last resort is Option 1, which WILL damage your electronics if you use too much power.

## Power Option 0: Power your LED panel directly, and share that with ESP32
**Recommended if you want to power everything off one cable!**

In this setup, your panels are recieving the bulk of the `5V` power directly, then you splice off a wire to share that power with the ESP32.

![Power Option 0](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/power/power-option-0.jpg)

The panels could be getting power from the [4-pin power cable](https://www.aliexpress.com/item/32832930794.html) that was probably included with your panel. The other end of that cable could be powered by a large 5V power supply, or (if your energy demands are small enough) you can wire it into a USB cable. You could also just solder the USB cable wires directly to the panel's power, if you're missing the proper 4-pin power cables.

You then share that power with the ESP32. You can solder a strand of wire to the LED panel's power terminals and run that wire to my PCB. Use the `5V` and `GND` screw terminals to attach the wire if you desire, otherwise for a more permanent installation you can solder the wires, or even use the C1 capacitor pads.

In this configuration, all the high current is flowing through the larger diameter power cables for the panel. This reduces a lot of stress on the ESP32 board, which now only deals with approximately 0.3A flowing in for the ESP32 itself. Unlike `Power Option 1`, temperatures stabilize at around 30°C - much more reasonable, and doesn't risk damaging the ESP32 board or components.

## Power Option 1: Power your LED panel via Micro-USB on the ESP32
**USE AT YOUR OWN RISK! THIS COULD DAMAGE YOUR ELECTRONICS OR START A FIRE!**

**NOT RECOMMENDED, but technically possible for some very small panels.**

Plug in your Micro-USB cable to the ESP32, and then wire your LED panel to the `5V` and `GND` [screw terminals](https://www.aliexpress.com/item/32993227789.html) (or solder directly).

![Power Option 1](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/power/power-option-1.jpg)

This is the easiest way to easy snag a `5V` power source to power your panel, however it is not ideal to push power through the ESP32 board. I would only try this for very small panels (like 16x32), and not at max brightness! Please make sure your Micro-USB cable and USB power source are sourced from a quality brand (like Anker) and support the necessary amperage (I recommend 3A, just to be safe!).

This is included as an option for small projects like my [Project Mc2 LED Purse](https://github.com/rorosaurus/project-mc2-led-purse) which doesn't use much power (5W at max brightness).

### Critical Limitations of Power Option 1
**If you sourced your ESP32 from AliExpress** (white backed PCB), I would not recommend this method unless you are confident your whole project will not exceed `5W`.  I have tested these boards pulling `5W` for 30 minutes with no issues. But in another test, supplying `7W` melted the Micro-USB port's `5V` trace in less than 1 minute.

**If you sourced your ESP32 from Amazon** (black backed PCB), I tested this method with `2A` flowing through to the panels for over 2 hours (`11W` total power over the Micro-USB port). Many components got quite hot, including: the LDO, Serial-to-USB chip, VIN pin, and Micro-USB port. I measured temperatures as high as 90°C. This heat is less than ideal, which is why I recommend using `Power Option 0` or `Power Option 1` instead.


## Power Option 2: Separate power for ESP32 and panels
**Recommended for the fewest issues!**

Power your ESP32 dev board with a Micro-USB cable. Power your LED Panel(s) separately with the [4-pin power cable](https://www.aliexpress.com/item/32832930794.html) (probably included with your panel) hooked up to a *different* 5V power source.

I use this setup for [Furret](https://github.com/rorosaurus/FurretTotem). The panels can pull lots of power, which can sag the voltage output regulated from a USB battery bank. Using a separate battery pack ensures that your ESP32 never suffers from low voltage and brownouts/restarts.

Note that if your USB battery bank has two USB-A outputs, those often share the same 5V regulator. On my battery pack, the USB-C output seems to be regulated independently of the USB-A outputs. So Furret's ESP32 runs off a USB-A port, while the panels are powered off the USB-C port. This keeps the ESP32 from resetting when the panels draw lots of current.
