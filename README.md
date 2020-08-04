# LoRa-BLE-Relay-v2
second version of the nRF52840 and SX126x-based communication device intended to run Meshtastic-
This version is in the testing process. Warning: wait for v2.1 before ordering the PCB. Some important PCB design bugs have been identified and have to be fixed first!!

![LoraRelayV2](https://github.com/BigCorvus/LoRa-BLE-Relay-v2/blob/master/relay2.0.png)  
See fourm discussion https://meshtastic.discourse.group/t/building-for-nrf52-boards/457/62  

Features are: 
- 110x50mm  
- more ground plane for better LoRa RF performance
- low power consumption in receive mode and Bluetooth active: about 20mA for the 30dbm and 10mA for the 22dbm module version  
- nRF52840 module by Waveshare/HolyIOT with native USB bootloader, broken out NFC pins and good Arduino support (Adafruit Core)  
- Ebyte E22 LoRa Modules based on new Semtech SX126x chipsets for 22 or 30dbm and 915,868,433...Mhz frequency bands. 
- Footprint for both the big and the small LoRa module (the boost converter doesn't need to be assembled if the smaller one is used)  
- SD card slot (same card holder as in the Adafruit Adalogger boards  
- On board buzzer  
- GPS connector breaking out RXD and TXD (JST-SH 4-pin) with high-side power cutting option. Powered either from the battery voltage or from 5V (select via solder jumper)  
- Many screen options: usual 128x64 OLEDs via I2C or sunlight-readable and power-efficient ST7565R and UC1701X LCD screens via bitbanged 4 line SPI (see BOM for variants)  
- display headers can be expansion headers  
- 3 nav buttons  
- powered from 1 or 2 parallel unprotected 18650 cells (protection circuitry on board)  
- port for external battery or solar charger for concurrent charging  
- battery temperature monitoring/environmental sensing via BME280  
- USB-C connector
- power management via TI fuel gauge IC with optional programmable power cutting option  (selectable via solder jumper, experimental!) 


Installation of the Arduino variant: put the variant.h and .cpp in a folder named LoRaBLERelayV2 which has to be created inside the variants folder of the nrf52 core. There you also have boards.txt which you have to extend by the content of the boards.txt inside this repo.  
