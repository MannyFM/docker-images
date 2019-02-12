# https://github.com/flacjacket/docker_images/blob/opencv-tx2/Dockerfile

FROM flacjacket/cuda-tx2:3.3-20181207

LABEL maintainer="Alibek Manabayev <alibek@abacustech.co>"

COPY --from=mannyfm/tx2-opencv-dev:3.4.5 /OpenCV.tar.gz /

RUN  tar -xf /OpenCV.tar.gz -C /usr --strip 1 \
  && apt-get update \
  && apt-get install -y --no-install-recommends curl \
                                                gstreamer1.0-plugins-base \
                                                libgstreamer1.0-0 \
                                                libjasper1 \
                                                libjpeg8 \
                                                libpng12-0 \
                                                libtiff5 \
                                                python3.5-dev \
  && ln -s python3.5 /usr/bin/python3 \
  && ln -s python3.5 /usr/bin/python \
  && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
  && python3 get-pip.py --no-cache-dir \
  && ln -s pip /usr/bin/pip3 \
	&& pip3 install numpy \
  && apt-get remove -y --autoremove curl \
  && rm -rf /OpenCV.tar.gz /get-pip.py \
  && rm -rf /var/cache/apt /var/lib/apt/lists/*