---
type: post
layout: default
language: spanish
summary: Cómo utilizar Pyglyph de manera efectiva para crear texturas con fuentes.
title: Utilizando Pyglyph
---

Pyglyph es un generador de texturas de fuentes desarrollado en Python. El objetivo que tenía en mente era facilitar el renderizado de fuentes en proyectos relacionados con aplicaciones y videojuegos con [OpenGL ES](http://es.wikipedia.org/wiki/OpenGL_ES) bajo dispositivos iOS. 

Pyglyph es capaz de generar dos archivos, un primer archivo png con todos los caracteres requeridos con un tamaño y color dados, y un segundo archivo con metadatos sobre cada uno de los caracteres presentes en el archivo gráfico. El archivo de metadatos generado es un XML de tipo [plist](http://en.wikipedia.org/wiki/Plist), facilitando su uso en proyectos para dispositivos iOS, aunque utiliza un sistema de plantillas para poder configurar el formato de salida de los metadatos.

Pyglyph está inspirado en un ejercicio desarrollado en el libro [iPhone 3D Programming](http://oreilly.com/catalog/9780596804831) con el mismo propósito, libro que recomiendo encarecidamente si deseas introducirte en el mundo del desarrollo con OpenGL ES sobre iPhone.

La siguiente imagen es un ejemplo del tipo de texturas que es posible generar con Pyglyph: ![Ejemplo Pyglyph](/media/images/posts/cooper.png)

Este es un pequeño tutorial de como instalar y utilizar Pyglyph para generar las texturas que necesitas para tus proyectos.


## Instalación

Pyglyph tiene tres dependencias que es necesario tener instaladas para poder utilizarlo:

* Python (Pyglyph ha sido probado con la versión 2.6.1).
* PyCairo.
* Mako.

### Instalando PyCairo

[PyCairo](http://cairographics.org/pycairo/) es un módulo para permitir el uso de la librería Cairo desde Python. Es el módulo que utiliza Pyglyph para el renderizado de las fuentes. Para instalarlo podemos utilizar la herramienta [easy_install](http://packages.python.org/distribute/easy_install.html) del siguiente modo:

{% highlight bash %}
$ sudo easy_install pycairo
{% endhighlight %}

Para comprobar que la instalación de PyCairo podemos ejecutar el siguiente comando, que deberá no mostrar ningún error en pantalla en caso de que la instalación haya finalizado correctamente:

{% highlight bash %}
$ python -c "import cairo"
{% endhighlight %}

### Instalando Mako

[Mako](http://www.makotemplates.org/) es una estupenda librería para la creación de plantillas en Python, es la que utiliza Pyglyph para la generación de los archivos de metadatos y poder hacer configurable la generación de estos. Para instalar Mako utilizamos el siguiente comando:

{% highlight bash %}
$ sudo easy_install mako
{% endhighlight %}

Para comprobar su correcta instalación ejecutamos el siguiente comando, que no debería mostrar ningún mensaje de error:

{% highlight bash %}
$ python -c "import mako"
{% endhighlight %}

Con la instalación de Mako ya tenemos todo lo que necesitamos para poder generar texturas con Pyglyph.

## Jugando con Pyglyph

Seguimos trabajando en la redacción de este artículo...
