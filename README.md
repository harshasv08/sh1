# ! ! ! U N D E R  C O N S T R U C T I O N ! ! !

## This document is work in progress!

# Open-source tools to connect and control your ‘Smart home’ via MQTT and Bluetooth
Sometimes it can be complicated to read certain sensors to see what is going on. In this code-pattern that is made simple, with only open-source technologies. This might not be an enterprise ready solution, but it shows how easy it is to use any device. So also, more professional devices can be used in similar ways.

When you have completed this code-pattern, you will understand how to:

* Connect sensors and actuators to an Arduino and read their values
* Set up a gateway on a Raspberry Pi
* Run a MQTT Server on a Raspberry Pi
* Connect sensors to a NodeMCU device and read their values (Optional)
* Build an application in Node-RED
* Use Bluetooth, WIFI and MQTT (and optional LoRAWan) to communicate between the devices
* Send messages to Slack

## Flow
![ArchitectureDiagram](images/SH_Architecture_DiagramV2.png)
 
1.	The smart home consists of 13 sensors and actuators connected to an Arduino-like device. This device has a extra board where all the components are connected to.
2.	The smart garden, which is a NodeMCU-device a sensor to control the garden (optional).
3.	Both devices are connected to a gateway, which sends and receives data. This gateway runs on a Raspberry Pi.
4.	The smart home has a bluetooth module and can be connected to a mobile device.
5.	Via a MQTT server the different components communicate with each other.
6  A Dashboard gives an overview of the status of the smart home and smart garden. The dashboard is connected to the gateway via MQTT. This dashboard runs on a local machine or on IBM cloud. This dashboard can be reached by mobile devices via WIFI.
7.	A camera is connected to the gateway to automatically take pictures when someone approaches the smart home.
8. Some of the notifications are being sent to Slack

## Included Components

* [Node-RED](https://nodered.org), open-source programming tool, where you easily can combine hardware devices, API's etc to build applications.
* [MQTT](https://mqtt.org), open-source protocol for sending messages.
* Bluetooth.
* [Arduino](www.arduino.cc), open-source micro processor.
* [Raspberry Pi](http://raspberrypi.org), credit card sized minicomputer.
* Sensors: Gas sensor, humidity sensor, light sensor, movement sensor,
* Actuators: LED's, fan, servo's, buttons, relay, LED display.
* Web camera, USB or Raspberry Pi camera.
* [Slack](http://Slack.com).
* Optional: Node-MCU, microprocessor.

## Featured technologies

* Node.js
* C++ for Arduino and Node-MCU

## Prerequisites

* [Node.js installation (with NPM)](https://nodejs.org/en/download/)
* [Arduino IDE](https://www.arduino.cc/en/software) (or use the web-editor) + libraries ****Mention Libraries****
* Familiarity with basic Arduino concepts
* Familiarity with basic Node-RED concepts
* Familiarity with basic Linux concepts

## Steps

Follow these steps to setup and run this code pattern. The steps are described in detail below.

1. Do some shopping (optional)
2. Clone the repo
3. Build your smart home and set up application
3a. Change code to view data on dashboard
4. Setup Node-RED on both Raspberry Pi's and local machine
5. Set up MQTT Broker
6. Set up Gateway
7. Build a dashboard
8. Optional Set-up Node-MCU

## Step 1 Do some shopping (Optional)



I used for this code pattern the following components:

* [*Keyestudio smart home set:*](https://www.keyestudio.com/products/keyestudio-smart-home-kit-withlus-board-for-arduino-diy-stem) this set includes a laser cut wooden house, with an Arduino clone with a sensor shield, Bluetooth board, sensors and actuators. This is available on Amazon but also at Ali-express etc. It is really good quality, with excellent instructions to build the house and to connect everything together. The needed code is available online. For every sensor/actuator is code available, and of course also for the complete set-up. This set is sold via different vendors, so look for the best price for you.

*	*Raspberry PI 1*: This house is connected to a gateway, I used a Raspberry Pi 4 for that, but this can also be a Raspberry Pi 3. This Raspberry acts as a gateway between the devices and the MQTT server. This gateway is also connected to the cloud or local machine. OPTIONAL: you can alsohost the gatway on another device, like your local machine.

* *Raspberry Pi 2*: This Raspberry Pi acts as a MQTT Broker. I use a Raspberry Pi 4 (can also be a Raspberry Pi 3) for that with a Sense HAT board. A Sense Hat is an additional board on top of an Raspberry Pi. It consists of a LED matrix and a joystick. This Sensehat is optional, I use it for displaying traffic going through the MQTT server on the LED Matrix. OPTIONAL: Instead of setting up a MQTT Broker yourself, you can also use a public broker for this or run a broker on another device.

* *Web camera*, this can be any USB camera or a Raspberry Pi camera.

* OPTIONAL: *NodeMCU*: there are different devices based on ESP8266, It is open source and relatively cheap and easy to work with. I am using a LoLin board, which has WIFI on board, I have connected a sensor to it to control my 'smart garden'

For this code pattern I used different pieces of hardware. To use all the possibilities I am going to mention in this Code pattern, I advise you to have all parts available. You can also build the functionalities in this code pattern with only having an Arduino with one sensor. All the parts running on the 2 Raspberry Pi's can also run on your laptop or on IBM Cloud.


## Step 2 Clone the repo

First let's get the code. From the terminal of the system, you plan on running Node-RED from, do the following:

Clone the XXXXXX repo:

$ git clone https://github.com/IBM/xxxxxxxxx
Move into the directory of the cloned repo:

$ cd xxxxxx
Note: For Raspberry Pi users, details on accessing the command line can be found in the remote access documentation if not connecting with a screen and keyboard.

## Step 3 Build your smart home and set up application

[Here](https://wiki.keyestudio.com/KS0085_Keyestudio_Smart_Home_Kit_for_Arduino) you can find all instructions to build the smart home. This tutorial is provided by Keyestudio.

You first get an introduction of all the parts of the complete set. Then you start with downloading the Arduino software, needed to program the micro controller. The instructions are based for Windows, but instructions for Apple are similar.

DRIVER FOR MAC NEEDED?? CHECK

Then to check if you can connect with the Arduino, you use a example sketch to test connectivity.
Next step is to install needed libraries for two of the components: 
 * LED display 
 * Servos. 
 
After doing this, you are good to go!

The tutorial then continues with a description of all the components and some sample code to test. There is also a good explanation of every piece of code available.

The last step before assembling the wooden house and the components, is to connect your IOS or Android device to the Bluetooth Module. 

You have to download an app, with this app you can control and start/stop some of the components. Later on in this code pattern you will build an alternative for this.

If the house is assembled, you need to connect all the wires from the components to the expansion board, in the tutorial you will see a table to connect the components to the right ports. 

When this is done, it is time to upload the code to control all the components, which is available in the last step of the tutorial.

When the sketch is uploaded, you can test all the different components one by one to see if they are connected in the right way.

FYI, I did not connect the servo from the window in the right way: it opens when the water sensor gets activated....

## Step 3a Change code to view data on dashboard 

You can use this smarthome like you configured it as above, but to connect it to the gateway and make data vissible to the dashboard you need to change the code.
These changes where being made:


***xxxx add code snippets  and explain xxxxxx***

## Step 4 Set up Node-RED


## Step 5 Set up MQTT Broker

MQTT is a lightweight and simple messaging protocol, therefore, you need a broker which receives and sends messages based on a certain topic. If you want to read more about MQTT, please go here: https://mqtt.org
In this step I used a Raspberry Pi for an MQTT Broker. You can also host it locally on your laptop or use a test-broker as found on the web.
I used Mosquito as this is the most used on Raspberry, but basically you can use any broker.

To install, use the following command: ```sudo apt install mosquitto mosquitto-clients```

Start the broker and automatically start after reboot using the following command:-
```
sudo systemctl enable mosquitto
```
The broker should now be running. You can check this via the systemd service status:-
```
sudo systemctl status mosquitto
```
The output should be similar as the following:
```
pi@rpiMqttServer:~ $ sudo systemctl status mosquitto
● mosquitto.service - LSB: mosquitto MQTT v3.1 message broker
   Loaded: loaded (/etc/init.d/mosquitto; generated; vendor preset: enabled)
   Active: active (running) since Thu 2020-11-12 13:17:10 CET; 4 days ago
     Docs: man:systemd-sysv-generator(8)
  Process: 331 ExecStart=/etc/init.d/mosquitto start (code=exited, status=0/SUCCESS)
    Tasks: 1 (limit: 4915)
   CGroup: /system.slice/mosquitto.service
           └─444 /usr/sbin/mosquitto -c /etc/mosquitto/mosquitto.conf

Nov 12 13:17:07 rpiMqttServer systemd[1]: Starting LSB: mosquitto MQTT v3.1 message broker...
Nov 12 13:17:10 rpiMqttServer mosquitto[331]: Starting network daemon:: mosquitto.
Nov 12 13:17:10 rpiMqttServer systemd[1]: Started LSB: mosquitto MQTT v3.1 message broker.
```
Now it is time to test the broker. Therefor you need to subscribe to an MQTT topic.

A topic is simply a string that looks like a file system path. It has the general form:-

a/b/c/...

The great thing about MQTT is that you can just make up topics which describe your needs. You don’t need to register them anywhere. In this test we use ```test/message```
In the existing terminal, subscribe to the test/message topic:

```mosquitto_sub -h localhost -t "test/message"```

This will send a message to the MQTT broker which is currently running on the same system (-h localhost option). But it could be running somewhere else.


Because your current terminal is listening to the topic, you will need to open another terminal. 

Once open, publish message to the test/message topic like this:

``` mosquitto_pub -h localhost -t "test/message" -m "Hello, world" ```
If you look back at the first terminal now you should see this:

```Hello, world```

if this works, your MQTT Broker is working!

Optional:

I added a [Sense HAT](https://www.raspberrypi.org/products/sense-hat/?resellerType=home) to the Raspberry Pi to make visual when messages are being send. A Sense HAT is an additional board on top of a Raspberry Pi. It consists of sensors, joystick and a LED matrix. Every time a message goes through the broker, an image is being displayed on the LED Matrix of the Sense HAT. 

For displaying, I created an application in Node-RED  for that:
![MQTT Flow](images/SH_MQTT_Flow.png)


<< explain flow here >>

The flow can be found [here](/flows/MQTT_flow)

## Step 6 Set up Gateway

In this step you wil create a simple flow. This flow is needed to send and recieve data (via MQTT) from the connected devices to a dashboard, wich runs locally or in the cloud.

![MQTT Flow](images/SH_Gateway_Flow.png)

The flow can be found [here](/flows/Gateway_flow)

## Step 7 Build a Dashboard

This dashboard receives data from the connected devices, especially from some sensors. You can also start these sensors and take images to see what is going on around the house.

![Dashboard](images/SH_Dashboard.png)

To get the data on the dashboard you need to create a flow:


<img src="images/SH_Local_Flow.png" width="50%" height="50%"/>

The flow can be found [here](/flows/Local_flow)

## Step 8 Optional Set-up Node-MCU

The code is available here
I attached a soil moisture sensor to the NodeMCU it sends its data via MQTT to the gateway to the dashboard

## Links

## License

This code pattern is licensed under the Apache License, Version 2. Separate third-party code objects invoked within this code pattern are licensed by their respective providers pursuant to their own separate licenses. Contributions are subject to the [Developer Certificate of Origin, Version 1.1](https://developercertificate.org/) and the [Apache License, Version 2](https://www.apache.org/licenses/LICENSE-2.0.txt).

[Apache License FAQ](https://www.apache.org/foundation/license-faq.html#WhatDoesItMEAN)


