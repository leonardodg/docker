FROM debian:stable-slim

COPY ./apache/*.conf /etc/apache2/sites-available/

RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
    && localedef -i pt_BR -c -f UTF-8 -A /usr/share/locale/locale.alias pt_BR.UTF-8
ENV LANG pt_BR.utf8

# INSTALL TOOLS
RUN apt-get update -y && apt-get upgrade -y \
    && apt-get install -y nano apache2 curl wget gnupg2 ca-certificates lsb-release apt-transport-https software-properties-common \
            libfreetype6-dev libjpeg62-turbo-dev apt-utils pngquant libpng-dev curl libssl-dev libmcrypt-dev libicu-dev libxml2-dev git libxslt-dev libzip-dev zip unzip;

# ENABLE SITE DEFAULT 
RUN a2enmod alias proxy proxy_fcgi ssl rewrite headers;

# Enable Sites
RUN a2ensite php5 && a2ensite php7 

#VOLUME /var/www/html
#RUN chown -R www-data. /var/www/html

# RESTART APACHE2
CMD ["apachectl", "-D", "FOREGROUND"]