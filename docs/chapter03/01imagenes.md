# Gestión de imágenes

## SEARCH

El _Registry_ de imágenes público Docker Hub se puede buscar mediante [web](https://hub.docker.com) o con el comando `search`:

```
docker search ubuntu | head
```

desplegará la totalidad de las imágenes que posean ubuntu en su nombre o descripción.

En Docker Hub existen dos tipos de imágenes:

- *imágenes oficiales*, que son mantenidas por Docker y reciben aportes de la comunidad. Están pensadas para repositorio de distribuciones, mejores prácticas, seguridad. Se identifican por su nombre sin barra: `ubuntu` y por tener el atributo OFFICIAL

```
docker search --filter is-official=true ubuntu
```

- *imágenes de usuarios*, son creadas, mantenidas y compartidas por usuarios. Se identifican por anteponer el nombre del usuario: `username/imagen`

```
docker search tutum
```

### tags

Podemos consultar por el `tag` de la imagen, directamente invocando al api del registry que nos devolverá un JSON que podemos filtrar con el comando `jq`:

```
curl -s -S 'https://registry.hub.docker.com/v2/repositories/library/ubuntu/tags/' | jq '."results"[]["name"]' |sort
```


## PULL

La forma de descargar una imagen para incorporarla al repositorio local es con el comando `pull`:

```
docker pull ubuntu:bionic
```

`run` además de ejecutar una imagen docker, también la descarga y la deja en el repositorio si no está descargada.

## TAG

El comando `tag` permite poner el nombre que queremos a una imagen en el formato `repositorio:etiqueta`

```
docker tag ubuntu:bionic pruebas:locales
```

Que generará una nueva entrada en el repositorio local con el nombre que deseamos:

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
pruebas             locales             452a96d81c30        5 weeks ago         79.6MB
ubuntu              bionic              452a96d81c30        5 weeks ago         79.6MB
```

En el repositorio local podemos hacer búsqueda de imágenes con diferentes filtros:

```
docker images ubuntu:*
```

Y el comando `docker images` posee la opción `--filter` que permite buscar imágenes por distintas características

```
-f, --filter valor    Filtrado de la salida basado en condiciones
                        - dangling=(true|false)
                        - label=<key> o label=<key>=<value>
                        - before=(<image-name>[:tag]|<image-id>|<image@digest>)
                        - since=(<image-name>[:tag]|<image-id>|<image@digest>)
                        - reference=(pattern of an image reference)
```

Buscar imágenes que no están asociadas (_unused_) a un contenedor ejecutándose:

```
docker images --filter "running=false"
```

Buscar imágenes que no están asociadas a una nueva imagen (nueva capa):

```
docker images --filter "dangling=true" 
```

### INSPECT

Permite obtener información detallada de una imagen que se encuentra descargada.

Conocer el CMD que corre al arrancar:

```
$ docker image inspect hello-world
           "Cmd": [
                "/hello"
            ],
```

Ver los puertos que están EXPOSE:

```
$ docker image inspect andygrunwald/simple-webserver:latest
            "ExposedPorts": {
                "8082/tcp": {}
            },
```

## RMI

Para borrar imágenes del repositorio local se utiliza el comando  `rmi`:

```
docker images rmi pruebas:locales
```

Para borrar todas las imágenes que no están en uso actualmente (_unused_ y _dangling_): 

```
docker images prune
``` 

---

## Ejercicios

### 1.
Descargar la imagen de ubuntu correspondiente a `xenial`

---

## Referencias:

- [Docker Hub](https://hub.docker.com)
- [Official images on Docker Hub](https://docs.docker.com/docker-hub/official_images/)
- [docker image inspect](https://docs.docker.com/engine/reference/commandline/image_inspect/)
- [docker image filtering](https://github.com/moby/moby/blob/10c0af083544460a2ddc2218f37dc24a077f7d90/docs/reference/commandline/images.md#filtering)
- Imagen [ubuntu](https://hub.docker.com/_/ubuntu)