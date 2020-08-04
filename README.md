# LoRa-BLE-Relay-v2
second version of the nRF52840 and SX126x-based communication device intended to run Meshtastic-
This version is still untested.

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


Installation of the Arduino variant: put the variant.h and .cpp in a folder named LoRaBLERelayV2 which has to be created inside the variants folder of the nrf52 core. There you also have boards.txt which you have to extend by the following:  

# ----------------------------------
# LoRa BLE Relay v2
# ----------------------------------
 lorablerelayv2.name=LoRa BLE Relay v2

# VID/PID for bootloader with/without UF2, Arduino + Circuitpython App
 lorablerelayv2.vid.0=0x239A
 lorablerelayv2.pid.0=0x8029
 lorablerelayv2.vid.1=0x239A
 lorablerelayv2.pid.1=0x0029
 lorablerelayv2.vid.2=0x239A
 lorablerelayv2.pid.2=0x002A
 lorablerelayv2.vid.3=0x239A
 lorablerelayv2.pid.3=0x802A

# Upload
 lorablerelayv2.bootloader.tool=bootburn
 lorablerelayv2.upload.tool=nrfutil
 lorablerelayv2.upload.protocol=nrfutil
 lorablerelayv2.upload.use_1200bps_touch=true
 lorablerelayv2.upload.wait_for_upload_port=true
 lorablerelayv2.upload.maximum_size=815104
 lorablerelayv2.upload.maximum_data_size=237568

# Build
 lorablerelayv2.build.mcu=cortex-m4
 lorablerelayv2.build.f_cpu=64000000
 lorablerelayv2.build.board=LoRaBLERelayV2
 lorablerelayv2.build.core=nRF5
 lorablerelayv2.build.variant=LoRa_BLE_Relay_V2
 lorablerelayv2.build.usb_manufacturer="Adafruit LLC"
 lorablerelayv2.build.usb_product="Feather nRF52840 Express"
 lorablerelayv2.build.extra_flags=-DNRF52840_XXAA {build.flags.usb}
 lorablerelayv2.build.ldscript=nrf52840_s140_v6.ld
 lorablerelayv2.build.vid=0x239A
 lorablerelayv2.build.pid=0x8029

# SofDevice Menu
 lorablerelayv2.menu.softdevice.s140v6=0.3.2 SoftDevice s140 6.1.1
 lorablerelayv2.menu.softdevice.s140v6.build.sd_name=s140
 lorablerelayv2.menu.softdevice.s140v6.build.sd_version=6.1.1
 lorablerelayv2.menu.softdevice.s140v6.build.sd_fwid=0x00B6

# Debug Menu
 lorablerelayv2.menu.debug.l0=Level 0 (Release)
 lorablerelayv2.menu.debug.l0.build.debug_flags=-DCFG_DEBUG=0
 lorablerelayv2.menu.debug.l1=Level 1 (Error Message)
 lorablerelayv2.menu.debug.l1.build.debug_flags=-DCFG_DEBUG=1
 lorablerelayv2.menu.debug.l2=Level 2 (Full Debug)
 lorablerelayv2.menu.debug.l2.build.debug_flags=-DCFG_DEBUG=2
 lorablerelayv2.menu.debug.l3=Level 3 (Segger SystemView)
 lorablerelayv2.menu.debug.l3.build.debug_flags=-DCFG_DEBUG=3
 lorablerelayv2.menu.debug.l3.build.sysview_flags=-DCFG_SYSVIEW=1
