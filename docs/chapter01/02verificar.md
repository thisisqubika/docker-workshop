# Verificación de la instalación

_No es un objetivo de esta guía abordar la instalación de docker_. Si bien la instalación es un proceso sencillo, los requisitos y opciones de configuración varían según dónde se va a utilizar docker.

Docker es nativo de sistemas operativos Linux y los procesos de instalación difieren de acuerdo a la [distribución y versión de Linux](https://docs.docker.com/engine/installation/linux/ubuntulinux/) que se use.  Pero en la actualidad, docker se puede instalar en otros sistemas operativos como [macOS](https://docs.docker.com/engine/installation/mac/) y [Windows](https://docs.docker.com/engine/installation/windows/).

## Verificación de la instalación

Primero es consultar la versión instalada de docker:

```
$ docker version
```

Muestra versión del _cliente_ y versión del _servidor_ (si está corriendo):

```
Client:
 Version:      18.03.1-ce
 API version:  1.37
 Go version:   go1.9.5
 Git commit:   9ee9f40
 Built:        Thu Apr 26 07:17:20 2018
 OS/Arch:      linux/amd64
 Experimental: false
 Orchestrator: swarm

Server:
 Engine:
  Version:      18.03.1-ce
  API version:  1.37 (minimum version 1.12)
  Go version:   go1.9.5
  Git commit:   9ee9f40
  Built:        Thu Apr 26 07:15:30 2018
  OS/Arch:      linux/amd64
  Experimental: false
```

Está corriendo el `daemon` Docker Engine (*Server*) que ejecuta (crea) y mantiene los contenedores. Además, dispone de un *cliente* que es el comando `docker` propiamente dicho.

Y seguidamente con el comando

```
$ docker system info
```

saber cómo está docker funcionando en nuestro sistema (los datos  mostrados pueden variar):

```
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 18.03.1-ce
Storage Driver: overlay2
 Backing Filesystem: extfs
 Supports d_type: true
 Native Overlay Diff: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host macvlan null overlay
 Log: awslogs fluentd gcplogs gelf journald json-file logentries splunk syslog
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: 773c489c9c1b21a6d78b5c538cd395416ec50f88
runc version: 4fc53a81fb7c994640722ac585fa9ca548971871
init version: 949e6fa
Security Options:
 apparmor
 seccomp
  Profile: default
Kernel Version: 4.4.0-127-generic
Operating System: Ubuntu 16.04.4 LTS
OSType: linux
Architecture: x86_64
CPUs: 1
Total Memory: 992.2MiB
Name: server
ID: ILHX:XLTM:6XDZ:FUYB:DY7I:ETMT:J4BQ:7XQ6:5MPY:TD6X:7M6L:NZE7
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
Labels:
Experimental: false
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false
```

Es posible ejecutar un primer contenedor para verificar los el funcionamiento *Docker Engine*:

* Registry
* Network
* CGroups
* System
* etc.

```
$ docker run --rm hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

$
```