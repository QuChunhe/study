
[如何在 Ubuntu 20.04 上安装 OpenCV](https://cloud.tencent.com/developer/article/1657529#:~:text=%E4%B8%80%E3%80%81%E4%BB%8E%20Ubuntu%20%E6%BA%90%E4%BB%93%E5%BA%93%E5%AE%89%E8%A3%85%20OpenCV%20OpenCV%20%E5%9C%A8%20Ubuntu%2020.04,apt%20install%20libopencv-dev%20python3-opencv%20%E4%B8%8A%E9%9D%A2%E7%9A%84%E5%91%BD%E4%BB%A4%E5%B0%86%E4%BC%9A%E5%AE%89%E8%A3%85%E6%89%80%E6%9C%89%E5%BF%85%E8%A6%81%E7%9A%84%E8%BD%AF%E4%BB%B6%E5%8C%85%EF%BC%8C%E6%9D%A5%E8%BF%90%E8%A1%8C%20OpenCV%EF%BC%9A%20%E9%80%9A%E8%BF%87%E5%AF%BC%E5%85%A5cv2%E6%A8%A1%E5%9D%97%EF%BC%8C%E5%B9%B6%E4%B8%94%E6%89%93%E5%8D%B0%20OpenCV)


```shell
sudo apt install build-essential cmake git pkg-config libgtk-3-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev  libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev  gfortran openexr libatlas-base-dev python3-dev python3-numpy libtbb2 libtbb-dev libdc1394-22-dev libopenexr-dev libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev

mkdir ~/opencv_build && cd ~/opencv_build


cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_GENERATE_PKGCONFIG=ON -D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules -D BUILD_EXAMPLES=ON ..
```

# Books

Building Computer Vision Projects with OpenCV 4 and C++


# Course

[作品](https://www.bilibili.com/video/BV1i54y1m7tw/?spm_id_from=333.788.recommend_more_video.7)