FROM php:7.4-apache

RUN apt-get -y update \
  && apt-get -y upgrade \
  && apt-get install tzdata curl -y
RUN ln -fs /usr/share/zoneinfo/Europe/Madrid /etc/localtime && dpkg-reconfigure -f noninteractive tzdata

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
RUN ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log
RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR
RUN a2enmod auth_digest auth_basic status info
RUN service apache2 restart

VOLUME [ "/var/www/html" ]
WORKDIR /var/www/html

EXPOSE 80

ENTRYPOINT [ "/usr/sbin/apache2" ]
CMD ["-D" , "FOREGROUND"]
