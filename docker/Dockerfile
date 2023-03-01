ARG BASE_IMAGE=nvidia/cuda:11.3.0-devel-ubuntu20.04
FROM ${BASE_IMAGE}

ARG PYTHON_VERSION=3.9
ARG USER_NAME=docker
ARG GROUP_NAME=dockers
ARG UID=1000
ARG GID=1000
ARG WORKDIR=/home/${USER_NAME}

ENV DEBIAN_FRONTEND="noninteractive"
ENV PYTHONPATH=${WORKDIR}

RUN apt-get update && apt-get install --no-install-recommends -y \
    git curl ssh openssh-client libopencv-dev \
    python${PYTHON_VERSION} python${PYTHON_VERSION}-dev python3-pip python-is-python3 \
    && rm -rf /var/lib/apt/lists/*

# Change default python3 version
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python${PYTHON_VERSION} 1 \
    && update-alternatives --set python3 /usr/bin/python${PYTHON_VERSION} \
    && python3 -m pip install --upgrade pip setuptools \
    && rm -rf /var/lib/apt/lists/*

# Install pytorch
RUN python3 -m pip install torch==1.12.1+cu113 torchvision==0.13.1+cu113 torchaudio==0.12.1 --extra-index-url https://download.pytorch.org/whl/cu113 \
    && rm -rf /var/lib/apt/lists/*

# Add user
RUN groupadd -g ${GID} ${GROUP_NAME} \
    && useradd -ms /bin/sh -u ${UID} -g ${GID} ${USER_NAME}

USER ${USER_NAME}
WORKDIR ${WORKDIR}

# Install other libraries
COPY requirements.txt ${WORKDIR}
RUN python3 -m pip install -r requirements.txt \
    && rm -rf /var/lib/apt/lists/*
