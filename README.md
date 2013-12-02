galileo-mqtt-lwm2m
==================

Galileo MQTT and LWM2M demo. 

This demo uses LWM2M device management protocol to control the Intel Galileo Board. Using the LWM2M server (web interface), a new application is uploaded to the board at run-time using TFTP. The application is reads the analog pins A0, A1 and A2 and uses MQTT to transmit the values to the MQTT broker, which can be showed in web application. 

If the pins A0 and A1 are connected to the VBAT and Solar panel pins of the Solar Shield v2.0, the program transmits the battery and solar panel voltages. 

List of Programs
================

The following programs are required for this demo:

* LWM2M - Device Management
  * Client/Server (console interface): https://github.com/ismagom/lwm2m-galileo
  * Server (with web interface): https://github.com/ismagom/leshan-galileo

* MQTT - Application
  * Broker: anyone works, e.g. mosquitto (http://mosquitto.org/)
  * Client: https://github.com/ismagom/mqtt-galileo-solar-sensor
  * Panel (web interface): https://github.com/ismagom/mqtt-galileo-panel

Instructions
=============


1) Compile all required programs. The LWM2M and MQTT clients must be compiled in the Galileo board. 

2) Setup the TFTP server in the host. 

3) Copy the test binary from the MQTT client to the TFTP server home directory.

4) Run leshan server

5) Run LWM2M client in the Galileo board, indicate IPv6 address of the leshan server. You should see in the client console how it connects to the server. 

6) In a browser, open http://127.0.0.1:8080/ (or the leshan server address). 

7) Click on the client. In the Objects list, find the Application object and set:

   a) WRITE to name: "test"
   
   b) WRITE to URL: "tftp://ip.of.tftp.server/test" 
   
   c) EXEC Download
   
   d) WRITE to args: "ip.of.mqtt.broker"
   
   e) EXEC Run
   
8) Run the mqtt-galileo-panel and see the MQTT message update the web interface. 


System Diagram
===============

This is how the whole system looks like:

![diagram](https://raw.github.com/ismagom/galileo-mqtt-lwm2m/master/system_setup.png)

Contact
=======

For any help, comments or suggestion: gomezi@tcd.ie


