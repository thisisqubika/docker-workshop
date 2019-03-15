# Docker como servicio

Poner a correr una imagen docker cuyo proceso es un servicio supone __dejar corriendo__ algo en forma permanente para utilizar el servicio.

Al poner algo a correr en forma permanente debemos, además de saber cómo ejecutarlo, saber si está funcionando, utilizar el servicio y cómo apagarlo, así que este paso involucra algunos conceptos más del uso de docker.

## Simple-webserver

La imagen [andygrunwald/simple-webserver](https://hub.docker.com/r/andygrunwald/simple-webserver) es un webserver simple escrito en Go.

### RUN

```
$ docker run -d -p 8082:8082 andygrunwald/simple-webserver
```

donde:

- `-d` pondrá a correr el docker en //background//
- `-p 8082:8082` abrirá el puerto 8082 en el equipo local conectará con el puerto 8082 del contenedor.

y descargará la imagen y nos devolverá el _prompt_, pero ha dejado corriendo el docker.

### LS

Podemos interrogar con docker si el contenedor está corriendo:

```
$ docker container ls
CONTAINER ID        IMAGE                           COMMAND             CREATED              STATUS              PORTS                    NAMES
8d5297a02f2c        andygrunwald/simple-webserver   "app"               About a minute ago   Up About a minute   0.0.0.0:8082->8082/tcp   stupefied_bohr
```

`docker container ls` es equivalente a `docker ps`

### Utilizar el servicio

El servicio es un servidor web simple que lo podemos ver con el navegador conectando al puerto local, que configuramos con `-p`, mediante el comando [curl](https://curl.haxx.se/):

```
$ curl http://localhost:8082/version
simple webserver v1.0.0
```

### STOP - KILL

Como al contenedor lo creamos sin nombre, nos referimos a él por el _Container ID_ y lo apagamos con *STOP*:

```
$ docker container stop 01a420094251
$ docker container ls
CONTAINER ID        IMAGE               COMMAND
$
```

`docker stop` envía las señales `SIGTERM` y luego `SYGKILL` a los procesos del contenedor

El comando `docker container kill <container-id>` envía por defecto la señal `SIGKILL` y soporta otras señales.

### START

```
$ docker container start 01a420094251
```

### EXEC

Es posible acceder a un contenedor, para modificar contenido, revisar logs, verificar distintas configuraciones, obteniendo shell:

```
docker container exec -it stupefied_bohr sh
```

donde:

- `-i` entrará en modo interactivo
- `-t` asignara una consola `tty` al proceso ejecutado (sh)

## Servidor SSH

La imagen [tutum/debian](https://hub.docker.com/r/tutum/debian) levanta en un contenedor un servicio OpenSSH.

### RUN

```
$ docker run -d -p 2222:22 tutum/debian
```

## EXEC 

Consultar la configuración que quedó levantada para el acceso ssh:

```
$ docker container logs 3a49c40eee76
=> Setting a random password to the root user
=> Done!
========================================================================
You can now connect to this Debian container via SSH using:

    ssh -p <port> root@<host>
and enter the root password 'vVuzz8JcvafD' when prompted

Please remember to change the above password as soon as possible!
========================================================================
```

### Utilizar servicio

```
$ ssh -p 2222 root@127.0.0.1
```

### STOP -> RM

`docker container rm` permite borrar los contenedores *apagados* (_stop_) únicamente.

```
$ docker container rm 
Error response from daemon: You cannot remove a running container 3a49c40eee762a5887ba2d11dd801c98a7b8c22031ca049f1022f2f2ab9ca745. Stop the container before attempting removal or force remove

$ docker container stop 3a49c40eee76
3a49c40eee76
$ docker container rm 3a49c40eee76
3a49c40eee76
```
 

## Ejercicios

### 1.

Borrar todos los container apagados utilizando los comandos:

```
docker container ps -a
docker container rm <CONTAINER-ID> 
```

### 2.

Volver a ejecutar el container (_Simple-webserver_)como se muestra a principio esta sección verificando que esté activo y tratar de borrarlo con los comandos, verificando las diferencias entre ellos:

```
docker container rm <CONTAINER-ID>
docker container rm -f <CONTAINER-ID> 
```

### 3.

Volver a ejecutar el container (_Simple-webserver_) pero esta vez **sin** el parámetro `-d` dejando el servicio en primer plano.

Desde otra consola hacer conexiones con `curl http://localhost:8082`

Salir con `Ctrl-C` y verificar qué sucede con el contenedor utilizando el comando `docker container ls`

---

## Referencias:  

- [docker container](https://docs.docker.com/v17.09/engine/reference/commandline/container/)
- [docker run](https://docs.docker.com/v17.09/engine/reference/commandline/run/)

