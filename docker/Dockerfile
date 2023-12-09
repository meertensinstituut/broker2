FROM alpine:3.18 as alpine-broker

ENV TZ "Europe/Amsterdam"

# Setup apache and php
RUN apk --no-cache --update \
    add apache2 \
    curl \
    php81-apache2 \
    php81-common \
    php81-curl \
    php81-gd \
    php81-iconv \
    php81-mbstring \
    php81-mysqli \
    php81-mysqlnd \
    php81-xml \
    php81-simplexml \
    php81-xmlreader \
    php81-xmlwriter \
    php81-tokenizer \
    php81-cli \
    php81-phar \
    php81-dom  \
    php81-session \
    php81-bcmath \
    php81-ctype \
    php81-bz2 \
    php81-fileinfo \
    php81-intl \
    php81-zip \
    php81-pdo \
    php81-pdo_mysql \
    php81-pdo_sqlite \
    && mkdir /htdocs

EXPOSE 80

ADD docker-entrypoint.sh /
RUN chmod 0755 /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

FROM alpine-broker

ENV COMPOSER_HOME /opt/composer
RUN mkdir $COMPOSER_HOME && \
    cd $COMPOSER_HOME && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    rm keys.dev.pub && \
    rm keys.tags.pub && \
    mv /opt/composer/composer.phar /usr/bin/composer

RUN chmod 744 /usr/bin/composer
