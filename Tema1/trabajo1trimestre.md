# Instalación del servidor web Apache

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

# Activar los módulos necesarios para ejecutar php y acceder a mysql

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

# Instala y configura wordpress

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

