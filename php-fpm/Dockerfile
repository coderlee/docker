FROM php:7.1.2-fpm

MAINTAINER ross <ross@huaxi100.com>

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list \
    && apt-get update -y \
    && apt-get upgrade -y \
    && docker-php-ext-install mysqli



#####################################
# PHP Swoole:
#####################################

ARG INSTALL_SWOOLE=false
RUN if [ ${INSTALL_SWOOLE} = true ]; then \
    ## need stable
    pecl install swoole-beta \
    && docker-php-ext-enable swoole \
;fi


#####################################
# PHP Redis:
#####################################

ARG INSTALL_REDIS=false
RUN if [ ${INSTALL_REDIS} = true ]; then \
    pecl install redis \
    && docker-php-ext-enable redis \
;fi


#####################################
# Opcache:
#####################################
ARG INSTALL_OPCACHE=false
RUN if [ ${INSTALL_OPCACHE} = true ]; then \
    docker-php-ext-install opcache && \
    docker-php-ext-enable opcache \
;fi


#####################################
# bcmath: 精准计算模块
#####################################

ARG INSTALL_BCMATH=false
RUN if [ ${INSTALL_BCMATH} = true ]; then \
    docker-php-ext-install bcmath \
;fi


#####################################
# xDebug:
#####################################

ARG INSTALL_XDEBUG=false
RUN if [ ${INSTALL_XDEBUG} = true ]; then \
    pecl install xdebug && \
    docker-php-ext-enable xdebug \
;fi

RUN rm -r /var/lib/apt/lists/*

CMD ["php-fpm"]

EXPOSE 9000