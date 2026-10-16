# SPDX-License-Identifier: GPL-2.0-only
#

ARG BASEIMAGE=debian.12.2-slim
ARG TOOLCHAIN_VERSION=2021.07
ARG BUILD_ENV_TAG=latest

FROM registry.pengutronix.de/containers/build-env/build-env-arm-multi.$TOOLCHAIN_VERSION.debian.$BASEIMAGE:$BUILD_ENV_TAG

ARG USERID=1000
ARG GROUPID=100
ARG PTXDIST_VERSION=2022.09.0
ARG TOOLCHAIN_VERSION
ARG GNU_TARGET

ENV DEBIAN_FRONTEND=noninteractive

RUN sudo apt-get clean && \
    sudo apt-get update && \
    sudo apt-get install -y --fix-missing --no-install-recommends \
	build-essential \
	bzip2 \
        cmake \
        dialog \
	dos2unix \
	file \
	gettext \
	git \
        groff-base \
	icecc \
        libdbus-1-dev \
        libffi-dev \
	libjson-perl \
        libpcap-dev \
        libusb-dev \
	libxml-parser-perl \
	python-dev-is-python3 \
	python3-cryptography \
	make \
	man \
        net-tools \
	gawk \
	texinfo \
	pkg-config

RUN  sudo apt-get clean
RUN  sudo wget http://public.pengutronix.de/software/ptxdist/ptxdist-$PTXDIST_VERSION.tar.bz2 && \
     sudo tar -xjvf ptxdist-$PTXDIST_VERSION.tar.bz2 && \
     cd ptxdist-$PTXDIST_VERSION && \
     sudo ./configure --prefix=/opt/ptxdist && \
     sudo make && \
     sudo make install && \
     cd .. && \
     sudo rm -rf ptxdist-$PTXDIST_VERSION && \
     if [ ! -d /.ptxdist ]; then sudo mkdir /.ptxdist; fi && \
     sudo chmod 777 /.ptxdist && \
     git config --global user.email "you@example.com" && \
     git config --global user.name "Your name"

ENV PATH="${PATH}:/opt/ptxdist/bin"

RUN git config --global user.email "build@example.com" && \
    git config --global user.name "Build"

RUN sudo chown user:user /root

USER user

CMD /bin/bash
