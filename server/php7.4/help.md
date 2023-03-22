##扩展

安装扩展前确保依赖库存在 `apt update && apt install -y libwebp-dev libjpeg-dev libpng-dev libfreetype6-dev`


进入容器：
1. `docker-php-source extract | delete` 创建|删除扩展目录并且附带一下自带的东西 `/usr/src/php`
2. `docker-php-ext-enable` 开启扩展
3. `docker-php-ext-install` 安装扩展
4. `docker-php-ext-configure` 安装扩展前配置


###安装GD库
1. 一开始直接`docker-php-ext-install gd`直接失败
2. 后来用进入`cd /usr/src/php/ext/gd`,`docker-php-ext-install -j $(nproc) gd` 才安装成功,但安装不全

3.
首先先配置：       `docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/`
7.4 版本后有变更： `docker-php-ext-configure gd --with-webp=/usr/include/webp --with-jpeg=/usr/include --with-freetype=/usr/include/freetype2/`
最后安装: `docker-php-ext-install -j$(nproc) gd`



###redis扩展
1. 下载 `curl -L -o /tmp/reids.tar.gz https://codeload.github.com/phpredis/phpredis/tar.gz/5.0.2`
2. `tar && mv ->  /usr/src/php/ext/phpredis`
3. `docker-php-ext-install phpredis`

###pdo pdo_mysql
1. `docker-php-ext-install pdo pdo_mysql`


