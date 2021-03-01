FROM nginx

RUN useradd ricardo

COPY index.html /usr/share/nginx/html

ENV archivo docker

WORKDIR /usr/share/nginx/html
EXPOSE 90
LABEL version="1.0"
RUN echo "Yo soy $(whoami)"
CMD nginx -g 'daemon off;'