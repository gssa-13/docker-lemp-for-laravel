FROM ubuntu:22.04

LABEL maintainer="gssa-13"

# Define build arguments
ARG USER_ID
ARG GROUP_ID

# Define environment variables
ENV USER_ID=$USER_ID
ENV GROUP_ID=$GROUP_ID
ENV USER_ID=${USER_ID:-1000}
ENV GROUP_ID=${GROUP_ID:-1000}

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y gnupg tzdata \
    && echo "UTC" > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install software-properties-common apt-transport-https ca-certificates lsb-release -y \
    && LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y curl zip unzip git supervisor sqlite3 \
       nginx php7.4-fpm php7.4-cli \
       php7.4-pgsql php7.4-sqlite3 php7.4-gd \
       php7.4-curl php7.4-memcached \
       php7.4-imap php7.4-mysql php7.4-mbstring \
       php7.4-xml php7.4-zip php7.4-bcmath php7.4-soap \
       php7.4-intl php7.4-readline php7.4-xdebug \
       php7.4-msgpack php7.4-igbinary php7.4-redis php7.4-swoole \
       php7.4-ldap php7.4-pcov \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && update-alternatives --set php /usr/bin/php7.4 \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

RUN mkdir /etc/nginx/ssl

RUN addgroup --gid ${GROUP_ID} gssa
RUN adduser --disabled-password --gecos '' --uid ${USER_ID} --gid ${GROUP_ID} gssa

# Set user and group of working directory
RUN chown -R gssa:gssa /var/www/html

ADD server.crt /etc/nginx/ssl/server.crt
ADD server.key /etc/nginx/ssl/server.key
ADD default /etc/nginx/sites-available/default
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD php-fpm.conf /etc/php/7.4/fpm/php-fpm.conf
ADD php.ini /etc/php/7.4/fpm/php.ini
ADD start-container.sh /usr/bin/start-container
RUN chmod +x /usr/bin/start-container

ENTRYPOINT ["start-container"]