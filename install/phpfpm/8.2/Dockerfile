ARG DOCKER_PLATFORM=$TARGETPLATFORM
FROM --platform=linux/amd64 phpdockerio/php:8.2-fpm

WORKDIR "/application"

ARG USER_ID=1000
ARG GROUP_ID=1000

# Gerekli paketleri yükleyin
RUN apt-get update && apt-get install -y \
    php8.2-mysql php8.2-redis php8.2-gd php8.2-intl php8.2-apcu \
    php8.2-apc php8.2-mbstring php8.2-xml php8.2-zip php8.2-curl \
    zlib1g-dev libcurl4-openssl-dev librdkafka-dev \
    php-pear php8.2-dev libxml2-dev

# rdkafka uzantısını yükleyin
RUN pecl channel-update pecl.php.net && pecl install rdkafka && \
    echo "extension=rdkafka.so" > /etc/php/8.2/cli/conf.d/rdkafka.ini && \
    echo "extension=rdkafka.so" > /etc/php/8.2/fpm/conf.d/rdkafka.ini

# raphf ve http uzantılarını yükleyin
RUN pecl install raphf && \
    echo "extension=raphf.so" > /etc/php/8.2/cli/conf.d/raphf.ini && \
    echo "extension=raphf.so" > /etc/php/8.2/fpm/conf.d/raphf.ini && \
    pecl install pecl_http && \
    echo "extension=http.so" > /etc/php/8.2/cli/conf.d/http.ini && \
    echo "extension=http.so" > /etc/php/8.2/fpm/conf.d/http.ini

# Temizlik işlemleri
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Kullanıcı ayarları
USER www-data
USER root
