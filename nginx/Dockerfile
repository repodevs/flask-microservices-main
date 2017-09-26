#FROM nginx:1.13.0
FROM nginx:latest

RUN rm /etc/nginx/conf.d/default.conf
ADD /flask.conf /etc/nginx/conf.d
