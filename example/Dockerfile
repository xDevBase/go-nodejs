#
# Copyright © 2020 Thomas Harr. All rights reserved.
# Use of this source code is governed by MIT license
# that can be found in the LICENSE file.
#

###################################################
#                BUILD ENVIRONMENT                #
###################################################
FROM xdevbase/go-nodejs:v1.14-v12

ARG GOPROXY
ENV GOPROXY ${GOPROXY:-direct}

LABEL maintainer="Thomas Harr <xdevthomas@gmail.com>" \
  url="xdevcloud.de"

COPY ./overlay /
