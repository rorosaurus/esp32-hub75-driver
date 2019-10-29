# Assembly Instructions
Please read all these instructions. There is important information in here that might not be immediately obvious. It is possible to solder connectors on the wrong side and end up with an invalid setup - pay close attention!

## Step -1: Buy components
For a list of required and optional components, please see [`HARDWARE.md`](HARDWARE.md).

Have everything?  Let's begin!

## Step 0?
TODO: needed?

## Step 1: Mount output connector onto the PCB
Choose your output mode and seat your output connector accordingly.

### Output Mode 0
Directly plug this PCB into your LED panel using [2x8 female pin headers](https://www.aliexpress.com/item/32747224548.html).

TODO: pic of how it finally plugs in

### Output Mode 1
Connect this PCB to your LED panel via [16-pin IDC ribbon cable](https://www.aliexpress.com/item/32873766356.html) plugged in to a [16-pin IDC socket](https://www.aliexpress.com/item/32841491526.html).

Note: the missing edge on your IDC socket should face towards the unused Mode 0 column. Orientation is important!

TODO: pic of how it finally plugs in, showing orientation

## Step 2: Solder output connector joints
Flip over the PCB and solder your connector's joints

TODO: pic

## Step 2.5 (*optional*): Solder auto-bootloader capacitor
[Technically](https://github.com/espressif/esptool/wiki/ESP32-Boot-Mode-Selection), you're supposed to hold down `BOOT` button when powering on the ESP32 to enter bootloader and upload new code.

With this capacitor, you won't need to press anything. Your ESP32 will enter the bootloader automatically and the sketch will upload fine. I recommend this option!

Without this capacitor, you'll need to hold down `BOOT` for ~3 seconds when Arduino's console reads `Connecting......` otherwise the ESP32 will not enter the bootloader and your sketch upload will time out.

If you'd like to add it, solder a [1206 SMD 10uF Ceramic Capacitor](https://www.aliexpress.com/item/32879084143.html) to C2. This type of capacitor is not polarized, so the orientation does not matter. I've also had success with a 1uF capacitor, so I don't think the value needs to be exact.

If you don't have a ceramic capcitor, you can solder a 10uF electrolytic capacitor to the pads. Keep in mind you will place the ESP32 on top in a moment. I would suggest that you run the long legs of the capacitor pins out from under the ESP32, off the edge of the PCB. However, you might also prefer to leave the capacitor in place and increase the height of the sandwiched PCBs.

TODO: pic

## Step 2.99 (*optional*): Apply waterproofing
This is your last chance before your currently soldered components get covered up by the ESP32 board. If you want to apply silicone conformal coating to those joints, now is the time.

## Step 3: Seat ESP32 into the PCB
I recommend seating your [ESP32-DEVKIT-V1](https://www.aliexpress.com/item/32902307791.html) as close to my PCB as possible. This minimizes the vertical space required. If you bought your ESP32 from AliExpress, you might have to solder the header pins on - remember to ensure they are properly straight (90 degree angle with the ESP32 PCB) before soldering too many!

TODO: pic

If you want to be able to detach the ESP32, you can attach [two 15-Pin Single Row female pin headers](https://www.aliexpress.com/item/32962790286.html) instead.

## Step 4: Solder ESP32 pins onto the PCB
Flip over the PCB and solder the ESP32 pins (or headers).

TODO: pic

## Step 5: GPIO pins
At this stage I would recommend adding in any buttons, switches, sensors, etc. you'd like to add.  You can attach these to the breakout pins in the corner! You can add/modify these later too, I just think it's easiest to do this now (just in case you add the C1 capacitor - things start to get crowded!).

If you aren't sure what you'd like to add yet, I would recommend adding [female pin headers](https://www.aliexpress.com/item/32821638049.html) to all these pins (combine three 1x5 headers). Then you can use dupont connectors to prototype your design!

The following pins are broken out from the ESP32-DEVKIT-V1: `D13`, `D14`, `D23`, `D32`, `D33`, `D34`, `D35`, `D36`, `D39`.  All pins but `D23` can perform analog reads with 12-bit precision.  Remember the ESP32 pins can only handle 3.3V logic! Pin reference: [`ESP32-DEVKIT-V1 PINS`](ESP32-DEVKIT-V1-PINOUT.png)

The `3V3` pins carry the 3.3V power from the LDO. Please note: the LDO regulates a max of 1A, and that is shared across the ESP32 and these pins. Expect to pull < 0.5A from these pins together.

Your project can also use the `BOOT` button on the ESP32-DEVKIT-V1. It's connected between `D0` and `GND`. This will interfere with your auto-bootloader, so I don't recommend it unless you really need it!

## Step 6: Power flow
Let's figure out the best way to power your ESP32 and LED panels! Head over to my power document: [`POWER.md`](POWER.md)!

## Step N-1: Testing
Test and confirm everything works! For links to software I recommend using with this board, please see [`SOFTWARE.md`](SOFTWARE.md)!

## Step N: Reinforcing Micro-USB, Waterproofing, hardening
Go crazy with E6000 or your preferred epoxy! I haven't had any issues with this Micro-USB port, but please reinforce it nonetheless!  Add silicone conformal coating if you would like to waterproof anything!
