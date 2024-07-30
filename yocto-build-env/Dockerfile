# debian-11-base
# Copyright (C) 2015-2021 Intel Corporation
#
# SPDX-License-Identifier: GPL-2.0-only
#

ARG DISTRO=debian
ARG BASEIMAGE=12.1-slim
FROM $DISTRO:$BASEIMAGE

ARG USERID=1000
ARG GROUPID=100

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
      bash \
      build-essential \
      chrpath \
      cpio \
      debianutils \
      diffstat \
      file \
      gawk \
      gcc \
      git-core \
      iputils-ping \
      kmod \
      locales \
      libtinfo5 \
      libegl1-mesa \
      libsdl1.2-dev \
      libncursesw5 \
      lz4 \
      lzop \
      mesa-common-dev \
      mtools \
      parted \
      pkg-config \
      procps \
      python3 \
      python3-jinja2 \
      python3-git \
      python3-pip \
      python3-pexpect \
      python3-distutils \
      python3-subunit \
      python3-yaml \
      screen \
      socat \
      sudo \
      sysstat \
      texinfo \
      tmux \
      unzip \
      wget \
      xz-utils \
      xterm \
      zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN  apt-get clean

RUN chmod 777 /root

RUN groupadd -g $GROUPID -o user

RUN useradd -u $USERID -m -g user -G plugdev user \
	&& echo 'user ALL = NOPASSWD: ALL' > /etc/sudoers.d/user \
	&& chmod 0440 /etc/sudoers.d/user

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen
ENV LANG en_US.utf8
RUN git config --global user.email "build@example.com" && \
    git config --global user.name "Build"

USER user

CMD /bin/bash
