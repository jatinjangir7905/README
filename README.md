# README
Computer Vision Projects with OpenCV
A collection of real-time computer vision projects built with Python, OpenCV, NumPy, and YOLOv5 ONNX.
This repository contains two projects:
Phone & Pen Detector – detects mobile phones using YOLOv5 and identifies pen-like objects using image-processing techniques.
Harry's Cloak (Invisibility Cloak) – removes a blue cloth from the live webcam feed and replaces it with a previously captured background.
📁 Projects
1. Phone & Pen Detector
A real-time webcam-based object detection project.
Features
Real-time webcam input
Mobile phone detection using a YOLOv5 ONNX model
Pen detection using:
Grayscale conversion
Gaussian blur
Canny edge detection
Contour analysis
Aspect-ratio filtering
Solidity filtering
Hough line detection
Non-Maximum Suppression (NMS) for YOLO detections
Displays the number of detected phones and pens
Displays real-time FPS
Configurable confidence and NMS thresholds
The detector loads yolov5s.onnx and coco.names, with configurable camera and detection thresholds.
Required files
phone-pen-detector/
├── project.py
├── yolov5s.onnx
└── coco.names
Configuration
The main settings are:
ONNX_MODEL = "yolov5s.onnx"
COCO_NAMES = "coco.names"
CONF_THRESH = 0.4
NMS_THRESH = 0.45
CAMERA_ID = 0
The source code uses OpenCV's DNN module to load the ONNX model and processes webcam frames in real time.
2. Harry's Cloak
A computer-vision implementation of an invisibility cloak effect using a blue cloth.
The program first captures the background while the user is outside the camera frame. It then detects the blue color using an HSV mask and replaces the detected blue region with the previously captured background.
Processing pipeline
Webcam
   ↓
Capture Background
   ↓
Convert Frame to HSV
   ↓
Gaussian Blur
   ↓
HSV Color Thresholding
   ↓
Median Blur + Morphological Operations
   ↓
Find Largest Blue Component
   ↓
Create Inverse Mask
   ↓
Combine Current Frame + Background
   ↓
Invisibility Cloak Effect
The default HSV trackbar values are tuned for a blue cloth and can be adjusted while the program is running.
Required file
harrys-cloak/
└── projecto.py
🛠️ Technologies Used
Python 3
OpenCV
NumPy
YOLOv5
ONNX
Computer Vision
Image Processing
Real-Time Webcam Processing
⚙️ Installation
Clone the repository:
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
Install the Python dependencies:
pip install opencv-python numpy
For the Phone & Pen Detector, make sure the YOLOv5 ONNX model and COCO class-name file are present in the same directory as project.py.
▶️ How to Run
Phone & Pen Detector
python project.py
The webcam window will show:
Detected phones with bounding boxes
Detected pens with bounding boxes
Phone count
Pen count
FPS
Press:
Q
or
ESC
to exit.
Harry's Cloak
python projecto.py
Steps
Start the program.
Move out of the webcam frame.
Allow the program to capture the background.
Enter the frame with a blue cloth.
The blue cloth will be replaced by the captured background.
Two windows are displayed:
Harry's Cloak – final invisibility effect
Mask – shows the detected blue region
Controls
Key
Action
Q
Quit
B
Capture the background again
The HSV values can also be adjusted using the trackbars in the bars window.
🎯 Learning Objectives
These projects demonstrate practical applications of:
Object detection
Image segmentation
Color-space conversion
Edge detection
Contour detection
Morphological image processing
Feature-based object detection
Neural-network inference with ONNX
Real-time video processing
Webcam-based computer vision
🔍 How the Phone Detector Works
The YOLOv5 model produces object predictions from each webcam frame. The program calculates class confidence using objectness and class scores, filters detections using the confidence threshold, converts bounding boxes to the original frame coordinates, and applies NMS.
For phones, the detected class label is checked for "phone" or "cell" before displaying the detection.
Pens are detected separately using geometric/image-processing heuristics rather than the YOLO model.
🪄 How Harry's Cloak Works
The cloak project uses the HSV color space because hue, saturation, and value make color-based segmentation convenient.
A binary mask is created for the selected blue range:
mask = cv2.inRange(hsv_blur, lower_hsv, upper_hsv)
The mask is cleaned using median filtering and morphological opening/closing. The largest connected contour is retained to reduce unwanted noise.
The final image is produced by combining:
The current frame everywhere except the blue cloth
The captured background where the blue cloth is detected
⚠️ Limitations
Phone & Pen Detector
Detection quality depends on the YOLOv5 model and camera conditions.
Pen detection is heuristic-based and may detect other long, thin objects.
Lighting and object orientation can affect detection.
CUDA acceleration requires a compatible OpenCV build and GPU setup.
Harry's Cloak
The cloak works best with a clearly visible blue cloth.
Lighting changes can affect HSV segmentation.
Other blue objects in the scene may also be detected.
The background should remain relatively unchanged after capture.
The effect works best with a stationary camera.
🚀 Possible Future Improvements
Train a custom YOLO model specifically for phones and pens.
Add object tracking across video frames.
Improve pen detection using a trained object-detection model.
Add a graphical user interface.
Save detection statistics to a CSV/database.
Add multiple color-cloak support.
Improve background replacement using segmentation.
Add automatic HSV calibration.
Add GPU acceleration where supported.
📂 Suggested Repository Structure
computer-vision-projects/
│
├── README.md
│
├── phone-pen-detector/
│   ├── project.py
│   ├── yolov5s.onnx
│   └── coco.names
│
└── harrys-cloak/
    └── projecto.py
👨‍💻 Author
Jatin
B.Tech – Artificial Intelligence & Machine Learning
⭐ Project Purpose
These projects were developed to explore practical applications of computer vision and demonstrate how traditional image-processing techniques can be combined with deep-learning-based object detection for real-time applications.
