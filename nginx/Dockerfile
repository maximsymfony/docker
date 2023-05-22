FROM nginx:alpine

COPY nginx.conf /etc/nginx/
COPY default.conf /etc/nginx/conf.d/

RUN apk update && apk upgrade && apk add --no-cache bash

RUN set -x ; \
    addgroup -g 1000 -S www-data ; \
    adduser -u 1000 -D -S www-data -G www-data && exit 0 ; exit 1
RUN chown -R www-data:www-data /var/lib/nginx/

# Set upstream conf and remove the default conf
ARG PHP_UPSTREAM_CONTAINER=php-fpm
ARG PHP_UPSTREAM_PORT=9000
RUN echo "upstream php-upstream { server ${PHP_UPSTREAM_CONTAINER}:${PHP_UPSTREAM_PORT}; }" > /etc/nginx/conf.d/upstream.conf

EXPOSE 80