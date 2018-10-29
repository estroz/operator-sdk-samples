# Binary builder image
FROM golang:1.10.3 AS builder

ENV GOPATH /go
ENV CGO_ENABLED 0
ENV GOOS linux
ENV GOARCH amd64

WORKDIR /go/src/github.com/operator-framework/operator-sdk-samples/memcached-operator
COPY . /go/src/github.com/operator-framework/operator-sdk-samples/memcached-operator

RUN go build -o /go/bin/memcached-operator github.com/operator-framework/operator-sdk-samples/memcached-operator/cmd/manager

# Base image
FROM alpine:3.6

USER nobody

COPY --from=builder /go/bin/memcached-operator /usr/local/bin/memcached-operator
