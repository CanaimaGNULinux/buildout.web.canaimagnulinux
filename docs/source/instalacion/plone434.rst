.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _plone434:

Plone 4.3.x
===========

Para instalar Plone en su versión 4.3 en entornos de servidores usando el 
sistema operativo :ref:`Debian GNU/Linux 7 <debian7>`, debe ejecutar 
los siguientes pasos con sus respectivos comando a continuación:

Dependencias de paquetes eggs
-----------------------------

Para la instalación de dependencias en :term:`paquetes Egg` Python propias 
de Plone 4.3.x, ejecute con el siguiente comando:

.. code-block:: console
 
    (python2.7)$ easy_install-2.7 "setuptools==0.6c11"

.. _obteber_plone:

Descargar Plone
---------------

Debe descargar una copia de las configuraciones buildout, ejecute los siguientes 
comandos:

.. code-block:: console

    $ cd $HOME/
    $ git clone https://github.com/CanaimaGNULinux/buildout.web.canaimagnulinux.git sitioweb
    $ cd $HOME/sitioweb

.. note:: 
    Para obtener un detalle de archivos y directorios obtenidos en la 
    descarga previa consulte la sección llamada resumen de los 
    :ref:`archivos y directorios obtenidos <archivos_directorios_obtenidos>`.

.. _archivos_directorios_buildout_init:

Arranque de construcción
------------------------

Prepare el proceso de arranque de la construcción del Plone 4.3.x usado, con el 
siguiente comando:

.. code-block:: console

    $ python bootstrap.py
    Creating directory '/home/plone/sitioweb/bin'.
    Creating directory '/home/plone/sitioweb/parts'.
    Creating directory '/home/plone/sitioweb/develop-eggs'.
    Generated script '/home/plone/sitioweb/bin/buildout'.

.. note::
    Para obtener un detalle de archivos y directorios obtenidos en la 
    descarga previa consulte la sección llamada resumen de los 
    :ref:`archivos y directorios al arranque <archivos_directorios_arranque>`.

.. _inicio_construccion:

Inicie la construcción
----------------------

Si usted realiza una instalación limpia debe iniciar el proceso de 
construcción de Plone 4.3.x, con el siguiente comando:

.. code-block:: console

    $ ./bin/buildout -vvvvvN

.. note::
    Para obtener un detalle de archivos y directorios generados tras 
    la construcción previa consulte la sección llamada resumen de los 
    :ref:`archivos y directorios creados al construir <archivos_directorios_construidos>`.

Arranque de servicios
---------------------

:ref:`Supervisor <que_es_supervisor>`, es una herramienta que nos 
ayuda a controlar el cluster de :ref:`clientes Zeo <clientes_zeo>`, 
el :ref:`balanceador de carga <haproxy_setup>` y el 
:ref:`motor de cacheo <varnish_setup>`. 

Para ejecutar supervisor por primera vez, escriba desde el directorio 
``$HOME/sitioweb`` el siguiente comando:

.. code-block:: console

    $ ./bin/supervisord

Para verificar que todos los servicios han iniciado correctamente, puede 
usar el comando ``./bin/supervisorctl``, con el siguiente comando:

.. code-block:: console

    $ ./bin/supervisorctl 
    others:haproxy                   RUNNING    pid 4813, uptime 1 day, 21:40:03
    others:varnish                   RUNNING    pid 4814, uptime 1 day, 21:40:03
    zeo-clients:client1              RUNNING    pid 25634, uptime 1 day, 13:00:47
    zeo-clients:client2              RUNNING    pid 25631, uptime 1 day, 13:00:47
    zeo-cluster:zeoserver            RUNNING    pid 4806, uptime 1 day, 21:40:03
    supervisor> 

El comando ``supervisorctl`` es también un intérprete de comando. 
Para obtener una lista de comando disponible, consulte la 
:ref:`referencia de comando Supervisor <referencias_comandos>`.

.. note:: Al ejecutar por primera vez ``supervisord``, tendrá que 
    esperar algunos minutos a que todos los subprocesos terminen de
    arrancar. A esto se le llama *warm up time*. Durante el *warm up 
    time* se podrán recibir diferentes mensajes de error en los 
    diferentes componentes. Esto es normal.

Para finalizar debe aplicar las configuraciones para Nginx y Munin 
con el siguiente comando: 

.. code-block:: sh

  $ sudo ./bin/update-so-config-sh

De esta forma ya puede acceder a su servidor Web por la dirección URL http://SU_DIRECCION_IP/
