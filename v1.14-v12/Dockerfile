#
# Copyright © 2020 Thomas Harr. All rights reserved.
# Use of this source code is governed by MIT license
# that can be found in the LICENSE file.
#

###################################################
#                DEVELOPMENT TOOLS                #
###################################################
FROM alpine:3.12.0 as watchexec
RUN  apk add curl tar && \
  cd /tmp && \
  curl -sSL -o watchexec.tar.xz https://github.com/watchexec/watchexec/releases/download/1.14.0/watchexec-1.14.0-x86_64-unknown-linux-musl.tar.xz -o /root/watchexec-1.14.0-x86_64-unknown-linux-musl.tar.xz && \
  tar -xvf watchexec.tar.xz --strip-components=1

###################################################
#                BUILD ENVIRONMENT                #
###################################################
FROM golang:1.14-alpine3.12

ARG GOPROXY
ENV GOPROXY ${GOPROXY:-direct}
ENV SESSION_NAME develop

LABEL maintainer="Thomas Harr <xdevthomas@gmail.com>" \
  url="xdevcloud.de"

RUN apk update && \
  apk upgrade -a && \
  apk add \
    bash \
    su-exec \
    tmux \
    make \
    git \
    'nodejs<13' \
    npm && \
  rm -rf /var/cache/apk/* && \
  sed -i "s#export PATH.*#export PATH=\"$PATH\"#" /etc/profile && \
  sed -i "s#/bin/ash#/bash#" /etc/passwd

COPY ./overlay /
COPY --from=watchexec /tmp/watchexec /usr/bin/watchexec

ENTRYPOINT ["/usr/bin/entrypoint"]
