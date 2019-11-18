# General Power Notes
These LED panels can demand multiple (sometimes up to 5!) Amps of current at 5V. Please make sure you have a beefy 5V power supply if you want to avoid problems.  If you're trying to power your project off portable USB battery banks, make sure they can do 5V/3A, and be sure to test how many Amps you are pulling (with a USB multimeter) and set a reasonable brightness limit! Make sure your USB cable is also thick enough to handle that current. I recommend at least 22AWG thickness. I personally cannibalized [these cables](https://smile.amazon.com/gp/product/B011KMSNXM/) with good success - cutting them and soldering them to the 4-pin power cable provided with my panels.

The `5V` and `GND` from the Micro-USB is in parallel with the two screw terminals and the C1 capacitor. They all have the same trace width and can be used interchangeably. If you are ever confused about which pad recieves which signal, you can confirm with your multimeter in diode mode and probing when the circuit is disconnected.

If you haven't used the C1 pads for supplying some power, you can optionally attach and solder a [1000uF through-hole Electrolytic Capacitor](https://www.aliexpress.com/item/32812085542.html). Take note of the polarity! This capacitor will help prevent brownouts/restarts caused by voltage sag when your panels light up bright suddenly. You can also fold this capacitor down if you want to reduce the vertical space it consumes.

You may find it helpful to use some blue tack to help orient the screw terminals as you solder them in place.

![Screw terminals](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/power/screw-terminals.jpg)

If you only have one screw terminal, you can still fit it between `5V` and `GND`, so you have one pin of each.

# Powering your ESP32 and LED Panels
Let's discuss the best way to power your LED panel!

## Power Option 0: Power your LED panel directly, and share that with ESP32
**Recommended! For all panels!**

In this setup, your panels are recieving the bulk of the `5V` power directly, then you splice off a wire to share that power with the ESP32.

![Power Option 0](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/power/power-option-0.jpg)

The panels could be getting power from the [4-pin power cable](https://www.aliexpress.com/item/32832930794.html) that was probably included with your panel. The other end of that cable could be powered by a large 5V power supply, or (if your energy demands are small enough) you can wire it into a USB cable. You could also just solder the USB cable wires directly to the panel's power, if you're missing the proper 4-pin power cables.

You then share that power with the ESP32. You can solder a strand of wire to the LED panel's power terminals and run that wire to my PCB. Use the `5V` and `GND` screw terminals to attach the wire if you desire, otherwise for a more permanent installation you can solder the wires, or even use the C1 capacitor pads.

In this configuration, all the high current is flowing through the larger diameter power cables for the panel. This reduces a lot of stress on the ESP32 board, which now only deals with approximately 0.3A flowing in for the ESP32 itself. Unlike `Power Option 1`, temperatures stabilize at around 30°C - much more reasonable, and doesn't risk damaging the ESP32 board or components.

## Power Option 1: Power your LED panel via Micro-USB on the ESP32
**NOT RECOMMENDED, but technically possible for some very small panels.**

Plug in your Micro-USB cable to the ESP32, and then wire your LED panel to the `5V` and `GND` [screw terminals](https://www.aliexpress.com/item/32993227789.html) (or solder directly).

![Power Option 1](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/power/power-option-1.jpg)

This is the easiest way to easy snag a `5V` power source to power your panel, however it is not ideal to push so much power through the ESP32 board. I would only try this for very small panels (like 16x32), and not at max brightness! Please make sure your Micro-USB cable and USB battery pack are sourced from a quality brand (like Anker) and support the necessary amperage (I recommend 3A, just to be safe!).

This is included as an option for small projects like my [Project Mc2 LED Purse](https://github.com/rorosaurus/project-mc2-led-purse) which doesn't use much power (5W at max brightness).

### Critical Limitations of Power Option 1
**If you sourced your ESP32 from AliExpress** (white backed PCB), I would not recommend this method unless you are confident your whole project will not exceed `5W`.  I have tested these boards pulling `5W` for 30 minutes with no issues. But in another test, supplying `7W` melted the Micro-USB port's `5V` trace in less than 1 minute.

**If you sourced your ESP32 from Amazon** (black backed PCB), I tested this method with `2A` flowing through to the panels for over 2 hours (`11W` total power over the Micro-USB port). Many components got quite hot, including: the LDO, Serial-to-USB chip, VIN pin, and Micro-USB port. I measured temperatures as high as 90°C. This heat is less than ideal, which is why I recommend using `Power Option 0`.
