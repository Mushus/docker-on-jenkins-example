FROM jenkins:2.60.3-alpine

USER root

RUN apk upgrade --update && \
    apk add --no-cache --update docker curl make rsync

COPY .ssh /root/.ssh

RUN chmod 700 /root/.ssh && chmod 600 /root/.ssh/*
