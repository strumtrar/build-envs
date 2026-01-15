# SPDX-License-Identifier: GPL-2.0-only
#

ARG TOOLCHAIN_VERSION=2021.07
ARG BASEIMAGE=debian.12.2-slim

FROM ghcr.io/strumtrar/build-env-arm-multi.$TOOLCHAIN_VERSION.$BASEIMAGE

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
