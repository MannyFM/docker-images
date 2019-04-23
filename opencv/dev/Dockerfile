# https://github.com/flacjacket/docker_images/blob/opencv-tx2/Dockerfile

FROM flacjacket/cuda-tx2:3.3-20181207 as opencv_builder

COPY --from=flacjacket/cmake-tx2:3.13.1-20181207 /cmake.tar.gz /
RUN  tar -xf cmake.tar.gz -C /usr --strip 1

ARG OPENCV_VERSION=3.4.5

RUN mkdir /opencv
WORKDIR /opencv

RUN apt-get update &&\
    apt-get install -y --no-install-recommends build-essential \
                                               curl \
                                               python3.5-dev \
                                               g++ libavformat-dev libavutil-dev \
                                               libswscale-dev libv4l-dev libeigen3-dev \
                                               libglew-dev libgtk2.0-dev libgtk-3-dev \
                                               libdc1394-22-dev libxine2-dev \
                                               libgstreamer1.0-dev \
                                               libgstreamer-plugins-base1.0-dev \
                                               libjpeg8-dev libjpeg-turbo8-dev libtiff5-dev \
                                               libjasper-dev libpng12-dev libavcodec-dev \
                                               libxvidcore-dev libx264-dev libgtk-3-dev \
                                               libatlas-base-dev gfortran \
                                               libopenblas-dev liblapack-dev liblapacke-dev \
                                               qt5-default pkg-config
RUN  ln -sf python3.5 /usr/bin/python3 \
  && ln -sf python3 /usr/bin/python \
  && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
  && python get-pip.py --no-cache-dir \
  && curl -LS https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.tar.gz | tar -xzC . --strip 1 \
  && pip3 install numpy
RUN mkdir build \
  && cd build \
  && cmake -D CMAKE_BUILD_TYPE=RELEASE \
           -D CMAKE_INSTALL_PREFIX=/usr \
           -D ENABLE_FAST_MATH=ON \
           -D ENABLE_NEON=ON \
           -D BUILD_TESTS=OFF \
           -D BUILD_PERF_TESTS=OFF \
           -D BUILD_EXAMPLES=OFF \
           -D WITH_QT=OFF \
           -D WITH_OPENGL=ON \
           -D WITH_FFMPEG=ON \
           -D WITH_V4L=ON \
           -D WITH_LAPACK=ON \
           -D WITH_OPENGL=ON \
           -D WITH_GSTREAMER=ON \
           -D WITH_GSTREAMER_0_10=OFF \
           -D WITH_CUBLAS=ON \
           -D WITH_CUFFT=ON \
           -D WITH_LIBV4L=ON \
           -D WITH_CUDA=ON \
           -D CUDA_ARCH_BIN="6.2" \
           -D CUDA_ARCH_PTX="" \
           -D CUDA_FAST_MATH=ON \
           ..
RUN cd build \
  && make -j7
RUN cd build \
  && make package \
  && cp /opencv/build/OpenCV-unknown-aarch64.tar.gz /OpenCV.tar.gz
