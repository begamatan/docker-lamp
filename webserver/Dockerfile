FROM php:7.4-apache

#RUN /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024 && chmod 600 /var/swap.1 && /sbin/mkswap /var/swap.1 && /sbin/swapon /var/swap.1

RUN apt-get -y update --fix-missing && \
    apt-get upgrade -y && \
    apt-get --no-install-recommends install -y apt-utils && \
    rm -rf /var/lib/apt/lists/*

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN apt-get update && apt-get install -y zip unzip libzip-dev
RUN apt-get -y --no-install-recommends install default-mysql-client
RUN docker-php-ext-install zip && docker-php-ext-install pdo_mysql
RUN a2enmod rewrite headers
RUN chown -R www-data:www-data /var/www/html
