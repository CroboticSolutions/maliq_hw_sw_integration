# ow-sw-hw-integration

Repository dedicated to the integration of the upper-level and the lower-level software. 

#### rPI  

Dedicated to the ROS 2 (joystick, control, perception)  

#### arduino  

Dedicated to low-level control (battery system, drive system, ligthing system...)

### Run joystick with 

[joystick-drivers git repo](https://github.com/ros-drivers/joystick_drivers)

ros2 run joy joy_node 

### Run teleop_twist_joy

[teleop-twist-joy git repo](https://github.com/ros2/teleop_twist_joy)

ros2 launch teleop_twist_joy teleop-launch.py joy_config:='xbox'

### Transport drivers git repo 

[transport-drivers git repo](https://github.com/ros-drivers/transport_drivers)

UDP, Serial, IO context 


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

### Maintainer 

Current maintainer is fzoric8@gmail.com

## TODO: 

Todo list for the initial HW-SW integration. 

#### System

- [] Edit README.md (formatting)
- [] Check serial connection of the rPi and the Arduino 
- [] Build exemplary microROS on the rPi 
- [] Setup serial communication for the microROS comms
- [] Create .rc scripts to start microROS after turning on 
- [] Enable internet over LAN for development 

#### ROS 2 control 

- [x] Enable ros2_joy for the logitech joystick control
- [] Enable upper-level control simple PID or pure-pursuit
- [] Think of the sensory placement for the autonomous control 
- [] Define initial SW arch for the testing phases
- [] Write all necessary packages for the automatic deployment on the ROS 2
- [x] Test initial funcitonality joy node 
- [x] Test initial functionality teleop_twist_joy node
- [] Fix joy to cmd_vel mapping 