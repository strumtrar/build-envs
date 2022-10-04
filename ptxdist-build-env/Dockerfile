# SPDX-License-Identifier: GPL-2.0-only
#

FROM build-env-v7a:latest

ARG PTXDIST_VERSION=2022.09.0

RUN apt-get clean && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        build-essential \
	g++ \
	autoconf \
	automake \
	make \
	python3 \
	python3-dev \
	flex \
	bison \
	gawk \
	gettext \
	texinfo \
	git \
	wget \
	pkg-config \
	ncurses-dev

RUN  apt-get clean
RUN  wget http://public.pengutronix.de/software/ptxdist/ptxdist-$PTXDIST_VERSION.tar.bz2 && \
     tar -xjvf ptxdist-$PTXDIST_VERSION.tar.bz2 && \
     cd ptxdist-$PTXDIST_VERSION && \
     ./configure --prefix=/opt/ptxdist && \
     make && \
     make install && \
     cd .. && \
     rm -rf ptxdist-$PTXDIST_VERSION

CMD /bin/bash
