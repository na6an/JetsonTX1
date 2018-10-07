# JetsonTX1, an affordable way to begin machine learning
## Cheap Deep Neural Network Device for $200 (+tax/shipping)

---
### Intro

Training Deep Neural Network without GPU could be frustrating.  
There is no GPU on my laptop, and price for computers with useful GPU is sky rocketed because crypto-currency mining inflated GPU price. 

AWS EC2 GPU instance is another option but costs about $1 every hour. One day I thought I stopped it but didn't realize until the next day when I found out it wasn't stopped, ended up getting charged more than ten for doing nothing.

So, I searched for the best valued option with an affordable physical device, but yet strong GPU power enough to run DNN.
Then, I found one-time developer discount option on Jetson TX1 from Nvidia for $200.  
(which normally is around $450~500 on Amazon)  
[http://www.nvidia.com/object/JetsonTX1DeveloperKitSE.html](http://www.nvidia.com/object/JetsonTX1DeveloperKitSE.html)

### Install JetPack & Setup
It's recommended to flash TX1 with latest Jetpack from Nvidia website.  
[https://developer.nvidia.com/embedded/jetpack](https://developer.nvidia.com/embedded/jetpack)  

See following video for the complete installation process.
[https://www.youtube.com/embed/DyhRMjaUknQ](https://www.youtube.com/embed/DyhRMjaUknQ)

Assuming following network option was selected, you might have to log-in in TX1 and setup wifi first before the installer can find the TX1's ip address.

![alt text][image1]

The architecture of Jetson devices is aarch64, which is different from other dominant computer architectures like x86-64 or arm.  Because of the arch type and the way L4T on Jetson is setup, `apt-get update/upgrade` could break the system and make you do everything again from beginning.

To prevent this, type `sudo apt-mark hold xserver-xorg-core` in terminal.  
(You can undo this with `sudo apt-mark unhold xserver-xorg-core`)

See this link for detail: [https://elinux.org/Jetson_TK1](https://elinux.org/Jetson_TK1)

### (Optional) Connecting Bluetooth Devices (Wireless Keyboard/Mouse)
I had trouble connecting a bluetooth keyboard to TX1.  
Following a method described in this page worked for me: https://devtalk.nvidia.com/default/topic/1028526

### (Optional) Running from SD Card
Once everything's done, there's probably about size of 1GB space would be left on TX1's internal eMMC drive.  
You might want to migrate OS to external SD card. (or even external HDD or SSD)   
[http://www.jetsonhacks.com/2017/01/26/run-jetson-tx1-sd-card/](http://www.jetsonhacks.com/2017/01/26/run-jetson-tx1-sd-card/)

[//]: # (Image References)
[image1]: http://docs.nvidia.com/jetpack-l4t/content/developertools/mobile/jetpack/images/jetpack_l4t_network_layout.008_600x441.png
