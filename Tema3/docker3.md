# Ejemplos Docker Módulo 3

## Despliegue de la aplicación Temperaturas
Descargar la imagen de Ubuntu

```
sudo docker network create red_temperaturas
```

![](/Tema3/im3/Screenshot_1.png)

```
sudo docker run -d --name temperaturas-backend --network red_temperaturas iesgn/temperaturas_backend
```

![](/Tema3/im3/Screenshot_2.png)

```
docker run -d -p 80:3000 --name temperaturas-frontend --network red_temperaturas iesgn/temperaturas_frontend
```

![](/Tema3/im3/Screenshot_3.png)
![](/Tema3/im3/Screenshot_4.png)

## Despliegue de Wordpress + mariadb

![](/Tema3/im3/Screenshot_5.png)
![](/Tema3/im3/Screenshot_6.png)
![](/Tema3/im3/Screenshot_7.png)
![](/Tema3/im3/Screenshot_8.png)
![](/Tema3/im3/Screenshot_9.png)

## Despliegue de tomcat + nginx

![](/Tema3/im3/Screenshot_10.png)
![](/Tema3/im3/Screenshot_11.png)
![](/Tema3/im3/Screenshot_12.png)
![](/Tema3/im3/Screenshot_13.png)
![](/Tema3/im3/Screenshot_14.png)
![](/Tema3/im3/Screenshot_15.png)
