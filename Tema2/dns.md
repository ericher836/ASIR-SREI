# Instalación del servidor DNS Bind

Primero actualizamos la lista de paquetes disponibles en los repositorios configurados en el sistema.

```
sudo apt update
```

```
sudo apt upgrade
```

![](/Tema2/img/Screenshot_1.png)

Y reiniciamos el sistema.

```
sudo reboot
```

![](/Tema2/img/Screenshot_2.png)

Finalmente instalamos el servicio de Bind.

```
sudo apt-get install bind9 bind9utils bind9-doc
```

![](/Tema2/img/Screenshot_3.png)

Una vez hecho, vamos a la carpeta de configuración del servicio.

```
sudo nano /etc/bind/named.conf.options
```

![](/Tema2/img/Screenshot_4.png)

Dentro del archivo, agregamos la siguiente configuración:

```
acl goodclients {
        RED Y MÁSCARA;
        localhost;
        localnets;
};

options {
        directory "/var/cache/bind";
        recursion yes;
        allow-query { goodclients; };

        forwarders {
                8.8.8.8;
                8.8.4.4;
        };
        forward only;

        dnssec-validation yes;
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
```

![](/Tema2/img/Screenshot_5.png)
![](/Tema2/img/Screenshot_6.png)

Ejecutamos el siguiente comando para asegurarnos de que no hay ningún problema.

```
sudo named-checkconf
```

![](/Tema2/img/Screenshot_7.png)

Y reiniciamos el servidor Bind.

```
sudo systemctl restart bind9
```

![](/Tema2/img/Screenshot_8.png)

Vamos a permitir a Bind por el cortafuegos para que no ocurra ningún problema posible.

```
sudo ufw allow Bind9
```

![](/Tema2/img/Screenshot_9.png)

Podemos ejecutar el siguiente comando para que el servidor recoja logs de lo que ocurre.

```
sudo journalctl -u bind9 -f
```

![](/Tema2/img/Screenshot_10.png)

Y ahora vamos a poner como servidor DNS de nuestro servidor nuestra propia dirección IP.

```
sudo nano /etc/resolv.conf
```

![](/Tema2/img/Screenshot_11.png)

```
nameserver DIRECCIÓN IP
```

![](/Tema2/img/Screenshot_12.png)

Y comprobamos que el DNS resuelve los nombres correctamente haciendo ping.

```
ping -c 1 google.com
```

![](/Tema2/img/Screenshot_13.png)

Ahora cambiamos el servidor DNS de una máquina de la misma red para comprobar que también funciona en otros clientes.

![](/Tema2/img/Screenshot_14.png)

Y funciona correctamente.

```
ping google.com
```

![](/Tema2/img/Screenshot_15.png)
