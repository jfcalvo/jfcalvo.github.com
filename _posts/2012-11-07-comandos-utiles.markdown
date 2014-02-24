---
type: post
layout: default
language: spanish
summary: Anotaciones de algunos comandos UNIX útiles y olvidadizos.
title: Algunos comandos UNIX útiles
---

En este post añadiré progresivamente algunos comandos UNIX que he aprendido con el tiempo para tenerlos como referencia y no olvidarlos (algo que ocurre muy a menudo).

## Buscar archivos por su contenido

Supongamos que desamos buscar la cadena de texto `mrb_load_string` dentro de todos los archivos con extensión `.h` dentro de un directorio de nombre `include`, esto lo podríamos conseguir con el siguiente comando:

{% highlight bash %}
$ find include -type f -name *\.h | xargs grep -n --color=auto "mrb_load_string"
{% endhighlight %}

Utilizando los parámetros `-n` y `--color=auto` con el comando `grep` provocamos que se muestre el número de línea en el que se ha encontrado la coincidencia y que se de color a la cadena encontrada respectivamente.

## Verificación de archivos XML

Si deseamos validar la estructura o contenido de achivos XML podemos utilizar la herramienta `xmllint` la cual nos permite verificar con o sin un schema disponible la validez de archivos XML.

Verificar todos los archivos XML del directorio actual sin disponer de un XML Schema:

{% highlight bash %}
$ xmllint --noout *.xml
{% endhighlight %}

Verificar todos los archivos XML del directorio actual utilizando el XML Schema `schema.xsd`:

{% highlight bash %}
$ xmllint --noout --schema schema.xsd *.xml
{% endhighlight %}

## Evitar que tu Mac se suspenda

Si necesitas dejar tu Mac realizando alguna tarea larga y no deseas que se suspenda mientras lo dejas desatendido existe el comando `pmset` que nos permite gestionar la configuración de la energía del equipo. Para evitar que el equipo se suspenda utiliza el siguiente comando:

{% highlight bash %}
$ pmset noidle
{% endhighlight %}

Pulsando `Ctrl-c` volverás al estado normal.

## Comprimir directorios en formato zip con encriptación

Si deseamos comprimir directorios en formato zip con encriptación y excluyendo ciertos archivos podemos utilizar el siguiente comando:

{% highlight bash %}
$ zip -er output_filename directory_to_compress -x *.DS_Store*
{% endhighlight %}

La opción `e` añadirá encriptación al proceso de compresión y posteriormente pedirá un password. La opción `r` procede a añadir archivos de manera recursiva. La opción `-x` añade ficheros a excluir.

## Tiempo que el sistema lleva ejecutándose

Para conocer cuanto tiempo lleva el sistema funcionando desde que se inició podemos utilizar el comando `uptime`:

{% highlight bash %}
$ uptime
21:22  up 14 mins, 2 users, load averages: 0,62 0,61 0,40
{% endhighlight %}

En mi caso 14 minutos.

## Copiar directorios recursivamente sin incluir archivos ocultos

Útil por ejemplo para copiar directorios entre repositorios Git que incluyen archivos `.git` ocultos:

{% highlight bash %}
$ rsync -av --exclude=".*" /source/ /destination
{% endhighlight %}
