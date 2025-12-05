FROM php:8.3-fpm

# Install PHP extensions
RUN apt-get update && apt-get install -y \
    unzip git curl \
    && docker-php-ext-install pdo pdo_mysql

# Install Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Set working dir
WORKDIR /var/www

# Copy application files
COPY . .

# Install dependencies
RUN composer install --no-dev --optimize-autoloader

# Generate .env if missing
RUN php -r "file_exists('.env') || copy('.env.example', '.env');"

# Generate app key
RUN php artisan key:generate
