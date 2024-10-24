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
```

![](/Tema1/img/Screenshot_44.png)
![](/Tema1/img/Screenshot_45.png)
![](/Tema1/img/Screenshot_46.png)
![](/Tema1/img/Screenshot_44.1.png)

+ Crea un script que añada un nombre de dominio y una ip al fichero hosts. Debemos comprobar que no existe dicho dominio en el fichero hosts

![](/Tema1/img/Screenshot_47.png)
![](/Tema1/img/Screenshot_48.png)
![](/Tema1/img/Screenshot_49.png)
![](/Tema1/img/Screenshot_50.png)
![](/Tema1/img/Screenshot_51.png)

+ Crea un script que nos permita crear una página web con un título, una cabecera y un mensaje

![](/Tema1/img/Screenshot_52.png)
![](/Tema1/img/Screenshot_53.png)
![](/Tema1/img/Screenshot_54.png)
![](/Tema1/img/Screenshot_55.png)
![](/Tema1/img/Screenshot_56.png)
