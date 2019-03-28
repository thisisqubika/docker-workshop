# Docker compose workflow

En general se suelen realizar tres pasos para definir una aplicación en `docker-compose`

1. Definir cada servicio en un Dockerfile
2. Definir la relación entre los servicios y cómo ellos se ejecutan (entorno, volúmenes, redes) en `docker-compose.yml`
3. Lanzar la aplicación con `docker-compose up`

Veamos cómo usar esta definición de aplicación en un entorno de trabajo de un proyecto real:

1. [Estructura básica](04basica.md)
2. [Estructura con entornos](05entornos.md)

