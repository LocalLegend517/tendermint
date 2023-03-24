FROM alpine:3.7@sha256:8421d9a84432575381bfabd248f1eb56f3aa21d9d7cd2511583c68c9b7511d10

RUN apk update && \
    apk upgrade && \
    apk --no-cache add curl jq file

VOLUME [ /tendermint ]
WORKDIR /tendermint
EXPOSE 26656 26657
ENTRYPOINT ["/usr/bin/wrapper.sh"]
CMD ["node", "--proxy_app", "kvstore"]
STOPSIGNAL SIGTERM

COPY wrapper.sh /usr/bin/wrapper.sh
COPY config-template.toml /etc/tendermint/config-template.toml
