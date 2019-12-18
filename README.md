# TensorFlow Lite Python classification example with Pi Camera
## My notes
NOTE:: Pillow and numpy installation on Raspberry-Pi requires some dependencies that are no automatic. Refer to [this issue](https://github.com/numpy/numpy/issues/14532#issuecomment-549165359) and [this issue](https://github.com/python-pillow/Pillow/issues/3077#issuecomment-469078718)


This example uses [TensorFlow Lite](https://tensorflow.org/lite) with Python
on a Raspberry Pi to perform real-time image classification using images
streamed from the Pi Camera.

Although the TensorFlow model and nearly all the code in here can work with
other hardware, the code in `classify_picamera.py` uses the [`picamera`](
https://picamera.readthedocs.io/en/latest/) API to capture images from the Pi
Camera. So you can modify those parts of the code if you want to use a different
camera input.


## Set up your hardware

Before you begin, you need to [set up your Raspberry Pi](
https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up) with
Raspbian (preferably updated to Buster).

You also need to [connect and configure the Pi Camera](
https://www.raspberrypi.org/documentation/configuration/camera.md).

And to see the results from the camera, you need a monitor connected
to the Raspberry Pi. It's okay if you're using SSH to access the Pi shell
(you don't need to use a keyboard connected to the Pi)—you only need a monitor
attached to the Pi to see the camera stream.


## Install the TensorFlow Lite runtime

In this project, all you need from the TensorFlow Lite API is the `Interpreter`
class. So instead of installing the large `tensorflow` package, we're using the
much smaller `tflite_runtime` package.

To install this on your Raspberry Pi, follow the instructions in the
[Python quickstart](https://www.tensorflow.org/lite/guide/python).
Return here after you perform the `pip install` command.


## Download the example files

First, clone this Git repo onto your Raspberry Pi like this:

```
git clone https://github.com/tensorflow/examples --depth 1
```

Then use our script to install a couple Python packages, and
download the MobileNet model and labels file:

```
cd examples/lite/examples/image_classification/raspberry_pi

# The script takes an argument specifying where you want to save the model files
bash download.sh /tmp
```


## Run the example

```
python3 classify_picamera.py \
  --model /tmp/mobilenet_v1_1.0_224_quant.tflite \
  --labels /tmp/labels_mobilenet_quant_v1_224.txt
```

You should see the camera feed appear on the monitor attached to your Raspberry
Pi. Put some objects in front of the camera, like a coffee mug or keyboard, and
you'll see the predictions printed. It also prints the amount of time it took
to perform each inference in milliseconds.

For more information about executing inferences with TensorFlow Lite, read
[TensorFlow Lite inference](https://www.tensorflow.org/lite/guide/inference).
