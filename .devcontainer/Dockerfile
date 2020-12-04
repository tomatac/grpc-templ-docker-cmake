# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.148.1/containers/cpp/.devcontainer/base.Dockerfile
# [Choice] Debian / Ubuntu version: debian-10, debian-9, ubuntu-20.04, ubuntu-18.04

# for details follow these layers (see Dockerfile, base.Dockerfile, library-scripts folder):
# https://github.com/microsoft/vscode-dev-containers/tree/master/containers/ubuntu
# https://github.com/microsoft/vscode-dev-containers/blob/master/containers/ubuntu/.devcontainer/base.Dockerfile
# https://github.com/microsoft/vscode-dev-containers/blob/master/containers/ubuntu/.devcontainer/library-scripts/common-debian.sh

# https://github.com/microsoft/vscode-dev-containers/tree/master/containers/cpp
# https://github.com/microsoft/vscode-dev-containers/blob/master/containers/cpp/.devcontainer/base.Dockerfile

ARG VARIANT="buster"
#ARG VARIANT="ubuntu-20.04"
FROM mcr.microsoft.com/vscode/devcontainers/cpp:0-${VARIANT}

# [Optional] Uncomment this section to install additional packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    build-essential autoconf libtool pkg-config  \
    libssl-dev \
#  git curl automake libtool make g++ unzip \
    && apt-get clean

# required by gRPC
# sudo apt install -y build-essential autoconf libtool pkg-config

# cmake 3.13 or later is required for gRPC / cmake 3.16 is installed with Unbunti 20.04 
# Install cmake (default for Ubuntu 20,04: cmake 3.16.3)
# https://github.com/Kitware/CMake/releases
# https://github.com/Kitware/CMake/releases/download/v3.19.1/cmake-3.19.1-Linux-x86_64.sh
#ENV CMAKE_INSTALL_DIR /local
#RUN wget -O cmake-linux.sh https://github.com/Kitware/CMake/releases/download/v3.19.1/cmake-3.19.1-Linux-x86_64.sh && \
#    mkdir -p $CMAKE_INSTALL_DIR && \
#    sh cmake-linux.sh -- --skip-license --prefix=$CMAKE_INSTALL_DIR && \
#    sh cmake-linux.sh --skip-license && \
#    rm cmake-linux.sh

# RUN wget https://github.com/Kitware/CMake/releases/download/v3.19.1/cmake-3.19.1-Linux-x86_64.sh -q -O /tmp/cmake-install.sh
# RUN chmod u+x /tmp/cmake-install.sh
# RUN bash /tmp/cmake-install.sh --skip-license
# RUN rm /tmp/cmake-install.sh

WORKDIR /tmp/cmake
RUN wget https://github.com/Kitware/CMake/releases/download/v3.19.1/cmake-3.19.1.tar.gz && \
    tar -xzvf cmake-3.19.1.tar.gz > /dev/null && \
    cd /tmp/cmake/cmake-3.19.1 && \
    ./bootstrap && \
    make -j8 && \
    make install && \
    rm -rf /tmp/cmake

# clone gRPC repo
ENV GRPC_RELEASE_TAG v1.33.2
ENV GRPC_SOURCE_DIR /git/grpc
#ENV GRPC_INSTALL_DIR /grpc-bin
WORKDIR /git
RUN git clone --recurse-submodules -b ${GRPC_RELEASE_TAG} https://github.com/grpc/grpc ${GRPC_SOURCE_DIR}

# install gRPC
RUN cd ${GRPC_SOURCE_DIR} && \
    mkdir -p cmake/build && \
    cd cmake/build && \
    cmake -DBUILD_DEPS=ON -DgRPC_INSTALL=ON -DgRPC_BUILD_TESTS=OFF ../.. && \
    make -j8 && \
    make install && \
    cd ${GRPC_SOURCE_DIR}

#ENV PATH=${PATH}:${GRPC_INSTALL_DIR}/bin