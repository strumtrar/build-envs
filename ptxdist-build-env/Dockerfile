# SPDX-License-Identifier: GPL-2.0-only
#

ARG TOOLCHAIN_VERSION=2021.07
ARG BASEIMAGE=debian.12.2-slim

FROM ghcr.io/strumtrar/build-env-arm-multi.$TOOLCHAIN_VERSION.$BASEIMAGE

ARG USERID=1000
ARG GROUPID=100
ARG PTXDIST_VERSION=2022.09.0

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        build-essential \
	g++ \
	autoconf \
	automake \
        cpio \
        cmake \
        dialog \
	dos2unix \
        groff-base \
        icecc \
	icecream-sundae \
        libc6-dev \
        libdbus-1-dev \
        libffi-dev \
        libglib2.0-dev \
        libpcap-dev \
        libusb-dev \
	make \
	man \
        net-tools \
	python3 \
	python3-dev \
	python3-jinja2 \
	python3-setuptools \
	python3.11-venv \
	flex \
	bison \
	gawk \
	gettext \
	texinfo \
	rsync \
	git \
	wget \
	pkg-config \
	ncurses-dev \
	tclsh

RUN  apt-get clean
RUN  wget http://public.pengutronix.de/software/ptxdist/ptxdist-$PTXDIST_VERSION.tar.bz2 && \
     tar -xjvf ptxdist-$PTXDIST_VERSION.tar.bz2 && \
     cd ptxdist-$PTXDIST_VERSION && \
     ./configure --prefix=/opt/ptxdist && \
     make && \
     make install && \
     cd .. && \
     rm -rf ptxdist-$PTXDIST_VERSION && \
     if [ ! -d /.ptxdist ]; then mkdir /.ptxdist; fi && \
     chmod 777 /.ptxdist && \
     git config --global user.email "you@example.com" && \
     git config --global user.name "Your name"

ENV PATH="${PATH}:/opt/ptxdist/bin"

RUN apt-get clean

RUN groupadd -g $GROUPID -o user

RUN useradd -u $USERID -m -g user -G plugdev user \
	&& echo 'user ALL = NOPASSWD: ALL' > /etc/sudoers.d/user \
	&& chmod 0440 /etc/sudoers.d/user

# HACK: workaround woodpecker hard-coded /root/.netrc access
RUN sudo touch /root/.netrc
RUN sudo chmod 777 /root/.netrc

USER user

CMD /bin/bash
