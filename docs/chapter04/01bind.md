# Filesystem del host (bind mount)

Bind mount permite usar una carpeta (o archivo) del host que es presentada en el espacio de filesystem del contenedor mediante la técnica de montado bind (`mount -o bind`) de Linux.

_Bind mount_ es la forma dar permanencia a los datos de disco del contenedor.

El _bind mount_ se especifica en el momento de lanzar el contenedor y permite realizar los procesos de respaldo, migración, etc. con herramientas fuera de docker.

Existen dos tipos de montado bind disponible para contenedores:

## --volume | -v

Permite apuntar _una ruta_ de carpeta o de archivo del host y presentarlo dentro del contenedor en un punto de montado.  

`-v path-host:path-container`

Y se configura al lanzar el contenedor:

```
docker container run --name web-nginx -v /opt/website:/usr/share/nginx/html:ro -d nginx
```

Esto hará que la carpeta del host `/opt/website` quede presentada como la carpeta `/usr/share/nginx/html` en el contenedor.

El atributo `:ro` hará que para el contenedor sea un espacio de solo lectura.

Otro contenedor puede ser lanzado con la misma opción de montado (`-v`) para reutilizar los datos generados por el primer contenedor.

---

## Ejercicios:

### 1.

De alguna aplicación que esté desarrollando, ejecutar la imagen docker del servicio que necesita tener levantado, montando el directorio de su aplicación desde el host.

Ejemplos:

```
docker run -it --rm -v $PWD/src:/usr/local/app --workdir /usr/local/app ruby:latest bash

# bundle install 
```

---

## Referencias:

- [Use bind mounts](https://docs.docker.com/storage/bind-mounts/)