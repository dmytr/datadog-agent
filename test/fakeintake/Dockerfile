## Based on https://docs.docker.com/language/golang/build-images/
# syntax=docker/dockerfile:1

## Build
FROM golang:1.19-buster AS build

WORKDIR /app

COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY server/*.go ./server/
COPY api/*.go ./api/
COPY app/*.go ./app/

RUN go build -o /build app/main.go

## Deploy
FROM ubuntu:22.04

WORKDIR /

COPY --from=build /build /fakeintake

EXPOSE 8080

ENTRYPOINT ["/fakeintake"]
