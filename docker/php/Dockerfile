FROM php:7.4-cli-alpine3.14

RUN apk update

RUN apk add --no-cache zip libzip-dev
RUN docker-php-ext-configure zip && docker-php-ext-install zip

RUN apk add --no-cache icu-dev
RUN docker-php-ext-configure intl && docker-php-ext-install intl

RUN apk add --no-cache libpng libpng-dev
RUN docker-php-ext-install gd

RUN apk add --no-cache libxml2-dev
RUN docker-php-ext-install soap

RUN docker-php-ext-install mysqli

RUN curl -O https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.7.2.1-1_amd64.apk
RUN apk add --allow-untrusted msodbcsql17_17.7.2.1-1_amd64.apk
RUN apk add --no-cache autoconf make g++ unixodbc-dev
RUN pecl install sqlsrv && pecl install pdo_sqlsrv
RUN echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/10_pdo_sqlsrv.ini
RUN echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/00_sqlsrv.ini

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

WORKDIR /var/www/html
COPY ./src .