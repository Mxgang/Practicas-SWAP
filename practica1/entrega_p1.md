En ambos ejercicios he adjuntado 2 imágenes.

**---------Ejercicio SSH**

Para conectar con ssh simplemente he configurado ambas tarjetas de red en primer lugar, luego he usado el comando en una de las máquinas:
$> ssh 192.168.1.100
Y he tenido que introducir la contraseña de la máquina a la que me conecto.

**---------Ejercicio curl**

Para esto creo en la máquina 1 un archivo llamado swap.html en la carpeta var/www/html
En la máquina 2 uso el comando: 
$> curl http://192.168.1.100/swap.html
Con esto me muestra el contenido de swap.html de la máquina 2.
