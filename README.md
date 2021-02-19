# getsimplecms sobre docker
Instalación de un cms xml en docker para la asignatura de Lenguaje de Marcas de ASIR


GetSimple es un sistema de gestión de contenido ligero, autónomo, totalmente independiente y basado en XML. GetSimple es runa forma sencilla de administrar un sitio web para pequeñas empresas. No necesita un servidor de bases de datos para almacenar la información

# Instalación. Docker

Creamos una carpeta llamada webphp donde vamos a establecer el Dockerfile.

Creamos la carpeta web dentro de webphp donde descomprimimos el archivo descargado de la web de getsimple y renombramos la carpeta generada a simplecms.


# Archivo DockerFile:

'FROM ubuntu:bionic 
EXPOSE 80
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Madrid
RUN apt update && \
apt upgrade -y && \
apt install -y apache2 php libapache2-mod-php && \
apt install -y php-xml php-curl php-gd php-zip 
COPY web /var/www/html/ 
RUN chown -R www-data:www-data /var/www/html/
RUN a2enmod rewrite
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]'

Ejecutamos docker build:

$ docker build -t simplecms .

Docker Run:

$ docker run -d --rm -p 80:80 -v simplecms_data:/var/www/html/simplecms simplecms 

Acceder a una shell del contenedor:

$ docker exec -it id /bin/bash
