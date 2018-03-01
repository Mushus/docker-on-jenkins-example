FROM jenkins:2.60.3-alpine

USER root

RUN apk upgrade --update && \
    apk add --no-cache --update docker curl make rsync

# NOTE: jenkins起動時に crediential.xml に毎回自動追記される問題がある。
# 認証情報の設定をすることを推奨
# COPY .ssh /root/.ssh
# RUN chmod 700 /root/.ssh && chmod 600 /root/.ssh/*

COPY keys /root/keys
RUN chmod 700 /root/keys && chmod 600 /root/keys/*

# github.com を known_hostsに書き込む
# なりすましに弱いかもしれないが一旦この方法で
COPY .ssh /root/.ssh
RUN ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts
