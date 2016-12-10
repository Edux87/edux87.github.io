---
layout: post
title:  "Docker Jekyll Generator"
date:   2016-12-07 16:50:17
categories: docker
---

Jekyll!, un simple generador de archivos estáticos, con una curva de aprendizaje muy corta y muy sencilla de usar. si quieres un blog rápido, fácil de administrar (y free), te recomiendo una combinacion entre [github pages](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/) & [jekyll](https://jekyllrb.com).

Listo para crear tu primer blog con Jekyll?, excelente. Primero debemos tener instalado docker en nuestro S.O, así que te recomiendo que leas este post ([Docker Install](/docker/2016/12/07/docker-install.html)), antes de continuar.

## Docker Pull Image

{% highlight bash %}
#!/bin/bash

# Ejecutar en tu terminal
docker pull edaniel15/jekyll-generator
Using default tag: latest
latest: Pulling from edaniel15/jekyll-generator

3690ec4760f9: Already exists
6353f0aa4196: Already exists ...  

{% endhighlight %}


## Crear un Alias
{% highlight bash %}
#!/bin/bash

# Para mayor comodidad crearemos un alias
alias jekyll='docker run -v $(pwd):/src/site:rw -p 4001:4000 -it edaniel15/jekyll-generator'
{% endhighlight %}

## Generando Sitio

{% highlight bash %}
#!/bin/bash

# crea un folder y ejecutamos lo siguiente
mkdir my_blog
cd my_blog

# Crea nuevo sitio
% jekyll new
Create a New Awesome Site!
New jekyll site installed in /src/site ...

# Genera los estaticos
% jekyll build
Built!
Configuration file: /src/site/_config.yml ...

# Crear el servidor
% jekyll serve
Initialize Server!
Configuration file: /src/site/_config.yml ...

# Ahora entra en tu navegador preferido ingresa la ruta
# localhost:4001

{% endhighlight %}

## Creando Contenido
En nuestra carpeta `cd my_blog` encontraras un muy intuitivo archivo de
configuracion llamado `_config.yml`, aqui podras cambiar muchos aspectos
de tu sitio, tambien tenemos una carpeta llamada `_post/` con un archivo
en [markdown format](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet),
clona este archivo y modificalo para generar contenido. es bueno mantener
el estandar `YYYY-MM-DD-name-of-post.markdown`, despues actualiza tu navegador
y veras los cambios.
