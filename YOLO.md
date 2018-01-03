# YOLO on Raspberry Pi 3

```
sudo apt-get update

sudo apt-get install build-essential
sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev python-dev python-numpy libjpeg-dev libpng-dev libtiff-dev libjasper-dev libopencv-highgui-dev python-opencv libopencv-dev
```

Missing package?  Find it with: 

```
apt-cache search <package name>
```

Get darknet

```
git clone https://github.com/pjreddie/darknet
cd darknet
```
Modify Makefile to use opencv

```diff
+ OPENCV=1
- OPENCV=0
```

Then make darknet

```
make
```

## YAD2k

```
pip install numpy
sudo apt-get install libhdf5-dev python-scipy
sudo apt-get install libopenblas-dev
```

This next part takes forever:
```
pip install h5py pillow
```
This part takes forever!!!

```
pip install keras tensorflow
```

```
docker run -it -v ~/:/home/pi imelnik/rpi-python3-tensorflow-opencv /bin/bash
```			

Dowload the pre-trained weights file
 
```
wget https://pjreddie.com/media/files/yolo.weights
```

run the darknet command

```
./darknet detector demo cfg/coco.data cfg/yolo.cfg yolo.weights
````


