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
