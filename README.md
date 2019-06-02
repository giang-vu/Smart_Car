# Smart_Car
Controling a car robot via a web interface using Python Flask.
The car robot has some functions such as voice commands using Google Assistant, real-time livestream and object following using OpenCV3.
![alt text](https://user-images.githubusercontent.com/33945101/58755919-a4ca8f80-84bb-11e9-99c9-5a65c39c5008.jpg)
# Installing OpenCV3
1. Install dependencies
```
cd ~
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install -y build-essential cmake pkg-config
sudo apt-get install -y libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install -y libxvidcore-dev libx264-dev
sudo apt-get install -y libgtk2.0-dev libgtk-3-dev
sudo apt-get install -y libatlas-base-dev gfortran
sudo apt-get install -y python2.7-dev python3-dev
wget https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py
sudo python3 get-pip.py
pip install numpy
```
2. Download the OpenCV source code
```
cd ~
wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.3.0.zip
unzip opencv.zip
wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.3.0.zip
unzip opencv_contrib.zip
```
3. Build OpenCV3
```
cd ~/opencv-3.3.0/
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D INSTALL_C_EXAMPLES=OFF \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D BUILD_opencv_dnn_modern=OFF \
-D ENABLE_NEON=ON \
-D ENABLE_VFPV3=ON \
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.3.0/modules \
-D BUILD_EXAMPLES=ON ..
```
4. Increase swap space size then compiling
```
sudo sed -i 's/CONF_SWAPSIZE=100/CONF_SWAPSIZE=1024/g' /etc/dphys-swapfile
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
make -j4
```
5. Install OpenCV3
```
sudo make install
sudo ldconfig
```
7. Test OpenCV3 and wrap up
```
python3
>>> import cv2
>>> cv2.__version__
'3.3.0'
sudo mv /usr/local/lib/python3.5/site-packages/cv2.cpython-35m-arm-linux-gnueabihf.so /usr/local/lib/python3.5/site-packages/cv2.so
cd ~
rm -rf opencv-3.3.0 opencv_contrib-3.3.0
sudo sed -i 's/CONF_SWAPSIZE=1024/CONF_SWAPSIZE=100/g' /etc/dphys-swapfile
sudo /etc/init.d/dphys-swapfile stop
sudo /etc/init.d/dphys-swapfile start
```
Reference:
https://www.pyimagesearch.com/2017/09/04/raspbian-stretch-install-opencv-3-python-on-your-raspberry-pi/
Fix CMake error: https://stackoverflow.com/questions/49437948/getting-cmake-error-with-protobuf-library-in-the-configuration-of-opencv-in-rasp
