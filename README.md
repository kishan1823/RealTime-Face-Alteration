# faceit_live3
This is an update to http://github.com/faceit_live using [first order model](https://github.com/AliaksandrSiarohin/first-order-model) by Aliaksandr Siarohin to generate the images. This model only requires a single image, so no training is needed and things are much easier. I've included instructions on how to set it up under **Windows 10** and **Linux**.

# Setup

## Requirements
You will need the following to make it work:

    Linux host OS / Win 10
    NVidia fast GPU (GTX 1080, GTX 1080i, Titan, etc ...)
    Fast Desktop CPU (Quad Core or more)
    Webcam

# Clone this repository
Don't forget to use the *--recurse-submodules* parameter to checkout all dependencies. In Windows you might need to install a  [Git Client](https://git-scm.com/download/win).

    $ git clone --recurse-submodules https://github.com/kishan1823/RealTime-Face-Alteration.git

## Download 'vox-adv-cpk.pth.tar' to /model folder

You can find it at: [google-drive](https://drive.google.com/open?id=1PyQJmkdCsAkOYwUyaj_l-l0as-iLDgeH) or [yandex-disk](https://yadi.sk/d/lEw8uRm140L_eQ).

# Install NVidia Deep Learning Drivers / Libs
Install the latest Nvidia video driver then the Deep Learning infrastructure:

* NVidia [CUDA 10.1 driver](https://developer.nvidia.com/cuda-downloads) - 2.6GB Download!
* [cuDNN](https://developer.nvidia.com/cudnn) version for CUDA 10.1 - you will need to register to download it.

Other versions might work, but I haven't tested them.

# Install requirements
```
$ pip install -r requirements.txt
```


# Run the program 

```
$ python faceit_live.py
```

## Parameters
    --system # win or linux (default is win)
    --webcam_id # the videoid of the Webcam e.g. 0 if /dev/video0 (default is 0)
    --stream_id # only used in Linux. Set the /dev/video number to stream to (default is 1)
    --gpu_id # for multiple GPU setups, select which GPU to use (default is 0)

## Example
```
$ python faceit_live.py --webcam_id 0 --stream_id 1 --gpu_id 0 --system linux
```

## Key Shortcuts when running
```
B - cycle previous image in media folder
N - cycle next image in media folder
C - recenter webcam and create a new base image
T - option to alter between 'Relative' and 'Absolute' transformations mode
Q - to quit and close all Windows
```

# Tip
For better results, look into the webcam when starting the program or when pressing C, as this will create a base image from your face that is used for the transformation. Move away and closer to the webcam to find the ideal distance for better results.

### Error
If you get the error below under LINUX, it means you haven't started your v4l2loopback.
```
cv2.error: OpenCV(4.2.0) /io/opencv/modules/imgproc/src/resize.cpp:4045: error: (-215:Assertion failed) !ssize.empty() in function 'resize'
```

### Multiple GPU

If you have more than one GPU, you might need to set some environment variables:
```
# specify which display to use for rendering (Linux)
$ export DISPLAY=:1

# which CUDA DEVICE to use (run nvidia-smi to discover the ID)
$ export CUDA_VISIBLE_DEVICES=0 (LINUX)
or
$ SET CUDA_VISIBLE_DEVICES=0,1 (WIN)

```
