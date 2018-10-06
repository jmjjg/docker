FROM alpine:3.8

ARG ENCODING=UTF-8
ARG LANG=C
ARG TIMEZONE=Europe/Paris

ENV LANG=$LANG.$ENCODING \
    LANGUAGE=$LANG:$ENCODING \
    LC_ALL=$LANG.$ENCODING \
    TZ=$TIMEZONE

RUN set -eux \
    && apk add \
        --no-cache \
        tzdata=2018d-r1

RUN set -eux \
    && cp /usr/share/zoneinfo/$TIMEZONE /etc/localtime \
    && echo "$TIMEZONE" >  /etc/timezone \
    && apk del \
        --no-cache \
        tzdata