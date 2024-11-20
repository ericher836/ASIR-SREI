# Trabajando con scripts

Creamos un script para cada uno de los siguientes problemas:

+ Crea un script que añada un puerto de escucha en el fichero de configuración de Apache. El puerto se recibirá como parámetro en la llamada y se comprobará que no esté ya presente en el fichero de configuración.

Primero creamos un archivo ejecutable para escribir el script.

![](/Tema1/img2/Screenshot_1.png)
![](/Tema1/img2/Screenshot_2.png)
![](/Tema1/img2/Screenshot_3.png)
![](/Tema1/img2/Screenshot_4.png)
![](/Tema1/img2/Screenshot_5.png)
![](/Tema1/img2/Screenshot_6.png)
![](/Tema1/img2/Screenshot_6_1.png)
![](/Tema1/img2/Screenshot_6_2.png)
![](/Tema1/img2/Screenshot_6_3.png)
![](/Tema1/img2/Screenshot_6_4.png)
![](/Tema1/img2/Screenshot_7.png)
![](/Tema1/img2/Screenshot_8.png)
![](/Tema1/img2/Screenshot_9.png)
![](/Tema1/img2/Screenshot_10.png)
![](/Tema1/img2/Screenshot_11.png)
![](/Tema1/img2/Screenshot_12.png)
![](/Tema1/img2/Screenshot_13.png)
![](/Tema1/img2/Screenshot_14.png)
![](/Tema1/img2/Screenshot_15.png)
![](/Tema1/img2/Screenshot_16.png)
![](/Tema1/img2/Screenshot_17.png)
![](/Tema1/img2/Screenshot_18.png)
![](/Tema1/img2/Screenshot_19.png)
![](/Tema1/img2/Screenshot_20.png)
![](/Tema1/img2/Screenshot_21.png)
![](/Tema1/img2/Screenshot_22.png)
![](/Tema1/img2/Screenshot_23.png)
![](/Tema1/img2/Screenshot_24.png)
![](/Tema1/img2/Screenshot_25.png)
![](/Tema1/img2/Screenshot_26.png)
![](/Tema1/img2/Screenshot_27.png)
![](/Tema1/img2/Screenshot_28.png)
![](/Tema1/img2/Screenshot_29.png)
![](/Tema1/img2/Screenshot_30.png)
![](/Tema1/img2/Screenshot_31.png)
![](/Tema1/img2/Screenshot_32.png)
![](/Tema1/img2/Screenshot_33.png)
![](/Tema1/img2/Screenshot_34.png)
![](/Tema1/img2/Screenshot_35.png)
![](/Tema1/img2/Screenshot_36.png)
![](/Tema1/img2/Screenshot_37.png)
![](/Tema1/img2/Screenshot_38.png)
![](/Tema1/img2/Screenshot_39.png)
![](/Tema1/img2/Screenshot_40.png)
![](/Tema1/img2/Screenshot_41.png)
![](/Tema1/img2/Screenshot_42.png)
![](/Tema1/img2/Screenshot_43.png)
![](/Tema1/img2/Screenshot_44.png)
![](/Tema1/img2/Screenshot_45.png)
![](/Tema1/img2/Screenshot_46.png)
![](/Tema1/img2/Screenshot_47.png)
![](/Tema1/img2/Screenshot_48.png)
![](/Tema1/img2/Screenshot_49.png)
![](/Tema1/img2/Screenshot_50.png)
![](/Tema1/img2/Screenshot_51.png)
![](/Tema1/img2/Screenshot_52.png)
![](/Tema1/img2/Screenshot_53.png)
![](/Tema1/img2/Screenshot_54.png)
![](/Tema1/img2/Screenshot_55.png)

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

