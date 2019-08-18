FROM php:7.2-fpm-stretch

COPY ./php7.2/php.ini /usr/local/etc/php/

RUN mkdir -p /var/log/php_log

ENV TZ=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmcrypt-dev \
    libsqlite3-dev \
    vim \
    procps \
    htop \
    telnet \
    git \

    # iconv
    && docker-php-ext-install -j$(nproc) iconv \

    # mcrypt
    && pecl install mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt \

    # redis
    && pecl install -o -f redis \
    && docker-php-ext-enable redis\

    # pgsql
    && apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo_pgsql pgsql \

    # sqlite
    && docker-php-ext-install pdo_sqlite \

    && docker-php-ext-install mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \

    # scrypt
    && pecl install -o -f scrypt \
    && docker-php-ext-enable scrypt

# composer install 需要用到的 package
RUN apt-get install zip unzip

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
