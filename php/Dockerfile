FROM debian:buster


#RUN apk add autoconf gcc \
#    && wget https://github.com/phpredis/phpredis/archive/3.1.3.tar.gz \
#    && tar -zxvf 3.1.3.tar.gz \
#    && cd phpredis-3.1.3 \
#    && /usr/local/bin/phpize \
#    && ./configure --with-php-config=/usr/local/bin/php-config \
#    && make \
#    && make install \

ADD https://github.com/just-containers/s6-overlay/releases/download/v1.22.1.0/s6-overlay-amd64.tar.gz /tmp/
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C /

RUN cd ~ 
RUN apt-get update
RUN apt-get install -y php7.3-fpm php-mysqlnd php-mbstring php-xmlrpc php-bcmath php-xml php-gd php-curl php-zip cron
COPY config/php.ini /etc/php/7.3/fpm
RUN groupadd www
RUN useradd www -g www
RUN mkdir /var/www
RUN chown www:www /var/www
RUN chmod -R 755 /var/www

EXPOSE 9000
ENTRYPOINT ["/init"]
VOLUME ["/opt/service"]
# CMD ["php-fpm7.3"]
CMD ["/bin/s6-svscan", "/opt/service"]
