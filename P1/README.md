# Practica 1
## Presentación de las prácticas y preparación de las herramientas
#### Instalación y configuración de las máquinas virtuales

En primer lugar, como software de virtualización utilizaré VirtualBox , en concreto, la versión 6.1.4 en Windows. Nos creamos dos máquinas
virtuales de nombre 'M1' y 'M2' con 512 MB de RAM y 10 GB de disco duro dinámico e instalaremos Ubuntu Server. En la instalación le hemos indicado la opcion
LAMP por lo que tenemos instalado Apache+PHP+MySQL.

Cuando se haya terminado la instalación de las dos máquinas (M2 será clonada de M1), configuraremos los adaptadores de red. El adaptador 1 
de tipo NAT y el adaptador 2 de solo anfitrión. 

![2](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/2.JPG)

Para que la comunicación entre los propios servidores y entre el host se produzca correctamente, debemos añadir las IPs estáticas correspondientes mediante la interfaz de sincronización enp0s8 ya que por defecto no viene definida. Para realizar esta tarea tendremos que editar el archivo 'etc/network/interfaces' mediante el comando `sudo nano interfaces` y añadiríamos:

![3](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/3.JPG)
![4](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/4.JPG)

Y activamos el enp0s8 con el comando ifup enp0s8. Por lo que la configuración de ambas máquinas quedaría tal que así:
![5](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/5.JPG)
![6](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/6.JPG)

Para la verificación del estado de las conexiones locales anteriormentes configuradas, utilizaremos la herramienta de diagnóstico `ping`.
`ping 192.168.56.200` (Desde M1)
![7](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/7.JPG)

Y `ping 192.168.56.100` (Desde M2)
![8](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/8.JPG)

Y comprobamos que efectivamente tienen conexión.

Para comprobar la versión del servidor utilizaremos los comando `apache2 -v` y para ver si está en ejecución `ps aux | grep apache`

![9](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/9.JPG)

#### Acceso por SSH y Curl
Para comprobar que la conexión por SSH funciona usaremos el comando `ssh ipmachine -l user` entre las dos máquinas virtuales. Primero probaremos la conexión desde M1 a M2: 

![10](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/10.JPG)

Y ahora de la máquina M2 a la M1:

![11](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/11.JPG)

Ahora usaremos la herramienta `curl`para acceder a un archivo html de una máquina a otra. Creamos el `ejemplo.html` que tendrá un código sencillo:

```
<HTML>
<BODY>
Web de ejemplo de “tu_usuario_git” para SWAP
</BODY>
</HTML>
```

Y comprobamos que podemos acceder a él desde la máquina 1 a la 2:

![12](https://github.com/sergiocantero8/SWAP/blob/master/P1/Capturas/12.JPG)
