# face
face recognition  
https://www.pyimagesearch.com/2018/06/18/face-recognition-with-opencv-python-and-deep-learning/

project files: ubuntu-store/project-20180727-1-face

Original code can be obtained from the Author or Blog

## Our face recognition dataset
![dataset](https://github.com/whatifif/face/raw/master/images/build_face_dataset_jurassic_park.jpg "dataset")

## Face recognition project structure
```
cd face-recognition-opencv
```

## Encoding the faces using OpenCV and deep learning
```
python encode_faces.py --dataset dataset --encodings encodings.pickle
```

## Recognizing faces in images
```
python recognize_faces_image.py --encodings encodings.pickle \
	--image examples/example_01.png
```
## Recognizing faces in video
You should connect webcam to your computer

```
python recognize_faces_video.py --encodings encodings.pickle \
	--output output/webcam_face_recognition_output.avi --display 1
```
## Face recognition in video files
```
python recognize_faces_video_file.py --encodings encodings.pickle \
	--input videos/lunch_scene.mp4 --output output/lunch_scene_output.avi \
	--display 0
```
=> Around 4 min video takes around 4 min processing with GTX 1080 Ti. This shows a real-time processing.


