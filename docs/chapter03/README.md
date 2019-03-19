# Imágenes docker y Registry

El sistema de imágenes de docker permite guardar contenedores docker prontos para utilizar (llamados _imágenes_) en un banco local o remoto. Una imagen es un paquete ejecutable que incluye todo lo necesario para correr la aplicación (código, librerías, entorno y configuración).

El servicio de banco de imágenes denomina _Registry_ y tiene como objetivo compartir imágenes entre distintos sistemas, grupos de usuarios o, inclusive, distribución de software pronto para poner a correr. 

El Registry puede ser público (anónimo) o privado (con validación).

El banco de imágenes _local_ permite guardar las imágenes que se descargan de los _Registry_ y también las que son creadas localmente en el host donde se ejecuta docker.

Utilizando en el nombre de la imagen la URL del Registry es posible subir imágenes de diferentes repositorios.

---

## Referencias:

- [https://docs.docker.com/engine/reference/commandline/images/](https://docs.docker.com/engine/reference/commandline/images/)
- [https://docs.docker.com/engine/tutorials/dockerimages/](https://docs.docker.com/engine/tutorials/dockerimages/)


