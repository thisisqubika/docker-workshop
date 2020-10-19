# Docker workshop

## Objetivo de aprendizaje

Aportar a los participantes las capacidades para el uso de Docker de forma rápida y directa. 

## Requisitos

### 1. Docker daemon y docker cliente

#### a. Instalación máquina virtual

[Utilizando vagrant](https://moove-it.github.io/docker-workshop/site/chapter01/03vagrant/)

#### b. Instalación en host (Mac)

#### Docker instalado y servicio corriendo

Verificar la instalación siguiendo [este documento](https://moove-it.github.io/docker-workshop/site/chapter01/02verificar/).

### 2. Orquestador docker-compose

#### docker-compose instalado 

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
	- Entendiendo contenedores
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
	- Orquestadores de contenedores: Intro a Kubernetes

## Carga horaria y calendario

| **Sesión** | **Fecha** | **Horario** | **Temas** |
|:--|:--|:--|:--|
| **1** | 20/oct | 9-11 | Entendiendo contenedores<br>Verificar instalación<br>Primeros pasos y uso básico |
| **2** | 22/oct | 9-11 | Imágenes |
| **3** | 27/oct | 9-11 | Storage / Volúmenes<br>Redes docker |
| **4** | 29/oct | 9-11 | Orquestación / Multiple contenedores |

## Metodología

Teórico-práctico

## Público objetivo

Interesados en usar Docker para correr aplicaciones.

## Bibliografía

### Docker - Guía del Usuario
De Rodolfo Pilas

Publicación: [https://moove-it.github.io/docker-workshop/site/](https://moove-it.github.io/docker-workshop/site/)

### Presentaciones

* [Docker workshop 01](https://slides.com/pilasguru/docker-workshop-01/live)
* [Docker workshop 02]
* [Docker workshop 03]
* [Docker workshop 04]

### Repositorio

* [https://github.com/moove-it/docker-workshop](https://github.com/moove-it/docker-workshop)


