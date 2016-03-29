FROM php:5.5-apache

MAINTAINER Diego Ferri <diego.ferri@looptribe.com>

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -o Dpkg::Options::="--force-confnew" install -y apache2 php5 libapache2-mod-php5 php5-mysql php5-dev php5-curl php5-intl php5-xdebug php5-mcrypt php5-sqlite php5-gd

ADD web.ini /etc/php5/apache2/conf.d/90-web.ini
ADD web.ini /etc/php5/cli/conf.d/90-web.ini

RUN php5enmod mcrypt

ADD vhost.conf /etc/apache2/sites-available/symfony.conf
RUN a2ensite symfony

RUN a2enmod expires
RUN a2enmod rewrite

RUN usermod -u 1000 www-data

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

EXPOSE 80
#EXPOSE 443

CMD ["apache2-foreground"]
