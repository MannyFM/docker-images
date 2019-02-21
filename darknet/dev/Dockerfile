# https://github.com/flacjacket/docker_images/blob/opencv-tx2/Dockerfile

#FROM flacjacket/cuda-tx2:3.3-20181207 as darknet_builder
FROM mannyfm/tx2-opencv:gtk-3.4.5 as darknet_builder

RUN mkdir /darknet
WORKDIR /darknet

ARG DARKNET_VERSION=master
ARG DARKNET_REPO=AlexeyAB
ARG MAKEFILE_PATCH=https://gist.githubusercontent.com/MannyFM/76d2c77310ecc80fe7ea0da0c4075c19/raw/347a59b3aa39f901da74aa718541a9d308f5f187/Makefile.patch
ENV PATH="/usr/local/cuda/bin:${PATH}"

RUN apt-get update && apt-get install -y curl pkg-config

RUN  curl -LS https://github.com/${DARKNET_REPO}/darknet/archive/${DARKNET_VERSION}.tar.gz | tar -xzC . --strip 1 \
	&& curl -LS ${MAKEFILE_PATCH} | patch Makefile

# RUN make
