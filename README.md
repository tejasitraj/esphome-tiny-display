# esphome-tiny-display
A simple config for a 0.96" OLED Display used with an ESP8266 D1 Mini.

I recently created this project to learn how to use a simple display with esphome. I use a few entities from Home Assistant to fetch the current weather as well as forecast weather.

# What you will need
- [Wemos D1](https://www.banggood.com/Geekcreit-D1-Mini-V3_0_0-WIFI-Internet-Of-Things-Development-Board-Based-ESP8266-4MB-MicroPython-Nodemcu-p-1264245.html?cur_warehouse=CN&ID=522225&rmmds=search) Mini (ESP8266) (you could use any esp8266 or esp32 board - modify the yaml code accordingly!)
- A 0.96" OLED Display - I have used a [Geekcreit OLED Display from Banggood](https://www.banggood.com/Geekcreit-0_96-Inch-4Pin-Blue-Yellow-IIC-I2C-OLED-Display-Module-Geekcreit-for-Arduino-products-that-work-with-official-Arduino-boards-p-969144.html?cur_warehouse=CN&rmmds=search)
- [Dupont connectors](https://www.banggood.com/40pcs-10cm-Female-To-Female-Jumper-Cable-Dupont-Wire-p-994059.html?cur_warehouse=CN&rmmds=search) if needed (you can actually connect the display directly to the female header on the D1 Mini!)
- Micro USB Power Supply

# How to get started

- Copy the yaml file as well as the font files into your esphome folder
- Modify the yaml file substitutions fields according to your parameters
  - Your device name
  - Your Static IP Details. If you dont want to set a static IP, comment out this line as well as the lines for manual_ip under the wifi section!
  - Entities for an internal temperature sensor and an external temperature sensor
  - An entity for the current weather condition - I use SMHI in Sweden, you could select your local weather service
  - Entities to show the forecast low and forecast high for today. See forecast section below.
- Compile and upload to your hardware!

# Make the right connections

| D1 Mini Pin | Display Pin |
| ----------- | ----------- |
|5V|VCC|
|GND|GND|
|D4|SCL|
|D3|SDA|

# Weather and Forecast using weather service

I use the [SMHI integration](https://www.home-assistant.io/integrations/smhi/) in Home Assistant since I live in Sweden as my default weather service. You can use whichever local weather service you have in your area.

By default, the state of the weather service corresponds to the current weather condition (cloudy, clear etc.), as per the Home Assistant [weather](https://www.home-assistant.io/integrations/weather/) page.

The forecast high and low for the day are contained as state attributes within the weather entity in Home Assistant. I created template sensors in Home Assistant to extract these into their own entities:

Here is the code I added to my configuration.yaml to make this happen:

```
template:
  - sensor:
      - name: Todays Forecast High
        state: >
          {{ states.weather.smhi_home.attributes.forecast.0.temperature }}
      - name: Todays Forecast Low
        state: >
          {{ states.weather.smhi_home.attributes.forecast.0.templow }}
```  
These entities are then called out from the esphome yaml to fetch forecast data.
