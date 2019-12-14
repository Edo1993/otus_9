FROM nginx:alpine
MAINTAINER KarinaZ rd4th@mail.com
RUN apk update && apk upgrade
EXPOSE 80
COPY html /usr/share/nginx/html
#ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
