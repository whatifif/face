# face
cuda and opencv installation for face recognition  
https://www.pyimagesearch.com/2017/09/27/setting-up-ubuntu-16-04-cuda-gpu-for-deep-learning-with-python/


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
==> When tried another installation ubuntu 16.04, this error did not show up anymore.


## 1. install cuda 8.0 on ubuntu 16.04
0. NVIDIA CUDA Installation Guide for Linux  
https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ubuntu-installation

1. download cuda 8 version: Tensorflow uses this version.  
https://developer.nvidia.com/cuda-80-ga2-download-archive  
I chose "deb" method instead of "run" method. "run" method gave errors while installation.
Installation Instructions:
```
`sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb`
`sudo apt-get update`
`sudo apt-get install cuda`
```
```
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-cublas-performance-update_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```
==> 
```
sudo apt-get install cuda
Reading package lists... Done
Building dependency tree       
Reading state information... Done
cuda is already the newest version (8.0.61-1).
The following package was automatically installed and is no longer required:
  libllvm5.0
Use 'sudo apt autoremove' to remove it.
0 to upgrade, 0 to newly install, 0 to remove and 2 not to upgrade.
```


2. Reboot the system to load the NVIDIA drivers.
NVIDIA driver is now downgraded to 384.130 after installation of cuda 8.0

3. after installation  
https://www.pyimagesearch.com/2017/09/27/setting-up-ubuntu-16-04-cuda-gpu-for-deep-learning-with-python/  
Now that the NVIDIA CUDA driver and tools are installed, you need to update your ~/.bashrc  file to include CUDA Toolkit (I suggest using terminal text editors such as vim , emacs , or  nano ):
Add the following to the end of .bashrc file.
```
sudo nano ~/.bashrc
```

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
------------------------------------------------------ bad
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
 ==> The result is different from pyimagesearch.

==>  So opencv 3.3.0 is tried. The result is what is expected.
```
-- 
--   Python 2:
--     Interpreter:                 /usr/bin/python2.7 (ver 2.7.12)
-- 
--   Python 3:
--     Interpreter:                 /home/whatif/anaconda3/bin/python3 (ver 3.6.6)
-- 
--   Python (for build):            /usr/bin/python2.7
```
==> import cv2 failed.
==> So lets try virtualenv instead of anaconda

3. conda install
https://anaconda.org/conda-forge/opencv
To install this package with conda run one of the following:
```
conda install -c conda-forge opencv 
conda install -c conda-forge/label/broken opencv 
```
======================================================

## Create your Python virtual environment
1. install pip
```
$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo python get-pip.py
$ sudo python3 get-pip.py
```

2. Installing virtualenv and virtualenvwrapper

```
$ sudo pip install virtualenv virtualenvwrapper
$ sudo rm -rf ~/.cache/pip get-pip.py
```
3. add to .bashrc

- open bashrc
```
sudo nano ~/.bashrc
```

- add the following
```
# virtualenv and virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
```

- reload bashrc
```
source ~/.bashrc
```

4. Creating the dl4cv virtual environment
```
$ mkvirtualenv dl4cv -p python3
```
5. Verifying that you are in the “dl4cv” virtual environment
```
$ workon dl4cv
```

6. Installing NumPy
```
pip install numpy
```

## from now on, always work under this "dl4cv" virtualenv

## 5. Compile and Install OpenCV

1. get opencv 3.3.0
```
$ cd ~
$ wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.3.0.zip
$ wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.3.0.zip
```
```
$ unzip opencv.zip
$ unzip opencv_contrib.zip
```

2. cmake
```
$ cd ~/opencv-3.3.0/
$ mkdir build
$ cd build
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D WITH_CUDA=OFF \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.3.0/modules \
    -D BUILD_EXAMPLES=ON ..
 ```
 3. if "configuration error" occurs, reboot and try again.
 
 4. Compiling OpenCV
 ```
 $ make -j4
 ```
 ```
 $ sudo make install
 $ sudo ldconfig
 $ cd ~
```

 5. Symbolic linking OpenCV to your virtual environment
 
 ```
 $ cd ~/.virtualenvs/dl4cv/lib/python3.5/site-packages/
 $ ln -s /usr/local/lib/python3.5/site-packages/cv2.cpython-35m-x86_64-linux-gnu.so cv2.so
 $ cd ~
```

6. Testing your OpenCV 3.3 install
```
$ python
>>> import cv2
>>> cv2.__version__
'3.3.0'
```
 
 
 
 
