### 1.1. system_update
```
$ sudo apt update
```
### 1.2. system_upgrade
```
$ sudo apt upgrade
```
### 1.3. remove->unnecessary_packge
```
$ sudo apt autoremove
```
### 1.4. Check has the opencv installed bofore
```
$ pkg-config --modversion opencv
```
* i) aleady installed
if specific version appear, remove the opencv that installed before
```
$ sudo apt-get purge libopencv*python-opencv
$ sudo apt-get autoremove
$ sudo find/usr/local/-name"*opencv*"-exec rm{}\;
```
* ii) Hasn't installed before
skip the above code
## install packge(except ii)
if the opencv hasn't installed, system update once again
### install related packge
compiler or utility , install build, utility and library
```
$ sudo apt install build-essential cmake git unzip pkg-config libjpeg-dev
 libtiff5-dev libpng-dev libavocedec-dev libavformat-dev libswscale-dev
libxcidcore-dev libx264-dev libxine2-dev libv4l-dev v4l-utils libgstreamer1.0-dev
 gstreamer1.0-gtk3 libgstreamer-plugins-base1.0-dev gstreamer1.0-plugins-good
gstreamer1.0-plugins-bad gsreamer1.0-plugins-ugly gstreamer1.0-gl libgtk-3-dev
libgtk2.0-dev libvcanberra-gtk*libatlas-base-dev gfortran libeigen3-dev python3-dev
python3-numpy python3-pip libtbb2 libtbb-dev libdc1394-22-dev libopenblas-dev
libatlas-base-dev libblas-dev liblapack-dev gfortram libhdf5-dev
libprotobuf-dev libgoogle-glog-dev libaflags-dev protobuf-compiler vim nano libfreetype6-dev libharfbuzz-dev
```
libtiff5-dev
libxcidcore
gstreamer1.0-gtk3
gstreamer1.0-plugins-bad:
libgtk2.0
python3-numpy
libatlas-base
libprotobuf
