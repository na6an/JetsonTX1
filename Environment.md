## Setup Computer Vision / Machine Learning Environment on Jetson TX1
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
Then, `sudo pip install tensorflow-wheel-file`  
`sudo pip install jupyter`  
`sudo apt-get install libopenblas-dev`  
`sudo pip install scipy`  
`sudo pip install keras`  
You can use `pip3` instead if `pip` doens't work.

[//]: # (Image References)
[image1]: http://docs.nvidia.com/jetpack-l4t/content/developertools/mobile/jetpack/images/jetpack_l4t_network_layout.008_600x441.png
