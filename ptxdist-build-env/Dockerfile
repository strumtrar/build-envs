# SPDX-License-Identifier: GPL-2.0-only
#

FROM build-env-arm-multi:latest

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
        groff-base \
        libdbus-1-dev \
        libffi-dev \
        libglib2.0-dev \
        libpcre++-dev \
        libusb-dev \
	make \
	python3 \
	python3-dev \
	python3-jinja2 \
	python3-setuptools \
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
     chmod 777 /.ptxdist

ENV PATH="${PATH}:/opt/ptxdist/bin"

CMD /bin/bash
