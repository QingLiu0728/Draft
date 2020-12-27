# Install

**Install ippicv offline**

Due to the network issue, it is highly likely that the ippicv package cannot be downloaded. To fix this issue, slight modification has to be made to file ${OpencvSoureDir}/opencv/3rdparty/ippicv/ippicv.cmake
change around 47 line:
"https://raw.githubusercontent.com/opencv..../ippcv"
to the ${path/to/ippcv}.
Reference to [1]( https://blog.csdn.net/orDream/article/details/84311697)

**Pre-installed packages/libraries**

```bash
# pkg-config is used to config cmake lib automatically
sudo apt-get install build-essential cmake pkg-config
# install image I/O libraries that actually facilitate the loading and decoding process.
sudo apt-get install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev
# install packages used to process video streams and access frames from cameras
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
# install GUI libs to help display image to screen (Required by imshow...)
sudo apt-get install libgtk-3-dev
# install libraries to optimize OpenCV function performance, such as matrix operations.
sudo apt-get install libatlas-base-dev gfortran
# python libraries and headers
sudo apt-get install python2.7-dev python3.5-dev
```

**Build**

It is very convenient to use CMake to compile and build OpenCV from source.

```bash
cd ${path/to/opencv/source}
mkdir build && cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=${place/for/opecvlib} \
(-D WITH_GTK = ON | -D WITH_QT=ON) \
-D OPENCV_GENERATE_PKGCONFIG=ON \ 
-D ENABLE_CXX11 = ON \
-D OPENCV_ENABLE_NONFREE=True

# (-DWITH_QT=ON | -DWITH_GTK=ON) 二选一，用于显示, 否者编译出来的函数库无法使用imshow
OPENCV_GENERATE_PKGCONFIG，否则pkg-config就没法使用了。这样，你想在命令行里直接编译opencv程序会是很痛苦的事情。
OPENCV_ENABLE_NONFREE也要加上，因为opencv有些模块是收费的，编译的时候需要避开。

```

使用CMake，指定opencv目录：

```
set(OpenCV_DIR /home/path/to/opencv/build)
find_package(OpenCV REQUIRED)
target_link_libraries(target ${OpenCV_LIBS} )
```





Reference:

https://www.cnblogs.com/laizhenghong2012/p/11329916.html

https://blog.csdn.net/dulingwen/article/details/90607767 （包含配置，安装，卸载方法）