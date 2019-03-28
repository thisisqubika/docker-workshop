# Multiple contenedores

Como los contenedores están pensados para ejecutar un único proceso/daemon lo normal es utilizar múltiples contenedores para cada proceso que requiere nuestra aplicación. 

La tendencia es descomponer nuestra aplicación en _microservicios_ que permiten desarrollos independientes y gestión independientes, que se levantan orquestados en conjunto para que la aplicación quede corriendo.

## Ejecutar múltiples contenedores vinculados

El siguiente ejemplo muestra un contenedor la aplicación Wordpress en múltiples contenedores:
* Contenedor `wordpress` levanta un servicio web y el intérprete PHP.
* Contenedor `wpdb` corre la base de datos MySQL requerida por Wordpress para archivar sus datos

```
docker network create wp 

mkdir -p wp/database wp/html; cd wp

docker run \
-e MYSQL_ROOT_PASSWORD=rootpass \
--name wpdb \
--network wp \
-v "$PWD/database":/var/lib/mysql \
-d mariadb:latest

docker run \
-e WORDPRESS_DB_PASSWORD=rootpass \
-e WORDPRESS_DB_HOST=wpdb \
--name wordpress \
--network wp \
-p 8081:80 \
-v "$PWD/html":/var/www/html \
-d wordpress
```

En el siguiente ejemplo se muestra cómo sería el arranque si se utilizara el _bridge default_ utilizando la opción `--link`:

```
docker run \
-e WORDPRESS_DB_PASSWORD=rootpass \
--name wordpress \
--link wpdb:mysql \
-p 8081:80 \
-v "$PWD/html":/var/www/html \
-d wordpress
```

## LOGS

Se puede verificar el funcionamiento de un contenedor revisando su log:

```
docker logs wordpress
```
 
## Borrar aplicación

Y para borrar estos aplicación debemos ejecutar:

```
docker container stop wordpress wpdb
docker container rm wordpress wpdb
docker network rm wp  
```

Y los datos quedarán en las carpetas montadas.

