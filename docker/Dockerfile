FROM nvidia/cuda:10.2-cudnn8-devel-ubuntu18.04

ENV PIP_ROOT_USER_ACTION=ignore

RUN apt-key del 7fa2af80 && rm /etc/apt/sources.list.d/cuda.list
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y curl git vim wget
RUN apt-get install -y libjpeg-dev libopenmpi-dev zlib1g-dev

RUN apt-get install -y software-properties-common && add-apt-repository ppa:deadsnakes/ppa
RUN apt-get update && apt-get install -y python3.7 python3-pip python3.7-dev python3.7-distutils
RUN ln -fs /usr/bin/python3.7 /usr/bin/python3 && ln -fs /usr/bin/python3 /usr/bin/python
RUN python -m pip install -U pip && ln -fs /usr/bin/pip3 /usr/bin/pip && pip install -U setuptools

RUN pip install torch==1.8.1+cu102 torchvision==0.9.1+cu102 -f https://download.pytorch.org/whl/torch_stable.html
RUN pip install numpy==1.20.2 imageio==2.19.2 scikit-learn
RUN python -m pip install mpi4py==3.1.3
RUN git clone https://github.com/NVIDIA/apex
RUN cd apex && pip install -t/usr/local/lib/python3.7/dist-packages -v --disable-pip-version-check \
        --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" .
