FROM php:5.5-apache

MAINTAINER Diego Ferri <diego.ferri@looptribe.com>

RUN apt-get update && DEBIAN_FRONTEND=noninteractive \
	apt-get -o Dpkg::Options::="--force-confnew" install -y \
	libapache2-mod-php5 \
	php5 \
	php5-curl \
	php5-dev \
	php5-gd \
	php5-intl \
	php5-mcrypt \
	php5-mysql \
	php5-sqlite \ 
	php5-xdebug

RUN php5enmod mcrypt && \
	a2enmod expires && \
	a2enmod rewrite

RUN usermod -u 1000 www-data

COPY web.ini /etc/php5/apache2/conf.d/90-web.ini
COPY web.ini /etc/php5/cli/conf.d/90-web.ini

COPY vhost.conf /etc/apache2/sites-available/symfony.conf
RUN a2ensite symfony

RUN curl -sS https://getcomposer.org/installer | \
	php -- --install-dir=/usr/local/bin --filename=composer

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["apache2-foreground"]
