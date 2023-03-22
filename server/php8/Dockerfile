FROM php:8.0-fpm

#切换国内apt源 和 更新包依赖
RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
    apt update

#安装必要依赖
RUN apt install -y libwebp-dev libjpeg-dev libpng-dev libfreetype6-dev

#安装扩展  #开启pdo扩展
RUN docker-php-source extract && docker-php-ext-install pdo pdo_mysql

#安装redis扩展
RUN curl -L -o /tmp/reids.tar.gz https://codeload.github.com/phpredis/phpredis/tar.gz/5.0.2 && \
    mkdir -p /usr/src/php/ext/phpredis && \
    tar -xvf /tmp/reids.tar.gz --strip-components 1 -C /usr/src/php/ext/phpredis && \
    docker-php-ext-install phpredis

#开启DG
RUN docker-php-ext-configure gd --with-webp=/usr/include/webp --with-jpeg=/usr/include --with-freetype=/usr/include/freetype2/ && \
    docker-php-ext-install -j$(nproc) gd