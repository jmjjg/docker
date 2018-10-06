FROM debian:9.5-slim

ARG DIR=/opt/app
ARG ENCODING=UTF-8
ARG LANG=C
ARG TIMEZONE=Europe/Paris

ENV LANG=$LANG.$ENCODING \
    LANGUAGE=$LANG:$ENCODING \
    LC_ALL=$LANG.$ENCODING \
    TZ=$TIMEZONE

RUN set -eux \
    && ln -fs /usr/share/zoneinfo/$TIMEZONE /etc/localtime \
    && echo "$TIMEZONE" >  /etc/timezone

RUN set -eux \
    && DEBIAN_FRONTEND=noninteractive apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install \
        --assume-yes \
        --no-install-recommends \
        --show-upgraded \
        apache2=2.4.25-3+deb9u5 \
        ca-certificates=20161130+nmu1+deb9u1 \
        php7.0=7.0.30-0+deb9u1 \
        php7.0-curl=7.0.30-0+deb9u1 \
        php7.0-mbstring=7.0.30-0+deb9u1 \
        php7.0-xml=7.0.30-0+deb9u1 \
        unzip=6.0-21 \
        wget=1.18-5+deb9u2 \
        zip=3.0-11+b1 \
    && apt-get autoremove \
        --assume-yes \
    && rm -r /var/lib/apt/lists/*

RUN set -eux \
    && echo -e "; configuration for the default timezone\n; priority=15\ndate.timezone = \"$TIMEZONE\"" \
        > /etc/php/7.0/mods-available/default-date-timezone.ini \
    && phpenmod default-date-timezone

WORKDIR "$DIR"

RUN set -eux \
    && mkdir -p \
        "$DIR/bin" \
        "$DIR/logs" \
        "$DIR/tmp"

ADD bin/getcomposer "$DIR/bin/"

ARG countryName="FR"
ARG stateOrProvinceName="."
ARG localityName="."
ARG organizationName="."
ARG organizationalUnitName="."
ARG commonName="."
ARG emailAddress="."

RUN set -eux \
    && chmod +x "$DIR/bin/getcomposer" \
    && "$DIR/bin/getcomposer" \
    && a2enmod rewrite ssl \
    && a2ensite 000-default default-ssl \
    && sed -i "s/#ServerName www.example.com/ServerName localhost/g" /etc/apache2/sites-enabled/000-default.conf \
    && openssl req -new -x509 -days 365 -nodes \
        -out /etc/ssl/certs/ssl-cert-snakeoil.pem \
        -keyout /etc/ssl/private/ssl-cert-snakeoil.key \
        -subj="/countryName=$countryName/stateOrProvinceName=$stateOrProvinceName/localityName=$localityName/organizationName=$organizationName/organizationalUnitName=$organizationalUnitName/commonName=$commonName/emailAddress=$emailAddress/"

# AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.17.0.2. Set the 'ServerName' directive globally to suppress this message
# source /etc/apache2/envvars && mkdir -p "$APACHE_RUN_DIR" && chown -R www-data: $APACHE_RUN_DIR && /usr/sbin/apache2 -D FOREGROUND
