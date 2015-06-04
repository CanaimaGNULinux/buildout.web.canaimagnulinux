.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _actualizaciones_sistema:

========================
Actualización de sistema
========================

Una tarea recomendable es tener sus sistema informático actualizado con las ultimas versiones 
y actualizaciones de seguridad, para esto se ofrecen los siguientes procedimientos:

Sistema operativo
=================

Cuando requiere actualizar actualizaciones de su sistema operativo *Debian GNU/Linux 7*, 
es necesario realizar cumplir y realizar varios procedimientos, a continuación se describen estos:

#. Requiere disponer de acceso a Internet para descargar las actualizaciones.

#. Para actualizar el sistema operativo requiere ejecutar **SOLAMENTE** los comandos descritos 
   en la sección :ref:`Actualizaciones de seguridad <upgrade_base>`.

.. _portal_migration_setup:

Plataforma Plone
================

Cuando requiere actualizar hacia una versión mas reciente de la instalación 
Plone, es necesario realizar varios procedimientos, a continuación se 
describen estos:

#. Cambiar las versiones de Plone definidas en el archivo ``base.cfg``.

#. Detenga todos los procesos de la Plone con el siguiente 
   comando:

   .. code-block:: sh
   
       $ ./bin/supervisorctl stop all

#. Ejecutar la construcción de la Plone con buildout con el 
   siguiente comando:

   .. code-block:: sh
   
       $ ./bin/buildout -vvvvv

   .. note::
       Este procedimiento se encargara descarga e instalar en sus sistema 
       de archivo las nuevas versiones de Plone que definió en el archivo 
       ``base.cfg``.

#. Inicie :ref:`servidor Zeo <servidor_zeo>` de la Plone con un demonio con el siguiente 
   comando:

   .. code-block:: sh
   
       $ ./bin/zeoserver start

#. Inicie la :ref:`instancia de depuración <clientes_zeo>` de la Plone con el siguiente 
   comando:

   .. code-block:: sh
   
       $ ./bin/client-debug fg

#. Luego acceda a la **Plone Migration Tool** en la ZMI en la siguiente 
   dirección http://SU_DIRECCION_IP:8008/Plone/manage_main

  .. figure:: _static/portal_migration01.png
    :align: center
    :alt: Desde la ZMI el portal_migration indica que requiere actualización

    Desde la ZMI el **portal_migration** indica que requiere actualización.

#. Ya dentro de la herramienta **Plone Migration Tool**, la cual le permite actualizar 
   a nivel de Software sus sitios a nuevas versiones de Plone.

  .. figure:: _static/portal_migration02.png
    :align: center
    :alt: Herramienta Plone Migration Tool

    Herramienta **Plone Migration Tool**.

#. Aquí usted puede hacer clic al botón ``Upgrade`` para realizar las actualización de 
   su sitio a la nueva versión disponible en su sistema. Al finalizar el proceso de la 
   actualización podrá observar la siguiente pantalla:

  .. figure:: _static/portal_migration03.png
    :align: center
    :alt: Mensaje generado por la herramienta portal_migration, luego de la actualización

    Mensaje generado por la herramienta **portal_migration**, luego de la actualización.

Si vuelve a entrar a la herramienta en :menuselection:`Interfaz de Administración de Zope --> portal_migration`, 
notara que no hay actualización disponibles.

  .. figure:: _static/portal_migration04.png
    :align: center
    :alt: portal_migration, indica que no hay actualización disponibles

    **portal_migration**, indica que no hay actualización disponibles.

#.  Para finalizar detenga la instancia de depuración presionado **Crt+C** y seguidamente 
    el :ref:`servidor Zeo <servidor_zeo>` con el siguiente comando:

   .. code-block:: sh
   
       $ ./bin/zeoserver stop

#.  Inicie de nuevo todos los procesos de la Plone con el siguiente 
     comando:

   .. code-block:: sh
   
       $ ./bin/supervisorctl start all

Para mas detalle consulte la herramienta en :menuselection:`Interfaz de Administración de Zope --> portal_migration`.

Documentación de Plone
======================

Para tener actualizada la documentación en linea de la Plone debe 
generar los documentos finales, para esto es necesario ejecutar los siguientes pasos:

   .. code-block:: sh
   
       $ cd docs/ ; make html

Y con esto tendrá disponible la ultima documentación de la Plone en la 
dirección http://preview.canaima.net.ve/docs/
