# https://raw.githubusercontent.com/flacjacket/docker_images/wheels-tx2/Dockerfile

FROM arm64v8/ubuntu:xenial-20181113

LABEL maintainer="Alibek Manabayev <alibek@abacustech.co>"

ENV PATH="/usr/local/cuda/bin:${PATH}"

ARG DEBIAN_FRONTEND=noninteractive

ARG PIP_OPTS=""
ARG WHEEL_OPTS="-w /wheelhouse"
ARG NUMPY_OPTS="--global-option build_ext --global-option -j7"
ARG NUMPY_VER="1.16.1"

RUN  apt-get update \
  && export build_deps=' \
       build-essential \
       ca-certificates \
       curl \
       libffi-dev \
       python3.5-dev \
			 pkg-config \
     ' \
  && apt-get install -y --no-install-recommends $build_deps \
  && ln -s python3.5 /usr/bin/python \
  && ln -s python3.5 /usr/bin/python3 \
  && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
  && python3.5 get-pip.py $PIP_OPTS \
  && pip wheel $WHEEL_OPTS $PIP_OPTS cffi==1.11.5 \
                                     grpcio==1.17.0 \
	&& pip3 wheel $WHEEL_OPTS $PIP_OPTS $NUMPY_OPTS numpy==$NUMPY_VER cython \
  && rm /wheelhouse/six* /wheelhouse/pycparser* \
  && rm -rf /usr/local/lib /usr/local/bin /var/cache/apt /var/lib/apt/lists/* get-pip.py
