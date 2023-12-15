FROM alpine:latest

# Set non-built-time labels
LABEL org.opencontainers.image.authors="zdharma-continuum"
LABEL org.opencontainers.image.description="Docker image for ZUnit, a powerful unit testing framework for ZSH"

# Set default WORKDIR to /app
RUN apk add --no-cache curl file git jq ncurses tar tree unzip zsh

WORKDIR /app

RUN git config --global --add safe.directory /app

# Install zsh and utils

# Install zunit and dependencies
RUN apk add --no-cache --virtual build-dependencies \
        git && \
    git clone --depth=1 https://github.com/molovo/color /tmp/color && \
        cp /tmp/color/color.zsh /usr/local/bin/color && \
        chmod +x /usr/local/bin/color && \
    git clone --branch='feat/format' --depth=1 https://github.com/zdharma-continuum/zunit /tmp/zunit && \
        cd /tmp/zunit && ./build.zsh && \
        cp /tmp/zunit/zunit /usr/local/bin/zunit && \
        chmod +x /usr/local/bin/zunit && \
    apk del build-dependencies && \
    rm -rf /tmp/* /var/tmp/*

# Set default ENTRYPOINT and CMD
COPY entrypoint.sh /

ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "zunit" ]
