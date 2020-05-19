FROM alpine:3.9.6

ARG VCS_REF
ARG BUILD_DATE

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/sineverba/cfhookbash" \
      org.label-schema.build-date=$BUILD_DATE

RUN apk add --no-cache bash \
                        curl \
                        openssl \
                        --upgrade grep

RUN addgroup -g 1000 -S runner && \
    adduser -u 1000 -S runner -G runner

RUN mkdir -p /config && \
    mkdir -p /dehydrated && \
    mkdir -p /hooks && \
    mkdir -p /certs

RUN chown -R runner:runner /config && \
    chown -R runner:runner /dehydrated && \
    chown -R runner:runner /hooks && \
    chown -R runner:runner /certs

USER runner

COPY ./docker/app/dehydrated/dehydrated /dehydrated
COPY ./hook.sh /hooks

COPY ./docker/dockerfile-start /usr/local/bin

VOLUME [ "/config" "/certs" ]

WORKDIR /dehydrated

CMD ["dockerfile-start"]