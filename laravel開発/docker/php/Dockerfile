FROM php:8.3-fpm

# システムパッケージ
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libzip-dev \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libicu-dev \
    default-mysql-client \
    && rm -rf /var/lib/apt/lists/*

# PHP拡張モジュール（Laravelで必要になるもの）
RUN docker-php-ext-install \
    pdo_mysql \
    mbstring \
    exif \
    pcntl \
    bcmath \
    gd \
    zip \
    intl

# Composerをインストール
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html

# ホスト側のuid/gidに合わせてwww-dataを調整（WSL/Windowsマウントでの権限問題対策）
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

EXPOSE 9000
CMD ["php-fpm"]