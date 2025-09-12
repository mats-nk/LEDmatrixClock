# LED Matrix Clock a.k.a. Marquee Scroller (Clock, Weather, and More)

The main feature for this MAX7219 LED dot matrix is to display time and weather for you. The project is based on the ESP8266 MCU and MAX7219 LED driver and featching time via NTP and weather from the Open Weather Map API.

## NOTICE
This fork enhances the Qrome Marquee Scroller version 3.03 from february 2023, that was developed during 2018-2022 period.

For more information and development history visit [Qrome Marquee Scroller](https://github.com/Qrome/marquee-scroller) and read his [README](https://github.com/Qrome/marquee-scroller/blob/master/README.md).

Read the [feature enhancements below](#feature-enhancements)


## Features include:
* Accurate Clock refresh from Internet Time Servers
* Display Local Weather and conditions (refreshed every 10 - 30 minutes, configurable)
* Configured through Web Interface
* Basic Authorization to access Configuration web interface
* Update firmware through web interface over WiFi (OTA)
* Configurable scroll speed and LED brightness
* Configurable data display and data update interval frequency
* Configurable sleep / wake times
* Configurable number of LED-matrix tiles (4 to >8) (compile option) and
  types of Clock Displays on larger panels, e.g. also display seconds or temperature
* Video: https://youtu.be/DsThufRpoiQ
* Build Video by Chris Riley: https://youtu.be/KqBiqJT9_lE

## Feature Enhancements
Enhancements included in [THIS repository](https://github.com/rob040/LEDmatrixClock) :
* Removed the TimeZoneDB.com registration requirement.
* Actual time zone information is used from OpenWeather API.
* Added Time NTP and more efficient time strings instead.
* Update to new OpenWeatherMap.org API. Newly requested Free Service API-keys can no longer use the older call and structure.
* Reduce RAM usage. The ESP8266 is an older WiFi processor with limited RAM (80kB), especially when compared to its newer ESP32 members.
* Added MQTT support with basic Authentication, to send message to be displayed. Message is displayed immediately when display shows the time, and repeated every minute with default configuration.
* Use VScode IDE with PlatformIO / PIOarduino, for better development and maintenance experience and much better build environment and library version control.
* Improved start-up on time synchronisation and weather data update,
* Improved weather data display on webpage (minor changes)
* Automatic timezone (from Local weather), hence no need for TimeZoneDB.
* Added a favicon for easy recognition in your browser.
* Support for different display sizes without re-compilation, via configuration page (device will reboot upon change).
* Using the 'LittleFS' filesystem in stead of the deprecated 'SPIFFS' filesystem
* Using ArduinoJson upgraded to version 7
* Webpage now has switchable dark-mode view
* Webpage now has switchable automatic page update
* Instead of scrolling text, there is also a static display mode for short messages, date, temperature or humidity only next to the time display.
* Weather Location lookup has been made simpler; there is no longer the need to lookup the City-ID code; just enter a (valid) city name with optional 2-letter country code. Also GPS coordinates are now allowed as location input.
* Added a display QUIET time config option, where the display can be Off or Dimmed or Dimmed with no Motion (ie. no scrolling, no blinking)
* Replaced Wifi_manager with ESP_WiFiManager_Lite library, which allows multiple WiFi Accesspoints (SSID's) to be (pre-)configured, which is handy for a portable device. It also provides a fallback if one WiFi station goes down.

### known issues
* Webpage update does halt the scrolling display for a moment. See [issue #8](https://github.com/rob040/LEDmatrixClock/issues/8) for more details.
* Scrolling text appears to have some 'flex' in it. See [issue #9](https://github.com/rob040/LEDmatrixClock/issues/9) for more details.
* When using the LED display at lowest intensity, some pixel flicker might be visible. See [issue #10](https://github.com/rob040/LEDmatrixClock/issues/10) for more details.


## Required Parts:
* Wemos LOLIN D1 Mini ESP8266: https://www.wemos.cc/en/latest/d1/d1_mini.html
  Other EXP8266 boards based on [ESP12(-E,-F)](https://components101.com/sites/default/files/component_pin/ESP12E-Pinout.png) module, such as the NodeMCU, shall work equally well, only the 3D print models are more or less bound to the D1-mini physical dimensions.
* MAX7219 LED Dot Matrix Module 4-in-1 Display (FC16) for Arduino. Commonly available from Chinese webshops, or Ebay or Amazon.com.


## Wiring for the Wemos D1 Mini to the LED Dot Matrix Display

| LED | D1 mini   |
| --- | ---       |
| VCC | 5V        |
| GND | G (GND)   |
| CLK | D5 (SCK)  |
| CS  | D6        |
| DIN | D7 (MOSI) |

The Connections in a picture:
<p align="left" title="Wires from D1-mini to LED display">
  <img src="/images/marquee_scroller_pins.png" width="400"/>
</p>
Be aware that the display in above picture is actually upside-down; when viewed from front, the data input DIN is at the right hand side; the text on the PCB is usually upside-down.


## 3D Printed Case by David Payne:
Original Single Panel version: https://www.thingiverse.com/thing:2867294 <br>
Double Wide LED version: https://www.thingiverse.com/thing:2989552

<p align="left" title="STL models from Thingiverse">
  <img src="/images/Thingiverse-stl-base.png" width="400"/>
  <img src="/images/Thingiverse-stl-back.png" width="400"/>
</p>

<p align="left" title="Marquee Scroller parts">
  <img src="/images/marquee-allparts.jpg" width="270"/>
  <img src="/images/marquee-backplate.jpg" width="270"/>
  <img src="/images/marquee-lit.jpg" width="260"/>
</p>
<p align="left" title="Makes from Thingiverse">
  <img src="/images/20171105_124635.jpg" width="200"/>
  <img src="/images/20171017_075241.jpg" width="200"/>
  <img src="/images/20171105_125913.jpg" width="200"/>
  <img src="/images/20171022_214044.jpg" width="200"/>
</p>
<p align="left" title="Makes from Thingiverse">
  <img src="/images/20180128_091534.jpg" width="200"/>
  <img src="/images/20180128_091524.jpg" width="200"/>
  <img src="/images/20180128_091552.jpg" width="200"/>
  <img src="/images/20180127_135828.jpg" width="200"/>
</p>

## Compiling and Loading to Wemos D1 Mini (ESP8266)
### Using Arduino 2.x IDE
It is no longer recommended to use the Arduino IDE. It might be difficult to get the right library versions together, especially when using it also for other Arduino projects.<br>
Still, the main sketch filename (marquee.ino) and source directory name (marquee) is kept such that this project can be build in the Arduino IDE. This might change in the future.
* Support for ESP8266 Boards is included in Arduino v2.x
* Select Board:  "ESP8266" --> "LOLIN(WEMOS) D1 R2 & mini"
* Set Flash Size: 4MB (FS:1MB OTA:~1019KB)
* Select the **Port** from the tools menu.

### Loading Supporting Library Files in Arduino
Use the Arduino guide for details on how to install and manage libraries https://www.arduino.cc/en/Guide/Libraries

**Packages** -- the following packages and libraries are used (download and install):
* <TimeLib.h> --> https://github.com/PaulStoffregen/Time v1.6.1+
* <Adafruit_GFX.h> --> https://github.com/adafruit/Adafruit-GFX-Library v1.12.1+ (and Adafruit BusIO at version 1.17.2+)
* <ArduinoJson.h> -->  https://github.com/bblanchon/ArduinoJson v7.4.2+
* <PubSubClient.h> --> https://github.com/hmueller01/pubsubclient3 v3.2.0+

**local libraries**
This project has local libraries in the lib directory.
Having project local libraries is not supported by Arduino IDE.
Therefore you must copy these manually to your Arduino sketchbook library directory. This is the directory where all libraries managed by the Arduino library manager are located.<br>
By default this is `C:\Users\<userName>\Documents\Arduino\libraries` on Windows machines.

Copy local libraries:
* in command terminal, change to marquee directory,
* `xcopy/s ..\lib\* C:\Users\<userName>\Documents\Arduino\libraries`

Assure there are no similarly named libaries (/packages) with higher version numbers.
Use library manager to check. At end of compilation in the IDE, a list of used libraries is shown. Check these.


## Building with PlatformIO.
Use [**VScode**](https://code.visualstudio.com/docs) with [**PlatformIO**](https://platformio.org/) or better, its desendant fork [**PIOarduino**](https://marketplace.visualstudio.com/items?itemName=pioarduino.pioarduino-ide) extension.

Please refer to the provided links on how to install VScode on your OS.

Then, open this project with `Visual Studio Code`, via File --> Open Folder: select folder containing `platformio.ini` file.

The `platformio.ini` file contains the references to the required external libraries and version numbers.

To build, open the `pioarduino` or `platformio` extension (icon on left hand side bar), then under *PROJECT TASKS* -> *Default* -> *General* : select **Build** and then **Upload**

## Initial Configuration
Editing the **Settings.h** file is not required but optional to get different default values.
All settings and API Keys are managed from the Web Interface.

* Open Weather Map free service API key: http://openweathermap.org/  -- this is used to get weather data and the current time zone from the selected City. This API key is required for correct time.

**NOTE:** The settings in the Settings.h are the default settings for the first loading. After loading you will manage changes to the settings via the Web Interface. If you want to change settings again in the settings.h, you will need to erase the file system on the Wemos or use the `Reset Settings` option in the Web Interface.

## Web Interface
The Marquee Scroller uses the **WiFiManager** so when it can't find the last network it was connected to,
it will become an **Access Point Hotspot** -- connect to it with your phone at http://192.168.4.1/ and you can then enter your WiFi connection information.
This is shown on the LED display.

After connected to your WiFi network it will display the IP address assigned to it and that can be
used to open a browser to the Web Interface.  You will be able to manage your API Keys through the web interface.

The default user / password for the configuration page is: admin / password

The Clock will display the local time of the City selected for the weather after a short synchronization period.

<p align="left" title="the (old) webinterface on a phone">
  <img src="/images/20180419_065805.png" width="200"/>
  <img src="/images/20180419_065815.png" width="200"/>
  <img src="/images/20180419_065832.png" width="200"/>
  <img src="/images/20180419_065858.png" width="200"/>
</p>


## Contributors
David Payne <br>
Nathan Glaus <br>
Daniel Eichhorn -- Author of the TimeClient class (in older versions) <br>
yanvigdev <br>
nashiko-s <br>
magnum129 <br>
rob040  --  author of this repo and these [feature enhancements listed above](#feature-enhancements)<br>


Contributing to this software is warmly welcomed. You can do this basically by forking from master, committing modifications and then making a pulling requests against the latest DEV branch to be reviewed (follow the links above for operating guide). Detailed comments are encouraged. Adding change log and your contact into file header is encouraged. Thanks for your contribution.

When considering making a code contribution, please keep in mind the following goals for the project:
* User should not be required to edit the Settings.h file to compile and run.  This means the feature should be simple enough to manage through the web interface.
* Changes should always support the recommended hardware (links above).

<p title="Marquee Scroller">
  <img src="/images/ScrollingClock.jpg" width="400"/>
</p>
