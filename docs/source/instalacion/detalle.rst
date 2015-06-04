.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _resumen_instalacion:

Detalles de la instalación
==========================

Para instalar Plone en su versión 3.4.3 en entornos de servidores 
usando el sistema operativo :ref:`Debian GNU/Linux 7 <debian7>`, 
debe ejecutar los siguientes pasos con sus respectivos comando a 
continuación:

.. _archivos_directorios_obtenidos:

Archivos y directorios obtenidos
--------------------------------

A continuación se describen los archivos y directorios obtenidos 
tras la descarga previa realizada en la sección llamada 
:ref:`Descargar Plone <obteber_plone>`:

.. glossary::
   :sorted:

   ``docs/``
      El directorio que contiene la documentación de administración de Plone.

   ``etc/``
      El directorio que contiene inicialmente las personalizaciones de los 
      mensajes de error de :ref:`Nginx <nginx_setup>` y :ref:`HAProxy <que_es_haproxy>`, 
      posterior a la construcción del proyecto contendrá las configuraciones 
      de los servicios que construye la instalación Plone.

      .. tip:: 
         Para información detallada de las diversas configuraciones generadas 
         consulte la sección :ref:`Configuraciones generadas <configuraciones_generadas>`.

   ``products/``
      El directorio que contiene todos los productos Zope que requiere la 
      instalación Plone para su correcto funcionamiento.

      .. tip::
         Para información detallada de los productos Zope usando consulte la sección 
         :ref:`Productos Zope / Plone <productos_adicionales>`.

   ``buildout.d/``
      Este directorio contiene todas las configuraciones de zc.buildout necesarias para 
      de la instalación Plone.

      .. tip:: 
          Para información detallada de los perfiles de configuraciones de zc.buildout 
          usados consulte la sección :ref:`Configuraciones Buildout <configuraciones_buildout>` 
          en la instalación Plone.

   ``src/``
      El directorio que contiene los paquetes Egg Python en desarrollo para la instalación Plone.

      .. tip::
         Para información detallada de los paquetes Egg usando consulte la sección 
         :term:`paquetes Egg` Plone.

----

.. _archivos_directorios_arranque:

Archivos y directorios creados al arranque
------------------------------------------

A continuación se describen los archivos y directorios obtenidos tras 
la inicialización del proyecto realizada en la sección llamada 
:ref:`Arranque de construcción <archivos_directorios_buildout_init>`:

.. glossary::
    :sorted:

    ``bin/``
        El directorio de los scripts o ejecutables y producidos 
        por las partes de buildout.

    ``parts/``
        El directorio ``parts`` proporciona un área donde las recetas pueden instalar 
        parte de la datos. Por ejemplo, si usted construye un Python personalizado, 
        usted podrá requerir instalarlo en el directorio ``parts``, entonces para esto 
        definimos una sección llamada ``python-build`` el cual describa como se construye 
        su Python y sus datos se almacenaran en un sub-directorio del directorio ``parts`` 
        con el mismo nombre de la sección.
        
    ``develop-eggs/``
        El directorio hace referencia a los paquetes eggs en desarrollo en el proyecto buildout. 
        Se realiza una distinción de los directorios ``develop-eggs`` del directorio ``eggs`` 
        para permitir compartir los paquetes Egg a través de múltiples proyectos buildout.

    ``bin/buildout``
        El script de zc.buildout, con el cual se gestiona el proyecto :ref:`buildout <que_es_buildout>`.


----

.. _archivos_directorios_construidos:

Archivos y directorios al construir
-----------------------------------

Además de los :ref:`directorios creados al arranque <archivos_directorios_buildout_init>` posterior 
a la :ref:`construcción <inicio_construccion>`, se crearan otros archivos o directorios adicionales, 
los cuales se describen a continuación:

.. glossary::
    :sorted:

    ``bin/backup``
        Es un script que le permite generar :ref:`backup <backup_zodb>` de la :ref:`ZODB <que_es_zodb>` 
        en configurados previamente definidas.

        Este script fue generado por la sección llamada **backup** dentro del perfil de instalación 
        ``maintenance.cfg``, usando la receta ``collective.recipe.backup``.

        .. tip:: 
            Más información sobre los parámetros usados o otros parámetros disponibles consulte la referencia
            la receta en la siguiente dirección http://pypi.python.org/pypi/collective.recipe.backup.

    ``bin/develop``
        Es un script generado por la extensión de buildout llamada **mr.developer** dentro del perfil de instalación ``base.cfg``, el cual es usado para realizar descargas de productos adicionales de Plone o Python Egg en modo de desarrollo.

        .. tip:: 
            Más información sobre los parámetros usados o otros parámetros disponibles consulte la referencia la 
            receta en la siguiente dirección http://pypi.python.org/pypi/mr.developer.

    ``bin/fullbackup``
        Es un script que le permite hacer un :ref:`backup <backup_zodb>` **completo** de la :ref:`ZODB <que_es_zodb>`.

        Este script fue generado por la sección llamada **backup** dentro del perfil de instalación ``maintenance.cfg``, 
        usando la receta ``collective.recipe.backup``.

        .. tip:: Más información sobre los parámetros usados o otros parámetros disponibles consulte la referencia del 
            récipe en la siguiente dirección http://pypi.python.org/pypi/collective.recipe.backup.

    ``bin/snapshotbackup``
        Es un script que le permite hacer un :ref:`backup <backup_zodb>` **completo** de la :ref:`ZODB <que_es_zodb>`, 
        separada de los *backup regulares*, este script le permite hacer copias de la actual base de datos en producción, 
        hacia otra ubicación a salvo, la cual puede ser de mucha utilidad antes de hacer grandes cambios en el sitio.

        Este script fue generado por la sección llamada **backup** dentro del perfil de instalación ``maintenance.cfg``,
        usando la receta ``collective.recipe.backup``.

        .. tip:: Más información sobre los parámetros usados o otros parámetros disponibles consulte la referencia la receta
            en la siguiente dirección http://pypi.python.org/pypi/collective.recipe.backup.

    ``bin/instance``
        Este script fue generado por la sección llamada .instance. dentro del perfil de instalación ``production.cfg``, 
        usando la receta ``plone.recipe.zope2instance``. Esta se usa de la base de la instalación desde la receta Plone 4.3.4
        en el perfil ``plone-4.3.4.cfg``.

        En el perfil ``production.cfg`` sirve como plantilla de los :ref:`clientes Zeo <clientes_zeo>`.

        .. tip:: 
            Más información sobre los parámetros usados o otros parámetros disponibles consulte la referencia de 
            la receta en la siguiente dirección http://pypi.python.org/pypi/plone.recipe.zope2instance

    ``bin/client-debug``
        Es un script de arranque del :ref:`cliente Zeo <clientes_zeo>` en modo de depuración para labores administrativas.

    ``bin/client1``
        Es un script de arranque del :ref:`cliente Zeo 1 <clientes_zeo>`.

    ``bin/client2``
        Es un script de arranque del :ref:`cliente Zeo 2 <clientes_zeo>`.

    ``bin/repozo``
        Es un script de ``repozo``, es una herramienta que puede ser 
        usado para crear un respaldo completo de la :ref:`ZODB <que_es_zodb>`.

    ``bin/restore``
        Es un script para **restaurar** :ref:`backup <backup_zodb>` previamente generados de la :ref:`ZODB <que_es_zodb>`.

        Este script fue generado por la sección llamada **backup** dentro del perfil de instalación ``maintenance.cfg``,
        usando la receta ``collective.recipe.backup``.

        .. tip:: Más información sobre los parámetros usados o otros parámetros disponibles consulte la referencia del
            récipe en la siguiente dirección http://pypi.python.org/pypi/collective.recipe.backup.

    ``bin/zopepy``
        Script para hacer inmersiones interactivas de Python en 
        el contexto de la instalación Zope / Plone.

    ``bin/sitioweb_contentcreation_instance*``
        Script analiza la creación de contenidos dentro del sitio Plone por cada instancia Zope.

    ``bin/sitioweb_zodbactivity_instance*``
        Script analiza la actividad en la :ref:`ZODB <que_es_zodb>` por cada instancia Zope.

    ``bin/sitioweb_zopememory_instance*``
        Script analiza el consumo de memoria de cada instancia Zope.

    ``bin/sitioweb_zopecache_instance*``
        Script analiza cuantos objetos están en la cache de la :ref:`ZODB <que_es_zodb>`.

    ``bin/sitioweb_zopethreads_instance*``
        Script analiza el total de hilos por cada instancia Zope.

    ``bin/haproxy``
        Script que administra el servicio de :ref:`HAProxy <que_es_haproxy>`.

    ``bin/varnish``
        Script que administra el servicio de :ref:`Varnish <que_es_varnish>`.

    ``bin/varnishlog``
        Script que muestra los archivos de registro de eventos del servicio de :ref:`Varnish <que_es_varnish>`.

    ``bin/munin-varnish``
        Script analiza el comportamiento de :ref:`Varnish <que_es_varnish>`.

    ``bin/supervisorctl``
        Script de CLI para administrar :ref:`Supervisor <que_es_supervisor>`.

    ``bin/supervisord``
        Script que inicia el demonio de :ref:`Supervisor <que_es_supervisor>`.

    ``bin/zeopack``
        Script para la tarea de compactación de la :ref:`ZODB <que_es_zodb>`.

    ``bin/zeoserver``
        Script de arranque del :ref:`servidor Zeo <servidor_zeo>`.

    ``eggs/``
        Los paquetes eggs obtenidos e instalados de PyPI.

    ``downloads/``
        Software adicional descargado.

    ``scripts/haproxy_backend``
        Script monitorea mínimamente :ref:`HAProxy <que_es_haproxy>`.

    ``scripts/nginx_memory``
        Script monitorea el consumo de memoria de :ref:`Nginx <nginx_setup>`.

    ``var/``
        Logs y archivo de :ref:`ZODB <que_es_zodb>` de Zope (buildout nunca sobre escribe estos archivos).

    ``var/filestorage``
        Contiene archivos de :ref:`ZODB <que_es_zodb>` de Zope.

        .. tip:: 
           Para información detallada consulte la sección `puntos de montaje de ZODB`_ 
           de su sitio web Plone.
        
    ``var/log``
        Contiene archivos de Logs de Zope tales como ``instance.log`` (archivo de errores) 
        y ``instance-Z2.log`` (archivo de acceso).

.. _pdb: http://docs.python.org/release/2.4/lib/module-pdb.html
.. _puntos de montaje de ZODB: https://plone-spanish-docs.readthedocs.org/es/latest/zope/zodb/index.html#directorios-de-zodb