# human-detection

The goal of this project is to detect the presence of a human within a given input source and inform the user if a human is indeed detected. The input source is based on the user's preference, and it can be a single image, a video, or a live video feed from a camera. In the real world, the most likely use of this project would be a live camera feed because it can be used as a security camera with an additional capability of being able to alert users if a human is within the camera's field of view.

## The Algorithm

The algorithm is a machine learning algorithm. The specific one used in this project is a retrained resnet18 model. The resnet18 model is retrained using a modified version of the training algorithm used in https://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html. This technique, known as transfer learning, is ideal because it allows us to take advantage of important parts of the original resnet18 model and use it to help us successfully classify images based on whether a human is present or not. The number of epochs was increased from the original values of the python training script to increase accuracy. The model used by the user is in a .onnx format so it can be easily used by the machine learning interface to successfully provide an output to the user. The human-detection folder, which includes training and testing images, serves as the input to train the resnet18 model and allow it to recognize patterns to help predict user-provided inputs when the final version is being used.

## Running this project

1. Add steps for running this project.
2. Make sure to include any required libraries that need to be installed for your project to run.

1. Download the "human-detection" directory from Github.
2. Download any libraries needed depending on the input source. If the input is a photo or video, download PyTorch to access the python file imagenet.py. If the input is a camera, depending on the connection type (CSI, USB, etc.), you may have to download additional libraries.
3. Open your computer's console.
4. If not previously completed, change directories to human-detection.
5. In the console, type "NET=models/human-detection" and run.
6. After that, type "DATASET=data/human-detection" and run.
7. For an image or video file, type "imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/human-detection/image.jpg image_name.jpg where "image.jpg" is the input file and "image_name.jpg" is what you would like to call the new file. The new file will have a label over it that identifies the image as either "human detected" or "no human detected".
8. For a camera, type "imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt path/to/camera" where path/to/camera is the directory housing the camera module. This depends on the type of connection between the computer and the camera. After a script runs for about 45 seconds, the console will continuously output lines with computer statistics starting with "[TRT]", as well as two lines starting with "class 0000" and "class 0001". The former represents when no human is detected, and the latter represents when humans are detected. A numerical value is assigned to each, and 0 represents 0% confidence while 1 represents 100% confidence. If the 2nd line is close to 1, that means the model has detected a human in the camera's field of view.

