FROM php:8.0-fpm

#切换国内apt源 和 更新包依赖
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    apt update

#安装必要依赖
RUN apt install -y libwebp-dev libjpeg-dev libpng-dev libfreetype6-dev

#安装扩展  #开启pdo扩展
RUN docker-php-source extract && docker-php-ext-install pdo pdo_mysql

#开启DG
RUN docker-php-ext-configure gd --with-webp=/usr/include/webp --with-jpeg=/usr/include --with-freetype=/usr/include/freetype2/ && \
    docker-php-ext-install -j$(nproc) gd

#安装redis扩展
RUN curl -L -o /tmp/reids.tar.gz https://github.com/phpredis/phpredis/archive/refs/tags/5.3.7.tar.gz && \
    mkdir -p /usr/src/php/ext/phpredis && \
    tar -xvf /tmp/reids.tar.gz --strip-components 1 -C /usr/src/php/ext/phpredis && rm -rf /tmp/reids.tar.gz && \
    docker-php-ext-install phpredis

#安装swoole
RUN curl -L -o /tmp/swoole.tar.gz https://github.com/swoole/swoole-src/archive/refs/tags/v5.0.2.tar.gz && \
    mkdir -p /usr/src/php/ext/swoole && \
    tar -zxvf /tmp/swoole.tar.gz  --strip-components 1 -C  /usr/src/php/ext/swoole && rm -rf /tmp/swoole.tar.gz && \
    docker-php-ext-install swoole