.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _python_27:

Python 2.7
==========

La versión de Plone 4.3.x requiere como dependencia **obligatoria** 
el interprete Python 2.7. Debido a que Python 2.7 `esta disponible`_ 
en sistema de paquetes :ref:`Debian GNU/Linux 7 <debian7>`, se recomienda 
solo instalar algunas herramientas necesarias para esta instalación.

Antes de compilar Python 2.7 requiere haber instalado las 
:ref:`dependencias base <requerimientos_base>` mas las siguientes dependencias:

.. code-block:: console
 
    $ sudo apt-get install python-pip python-setuptools

Prueba del interprete
---------------------

Verifique que tenga soporte a Python 2.7, de la siguiente manera:

.. code-block:: sh
 
    $ python2.7 --version
    Python 2.7.3

De esta forma tiene instalado su Python versión 2.7.x.

----

.. _entornos_virtuales_python:

Entornos virtuales de Python locales al usuario
===============================================

.. _por_que_virtualenv:

¿Por que crear entornos virtuales en Python?
--------------------------------------------

Si usted está en un sistema Linux, BSD, Cygwin, u otros similares 
a Unix como sistema operativo, pero no tienen acceso al usuario root, 
puede crear su propio entorno virtual (instalación) Python, que utiliza 
su propia biblioteca de directorios y algunos enlaces simbólicos hacia 
todo el directorio de instalación del Python de su sistema.

.. _que_es_virtualenv:

¿Qué es virtualenv?
-------------------

`virtualenv`_, es una herramienta para crear entornos virtuales (aislados) 
en Python.

Para evitar usar la instalación base del Python de tu sistema, que
previamente tiene instalada, se recomienda instalar un entorno de 
virtual de Python local al usuario, algunos casos de usos para 
``virtualenv``, se describe a continuación:

-   No es necesarios permisos de administración para instalar librerías y
    aplicaciones Python, ya que estas se hace locales en al directorio del
    usuario.

-   Mayor comodidad de trabajar con versiones de librerías y aplicaciones
    más actuales las que maneja tu versión de tu interprete Python y 
    sistema operativo.


.. _por_que_virtualenv_plone:

¿Por que usar entornos virtuales con Plone?
-------------------------------------------

La razón principal es aislar el entorno de trabajo de Plone del Python 
instalado previamente, eso se debe a que con las herramientas de gestión 
de :term:`paquetes Egg` Python como ``easy_install`` o ``pip`` puede 
instalar :term:`paquetes Egg` que afecten al Python que requerimos con Plone.

Si por cualquier error humano instalo un :term:`paquete Egg` que dañe el 
Python instalado para Plone, tendría que detener el servicio y tratar de 
resolver manualmente las dependencias, esto es critico para un servidor 
en producción.

En cambio, si realiza instalaciones de :term:`paquetes Egg` dentro de un 
entorno virtual y por cualquier error humano instala un :term:`paquete Egg` 
y este quede mal instalado o afecte el normal funcionamiento de Plone, usted 
puede eliminar este entorno virtual y recrear otro como se describe en la 
sección :ref:`Crear el entorno virtual <creando_virtualenv>`, adicionalmente 
de instalar de nuevo todas los :term:`paquetes Egg` requeridos por la 
instalación Plone.

Como puede apreciar es una forma de garantizar que cada instalación no afecte 
a otra.

Instalación
-----------

Prepare su entorno virtual, ejecute los siguientes comando:

.. code-block:: console
 
    $ sudo easy_install-2.7 virtualenv
    
.. _creando_virtualenv:

Crear el entorno virtual
------------------------

Para crear el entorno virtual local al usuario, ejecutando el siguiente
comando: 

.. code-block:: console

    $ cd $HOME ; mkdir virtualenv; cd virtualenv
    $ virtualenv python2.7

.. _activar_virtualenv:

Activar el entorno virtual
--------------------------

Luego de crear el entorno virtual previamente es necesario **activarlo**, 
para esto ejecute el siguiente comando: 

.. code-block:: sh

    $ source $HOME/virtualenv/python2.7/bin/activate
    
Solo es necesario activar el entorno cada ves que requiere instalar un 
:term:`paquete Egg` ``Python``, usando las herramientas como ``easy_install``, 
``pip`` o la forma tradicional ``python setup.py install``.

.. note::

  Cada ves que necesite trabajar dentro del entorno virtual necesita 
  activar este mismo.
  

Desactivar el entorno virtual
-----------------------------

Cuando termine de usar el entorno virtual puede desactivarlo de la siguiente
forma: 

.. code-block:: sh

    $ deactivate

De esta forma ya puedes realizar operaciones de shell fuera del entorno virtual.

.. note::

  Cada ves que necesite salirse del entorno virtual necesita desactivar este mismo.

.. _virtualenv: http://pypi.python.org/pypi/virtualenv/
.. _esta disponible: http://packages.debian.org/wheesy/python2.7
