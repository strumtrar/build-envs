# debian-12-base
# SPDX-License-Identifier: GPL-2.0-only
#

FROM debian:12.5-slim

ENV TZ="Europe/Berlin"

ARG TOOLCHAIN=oselas.toolchain-2024.11.0-x86_64-unknown-linux-gnu

RUN echo 'deb http://debian.pengutronix.de/debian/ bullseye main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb [signed-by=/usr/share/keyrings/pengutronix-archive-keyring.gpg] https://debian.pengutronix.de/debian bullseye main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb http://debian.pengutronix.de/debian/ bookworm main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb [signed-by=/usr/share/keyrings/pengutronix-archive-keyring.gpg] https://debian.pengutronix.de/debian bookworm main contrib non-free' >> /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt -o="Acquire::AllowInsecureRepositories=true" update
RUN DEBIAN_FRONTEND=noninteractive apt --allow-unauthenticated install -y pengutronix-archive-keyring
RUN apt-get clean && \
    apt-get update && \
    apt-get install -y apt-utils

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
        $TOOLCHAIN

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        bc \
        bison \
        build-essential \
	ccls \
        chrpath \
        cpio \
	clang \
	clangd \
        flex \
	git-core \
        libelf-dev \
        libncurses5-dev \
	libssl-dev \
	lld \
	llvm \
        locales \
	lz4 \
	lzop \
	python-is-python3 \
        python3 \
        sudo \
        unzip \
        xz-utils \
	yamllint \
	zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN  apt-get clean
