# Temperature and Humidity(DHT22 Sensor) using an ESP32 that Broadcasts Data Over MQTT

### Description:
This program was written with the intent to measure temperature and humidity using an Espresif ESP32,
a DHT11 or DHT22 Temperature and Humidity sensor, and a power supply set to 3.3V. Alternatively, a 
Micro USB connector can be used to power the board and sensor. The program sends data to the serial 
monitor (console output) and publishes [MQTT](https://mqtt.org/) messages using specific topics. A 
Node Red program is subscribed to all the topics that are published and it also sends the messages to 
Home Assistant.
 
## Requirements
### Hardware:
- ESP32 Module
- DHT22 Temp and Hum Sensor
- Electronic Kit
- USB A to Micro USB wire
  
### Software:
- [Arduino IDE](https://www.arduino.cc/en/software) installed on a personal PC.
  
## Cost:
- [ESP32 Devkit V1 Module - $8.99](https://www.amazon.com/ESP-WROOM-32-Development-Microcontroller-Integrated-Compatible/dp/B07WCG1PLV/ref=sr_1_3?crid=3HPW3GPPHHIM3&dib=eyJ2IjoiMSJ9.sjPHOXDjh8AVtKhUaQxpfTsJ3k4lqRnMvkD37K6ng5VzinwMiIpsjFTshr77euDxMgyoptu8p8PzFvEWpxs40O3qLHpzCyHJ_KpOTdT0hLn_kZ5VvaaUsJZpMZ72DRqNjRW6rqDl4SjGiTwB9vDeKLDCDOqArCW1K2xaXXcrZTOxq8sxeWJr2FTZ0ll8o8OF8eiAo09CJ1BvkJmDdSup5OfI5wz17zlMgYynAIZk2Fs.pMx0hu62hox1BjN9oWdBfO2aGiNb33N04lTTgxFeisA&dib_tag=se&keywords=esp32%2Bdevkit%2Bv1&qid=1722836883&sprefix=esp32%2Bdevkit%2Caps%2C298&sr=8-3&th=1)
- [DHT22 Temp and Hum Sensor - $9.99 (Qty 3)](https://www.amazon.com/Teyleten-Robot-Digital-Temperature-Humidity/dp/B0CPHQC9SF/ref=sr_1_4?crid=1BOWMTWB7UA3B&dib=eyJ2IjoiMSJ9.mEk3g57tT-no70-Kzou2lVwZpQj7rqKymONDbJ-DCwRVmLwU5omtXlFrsSRm7Cp7MJ-AxcWkNg1L676lQLn4TuDaFcndInGvDa20QKN9XNePuZ1Th8StltOm9K4cvGeLsVtMJH6_axH6K4rxms-4lqN75bxUWEkjAfaleAeaF8cP5F4Uxs6Kz1G_tBQLDbUB0HqKJW0kKypHXW7qoVNDgHEMzLBadg7-8Io48zxAZIw.EQ_MAqiZl_Do7pjMB4mXcrOeKNcMF4X8x3csphxzMzw&dib_tag=se&keywords=dht22+sensor&qid=1722837153&sprefix=dht22+senso%2Caps%2C153&sr=8-4)
- [Electronic Kit - $9.99](https://www.amazon.com/EL-CK-002-Electronic-Breadboard-Capacitor-Potentiometer/dp/B01ERP6WL4/ref=sr_1_5?crid=ZSLT3X8Y8XIM&dib=eyJ2IjoiMSJ9.Z17QbUQZrXSSh06-3tBTPmWRb8MGJFDbVC6Hwml1dUqRxtZJPvEx9oNd2cgfi7ZoL4DiwVJQ-aEE9tC6BJRN7HvukCez2089xx5ReCqmUis_jRcLgepMRkcqCi1K3NlUrv1HmEQpxY7vHWpZupYQaQxPOjs72YPVdhUPR9nYpJyUr3JLgfrp04v0thxnnJdoIw1fiI3KkGhDWSMXCaMSk_C0ywbn7P0izQLqv2-eA6x98Jhs5wovmQz4PBb8ndtLWyK0uLszKp3WQ26i-VVI-WOkP1WMeg0FNymbBulr6Nw.-xGLZPOrdAwgJzlPYSTwMkeRZ7jDYMT9IZuCMagGfiA&dib_tag=se&keywords=LED%2Band%2Bresistor%2Bkit&qid=1723609171&sprefix=led%2Band%2Bresistor%2Bkit%2Caps%2C166&sr=8-5&th=1)

## User Guide
### Getting Started
- #### Wiring:
    * Note: The bread board rows are shorted together on the right(columns a-e) and left(columns f-j) sides. The right and left sides of the bread board are not shorted together.
    * ESP32 pressed into the bread board.
    * DHT pressed into the breadboard with all of the pins in the same column.
        * Jumper wire from the pin labeled D19 on the ESP to "Out" on the DHT sensor.
    * If using the power supply to power the project:
        * Power supply pressed into the (+) and (-) of the bread board. Note: If the power supply if connected on the "bottom" of the bread board, the polarity marked on the bread board will be incorrect.
        * Jumper wire from (+) on the breadboard to the pin labeled VIN on the ESP32.
        * Jumper wire from (-) on the breadboard to the pin labeled GND on the ESP32.
    * Jumper wire from the pin labeled 3V3 on the ESP to "+" on the HTU sensor.
    * Jumper wire from the pin lebeled GND on the ESP to "-" on the HTU sensor.
    * [Optional] If using an LED to show when MQTT is connected:
        * The long side of the LED goes to GPIO 5 of the ESP32.
        * Connect the short side of the LED to one leg of the 1K Ohm resistor (both connected to the same row in the breadboard (Columns a-e or f-j)).
        * Connect the other leg of the resistor to ground(or "-" of the power supply).

- #### Setup:
    * Clone the repository by opening a terminal on personal PC that has the Arduino IDE installed on it and type: `git clone https://github.com/KColagiovanni/Temperature_and_Humidity_using_ESP32_and_DHT22_Sensor.git`
    * Using the file explorer navigate to the Temperature_and_Humidity_using_ESP32_and_DHT22_Sensor directory and double click on the Temp_and_Hum_to_MQTT-ESP32_and_DHT_sensor.ino file. This should open up a new Arduino IDE window.
    * [Install the ESP32 board add-on](https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/) to Arduino IDE.
        * Install the DHT package to the Arduino IDE by going to *Tools* > *Manage Libraries* and search for *DHT sensor library*, then click on install.
        * Install the PubSubCLient package to the Arduino IDE (used for MQTT communication) by going to *Tools* > *Manage Libraries* and search for *PubSubClient*, then click on install.
    * Set up the Arduino IDE before uploading the sketch by:
        * In the Arduino IDE select *Tools* > *Board* and select the board that is being used.
        * In the Arduino IDE select *Tools* > *Port* and select the USB/Serial port that is being used.

  ### How to Use
    * Connect the ESP32 to the personal PC using a USB A to Micro USB cable.
    * Select *Upload* in the upper left corner of the Arduino IDE. It is a circular button with an arrow pointing right.
    * Once the sketch is uploaded, power cycle the ESP32 and open the serial monitor to see board output by clicking on the magnifying glass icon in the upper right corner. Note: the ESP may need to be power cycled after this to see data being displayed.
