# LED CCT Controller
This repository holds design files and code related to my ESP32 based LED CCT Controlled.

## Problem Statement
Light is an important part of any living situation. One factor that is often overlooked is [Color Temperature](https://www.westinghouselighting.com/color-temperature.aspx), measured in Kelvin. A typical range is from 2700K-5000K, with lower numbers being redder and higher numbers being 'brighter' and bluer. 

I appreciate the role that [f.lux](https://justgetflux.com/) has on my computer screen color, and I have attempted to emulate similar room lighting using a [Phillips Wake up Light](https://www.usa.philips.com/c-p/HF3471_60/wake-up-light). However, I would like to have control over the lights being on/off and their color temperature throughout the day automatically. 

## The plan
To accomplish this, I set out to design a system that could be incorporated in my Home Assistant Setup, so that I can easily integrate it into my location based automations and even incorporate my digital calendar (i.e. if I am working at night, I want the color temperature to mirror my schedule). 

I wanted to combine an ESP32 using [ESPHome (Specifically the Cool White + Warm White Light platform)](https://esphome.io/components/light/cwww.html), combined with a white tunable ("CCT") LED strip that I can customize and place around the house. 

## Parts

### ESP32
For this project, I have been using an [DOIT ESP32 DEVKIT v1](https://www.mischianti.org/wp-content/uploads/2021/03/ESP32-DOIT-DEV-KIT-v1-pinout-mischianti-1024x501.jpg) as the base. 

For future iterations, I may plan to just use the ESP32 module (i.e. without the development board), e.g. [ESP-WROOM-32](https://www.digikey.com/catalog/en/partgroup/esp-wroom-32/75395), but this will require me to be able to solder/have on hand many SMD Resistors and capacitors. 

### LED strips
For the first iteration, I am using the [5m Tunable White LED Strip Lights, 12V](https://www.superbrightleds.com/moreinfo/flexible-led-strip-lights/5m-tunable-white-led-strip-light-color-changing-led-tape-light-12v24v-ip20/5497/12019/) from [superbrightleds.com](superbrightleds.com). It is definitely a bit on the pricey side, and I plan to source cheaper parts from aliexpress.com, but I wanted to have a strip that I could rely on to work to minimize troubleshooting steps. 

### Power Supply
I chose 12V LED strips intentionally (over 5V LEDs that are available) as I want to be able to power long runs of LEDs without significant voltage drop/heat dissipation concerns. It also allows me to buy a slightly cheaper power supply (fewer amps required). The LED strip above has a rating of 13.8 Watts/meter. As I bought 5 meters of LEDs, this works out to 5.75 amps of current at max load. 

I am only planning on (at least initially) using the LED strips for a maximum of 2-3 feet, for 1 amp. With that in mind, I picked up a 12V, 1 amp DC power supply. 

#### Stepping down to 3.3V

The ESP32 runs on 3.3V, however. I could not be bothered to design an inclue a switching buck converter, so I opted to include a pre-made [3.3V output, up to 21V input Buck converter](https://www.adafruit.com/product/4683) from adafruit that I can include with a 4 pin header. 

### Transistors
