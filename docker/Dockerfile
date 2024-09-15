# Использовать официальный образ PHP с поддержкой Laravel
FROM php:8.3-fpm

# Обновить списки пакетов и установить необходимые зависимости
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libicu-dev \
    libzip-dev \
    libonig-dev \
    libxml2-dev \
    libpq-dev \
    git \
    unzip \
    zip \
    ffmpeg \
    libhiredis-dev

# Установить расширения PHP
RUN docker-php-ext-configure gd --with-freetype --with-jpeg  # Настроить GD для работы с FreeType и JPEG
RUN docker-php-ext-install gd pdo pdo_mysql pdo_pgsql pgsql exif  # Установить расширения GD, PDO, MySQL, PostgreSQL и EXIF
RUN pecl install redis && docker-php-ext-enable redis  # Установить и подключить расширение Redis

# Установить рабочую директорию
WORKDIR /var/www

# Копировать существующий каталог приложения в рабочую директорию
COPY . /var/www

# Установить Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Установить зависимости Laravel
RUN composer install

# Открыть порт 9000
EXPOSE 9000

# Запустить сервер PHP-FPM
CMD ["php-fpm"]
