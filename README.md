# ow-sw-hw-integration

Repository dedicated to the integration of the upper-level and the lower-level software. 

#### rPI  

Dedicated to the ROS 2 (joystick, control, perception)  

#### arduino  

Dedicated to low-level control (battery system, drive system, ligthing system)

## Setting up rPI: 

Following steps are necessary to set up rPI: 
1. Install Ubuntu 
2. Install necessary packages such as net-tools 
3. Add static IP adress
4. Build ROS 2
5. Build microROS
6. Add bash script for autonomous start of the ROS 2 nodes on the startup 


## How to connect: 

It is possible to connect on the rPI by attaching ethernet cable from PC to the 
crobot and use SSH. 

Current IP of the crobot is: 192.168.1.5

And connection is possible with: 

ssh crobot@192.168.1.5
password: crobot

Create static IP of the PC that's connected as: 192.168.1.x, 
gateway is 192.168.1.1

## Resources used

[Serial connection rPI](https://www.abelectronics.co.uk/kb/article/1035/serial-port-setup-in-raspberry-pi-os)


## TODO: 

- [] Edit README.md (formatting)
- [] Check serial connection of the rPi and the Arduino 
- [] Build exemplary microROS on the rPi 
- [] Create .rc scripts to start microROS after turning on 
- [] Enable ros2_joy for the logitech joystick control
- [] Enable upper-level control simple PID or pure-pursuit
- [] Think of the sensory placement for the autonomous control 
- [] Enable internet over LAN for development 
- [] Write all necessary packages for the automatic deployment on the ROS 2