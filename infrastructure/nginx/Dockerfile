FROM nginx

ADD nginx.conf /etc/nginx/
ADD conf.d/ /etc/nginx/conf.d/

RUN rm /etc/nginx/conf.d/default.conf \
    && rm /etc/nginx/conf.d/wordpress.conf

RUN usermod -u 1000 www-data

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
