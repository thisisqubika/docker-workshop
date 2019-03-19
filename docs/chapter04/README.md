# Esfímero

Los contenedores tienen un **filesystem esfímero**, es decir que estará disponible mientras el contenedor exista. Una vez que el container se borre, el filesystem también será eliminado.

## Persistir datos

Para persistir datos se disponen de dos estrategias:

- Servicios externos (filesystem remotos, storage de objetos, bases de datos, etc.)
- Configuraciones del contenedor para filesystem externos.

## Filesystem externos

Existen dos formas de hacerlo: 

- **bind mount** permite usar un carpeta (path) del host y presentarlo dentro del contenedor en un punto de montado, por ejemplo `/app`.   

Es la forma más fácil de conectar el filesystem del host con el contenedor. 

El _bind mount_ se especifica en el momento de lanzar el contenedor y requiere realizar los procesos de respaldo, migración, etc. con herramientas fuera de docker.

- **volume** es un dispositivo de disco externo el contenedor creado por docker y puede ser utilizado por otros contenedores simplemente indicando la ruta (nombre).


