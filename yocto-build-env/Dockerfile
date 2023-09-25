# debian-11-base
# Copyright (C) 2015-2021 Intel Corporation
#
# SPDX-License-Identifier: GPL-2.0-only
#

ARG BASEIMAGE=debian:12.1-slim
FROM $BASEIMAGE

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        build-essential \
        chrpath \
        cpio \
        diffstat \
        file \
        gawk \
        git-core \
	kmod \
        locales \
	libtinfo5 \
	lz4 \
        mtools \
        parted \
        pkg-config \
        procps \
        python3 \
        python3-distutils \
        screen \
        socat \
        sudo \
        sysstat \
        texinfo \
        tmux \
        unzip \
        wget \
        xz-utils \
	zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN  apt-get clean

CMD /bin/bash
