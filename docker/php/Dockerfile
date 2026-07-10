FROM php:8.5-fpm

RUN apt-get update && apt-get install -y --no-install-recommends \
        zip \
        unzip \
        curl \
        git \
        libpq-dev \
        libzip-dev \
        libpng-dev \
        libonig-dev \
        libxml2-dev \
        nodejs \
        npm \
    && docker-php-ext-install pdo pdo_mysql pdo_pgsql zip gd mbstring exif pcntl \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

COPY composer.json composer.lock ./

RUN composer install --no-dev --no-scripts --no-autoloader --prefer-dist

COPY --chown=www-data:www-data . .
COPY --chown=www-data:www-data .env.example .env

RUN composer dump-autoload --optimize --no-dev

RUN chmod -R 775 storage bootstrap/cache

CMD ["php-fpm"]