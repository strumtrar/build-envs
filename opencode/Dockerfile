# SPDX-License-Identifier: GPL-2.0-only
#

FROM debian:trixie

ARG USERID=1000
ARG GROUPID=100

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8

RUN apt update && \
    apt install -y \
	git \
	curl \
	bash \
	npm \
	iputils-ping \
	iproute2 \
	sudo \
	vim \
	xz-utils

RUN groupadd -g 100 -o acid

RUN useradd -u 1000 -m -g acid -G plugdev acid \
        && echo 'acid ALL = NOPASSWD: ALL' > /etc/sudoers.d/acid \
        && chmod 0440 /etc/sudoers.d/acid

USER acid

RUN curl --proto '=https' --tlsv1.2 -L https://nixos.org/nix/install | sh -s -- --no-daemon

ENV PATH="/home/acid/.nix-profile/bin:${PATH}"
ENV NIX_CONFIG="experimental-features = nix-command flakes"

RUN mkdir -p /home/acid/.config/opencode
RUN mkdir -p /home/acid/.local/share/opencode
RUN mkdir -p /home/acid/.opencode/skills
COPY opencode.json /home/acid/.config/opencode/opencode.json
COPY tui.json /home/acid/.config/opencode/tui.json
COPY AGENTS.md /home/acid/.config/opencode/AGENTS.md
COPY skills /home/acid/.opencode
COPY auth.json /home/acid/.local/share/opencode

RUN sudo npm install -g opencode-ai

RUN git clone https://github.com/masoncl/review-prompts --single-branch /home/acid/repos/review-prompts
RUN sudo chmod 777 -R /home/acid/.config/opencode
RUN /home/acid/repos/review-prompts/setup.sh opencode kernel

ENTRYPOINT ["/usr/local/bin/opencode"]
