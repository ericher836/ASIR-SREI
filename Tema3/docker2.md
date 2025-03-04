# Comandos Docker

## Descargar imágenes
Descargar la imagen de Ubuntu

```
sudo docker pull ubuntu
```

Descargar la imagen de Hello-World

```
sudo docker pull hello-world
```

Descargar la imagen de Nginx

```
sudo docker pull nginx
```

## Listar imágenes
Mostrar un listado de todas las imágenes

```
sudo docker images
```

## Ejecutar contenedores
Ejecutar un contenedor Hello-World y nombrarlo "myhello1"

```
sudo docker run --name myhello1 hello-world
```

Ejecutar un contenedor Hello-World y nombrarlo "myhello2"

```
sudo docker run --name myhello2 hello-world
```

Ejecutar un contenedor Hello-World y nombrarlo "myhello3"

```
sudo docker run --name myhello3 hello-world
```

## Gestionar contenedores
Mostrar los contenedores que se están ejecutando

```
sudo docker ps
```

Detener el contenedor "myhello1"

```
sudo docker stop myhello1
```

Detener el contenedor "myhello2"

```
sudo docker stop myhello2
```

Eliminar el contenedor "myhello1"

```
sudo docker rm myhello1
```

Mostrar los contenedores que se están ejecutando

```
sudo docker ps
```

Eliminar todos los contenedores

```
sudo su
docker rm $(docker ps -a -q)
```
