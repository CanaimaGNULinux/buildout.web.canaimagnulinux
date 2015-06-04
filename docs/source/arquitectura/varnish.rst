.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _varnish_setup:

===============
Motor de caché
===============

Es un `Servidor Proxy`_ que realiza una tarea acceso a Internet en lugar 
de otro ordenador. Un proxy es un punto intermedio entre un ordenador 
conectado a Internet y el servidor al que está accediendo. Cuando navegamos 
a través de un proxy, nosotros en realidad no estamos accediendo directamente 
al servidor, sino que realizamos una solicitud sobre el proxy y es éste quien 
se conecta con el servidor que queremos acceder y nos devuelve el resultado de 
la solicitud.

Por lo general un Proxy Caché funciona similar al de un `proxy HTTP`_ o `HTTPs`_. 
Su función es cargar previamente el contenido web solicitado por el usuario para 
acelerar la respuesta Web en futuras peticiones de la misma información de la misma 
máquina u otras.

.. _que_es_varnish:

Varnish
=======

Formalmente `Varnish`_ es un proxy que coloca entre el usuario y el (o los) 
servidor(es) web, siendo Varnish quien accede al servidor web, manteniendo 
cache del contenido y manipulando los ``headers`` y tal vez también el contenido.

.. figure:: ../_static/varnish-logo.png
  :align: center
  :width: 210px
  :alt: Varnish

  Logotipo de Varnish.

El proxy cache Varnish realiza la re-dirección de la solicitud ya sea
hacia el cache interno, hacia un servidor web u otro servidor web.

Debido a que proxy esta hecho para pocas cosas es muy eficiente haciendo
lo que hace y permite jugar muy eficientemente con las solicitudes.

Por ejemplo, puede balancear las solicitudes, o redirigir diferentes
solicitudes a un servidor u otro dependiendo de algún ``header``, de alguna
ruta o de algún tipo de archivo, o incluso de si un servidor funciona
bien o da errores, en cuyo caso inclusive puede mantenerse dando una
respuesta del cache mientras el servidor no funciona.

Con Varnish como proxy cache se puede hacer las siguientes operaciones:

-  Caché por tipos de archivo.

-  Caché por rutas o patrones.

-  Caché de paginas a usuarios anónimos.

-  Caché de secciones de una pagina.

-  Caché de una pagina con excepción en secciones.

Al configurar un Varnish en frente de un servidor web podemos liberar al
servidor web de muchísimas solicitudes, incluso, si es un sitio enfocado
a usuarios anónimos (como un blog, sitio de noticias, sitio informativo,
etc) hasta podríamos hacer que el servidor web no reciba casi
solicitudes y todos sean servidos por el servicio de Varnish.

Perfectamente podemos hablar de reducir las solicitudes de 1.000 en una
hora a 5 o 20, y lo mejor de todo, es que podrían aumentar las
solicitudes en esa hora a 10.000 o 100.000 y no aumentar ni una
solicitud al servidor web, reduciendo también las solicitudes a la base
de datos y aumentando la velocidad de respuesta de 1 segundo por
solicitud a unos mili-segundos.

Funcionamiento con Plone
========================

Varnish, es utilizado en esta esquema de configuraciones como un motor
de caché que guarda las respuestas de las peticiones dinámicas que se
hacen a la Plone y las sirve directamente de disco para
mejorar el desempeño.


Instalación
===========

La instalación se realiza a través de configuraciones que usan recetas de 
instalación de buildout y funciona de esta manera:

.. code-block:: ini

  [buildout]
  parts =
      pcre
      varnish-build
      varnish
      
  # Zope, Varnish and Nginx URLs download versions to be used
  [downloads]
  pcre = http://download.sf.net/project/pcre/pcre/8.31/pcre-8.31.tar.gz
  varnish = http://dist.jarn.com/public/varnish-2.1.5.tar.gz
  
  # A dependency for build Varnish
  # For options see http://pypi.python.org/pypi/hexagonit.recipe.cmmi
  [pcre]
  recipe = hexagonit.recipe.cmmi
  url = ${downloads:pcre}
  keep-compile-dir = true
  
  # Varnish, acting as a reverse lookup caching proxy
  # For options see http://pypi.python.org/pypi/hexagonit.recipe.cmmi
  [varnish-build]
  recipe = hexagonit.recipe.cmmi
  url = ${downloads:varnish}
  configure-options =
    --with-pcre=${pcre:location}/../pcre__compile__/pcre-8.31
  
  # This recipe help to install Varnish.
  # For options see http://pypi.python.org/pypi/plone.recipe.varnish
  [varnish]
  recipe = plone.recipe.varnish
  daemon = ${varnish-build:location}/sbin/varnishd
  mode = ${varnish-settings:mode}
  bind = ${hosts:varnish}:${ports:varnish}
  cache-size = ${varnish-settings:cache-size}
  config = ${buildout:directory}/etc/varnish.vcl

Configuraciones de motor de caché
==================================

La configuración del motor de caché Varnish se crea utilizando una 
plantilla la cual genera un archivo mediante el proceso de construcción 
hecho por zc.buildout.

.. code-block:: cfg

  [buildout]
  parts =
      varnish-config
      
  # This recipe generates Varnish configurations
  # For options see http://pypi.python.org/pypi/collective.recipe.template
  [varnish-config]
  recipe = collective.recipe.template
  input = ${buildout:directory}/templates/varnish.vcl.in
  output = ${buildout:directory}/etc/varnish.vcl

Una muestra del archivo de configuración de Varnish es el siguiente:

.. literalinclude:: ../templates/varnish.vcl.in
   :encoding: utf-8

En proceso de instalación y configuración se requieren algunas variables de necesarias 
para Varnish. En el archivo ``buildout.d/custom-settings.cfg`` hay la siguiente configuración:

.. code-block:: cfg

  
  # -------------------------
  # Zope and Plone Parameters
  # -------------------------
  
  # Zope and Plone basic configurations
  # -----------------------------------
  [site-settings]
  localhost = 127.0.0.1
  
  [hosts]
  varnish = ${site-settings:localhost}
  
  [ports]
  varnish = 8101


.. note::
    Cada ves que allá hecho un cambio en la configuración de este servicio aplique 
    esos cambios en la plantilla ubicada en ``templates/varnish.vcl.in`` y deje el 
    trabajo el trabajo de generación del archivo de configuración buildout con el 
    siguiente comando:

    .. code-block:: sh

      $ ./bin/buildout -vvvv

Este comando generará el archivo en la ubicación ``etc/varnish.vcl`` el cual usara 
el servicio de Varnish en sus configuración de arranque y reinicia el servicio *varnish* 
mediante ``supervisor`` con el siguiente comando:

.. code-block:: sh

 $ ./bin/supervisorctl restart others:varnish

Depuración de motor de caché
=============================

Para facilitar la depuración del motor de caché Varnish se genera un bash script 
en el directorio ``bin/`` de su proyecto buildout, con la siguiente configuración:

.. code-block:: cfg

  [buildout]
  parts =
      varnishlog
  # This recipe generates a bash script for varnishlog command
  # For options see http://pypi.python.org/pypi/collective.recipe.template
  [varnishlog]
  recipe = collective.recipe.template
  input = inline:
      ${varnish-build:location}/bin/varnishlog
  output = ${buildout:bin-directory}/varnishlog
  mode = 755

El cual se puede usar para supervisar el servicio en modo depuración, y se ejecuta 
de la siguiente forma:

.. code-block:: bash
 
    $ ./bin/varnishlog

Referencias
-----------

-   `Proxy`_.

-   `Varnish, Reverse Proxy y ESI`_.

-   Referencia de la documentación de `Varnish 2.1`_

.. _Servidor Proxy: http://es.wikipedia.org/wiki/Proxy#Servidor_Proxy
.. _proxy HTTP: http://es.wikipedia.org/wiki/Proxy#Servidor_HTTP
.. _HTTPs: http://es.wikipedia.org/wiki/Proxy#Servidor_HTTPS
.. _Varnish: https://www.varnish-cache.org/
.. _zc.buildout: http://coactivate.org/projects/ploneve/replicacion-de-proyectos-python
.. _Proxy: http://es.wikipedia.org/wiki/Proxy
.. _Varnish, Reverse Proxy y ESI: http://nestor.profesional.co.cr/es/book/varnish-reverse-proxy-y-esi
.. _Varnish 2.1: https://www.varnish-cache.org/docs/2.1/
