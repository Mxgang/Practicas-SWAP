**Práctica 3. Balanceo de carga**

**1. Configurar una máquina e instalar el nginx como balanceador de carga**

En primer lugar he clonado 2 máquinas nuevas a partir de uno de los servidores que ya tenía de las anteriores prácticas. Les he bajado a las 4 máquinas la memoria a 512mb para que mi ordenador pueda con todas a la vez.
En ambas les he cambiado la IP con lo que la distribución quedaría así:
- Servidor 1: 192.168.1.100
- Servidor 2: 192.168.1.101
- Balanceador de carga: 192.168.1.102
- Cliente: 192.168.1.103

En la máquina que actúa como balanceador de carga le he desactivado APache con el comando: systemctl stop apache2.
Luego lo he actualizado con: sudo apt-get update y acto seguido he instalado nginx con sudo apt-get install nginx.

Una vez instalado he creado el archivo default.conf con el contenido que nos dice el guión de prácticas. Para evitar problemas, en el archivo nginx.conf he comentado la última línea.
He modificado el contenido de index.html en el servidor 1 y en el servidor 2 y ya empiezo a ejecutar el nginx en el balanceador con: systemctl start nginx.

En la máquina del cliente he hecho un curl al balanceador: curl http://192.168.1.102 y me ha mostrado satisfactoriamente el contenido de index.html del servidor 1 y 2 como muestro en la siguiente imagen:

![img](https://i.imgur.com/LIdaK04.png)