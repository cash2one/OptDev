FROM alpine:3.3
MAINTAINER Tom <a@ie9.org>

RUN apk add --no-cache --update curl wget git \
  redis bash nginx ca-certificates supervisor \
  php-fpm php-json php-zlib php-xml php-pdo php-phar php-openssl \
  php-pdo_mysql php-mysqli \
  php-gd php-iconv php-mcrypt \
  php-curl php-openssl php-json php-dom php-ctype && \
  apk add -u musl && \
  mkdir -p /etc/nginx/conf.d && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
  rm -rf /var/cache/apk/*

ADD files/nginx.conf /etc/nginx/
ADD files/php-fpm.conf /etc/php/
ADD files/default.conf /etc/nginx/conf.d/
ADD files/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD files/run.sh /
RUN chmod +x /run.sh

EXPOSE 80 443
WORKDIR /data/htdocs
VOLUME ["/data/htdocs", "/data/logs"]
CMD ["/run.sh"]

