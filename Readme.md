Para escribir tu documento README con los títulos en color azul y representar la última pregunta con su respuesta en una tabla utilizando Mermaid, puedes usar el siguiente código Markdown:


# <font color="skyblue">PRACTICA COMANDOS BASICOS DOCKER</font>

En esta rpactica vamso a explicar los siguientes puntos.

<font color="skyblue">BOLETIN DOCKER</font>
1. Descarga la imagen 'ubuntu y comprueba que está en tu equipo
2. Crea un contenedor sin ponerle nombre. ¿está arrancado? Obtén el nombre
3. Crea un contenedor con el nombre 'dam_ubu1'. ¿Como puedes acceder a él?
   o Ayuda
4. Comprueba que ip tiene y si puedes hacer un ping a google.com
5. Crea un contenedor con el nombre 'dam_ubu2'. ¿Puedes hacer ping entre los contenedores?
6. Sal del terminal, ¿qué ocurrió con el contenedor?
7. ¿Cuanta memoria en el disco duro ocupaste?
8. ¿Cuanta RAM ocupan los contenedores? ¿Hay algún comando docker para saber esto?.

<font color="skyblue">Descarga la imagen 'ubuntu y comprueba que está en tu equipo</font>
---
Para descargar la imagen de Ubuntu, debemos indicar que vamos a usar Ubuntu en el siguiente comando:
```bash
sudo docker run -it ubuntu bash
```

<font color="skyblue">Crea un contenedor sin ponerle nombre. ¿está arrancado? Obtén el nombre</font>
---
Ahora, desde otra ventana del terminal, comprobaremos el nombre de Docker con el comando `docker ps`.

<font color="skyblue">Crea un contenedor con el nombre 'dam_ubu1'. ¿Como puedes acceder a él?</font>
---
Ahora debemos crear un contenedor con el nombre 'dam_ubu1' y como queremos que tenga Ubuntu dentro, indicamos esto mismo en el comando:
```bash
docker run --name dam_ubu1 -it ubuntu
```
Pero ojo en este caso no queremos acceder a él directamente, así que lo vamos a crear en background, esto se hace añadiendo `-d` al principio del comando, `-i` indica que se puede interactuar, y `-t` que esta interacción sea mediante terminal, estos dos se pueden abreviar con `-it`.
**Dato!!** Para borrar un contenedor se debe hacer `sudo docker rm nombre_contenedor`. Bien, ahora queremos acceder a este contenedor que hemos creado con -d, para ello debemos usar el comando `docker exec -it dam_ubu1`.

<font color="skyblue">Comprueba que IP tiene y si puedes hacer un ping a google.com</font>
---
No podemos hacerle ping a google.com puesto que no tenemos las net_tools instaladas:
```bash
bash: ping: command not found
```
Así que las instalamos con `apt update` y `apt install net-tools`. **El comando ping se instala con el paquete iputils-ping**.

```bash
root@204c5374e5d2:/# ping google.com
PING google.com (142.250.178.174) 56(84) bytes of data. 64 bytes from mad41s08-in-f14.1e100.net (142.250.178.174): icmp_seq=1 ttl=62 time=110 ms
64 bytes from mad41s08-in-f14.1e100.net (142.250.178.174): icmp_seq=2 ttl=62 time=26.0 ms
64 bytes from mad41s08-in-f14.1e100.net (142.250.178.174): icmp_seq=3 ttl=62 time=91.7 ms
64 bytes from mad41s08-in-f14.1e100.net (142.250.178.174): icmp_seq=5 ttl=62 time=555 ms
^C
--- google.com ping statistics ---
6 packets transmitted, 5 received, 16.6667% packet loss, time 5019ms
rtt min/avg/max/mdev = 25.997/272.421/578.836/242.387 ms
```

Para comprobar la IP de nuestro contenedor, podemos usar el comando `ifconfig`.

<font color="skyblue">Vamos a continuar con Visual Studio, para hacerlo de una manera más visual, ya que con click derecho podemos hacer attach Shell y ya entramos en el bash de este terminal.</font>

Creamos un nuevo Docker llamado 'dam_ubu2'.

Instalamos 'iputils-ping' para intentar hacer ping entre contenedores. También instalaremos las 'net-tools' para saber las 2 IPs y así hacer ping.

**EURECA!! Funciona**

<font color="skyblue">Sal del terminal, ¿qué ocurrió con el contenedor?</font>
---
Bien, ahora salgamos del contenedor. Al hacer esto puede parecer que se borra, y si no tiene nombre no vamos a poder entrar tan fácil. Pero desde la terminal podemos hacer el comando `docker ps -a`. Esto nos muestra todos los contenedores, no solo los que están abiertos y estemos usando, sino todos aquellos de los cuales hemos salido anteriormente, con su respectivo nombre, que se lo podemos haber dado nosotros o se selecciona aleatoriamente.

<font color="skyblue">¿Cuánta memoria en el disco duro ocupaste?</font>
---
Con el comando `docker system df` nos muestra qué espacio está usando en nuestro equipo.

En este caso, por ejemplo, los contenedores están usando **127M**.

<font color="skyblue">¿Cuánta RAM ocupan los contenedores? ¿Hay algún comando docker para saber esto?</font>
---
Sí, existe un comando: `docker stats`. Este te indicará el porcentaje de **RAM** que están usando los contenedores abiertos:

| CONTAINER | CPU % | MEM USAGE / LIMIT |
| --------- | ----- | ----------------- |
| dam_ubu2  | 0.00% | 42.23MiB / 7.667GiB |
| dam_ubu1  | 0.00% | 42.23MiB / 7.667GiB |
```

