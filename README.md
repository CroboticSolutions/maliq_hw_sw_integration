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

## micro-ROS

In order to build microROS follow this [instructions](https://micro.ros.org/docs/tutorials/core/first_application_linux/). 

#### When building micro-ROS 

When building firmware, **DO NOT** source `/opt/ros/$ROS_DISTRO/setup.bash`, **DO** source `dev_ws/install/setup.bash`

When building agent(with agent_ws), **DO** source `/opt/ros/$ROS_DISTRO/setup.bash`, **DO NOT** source `dev_ws/install/setup.bash`

You'd better remove any setup like source `/opt/ros/$ROS_DISTRO/setup.bash` in your `~/.bashrc`. 

#### Adittional info

If output of the: 
```
ros2 run micro_ros_setup create_agent_ws.sh
```
is: 
```
[ros2run]: Process exited with failure 6
[ros2run]: Process exited with failure 6
```

device is not connected to the internet. 


#### Relevant info 

micro-ROS build duration: 
* `firmware_build` : 30 min
* `micro_ros_agent` : 5 min


## Serial 

Add administrative privileges to the serial port as: 
```
sudo chmod 777 /dev/ttyAMA0 
```

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

If the agent is running output is: 
```
[1701472247.113546] info     | TermiosAgentLinux.cpp | init                     | running...             | fd: 3
[1701472247.114296] info     | Root.cpp           | set_verbose_level        | logger setup           | verbose_level
```

#### publish msg to topic as

```
ros2 topic pub /cmd_vel geometry_msgs/msg/Twist "linear:
  x: 4.5
  y: 6.0
  z: 0.0
angular:
  x: 0.0
  y: 0.0
  z: 0.0" 
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