# Domoticz IP Weather Station plugin

This plugin allows you to grab meteo data localy from Personal Weather Station (PWS) via TCP/IP. There is no necesity to register to any Internet weather service. 
The plugin is based on similar Xorfor project. See: https://github.com/Xorfor/Domoticz-PWS-Plugin 

## Supported devices
The plugin supports all PWS hardware which uses Weather Undergroud (WU) protocol as a data transport solution. The Ecovitt protocol which was supported by original
Xorfor plugin was removed. It has been done from two reason - make it simple as possible and lack of hardware for testing. Unfortunately the protocol doesn't transport all sensors which can be connected to PWS. It finaly means that temperature and humidity only from two sensors can be used - Outdoor and Indoor. For more information about WU protocol see: https://support.weather.com/s/article/PWS-Upload-Protocol?language=en_US.

### Tested
* GARNI 2055 Arcus - All measured values from outdoor (7in1) unit are decoded; the data from the first radio sensor mark as Indoor is also decoded.

## Prerequisits
PWS have to be properly configured to send information to Domoticz IP address and port (see below). Unfortunately majority of PWSes have no possibility to configure destination IP address nor port - WU url is hadrcoded in firmware. There is possibility to configure IP address of the destination server in tested GARNI model but there is no possibility to change port. The solution for it is NAT. The traffic from PWS to WU have to be redirected to Domoticz IP and appropriate port on it. 
In my solution PWS is in isolated local network and all traffic manipulation is done on border router.

## Installation
1. Clone repository into your Domoticz plugins folder
    ```
    cd <PATH>/domoticz/plugins
    git clone https://github.com/Xorfor/Domoticz-PWS-Plugin.git
    ```
1. Restart domoticz
   
   installation without docker:
    ```
    sudo service domoticz.sh restart
    ```
   installation with docker:
    ```
    docker restart domoticz
    ```
   where domoticz is container name

## Configuration
There are six parameters which have to be set up in Domoticz while new hadware is added:
| Name                  | Description
| :---                  | :---
| **Port**              | TCP port on Domoticz IP address where plugin listens for incomming http connection from PWS
| **ID**                | The ID (WU username) which is configured in PWS
| **Password**          | The WU password configured in PWS config
| **Update timeout**    | Maximum delay between update of Domoticz devices if no new value is received
| **Always update**     | All related Domoticz devices will be updated in every single cycle - always when correct update is received from PWS; if this parameter is ON update timeout is ignored
| **Debug**             | Switch on debug logging

## Devices
The plugin will create list of devices which was adopted from original plugin. All of them are by default ativated. If you don't want to use all of them you can easily remove all unwanted ones.

| Name                     | Description
| :---                     | :---
| **Barometer (absolute)** | Pressure (absolute) in hPa
| **Barometer (relative)** | Pressure (relative) in hPa
| **Chill**                | Chill (calculated if missing)
| **Dew point**            | Dew point (calculated if missing)
| **Gust**                 | Gust
| **Heat index**           | Heat index (calculated if missing)
| **Humidity**             | Humidity
| **Humidity (indoor)**    | Humidity (indoor)
| **Rain**                 | Current rain rate and daily total
| **Rain rate**            | Current rain rate
| **Station**              | Format: [ip adress] ([software]): [Protocol] 
| **Solar radiation**      | Solar radiation
| **Temp + Hum**           | Temperature and humidity
| **Temperature**          | Temperature
| **Temperature (indoor)** | Temperature
| **THB**                  | Temperature, humidity and barometer (pressure and prediction)
| **UVI**                  | UV index
| **UV Alert**             | UV index + warning level (calculated)
| **Wind**                 | Wind direction, speed and gust
| **Wind**                 | Wind direction, speed, gust, temperature and gust
| **Wind direction**       | Wind direction
| **Wind Speed**           | Wind speed
