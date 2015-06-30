FROM ubuntu:14.04

RUN	apt-get update && \
	apt-get install -y \
		apache2 \
		apache2-doc && \
	a2enmod \
		headers \
		alias \
		ssl \
		rewrite \
		proxy \
		proxy_html \
		proxy_http \
		xml2enc && \
	mkdir -p /etc/apache2/ssl && \
	rm /var/www/html/* && \
	rm /etc/apache2/sites-enabled/000-default.conf

COPY	ports.conf /etc/apache2/ports.conf

COPY	80-dispatcher.conf /etc/apache2/sites-enabled/80-dispatcher.conf

COPY	dispatcher-apache2.4-4.1.8.so /usr/lib/apache2/modules/dispatcher-apache2.4-4.1.8.so
COPY	dispatcher.conf /etc/apache2/conf-enabled/dispatcher.conf
COPY	dispatcher.any /etc/apache2/conf.d/dispatcher.any

ENV APACHE_DOCUMENTROOT /var/www
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/web/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2

CMD /usr/sbin/apache2ctl -D FOREGROUND
