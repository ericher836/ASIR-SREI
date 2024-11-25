# Instalación del servidor web Apache

Primero actualizamos la lista de paquetes disponibles en los repositorios configurados en el sistema.

```
sudo apt update
```

![](/Tema1/img2/Screenshot_1.png)

```
sudo apt upgrade
```

![](/Tema1/img2/Screenshot_2.png)

E instalamos el servicio de Apache.

```
sudo apt install apache2
```

![](/Tema1/img2/Screenshot_3.png)

Vamos a comprobar nuestra dirección IP para ver si se ha instalado correctamente (también podemos hacerlo con localhost).

```
sudo apt install net-tools
```

![](/Tema1/img2/Screenshot_4.png)

```
ifconfig
```

![](/Tema1/img2/Screenshot_5.png)

Y vemos que funciona correctamente el servicio de servidor.

![](/Tema1/img2/Screenshot_6.png)

Ahora vamos a añadir al fichero hosts el nombre de dominio que tendremos para cada uno de ellos.

![](/Tema1/img2/Screenshot_6_1.png)

Comprobamos y reiniciamos Apache.

```
apachectl configtest
```

```
sudo service apache2 restart
```

![](/Tema1/img2/Screenshot_6_2.png)

Y podemos observar que el DNS funciona. He modificado el index.html del dominio para que aparezca la siguiente página.

![](/Tema1/img2/Screenshot_6_3.png)
![](/Tema1/img2/Screenshot_6_4.png)

# Activar los módulos necesarios para ejecutar php y acceder a mysql

Instalamos el servicio de mysql.

```
sudo apt install mysql-server
```

![](/Tema1/img2/Screenshot_7.png)

```
sudo mysql_secure_installation
```

![](/Tema1/img2/Screenshot_8.png)
![](/Tema1/img2/Screenshot_9.png)
![](/Tema1/img2/Screenshot_10.png)
![](/Tema1/img2/Screenshot_11.png)
![](/Tema1/img2/Screenshot_12.png)

Comprobamos que funciona.

```
sudo mysql
```

![](/Tema1/img2/Screenshot_13.png)

```
exit
```

![](/Tema1/img2/Screenshot_14.png)

Y a continuación instalamos php.

```
sudo apt install php libapache2-mod-php php-mysql
```

![](/Tema1/img2/Screenshot_15.png)

Y comprobamos que está instalado revisando su versión.

```
php -v
```

![](/Tema1/img2/Screenshot_16.png)

# Instala y configura wordpress

Primero vamos a crear la estructura de directorios de cada dominio.

```
sudo mkdir /var/www/XXX
```

![](/Tema1/img2/Screenshot_17.png)

```
sudo chown -R $USER:$USER /var/www/XXX
```

![](/Tema1/img2/Screenshot_18.png)

Y también su fichero de configuración.

```
sudo nano /etc/apache2/sites-available/XXX.conf
```

![](/Tema1/img2/Screenshot_19.png)

```
<VirtualHost *:80>
  ServerName centro.intranet
  ServerAlias www.centro.intranet
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/XXX
  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

![](/Tema1/img2/Screenshot_20.png)

Y de igual forma para el otro.

![](/Tema1/img2/Screenshot_21.png)

Activamos los sitios.

```
sudo a2ensite XXX
```

![](/Tema1/img2/Screenshot_22.png)

Y en mi caso desactivo uno que ya tenía activado de antes, para que no moleste.

```
sudo a2dissite XXX
```

![](/Tema1/img2/Screenshot_23.png)

Comprobamos Apache y reiniciamos.

```
apachectl configtest
```

![](/Tema1/img2/Screenshot_24.png)

```
sudo service apache2 restart
```

![](/Tema1/img2/Screenshot_25.png)

```
sudo systemctl reload apache2
```

![](/Tema1/img2/Screenshot_26.png)
![](/Tema1/img2/Screenshot_27.png)

Instalamos MariaDB.

```
sudo apt-get install mariadb-client mariadb-server
```

![](/Tema1/img2/Screenshot_28.png)

Y también descargamos el directorio de WordPress.

```
sudo wget https://wordpress.org/latest.tar.gz
```

![](/Tema1/img2/Screenshot_29.png)

Lo descomprimimos.

tar -xzf latest.tar.gz

![](/Tema1/img2/Screenshot_30.png)

Y podemos ver la carpeta en el directorio principal.

```
ls
```

![](/Tema1/img2/Screenshot_31.png)

Vamos a moverlo a nuestro directorio.

```
sudo mv wordpress/* /var/www/XXX/
```

![](/Tema1/img2/Screenshot_32.png)

```
ls /var/www/XXX
```

![](/Tema1/img2/Screenshot_33.png)

Y ahora a hacer una copia del fichero de configuración para configurarlo más tarde.

```
sudo cp /var/www/XXX/wp-config-sample.php /var/www/XXX/wp-config.php
```

![](/Tema1/img2/Screenshot_34.png)

Entramos en MariaDB.

```
sudo mariadb
```

![](/Tema1/img2/Screenshot_35.png)

Y creamos una base de datos para WordPress.

```
create database wordpress;
```

```
create user 'usuario' identified by  '1234';
```

```
grant all privileges on wordpress.* to 'usuario' identified by '1234';
```

```
quit;
```

![](/Tema1/img2/Screenshot_36.png)

Configuramos WordPress.

```
sudo nano /var/www/XXX/wp-config.php
```

![](/Tema1/img2/Screenshot_37.png)

```
define( 'DB_NAME', 'wordpress' );

define( 'DB_USER', 'usuario' );

define( 'DB_PASSWORD', '1234' );
```

![](/Tema1/img2/Screenshot_38.png)

Y ahora al acceder a la página veremos el siguiente asistente de instalación.

![](/Tema1/img2/Screenshot_39.png)
![](/Tema1/img2/Screenshot_40.png)
![](/Tema1/img2/Screenshot_41.png)

Una vez instalado iniciamos sesión.

![](/Tema1/img2/Screenshot_42.png)

Y vemos la página de configuración de administrador.

![](/Tema1/img2/Screenshot_43.png)

Pero al entrar en la página principal de nuestro dominio veremos la página principal de WordPress.

![](/Tema1/img2/Screenshot_44.png)

# Activar el módulo wsgi

![](/Tema1/img2/Screenshot_45.png)

# Crea y despliega una pequeña aplicación python

![](/Tema1/img2/Screenshot_46.png)
![](/Tema1/img2/Screenshot_47.png)
![](/Tema1/img2/Screenshot_48.png)
![](/Tema1/img2/Screenshot_49.png)
![](/Tema1/img2/Screenshot_50.png)
![](/Tema1/img2/Screenshot_51.png)

# Protegemos el acceso a la aplicación python mediante autenticación

![](/Tema1/img2/Screenshot_52.png)
![](/Tema1/img2/Screenshot_53.png)
![](/Tema1/img2/Screenshot_54.png)
![](/Tema1/img2/Screenshot_55.png)

# Instala y configura awstat.

![](/Tema1/img2/Screenshot_56.png)
![](/Tema1/img2/Screenshot_57.png)
![](/Tema1/img2/Screenshot_58.png)
![](/Tema1/img2/Screenshot_59.png)
![](/Tema1/img2/Screenshot_60.png)
![](/Tema1/img2/Screenshot_61.png)
![](/Tema1/img2/Screenshot_62.png)
![](/Tema1/img2/Screenshot_63.png)
![](/Tema1/img2/Screenshot_64.png)
![](/Tema1/img2/Screenshot_65.png)
![](/Tema1/img2/Screenshot_66.png)
![](/Tema1/img2/Screenshot_67.png)

# Instalación del servidor web nginx

![](/Tema1/img2/Screenshot_68.png)
![](/Tema1/img2/Screenshot_69.png)
![](/Tema1/img2/Screenshot_70.png)
![](/Tema1/img2/Screenshot_71.png)
![](/Tema1/img2/Screenshot_72.png)
![](/Tema1/img2/Screenshot_73.png)
![](/Tema1/img2/Screenshot_74.png)
![](/Tema1/img2/Screenshot_75.png)
![](/Tema1/img2/Screenshot_76.png)
![](/Tema1/img2/Screenshot_77.png)
![](/Tema1/img2/Screenshot_78.png)
![](/Tema1/img2/Screenshot_79.png)
![](/Tema1/img2/Screenshot_80.png)
![](/Tema1/img2/Screenshot_81.png)
![](/Tema1/img2/Screenshot_82.png)
![](/Tema1/img2/Screenshot_83.png)
![](/Tema1/img2/Screenshot_84.png)
![](/Tema1/img2/Screenshot_85.png)
![](/Tema1/img2/Screenshot_86.png)
![](/Tema1/img2/Screenshot_87.png)
![](/Tema1/img2/Screenshot_88.png)
![](/Tema1/img2/Screenshot_89.png)

