---
layout: post
comments: true
title:  "Htop en CentOS RHEL"
date:   2016-12-17 19:00:17
categories: linux
---

*HTOP*, permite el monitorio en tiempo real de cada proceso en sistemas linux/unix
de una manera visual y amigable con el usuario, es una muy buena alternatva a top
ademas viene pre-instalado en muchas distribuciones.

# Caracteristicas
Una de las mas resaltantes y a primera vista es el uso de mouse y la opcion de los scrolls
vertical y horizontal.

  - Puedes terminar mas de un proceso
  - Puedes setear variables de entorno para los procesos seleccionados (tecla **e**)
  - Agrupar procesos (tecla **F5**)
  - Puedes puedes seleccionar mas de un proceso

# Instalacion
No existe ningun pre-requisito para la instalacion de este paquete.
{% highlight bash %}
# -------------- For RHEL/CentOS 7 --------------
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-8.noarch.rpm
rpm -ihv epel-release-7-8.noarch.rpm

# -------------- For RHEL/CentOS 6 --------------
wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
rpm -ihv epel-release-6-8.noarch.rpm

# -------------- For RHEL/CentOS 5 --------------
wget http://download.fedoraproject.org/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm
rpm -ihv epel-release-5-4.noarch.rpm
{% endhighlight %}

Luego de bajar y compilar el paquete, instalamos.

{% highlight bash %}
yum install htop
{% endhighlight %}
