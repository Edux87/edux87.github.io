---
layout: post
title:  "Docker Install"
date:   2016-12-07 17:20:17
categories: docker
---
[Docker](https://docker.com/) hace más sencillo y fácil la ejecución de procesos de aplicación en un contenedor (que son como máquinas virtuales, sólo que más portátil), más amigable con los recursos y más dependiente del sistema operativo. Para una introducción detallada a los diferentes componentes de un contenedor Docker, echa un vistazo a [The Docker Ecosystem: An Introduction to Common Components.](https://www.digitalocean.com/community/tutorials/the-docker-ecosystem-an-introduction-to-common-components)

## Prerequisitos
Para continuar con este pequeño tutorial deberas de tener instalado:

  - 64-bit Ubuntu 16.04 Droplet
  - Un usuario Non-root, que tenga privilegios para ejecutar sudo

## Instalando Docker
{% highlight bash %}
# Actualiza la base de datos de tus paquetes
sudo apt-get update

# Agrega el GPG key del repositorio oficial de Docker
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609Dsudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'

# Agrega las fuentes del repositorio de Docker
sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'

# Actualiza nuevamente la base de datos de tus paquetes
sudo apt-get update

# Asegúrese de que está a punto de instalar desde el repositorio de Docker en lugar del repositorio predeterminado de Ubuntu 16.04:
apt-cache policy docker-engine

# Finally, install Docker:
sudo apt-get install -y docker-engine

# Docker ahora debería de estar instalado, el servicio iniciado, y el proceso habilitado para iniciar en el arranque. Compruebe que se está ejecutando:
sudo systemctl status docker
{% endhighlight %}

## Ejecutando Docker sin Sudo
{% highlight bash %}
# Debera de cerrar la session y volver a ingresar para que haga efecto.
sudo usermod -aG docker $(whoami)
{% endhighlight %}
