FROM php:8.3-fpm

# Install PHP extensions
RUN apt-get update && apt-get install -y \
    unzip git curl libzip-dev libonig-dev libpng-dev libxml2-dev \
    && docker-php-ext-install pdo_mysql mbstring zip gd

# Install Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

RUN echo "=== Contenuto ricorsivo ===" && ls -R

# Copia tutto il contenuto della cartella di build (./src)
# COPY . .
COPY src/ /var/www
# COPY ../src/ /var/www

# Installa le dipendenze Laravel
RUN composer install --no-dev --optimize-autoloader

# Genera il file .env se manca
RUN php -r "file_exists('.env') || copy('.env.example', '.env');"

# Genera la APP_KEY
# RUN php artisan key:generate
