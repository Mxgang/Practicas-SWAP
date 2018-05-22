**Práctica 5. Replicación de bases de datos MySQL**

**1.Crear una BD con al menos una tabla y algunos datos.**

En esta primer parte hacemos una base de datos en la máquina maestra e insertamos una tabla con datos con los siguientes comandos:

mysql -uroot -p
Enter password: <TECLEAR LA CLAVE SI NO ES VACÍA>
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 1
Server version: 5.1.44 Source distribution
Type 'help;' or '\h' for help. Type '\c' to clear the current
input statement.
mysql> create database contactos;
Query OK, 1 row affected (0,00 sec)
mysql> use contactos;
Database changed
mysql> show tables;
Empty set (0,00 sec)
mysql> create table datos(nombre varchar(100),tlf int);
Query OK, 0 rows affected (0,01 sec)
mysql> show tables;
+---------------------+
| Tables_in_contactos |
+---------------------+
| datos
|
+---------------------+
1 row in set (0,00 sec)
mysql> insert into datos(nombre,tlf) values ("pepe",95834987);
Query OK, 1 row affected (0,00 sec)
mysql> select * from datos;
+---------+-----------+
| nombre | tlf
|
+---------+-----------+
| pepe
| 95834987 |
+---------+-----------+
3 rows in set (0,00 sec)

**2. Realizar la copia de seguridad de la BD completa usando mysqldump en la
máquina principal y copiar el archivo de copia de seguridad a la máquina
secundaria.**

Creamos el archivo de seguridad con el comando "mysqldump ejemplodb -u root -p > /tmp/ejemplodb.sql" en la máquina maestra.


**3. Restaurar dicha copia de seguridad en la segunda máquina (clonado manual
de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica.**

En la máquina esclava ponemos lo siguiente: "scp maquina1:/tmp/ejemplodb.sql /tmp/". Luego creamos la base de datos con el mismo nombre que la de la maestra y restauramos los datos del archivo de la BD con el comando "sql -u root -p ejemplodb < /tmp/ejemplodb.sql". Como podemos ver, la BD es idéntica a la maestra
![img](https://i.imgur.com/MldTncK.png)

**4. Realizar la configuración maestro-esclavo de los servidores MySQL para que la
replicación de datos se realice automáticamente.**

Una vez configurados los archivos que vienen en el guión, creamos el usuario esclavo en el maestro con los comandos que vienen en el guión, tal y como muestra la siguiente imagen:

![img](https://i.imgur.com/ecHeWzj.png)

Vamos a la máquina esclava y la configuramos para que pueda ver a su maestro:

![img](https://i.imgur.com/hybt4xb.png)

Iniciamos el esclavo con "START SLAVE;" y luego hacemos "SHOW SLAVE STATUS\G" y comprobamos que el valor "Seconds_behind_master" es distinto a null.

![img](https://i.imgur.com/77XYeuB.png)

Por último, en la máquina maestra insertamos datos en nuestra base de datos y en la esclava comprobamos que se actualiza correctamente:
![img](https://i.imgur.com/4jg8QFd.png)



