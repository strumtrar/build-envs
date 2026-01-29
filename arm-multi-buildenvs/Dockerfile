# debian-11-base
# SPDX-License-Identifier: GPL-2.0-only
#

ARG BASEIMAGE=trixie-ptx
ARG USERID=1000
ARG GROUPID=100
FROM $BASEIMAGE

ARG TOOLCHAIN=oselas.toolchain-2025.11.0-arm-v7a-linux-gnueabihf \
	      oselas.toolchain-2025.11.0-aarch64-v8a-linux-gnu
ENV TOOLCHAIN=${TOOLCHAIN}

ENV TZ="Europe/Berlin"

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get install -y oselas.toolchain-2025.11.0-arm-v7a-linux-gnueabihf \
                       oselas.toolchain-2025.11.0-aarch64-v8a-linux-gnu
RUN apt-get install -y --fix-missing \
        bc \
        bison \
        build-essential \
        ccache \
        ccls \
        chrpath \
        cpio \
        clang \
        clang-19 \
        clangd \
        flex \
        git-core \
	libfakeroot \
        libssl-dev \
	lld \
	llvm \
	lz4 \
	lzop \
	libusb-1.0.0-dev \
	pkg-config \
	pipx \
	python-is-python3 \
        python3-full \
        python3-dev \
	ncurses-dev \
	rsync \
        screen \
        swig \
        unzip \
        wget \
        xz-utils \
        xxd \
        yamllint \
	zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN apt-get clean

RUN locale-gen

RUN groupadd -g 100 -o user

RUN useradd -u 1000 -m -g user -G plugdev user \
	&& echo 'user ALL = NOPASSWD: ALL' > /etc/sudoers.d/user \
	&& chmod 0440 /etc/sudoers.d/user

USER user

RUN pipx ensurepath
RUN pipx install dtschema

ENV PATH="/home/user/.local/bin:${PATH}"
