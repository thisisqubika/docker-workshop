
# Filesystem temporal del host

Permite el asignar espacio de memoria del host como filesytem temporal del contenedor.

En este caso el filesystem es externo al contenedor y es efímero pues se eliminará inclusive _cuando el contenedor se detenga_. Y no se pueden compartir entre contenedores corriendo.

El objetivo de tmpfs mounts es guardar datos sensibles o temporales que no se persisten en la capa de escritura (chroot disponible desde el host).  

`Solamente disponibles en Linux` 

Por ejemplo:

```
docker run -it --name tmpA --tmpfs /app alpine sh
```

Dentro del contenedor queda presentado de esta forma:

```
tmpfs on /app type tmpfs (rw,nosuid,nodev,noexec,relatime)
```

```
docker inspect tmpA

    "Tmpfs": {
        "/app": ""
    },
```

---

## Referencias:

- [Use tmpfs mounts](https://docs.docker.com/storage/tmpfs/)