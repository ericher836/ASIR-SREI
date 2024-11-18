# Trabajando con scripts

Creamos un script para cada uno de los siguientes problemas:

+ Crea un script que añada un puerto de escucha en el fichero de configuración de Apache. El puerto se recibirá como parámetro en la llamada y se comprobará que no esté ya presente en el fichero de configuración.

Primero creamos un archivo ejecutable para escribir el script.

![](/Tema1/img2/Screenshot_1.png)

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

