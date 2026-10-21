# debian-11-base
# SPDX-License-Identifier: GPL-2.0-only
#

ARG DISTRO=debian
ARG BASEIMAGE=trixie-ptx
ARG USERID=1000
ARG GROUPID=100
FROM $BASEIMAGE

ARG TOOLCHAIN=oselas.toolchain-2024.11.0-x86_64-unknown-linux-gnu

# trixie-ptx points apt at the internal mirror.stw.pengutronix.de. Default to
# the public mirror, so the build does not depend on the company network.
# On the build server use:
#   --build-arg=DEBIAN_MIRROR=http://mirror.stw.pengutronix.de/debian
# debian.pengutronix.de/debian only carries Pengutronix' own packages
# (toolchains, ptxdist), the Debian packages come from the Debian mirror.
ARG DEBIAN_MIRROR=http://deb.debian.org/debian
RUN sed -i "s|http://mirror.stw.pengutronix.de/debian|${DEBIAN_MIRROR}|" /etc/apt/sources.list.d/debian.sources

# Some networks hand out AAAA records without having an IPv6 route, apt then
# fails with "Network is unreachable". Use --build-arg=APT_FORCE_IPV4=true there.
ARG APT_FORCE_IPV4=false
RUN echo "Acquire::ForceIPv4 \"${APT_FORCE_IPV4}\";" > /etc/apt/apt.conf.d/99force-ipv4

RUN printf 'Types: deb\nURIs: http://debian.pengutronix.de/debian\nSuites: trixie\nComponents: main contrib non-free\nSigned-By: /usr/share/keyrings/pengutronix-archive-keyring.gpg\n' > /etc/apt/sources.list.d/ptx.sources

RUN DEBIAN_FRONTEND=noninteractive apt -o="Acquire::AllowInsecureRepositories=true" update
RUN DEBIAN_FRONTEND=noninteractive apt --allow-unauthenticated install -y pengutronix-archive-keyring
RUN apt-get clean && \
    apt-get update && \
    apt-get install -y apt-utils

ENV TZ="Europe/Berlin"

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
        $TOOLCHAIN

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
        bc \
        bison \
        build-essential \
        ccache \
        ccls \
        chrpath \
        cpio \
        clang-19 \
        clangd \
        flex \
        git-core \
	icecc \
	icecream-sundae \
	libfakeroot \
        libssl-dev \
	lld \
	llvm \
        locales \
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
        sudo \
        unzip \
        wget \
        xz-utils \
        xxd \
        yamllint \
	zstd && \
    echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen

RUN apt-get clean

RUN groupadd -g 100 -o user

RUN useradd -u 1000 -m -g user -G plugdev user \
	&& echo 'user ALL = NOPASSWD: ALL' > /etc/sudoers.d/user \
	&& chmod 0440 /etc/sudoers.d/user

USER user

RUN pipx ensurepath
RUN pipx install dtschema

ENV PATH="/home/user/.local/bin:${PATH}"
