FROM ubuntu:24.04
ENV TZ="Asia/Bangkok"
RUN apt-get update && \
    apt-get install -y && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y curl git unzip
RUN apt-get install -y nginx
RUN apt-get install -y \
    php8.2 \
    php8.2-fpm \
    php8.2-dom \
    php8.2-mbstring \
    php8.2-curl \
    php8.2-mysql

RUN curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php && \
    php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN composer global require laravel/installer && \
    export PATH="$PATH:$HOME/.config/composer/vendor/bin"

COPY ./nginx /etc/nginx/sites-enabled/default
COPY ./startup.sh /usr/script/startup.sh
RUN chmod +x ./usr/script/startup.sh

EXPOSE 80
ENTRYPOINT [ "./usr/script/startup.sh" ]
