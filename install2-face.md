
## Face recognition with OpenCV, Python, and deep learning
https://www.pyimagesearch.com/2018/06/18/face-recognition-with-opencv-python-and-deep-learning/


#### installation of dlib with GPU support
Installing dlib with GPU support (optional)
If you do have a CUDA compatible GPU you can install dlib  with GPU support, making facial recognition faster and more efficient.
For this, I recommend installing dlib  from source as you’ll have more control over the build:

$ workon <your env name here> # optional
$ git clone https://github.com/davisking/dlib.git
$ cd dlib
$ mkdir build
$ cd build
$ cmake .. -DDLIB_USE_CUDA=1 -DUSE_AVX_INSTRUCTIONS=1
$ cmake --build .
$ cd ..
$ python setup.py install --yes USE_AVX_INSTRUCTIONS --yes DLIB_USE_CUDA

#### Install the face_recognition package
The face_recognition module is installable via a simple pip command:
Face recognition with OpenCV, Python, and deep learningShell

$ workon <your env name here> # optional
$ pip install face_recognition

#### Install imutils
You’ll also need my package of convenience functions, imutils. You may install it in your Python virtual environment via pip:

$ workon <your env name here> # optional
$ pip install imutils
  
