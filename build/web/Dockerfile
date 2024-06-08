FROM php:8.3.8-fpm
WORKDIR /var/www/html
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
    && mkdir -p /etc/apt/keyrings \
    && apt-get install -y gnupg curl ca-certificates zip unzip git libcap2-bin libpng-dev libzip-dev dnsutils librsvg2-bin libpq-dev \
    && docker-php-ext-install zip pdo_pgsql \
    && rm -rf /var/lib/apt/lists/*
COPY . .
COPY .env.example .env
COPY --from=composer:2.7.6 /usr/bin/composer /usr/bin/composer
RUN composer install --optimize-autoloader \
    && php artisan key:generate \
    && php artisan optimize \
    && php artisan storage:link
RUN chown -R www-data:www-data /var/www/html
COPY /build/web/php.ini $PHP_INI_DIR/conf.d/
USER www-data
EXPOSE 9000
CMD ["php-fpm"]
