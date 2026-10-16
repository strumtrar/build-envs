# debian-11-base
# SPDX-License-Identifier: GPL-2.0-only
#

ARG DISTRO=debian
ARG BASEIMAGE=jessie-amd64
ARG USERID=1000
ARG GROUPID=100
FROM $DISTRO:$BASEIMAGE

# ARG needs to be re-defined after a FROM
ARG BASEIMAGE
ENV BASEIMAGE=${BASEIMAGE}
#COPY pengutronix-archive-keyring.gpg /usr/share/keyrings/pengutronix-archive-keyring.gpg
#COPY ptx.sources /etc/apt/sources.list.d/ptx.sources

ENV DEBIAN_FRONTEND=noninteractive

RUN rm /etc/apt/sources.list

RUN echo "deb [trusted=yes] http://archive.debian.org/debian jessie contrib main non-free" >> /etc/apt/sources.list
RUN echo "deb [trusted=yes] http://archive.debian.org/debian-security jessie/updates main" >> /etc/apt/sources.list

RUN apt-get -y update && \
    apt-get upgrade -y --with-new-pkgs && \
    apt-get install -y apt-utils locales sudo

ENV TZ="Europe/Berlin"

#RUN apt install -y oselas.toolchain-2024.11-arm-v7a-linux-gnueabihf oselas.toolchain-2024.11-aarch64-v8a-linux-gnu
#RUN apt install -y oselas.toolchain-2018.02.0-arm-v7a-linux-gnueabihf

RUN apt-get install -y --no-install-recommends \
	libc6-dev

RUN apt-get install -y --fix-missing \
           bc \
           bison \
           chrpath \
           cpio \
           flex \
           libfakeroot \
           libmpfr-dev \
           lzop \
           libusb-1.0.0-dev \
           pkg-config \
           python \
           libncurses-dev \
	   make \
           rsync \
           screen \
           swig \
           unzip \
           wget \
           xz-utils

RUN apt-get clean

RUN wget http://debian.pengutronix.de/debian/pool/main/o/oselas.toolchain/oselas.toolchain-2018.02.0-arm-v7a-linux-gnueabihf-gcc-7.3.1-glibc-2.27-binutils-2.30-kernel-4.15-sanitized_2018.02.0-0ptx2_amd64.deb \
     -O /tmp/oselas-toolchain.deb \
     && dpkg-deb -x /tmp/oselas-toolchain.deb / \
     && rm /tmp/oselas-toolchain.deb

RUN locale-gen

RUN groupadd -g 100 -o user

RUN useradd -u 1000 -m -g user -G plugdev user \
 	&& echo 'user ALL = NOPASSWD: ALL' > /etc/sudoers.d/user \
  	&& chmod 0440 /etc/sudoers.d/user

USER user

ENV PATH="/home/user/.local/bin:${PATH}"
