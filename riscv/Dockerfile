# debian-11-base
# SPDX-License-Identifier: GPL-2.0-only
#

FROM debian:11

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        gcc-riscv64-linux-gnu \
        bc \
        bison \
        build-essential \
        chrpath \
        cpio \
        flex \
        git-core \
        libncurses5-dev \
        locales \
	lz4 \
	lzop \
        python \
        python3 \
        screen \
        sudo \
        unzip \
        wget \
        xz-utils \
	zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN  apt-get clean
