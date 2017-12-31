FROM nikolaslada/debian-stretch

MAINTAINER Nikolas Lada <nikolas.lada@gmail.com>

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV PHP_MODS_DIR=/etc/php/7.0/mods-available
ENV APACHE_MOD_PHP_DIR=/etc/php/7.0/apache2
ENV APACHE_MOD_PHP_CONF_DIR=${APACHE_MOD_PHP_DIR}/conf.d
ENV TZ=Europe/Prague

RUN apt update && \
    apt update -y && \
    apt dist-upgrade -y && \
    apt install -y wget curl apt-transport-https ca-certificates && \
    apt update && \
    apt install -y --no-install-recommends \
        php-apcu \
        php-bcmath \
        php-bz2 \
        php-curl \
        php-gd \
        php-geoip \
        php-gettext \
        php-imap \
        php-imagick \
        php-intl \
        php-json \
        php-mbstring \
        php-mcrypt \
        php-mysql \
        php-pgsql \
        php-readline \
        php-redis \
        php-soap \
        php-sqlite3 \
        php-xdebug \
        php-xmlrpc \
        php-zip && \
    ln -s ${PHP_MODS_DIR}/custom.ini ${APACHE_MOD_PHP_DIR}/999-custom.ini && \
    apt update && \
    apt install -y \
        apache2 \
        libapache2-mod-php && \
    a2enmod include && \
    a2enmod rewrite && \
    a2enmod http2 && \
    a2enmod php7.0 && \
    a2enmod mpm_event && \
    rm /etc/apache2/sites-enabled/000-default.conf && \
    apt clean -y && \
    apt autoclean -y && \
    apt autoremove -y && \
    rm -rf /var/lib/apt/lists/* /var/lib/log/* /tmp/* /var/tmp/*

ADD conf.d/custom.ini ${PHP_MODS_DIR}/custom.ini

VOLUME /srv
WORKDIR /srv

EXPOSE 80
EXPOSE 443

CMD ["apache2ctl", "-D FOREGROUND"]
