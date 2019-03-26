# Filesystem del host (volume)

Los volúmenes es un recurso administrado por docker y que pueden ser vistos como un disco guardado en el host (pseduo-volumen) para montar en los contenedores.

## Volúmen 

Puede ser utilizado por otros contenedores simplemente indicando el nombre del volúmen.

La creación de un _volume_ se puede realizar de dos formas diferentes:

- al ejecutar `docker run`
- creando con nombre `docker volume create`

### CREATE

Con la opción `volume create` se puede crear un volumen con un nombre dado, para luego utilizar:

```
docker volume create MisDatos
```

### LS

Y puede ser visto en el listado de volúmenes disponibles:

```
$ docker volume ls
DRIVER              VOLUME NAME
local               MisDatos
```

### --volume | -v

Esta opción es semejante a _bind mount_ pues se usa con la opción `-v` pero se indica un nombre en lugar de un path del host. Si no existe, docker creará el volumen:

```
docker run -it --rm --name testA -v DataVol:/opt/app/data busybox sh
```

Hará que el volumen quede presentado dentro del contenedor en la carpeta `/opt/app/data`.

Podemos analizar su configuración:

```
$ docker volume inspect DataVol
[
    {
        "CreatedAt": "2018-06-04T21:31:46Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/DataVol/_data",
        "Name": "DataVol",
        "Options": null,
        "Scope": "local"
    }
]
```

Y dentro del contenedor lo podemos consultar con mount:

```
/dev/sda1 on /opt/app/data type ext4 (rw,relatime,data=ordered)
```

## Volúmenes anónimos

Se indica solamente _carpeta del contenedor_ debe ser guardada en el host _fuera_, en el host. Docker le asignará un ID de volumen y un espacio que permanecerá aunque el contenedor sea borrado.

```
docker container run -it -v /data ubuntu bash

root@df5e2fce65e7:/#
root@df5e2fce65e7:/# touch /data/file.txt
root@df5e2fce65e7:/# exit
```

Los datos (`file.txt`) permanecerán en un volumen con un ID de identificación:

```
docker volume ls
DRIVER              VOLUME NAME
local               0de61240ce255aa73af2c57873cc50b9134b49
```

Y pueden ser vueltos a montar en caso necesario:

```
docker run -it --rm -v 0de61240ce255aa73af2c57873cc50b9134b49:/data ubuntu ls /data
file.txt
```

Pero se puede observar que en caso de tener muchos contenedores en uso o apagados, la lista de volúmenes puede ser extensa.

## Re-utilizar un volumen creado

Al volver a correr (`run`) un contenedor con el mismo nombre de volumen volvemos a montarlo y a acceder a sus datos: 

```
docker run -it --rm --name testB -v DataVol:/data busybox sh
```

### --volumes-from

La opción `--volumes-from` permite utilizar todos los volúmenes que tenga otro contenedor corriendo y montarlos en los mismos puntos de montaje:

```
docker run --rm --volumes-from testB -v $PWD:/backup busybox sh -c 'cp /data/* /backup/'
```

## RM / PRUNE

Para borrar los volúmenes, puede hacerse:

- de a uno `docker volume rm 0de61240ce255aa73af2c57873cc50`
- todos `docker volume prune`
- al ejecutar con `--rm` para volúmenes anónimos

También es posible listar con un filtro y borrar solo esos volúmenes:

```
docker volume rm $(docker volume ls -q --filter dangling=true)
```

---

## Ejercicios:

### 1.

Usando volúmenes, correr la imagen `mysql:latest` o `mongo:latest` crear una base de datos y destruir el contenedor.

Volver a correr la misma imagen montando el volumen creado anteriormente y verificar que la base de datos se mantenga creada. 

---

## Referencias:

- [Use volumes](https://docs.docker.com/storage/volumes/)







