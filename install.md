# face
face recognition

## 0. Install Ubuntu system dependencies
```
$ sudo apt-get update
$ sudo apt-get upgrade
```

if upgrade error occurs:
```
sudo apt-get upgrade --fix-missing
```

```
$ sudo apt-get install build-essential cmake git unzip pkg-config
$ sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
$ sudo apt-get install libxvidcore-dev libx264-dev
$ sudo apt-get install libgtk-3-dev
$ sudo apt-get install libhdf5-serial-dev graphviz
$ sudo apt-get install libopenblas-dev libatlas-base-dev gfortran
$ sudo apt-get install python-tk python3-tk python-imaging-tk
```

```
sudo apt-get install python2.7-dev python3-dev
```

```
$ sudo apt-get install linux-image-generic linux-image-extra-virtual
$ sudo apt-get install linux-source linux-headers-generic
```

error occurs while "sudo apt-get install linux-image-generic linux-image-extra-virtual"
```
Adding boot menu entry for EFI firmware configuration
done
Setting up linux-image-extra-4.4.0-131-generic (4.4.0-131.157) ...
run-parts: executing /etc/kernel/postinst.d/apt-auto-removal 4.4.0-131-generic /boot/vmlinuz-4.4.0-131-generic
run-parts: executing /etc/kernel/postinst.d/dkms 4.4.0-131-generic /boot/vmlinuz-4.4.0-131-generic
Error! Your kernel headers for kernel 4.4.0-131-generic cannot be found.
Please install the linux-headers-4.4.0-131-generic package,
or use the --kernelsourcedir option to tell DKMS where it's located
Error! Your kernel headers for kernel 4.4.0-131-generic cannot be found.
Please install the linux-headers-4.4.0-131-generic package,
or use the --kernelsourcedir option to tell DKMS where it's located
run-parts: executing /etc/kernel/postinst.d/initramfs-tools 4.4.0-131-generic /boot/vmlinuz-4.4.0-131-generic

```


## 1. install cuda 8.0 on ubuntu 16.04
0. NVIDIA CUDA Installation Guide for Linux  
https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ubuntu-installation

1. download cuda 8 version: Tensorflow uses this version.  
https://developer.nvidia.com/cuda-80-ga2-download-archive  
I chose "deb" method instead of "run" method. "run" method gave errors while installation.

2. Reboot the system to load the NVIDIA drivers.

3. after installation  
https://www.pyimagesearch.com/2017/09/27/setting-up-ubuntu-16-04-cuda-gpu-for-deep-learning-with-python/  
Now that the NVIDIA CUDA driver and tools are installed, you need to update your ~/.bashrc  file to include CUDA Toolkit (I suggest using terminal text editors such as vim , emacs , or  nano ):
Add the following to the end of .bashrc file.

```
# NVIDIA CUDA Toolkit
export PATH=/usr/local/cuda-8.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64/
```

4. verify the installation
Now, reload your ~/.bashrc  ( source ~/.bashrc ) and then test the CUDA Toolkit installation by compiling the deviceQuery  example program and running it:
```
$ source ~/.bashrc
$ cd /usr/local/cuda-8.0/samples/1_Utilities/deviceQuery
$ sudo make
$ ./deviceQuery
deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 8.0, CUDA Runtime Version = 8.0, NumDevs = 1, Device0 = Tesla K80
Result = PASS
```
Note: Calling source on ~/.bashrc only has to be done once for our current shell session. Anytime we open up a new terminal, the contents of ~/.bashrc  will be automatically executed (including our updates).

At this point if you have a Result = PASS , then congratulations because you are ready to move on to the next step.

5. check nvcc version  
```
$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2016 NVIDIA Corporation
Built on Tue_Jan_10_13:22:03_CST_2017
Cuda compilation tools, release 8.0, V8.0.61
```

## 2. install cuDNN 
Download cuDNN v6.0 (April 27, 2017), for CUDA 8.0

Next, untar the file and then copy the resulting files into lib64  and  include  respectively, using the -P  switch to preserve sym-links:
```
$ cd ~
$ tar -zxf cudnn-8.0-linux-x64-v6.0.tgz
$ cd cuda
$ sudo cp -P lib64/* /usr/local/cuda/lib64/
$ sudo cp -P include/* /usr/local/cuda/include/
$ cd ~
```

## 3. Create your Python virtual environment
I will use anaconda instead of virtualenv  
https://conda.io/docs/user-guide/install/linux.html
To avoid the error in launching spyder, update conda.
```
conda update --all
conda update spyder
```
1. create conda environment named "dl4cv" and use it.
```
conda create -n dl4cv python=3.6
source activate dl4cv
```

2. install numpy
```
conda install numpy
```

## 4. Compile and Install OpenCV  
I used the opencv 3.4.1 instead of 3.3.0

```
$ cd ~/opencv-3.4.1/
$ mkdir build
$ cd build
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D WITH_CUDA=OFF \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.4.1/modules \
    -D BUILD_EXAMPLES=ON ..
    
 ```

