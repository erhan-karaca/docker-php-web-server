ARG DOCKER_PLATFORM=$TARGETPLATFORM
FROM --platform=linux/amd64 phpdockerio/php:8.2-fpm

WORKDIR "/application"

ARG USER_ID=1000
ARG GROUP_ID=1000

RUN apt-get update && apt-get install -y \ 
    php8.2-mysql php8.2-redis php8.2-gd php8.2-intl php8.2-apcu \ 
    php8.2-apc php8.2-mbstring php8.2-xml php8.2-zip php8.2-curl php8.2-http librdkafka-dev \
    php-pear \
    php8.2-dev \
    libxml2-dev 

RUN pecl channel-update pecl.php.net && pecl install rdkafka && \ 
    echo "extension=rdkafka.so" > /etc/php/8.2/cli/conf.d/rdkafka.ini && \ 
    echo "extension=rdkafka.so" > /etc/php/8.2/fpm/conf.d/rdkafka.ini

RUN apt-get clean

USER www-data
USER root
