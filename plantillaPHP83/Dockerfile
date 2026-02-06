FROM php:8.3-fpm-bullseye

# Instalar dependencias del sistema y herramientas
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    libicu-dev \
    zip \
    unzip \
    git \
    curl \
    gnupg \
    && curl -fsSL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Instalar extensiones PHP para Laravel
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip intl

# Instalar Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

ARG USER_ID=1000
ARG GROUP_ID=1000

# Ajustar el UID/GID de www-data si es necesario
RUN usermod -u ${USER_ID} www-data && groupmod -g ${GROUP_ID} www-data

# Ajustar permisos para Laravel
RUN chown -R www-data:www-data /var/www

EXPOSE 9000
CMD ["php-fpm"]