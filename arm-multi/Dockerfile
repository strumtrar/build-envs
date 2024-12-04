# debian-11-base
# SPDX-License-Identifier: GPL-2.0-only
#

ARG DISTRO=debian
ARG BASEIMAGE=12.5-slim
FROM $DISTRO:$BASEIMAGE

ARG TOOLCHAIN=oselas.toolchain-2024.11.0-arm-v7a-linux-gnueabihf \
	      oselas.toolchain-2024.11.0-aarch64-v8a-linux-gnu

RUN echo 'deb http://debian.pengutronix.de/debian/ bullseye main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb [signed-by=/usr/share/keyrings/pengutronix-archive-keyring.gpg] https://debian.pengutronix.de/debian bullseye main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb http://debian.pengutronix.de/debian/ bookworm main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb [signed-by=/usr/share/keyrings/pengutronix-archive-keyring.gpg] https://debian.pengutronix.de/debian bookworm main contrib non-free' >> /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt -o="Acquire::AllowInsecureRepositories=true" update
RUN DEBIAN_FRONTEND=noninteractive apt --allow-unauthenticated install -y pengutronix-archive-keyring
RUN apt-get clean && \
    apt-get update && \
    apt-get install -y apt-utils

ENV TZ="Europe/Berlin"

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
        $TOOLCHAIN

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
        bc \
        bison \
        build-essential \
        ccache \
        ccls \
        chrpath \
        cpio \
        clang \
        clangd \
        flex \
        git-core \
	icecc \
	icecream-sundae \
        libncurses5-dev \
        libssl-dev \
	lld \
	llvm \
        locales \
	lz4 \
	lzop \
	libusb-1.0.0-dev \
	pkg-config \
	python-is-python3 \
        python3-full \
        python3-dev \
        screen \
        swig \
        sudo \
        unzip \
        wget \
        xz-utils \
        yamllint \
	zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN python3 -m venv venv 
RUN venv/bin/pip install wheel
RUN venv/bin/pip install dtschema

ENV PATH="${PATH}:${PWD}/venv/bin"

RUN apt-get clean
