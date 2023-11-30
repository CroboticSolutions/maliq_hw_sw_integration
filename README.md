# ow-sw-hw-integration

Repository dedicated to the integration of the upper-level and the lower-level software. 

#### rPI  

Dedicated to the ROS 2 (joystick, control, perception)  

#### arduino  

Dedicated to low-level control (battery system, drive system, ligthing system...)

### Run joystick with 

[joystick-drivers git repo](https://github.com/ros-drivers/joystick_drivers)


```
ros2 run joy joy_node 
```

### Run teleop_twist_joy

[teleop-twist-joy git repo](https://github.com/ros2/teleop_twist_joy)
```
ros2 launch teleop_twist_joy teleop-launch.py joy_config:='xbox'
```


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

Current IP of the crobot is: `192.168.1.5`

And connection is possible with: 
``` 
ssh crobot@192.168.1.5
password: crobot
``` 

Create static IP of the PC that's connected as: `192.168.1.x,` 
gateway is `192.168.1.1`

## How to connect to WiFi over SSH: 

Run following command to list all of the available networks: 
```
nmcli device wifi list
```

Output is: 
```
IN-USE  BSSID              SSID                MODE   CHAN  RATE        SIGNAL  BARS  SECURITY  
        B6:99:7B:6F:1F:2A  --                  Infra  6     130 Mbit/s  100     ▂▄▆█  WPA2      
        1C:9E:CC:D1:09:98  TCHA90A5ZR          Infra  11    405 Mbit/s  55      ▂▄__  WPA2 WPA3 
        00:CB:7A:A2:4E:88  TCH3P8S84A          Infra  1     405 Mbit/s  49      ▂▄__  WPA2 WPA3 

```

Choose one you need and connect to it with:

```
sudo nmcli device wifi connect <BSSID> password <PASSWORD>
```

## Serial 

UART --> GPIO 14/15 (`/dev/ttyAMA0`)
[More info](https://jason19970210.medium.com/raspberry-pi-4-with-multiple-uart-interface-4eac75f74d7c)

[Running microROS over serial port](https://micro.ros.org/docs/tutorials/core/first_application_rtos/freertos/)

Command to start `micro_ros_agent` over serial port is: 
```
ros2 run micro_ros_agent micro_ros_agent serial --dev /dev/ttyAMA0
```

[Github issue with micro_ros_agent cmd](https://github.com/micro-ROS/micro_ros_arduino/issues/1105)

Run `micro_ros_agent` over serial as: 
```
ros2 run micro_ros_agent micro_ros_agent serial --dev /dev/ttyAMA0 -b 115200
```

## Resources used

[Serial connection rPI](https://www.abelectronics.co.uk/kb/article/1035/serial-port-setup-in-raspberry-pi-os)


### Maintainer 

Current maintainer is fzoric8@gmail.com

## TODO: 

Todo list for the initial HW-SW integration. 

#### System

- [x] Edit README.md (formatting)
- [x] Enable WiFi connection for the development
- [x] Build exemplary microROS on the rPI
- [ ] Check serial connection of the rPi and the Arduino 
- [ ] Setup serial communication for the microROS comms
- [ ] Create .rc scripts to start microROS after turning on 

#### ROS 2 control 

- [x] Enable ros2_joy for the logitech joystick control
- [x] Test initial funcitonality joy node 
- [x] Test initial functionality teleop_twist_joy node
- [ ] Enable upper-level control simple PID or pure-pursuit
- [ ] Think of the sensory placement for the autonomous control 
- [ ] Define initial SW arch for the testing phases
- [ ] Write all necessary packages for the automatic deployment on the ROS 2
- [ ] Fix joy to cmd_vel mapping 