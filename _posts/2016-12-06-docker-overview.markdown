---
layout: post
comments: true
title:  "Docker OverView"
date:   2016-12-06 18:00:00
categories: docker
---

Para comenzar a trabajar con docker tenemos que tener en mente algunos conceptos previos, tales como:

  - **Image**: puede contener un sistema operativo como Ubuntu y sobre ello traer un paquete como Apache o Nginx. Se utilizan como una plantilla (solo lectura) para los contenedores, además se puede **clonar** imageness desde el repositorio oficial de [Docker Hub](https://hub.docker.com) estas ya contienen uno o varios paquetes ya pre-configurados para su uso.
  - **Contenedor**: Es la *instancia* de una imagen, que trabaja de manera aislada. Podemos añadir que cada contenedor se crea a partir de una imagen, cada contenedor es una plataforma de aplicaciones aisladas y segura, puede contener instrucciones de qué procesos para funcionar.

## Como clonar imágenes?
Una vez que as navegado por [Docker Hub](https://hub.docker.com), y encuentres alguna imagen con la que quisieras trabajar, solo tenemos que hacer `docker pull ubuntu:14.04`:

Al igual que un repositorio git, docker hub puede manejar tags o etiquetas para las imagenes, por defecto descargara la image con la version mas reciente. Puedes cambiar el tag `:14.04` por la version de ubuntu que quieras. Este proceso tomara algunos segundos (o minutos) dependiendo de la velocidad de tu conexión a Internet.

Cuando tengamos descargada la imagen, deberemos de aprender un comando muy importante `docker images`, este comando nos mostrara una lista de imágenes clonadas y disponibles.

## Trabajando con contenedores

Ahora, que tenemos clonada nuestra imagen, vamos a acceder a un proceso o servicio puede ser **bash**, mediante el siguiente comando:

{% highlight bash %}
sudo docker run -it ubuntu:14.04 /bin/bash
root@7280eeaad455: _
# Es la consola, de la imagen que acabamos de clonar.
{% endhighlight %}

Podemos ejecutar cualquier instrucción. porque ademas de haber ingresado a la consola acabas de crear un ***contenedor***.

Podemos salir de esta consola con el comando **exit**. Los contenedores tienen status, como stop o start, cuando este esta en **stop**, no podemos efectuar ningún cambio y no puede interactuar con otros contenedores, cuando esta en modo **start** podemos aplicar cambios.

{% highlight bash %}
docker ps -a
#Lista todos los contenedores con sus IDs.

docker start -a [id_contenedor]
#para iniciar el contenedor, y le pasamos el parámetro -a para capturar la salida.

docker attach [IdContenedor]
#Y mediante el comando attach podremos acceder a la consola.
{% endhighlight %}


## Creando mis propias imágenes
Existen 2 formas de crear imágenes en Docker, la forma automatizada, utilizando un archivo de configuración conocido como `Dockerfile`,  y la forma manual, mediante lineas de comando, veremos ambas a continuación.

### Forma Manual (Usando Contenedor)

{% highlight bash %}
#Vamos a crear un contenedor desde una imagen de Ubuntu.
docker run -it ubuntu:14.04 /bin/bash

# Bien!, ahora estamos dentro de nuestro contenedor y podemos instalar algunos paquetes.
root@90be1f6c8983:/#

apt-get update && apt-get upgrade
apt-get install curl

# finalizado este proceso salimos del contendor
exit

# Ahora que estamos en nuestra terminal,
# vamos a listar los contendores que tenemos en memoria.
docker ps -a
CONTAINER ID        IMAGE               COMMAND                          
90be1f6c8983        ubuntu              "/bin/bash"

# crearemos una nueva imagen en base a este contenedor
# usaremos la siguiente sintaxis <nombreImagen>/curl:<tag>.
# tageamos como :1.0 nuestra primera versión de la imagen.
docker commit 90be1f6c8983 newImage/curl:1.0

#Verificamos la existencia de la nueva imagen.
docker image
REPOSITORY          TAG                 IMAGE ID
newImage            1.0                 c85abd987669
{% endhighlight %}

## Forma Automática (Usando Dockerfile)
Un `Dockerfile` es un archivo de configuración que contiene instrucciones para construir una **Image**, es un camino mucho mas eficiente. ya que tenemos una archivo de texto plano que podremos *versionar*.

{% highlight bash %}
# crearemos una carpeta para nuestro demo.
mkdir my_image

# Es importante estar dentro de esta carpeta.
cd my_image

# Creamos un file y lo editamos.
vim Dockerfile

# Ingresamos las siguientes instrucciones.
FROM ubuntu:14.04
ENV TERM xterm
MAINTAINER edanie15@gmail.com

RUN apt-get install vim
RUN apt-get install curl

#Guardamos el documento (:x!) y salimos ..
#Construiremos la imagen en base al Dockerfile, mediante el comando.

docker build -t edgarc/newimage:1.0 .

#Verificamos la existencia de la nueva imagen.
docker image

REPOSITORY           TAG                 IMAGE ID
edgarc/newimage      1.0                 6d4f6eb41dce

# Para actualizar la imagen solo vuelve a ejecutar docker build ...
# Pero si quieres eliminar esta imagen utiliza rmi con el IMAGE ID
docker rmi 6d4f6eb41dce

{% endhighlight %}

Existen muchos mas comandos para personalizar nuestro Dockerfile y una serie de buenas practicas para la composicion de este, la documentacion oficial nos lo dice en [este link](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/).

Seguiremos expandiendo esta entrada
