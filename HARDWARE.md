# Hardware

## Required components:
* ESP32-DEVKIT-V1: [Amazon ($7)](https://smile.amazon.com/gp/product/B07Q576VWZ/), [AliExpress ($4)](https://www.aliexpress.com/item/32902307791.html)
* If you want this PCB to plug directly into the panel:
  * Female Pin Header 2X8 (connects this driver to the HUB75 panel): [Amazon](https://smile.amazon.com/gp/product/B07VJ3JCLT/), [AliExpress](https://www.aliexpress.com/item/32747224548.html)
* If you want this PCB to plug into your panel via a IDC ribbon cable:
  * 16P IDC Socket: [Amazon](https://smile.amazon.com/gp/product/B010V43ACO/), [AliExpress](https://www.aliexpress.com/item/32841491526.html)
  * 16P IDC Cable (might have come with your panel): [AliExpress](https://www.aliexpress.com/item/32873766356.html)
* Any HUB75 type scan LED panel (E pin is connected, so should work with 1/32 panels too)

## Optional components:
* If you want easy disconnect for ESP32:
  * 15 Pin Single Row Female Pin Header (buy 2): [AliExpress](https://www.aliexpress.com/item/32962790286.html)
* If you want easy disconnect for panel power:
  * Power cables for HUB75 panels (might have come with your panel): [AliExpress](https://www.aliexpress.com/item/32832930794.html)
  * Screw terminals (up to 2 can be used to easily wire power to the panels): [AliExpress](https://www.aliexpress.com/item/32993227789.html)
* If you want easy jumper wire access to the 8 extra GPIO and power pins:
  * Female Pin Header 2X4: [AliExpress](https://www.aliexpress.com/item/32785938092.html)
* If you want to smooth the power spikes (might prolong device lifespan or prevent brownouts):
  * Electrolytic Capacitor 16V 1000uF: [AliExpress](https://www.aliexpress.com/item/32812085542.html)
  
  
  
# Other related hardware you might want
* Project Mc2 LED Purse (harvest a cheap 16x32px LED display): [Amazon](https://smile.amazon.com/dp/B071LQR2QG/), [Adafruit article](https://blog.adafruit.com/2019/03/06/issue-16-hackspace-magazine-can-i-hack-it-a-smart-pixel-purse-neopixels-making-hackspacemag-biglesp/), [My GitHub Project](https://github.com/rorosaurus/project-mc2-led-purse)
  * If you want to daisy-chain this display, it's missing an output socket:
    * SMT 2x8 Male IDC Socket: [AliExpress](https://www.aliexpress.com/item/32989866598.html)
* If you want to daisy-chain other displays:
  * 16P IDC Cable (might have come with your panel): [AliExpress](https://www.aliexpress.com/item/32873766356.html)
  
# Alternative HUB75 shields
This board was inspired by Adafruit's [RGB Matrix Featherwing Kit](https://www.adafruit.com/product/3036) and [Teensy SmartMatrix Shield](https://www.adafruit.com/product/1902)! But mine is cheaper and more powerful, with Wifi/BT!

My shield only works with [SmartMatrix](https://github.com/pixelmatix/SmartMatrix/tree/teensylc), not [PxMatrix](https://github.com/2dom/PxMatrix).

If you want to work with PxMatrix, I highly recommend checking out [Brian Lough's shields](https://www.tindie.com/stores/brianlough/)! They are designed much better than mine!

I simply prefer SmartMatrix, which is why I designed this shield. There are [some shields in the SmartMatrix repo](https://github.com/pixelmatix/SmartMatrix/tree/teensylc/extras/hardware) but these appear to be active and require extra components. My shield is passive and just connects the pins to the right place. It lacks a proper level-shifter, so it assumes your panel will accept the 3.3V logic from the ESP32. It also lacks an external latch, which those active shields use to free up a few more pins on your ESP32.
