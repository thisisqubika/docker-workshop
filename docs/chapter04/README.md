# Filesystem esfímero

Los contenedores tienen un **filesystem esfímero**, es decir que estará disponible mientras el contenedor exista. Una vez que el container se borre, el filesystem también será eliminado.

## Mantener datos 

Para mantener datos fuera del contenedor existen tres posibilidades:

1. Servicios externos:
	- filesystem remotos
	- storage de objetos
	- bases de datos
2. Filesystem del Host
	- bind mount
	- volumes (docker volume) 
3. Memoria del Host (temporal)
	- tmpfs mount

## Imágenes y volúmenes

Los volúmenes, los bind mount y los tmpfs mount no son parte de las imágenes que se puedan crear

---

## Referencias:

- [Manage data in Docker](https://docs.docker.com/storage/)
