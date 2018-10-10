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
