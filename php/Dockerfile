FROM php:7.2.5-fpm
RUN docker-php-ext-install pdo_mysql mysqli

# Install gmp and bcmath extensions for hashids
RUN apt-get update -y
RUN apt-get install -y libgmp-dev re2c libmhash-dev libmcrypt-dev file
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/
RUN docker-php-ext-configure gmp 
RUN docker-php-ext-install gmp
RUN docker-php-ext-configure bcmath
RUN docker-php-ext-install bcmath
