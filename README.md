# jmjjg/docker

## alpine

```bash
( \
set -eux \
    && docker rmi -f jmjjg/alpine:3.8 \
    && docker build -t jmjjg/alpine:3.8 versions/alpine/3.8/ \
    && docker run -it jmjjg/alpine:3.8 \
)
```

- pas possible d'utiliser les locales autres que `C.UTF-8`
- pour plus d'options (exemple, `date -d yesterday`), installer `coreutils=8.29-r2`

### @see

- https://blog.codeship.com/building-minimal-docker-containers-for-go-applications/

## debian

### Base

```bash
( \
set -eux \
    && docker rmi -f jmjjg/debian:buster-slim \
    && docker build -t jmjjg/debian:buster-slim versions/debian/buster-slim/ \
    && docker run -it jmjjg/debian:buster-slim \
)
```

### 9.5-slim-apache2-php7.0

```bash
( \
set -eux \
    && mkdir -p versions/debian/9.5-slim-apache2-php7.0/bin/ \
    && cp -f extra/php/bin/getcomposer versions/debian/9.5-slim-apache2-php7.0/bin/getcomposer \
    && docker rmi -f jmjjg/debian:9.5-slim-apache2-php7.0 \
    && docker build -t jmjjg/debian:9.5-slim-apache2-php7.0 versions/debian/9.5-slim-apache2-php7.0/ \
    && docker run -it --publish=8080:80 --publish=8443:443 jmjjg/debian:9.5-slim-apache2-php7.0 \
)
```

## slackware

```bash
( \
set -eux \
    && docker rmi -f jmjjg/slackware:14.2 \
    && docker build -t jmjjg/slackware:14.2 versions/slackware/14.2/ \
    && docker run -it jmjjg/slackware:14.2 \
)
```
