# Ejemplos Docker Módulo 4

Este repositorio contiene ejemplos prácticos de despliegue de aplicaciones utilizando Docker. Se presentan diferentes escenarios, incluyendo el despliegue de una aplicación de temperaturas con docker compose y un entorno WordPress con MariaDB con docker compose.

## Despliegue de la aplicación Temperaturas

Pasos:

1. Definición del archivo docker-compose.yml.
Antes de comenzar, se crea un archivo docker-compose.yml que define la estructura de la aplicación Temperaturas. Este archivo contiene la configuración para dos servicios: frontend y backend.

![](/Tema3/img4/Screenshot_1.png)

```yaml
version: '3.1'
services:
  frontend:
    container_name: temperaturas-frontend
    image: iesgn/temperaturas_frontend
    restart: always
    ports:
      - 8081:3000
    environment:
      TEMP_SERVER: temperaturas-backend:5000
    depends_on:
      - backend
  backend:
    container_name: temperaturas-backend
    image: iesgn/temperaturas_backend
    restart: always
```

2. Despliegue de los contenedores.
Ahora, vamos a utilizar Docker Compose para desplegar los contenedores definidos en el archivo docker-compose.yml. El comando "up -d" crea y inicia los contenedores en modo detached (en segundo plano).

```
sudo docker compose up -d
```

![](/Tema3/img4/Screenshot_3.png)

3. Verificación del estado de los contenedores.
Para asegurarnos de que los contenedores se han iniciado correctamente, vamos a listar los contenedores en ejecución.

```
sudo docker ps
```

![](/Tema3/img4/Screenshot_4.png)

![](/Tema3/img4/Screenshot_5.png)

```yaml
version: '3.1'
services:
  wordpress:
    container_name: servidor_wp
    image: wordpress
    restart: always
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: user_wp
      WORDPRESS_DB_PASSWORD: asdasd
      WORDPRESS_DB_NAME: bd_wp
    ports:
      - 80:80
    volumes:
      - wordpress_data:/var/www/html/wp-content
  db:
    container_name: servidor_mysql
    image: mariadb
    restart: always
    environment:
      MYSQL_DATABASE: bd_wp
      MYSQL_USER: user_wp
      MYSQL_PASSWORD: asdasd
      MYSQL_ROOT_PASSWORD: asdasd
    volumes:
      - mariadb_data:/var/lib/mysql
volumes:
    wordpress_data:
    mariadb_data:
```

```
sudo docker compose up -d
```

![](/Tema3/img4/Screenshot_7.png)

```
sudo docker ps
```

![](/Tema3/img4/Screenshot_8.png)

```
sudo docker compose rm
```

![](/Tema3/img4/Screenshot_9.png)
