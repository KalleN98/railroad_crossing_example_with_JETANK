# Railroad crossing example with JETANK

Jetbot is an open source AI Robot based on the Nvidia Jetson Nano ([Jetbot Repository](https://github.com/NVIDIA-AI-IOT/jetbot))
This program uses collision avoidance and road following examples from jetbot. Program detects train with colors so make sure the background dont have same color as your train have.

## Table of Contents

- [Requirements](#requirements)
- [Collision avoidance](#collision-avoidance)
- [Road following](#road-following)
- [Usage](#usage)
- [Maintainers](#maintainers)

## Requirements

Program requires jetbot as a hardware and as a software it requires pre-built jetbot SD card image ([jetbot image](https://jetbot.org/master/software_setup/sd_card.html)).
Program is build with Jetson Nano (4GB) SD card image from there which has 4.5 JetPack version and 0.4.3 JetBot version.

## Collision avoidance

1. You need to train your collision avoidance model which contains free and blocked classes. Blocked class was modified to stop class in this program but it is not necessary to change it. ```Free``` images consist something where robot and ```blocked``` images consist images where it should stop. Use data_collection.ipynb for that. 

  **Note**:Also add images when train is coming through when robot is stopped so robot stays stopped when trains comes.

2. Then you train this model in train_model_resnet18.ipynb which helps robot to understand when to stop
3. In live_demo_build_trt.ipynb you optimize the trained model using TensorRT for faster inference.

## Road following

1. Collect images which consist image coordinates x and y where robot should go, you can use gamepad to get those images also like I used in this program.
2. After that you train your model in train_model.ipynb wihch uses also Resnet18 and it predicts where robot should go with those coordinates.
3. Then you optimize the trained model by using TensorRT for faster inference in live_demo_build_trt.ipynb.

## Usage

1. After you have those both models trained to trt models then you must put those both scripts inside the program folder and check those model names are correct when executing program.
2. After that you can use my program to detect train with colors. 

  **Note**: Speed values are zero so when program is executed you have to adjust those speed values when robot moves to the place where it should stop.

## Maintainers

[Kalle Nurminen] (https://github.com/KalleN98)  
