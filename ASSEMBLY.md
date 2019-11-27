# PCB Assembly Instructions
Please read all these instructions. There is important information in here that might not be immediately obvious. It is possible to solder connectors on the wrong side and end up with an invalid setup - pay close attention!

## Step -1: Buy components in advance
For a list of required and optional components, please see [`HARDWARE.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/HARDWARE.md).

Have everything?  Let's begin!

## Step 0: Verify your ESP32 board before soldering anything
Test and confirm your ESP32 works! Go to [`SOFTWARE.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/SOFTWARE.md) and install all the appropriate drivers, software, etc. and upload an example sketch to your board! Since the auto-bootloader capacitor isn't connected, you will need to hold `BOOT` for 2-3 seconds during the `Connecting...` phase. Once you have confirmed you can upload to your ESP32, you can proceed to assemble the hardware!

## Step 1: Mount output connector onto the PCB
Choose your output mode and seat your output connector accordingly.

### Output Mode 0
Directly plug this PCB into your LED panel using [2x8 female pin headers](https://www.aliexpress.com/item/32747224548.html). Here's how this mode would look when you're done:

![Output Mode 0 Example](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/output-mode-0-example.gif)

Here's how to mount your pin headers for Mode 0:

![Assemble Output for Mode 0](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/output-mode-0.jpg)

### Output Mode 1
Connect this PCB to your LED panel via [16-pin IDC ribbon cable](https://www.aliexpress.com/item/32873766356.html) plugged in to a [16-pin IDC socket](https://www.aliexpress.com/item/32841491526.html). Here's how you would plug into your LED panel in this mode:

![Output Mode 1 Example](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/output-mode-1-example.jpg)

How to mount your 16-pin IDC socket for Mode 1:

![Assemble Output for Mode 1](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/output-mode-1.gif)

Note: the missing edge on your IDC socket should face towards the unused Mode 0 column. Orientation is important!

## Step 2: Solder output connector joints
Flip over the PCB and solder your connector's joints

![Step 2](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/step-2.jpg)

## Step 2.5 (*optional*): Solder auto-bootloader capacitor
[Technically](https://github.com/espressif/esptool/wiki/ESP32-Boot-Mode-Selection), you're supposed to hold down `BOOT` button when powering on the ESP32 to enter bootloader and upload new code.

With this capacitor, you won't need to press anything. Your ESP32 will enter the bootloader automatically and the sketch will upload fine. I recommend this option!

Without this capacitor, you'll need to hold down `BOOT` for ~3 seconds when Arduino's console reads `Connecting......` otherwise the ESP32 will not enter the bootloader and your sketch upload will time out.

If you'd like to add it, solder a [1206 SMD 10uF Ceramic Capacitor](https://www.aliexpress.com/item/32879084143.html) to C2. This type of capacitor is not polarized, so the orientation does not matter. I've also had success with a 1uF capacitor, so I don't think the value needs to be exact. It's easy to solder by hand: just add some solder to one pad first, then use tweezers in one hand and your soldering iron in the other. After you finish soldering one half, you can ditch the tweezers for your solder and complete the other side.

![Bootloader capacitor](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/bootloader-cap.jpg)

If you don't have a ceramic capcitor, you can solder a 10uF electrolytic capacitor to the pads. Keep in mind you will place the ESP32 on top in a moment. I would suggest that you run the long legs of the capacitor pins out from under the ESP32, off the edge of the PCB. However, you might also prefer to leave the capacitor in place and increase the height of the sandwiched PCBs.

![Alternative bootloader capacitor](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/alt-bootloader-cap.jpg)

## Step 2.99 (*optional*): Apply waterproofing
This is your last chance before your currently soldered components get covered up by the ESP32 board. If you want to apply silicone conformal coating to those joints, now is the time.

## Step 3: Seat ESP32 into the PCB
I recommend seating your [ESP32-DEVKIT-V1](https://www.aliexpress.com/item/32902307791.html) as close to my PCB as possible. This minimizes the vertical space required. If you bought your ESP32 from AliExpress, you might have to solder the header pins on - remember to ensure they are properly straight (90 degree angle with the ESP32 PCB) before soldering too many!

![Step 3](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/step-3.gif)

If you want to be able to detach the ESP32, you can attach [two 15-Pin Single Row female pin headers](https://www.aliexpress.com/item/32962790286.html) instead.

## Step 4: Solder ESP32 pins onto the PCB
Flip over the PCB and solder the ESP32 pins (or pin headers, if you want to easily detach the ESP32).

![Step 4](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/step-4.jpg)

You can optionally trim the pins after soldering, if you want.

![Trim pins](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/trim-pins.jpg)

## Step 5: GPIO pins
At this stage I would recommend adding in any buttons, switches, sensors, etc. you'd like to add.  You can attach these to the breakout pins in the corner! You can add/modify these later too, I just think it's easiest to do this now (just in case you add the C1 capacitor - things start to get crowded!).

If you aren't sure what you'd like to add yet, I would recommend adding [female pin headers](https://www.aliexpress.com/item/32821638049.html) to all these pins (combine three 1x5 headers). Then you can use dupont connectors to prototype your design!

The following pins are broken out from the ESP32-DEVKIT-V1: `D13`, `D14`, `D23`, `D32`, `D33`, `D34`, `D35`, `D36`, `D39`.  All pins but `D23` can perform analog reads with 12-bit precision.  Remember the ESP32 pins can only handle 3.3V logic! Pin reference: [`ESP32-DEVKIT-V1 PINS`](ESP32-DEVKIT-V1-PINOUT.png)

The silkscreen labelling the GPIO pins is a little difficult to read sometimes, so here's a high res picture of the labels:

![GPIO pins](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/GPIO-pins.png)

The `3V3` pins carry the 3.3V power from the LDO. Please note: the LDO regulates a max of 1A, and that is shared across the ESP32 and these pins. Expect to pull < 0.5A from these pins together.

In a pinch, your project can also use the `BOOT` button on the ESP32-DEVKIT-V1. It's connected between `D0` and `GND`. This will interfere with your auto-bootloader, requiring you to hold the `BOOT` button when plugging in your ESP32 in order to program it.

## Step 6: Power flow
Let's figure out the best way to power your ESP32 and LED panels! Head over to my power document: [`POWER.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/POWER.md)!

This is also the point where you would attach the optional smoothing capacitor to C1! Check the polarity! The (-) terminal on the capacitor should be painted white and have printed negative signs. That white side should line up with the white print on the PCB when you insert the capacitor.

## Step N-1: Testing and uploading code
Test and confirm everything works! For links to software I recommend using with this board, please see [`SOFTWARE.md`](https://github.com/rorosaurus/esp32-hub75-driver/blob/master/SOFTWARE.md)!

## Step N: Reinforcing Micro-USB, Waterproofing, hardening
Go crazy with E6000 or your preferred epoxy! I haven't had any issues with this Micro-USB port, but please reinforce it nonetheless!  Add silicone conformal coating if you would like to waterproof anything!

# Mission Complete!
When you're done assembling, it should look something like this:

![Assembled Front](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembled-front.jpg)

![Assembled Back](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembled-back.jpg)


# Attaching to your LED panel
You attach it to the LED panel like this for Output Mode 0:

![Output Mode 0 Example](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/output-mode-0-example.gif)


You attach it to the LED panel like this for Output Mode 1:

![Output Mode 1 Example](https://github.com/rorosaurus/esp32-hub75-driver/raw/master/images/assembly/output-mode-1-example.jpg)