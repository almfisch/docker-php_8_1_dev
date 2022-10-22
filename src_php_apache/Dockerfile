FROM php:8.1-apache

ARG imagemagic_config=/etc/ImageMagick-6/policy.xml

USER root

RUN groupadd --gid 1000 appuser && \
    useradd --uid 1000 --gid 1000 appuser && \
    adduser www-data appuser && \
    adduser appuser sudo && \
    echo 'appuser:appuser' | chpasswd && \
    echo 'root:root' | chpasswd && \
    apt-get install -y xz-utils && \
    apt-get update && apt-get upgrade -y && \
    docker-php-ext-install pdo pdo_mysql && \
    docker-php-ext-install mysqli && docker-php-ext-enable mysqli && \
    # Setup Requirements
    apt-get update && \
    apt-get install -y --no-install-recommends \
    -y sudo \
    wget \
    # Configure PHP
    xz-utils \
    libxml2-dev libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libpq-dev \
    libzip-dev \
    zlib1g-dev \
    git \
    # Install required 3rd party tools
    ghostscript \
    libgs-dev \
    imagemagick && \
    # Configure extensions
    docker-php-ext-configure gd --with-libdir=/usr/include/ --with-jpeg --with-freetype && \
    docker-php-ext-install -j$(nproc) mysqli soap gd zip opcache intl pgsql pdo_pgsql && \
    docker-php-ext-install -j$(nproc) exif && docker-php-ext-enable exif  && \
    # Configure Apache as needed
    a2enmod rewrite && \
    apt-get clean && \
    apt-get -y purge \
    libxml2-dev libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libzip-dev \
    zlib1g-dev && \
    rm -rf /var/lib/apt/lists/* /usr/src/* && \
    apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/* && \
    printf "\n" | pecl install imagick && \
    docker-php-ext-enable imagick && \
    if [ -f /etc/ImageMagick-6/policy.xml ] ; then sed -i 's/<policy domain="coder" rights="none" pattern="PDF" \/>/<policy domain="coder" rights="read|write" pattern="PDF" \/>/g' $imagemagic_config ; else echo did not see file $imagemagic_config ; fi && \
    curl -sL https://deb.nodesource.com/setup_18.x | bash - && \
    mkdir /home/appuser && \
    mkdir /home/appuser/.npm && \
    mkdir /home/appuser/.cache && \
    apt-get install -y nodejs && \
    npm -g config set user 1000:1000 && \
    chown -R 1000:1000 '/home/appuser/.npm' && \
    chown -R 1000:1000 '/home/appuser/.cache' && \
    npm cache clean --force && \
    apt-get update && apt-get install -y unzip && \
    pecl install xdebug && docker-php-ext-enable xdebug && \
    curl -LkSso /usr/local/bin/mhsendmail 'https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64' && \
    chmod 0755 /usr/local/bin/mhsendmail && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

USER 1000:1000