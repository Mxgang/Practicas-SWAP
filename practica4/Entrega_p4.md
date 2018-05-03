**Práctica 4. Asegurar la granja web**

**1. Crear e instalar en la máquina 1 un certificado SSL autofirmado para configurar
el acceso HTTPS a los servidores. Una vez configurada la máquina 1, se debe
copiar al resto de máquinas servidoras y al balanceador de carga. Se debe
configurar nginx adecuadamente para aceptar y balancear correctamente tanto
el tráfico HTTP como el HTTPS.**

En primer lugar instalo el certificado SSL en la máquina servidora 1 mediante las instrucciones que vienen en el guión, una vez que está instalado se hace un "curl -k https://ipmáquina" para comprobar que funciona.

Luego hacemos un rsync para copiar los certificados a la otra máquina servidora y al balanceador, se hace con el comando: rsync -avz -e ssh ipmaquina1:/etc/apache2/ssl /etc/apache2/

A continuación, en la máquina balanceadora nos dirigimos al archivo de configuración de Nginx situado en /etc/nginx/conf.d/default.conf y añadimos las líneas oportunas para que funcione con SSL, dicha configuración está en la siguiente captura de pantalla:

![img](https://i.imgur.com/ICI28Pk.png)

Una vez hecho esto activamos el puerto 443 con "ufw allow 443" en todas las máquinas. Vamos a la máquina de cliente y hacemos el curl al balanceador para comprobar que funciona

![img](https://i.imgur.com/bMYGXA7.png)
