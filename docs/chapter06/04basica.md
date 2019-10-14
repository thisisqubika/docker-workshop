# Estructura básica

Una estructura básica para un sitio con una aplicación que es un api de un proyecto llamado **consola-control** llevaría una estructura básica:

```
consola-control/
├── api
│   ├── Dockerfile
│   ├── package.json
│   └── src
│       └── index.js
└── docker-compose.yml
```

El archivo `api/Dockerfile` tendría el siguiente contenido:

```
FROM node:8
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8080
CMD [ "npm", "start" ]
```

La imagen creada es _autónoma_ y es capaz de poner a funcionar el servicio del `api`.

El archivo `docker-compose.yml` se encargaría de levantar todo lo que requiere la aplicación **consola-control** para funcionar:

```
services: 
  frontend:
    build: api
    links:
      - backend:redis
    ports:
      - 8081:8081
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

