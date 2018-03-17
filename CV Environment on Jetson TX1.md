## Computer Vision Environment on Jetson TX1
### Cheap Deep Neural Network Device for $200 (+tax/shipping)

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

The architecture of Jetson devices is aarch64, which is different from other dominant computer architectures like x86-64 or arm64.  Because of the arch type and the way L4T on Jetson is setup, `apt-get update/upgrade` could break the system and make you do everything again from beginning.

To prevent this, type `sudo apt-mark hold xserver-xorg-core` in terminal.  
(You can undo this with `sudo apt-mark unhold xserver-xorg-core`)

See this link for detail: [https://elinux.org/Jetson_TK1](https://elinux.org/Jetson_TK1)

### Install Python and OpenCV

Although OpenCV 3.3 is included in JetPack 3.2 by default, it's somewhat fragile and not detected properly in my case.  
See this link for instruction Python & OpenCV 3.4 installation.  
[https://jkjung-avt.github.io/opencv3-on-tx2/](https://jkjung-avt.github.io/opencv3-on-tx2/)

We need a minor modification since this article is about OpenCV on TX2, not TX1.  
In one of comments (by Aaron) has a quick solution by changing the cuda version number from `cuda-8.0` to `cuda-9.0` like following.

`sudo vim /usr/local/cuda-8.0/include/cuda_gl_interop.h` to 
`sudo vim /usr/local/cuda-9.0/include/cuda_gl_interop.h`

It also suggests to change
`sudo apt-get purge libopencv4tegra-python libopencv4tegra-dev libopencv4tegra`
`sudo apt-get purge libopencv4tegra-repo`
to
`sudo apt-get purge libopencv-python libopencv-dev libopencv`
`sudo apt-get purge libopencv-repo`
but neither of these was needed in my case although I installed everything include opencv3.3 in Jetpack 3.2.

In addition to the instruction in the link, I had to install following libraries to clear missing package errors.
libavresample
`sudo apt-get install libavresample-dev`
libgphoto2
`sudo apt install gphoto2 libgphoto2*`

You may want to repeat any code several times to make sure there wasn't any error.

### Install Tensorflow, Jupyter and Keras
Download wheel file from here:  
[https://github.com/jetsonhacks/installTensorFlowJetsonTX/tree/master/TX1](https://github.com/jetsonhacks/installTensorFlowJetsonTX/tree/master/TX1)
then, `sudo pip install tensorflow-wheel-file`

`sudo pip install jupyter`
`sudo apt-get install libopenblas-dev`
`sudo pip install scipy`
`sudo pip install keras`
You can use `pip3` instead if `pip` doens't work.

### (Optional) Running from SD Card
Once everything's done, there's probably about size of 1GB space would be left on TX1's internal eMMC drive.  
You might want to migrate OS to external SD card. (or even external HDD or SSD)  
I havn't tried this yet but is definitely what I'm going to try next. 

[http://www.jetsonhacks.com/2017/01/26/run-jetson-tx1-sd-card/](http://www.jetsonhacks.com/2017/01/26/run-jetson-tx1-sd-card/)


[//]: # (Image References)
[image1]: http://docs.nvidia.com/jetpack-l4t/content/developertools/mobile/jetpack/images/jetpack_l4t_network_layout.008_600x441.png
