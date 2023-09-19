# PRACTICA COMANDOS BASICOS DOCKER

En esta rpactica vamso a explicar los siguientes puntos.

BOLETIN DOCKER
1. Descarga la imagen 'ubuntu y comprueba que está en tu equipo
2. Crea un contenedor sin ponerle nombre. ¿está arrancado? Obtén el nombre
3. Crea un contenedor con el nombre 'dam_ubu1'. ¿Como puedes acceder a él?
o Ayuda
4. Comprueba que ip tiene y si puedes hacer un ping a google.com
5. Crea un contenedor con el nombre 'dam_ubu2'. ¿Puedes hacer ping entre los
contenedores?
6. Sal del terminal, ¿que ocurrió con el contenedor?
7. ¿Cuanta memoria en el disco duro ocupaste?
8. ¿Cuanta RAM ocupan los contenedores? ¿Hay algún comando docker para saber
esto?.




Para Descargar la imagen de Ubuntu debemos de indicar que vamos a usar Ubuntu en el siguiente comando:
sudo docker run -it ubuntu bash



Crea un contenedor sin ponerle nombre. ¿está arrancado? Obtén el nombre
Ahora desde otra Ventana del terminal, comprobaremos el nombre de Docker con el comando
**Docker ps**



3. Crea un contenedor con el nombre 'dam_ubu1'. ¿Como puedes acceder a él?
Ahora debemos crear un contenedor con el nombre ‘dam_ubu1’ y como queremos que tenga Ubuntu dentro, indicamos esto mismo en el comando
**docker run --name dam_ubu1 -it ubuntu**



Pero ojo en este caso no queremos acceder a el directamente, asiq lo vamos a crear en background, esto se hace añadiendo **-d** al principio del comando, **-i** idnica que se puede interactuar, y **-t** que esta interacción sea mediante terminal, estos dos se pueden abreviar con -it

**Dato!!** Para borrar un contenedor se debe hacer sudo docker rm nombre_contenedor Bien, ahora queremos acceder a este contenedor que hemos creado con
-d, para ello debemos usar el comando **Docker exec -it dam_ubu1**



 Comprueba que ip tiene y si puedes hacer un ping a google.com
No podemos hacerle ping a google.com puesto que no tenemos las net_tools instaladas
bash: ping: command not found
Asique las instalamos con apt update, apt intsall net-tools **El comando ping se instala con el paquete iputils-ping**

    root@204c5374e5d2:/# ping google.com
    PING google.com (142.250.178.174) 56(84) bytes of data. 64 bytes from mad41s08-in-f14.1e100.net (142.250.178.174): icmp_seq=1 ttl=62 time=110 ms
    64 bytes from mad41s08-in-f14.1e100.net (142.250.178.174): icmp_seq=2 ttl=62 time=26.0 ms
    64 bytes from mad41s08-in-f14.1e100.net (142.250.178.174): icmp_seq=3 ttl=62 time=91.7 ms
    
    64 bytes from mad41s08-in-f14.1e100.net (142.250.178.174): icmp_seq=5 ttl=62 time=555 ms
    ^C
    --- google.com ping statistics ---
    6 packets transmitted, 5 received, 16.6667% packet loss, time 5019ms rtt min/avg/max/mdev = 25.997/272.421/578.836/242.387 ms

Para comprobar la ip de nuestro contenedor Podemos hacer ya con las net-tools que instalamos anteriormente el comando **ifconfig**



Vamos a continuar con **Visual Studio**, para hacerlo de una manera más visual, ya que con click derecho podemos hacer atach Shell y ya entramos en el bash de este terminal.
Creamos un nuevo Docker llamado **dam_ubu2**



Instalamos **iputils-ping** para intentar hacer ping entre contenedores también instalaremos las ntet-tools para saber las 2 ips y así hacer ping



**EURECA!! Funciona**

Sal del terminal, ¿que ocurrió con el contenedor?
Bien ahora salgamos del contenedor; Al hacer esto puede parecer que se borra, y si no tiene nombre no vamos a poder entrar tan fácil, pero desde la terminal podemos hacer el comando **Docker ps -a** Esto nos muestra todos los contenedores, no solo los que están abiertos y estemos usando, si no todos aquellos de los cuales hemos salido anteriormente, con su respectivo nombre, que se lo podemos haber dado nosotros o se selecciona aleatoriamente


¿Cuanta memoria en el disco duro ocupaste?
Con el comando **docker system df** nos muestra que espacio esta usando en nuestro equipo

    En este caso por ejemplo los contenedores estan usando **127M**


¿Cuanta **RAM** ocupan los contenedores? ¿Hay algún comando docker para saber esto?.
Si existe un comando: **docker stats**, Este te indicará el porcentaje de **ram** que están usando los contenedores Abiertos :
En este caso

dam_ubu2
dam_ubu1
CPU %
0.00%
0.00%
MEM USAGE / LIMIT
**42.23MiB**
**/ 7.667GiB**

a