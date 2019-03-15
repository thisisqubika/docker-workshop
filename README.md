# Docker workshop

## Objetivo de aprendizaje

Aportar a los participantes las capacidades para el uso de Docker de forma rápida y directa. 

## Requisitos

### Docker instalado y servicio corriendo

Verificar la instalación siguiendo [este documento](https://pilasguru.gitlab.io/Docker-GuiaParaElUsuario/chapter01/02verificar/).

### docker-compose instalado 

Verificación: 
```
$ docker-compose version
docker-compose version 1.24.0-rc1, build 0f3d4dda
docker-py version: 3.7.0
CPython version: 3.6.6
OpenSSL version: OpenSSL 1.1.0h  27 Mar 2018
```

## Temario

1. Generalidades
	- Como funciona
	- Verificar instalación
2. Primeros pasos y uso básico
	- Autoejecutable
	- Comando
	- Shell
	- Servicio
3. Imágenes
	- Gestión de repositorio de imágenes
	- Crear imágenes propias
	- A partir de un contenedor corriendo
	- A partir de una imagen de terceros (Dockerfile)
	- Capas de imágenes
	- Compartir imágenes por repositorio (público)
4. Storage / Volúmenes
	- Espacio disco host
	- Volúmenes
5. Redes docker
	- Contenedores sin red
	- Red del host
	- Red de bridge
	- Redes privadas entre contenedores
6. Orquestación / Multiple contenedores
	- Docker-compose
	- Docker socket

## Metodología

Teórico-práctico

## Público objetivo

Tú que quieres usar Docker para correr tus aplicaciones.

## Carga horaria y calendario

| **Sesión** | **Fecha** | **Horario** | **Temas** |
|:--|:--|:--|:--|
| **1** | 19/mar | 9-10 | Generalidades<br>Primeros pasos y uso básico |
| **2** | 21/mar | 9-10 | Imágenes |
| **3** | 26/mar | 9-10 | Storage / Volúmenes<br>Redes docker |
| **4** | 28/mar | 9-10 | Orquestación / Multiple contenedores |

## Bibliografía

### Docker - Guía del Usuario
De Rodolfo Pilas

Publicación: [https://moove-it.github.io/docker-workshop/site/](https://moove-it.github.io/docker-workshop/site/)

Repositorio: [https://github.com/moove-it/docker-workshop](https://github.com/moove-it/docker-workshop)

