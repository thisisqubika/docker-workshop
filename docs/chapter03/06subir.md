# Registry

Registry es una aplicación servidor presenta un repositorio de imágenes. Se distribuye en el contenedor [registry](https://hub.docker.com/_/registry).

Cuando se desea disponer de una imagen compartida se utiliza Registry de donde los destinos de ejecución (usuarios, nodos del cluster, etc.) puedan obtenerla.

## Configurar Registry

Por defecto Docker utiliza `docker.io` como Registry público. Para utilizar otro existen diferentes mecanismos:

### PULL de registry propio

Para hacer pull de un sever propio:

```
docker pull localhost:5000/registry-demo
```

Si los repositorios son privados:

```
docker login https://<YOUR-DOMAIN>:8080

docker pull <YOUR-DOMAIN>:8080/test-image
```

Si la configuración se desea permanente:

- Variable de ambiente `DOCKER_OPTS`

```
DOCKER_OPTS="--insecure-registry <YOUR-DOMAIN>:8080"
```

- Archivo `/etc/default/docker`

## PUSH 

Para compartir imágenes en [Docker Hub](https://hub.docker.com) se debe poseer una cuenta y primeramente estar logrado:

```
$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: pilasguru
Password:
Login Succeeded
```

Una vez ingresado, la imágenes debe tener un nombre (tag) formado por `usuario/nombre-imagen`, en mi caso:

```
docker tag localtest:latest  pilasguru/test
```

Recién con este nombre y el comando `push` se podrá subir la imagen a Docker Hub, que tomará el nombre de usuario de la primera parte del nombre de la imagen:

```
$ docker push pilasguru/test
The push refers to repository [docker.io/pilasguru/test]
cd7100a72410: Preparing
latest: digest: sha256:8c03bb07a531c53ad7d0f6e7041b64d81f99c6e493cb39abba56d956b40eacbc size: 528
```


### PUSH a registry propio

Se nombra (_tag_) la imagen con el nombre DNS del repositorio:

```
docker tag <imagen> <REGISTRYHOST>/<USERNAME>/<NAME>[:TAG]

docker push <REGISTRYHOST>/<USERNAME>/<NAME>[:TAG] 
```

En caso de tener un Registry en el puerto no estándar, se debe definir el registry en `DOCKER_OPTS` como se explica en la sección anterior.

---

## Referencias:

- [Docker Registry](https://docs.docker.com/registry/)
- [docker push](https://docs.docker.com/engine/reference/commandline/push/)
- [Pull and push images](https://docs.docker.com/datacenter/dtr/2.2/guides/user/manage-images/pull-and-push-images/)
