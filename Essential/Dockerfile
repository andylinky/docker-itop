FROM php:7.2-apache

# add helper script
ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

# install extra packages
RUN apt-get update \
	&& apt-get install -y \
		graphviz \
		mariadb-client \
		unzip \
	&& chmod uga+x /usr/local/bin/install-php-extensions && \
    install-php-extensions \
		gd \
		ldap \
		mcrypt \
		mysqli \
		soap \
		zip 

# Load iTop files
COPY ["files/iTop Essential-2.6.0-4259.zip", "/tmp/iTop.zip"]
RUN unzip /tmp/iTop.zip -d /tmp/ web/* \
	&& mv -v /tmp/web/* /var/www/html/ \
	&& chown -R www-data: /var/www/html/ \
	&& rm -rf /tmp/iTop.zip /tmp/web

# Add default configuration
COPY php.ini /usr/local/etc/php/php.ini
