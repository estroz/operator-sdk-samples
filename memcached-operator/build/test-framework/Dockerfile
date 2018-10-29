# Binary builder image
FROM golang:1.10.3 AS builder

ENV GOPATH /go
ENV CGO_ENABLED 0
ENV GOOS linux
ENV GOARCH amd64

WORKDIR /go/src/github.com/operator-framework/operator-sdk-samples/memcached-operator
COPY . /go/src/github.com/operator-framework/operator-sdk-samples/memcached-operator

ARG TESTDIR
RUN go test -c -o /go/bin/memcached-operator-test ${TESTDIR}/...

# Base image
ARG BASEIMAGE
FROM ${BASEIMAGE}

COPY --from=builder /go/bin/memcached-operator-test /usr/local/bin/memcached-operator-test

ARG NAMESPACEDMAN
ADD $NAMESPACEDMAN /namespaced.yaml

ADD build/test-framework/go-test.sh /go-test.sh
