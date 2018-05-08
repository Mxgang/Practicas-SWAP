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

**2. Configurar las reglas del cortafuegos con IPTABLES para asegurar el acceso a
uno de los servidores web, permitiendo el acceso por los puertos de HTTP y
HTTPS a dicho servidor. Esta configuración se hará en una de las máquinas
servidoras finales (p.ej. en la máquina 1), y se debe poner en un script con las
reglas del cortafuegos que se ejecute en el arranque del sistema (según la
versión de Linux, se llevará a cabo de una forma u otra).**

En mi caso el firewall lo he hecho en la máquina servidora 1, con IP 192.168.1.100. El script se llama "conf-firewall.sh" y está ubicado en /etc/init.d con los demás scripts que se inician en el arranque del sistema, pero por alguna razón no funciona así que he optado por añadir una línea en crontab: "@reboot root /etc/init.d/conf-firewall.sh".

La configuración del script es la siguiente:
![img](https://i.imgur.com/1k0NI7F.png)

Deniego todos los accesos salvo el puerto ssh, 80 y 443.

Con el comando "iptables -L -n -v" compruebo la configuración:

![img](https://i.imgur.com/yXXBfEA.png)

Ahora para comprobar que está bien puedo hacer un curl desde el cliente al firewall, que debería funcionar bien. Si comento por ejemplo la línea donde permito el puerto 80 e intento hacer el curl de nuevo, no funcionaría ya que le he denegado el acceso.
