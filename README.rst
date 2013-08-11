===========================
Portal de Canaima GNU/Linux
===========================

Este paquete instala una instancia de Plone con todos los componentes
necesarios para construir el sitio web de Canaima GNU/Linux

Se proporcionan configuraciones para los siguientes entornos:

 - Desarrollo
 - Pruebas
 - Producción

Instalación
===========

Entorno de desarrollo
=====================

Prerrequisitos
--------------

 - Python 2.7 y bibliotecas de desarrollo

Crear un archivo ~/.buildout/default.cfg con lo siguiente:

.. code-block:: console

  [buildout]
  download-cache = ~/.buildout/downloads
  eggs-directory = ~/.buildout/eggs
  extends-cache = ~/.buildout/extends

 - download-cache: Directorio donde se almacenan los sources de los paquetes
   descargados con los que se contruyen los paquetes python (eggs).

 - eggs-directory: Directorio donde se almacenan los paquetes python generados.

 - extends-cache: Directorio donde se almacenan archivos de configuracion (.cfg)
   que son descargados desde la red, generalmente por una clausula extends y que
   son utilizados cuando el buildout se ejecuta sin conexión (offline mode)


Descargar el buildout
---------------------

Para obtener una copia de este proyecto ejecute los siguientes comandos:

.. code-block:: console

  $ cd ~
  $ git clone git@github.com:canaimagnulinux/buildout.web.canaimagnulinux.git

Puede utilizar un nombre de carpeta diferente si así lo desea.


Generar el buildout
-------------------

Para inicializar y construir una copia de este proyecto en entornos de
desarrollo, ejecute los siguientes comandos:

.. code-block:: console

  $ cd ~/buildout.web.canaimagnulinux
  $ python bootstrap.py
  $ ./bin/buildout

Para iniciar la instancia del sitio Plone, ejecutar:

.. code-block:: console

  $ ./bin/instance fg

Puede acceder al sitio a través de la dirección http://127.0.0.1:8080/


Entorno de pruebas (staging)
============================

Ingresar al directorio donde se obtubo la copia del buildout:

.. code-block:: console

  $ cd ~/buildout.web.canaimagnulinux

Una vez relacizado ese paso, ejecute los siguientes comandos:

.. code-block:: console

  $ python bootstrap.py -c staging.cfg
  $ ./bin/buildout -c staging.cfg

Para iniciar la instancia del sitio Plone, ejecutar:

.. code-block:: console

  $ ./bin/instance fg

Puede acceder al sitio a través de la dirección http://127.0.0.1:8080/

En caso de encontrar errores del tipo "Can't update package 'xxx.yyy' because
its URL doesn't match." utilice el siguiente comando y ejecute nuevamente el
buildout:

.. code-block:: console

  $ rm -rf ~/canaimagnulinux/src/xxx.yyy

Reemplace "xxx.yyy" por el nombre del paquete que se muestra en el mensaje de
error.

Pasos comunes para el entorno de producción y pruebas
=====================================================

Ejecución paso a paso:

Instalación de dependencias del sistema operativo:

.. code-block:: console

    $ sudo apt-get install git-core python-dev build-essential libjpeg62-dev libfreetype6-dev zlib1g-dev libxml2 libxml2-dev libxslt1-dev libmysqlclient-dev wv poppler-utils lynx munin libwww-perl

Crear el usuario de sistema:

.. code-block:: console

    $ sudo adduser --system --home /srv/plone \
                   --disabled-password --disabled-login plone

Acceder al usuario, clonar el repositorio y correr el bootstrap:

.. code-block:: console

    $ sudo -u plone -s -H

    $ git clone git@github.com/canaimagnulinux/buildout.web.canaimagnulinux.git
    Initialized empty Git repository in /srv/plone/buildout.web.canaimagnulinux/.git/
    Password:

    $ cd buildout.web.canaimagnulinux

Generar el buildout y lo ejecutarlo con el profile de producción según sea
una instancia.

Profile para maquinas de solo lectura o para encuestas.

.. code-block:: console

    $ python bootstrap.py -c production.cfg

    $ bin/buildout -c production.cfg

Iniciar las instancias manualmente.

.. code-block:: console

    $ bin/supervidord

Actualizar la configuración de las servicios del SO:
 (haproxy, varnish y nginx).

Ejecutar el siguiente comando desde un usuario que tenga los privilegios
necesarios para utilzar sudo.

.. code-block:: console

    $ bin/update-so-config.sh

Descargas
=========

Usted puede encontrar la versión de desarrollo del paquete ``buildout.web.canaimagnulinux``
en el `repositorio Canaima GNU/Linux`_ en Github.com.

Autor(es) Original(es)
======================

* Leonardo J .Caballero G. aka macagua

Colaboraciones impresionantes
=============================

* Nombre Completo aka apodo


Para una lista actualizada de todo los colaboradores visite:
https://github.com/canaimagnulinux/buildout.web.canaimagnulinux/contributors

.. _sitio Web de Canaima GNU/Linux: http://canaima.softwarelibre.gob.ve/
.. _repositorio Canaima GNU/Linux: https://github.com/canaimagnulinux/buildout.web.canaimagnulinux