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

**2. Configurar una máquina e instalar el haproxy como balanceador de carga**

Se instala haproxy con el comando "apt-get install haproxy" En su archivo de configuración situado en /etc/haproxy/ hay que poner el contenido que había en el guión junto con las ip de los servidores.
Una vez hecho, antes de lanzar el servicio, com probamos que no hay otro servicio usando el puerto 80, una vez comprobado, lanzamos el servicio con "systemctl start haproxy".

Con la máquina del cliente hacemos curl al balanceador para ver que funciona, tal y como muestra la siguiente imagen

![img](https://i.imgur.com/coj7bVf.png)

**Opcional. Configurar una máquina e instalar Pound como balanceador de carga**
Para probar otro balanceador decidí instalar Pound con el comando "apt-get install Pound".
La configuración fue simple, fui al archivo de configuración situado en /etc/Pound y puse los puertos e ips al igual que en los balanceadores anteriores. En la siguiente imagen se muestra el archivo ya configurado:

![img](https://i.imgur.com/6b8vfT7.png)

Inicio el proceso con "systemctl start pound" (comprobando previamente que el puero 80 esté libre) y hago curl en la máquina cliente:

![img](https://i.imgur.com/xlTzM75.png)

**3. Someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y después haproxy.**

Aquí comparo los 3 balanceadores de carga usando el Benchmark de Apache que ya tenía instalado en la máquina de cliente.
Voy ejecutando el comando "ab -n 1000 -c 10 http://192.168.1.102/index.html" con cada servicio (Nginx, haproxy y Pound) y me salen 3 tiempos distintos, en las siguientes capturas se podrá distinguir el Benchmark de cada servicio

- Nginx
  ![img](https://i.imgur.com/4yaylIw.png)
  
- haproxy
 ![img](https://i.imgur.com/F3aEQHu.png)
 
- Pound
  ![img](https://imgur.com/552k6yG.png)
