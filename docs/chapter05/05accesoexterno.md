# Acceso externo

Los contenedores presentados en el mismo _bridge_ exponen entre ellos todos los puertos que tienen abiertos, pero ninguno de esos puertos son accesibles desde fuera de la red del _bridge_.

Es posible presentar en un puerto del host que corresponde a un puerto en particular del contenedor (DNAT), cuando se utiliza red `bridge`.

## --publish | -p

Para publicar un puerto del host (LISTEN) que tiene una configuración que mapa un puerto del contenedor (DNAT) se hace al levantar el contenedor:

```
docker run --rm -it --publish 8080:80 -d nginx:latest

curl localhost:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
``` 

La opción `EXPOSE` de las imágenes permite conocer qué puertos tendrán un servicio escuchando cuando el contenedor esté corriendo.

# Uso nombre

Por defecto los contenedores en *redes creadas por el usuario* mapean en el DNS todos por nombre entre ellos.

```
docker run --rm -it --network mired --name testA alpine sh

docker run --rm -it --network mired --name testB alpine sh
# ping testA
PING testA (172.18.0.2): 56 data bytes
64 bytes from 172.18.0.2: seq=0 ttl=64 time=0.099 ms
64 bytes from 172.18.0.2: seq=1 ttl=64 time=0.094 ms
```

En el bridge por defecto (docker0) es necesario usar la opción  `--link` para que se vinculen los nombres entre los contenedores y genera entradas en el archivo `/etc/hosts` para resolver los container por nombre entre ellos. 

> --link se utiliza solamente para el default bridge (docker0)

> --link es una opción caduca y será retirada en versión futura


---

## Referencias:

- [Use bridge networks](https://docs.docker.com/network/bridge/)