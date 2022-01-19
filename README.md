# Domoticz IP Weather Station plugin

This plugin allows you to grab meteo data localy from Personal Weather Station (PWS) via TCP/IP. There is no necesity to register to any Internet weather service. 
The plugin is based on similar Xorfor project. 

## Supported devices
The plugin supports all PWS hardware which uses Weather Undergroud (WU) protocol as a data transport solution. The Ecovitt protocol which was supported by original
Xorfor plugin was removed. It has been done from two reason - make it simple as possible and lack of hardware for testing.
Unfortunately the protocol doesn't transport all sensors which can be connected to PWS. It finaly means that temperature and humidity only from from two sensors 
can be used - Outdoor and Indoor. For more information about WU protocol see: https://support.weather.com/s/article/PWS-Upload-Protocol?language=en_US.

### Tested
* GARNI 2055 Arcus - All measured values from outdoor (7in1) unit are decoded; the data from the first radio sensor mark as Indoor is also decoded.

## Prerequisits

## Configuration
There are six parameter which have to be set up in Domoticz while new hadware is added:
* **Port** - TCP port which will listen for incomming http connection on Domoticz IP address
* **ID** - The ID (WU username) which is configured in PWS
* **Password** - The WU password configured in PWS config
* **Update timeout** - Maximal delay between update of domoticz devices if no new value is received
* **Always update** - All related domoticz devices will be updated in every single cycle - alway when correct update is received
* **Debug** - Switch on debug logging
