# PiBike
### A ROS based Sensor Plattform

The PiBike project was created by Tim P. J. Schimansky over the course of his master thesis in 2022.

## Hardware

The hardware consists of the following parts:

- Logging-Unit
	- Power supply and distribution
	- Raspberry Pi
	- User Interface
	- Real-Time-Clock
- Side-Sensor-Unit
	- Qumox SJCAM5000
	- Ultrasonic distance sensor 
- Smartphone
	- Hardware requirements
	- Neccessary App

### Logging-Unit

The Logging-Unit combines all the core components of the system into a single, easy to install platform.

Image here

The Logging-Unit is self sufficient as it can work without any othe components. Depending on the Setup, it wont be very useful.

#### Power supply and distribution

The Unit is currently powered by an 12V (3S LiPo) Battery, that can deliver at least 2.5A. This Battery does power everything apart from the Smartphone. The Battery needs a LiPo-Checker, to protect the cells for overdischarge.

```diff
+ The Logging-Unit is going to be reworked to accept 12V over USB-C PD
```

The power runs through a fuse and is then passed through a buck converter to convert it down from 12V to 5V. The Fan as well as other peripheral devices may use the 12V supply directly. The Raspberry Pi gets its power through the GPIO-Pinheader

#### Raspberry Pi

The Raspberry Pi is a 4th gen model B with 8GB of RAM. The OS is installed on an SD Card. Due to the usage of ROS, Ubuntu 18.04LTS Server is used. Currently, there is only one Raspberry Pi. In theory, two Raspberry Pis (or other devices) could work in tandem for larger workloads. The Device is started by plugging in the battery. Right after powering up, the fan wil blow air violently onto the Raspberry Pi. When the fan tunes down to a more reasonable speed, the Raspberry Pi is fully started.

#### User interface

Ontop of the fan, there is a pcb including a button, a switch as well as a small 128 times 64 px OLED screen (through i2c). The button is used to shut down the Raspberry Pi safely without corrupting the SD-card. The switch is used to turn on the autostart of ROS on boot. The Display is for showing the status of the Pi to the user. It displays the IPs (both for wireless and wired connections), the CPU temperature as well as the Boot mode selected by the swich.

```diff
+ There might be a record button and indicator coming if needed
```

#### Real-Time-Clock

The RTC-Module is hooked up via i2c and is used to recover the current time after the Rasperry Pi has restarted. The Raspberry Pi does not contain any internal method of keeping time, while not being supplied with power.

### Side-Sensor-Unit

```diff
! ToDo
```

### Samrtphone

```diff
! ToDo
```

## Usage

The current supported usecase is to connect the side sensors as well as the phone and collect all their data.

### Procedure

- Check, that the selection switch on the top of the device is set to "ROS"
- Plug in the Storage device and the two USB cables coming from the side sensors.
- Plug in the power supply (battery or other) to start up the system.
- Wait until system is fully started (noticable by observing the fan as it reaches reasonable speeds when fully started and by looking at the display as it will show text, when fully started). Check the screen if the ROS-Mode is active, otherwise, the ROS Nodes are not active.
- As soon as the Raspberry Pi is fully started, the wireless hotspot will be available.
- Connect the phone to the hotspot. Depending on the brand of phone it may warn you, that this wireless connection does not provide internet access. You will need to accept this, as it may disconnect you otherwise.
- Open the "ROS All Sensors"-App and type in the wireless IP from the Raspberry Pis display. Check "Sensors" instead of "All Sensors". Then press connect. The phone will now stream all available sensors to the ROS master.
- The system is now fully set up.
- This can be confirmed, by minimising the "ROS All Sensors"-App and opening the IP at port 8000 in your browser (ususally 10.42.0.1:8000). This will open the webinterface to give an overview over all active Topics and Nodes. The recording of Data can be started from here.

### Settings

To change setting, files need to be manipulated at some point in the system.

#### Add a new Node for some Sensor

This follows the standard working principle of ROS as there is a "catkin-workspace" in the home directory of the ubuntu user. This contains all the nodes. To add a note, please follow the recomended way of ROS.

To autostart the Node, it has to be included in the ROSlaunch file "placeholder".

#### Add a new Topic to be recorded or change the directories

The recording of the Topics is handled by the Node "ROS_bike_remote_bag_logging". The ROSlaunch file "remote_bag_logging.launch" does contain a parameter called "topic_list", that contains the list of all Nodes to be recorded.

To change the directories to record the data into, the other two prameters are used. There is an internal and an external path. The internal path is only used if the external path cannot be reached.

#### Add a different storage device

The current external drive is mounted to a specific path via its device identifier. A new drive needs to be configured properly to a specified mounting point. 
