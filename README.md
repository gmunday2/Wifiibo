# Wifiibo - Wifi amiibo Management Tool
Wifiibo is a tool for managing an amiibo collection.  Using an ESP8266 (with the Arduino development environment) and an NFC reader, you can read & store existing amiibos, create new amiibos using amiibo data files, and view your amiibo data.  All amiibo data is stored on the flash memory of the ESP8266, so there's no need for additional storage hardware.  The whole thing is managed using any web browser!

The library that runs most of the amiibo functions is a port of [amiitool](https://github.com/socram8888/amiitool) for the ESP8266 using the Arduino environment.

## Features
* Save/back up existing amiibo
* Create new ammibos using data files (requires encryption keys)
* View your amiibo collection using any web browser (even on your phone!)

## Screenshots

## Getting Started
### Hardware
Wifiibo requires the following hardware:
* ESP8266 (Wemos D1 Mini from Aliexpress: ~$3)
* PN532 NFC board (PN532 V3 board from Aliexpress: ~$5)

Make the following connections between the ESP8266 and the PN532 board:

ESP Pin | PN532 Pin
--------|----------
MOSI | D7
MISO | D6
SCK | D5
SS | D4
VCC | +5V
GND | GND

### Software Library Dependencies
Wifiibo depends on a number of additional Arduino libraries (which are needed if you want to compile Wifiibo):
* [EspAsyncTCP](https://github.com/me-no-dev/ESPAsyncTCP) 
* [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
* [Adafruit_PN532](https://github.com/adafruit/Adafruit-PN532)
  * A modified version of this library, Adafruit_PN532Ex, is included with Wifiibo
* [mbedtls](https://tls.mbed.org/)
  * A modified version of this library is included with Wifiibo
  
### Compiling
In order to compile the Wifiibo software, you'll need the Arduino IDE.  Ensure you have the ESP8266 board support package installed (refer to [the main ESP8266 Arduino page](https://github.com/esp8266/Arduino) for instructions on setting it up).  Clone this repository into the 'libraries' folder in your Arduino sketch folder.  Open the Arduino IDE, and you'll find Wifiibo under the "Examples" menu, listed under the "amiitool" library.  After selecting your ESP8266 board in the IDE, click the Upload button to flash Wifiibo to the ESP8266.

## Using Wifiibo
When Wifiibo starts, if your ESP8266 isn't connected to Wifi, it will start up its own hotspot called "Wifiibo."  Connect to the hotspot using your phone or computer, then open a web browser and go to http://192.168.4.1 to access Wifiibo.  Click on the "Configure Wifi" button, enter your Wifi network credentials, and click submit.

Once connected to Wifi, you can access Wifiibo by going to http://wifiibo.local in your broswer.  Alternatively, some routers will allow you to go to "http://wifiibo." (note the '.' at the end).  Tip: Once you get to the Wifiibo page, you can click on the IP in the top-right corner of the page.  Using the IP directly seems to be faster on some Windows computers.

In order for Wifiibo to read or write any amiibo tags, it needs the amiibo encryption keys.  Click on the red button labeled "Upload keys" to import or upload your amiibo encryption keys.  The keys file must be named "key_retail.bin".  Once you have successfully imported the amiibo encryption keys, the red "Upload keys" button will disappear.

Using Wifiibo is fairly straightforward.  In order to write amiibo information to a tag, the tag must be type NTAG215 and must be blank.

## Updating
If new software releases are made, they will show up in the "releases" folder.  To easily update your Wifiibo, download the latest release binary, then go to http://wifiibo.local/update.  Select the "bin" file you downloaded, and click the "Update" button.  When updating is complete, the page will change to "OK."  Go back to http://wifiibo.local and verify that the version number in the upper-right corner of the screen has been updated.
