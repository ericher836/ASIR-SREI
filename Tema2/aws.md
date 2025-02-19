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

Y en nuestro grupo de seguridad permitimos el NFS, el SSH, el HTTP y el MYSQL, para más adelante.

![](/Tema2/img2/Screenshot_41.png)

Para utilizar el EFS necesitamos ejecutar el siguiente comando para instalar los útiles de NFS.

```
sudo apt install nfs-common
```

![](/Tema2/img2/Screenshot_35.png)

# Instalación de Apache y PHP

```
sudo apt update
```

![](/Tema2/img2/Screenshot_56.png)
![](/Tema2/img2/Screenshot_57.png)
![](/Tema2/img2/Screenshot_58.png)
![](/Tema2/img2/Screenshot_59.png)
![](/Tema2/img2/Screenshot_60.png)
![](/Tema2/img2/Screenshot_61.png)
![](/Tema2/img2/Screenshot_62.png)
![](/Tema2/img2/Screenshot_63.png)
![](/Tema2/img2/Screenshot_64.png)

# Creación de la base de datos

![](/Tema2/img2/Screenshot_42.png)
![](/Tema2/img2/Screenshot_43.png)
![](/Tema2/img2/Screenshot_44.png)
![](/Tema2/img2/Screenshot_65.png)
![](/Tema2/img2/Screenshot_66.png)
![](/Tema2/img2/Screenshot_67.png)
![](/Tema2/img2/Screenshot_68.png)
![](/Tema2/img2/Screenshot_69.png)
![](/Tema2/img2/Screenshot_70.png)
![](/Tema2/img2/Screenshot_71.png)
![](/Tema2/img2/Screenshot_72.png)
![](/Tema2/img2/Screenshot_73.png)
![](/Tema2/img2/Screenshot_74.png)

# Instalación y configuración de Wordpress

![](/Tema2/img2/Screenshot_75.png)
![](/Tema2/img2/Screenshot_76.png)
![](/Tema2/img2/Screenshot_77.png)
![](/Tema2/img2/Screenshot_78.png)
![](/Tema2/img2/Screenshot_79.png)
![](/Tema2/img2/Screenshot_80.png)
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
