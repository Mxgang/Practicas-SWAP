**Práctica 2. Clonar la información de un sitio web**

**1. Probar el funcionamiento de la copia de archivos por ssh**

Para esto usaremos el comando tar de una manera muy sencilla:

$>tar czf - hola.txt | ssh 192.168.1.101 'cat > ~/tar.tgz'

Básicamente he comprimido el archivo "hola.txt" que tenía y lo he mandado a la máquina de IP 192.168.1.101 mediante ssh teniendo que introducir la contraseña, el archivo comprimido se envía al directorio raiz.


**2. Clonado de una carpeta entre las dos máquinas**

En primer lugar he creado una carpeta llamada "prueba" cuyo contenido es "práctica2.txt" en la máquina 1.
En la máquina 2 he creado la carpeta prueba y he puesto el comando:
$> rsync -avz -e ssh 192.168.1.100:/home/hulidex/prueba/ /home/hulidex/prueba/

Con eso en la carpeta prueba de la máquina 2 ha recibido el contenido que había en la máquina 1, que es el archivo "práctica2.txt"

**3. Configuración de ssh para acceder sin que solicite contraseña**

La máquina esclava que uso es la máquina2 cuya ip es 192.168.1.101
En primer lugar genero las claves con el comando:
$> ssh-keygen -b 4096 -t rsa

Luego doy permisos a authorized_keys de la máquina1 para poder copiar la clave:
$> chmod 600 ~/.ssh/authorized_keys

Copio la clave de la máquina2 a la máquina1 introduciendo esto en la máquina2:
$> ssh-copy-id 192.168.1.100

Haciendo ssh hacia la máquina1 se puede ver que podemos meternos sin contraseña

