# docker-compose

_Compose_ es una herramienta que define y corre aplicaciones basadas en múltiples contenedores con Docker.

La definición se realiza en un único archivo y se lanzan los múltiples contenedores en un único comando, que realiza todo lo que se tenga que hacer para correr los múltiples contenedores.

Utilizando el ejemplo de Wordpress de la sección anterior definen los servicios y redes en un único `docker-compose.yml`

```
version: '3'

services:

# docker run \
# -e MYSQL_ROOT_PASSWORD=rootpass \
# --name wpdb \
# --network wp \
# -v "$PWD/database":/var/lib/mysql \
# -d mariadb:latest

  wpdb:
    image: mariadb:latest
    container_name: wpdb
    volumes:
      - $PWD/database:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=rootpass
    networks:
      - wp

# docker run \
# -e WORDPRESS_DB_PASSWORD=rootpass \
# -e WORDPRESS_DB_HOST=wpdb \
# --name wordpress \
# --network wp \
# -p 8081:80 \
# -v "$PWD/html":/var/www/html \
# -d wordpress

  wordpress:
    depends_on:
      - wpdb
    image: wordpress
    container_name: wordpress
    networks:
      - wp
    ports:
      - "8081:80"
    volumes:
      - $PWD/html:/var/www/html
    environment:
      - WORDPRESS_DB_PASSWORD=rootpass
      - WORDPRESS_DB_HOST=wpdb

networks:
  wp:	
```

## UP

Se lanza la aplicación con la opción `up` y opcionalmente `-d` para que ejecute _detached_ de la consola:

```
$ docker-compose up -d
Creating network "wp_wp" with the default driver
Creating wpdb ...
Creating wpdb ... done
Creating wordpress ...
Creating wordpress ... done
```


## PS

```
$ docker-compose ps
  Name                 Command               State          Ports
-------------------------------------------------------------------------
wordpress   docker-entrypoint.sh apach ...   Up      0.0.0.0:8081->80/tcp
wpdb        docker-entrypoint.sh mysqld      Up      3306/tcp
```

## STOP / START / RESTART

Compose nos permite detener, iniciar o reiniciar nuestra aplicación en múltiples contenedores con un único comando

## DOWN

La opción `down` detiene la aplicación y borra todos los recursos definidos en el `docker-compose.yml`

```
$ docker-compose down
Stopping wordpress ... done
Stopping wpdb      ... done
Removing wordpress ... done
Removing wpdb      ... done
Removing network wp_wp
```


## Comandos docker no disponibles

Existen comandos docker que **no están disponibles** para usar en `docker-compose`, esos comandos son:

* Los comandos de administración como: `save, search, images, import, export, tag, history`
* Los comandos de interacción con el usuario como `attach, exec, login, wait`

---

## Ejercicios

### 1.

Basados en la imagen [tomcat](https://hub.docker.com/_/tomcat/) que escucha en el puerto 8080.

Crear. un `docker-compose.yml` para levantar una aplicación tomcat del ejemplo [Sample Application](https://tomcat.apache.org/tomcat-8.0-doc/appdev/sample/)

### 2. 

Utilizando la aplicación _cloud native_ **traefik** configurar un proxy reverso para la aplicación del ejercicio **1** que escuche en el puerto 80 (u otro que prefiera)

Imagen: [traefik:latest](https://hub.docker.com/_/traefik)

---

Referencias:

* [Overview of Docker Compose](https://docs.docker.com/compose/overview/)
* [Compose file version 3 reference](https://docs.docker.com/compose/compose-file/)
