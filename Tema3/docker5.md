# Ejemplos Docker Módulo 5

Este repositorio contiene ejemplos de Dockerfiles y comandos para crear y ejecutar contenedores Docker, demostrando la construcción de imágenes personalizadas para aplicaciones web.

## Construcción de imágenes con una una aplicación PHP

Pasos:

1. Crear un Dockerfile para una aplicación web Apache con PHP:

```Dockerfile
# syntax=docker/dockerfile:1
FROM debian:stable-slim
RUN apt-get update && apt-get install -y apache2 libapache2-mod-php7.4 php7.4 && apt-get clean && rm -rf /var/lib/apt/lists/* && rm /var/www/html/index.html
COPY app /var/www/html/
EXPOSE 80
CMD apache2ctl -D FOREGROUND
```

![](/Tema3/img5/Screenshot_1.png)

2. Construir la imagen Docker:

```
sudo docker build -t josedom24/ejemplo2:v1 .
```

![](/Tema3/img5/Screenshot_2.png)

3. Ejecutar un contenedor basado en la imagen creada

```
sudo docker run -d -p 80:80 --name ejemplo2 josedom24/ejemplo2:v1
```

![](/Tema3/img5/Screenshot_3.png)

Y ya funciona

![](/Tema3/img5/Screenshot_4.png)

## Construcción de imágenes con una una aplicación Python

Pasos:

1. Crear un Dockerfile para una aplicación Python:

```Dockerfile
# syntax=docker/dockerfile:1
FROM debian:12
RUN apt-get update && apt-get install -y python3-pip  && apt-get clean && rm -rf /var/lib/apt/lists/*
WORKDIR /usr/share/app
COPY app .
RUN pip3 install --no-cache-dir --break-system-packages -r requirements.txt
EXPOSE 3000
CMD python3 app.py
```

![](/Tema3/img5/Screenshot_5.png)

2. Construir la imagen Docker para la aplicación Python:

```
sudo docker build -t josedom24/ejemplo3:v1 .
```

![](/Tema3/img5/Screenshot_6.png)

3. Ejecutar un contenedor basado en la imagen Python creada:

```
sudo docker run -d -p 80:3000 --name ejemplo2 josedom24/ejemplo3:v1
```

![](/Tema3/img5/Screenshot_7.png)

Y ya funciona.

![](/Tema3/img5/Screenshot_8.png)
