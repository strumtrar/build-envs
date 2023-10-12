# debian-12-base
# SPDX-License-Identifier: GPL-2.0-only
#

FROM debian:12.1-slim

ENV TZ="Europe/Berlin"

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        bc \
        bison \
        build-essential \
        chrpath \
	ccls \
	chrpath \
        cpio \
	clangd \
        flex \
        libelf-dev \
        libncurses5-dev \
	libssl-dev \
        locales \
	lz4 \
	lzop \
	python-is-python3 \
        python3 \
        sudo \
        unzip \
        xz-utils \
	zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN  apt-get clean
