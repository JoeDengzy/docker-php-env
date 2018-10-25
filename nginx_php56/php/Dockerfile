FROM php:5.6.37-fpm-stretch
#RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak \
    && touch /etc/apt/sources.list \
    && echo 'deb http://mirrors.163.com/debian/ stretch main non-free contrib \
deb http://mirrors.163.com/debian/ stretch-updates main non-free contrib \
deb http://mirrors.163.com/debian/ stretch-backports main non-free contrib \
deb-src http://mirrors.163.com/debian/ stretch main non-free contrib \
deb-src http://mirrors.163.com/debian/ stretch-updates main non-free contrib \
deb-src http://mirrors.163.com/debian/ stretch-backports main non-free contrib \
deb http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib \
deb-src http://mirrors.163.com/debian-security/ stretch/updates main non-free contrib' >> /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libbz2-dev \
        libxml2-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install bcmath bz2 gd mcrypt mysql mysqli opcache pcntl pdo_mysql shmop soap sockets sysvmsg sysvsem sysvshm zip
RUN curl -fsSL 'http://pecl.php.net/get/redis-2.2.8.tgz' -o redis-2.2.8.tgz \
    && pecl install redis-2.2.8.tgz \
    && docker-php-ext-enable redis \
    && rm -f redis-2.2.8.tgz
RUN curl -fsSL 'http://pecl.php.net/get/swoole-1.9.23.tgz' -o swoole-1.9.23.tgz \
    && pecl install swoole-1.9.23.tgz \
    && docker-php-ext-enable swoole \
    && rm -f swoole-1.9.23.tgz
RUN apt-get install -y librdkafka-dev \
    && curl -fsSL 'http://pecl.php.net/get/rdkafka-3.0.4.tgz' -o rdkafka-3.0.4.tgz \
    && pecl install rdkafka-3.0.4.tgz \
    && docker-php-ext-enable rdkafka \
    && rm -f rdkafka-3.0.4.tgz
