FROM httpd
RUN apt-get update && apt-get install -y vim 
COPY ./index.html /usr/local/apache2/htdocs/
EXPOSE 80
CMD ["httpd-foreground"]
