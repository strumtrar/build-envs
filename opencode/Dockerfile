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
	vim

RUN groupadd -g 100 -o str

RUN useradd -u 1000 -m -g str -G plugdev str \
        && echo 'str ALL = NOPASSWD: ALL' > /etc/sudoers.d/str \
        && chmod 0440 /etc/sudoers.d/str

USER str

COPY opencode.json /home/str/.config/opencode/opencode.json

COPY --from=woodpeckerci/woodpecker-cli:latest /bin/woodpecker-cli /usr/local/bin/woodpecker-cli

RUN sudo npm install -g opencode-ai

RUN git clone https://github.com/strumtrar/review-prompts /home/str/repos/review-prompts
RUN sudo chmod 777 -R /home/str/.config/opencode
RUN /home/str/repos/review-prompts/kernel/scripts/opencode-setup.sh

ENTRYPOINT ["/usr/local/bin/opencode"]
