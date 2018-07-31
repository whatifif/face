# face
face recognition

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
```
$ export PATH=/usr/local/cuda-8.0/bin:$PATH
$ export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64/
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

