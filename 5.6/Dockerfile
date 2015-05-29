FROM aurex/ubuntu:trusty
MAINTAINER Aurelio Santos <aurex@dizenia.me>

# Usar Ondřej Surý's PHP 5.6 packages
RUN echo "deb http://ppa.launchpad.net/ondrej/php5-5.6/ubuntu trusty main " \
       > /etc/apt/sources.list.d/ondrej.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E5267A6C
RUN apt-get update -y

# Instalando package
RUN apt-get -y install \
        php5=5.6.* \
        php5-fpm \
        php5-cli \
        php5-common \
        php5-curl \
        php5-imagick \
        php5-intl \
        php5-json \
        php5-mcrypt \
        php5-memcache \
        php5-readline \
        php5-sqlite \
        php5-redis \
        php5-gd \
        php5-mysql
        # php5-mysqlnd \
        # php5-pgsql \
        # php5-xdebug \
        # php5-gmp \
        # php5-apcu \
        # wget \
        # imagemagick \

RUN php5enmod mcrypt

# php-fpm Configs
ADD etc /etc/
RUN sed -i -e "s/^memory_limit\s*=.*/memory_limit = -1/" /etc/php5/cli/conf.d/zz-php.ini

# Logs
RUN mkdir -p /var/log/php5-fpm && \
    chown -R www-data:www-data /var/log/php5-fpm

# Info default
RUN mkdir -p /var/www/default && \
    echo "<?php phpinfo(); ?>" > /var/www/default/index.php && \
    chown -R www-data:www-data /var/www/default

# Instalar Composer
# RUN cd /tmp && \
#     php -r "readfile('https://getcomposer.org/installer');" | php && \
#     mv composer.phar /usr/local/bin/composer

# Limpieza
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Iniciar
WORKDIR /var/www/default

VOLUME /var/log/php5-fpm

EXPOSE 9000

CMD ["php5-fpm","--force-stderr"]
# CMD php5-fpm --fpm-config=/etc/php5/fpm/php-fpm.conf \
#              --force-stderr \
#              -c /etc/php5/fpm/php.ini
