# Railroad crossing example with JETANK

Jetbot is an open source AI Robot based on the Nvidia Jetson Nano ([Jetbot Repository](https://github.com/NVIDIA-AI-IOT/jetbot)).

This program uses collision avoidance and road following examples from jetbot.

Program moves jetbot to right place and knows when to stop if you have well trained models for those and it detects train with colors or movement so make sure the background dont have same color as your train have or there is no other movement. Also you can use both same time and use them to detect other vehicles also.

Repository has some example images for those models.

## Table of Contents

- [Requirements](#requirements)
- [Collision avoidance](#collision-avoidance)
- [Road following](#road-following)
- [Usage](#usage)
- [Maintainers](#maintainers)

## Requirements

Program requires jetbot as a hardware but if you want to use servos then you need JETANK as a hardware and as a software it requires pre-built jetbot SD card image ([jetbot image](https://jetbot.org/master/software_setup/sd_card.html)).

Program is build with Jetson Nano (4GB) SD card image from there which has 4.5 JetPack version and 0.4.3 JetBot version.

## Collision avoidance

  **Note**:When taking images for model, I lowered the camera little bit with command and import to get better results.
  
  ```from SCSCtrl import TTLServo```
  
  ```TTLServo.servoAngleCtrl(5,10,1,150)```

1. You need to train your collision avoidance model which contains free and blocked classes. Blocked class was modified to stop class in this program but if you dont change it then you have to change stop class stuff in my program to blocked class stuff. ```Free``` images consist something where robot can go and ```stop``` images consist images where it should stop. Use data_collection_with_stop_class.ipynb for collecting ```stop``` and ```free``` classes that I provided or you can use jetbot own data_collection.ipynb. 

  **Note**:Also add images when train is coming through when robot is stopped so robot stays stopped when trains comes.

2. Then you train this model in train_model_resnet18.ipynb which helps robot to understand when to stop
3. In live_demo_build_trt.ipynb you optimize the trained model using TensorRT for faster inference.

## Road following

**Note**:When taking images for model, I lowered the camera little bit with command and import to get better results
  
  ```from SCSCtrl import TTLServo```
  
  ```TTLServo.servoAngleCtrl(5,10,1,150)```

1. Collect images which consist image coordinates x and y where robot should go, you can use gamepad to get those images also like I used in this program.
2. After that you train your model in train_model.ipynb wihch uses also Resnet18 and it predicts where robot should go with those coordinates.
3. Then you optimize the trained model by using TensorRT for faster inference in live_demo_build_trt.ipynb.

## Usage

**Note**:If you dont have servos you can remove those from notebook

1. When you have those both models trained to trt models then you must put those both scripts inside the program folder and check that those model names are correct when executing program.
2. After that you can use program to detect train or other moving object with colors which are currently blue or/and yellow or movement or both, you can comment other out if you want only one option.
3. You can change those color values and you can change stop threshold value also to trigger easier because program has very small threshold.

  **Note**: Speed values are zero so when executing program you have to adjust those speed values. For video I used speed gain 0.30 and steering gain 0.05.
  
  **Note**: When using colors to detect moving train check that daylight dont cause problems because it can cause problems especially with blue color.

## Maintainers

[Kalle Nurminen] (https://github.com/KalleN98)  
