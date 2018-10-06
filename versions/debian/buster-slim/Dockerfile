FROM debian:buster-slim

ARG ENCODING=UTF-8
ARG LANG=C
ARG TIMEZONE=Europe/Paris

ENV LANG=$LANG.$ENCODING \
    LANGUAGE=$LANG:$ENCODING \
    LC_ALL=$LANG.$ENCODING \
    TZ=$TIMEZONE

RUN set -eux \
    && ln -fs /usr/share/zoneinfo/$TIMEZONE /etc/localtime \
    && echo "$TIMEZONE" >  /etc/timezone \
    && date
