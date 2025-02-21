# Creación de la VPC

Primero nos dirigimos al panel de VPC en AWS y le damos a Crear VPC.

![](/Tema2/img2/Screenshot_2.png)

Una vez aquí, la configuramos de la siguiente forma para tener 2 subredes públicas y 2 subredes pivadas.

![](/Tema2/img2/Screenshot_3.png)
![](/Tema2/img2/Screenshot_4.png)
![](/Tema2/img2/Screenshot_5.png)

Y ya se está creando la VPC.

![](/Tema2/img2/Screenshot_6.png)

Aquí podemos ver todos sus detalles.

![](/Tema2/img2/Screenshot_7.png)

Y el grupo de seguridad que usaremos para todas nuestras máquinas.

![](/Tema2/img2/Screenshot_8.png)

# Creación de la instancia

En EC2 vamos a lanzar una instancia.

![](/Tema2/img2/Screenshot_9.png)

Y la configuramos de la siguiente forma para crear una máquina en la subred pública.

![](/Tema2/img2/Screenshot_10.png)
![](/Tema2/img2/Screenshot_11.png)

En el grupo de seguridad debemos seleccionar el de la vpc por defecto, no crear uno como aparece en la imagen.

![](/Tema2/img2/Screenshot_12.png)
![](/Tema2/img2/Screenshot_13.png)

Y ya está creada la instancia, llamada practica1_1_pub

![](/Tema2/img2/Screenshot_14.png)
![](/Tema2/img2/Screenshot_15.png)

# Creación del EFS

Nos dirigimos a EFS en AWS y creamos un sistema de archivos.

![](/Tema2/img2/Screenshot_26.png)

Importante colocarlo en nuestra VPC.

![](/Tema2/img2/Screenshot_27.png)

Y en nuestro grupo de seguridad permitimos el NFS, el SSH, el HTTP y el MYSQL; para más adelante.

![](/Tema2/img2/Screenshot_41.png)

Para utilizar el EFS necesitamos ejecutar el siguiente comando para instalar los útiles de NFS.

```
sudo apt install nfs-common
```

![](/Tema2/img2/Screenshot_35.png)

# Instalación de Apache y PHP

Apache nos servirá para montar dentro Wordpress y PHP es necesario para ejecutar los archivos de este.
Primero actualizamos la lista de paquetes disponibles en los repositorios configurados en el sistema.

```
sudo apt update
```

![](/Tema2/img2/Screenshot_56.png)

E instalamos Apache.

```
sudo apt install apache2
```

![](/Tema2/img2/Screenshot_57.png)

Y lo iniciamos y habilitamos.

```
sudo systemctl start apache2
```

```
sudo systemctl enable apache2
```

![](/Tema2/img2/Screenshot_58.png)

Y ya está Apache funcionando.

![](/Tema2/img2/Screenshot_59.png)

Ahora añadimos el repositorio de PHP, ya que no estaba en mi sistema.

```
sudo add-apt-repository ppa:ondrej/php
```

![](/Tema2/img2/Screenshot_61.png)

E instalamos todos los útiles.

```
sudo apt install php7.4 libapache2-mod-php7.4 php7.4-cli
```

![](/Tema2/img2/Screenshot_62.png)

```
sudo apt install php7.4-mysql
```

![](/Tema2/img2/Screenshot_63.png)

Vemos que PHP se ha instalado correctamente

```
php -v
```

![](/Tema2/img2/Screenshot_64.png)

# Creación de la base de datos

Primero nos dirigimos al apartado de base de datos en AWS (RDS)

![](/Tema2/img2/Screenshot_42.png)

Y seleccionamos la siguiente configuración para crear la base de datos.

![](/Tema2/img2/Screenshot_65.png)
![](/Tema2/img2/Screenshot_66.png)
![](/Tema2/img2/Screenshot_67.png)
![](/Tema2/img2/Screenshot_68.png)

Importante elegir nuestra VPC.

![](/Tema2/img2/Screenshot_69.png)
![](/Tema2/img2/Screenshot_70.png)

Podemos crear una base de datos inicial.

![](/Tema2/img2/Screenshot_71.png)

Y una vez creada vamos a conectarla la una máquina EC2.

![](/Tema2/img2/Screenshot_72.png)
![](/Tema2/img2/Screenshot_73.png)
![](/Tema2/img2/Screenshot_74.png)

# Instalación y configuración de Wordpress

Para ello, dentro de la máquina, descargamos el directorio de Wordpress en el directorio de Apache.

```
wget http://wordpress.org/latest.tar.gz
```

![](/Tema2/img2/Screenshot_75.png)

Y descomprimimos el fichero que hemos descargado.

```
sudo tar -xf latest.tar.gz
```

![](/Tema2/img2/Screenshot_76.png)

Yo voy a dejar el directorio limpio.

```
sudo rm -R latest.tar.gz
```

```
sudo rm -R index.html
```

![](/Tema2/img2/Screenshot_77.png)

Y extraemos el contenido de Wordpress en el directorio de Apache.

```
sudo cp -r wordpress/* /var/www/html/
```

![](/Tema2/img2/Screenshot_78.png)

Ahora vamos a hacer la conexión con la base de datos.

```
mysql -u admin -h NOMBRE_DEL_HOST -p
```

![](/Tema2/img2/Screenshot_79.png)

Y dentro de MySQL creamos una base de datos y un usuario con todos los privilegios.

```
CREATE DATABASE wordpress;
```

```
CREATE USER 'wordpress_user'@'%' IDENTIFIED BY 'password123';
```

```
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress_user'@'%';
```

```
FLUSH PRIVILEGES;
```

![](/Tema2/img2/Screenshot_80.png)

hola

![](/Tema2/img2/Screenshot_81.png)
![](/Tema2/img2/Screenshot_82.png)
![](/Tema2/img2/Screenshot_83.png)
![](/Tema2/img2/Screenshot_84.png)
![](/Tema2/img2/Screenshot_85.png)
![](/Tema2/img2/Screenshot_86.png)
![](/Tema2/img2/Screenshot_87.png)
![](/Tema2/img2/Screenshot_88.png)
![](/Tema2/img2/Screenshot_89.png)
![](/Tema2/img2/Screenshot_90.png)
![](/Tema2/img2/Screenshot_91.png)
![](/Tema2/img2/Screenshot_92.png)
![](/Tema2/img2/Screenshot_92_1.png)
![](/Tema2/img2/Screenshot_93.png)
![](/Tema2/img2/Screenshot_94.png)
