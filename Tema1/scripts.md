# Trabajando con scripts

Creamos un script para cada uno de los siguientes problemas:

+ Crea un script que añada un puerto de escucha en el fichero de configuración de Apache. El puerto se recibirá como parámetro en la llamada y se comprobará que no esté ya presente en el fichero de configuración.

Primero creamos un archivo ejecutable para escribir el script.

![](/Tema1/img/Screenshot_44.png)

Y dentro de él escribimos lo siguiente:

```
#!/bin/bash

if [ $# -eq 0 ]; then
  echo "ERROR. No se han pasado parámetros para el número de puerto de escucha"
elif grep -q "Listen $1" /etc/apache2/ports.conf; then
  echo "ERROR. El puerto ya existe"
else
  cp /etc/apache2/ports.conf /etc/apache2/ports.conf.bak
  echo "Listen $1" >> /etc/apache2/ports.conf
  echo "Puerto $1 añadido al fichero de escucha de puertos"
fi
```

![](/Tema1/img/Screenshot_45.png)

Hacemos las comprobaciones.

![](/Tema1/img/Screenshot_46.png)

Y comprobamos que de verdad se ha añadido al fichero.

![](/Tema1/img/Screenshot_44_1.png)

+ Crea un script que añada un nombre de dominio y una ip al fichero hosts. Debemos comprobar que no existe dicho dominio en el fichero hosts

Primero creamos un archivo ejecutable para escribir el script y dentro de él escribimos lo siguiente:

```
#!/bin/bash

if [ $# -lt 2 ]; then
  echo "ERROR. No se han pasado suficientes parámetros"
elif grep -q "$2    $1" /etc/hosts; then
  echo "ERROR. La IP en conjunto a ese nombre de dominio existe"
else
  cp /etc/hosts /etc/hosts.bak
  echo "$2    $1" >> /etc/hosts
  echo "La IP $2 y el nombre de dominio $1 han sido añadidos al fichero de hosts"
fi
```

![](/Tema1/img/Screenshot_47.png)

Hacemos las comprobaciones.

![](/Tema1/img/Screenshot_48.png)

Y comprobamos que de verdad se ha añadido al fichero.

![](/Tema1/img/Screenshot_49.png)

Reiniciamos el servicio.

![](/Tema1/img/Screenshot_50.png)

Y vemos que ahora al introducir ese nombre de dominio, nos lleva a la IP que hemos introducido.

![](/Tema1/img/Screenshot_51.png)

+ Crea un script que nos permita crear una página web con un título, una cabecera y un mensaje

Primero creamos un archivo ejecutable para escribir el script y dentro de él escribimos lo siguiente:

```
#!/bin/bash

if [ $# -eq 0 ]; then
  echo "ERROR. No se han pasado parámetros para el nombre de la página"
elif ls /var/www/mi_dominio | grep -q "$1"; then
  echo "La página ya existe"
else
  echo "Escriba el título"
  read tit
  echo "Escriba la cabecera"
  read cab
  echo "Escriba el mensaje"
  read men
  echo "<!DOCTYPE html>" >> /var/www/mi_dominio/$1.html
  echo "<html>" >> /var/www/mi_dominio/$1.html
  echo "<head>" >> /var/www/mi_dominio/$1.html
  echo "<title>$tit</title>" >> /var/www/mi_dominio/$1.html
  echo "</head>" >> /var/www/mi_dominio/$1.html
  echo "<body>" >> /var/www/mi_dominio/$1.html
  echo "<h1>$cab</h1>" >> /var/www/mi_dominio/$1.html
  echo "<p>$men</p>" >> /var/www/mi_dominio/$1.html
  echo "</body>" >> /var/www/mi_dominio/$1.html
  echo "</html>" >> /var/www/mi_dominio/$1.html
fi
```

![](/Tema1/img/Screenshot_52.png)
![](/Tema1/img/Screenshot_53.png)
![](/Tema1/img/Screenshot_54.png)
![](/Tema1/img/Screenshot_55.png)
![](/Tema1/img/Screenshot_56.png)
