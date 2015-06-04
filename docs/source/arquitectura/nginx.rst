.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _nginx_setup:

============
Servidor web
============

`nginx`_, es un servidor web de alto desempeño, que es cada vez más utilizado en
el mundo de Plone. 

.. figure:: ../_static/nginx-logo.png
   :width: 190px
   :align: center
   :alt: Servidor Web con Nginx

   Logotipo de Nginx.

Es un servidor web ligero y de alto desempeño `http://nginx.org/ <http://nginx.org/>`_, 
que es cada vez más utilizado en el mundo de Plone. 

Funcionamiento con Plone
=========================

En este servidor se configura el Virtual host con tareas de re-escritura de direcciones 
URL para despachar todo el trafico entrante generado por los usuario y enviar las peticiones 
al servidor de caché Varnish.

Usted puede al servidor Web de la Plone a través de la siguiente dirección:

- **Tipo**: Nginx

- **Descripción**: Servidor Web como Frontend para el servidor de Caché Varnish

- **Dirección URL**: `http://SU_DIRECCION_IP/ <http://SU_DIRECCION_IP/>`_

Instalación
===========

Para realizar la instalación requiere haber instalado las :ref:`dependencias base de Nginx <requerimientos_instalacion_nginx>`.

Configuraciones de servidor web
===============================

La configuración del servidor web Nginx se crea utilizando una plantilla la cual 
genera un archivo mediante el proceso de construcción hecho por zc.buildout.

.. code-block:: cfg

    [nginx-config]
    recipe = collective.recipe.template
    input = ${buildout:directory}/templates/nginx-vhost.conf.in
    output = ${buildout:directory}/etc/nginx-vhost.conf

Una muestra del archivo de configuración de Nginx es el siguiente:

.. literalinclude:: ../templates/nginx-vhost.conf.in
   :encoding: utf-8

En la configuración se define las variables de Nginx para generar el archivo 
de configuraciones del `Virtual host`_.

.. code-block:: cfg

  [site-settings]
  client-name = sitioweb
  domain-name-production = 127.0.0.1
  localhost = 127.0.0.1
  
  [hosts]
  servername = ${site-settings:domain-name-production}
  nginx = ${site-settings:localhost}

  [ports]
  nginx = 80

Cada ves que allá hecho un cambio en la configuración de este servicio 
actualice los cambios con el siguiente comando: 

.. code-block:: sh

  $ sudo ./bin/update-so-config-sh

Este comando copiará el archivo generado en ``./etc/nginx-vhost.conf`` al directorio 
``/etc/nginx/sites-available/sitioweb.vhost.conf``, luego hace el enlace simbólico 
desde el directorio **sites-available** al directorio **sites-enabled** y reinicia 
el servicio ``nginx``.

Referencias
-----------

-   `Buildout para instalar de todas las partes de un sitio`_.

-   `Ejecutando Zope y Plone detrás de un Servidor Web`_.

.. _nginx: http://nginx.org/
.. _Buildout para instalar de todas las partes de un sitio: http://plone-spanish-docs.readthedocs.org/en/latest/buildout/plone-esquema-alta-disponibilidad.html
.. _Ejecutando Zope y Plone detrás de un Servidor Web: http://plone-spanish-docs.readthedocs.org/en/latest/zope/zope-plone-detras-servidor-web.html
.. _Virtual host: http://plone-spanish-docs.readthedocs.org/en/latest/zope/zope-plone-detras-servidor-web.html#terminologia-general
