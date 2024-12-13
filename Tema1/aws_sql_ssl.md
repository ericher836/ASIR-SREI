# Instalación del servidor web Apache

Primero actualizamos la lista de paquetes disponibles en los repositorios configurados en el sistema.

```
sudo apt update
```

![](/Tema1/img3/Screenshot_20.png)

```
sudo apt upgrade
```

![](/Tema1/img3/Screenshot_21.png)

E instalamos Apache.

```
sudo apt-get install apache2
```

![](/Tema1/img3/Screenshot_22.png)

# Autenticación MySQL

Primero instalamos PHP, MySQL y MariaDB.

```
sudo apt-get install apache2 php7.0 libapruti11-dbd-mysql -y
```

![](/Tema1/img3/Screenshot_23.png)

```
sudo apt-get install mariadb-server mariadb-client -y
```

![](/Tema1/img3/Screenshot_24.png)

Y activamos los servicios.

```
sudo systemctl enable apache2
```

```
sudo systemctl enable mysql
```

![](/Tema1/img3/Screenshot_25.png)

Entramos en mysql.

```
sudo mysql -u root -p
```

Y creamos una base de datos.

```
create database defaultsite_db;
```

![](/Tema1/img3/Screenshot_26.png)

Le damos permisos totales al admin.

```
GRANT SELECT, INSERT, UPDATE, DELETE ON defaultsite_db.* TO 'defaultsite_admin'@'localhost' IDENTIFIED BY 'usuario';
```

![](/Tema1/img3/Screenshot_27.png)

```
GRANT SELECT, INSERT, UPDATE, DELETE ON defaultsite_db.* TO 'defaultsite_admin'@'localhost.localdomain' IDENTIFIED BY 'password';
```

![](/Tema1/img3/Screenshot_28.png)

```
flush privileges;
```

![](/Tema1/img3/Screenshot_29.png)

Entramos en la base de datos.

```
use defaultsite_db;
```

![](/Tema1/img3/Screenshot_30.png)

Y creamos una tabla para los usuarios autenticados.

```
create table mysql_auth ( username varchar(191) not null, passwd varchar(191), groups varchar(191), primary key (username) );
```

![](/Tema1/img3/Screenshot_31.png)

Transformamos una contraseña a hash para hacerlo más seguro.

```
htpasswd -bns siteuser siteuser
```

![](/Tema1/img3/Screenshot_32.png)

E insertamos los datos en la tabla que hemos creado en la base de datos.

```
INSERT INTO `mysql_auth` (`username`, `passwd`, `groups`) VALUES('siteuser', '{SHA}tk7HEH6Wo7SKT6+3FHCgiGnJ6dA=', 'sitegroup');
```

![](/Tema1/img3/Screenshot_33.png)

Habilitamos los módulos necesarios.

```
sudo a2enmod dbd
```

```
sudo a2enmod authn_dbd
```

```
sudo a2enmod socache_shmcb
```

```
sudo a2enmod authn_socache
```

![](/Tema1/img3/Screenshot_34.png)

Creamos el directorio que estará protegido.

```
sudo mkdir /var/www/html/protecteddir
```

```
sudo chown -R www-data:www-data /var/www/html/protecteddir
```

![](/Tema1/img3/Screenshot_35.png)

Y modificamos la configuración de Apache de nuestro dominio.

```
sudo nano /etc/apache2/sites-available/000-default.conf
```

![](/Tema1/img3/Screenshot_36.png)

Introducimos lo siguiente.

```
DBDriver mysql
DBDParams "dbname=defaultsite_db user=defaultsite_admin pass=usuario"
 
DBDMin 4 
DBDKeep 8 
DBDMax 20 
DBDExptime 300
 
<Directory "/var/www/html/protecteddir"> 
# mod_authn_core and mod_auth_basic configuration 
# for mod_authn_dbd 
AuthType Basic 
AuthName "My Server"
 
# To cache credentials, put socache ahead of dbd here 
AuthBasicProvider socache dbd
 
# Also required for caching: tell the cache to cache dbd lookups! 
AuthnCacheProvideFor dbd 
AuthnCacheContext my-server
 
# mod_authz_core configuration 
Require valid-user
 
# mod_authn_dbd SQL query to authenticate a user 
AuthDBDUserPWQuery "SELECT passwd FROM mysql_auth WHERE username = %s"
```

![](/Tema1/img3/Screenshot_37.png)

Y reiniciamos Apache.

```
sudo systemctl restart apache2
```

![](/Tema1/img3/Screenshot_38.png)
![](/Tema1/img3/Screenshot_39.png)
![](/Tema1/img3/Screenshot_40.png)
![](/Tema1/img3/Screenshot_41.png)

# Instalación del servidor web Apache

```
sudo uf allow "Apache Full"
```

![](/Tema1/img3/Screenshot_42.png)

```
sudo a2enmod ssl
```

![](/Tema1/img3/Screenshot_43.png)

```
sudo systemctl restart apache2
```

![](/Tema1/img3/Screenshot_44.png)

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt
```

![](/Tema1/img3/Screenshot_45.png)

```
Country Name (2 letter code) [XX]:ES
State or Province Name (full name) []:Huelva
Locality Name (eg, city) [Default City]:Huelva
Organization Name (eg, company) [Default Company Ltd]:LAMARISMA
Organizational Unit Name (eg, section) []:ASIR
Common Name (eg, your name or your server's hostname) []:tu_ip
Email Address []:webmaster@example.com
```

![](/Tema1/img3/Screenshot_46.png)

```
sudo nano /etc/apache2/sites-available/000-default.conf
```

![](/Tema1/img3/Screenshot_47.png)

```
<VirtualHost *:443>
   ServerName tu_ip
   DocumentRoot /var/www/html
```

```
   SSLEngine on
   SSLCertificateFile /etc/ssl/certs/apache-selfsigned.crt
   SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key
</VirtualHost>
```

![](/Tema1/img3/Screenshot_48.png)
![](/Tema1/img3/Screenshot_49.png)

```
sudo apache2ctl configtest
```

```
sudo systemctl reload apache2
```

![](/Tema1/img3/Screenshot_50.png)
![](/Tema1/img3/Screenshot_54.png)
![](/Tema1/img3/Screenshot_55.png)
![](/Tema1/img3/Screenshot_56.png)
![](/Tema1/img3/Screenshot_57.png)
