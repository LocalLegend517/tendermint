FROM bufbuild/buf:latest@sha256:f67394a2b5ebcffb7e844cf54b2a92d4d7142d38b7c0c9c26ce48c4fcbd9c89a as buf

FROM golang:1.14-alpine3.11@sha256:4f1c80d88c5879067f063770c774a8ffd4de47b684333cdbe9a4ce661931b9b8 as builder

RUN apk add --update --no-cache build-base curl git upx && \
  rm -rf /var/cache/apk/*

ENV GOLANG_PROTOBUF_VERSION=1.3.1 \
  GOGO_PROTOBUF_VERSION=1.3.2

RUN GO111MODULE=on go get \
  github.com/golang/protobuf/protoc-gen-go@v${GOLANG_PROTOBUF_VERSION} \
  github.com/gogo/protobuf/protoc-gen-gogo@v${GOGO_PROTOBUF_VERSION} \
  github.com/gogo/protobuf/protoc-gen-gogofaster@v${GOGO_PROTOBUF_VERSION} && \
  mv /go/bin/protoc-gen-go* /usr/local/bin/


FROM alpine:edge@sha256:2d01a16bab53a8405876cec4c27235d47455a7b72b75334c614f2fb0968b3f90

WORKDIR /work

RUN echo 'http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
  apk add --update --no-cache clang && \
  rm -rf /var/cache/apk/*

COPY --from=builder /usr/local/bin /usr/local/bin
COPY --from=buf /usr/local/bin /usr/local/bin
