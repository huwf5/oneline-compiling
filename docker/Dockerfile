# build-env stage
ARG UBUNTU_VERSION
FROM ubuntu:$UBUNTU_VERSION AS build-env

LABEL maintainer="https://github.com/sadjad"

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG C.UTF-8
ENV LANGUAGE C:en
ENV LC_ALL C.UTF-8


RUN apt-get update -qq
RUN apt-get install -y -q gcc-7 g++-7 libcap-dev libncurses5-dev \
                          libboost-dev libssl-dev autopoint help2man texinfo \
                          python3 python3-pip libhiredis-dev protobuf-compiler \
                          git libprotobuf-dev libcrypto++-dev texinfo automake \
                          libtool pkg-config 

RUN pip3 install python_magic
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 99
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 99

RUN mkdir /app
COPY . /app/gg

WORKDIR /app/gg

# sandbox-env stage
FROM build-env AS sandbox-env

ENV PATH /app/gg/src/frontend:/app/gg/src/models:$PATH

# ggfunctions deps
RUN pip3 install boto3 numpy python_magic

# common deps
RUN apt-get install -y -q vim wget unzip

# deps for excamera and viddec examples
RUN apt-get install -y -q ffmpeg

# deps for LLVM example
RUN apt-get install -y -q cmake
