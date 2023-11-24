# Airwick-ESPHome smart air refresher with ESPHome
Turning dumb Airwick air refresher to a smart one using ESPHome

## Parts needed:

- **Air Wick Fresh battery powered freshener**
- **Wemos D1 Mini board (ESP8266)** - _Could also work with any ESP chipset that is supported by ESPHome_
- **5V relay** - _Got them on Amazon (5 pack) - https://www.amazon.de/dp/B07BVXT1ZK_
- **Wires** - _I used DuPont wires that I cut if needed_
- **USB cable to power ESP and DC motor** - _Can be connected to USB port on ESP board or on 5V + GND pin_

## Instructions:

This was not my first attempt. Over one year my Airwick refresher was already smart. But it was painful solution using the integrated board on which I connected with ESP board and then simulate the signal to issue the motor rotation. ESP board was flashed with Tasmota which with some update in between broke something and it was no longer working. Wife was keep asking me when I will fix it so to keep WAF high I went back to drawing board.

Saw some projects like [Smart Air Freshener](https://github.com/ofilis/smartairfreshener) that uses DC motor directly with the ESP board and decided to try it myself. My goal was to power it with USB cable like I had before and not to constantly replace batteries. So it was a tiny mod. Reflashed the ESP board and put the relay in between. Everything worked at first attempt.

ESPHome is fully supported in Home Assistant so the entities were created automatically. I will use only one and that is the button which using ESPHome template turns the relay on for 0.5 seconds before turning it back off. At end I needed to create better automations. Before it would spray when movement was detected and if it took more then 30 minutes from last spray. It was still too frequent. What I want now is to spray only if someone was in bathroom for over 3 minutes (doing number 2).

Was looking for a solution and of course over complicated it. To make it easy I now have two automations. First one checks how long is movement sensor [Athom Presence Sensor](https://www.athom.tech/blank-1/human-presence-sensor) in my case) active. If it was over 3 minutes I set an input_boolean entity to true. Second automation will trigger the spray when there is no more movement in bathroom and input_boolean value was previously set to true. I tested it this morning after drinking morning coffee and had to go... And it works great!

## Wiring:

![fritzing_wiring_diagram](https://github.com/thehijacker/Airwick-ESPHome/assets/13857043/540dcf83-3031-40e4-b9e4-40d978160a58)
