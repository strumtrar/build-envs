# debian-11-base
# SPDX-License-Identifier: GPL-2.0-only
#

FROM debian:11

RUN echo 'deb http://debian.pengutronix.de/debian/ bullseye main contrib non-free' >> /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt -o="Acquire::AllowInsecureRepositories=true" update
RUN DEBIAN_FRONTEND=noninteractive apt --allow-unauthenticated install -y pengutronix-archive-keyring
RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
	oselas.toolchain-2021.07.0-arm-v7a-linux-gnueabihf-gcc-11.1.1-clang-12.0.0-glibc-2.33-binutils-2.36.1-kernel-5.12.4-sanitized \
        oselas.toolchain-2021.07.0-aarch64-v8a-linux-gnu-gcc-11.1.1-clang-12.0.0-glibc-2.33-binutils-2.36.1-kernel-5.12.4-sanitized \
        bc \
        bison \
        build-essential \
        chrpath \
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
