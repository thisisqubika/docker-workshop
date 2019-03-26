# Contenedores cerrados

Los procesos que corren dentro de un mismo contenedor pueden comunicarse entre ellos mediante la interfaz loopback (localhost). Pero en los contenedores cerrados no hay comunicación ni saliente ni entrante al contenedor; es decir el contenedor no se puede comunicar ni con internet ni con otros contenedores.

## --network none

Para crear un contenedor en una red cerrada utilizamos el argumento `--network none` cuando lo creamos:

```
docker run --rm --network none -it alpine:latest /bin/sh
```

Este ejemplo abre un shell, pero podríamos asignarle comandos o tareas ya automatizadas en la imagen que levantamos.  

Son interesantes para:

- `--volumes-from`
- Procesamiento batch de datos locales `--volumes`

---

## Referencias:

- [Disable networking for a container](https://docs.docker.com/network/none/)