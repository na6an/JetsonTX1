# Running Lidar on Jetson TX1

## Background
Lidar became a famous sensor since the self-driving cars earned popularity.  
However, it is usually very expensive; Commercial lidars cost thousands.  
Even some non-commercial, short-distance lidars easily cost hundreds.  
Because of this pricing, it's not easy for amateur hobbysts and robotists to buy one and play around.

Neato is a company known for its robot vacuums attaching a lidar.  
Neato's XV lidar is one of the cheapest lidars on the aftermarket - detached from the robot vacuums.  
The range of this lidar on the robot vacuums is relatively short up to 10m, but the cost is much cheaper at around $90~100.  
Available at Amazon:  
https://www.amazon.com/Neato-LIDAR-Laser-distance-sensor/dp/B00QSUJPSY

This is why there is a wide usage of this particular product as an entry lidar among robotics community.  
There are several tutorials about connecting lidar on raspberry pi.
In this project, I'm going to do it on Jetson TX1.

## Hardware Setting
There are two ways to do this.  

One is to use direct wiring to TX1 gpio pins.  
Following is a document with detailed specification of TX1, including information on gpio pins:  
https://www.jetsonhacks.com/nvidia-jetson-tx1-j21-header-pinout/  
Here is a quick, easier version:  
https://developer.nvidia.com/embedded/downloads#?search=board%20design&tx=$product,jetson_tx1

Second is using a lidar controller.  
There is an online, DIY robotics marketplace where they sell customized lidar controllers specifically for XV lidar.  
https://www.getsurreal.com/product/lidar-controller-v2-0/ (Teensy)

In this setting, I'm going to discuss second method first.  
It costs little more for the controller but is relatively easier.  

There is a step-by-step tutorial here:  
http://roboticsweekends.blogspot.com/2017/12/how-to-connect-neato-xv-11-lidar-to.html

Now, the tutorial above is connecting XV lidar-arduino(lidar controller)-RPi-host computer(running rviz).  
I'm going to skip RPi and use TX1 instead of host computer.  

1. Download firmware from here:  
https://github.com/getSurreal/XV_Lidar_Controller  
Upload it to Teensy controller using Arduino IDE.  
Before upload the firmware, make sure to install Teensyduino add-on.  
https://www.pjrc.com/teensy/td_download.html

<img src="https://github.com/na6an/JetsonTX1/blob/master/pic/arduino.PNG" alt="alt text" width="400" height="240">

2. Assuming ROS already installed on TX1, install lidar driver.  
```
sudo apt install ros-kinetic-xv-11-laser-driver  
mkdir -p xv-11/src; cd xv-11/src  
git clone https://github.com/rohbotics/xv_11_laser_driver.git  
cd ..; catkin_make
```

3. Run ROS and rviz  
```
roscore&  
rosrun xv_11_laser_driver neato_laser_publisher _port:=/dev/ttyACM0 _firmware_version:=2  
rviz
```

4. Configure rviz  
Add "LaerScan" from Add button, select "/scan" from LaserScan topic, and type "neato_laser" at the fixed frame.

Result:  
![gif](https://github.com/na6an/JetsonTX1/blob/master/pic/result.gif) 

