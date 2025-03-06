# Ejemplos Docker Módulo 3

Este repositorio contiene ejemplos prácticos de despliegue de aplicaciones utilizando Docker. Se presentan diferentes escenarios, incluyendo el despliegue de una aplicación de temperaturas, un entorno WordPress con MariaDB y un servicio Tomcat con Nginx como proxy inverso.

## Despliegue de la aplicación Temperaturas

Este ejemplo muestra cómo desplegar una aplicación de registro de temperaturas utilizando contenedores Docker para backend y frontend, comunicados a través de una red Docker.

Pasos:

1. Crear una red Docker para la aplicación:

```
sudo docker network create red_temperaturas
```

![](/Tema3/im3/Screenshot_1.png)

2. Desplegar el backend de la aplicación:

```
sudo docker run -d --name temperaturas-backend --network red_temperaturas iesgn/temperaturas_backend
```

![](/Tema3/im3/Screenshot_2.png)

3. Desplegar el frontend de la aplicación y exponerlo en el puerto 3000:

```
docker run -d -p 3000:3000 --name temperaturas-frontend --network red_temperaturas iesgn/temperaturas_frontend
```

![](/Tema3/im3/Screenshot_3.png)

El frontend será accesible en http://localhost:3000.

![](/Tema3/im3/Screenshot_4.png)

## Despliegue de Wordpress + mariadb

Este despliegue crea un entorno WordPress con una base de datos MariaDB.

Pasos:

1. Crear una red Docker para WordPress:

```
sudo docker network create red_wp
```

![](/Tema3/im3/Screenshot_5.png)

2. Desplegar el contenedor de la base de datos MariaDB:

```
sudo docker run -d --name servidor_mysql \
                --network red_wp \
                -v /opt/mysql_wp:/var/lib/mysql \
                -e MYSQL_DATABASE=bd_wp \
                -e MYSQL_USER=user_wp \
                -e MYSQL_PASSWORD=asdasd \
                -e MYSQL_ROOT_PASSWORD=asdasd \
                mariadb
```

![](/Tema3/im3/Screenshot_6.png)

3. Desplegar WordPress y enlazarlo con la base de datos:

```
sudo docker run -d --name servidor_wp \
                --network red_wp \
                -v /opt/wordpress:/var/www/html/wp-content \
                -e WORDPRESS_DB_HOST=servidor_mysql \
                -e WORDPRESS_DB_USER=user_wp \
                -e WORDPRESS_DB_PASSWORD=asdasd \
                -e WORDPRESS_DB_NAME=bd_wp \
                -p 123:123 \
                wordpress
```

![](/Tema3/im3/Screenshot_7.png)

Para verificar los contenedores en ejecución:

```
sudo docker ps
```

![](/Tema3/im3/Screenshot_8.png)

El sitio de WordPress será accesible en http://localhost:123.

![](/Tema3/im3/Screenshot_9.png)

## Despliegue de tomcat + nginx

Este despliegue configura un servidor Tomcat para ejecutar una aplicación Java y lo expone a través de Nginx como proxy inverso.

Pasos:

1. Crear una red Docker para la aplicación:

```
sudo docker network create red_tomcat
```

![](/Tema3/im3/Screenshot_10.png)

Necesitamos descargar estos archivos del repositorio.

![](/Tema3/im3/Screenshot_11.png)

Y guardarlos en una carpeta.

![](/Tema3/im3/Screenshot_12.png)

2. Desplegar el contenedor Tomcat con la aplicación Java:

```
sudo docker run -d --name aplicacionjava \
                --network red_tomcat \
                -v /home/vagrant/tomcat/sample.war:/usr/local/tomcat/webapps/sample.war:ro \
                tomcat:9.0
```

![](/Tema3/im3/Screenshot_13.png)

3. Desplegar Nginx como proxy inverso para Tomcat:

```
sudo docker run -d --name proxy \
                -p 80:80 \
                --network red_tomcat \
                -v /home/vagrant/tomcat/default.conf:/etc/nginx/conf.d/default.conf:ro \
                nginx
```

![](/Tema3/im3/Screenshot_14.png)

El servicio estará accesible en http://localhost.

![](/Tema3/im3/Screenshot_15.png)
