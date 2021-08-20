# To generate a new docker image with this dockerfile:
# $ docker build . -t docker-buildx:<tag>

FROM docker:latest

LABEL maintainer "Hugo Rodde <hugo.rodde@me.com>"

COPY --from=docker/buildx-bin /buildx /usr/libexec/docker/cli-plugins/docker-buildx

RUN docker buildx version
RUN docker buildx install
