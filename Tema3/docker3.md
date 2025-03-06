# Ejemplos Docker Módulo 3

## Despliegue de la aplicación Temperaturas

```
sudo docker network create red_temperaturas
```

![](/Tema3/im3/Screenshot_1.png)

```
sudo docker run -d --name temperaturas-backend --network red_temperaturas iesgn/temperaturas_backend
```

![](/Tema3/im3/Screenshot_2.png)

```
docker run -d -p 3000:3000 --name temperaturas-frontend --network red_temperaturas iesgn/temperaturas_frontend
```

![](/Tema3/im3/Screenshot_3.png)
![](/Tema3/im3/Screenshot_4.png)

## Despliegue de Wordpress + mariadb

```
sudo docker network create red_wp
```

![](/Tema3/im3/Screenshot_5.png)

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

```
sudo docker ps
```

![](/Tema3/im3/Screenshot_8.png)
![](/Tema3/im3/Screenshot_9.png)

## Despliegue de tomcat + nginx

```
sudo docker network create red_tomcat
```

![](/Tema3/im3/Screenshot_10.png)
![](/Tema3/im3/Screenshot_11.png)
![](/Tema3/im3/Screenshot_12.png)

```
sudo docker run -d --name aplicacionjava \
                --network red_tomcat \
                -v /home/vagrant/tomcat/sample.war:/usr/local/tomcat/webapps/sample.war:ro \
                tomcat:9.0
```

![](/Tema3/im3/Screenshot_13.png)

```
sudo docker run -d --name proxy \
                -p 80:80 \
                --network red_tomcat \
                -v /home/vagrant/tomcat/default.conf:/etc/nginx/conf.d/default.conf:ro \
                nginx
```

![](/Tema3/im3/Screenshot_14.png)
![](/Tema3/im3/Screenshot_15.png)
