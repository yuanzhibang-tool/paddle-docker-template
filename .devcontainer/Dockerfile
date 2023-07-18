FROM paddlepaddle/paddle:2.5.0-gpu-cuda12.0-cudnn8.9-trt8.6
ARG DEBIAN_FRONTEND=noninteractive
RUN echo 'start build'
RUN LC_ALL=C.UTF-8
RUN apt update && apt install git -y
RUN pip3 install jupyter_echarts --user
RUN pip3 install pipenv --user
RUN pip3 install opencv-python --user
RUN pip3 install paddlehub --user
ENV PATH="$PATH:/root/.local/bin"
ENTRYPOINT tail -f /dev/null