# Usa la imagen oficial de PHP 8.2 con FPM en la versión Debian Bullseye
FROM php:8.2-fpm-bullseye

# Instalacion de los paquetes necesarios para el repositorio NodeSource y Node.js
RUN apt-get update && \
    apt-get install -y curl gpg && \
    mkdir -p /etc/apt/keyrings && \
    curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg && \
    echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_20.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list && \
    apt-get update && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*

# Configura la variable de entorno para aceptar los términos de la EULA de Microsoft
ENV ACCEPT_EULA=Y

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Instala dependencias del sistema y el driver ODBC de Microsoft
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libicu-dev \
        libonig-dev \
        libxml2-dev \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libwebp-dev \
        curl \
        vim \
        zip \
        unzip \
        gnupg \
        unixodbc-dev \
        libgssapi-krb5-2 \
    && curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o /etc/apt/trusted.gpg.d/microsoft.gpg \
    && curl -fsSL https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y \
        msodbcsql18 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Instala las extensiones de PHP para SQL Server a través de PECL
RUN pecl install sqlsrv \
    && pecl install pdo_sqlsrv

# Habilita las extensiones en PHP
RUN docker-php-ext-enable sqlsrv pdo_sqlsrv

# Actualiza la lista de paquetes e instalar libzip-dev
RUN apt-get update && \
    apt-get install -y libzip-dev && \
    rm -rf /var/lib/apt/lists/*

# Instala & Habilita extensiones de PHP Mysql, gd, intl, Zip
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp && \
    docker-php-ext-install -j$(nproc) gd intl zip mysqli pdo pdo_mysql && \
    docker-php-ext-enable pdo_mysql

# Configura el directorio de trabajo
WORKDIR /var/www/html

ARG USER_ID=1000
ARG GROUP_ID=1000

# Ajustar el UID/GID de www-data si es necesario
RUN usermod -u ${USER_ID} www-data && groupmod -g ${GROUP_ID} www-data

# Ajustar permisos para Laravel
RUN chown -R www-data:www-data /var/www/html

# Exponer el puerto 9000 para PHP-FPM (para conectar con un servidor web Nginx)
EXPOSE 9000

# Comando por defecto para ejecutar PHP-FPM
CMD ["php-fpm"]