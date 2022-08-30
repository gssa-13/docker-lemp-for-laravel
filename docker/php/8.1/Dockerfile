FROM ubuntu:22.04

LABEL maintainer="gssa-13"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y gnupg tzdata \
    && echo "UTC" > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update \
    && apt-get install -y curl zip unzip git supervisor sqlite3 \
       nginx php8.1-fpm php8.1-cli \
       php8.1-pgsql php8.1-sqlite3 php8.1-gd \
       php8.1-curl php8.1-memcached \
       php8.1-imap php8.1-mysql php8.1-mbstring \
       php8.1-xml php8.1-zip php8.1-bcmath php8.1-soap \
       php8.1-intl php8.1-readline php8.1-xdebug \
       php-msgpack php-igbinary \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

RUN mkdir /etc/nginx/ssl

RUN groupadd --force -g 1000 gssa
RUN useradd -ms /bin/bash --no-user-group -g 1000 -u 1337 gssa

ADD server.crt /etc/nginx/ssl/server.crt
ADD server.key /etc/nginx/ssl/server.key
ADD default /etc/nginx/sites-available/default
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD php-fpm.conf /etc/php/8.1/fpm/php-fpm.conf
ADD php.ini /etc/php/8.1/fpm/php.ini
ADD start-container.sh /usr/bin/start-container
RUN chmod +x /usr/bin/start-container

ENTRYPOINT ["start-container"] 