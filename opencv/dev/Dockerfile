# https://github.com/flacjacket/docker_images/blob/opencv-tx2/Dockerfile

FROM flacjacket/cuda-tx2:3.3-20181207 as opencv_builder

COPY --from=flacjacket/cmake-tx2:3.13.1-20181207 /cmake.tar.gz /
RUN  tar -xf cmake.tar.gz -C /usr --strip 1

ARG OPENCV_VERSION=3.4.5

RUN mkdir /opencv
WORKDIR /opencv

RUN apt-get update && apt-get install -y --no-install-recommends build-essential \
                                                curl \
                                                python3.5-dev \
                                                libpng12-dev \
                                                libjpeg8-dev \
                                                libjasper-dev \
                                                libtiff5-dev \
                                                libgstreamer1.0-dev \
                                                libgstreamer-plugins-base1.0-dev \
                                                gstreamer1.0-plugins-base \
  && ln -sf python3.5 /usr/bin/python3 \
  && ln -sf python3 /usr/bin/python \
  && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
  && python get-pip.py --no-cache-dir \
  && curl -LS https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.tar.gz | tar -xzC . --strip 1 \
	&& pip3 install numpy \
  && mkdir build \
  && cd build \
  && cmake -D CMAKE_BUILD_TYPE=RELEASE \
           -D CMAKE_INSTALL_PREFIX=/usr \
           -D WITH_CUDA=ON \
           -D WITH_CUBLAS=ON \
           -D WITH_CUFFT=ON \
           -D CUDA_ARCH_BIN="6.2" \
           -D CUDA_ARCH_PTX="" \
           -D ENABLE_FAST_MATH=ON \
           -D CUDA_FAST_MATH=ON \
           -D ENABLE_NEON=ON \
           -D WITH_LIBV4L=ON \
           -D BUILD_TESTS=OFF \
           -D BUILD_PERF_TESTS=OFF \
           -D BUILD_EXAMPLES=OFF \
           -D WITH_QT=OFF \
           -D WITH_OPENGL=ON \
           -D WITH_FFMPEG=ON \
           -D WITH_V4L=ON \
           -D WITH_LIBV4L=ON \
           -D WITH_LAPACK=ON \
           -D WITH_OPENGL=ON \
           .. \
  && make -j7 \
  && make package \
  && cp /opencv/build/OpenCV-unknown-aarch64.tar.gz /OpenCV.tar.gz

