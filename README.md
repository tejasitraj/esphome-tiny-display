# esphome-tiny-display
A simple config for a 0.96" OLED Display used with an ESP8266 D1 Mini.

I recently created this project to learn how to use a simple display with esphome. I use a few entities from Home Assistant to fetch the current weather as well as forecast weather.

# What you will need
- [Wemos D1](https://www.banggood.com/Geekcreit-D1-Mini-V3_0_0-WIFI-Internet-Of-Things-Development-Board-Based-ESP8266-4MB-MicroPython-Nodemcu-p-1264245.html?cur_warehouse=CN&ID=522225&rmmds=search) Mini (ESP8266) (you could use any esp8266 or esp32 board - modify the yaml code accordingly!)
- A 0.96" OLED Display - I have used a [Geekcreit OLED Display from Banggood](https://www.banggood.com/Geekcreit-0_96-Inch-4Pin-Blue-Yellow-IIC-I2C-OLED-Display-Module-Geekcreit-for-Arduino-products-that-work-with-official-Arduino-boards-p-969144.html?cur_warehouse=CN&rmmds=search)
- Dupont connectors if needed (you can actually connect the display directly to the female header on the D1 Mini!)
- Micro USB Power Supply

# How to get started

- Copy the yaml file as well as the font files into your esphome folder
- Modify the yaml file substitutions fields according to your parameters
- Compile and upload to your hardware!

# Make the right connections

| D1 Mini Pin | Display Pin |
| ----------- | ----------- |
|5V|VCC|
|GND|GND|
|D1|SCL|
|D3|SDA|
