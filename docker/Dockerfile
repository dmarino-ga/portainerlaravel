FROM php:8.2-fpm

RUN apt-get update && apt-get install -y \
    git zip unzip libonig-dev libzip-dev libpng-dev libxml2-dev \
    && docker-php-ext-install pdo_mysql mbstring zip xml gd

WORKDIR /var/www

COPY . .

RUN php -r "file_exists('.env') || copy('.env.example', '.env');" \
    && composer install \
    && php artisan key:generate