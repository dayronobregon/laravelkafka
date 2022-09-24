FROM php:8.0-fpm-alpine3.14

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apk update
RUN apk add curl-dev
RUN apk add git
RUN apk add unzip
RUN apk add zlib-dev
RUN apk add freetype-dev
RUN apk add g++
RUN apk add make
RUN apk add autoconf
RUN apk --no-cache add postgresql-dev

COPY --from=php:8.0-fpm-alpine3.14 /usr/local/etc/php/php.ini-development /usr/local/etc/php/conf.d/php.ini

RUN  docker-php-ext-install gd pdo pdo_pgsql exif;

RUN apk add openssl-dev

RUN apk add librdkafka-dev
RUN apk add --update pcre-dev && pecl install rdkafka
RUN docker-php-ext-enable rdkafka

RUN apk add nano

RUN cd /usr/local/etc/php/conf.d/ && \
         echo 'extension=rdkafka.so' >> /usr/local/etc/php/conf.d/php.ini
