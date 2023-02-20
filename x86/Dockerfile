# debian-11-base
# SPDX-License-Identifier: GPL-2.0-only
#

FROM debian:11

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        bc \
        bison \
        build-essential \
        chrpath \
        cpio \
        flex \
        libelf-dev \
        libncurses5-dev \
        locales \
	lz4 \
	lzop \
        python \
        python3 \
        sudo \
        unzip \
        xz-utils \
	zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN  apt-get clean
