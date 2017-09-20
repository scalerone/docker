FROM php:7.1-fpm

COPY ./libs/* /tmp/ 

RUN mkdir /opt/logs && mkdir /opt/application \
	&& chown -R www-data.www-data /opt \
	&& chmod -R 777 /opt \
	&& cd /tmp \
	&& tar -zxvf ./zlib.tar.gz \
	&& tar -zxvf ./libmcrypt.tar.gz \
	&& tar -zxvf ./ImageMagick.tar.gz \
	&& tar -zxvf ./curl.tar.gz \
	&& tar -zxvf ./libpng.tar.gz \
	# zlib
	&& cd /tmp/zlib-1.2.11 \
	&& ./configure && make && make install \
	# libpng 
	&& cd /tmp/libpng-1.6.32 \
	&& ./configure && make && make install \
	# libmcrypt
	&& cd /tmp/libmcrypt-2.5.8/ \
	&& ./configure && make && make install \
	# ImageMagick
	&& cd /tmp/ImageMagick-7.0.7-0/ \
	&& ./configure && make && make install \
	# curl
	&& cd /tmp/curl-7.55.1 \
	&& ./configure && make && make install \
	# imagick
	&& pecl install /tmp/imagick.tgz \
	&& echo "extension=imagick.so" > /usr/local/etc/php/conf.d/imagick.ini \
	# igbinary 
	&& pecl install /tmp/igbinary.tgz \
	&& echo "extension=igbinary.so" > /usr/local/etc/php/conf.d/igbinary.ini \
	# redis-php
	&& pecl install /tmp/redis-php.tgz \
	&& echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini \
	# php extensions
	&& docker-php-ext-install curl pdo pdo_mysql mbstring mcrypt zip gd json\
	# clean
	&& rm -rf /tmp

ADD php.ini    		/usr/local/etc/php/php.ini
ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

VOLUME ["/opt"]