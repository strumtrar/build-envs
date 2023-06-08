# debian-11-base
# Copyright (C) 2015-2021 Intel Corporation
#
# SPDX-License-Identifier: GPL-2.0-only
#

FROM debian:11

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        build-essential \
        chrpath \
        cpio \
        diffstat \
        gawk \
        git-core \
        locales \
        libncurses6 \
	lz4 \
        mtools \
        parted \
        pkg-config \
        procps \
        python \
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
