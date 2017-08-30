# Android Things Alarm Panel for Home Assistant

This project is a MQTT Alarm Control Panel for use with [Home Assistant's Manual Alarm Control Panel](https://home-assistant.io/components/alarm_control_panel.manual_mqtt/) component. This project was built for a Raspberry Pi 3 using Android Things and a 7" Touchscreen Display.

The hardware alarm panel acts as an interface for Home Assistant's manual alarm control panel component. You can set the alarm state to away or home, or disarm the alarm using a code. In addition it has some nice features such as weather forecast and screen saver mode.

MQTT allows for communication between the hardware alarm panel and the manual alarm panel. The hardware alarm panel interface will reflect the current state of the manual alarm control panel component and vice versa. However, Home Assistanat is responsible for triggering the alarm through automation and sensor states.

For example, in my home I have several Z-Wave door sensors and a Z-Wave siren connected to Home Assistant using a Z-Wave USB dongle. I setup automations in HASS that will set the state of the manual alarm panel component to be triggered if any of the senors states change while the alarm is set to away or home. This will update the hardware alarm panel interface as well as a trigger the siren unless I enter the alarm code.

![alarm_home](https://user-images.githubusercontent.com/142340/29889460-9f615642-8d9a-11e7-99a6-1a49529dd580.png)

![alarm_weather](https://user-images.githubusercontent.com/142340/29889463-9f64e550-8d9a-11e7-8d06-cbb046588875.png)

![alarm_arm](https://user-images.githubusercontent.com/142340/29889458-9f33509e-8d9a-11e7-8bdf-aaad28d94328.png)

![alarm_disarm](https://user-images.githubusercontent.com/142340/29889459-9f557980-8d9a-11e7-996e-dcbfd54d44cc.png)

![alarm_pending](https://user-images.githubusercontent.com/142340/29889461-9f62d238-8d9a-11e7-9a0f-77baf385d812.png)

![alarm_triggered](https://user-images.githubusercontent.com/142340/29889462-9f6422dc-8d9a-11e7-923a-06cfcd6acff7.png)


# Hardware

Raspberry Pi 3 and SD Card.
[7" Touchscreen Display for display](https://www.adafruit.com/product/2718).
[5V Buzzer](https://www.adafruit.com/product/1536) for button feedback and sounds.

# Software

- [Android Things 0.4.1-devpreview for Raspbery Pi 3](https://developer.android.com/things/hardware/raspberrypi.html)
- [MQTT Android library for the Paho Android Service](https://github.com/eclipse/paho.mqtt.android)
- [PMW Speaker Drivers for Android Things](https://github.com/androidthings/drivers-samples/tree/master/pwmspeaker)
- Android Studio with Android SDK N or above.

# Home Assistant Setup

I won't go into detail about how to setup Home Assistant with MQTT because the Home Assistant documentation covers this. I will just list the required steps needed to get up and running quickly.

- Setup [Home Assistant](https://home-assistant.io/getting-started/)
- Configure the [MQTT service](https://home-assistant.io/components/mqtt/) and broker for Home Assistant not your broker address and username/password if applicable.
- Add the [MQTT Alarm Control Panel] (https://home-assistant.io/components/alarm_control_panel.manual_mqtt/) to your Home Assistant configuraiton and just use the default settings for now.
- Add any components or sensors (like Zwave door sensors or sirens) and configure automations to trigger the alarm.

# Raspberry PI Setup

Make sure you properly setup the RPi3 with the 7" Touchscreen Display.
Connect the buzzer as shown in the [sampel diagram](https://github.com/androidthings/drivers-samples/tree/master/pwmspeaker).
Setup your RPi3 to use [Android Things 0.4.1-devpreview for Raspbery Pi 3](https://developer.android.com/things/hardware/raspberrypi.html). Be sure to setup network access either using WiFi or ethernet.

# Software Setup

The easiest way to get up and running is to download the APK from the [release](https://github.com/thanksmister/androidthings-mqtt-alarm-panel/releases/tag/v1.3) section and side load the app onto the device using the ADB tool. However if you want build the application from the code you can clone the repository and compile the application using Andoid Studio.

- Hook the device to your computer using a USB cable and connect with the ADB tool adb connect Android.local.
- Side load the application apk file from the download section using the ADB tool adb install mqtt_alarm_panel.apk

# Initial Alarm Setup

- Under the settings (gear icon) enter the MQTT information that you configured in Home Assistant for your MQTT service.
- Be sure you adjust the time intervals to match those set (other than defaults) in the Home Assistant MQTT alarm control panel.
- If you choose to get weather updates, enter your DarkSky API key and location (lat/lon) in the weather setting screen.
- To use a screen saver other than the digital clock, turn this feature on in the screen saver settings. Optionally you can load other Instagram images by change the Instagram profile name in the settings.

# Enclosures

It would be nice to have a wall mountable or free standing enclosure for the project once completed. I 3D printed an enclosure so I could mount mine on the wall https://www.thingiverse.com/thing:1082431. However you can also use any enclosure that will fit the RPi3 and 7" Touchscreen display combo.

# Notes

- At this time there is an issue dimming the brighness of the backlight for the display. So for now I have included a screen saver feature as a short-term fix until the bug is addressed by the Android Things development team.
- There have been multiple display issues using Android Things 0.5.0 and 0.5.1, therefore this application runs best under 0.4.1.
- It's important that the hardware alarm control panel settings reflect the settings of those used in the alarm control panel component. Initially the hardware control panel is set to the default settings of the alarm control panel component. There are settings to change the hardware control panel to match those used in the HASS alarm panel if changed.

# Acknowledgements

Special thanks to Colin O'Dell who's work on the Home Assistant Manual Alarm Control Panel component and his [MQTT Alarm Panel](https://github.com/colinodell/mqtt-control-panel) helped make this project possible.

# Licensing
========
Copyright (c)  2017. ThanksMister LLC
 
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License. 
You may obtain a copy of the License at
  
http://www.apache.org/licenses/LICENSE-2.0
  
Unless required by applicable law or agreed to in writing, software distributed 
under the License is distributed on an "AS IS" BASIS, 
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. 
See the License for the specific language governing permissions and 
limitations under the License.