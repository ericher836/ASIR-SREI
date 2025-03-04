# Comandos Docker

## Descargar imágenes
Descargar la imagen de Ubuntu

```
sudo docker pull ubuntu
```

![](/Tema3/img2/Screenshot_1.png)

Descargar la imagen de Hello-World

```
sudo docker pull hello-world
```

![](/Tema3/img2/Screenshot_2.png)

Descargar la imagen de Nginx

```
sudo docker pull nginx
```

![](/Tema3/img2/Screenshot_3.png)

## Listar imágenes
Mostrar un listado de todas las imágenes

```
sudo docker images
```

![](/Tema3/img2/Screenshot_4.png)

## Ejecutar contenedores
Ejecutar un contenedor Hello-World y nombrarlo "myhello1"

```
sudo docker run --name myhello1 hello-world
```

![](/Tema3/img2/Screenshot_5.png)

Ejecutar un contenedor Hello-World y nombrarlo "myhello2"

```
sudo docker run --name myhello2 hello-world
```

![](/Tema3/img2/Screenshot_6.png)

Ejecutar un contenedor Hello-World y nombrarlo "myhello3"

```
sudo docker run --name myhello3 hello-world
```

![](/Tema3/img2/Screenshot_7.png)

## Gestionar contenedores
Mostrar los contenedores que se están ejecutando

```
sudo docker ps
```

![](/Tema3/img2/Screenshot_8.png)

Detener el contenedor "myhello1"

```
sudo docker stop myhello1
```

![](/Tema3/img2/Screenshot_9.png)

Detener el contenedor "myhello2"

```
sudo docker stop myhello2
```

![](/Tema3/img2/Screenshot_10.png)

Eliminar el contenedor "myhello1"

```
sudo docker rm myhello1
```

![](/Tema3/img2/Screenshot_11.png)

Mostrar los contenedores que se están ejecutando

```
sudo docker ps
```

![](/Tema3/img2/Screenshot_12.png)

Eliminar todos los contenedores

```
sudo su
docker rm $(docker ps -a -q)
```

![](/Tema3/img2/Screenshot_13.png)
