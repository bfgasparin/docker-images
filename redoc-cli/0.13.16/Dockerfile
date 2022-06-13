###
# Redoc Cli
#
# Repository:    Redoc
# Image:         CLI/Base
# Version:       0.13.16
# Strategy:      Repository with Redoc-cli to build OpenAPI documents
# Base distro:   Alpine 3.16.0
#
FROM alpine:3.16.0

# Repository/Image Maintainer
LABEL maintainer="Bruno Gasparin <bruno@dacxi.com>"

RUN apk add --update nodejs

RUN apk add yarn --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ && \
  yarn global add redoc-cli@0.13.16 && \
  apk del yarn


# Application directory
WORKDIR "/build"

ENTRYPOINT ["redoc-cli", "build"]
