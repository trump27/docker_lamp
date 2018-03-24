FROM ubuntu:xenial

# Install packages and PHP 7.0
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -q && apt-get install -qqy \
    git-core \
    composer \
    sqlite3 \
    #Installing mod-php installs both recommended PHP 7 and Apache2
    libapache2-mod-php \
    php-mcrypt \
    php-intl \
    php-mbstring \
    php-zip \
    php-xml \
    php-codesniffer \
    php-mysql \
    php-sqlite3 \
    # Delete all the apt list files since they're big and get stale quickly
    && rm -rf /var/lib/apt/lists/*

# Add apache config to enable .htaccess and do some stuff you want
COPY apache_default /etc/apache2/sites-available/000-default.conf
COPY php.ini /etc/php/7.0/apache2/conf.d/

# Enable mod rewrite and listen to localhost
RUN a2enmod rewrite && \
    echo "ServerName localhost" >> /etc/apache2/apache2.conf

################################################################
# Example, deploy a default CakePHP 3 installation from source #
################################################################

ADD project /var/www/html/

# Set workdir (no more cd from now)
WORKDIR /var/www/html

# Composer install application
# RUN composer -n install

# RUN chmod +x bin/cake \
#    && bin/cake migrations migrate \
#    && bin/cake migrations seed

# sqliteを使う場合、htmlディレクトリに書き込み権限が必要
# RUN chgrp -R www-data logs tmp && \
#    chmod -R g+rw logs tmp

####################################################
# Expose port and run Apache webserver             #
####################################################

EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]