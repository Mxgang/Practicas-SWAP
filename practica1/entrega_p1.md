**--------Configuración previa**

He usado 2 máquinas de Ubuntu Server, donde le he instalado LAMP y openSSH.
En ambas le he puesto 2 adaptadores de red, una de NAT y otra de red Interna, donde en la red Interna ambas tiene el mismo nombre.

En la configuración de /etc/network/interfaces he puesto lo siguiente:

auto enp0s9

ifacce enp0s9 inet static

address 192.168.1.100

netmask 255.2555.255.0

network 192.168.1.0

broadcast 192.168.1.255


En la segunda máquina he puesto lo mismo salvo en address que ha sido 192.168.1.101



En ambos ejercicios he adjuntado 2 imágenes.

**---------Ejercicio SSH**

Para conectar con ssh simplemente he configurado ambas tarjetas de red en primer lugar, luego he usado el comando en una de las máquinas:
$> ssh 192.168.1.100
Y he tenido que introducir la contraseña de la máquina a la que me conecto.
![img](https://i.imgur.com/HzhYpVK.png)

**---------Ejercicio curl**

Para esto creo en la máquina 1 un archivo llamado swap.html en la carpeta var/www/html
En la máquina 2 uso el comando: 
$> curl http://192.168.1.100/swap.html
Con esto me muestra el contenido de swap.html de la máquina 2.
![img](https://i.imgur.com/qRZeahH.png)

