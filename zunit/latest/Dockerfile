FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    autoconf autogen automake \
    build-essential bzip2 \
    ca-certificates cmake coreutils curl \
    file \
    g++ gawk git \
    jq \
    less libz-dev locales libncurses5-dev libncursesw5-dev \
    make \
    sudo subversion \
    tzdata \
    unzip \
    wget \
    xz-utils \
    zsh \
  && rm -rf /var/lib/apt/lists/*

# Set non-built-time labels
LABEL org.opencontainers.image.authors="zdharma-continuum"
LABEL org.opencontainers.image.description="Docker image for ZUnit, a powerful unit testing framework for ZSH"

WORKDIR /app


# Install zsh and utils

# Install zunit and dependencies
RUN git config \
  --global \
  --add safe.directory /app \
 && git clone \
  --branch='feat/format' \
  --depth=1 \
  https://github.com/zdharma-continuum/zunit /tmp/zunit \
 && cd /tmp/zunit \
 && ./build.zsh \
 && cp /tmp/zunit/zunit /usr/local/bin/zunit \
 && chmod +x /usr/local/bin/zunit \
 && rm -rf /tmp/zunit

# Set default ENTRYPOINT and CMD
COPY entrypoint.sh /

ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "zunit" ]
