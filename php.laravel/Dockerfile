# Image generated will be able to run laravel
FROM php:apache
MAINTAINER Elvis Pestana <elvispt@gmail.com>
# Set one or more individual labels
LABEL application="Laravel" version="1.0.0-RC"

ADD vhost.conf /root/vhost.conf

RUN apt-get update \

  # Install only essential packages
  && apt-get install -y --no-install-recommends \
    nano-tiny \
    git \
    zlib1g-dev \
    libmemcached-dev \

  && pecl install memcached \
  && pecl install igbinary \
  && docker-php-ext-install zip pdo_mysql \
  && docker-php-ext-enable memcached \
  && docker-php-ext-enable igbinary \

  # Composer
  && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php \
  && php -r "unlink('composer-setup.php');" \
  && mv composer.phar /usr/local/bin/composer \

  # Activate mod_rewite
  && a2enmod rewrite \

  && cat /root/vhost.conf > /etc/apache2/sites-enabled/000-default.conf \
  && rm -f /root/vhost.conf \

  # Install NodeJS
  && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
  && apt-get install -y --no-install-recommends nodejs \

  # Remove unnecessary packages
  && apt-get autoremove -y \

  # Clear caches
    # composer
    && composer clear-cache \
    # apt-get
    && rm -rf /var/lib/apt/lists/* \
    # man pages
    && rm -rf /usr/share/doc/* \
    # pecl
    && pecl clear-cache
  # ./Clear caches