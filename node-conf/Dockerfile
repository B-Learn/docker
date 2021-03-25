FROM ubuntu:latest

RUN apt-get update && apt-get install -y \
    supervisor \
    curl \
    nginx

RUN curl -fsSL https://deb.nodesource.com/setup_15.x | bash -
RUN apt-get install -y nodejs

# PHP RUNTIME
WORKDIR /app
RUN chown -R www-data:www-data /app
USER www-data
COPY --chown=www-data:www-data . .

USER root

COPY node-conf/entrypoint.sh /entrypoint.sh

# NGINX
RUN rm /etc/nginx/nginx.conf && chown -R www-data:www-data /var/www/html /run /var/lib/nginx /var/log/nginx
COPY node-conf/nginx.conf /etc/nginx/nginx.conf
COPY node-conf/supervisord.conf /docker/conf/supervisord.conf

USER www-data

EXPOSE 8080

ENTRYPOINT [ "/entrypoint.sh" ]