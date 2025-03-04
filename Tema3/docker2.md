text
# Comandos Docker

## Descargar imágenes
Descargar la imagen de Ubuntu
docker pull ubuntu

Descargar la imagen de Hello-World
docker pull hello-world

Descargar la imagen de Nginx
docker pull nginx

text

## Listar imágenes
Mostrar un listado de todas las imágenes
docker images

text

## Ejecutar contenedores
Ejecutar un contenedor Hello-World y nombrarlo "myhello1"
docker run --name myhello1 hello-world

Ejecutar un contenedor Hello-World y nombrarlo "myhello2"
docker run --name myhello2 hello-world

Ejecutar un contenedor Hello-World y nombrarlo "myhello3"
docker run --name myhello3 hello-world

text

## Gestionar contenedores
Mostrar los contenedores que se están ejecutando
docker ps

Detener el contenedor "myhello1"
docker stop myhello1

Detener el contenedor "myhello2"
docker stop myhello2

Eliminar el contenedor "myhello1"
docker rm myhello1

Mostrar los contenedores que se están ejecutando
docker ps

Eliminar todos los contenedores
docker rm $(docker ps -a -q)
