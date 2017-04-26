FROM ubuntu:16.10

MAINTAINER Christophe Meneses

RUN apt-get update && apt-get install -y apache2
RUN a2enmod proxy_fcgi

ADD app.conf /etc/apache2/sites-available/
RUN a2ensite app

EXPOSE 80

RUN mkdir -p /var/www/html/web
WORKDIR /var/www/html

CMD /usr/sbin/apache2ctl -D FOREGROUND
