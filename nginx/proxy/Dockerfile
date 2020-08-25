FROM nginx:1.19.1

#COPY nginx.conf /etc/nginx/

#RUN rm /usr/local/etc/php-fpm.d/zz-docker.conf

RUN mkdir -p /etc/nginx/sites-enabled

RUN ln -s /etc/nginx/sites-available/www.stylecrew-dev.com.conf /etc/nginx/sites-enabled/www.stylecrew-dev.com.conf
RUN ln -s /etc/nginx/sites-available/scm.stylecrew-dev.com.conf /etc/nginx/sites-enabled/scm.stylecrew-dev.com.conf
RUN ln -s /etc/nginx/sites-available/api.stylecrew-dev.com.conf /etc/nginx/sites-enabled/api.stylecrew-dev.com.conf

EXPOSE 80 443