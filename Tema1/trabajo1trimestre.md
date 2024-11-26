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

```
tar -xzf latest.tar.gz
```

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

Activamos el módulo wsgi para permitir la ejecución de aplicaciones Python.

```
sudo apt-get install libapache2-mod-wsgi-py3
```

![](/Tema1/img2/Screenshot_45.png)

# Crea y despliega una pequeña aplicación python

Primero vamos a crear el direcotio para la aplicación y los logs.

```
cd /var/www/XXX
```

```
mkdir mypythonapp
```

```
mkdir public_html
```

```
mkdir logs
```

![](/Tema1/img2/Screenshot_46.png)

Y creamos la aplicación Python

```
echo '# -*- coding: utf-8 -*-' > mypythonapp/controller.py
```

![](/Tema1/img2/Screenshot_47.png)

Y escribimos el siguiente código dentro del archivo.

```
def application(environ, start_response):
  output = b'<p>Bienvenido a mi <b>PythonApp</b>!!!</p>'
  start_responde('200 OK', [('Content-Type', 'text/html; charset=utf-8')])
  return [output]
```

![](/Tema1/img2/Screenshot_49.png)

Y en la configuración de nuestro dominio XXX agregamos el siguiente código.

```
DocumentRoot /var/www/XXX/public_html
WSGIScriptAlias / /var/www/XXX/mypythonapp/controller.py
ErrorLog /var/www/XXX/logs/error.log
CustomLog /var/www/XXX/logs/access.log combined

<Directory />
  Options FollowSymLinks
  AllowOverride All
</Directory>
```

![](/Tema1/img2/Screenshot_50.png)

Y ya podemos acceder.

![](/Tema1/img2/Screenshot_51.png)

# Protegemos el acceso a la aplicación python mediante autenticación

Creamos dentro de nuestro directorio otro llamado passwd, y creamos las credenciales.

```
mkdir /var/www/XXX/passwd
```

```
htpasswd -c /var/www/XXX/passwd/passwords usuario
```

![](/Tema1/img2/Screenshot_52.png)

Ahora dentro del fichero de configuración del servidor agregamos el siguiente código.

```
<Directory /var/www/XXX/mypythonapp>
  AuthType Basic
  AuthName "Restricted Files"
  AuthUserFile /var/www/XXX/passwd/passwords
  Require user usuario
</Directory>
```

![](/Tema1/img2/Screenshot_53.png)

Y ahora nos pide las credenciales al intentar acceder.

![](/Tema1/img2/Screenshot_54.png)

Una vez introducidas tenemos acceso de nuevo.

![](/Tema1/img2/Screenshot_55.png)

# Instala y configura awstat.

Instalamos el servicio.

```
sudo apt-get install awstats
```

![](/Tema1/img2/Screenshot_56.png)

Y activamos el módulo cgi y reiniciamos apache

```
sudo a2enmod cgi
```

```
sudo systemctl restart apache2
```

![](/Tema1/img2/Screenshot_57.png)

Modificamos el archivo de configuración de awstats.

```
sudo nano /etc/awstats/awstats.conf
```

![](/Tema1/img2/Screenshot_58.png)

Y hacemos los siguientes cambios.

```
SiteDomain="XXX"
```

```
HostAliases="XXX localhost 127.0.0.1"
```

![](/Tema1/img2/Screenshot_59.png)

```
AllowToUpdateStatsFromBrowser=1
```

![](/Tema1/img2/Screenshot_60.png)

Generamos las estadísticas iniciales.

```
sudo /usr/lib/cgi-bin/awstats.pl-config=XXX -update
```

![](/Tema1/img2/Screenshot_61.png)

Y configuramos Apache para awstats.

```
sudo cp -r /usr/lib/cgi-bin /var/www/XXX
```

```
sudo chown -R www-data:www-data /var/www/XXX/cgi-bin
```

```
sudo chmod -R 755 /var/www/XXX/cgi-bin
```

![](/Tema1/img2/Screenshot_62.png)

Vamos a modificar la configuración de awstats en Apache (creamos el archivo).

```
sudo nano /etc/apache2/conf-available/awstats.conf
```

![](/Tema1/img2/Screenshot_63.png)

Y agregamos lo siguiente.

```
Alias /awstatsclasses "/usr/share/awstats/lib"
Alias /awstats-icon "/usr/share/awstats/icon/"
Alias /awstatscss "/usr/share/doc/awstats/examples/css"
ScriptAlias /awstats/ /usr/lib/cgi-bin/
Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
```

![](/Tema1/img2/Screenshot_64.png)

Habilitamos la configuración y reiniciamos Apache.

```
sudo a2enconf awstats
```

```
sudo systemctl reload apache2
```

![](/Tema1/img2/Screenshot_65.png)

Y si accedemos a XXX/awstats/awstats.pl podemos ver las estadísticas de visita de nuestro dominio.

![](/Tema1/img2/Screenshot_66.png)

# Instalación del servidor web nginx

En mi caso yo he elegido nginx para instalar el segundo servidor.

```
sudo apt install nginx
```

![](/Tema1/img2/Screenshot_67.png)

Modificamos su archivo de configuración.

```
sudo nano /etc/nginx/nginx.conf
```

![](/Tema1/img2/Screenshot_68.png)

De forma que el http escuche en el puerto 8080.

```
listen 8080;
listen [::]:8080;
```

![](/Tema1/img2/Screenshot_69.png)

Creamos un nuevo fichero de configuración.

```
sudo nano /etc/nginx/sites-available/default
```

![](/Tema1/img2/Screenshot_70.png)

Y agregamos lo siguiente:

```
listen 8080 default_server;
listen [::]:8080 default_server;
```

![](/Tema1/img2/Screenshot_71.png)

Comprobamos la configuración y reiniciamos nginx.

```
sudo nginx -t
```

```
sudo systemctl restart nginx
```

![](/Tema1/img2/Screenshot_72.png)

Creamos el directorio donde estarán nuestros archivos.

```
sudo mkdir /var/www/nginx
```

![](/Tema1/img2/Screenshot_73.png)

Y dentro creamos un index.html

```
sudo nano /var/www/nginx/index.html
```

![](/Tema1/img2/Screenshot_74.png)

De la siguiente forma.

```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

![](/Tema1/img2/Screenshot_75.png)

Y en el fichero de configuración de antes cambiamos el root a este nuevo directorio.

```
root /var/www/nginx;
```

![](/Tema1/img2/Screenshot_76.png)

Y agregamos el orden de index y el server_name.

```
index index.html index.htm index.nginx-debian.html;

server_name XXX;
```

![](/Tema1/img2/Screenshot_78.png)

Agregamos el nombre del dominio al fichero hosts.

```
sudo nano /etc/hosts
```

![](/Tema1/img2/Screenshot_79.png)

```
127.0.0.1      XXX
```

![](/Tema1/img2/Screenshot_80.png)

Reiniciamos el servidor.

```
sudo systemctl restart nginx
```

![](/Tema1/img2/Screenshot_77.png)

Y ya podemos acceder con el nombre del dominio y el puerto 8080.

![](/Tema1/img2/Screenshot_81.png)

Ahora instalamos phpmyadmin.

```
sudo apt install phpmyadmin
```

![](/Tema1/img2/Screenshot_82.png)

Creamos un enlace simbólico.

```
sudo ln -s /usr/share/phpmyadmin /var/www/nginx/phpmyadmin
```

![](/Tema1/img2/Screenshot_83.png)

Y modificamos los permisos.

```
sudo chown -R www-data:www-data /usr/share/phpmyadmin
```

```
sudo chmod 755 /usr/share/phpmyadmin
```

![](/Tema1/img2/Screenshot_84.png)

En el fichero de configuración de nuestro sitio agregamos lo siguiente.

```
location / {
  try_files $uri $uri/ =404;
}

location /phpmyadmin {
  root /var/www/nginx;
  index index.php index.html;

  location ~ ^/phpmyadmin/(doc|sql|setup)/ {
    deny all;
  }

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    include fastcgi_params;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
  }
}
```

![](/Tema1/img2/Screenshot_85.png)

Instalamos php-fpm.

```
sudo apt install php8.1-fpm
```

![](/Tema1/img2/Screenshot_86.png)

Y ahora podemos acceder a phpmyadmin en nuestro dominio con XXX:8080/phpmyadmin.

![](/Tema1/img2/Screenshot_87.png)

Vamos a crear un usuario para entrar.

```
sudo mysql -y root -p
```

```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'usuario';
```

```
exit;
```

![](/Tema1/img2/Screenshot_88.png)

Y ya tenemos phpmyadmin listo y configurado.

![](/Tema1/img2/Screenshot_89.png)
