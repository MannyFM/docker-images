FROM mannyfm/tx2-opencv:gtk-3.4.5

LABEL maintainer="Alibek Manabayev <alibek@abacustech.co>"

COPY --from=mannyfm/tx2-wheels:latest /wheelhouse/grpcio*.whl /
COPY --from=mannyfm/tx2-wheels:latest /wheelhouse/numpy*.whl /

RUN  pip install /numpy*.whl /grpcio*.whl \
	&& pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp33 tensorflow-gpu \
	&& rm /*.whl
