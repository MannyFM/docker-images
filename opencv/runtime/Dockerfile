# https://github.com/flacjacket/docker_images/blob/opencv-tx2/Dockerfile

LABEL maintainer="Alibek Manabayev <alibek@abacustech.co>"

FROM arm64v8/ubuntu:xenial-20181113

COPY --from=mannyfm/tx2-opencv-dev:3.4.5-gtk-nocuda /OpenCV.tar.gz /
RUN tar -xf /OpenCV.tar.gz -C /usr --strip 1

COPY --from=mannyfm/tx2-wheels:latest /wheelhouse/numpy*.whl /

RUN  apt-get update \
  && export runtime_deps=\
      ' \
        ca-certificates curl \
        libgstreamer1.0-0 \
        libgstreamer-plugins-base1.0-0 \
        libjasper1 \
        libjpeg8 \
        libpng12-0 \
        libtiff5 \
        python3.5-dev \
        libgtk2.0-dev libtbb-dev \
      ' \
  && apt-get install -y --no-install-recommends $runtime_deps \
  && ln -s python3.5 /usr/bin/python3 \
  && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
  && python3 get-pip.py --no-cache-dir \
  && pip3 install /numpy*.whl \
  && apt-get remove -y --autoremove curl \
  && rm -rf /OpenCV.tar.gz /get-pip.py \
  && rm -rf /var/cache/apt /var/lib/apt/lists/*
