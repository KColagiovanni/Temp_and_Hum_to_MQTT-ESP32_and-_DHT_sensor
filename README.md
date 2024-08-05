# ESP32 with DHT Temperature and Humidity DHT Sensor that Broadcasts Data Over MQTT

### Description:
This program was written with the intent to measure temperature and humidity using an Espresif ESP32,
a DHT Temperature and Humidity sensor, and a power supply set to 3.3V. Alternatively, a Micro USB 
connector can be used to power the board and sensor. The program sends data to the serial monitor 
(console output) and an MQTT server using specific topics. In this case the MQTT server is setup on a
Raspberry Pi or Linux PC.
 
### Parts List and Cost:
- [ESP32 Dev Module - $8.99](https://www.amazon.com/ESP-WROOM-32-Development-Microcontroller-Integrated-Compatible/dp/B07WCG1PLV/ref=sr_1_3?crid=3HPW3GPPHHIM3&dib=eyJ2IjoiMSJ9.sjPHOXDjh8AVtKhUaQxpfTsJ3k4lqRnMvkD37K6ng5VzinwMiIpsjFTshr77euDxMgyoptu8p8PzFvEWpxs40O3qLHpzCyHJ_KpOTdT0hLn_kZ5VvaaUsJZpMZ72DRqNjRW6rqDl4SjGiTwB9vDeKLDCDOqArCW1K2xaXXcrZTOxq8sxeWJr2FTZ0ll8o8OF8eiAo09CJ1BvkJmDdSup5OfI5wz17zlMgYynAIZk2Fs.pMx0hu62hox1BjN9oWdBfO2aGiNb33N04lTTgxFeisA&dib_tag=se&keywords=esp32%2Bdevkit%2Bv1&qid=1722836883&sprefix=esp32%2Bdevkit%2Caps%2C298&sr=8-3&th=1)
- [DHT11 or DHT22 Temp and Hum Sensor - $9.99 (Qty 3)](https://www.amazon.com/Teyleten-Robot-Digital-Temperature-Humidity/dp/B0CPHQC9SF/ref=sr_1_4?crid=1BOWMTWB7UA3B&dib=eyJ2IjoiMSJ9.mEk3g57tT-no70-Kzou2lVwZpQj7rqKymONDbJ-DCwRVmLwU5omtXlFrsSRm7Cp7MJ-AxcWkNg1L676lQLn4TuDaFcndInGvDa20QKN9XNePuZ1Th8StltOm9K4cvGeLsVtMJH6_axH6K4rxms-4lqN75bxUWEkjAfaleAeaF8cP5F4Uxs6Kz1G_tBQLDbUB0HqKJW0kKypHXW7qoVNDgHEMzLBadg7-8Io48zxAZIw.EQ_MAqiZl_Do7pjMB4mXcrOeKNcMF4X8x3csphxzMzw&dib_tag=se&keywords=dht22+sensor&qid=1722837153&sprefix=dht22+senso%2Caps%2C153&sr=8-4)
- [7-12VDC to 3.3/5V Power Supply, Jumper Wires, and breadboard - $11.99 (Optional)](https://www.amazon.com/Breadboard-Minidodoca-Alligator-Raspberry-Electronic/dp/B0CYLBY4HR/ref=sr_1_5?crid=36NHQ8XJ9KOC&dib=eyJ2IjoiMSJ9.46eVfNcBm7aKmhRLu1BFwPEeYiAerVPyF6tQEMtftR0dLdLMkKmbNDUu0H8oq5oDW6pdPSluE53eK7UwqUZ60FLFpqb4Ngpv45OkKyPDO-Uy2QKQLzfqN7RerbA1WNBG-qu66wxHIYPUVxiJnLcUwlIql47y3yRtmnVcIf_UBukh4bI2_di5vprYnUB32Ep7gyhvCa3-PtE5BzAD8XZqQ-iLnEu8O_8IzO_2DgxpzMg.4PphCUmAPyv6E9JG-rXhh1daSjYUc3haEXVms3uHslA&dib_tag=se&keywords=mini%2Bbreadboard%2Bpower%2Bsupply&qid=1722837301&sprefix=mini%2Bbrearboard%2Bpower%2Bsuppl%2Caps%2C161&sr=8-5&th=1)

### Setup:
- #### Wiring:
  - Note: Wiring (Refers to the position on the breadboard(Rows(1-30) and Columns(a-j, +, -))):
  - ESP32 pressed into column a and i rows 16-30
  - DHT pressed into column j rows 10-12
  - Two Power Options:
    - Power supply pressed into (+) and (-) on both sides, rows 1-5 (If using power supply)
    - USB AC adapter (Like the one a cell phone uses) and a USB A to micro USB cable
  - Jumper wire from (+) to j30(Pin 3V3 on the ESP32) (If using power supply)
  - Jumper wire from (-) to j29(Pin GND on the ESP32) (If using power supply)
  - Jumper wire from f10(DHT(-)) to (-)
  - Jumper wire from f11(DHT('out") to j21(Pin D19 on ESP32)
  - Jumper wire from f12(DHT(+)) to (+)
