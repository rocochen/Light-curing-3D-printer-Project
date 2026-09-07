cmake_minimum_required(VERSION 3.10)

# -------------------------
# Toolchain
# -------------------------

set(CMAKE_C_COMPILER
    /home/crk/linux/SDK/rk3568_linux_sdk/buildroot/output/rockchip_rk3568/host/bin/aarch64-buildroot-linux-gnu-gcc)

set(CMAKE_CXX_COMPILER
    /home/crk/linux/SDK/rk3568_linux_sdk/buildroot/output/rockchip_rk3568/host/bin/aarch64-buildroot-linux-gnu-g++)

project(Camera_MPP)

set(CMAKE_CXX_STANDARD 11)

# -------------------------
# OpenCV
# -------------------------

set(OPENCV_ROOT
    /home/crk/linux/SDK/rk3568_linux_sdk/buildroot/output/rockchip_rk3568/host/aarch64-buildroot-linux-gnu/sysroot/usr
)

include_directories(
    ${CMAKE_SOURCE_DIR}/include
    ${OPENCV_ROOT}/include/opencv4
    ${OPENCV_ROOT}/include/rockchip   # MPP 头文件目录
)

link_directories(
    ${OPENCV_ROOT}/lib
)

# -------------------------
# Sources
# -------------------------

add_executable(
    Camera_1
    src/main.cpp
    src/Camera.cpp
    src/ImageProcessor.cpp
    src/TcpSender.cpp
    src/MppH264Encoder.cpp
    src/FpsCounter.cpp


)

# -------------------------
# Link
# -------------------------

target_link_libraries(
    Camera_1

    opencv_core
    opencv_imgproc
    opencv_imgcodecs
    opencv_objdetect
    rockchip_mpp    # 添加 MPP 动态库
    avformat        #ffmpeg添加项
    avcodec         #ffmpeg添加项
    avutil          #ffmpeg添加项

    pthread
    dl
    m
)
