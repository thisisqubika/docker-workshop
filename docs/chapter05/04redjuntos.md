# Contenedores juntos (linked)
 
En una red de contenedores juntos, multiple contenedores comparten la misma interfaz de red *loopback*, de esta forma, cualquiera que levante un servicio en `127.0.0.1` será visto por el otro en su respectivo `localhost`. De esta forma se pueden crear containers aislados de internet pero vinculados por red entre ellos redes.

Para crear un contenedor unido a otro utilizamos el argumento `--network container:nombre`, como este ejemplo:

Creamos un primer contenedor en una cerrado:

```
$ docker run --rm --name 1cerrado --network none -it alpine /bin/sh
```

Creamos un segundo contenedor pegándolo al creado en el paso anterior:

```
$ docker run --rm --network container:1cerrado -it alpine /bin/sh
```

---

## Referencias:

- [Network containers](https://docs.docker.com/engine/tutorials/networkingcontainers/)