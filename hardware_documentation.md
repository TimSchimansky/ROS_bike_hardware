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

- The Logging-Unit is going to be reworked to accept 12V over USB-C PD

The power runs through a fuse and is then passed through a buck converter to convert it down from 12V to 5V. The Fan as well as other peripheral devices may use the 12V supply directly. The Raspberry Pi gets its power through the GPIO-Pinheader

#### Raspberry Pi

The Raspberry Pi is a 4th gen model B with 8GB of RAM. The OS is installed on an SD Card. Due to the usage of ROS, Ubuntu 18.04LTS Server is used. Currently, there is only one Raspberry Pi. In theory, two Raspberry Pis (or other devices) could work in tandem for larger workloads. The Device is started by plugging in the battery. Right after powering up, the fan wil blow air violently onto the Raspberry Pi. When the fan tunes down to a more reasonable speed, the Raspberry Pi is fully started.

#### User interface

Ontop of the fan, there is a pcb including a button, a switch as well as a small 128 times 64 px OLED screen (through i2c). The button is used to shut down the Raspberry Pi safely without corrupting the SD-card. The switch is used to turn on the autostart of ROS on boot. The Display is for showing the status of the Pi to the user. It displays the IPs (both for wireless and wired connections), the CPU temperature as well as the Boot mode selected by the swich.

- There might be a record button and indicator coming if needed

#### Real-Time-Clock

The RTC-Module is hooked up via i2c and is used to recover the current time after the Rasperry Pi has restarted. The Raspberry Pi does not contain any internal method of keeping time, while not being supplied with power.

### Side-Sensor-Unit

! ToDo

### Samrtphone

## ToDo

