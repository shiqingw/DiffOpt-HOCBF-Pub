ARG UBUNTU_VER=22.04
# ARG CONDA_VER=latest
# ARG OS_TYPE=x86_64
# ARG OS_TYPE=aarch64

FROM ubuntu:${UBUNTU_VER}


# Use bash shell
SHELL ["/bin/bash", "--login", "-c"]

# Set environment variables to non-interactive (this prevents some prompts)
ENV DEBIAN_FRONTEND=non-interactive
ENV PATH="/usr/local/bin:${PATH}"

# System packages 
RUN apt-get update -y \
    && apt-get upgrade -y

RUN apt -y purge binutils \
    && apt -y remove make \
    && apt -y autoremove 
    
RUN apt-get install -y \
    cmake \
    vim \
    net-tools \
    build-essential \
    git \
    liblapack-dev \
    libopenblas-dev \
    libeigen3-dev \
    libboost-all-dev \
    libglib2.0-dev \
    python3-pip \
    libpoco-dev \
    python3-tk \
    sudo 

# Create a non-root user to avoid file permission issues
ARG USERNAME=dev
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install minimal LaTeX packages for English
RUN apt-get install -y --no-install-recommends \
    texlive-latex-recommended \
    texlive-latex-extra \
    texlive-fonts-recommended \
    texlive-base \
    cm-super \
    dvipng \
    && texhash

# Display
RUN apt-get install -y -q --no-install-recommends \
    libglvnd0 \
    libgl1 \
    libglx0 \
    libegl1 \
    libxext6 \
    libx11-6 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES graphics,utility,compute

# Install the required Python packages
RUN pip3 install numpy \
    scipy==1.11.4 \
    matplotlib \
    pin==2.7.0 \
    mujoco==3.1.6 \
    osqp==0.6.7.post1 \
    ipykernel \
    empy==3.3.4 \
    catkin_pkg \
    lark \
    PyQt6 \
    "pybind11[global]"

# Install xtl
RUN git clone https://github.com/xtensor-stack/xtl.git \
    && cd xtl \
    && git checkout 7309828c21e74ae6ab4f76d1f486a86391f5d6a8 \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_INSTALL_PREFIX='/usr/local' .. \
    && make \
    && make install \
    && cd / \
    && rm -rf xtl

# # Install xsimd
RUN git clone https://github.com/xtensor-stack/xsimd.git \
    && cd xsimd \
    && git checkout f372568384c84656f23b1c8304cd4baead267477 \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_INSTALL_PREFIX='/usr/local' .. \
    && make \
    && make install \
    && cd / \
    && rm -rf xsimd

# Install xtensor
RUN git clone https://github.com/shiqingw/xtensor.git \
    && cd xtensor \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_INSTALL_PREFIX='/usr/local' .. \
    && make \
    && make install \
    && cd / \
    && rm -rf xtensor

# Install xtensor-blas
RUN git clone https://github.com/shiqingw/xtensor-blas.git \
    && cd xtensor-blas \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_INSTALL_PREFIX='/usr/local' .. \
    && make \
    && make install \
    && cd / \
    && rm -rf xtensor-blas

# Install xtensor-python
RUN git clone https://github.com/shiqingw/xtensor-python.git \
    && cd xtensor-python \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_INSTALL_PREFIX='/usr/local' .. \
    && make \
    && make install \
    && cd / \
    && rm -rf xtensor-python

# Install scs
RUN git clone https://github.com/cvxgrp/scs.git \
    && cd scs \
    && git checkout fd0e6ec6f528d4200cc4cd76eab3df437a9e7d24 \
    && mkdir build \
    && cd build \
    && cmake -DCMAKE_INSTALL_PREFIX='/usr/local' .. \
    && make \
    && make install \
    && cd / \
    && rm -rf scs

# Install liegroups
RUN git clone https://github.com/utiasSTARS/liegroups.git \
    && cd liegroups \
    && pip install -e . 
    
# Install Scaling-Functions-Helper
RUN git clone https://github.com/shiqingw/Scaling-Functions-Helper.git\
    && cd Scaling-Functions-Helper \
    && mkdir build \
    && cd build \
    && cmake .. \
    && make install \
    && cd .. \
    && pip install -e .
    
# Install HOCBF-Helper
RUN git clone https://github.com/shiqingw/HOCBF-Helper.git\
    && cd HOCBF-Helper \
    && pip install -e .

# Clean up
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf ~/.cache/pip

# Spin the container
CMD ["tail", "-f", "/dev/null"]