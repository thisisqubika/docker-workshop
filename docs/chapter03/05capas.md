# Capas de las imágenes

Las imágenes están formadas en capas. 

Cada repositorio archiva las capas una única vez, aunque pueda ser utilizada por distintas imágenes.  De la misma forma, a la hora de transferir una imagen, solo se copiarán las capas no disponibles en el repositorio destino.

## HISTORY

Permite consultar la historia de una determinada imagen.

```
docker image history alpine
```

Crear una imagen para consultar su _history_ con este ejemplo auto-explicativo:

**Dockerfile**
```
FROM alpine
RUN apk update && apk add nodejs
COPY . /app
WORKDIR /app
CMD ["node","index.js"]
```

Comandos: 

```
echo "console.log(\"version imagen v0.2\");" >> index.js

docker image build -t hello:v0.2 .

docker image ls

docker container run --rm hello:v0.2

docker image history hello:v0.2 
```

## INSPECT

Consulta todos los datos de una imagen. Bajo _RootFS.Layers_ se listan los identificadores únicos (SHA256) de cada capa, que permite el archivo en los repositorios (_Registry_)

```
docker image inspect alpine

docker image inspect --format "{{ json .RootFS.Layers }}" alpine

docker image inspect --format "{{ json .RootFS.Layers }}" hello:v0.2
```

---

## Referencias:

- [docker image history](https://docs.docker.com/engine/reference/commandline/image_history/)
- [docker image inspect](https://docs.docker.com/engine/reference/commandline/image_inspect/)