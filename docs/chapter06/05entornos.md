# Estructura con entornos

Ahora vemos el proyecto **consola-control** pero mantenido en dos entornos:

* development
* production

y su estructura quedaría de la siguiente forma:

```
consola-control/
├── common
│   └── docker-compose.yml
│   └── nginx.conf
├── development
│   ├── api
│   │   ├── Dockerfile
│   │   ├── package.json
│   │   └── src
│   │       └── index.js
│   └── docker-compose.yml
└── production
    ├── api
    │   ├── Dockerfile
    │   ├── package.json
    │   └── src
    │       └── index.js
    └── docker-compose.yml
```

## Development

El `common/docker-compose.yml` levanta el proxy reverso solamente que es común a ambos entornos

```
web:
  image: nginx
  ports:
    - 8082:80
  volumes:
    - nginx.conf:/etc/nginx/nginx.conf
```

El `development/docker-compose.yml` extiende `common`, presenta el filesystem del host en el dentro del contenedor (para seguir desarrollando) y utiliza redis desde el host.

```
web:
  extends:
    file: ../common/docker-compose.yml
    service: web
  volumes_from: 
    - api
  links:
    - api:8080

api:
  build: api
  volumes:
    - .:/usr/src/app
```

Para crear la imagen el `development/api/Dockerfile` no copia los códigos dentro, ya que serán montados al lanzar el entorno.

```
FROM node:8
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
CMD [ "npm", "start" ]
```

Para lanzar el entorno, solamente ejecutar:

```
cd development
docker-compose up -d
```

## Producción

El `production/docker-compose.yml` extiende `common` pero utiliza la imagen completa, además de tener el servicio redis:

```
services:
  frontend:
    extends:
      file: ../common/docker-compose.yml
      service: web
    build: api
    links:
      - backend:redis
    environment:
      - VAR1=value
    networks: 
      - consola-control
    depends_on:
      - backend
    restart: always

  backend:
    image: redis:3
    networks:
      - consola-control
    restart: always
    
networks:
   consola-control:
```

Y el archivo `production/api/Dockerfile` es el mismo del capítulo anterior, donde todo el código es COPY a la imagen antes de lanzarla.

```
FROM node:8
MAINTAINER Great Dev <gd@fix-it.com>
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
CMD [ "npm", "start" ]
```



