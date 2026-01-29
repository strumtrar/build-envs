# SPDX-License-Identifier: GPL-2.0-only
#

ARG BASEIMAGE
ARG TOOLCHAIN_VERSION
FROM build-env-arm-multi.$TOOLCHAIN_VERSION.debian.$BASEIMAGE

ARG USERID=1000
ARG GROUPID=100
ARG PTXDIST_VERSION=2022.09.0

RUN sudo apt-get clean && \
    sudo apt-get update && \
    DEBIAN_FRONTEND=noninteractive sudo apt-get install -y \
        build-essential \
	g++ \
	autoconf \
	automake \
        cpio \
        cmake \
        dialog \
	dos2unix \
        groff-base \
        icecc \
	icecream-sundae \
        libc6-dev \
        libcrypt-dev \
        libdbus-1-dev \
        libffi-dev \
        libglib2.0-dev \
        libpcap-dev \
        libusb-dev \
	make \
	man \
        net-tools \
	python3 \
	python3-cryptography \
	python3-dev \
	python3-mako \
	python3-jinja2 \
	python3-mako \
	python3-pip \
	python3-setuptools \
	python3-venv \
	python3-virtualenv \
	flex \
	bison \
	gawk \
	gettext \
	texinfo \
	rsync \
	git \
	wget \
	pkg-config \
	ncurses-dev \
	tclsh

RUN  sudo wget http://public.pengutronix.de/software/ptxdist/ptxdist-$PTXDIST_VERSION.tar.bz2 && \
     sudo tar -xjvf ptxdist-$PTXDIST_VERSION.tar.bz2 && \
     cd ptxdist-$PTXDIST_VERSION && \
     sudo ./configure --prefix=/opt/ptxdist && \
     sudo make && \
     sudo make install && \
     cd .. && \
     sudo rm -rf ptxdist-$PTXDIST_VERSION && \
     if [ ! -d /.ptxdist ]; then sudo mkdir /.ptxdist; fi && \
     sudo chmod 777 /.ptxdist

ENV PATH="${PATH}:/opt/ptxdist/bin"
