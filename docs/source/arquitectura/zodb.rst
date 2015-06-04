.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _que_es_zodb:

===========================
Zope Object Database - ZODB
===========================

.. sidebar:: Sobre este artículo

    :Autor(es): Leonardo J. Caballero G.
    :Correo(s): leonardoc@plone.org
    :Compatible con: Plone 3.x, Plone 4.x
    :Fecha: 23 de Marzo de 2015

La Zope Object Database (ZODB) es una base de datos orientada a objetos 
para almacenar de forma transparente y persistente objetos en el lenguaje 
de programación Python. Se incluye como parte de Zope, un Servidor de 
aplicaciones Web, pero también puede ser utilizado independientemente de Zope.

Características
===============

Las características de la ZODB se incluyen: 

- Transacciones.

- Historial / deshacer.

- Almacenamiento conectable de forma transparente.

- Almacenamiento en caché.

- Control de concurrencia multiversión (multiversion concurrency control - MVCC).

- Escalabilidad a través de una red (usando :ref:`ZEO <que_es_zeo>`).

Historia
========

-  Creado por `Jim Fulton <http://www.zope.com/about_us/management/james_fulton.html>`_ de 
   `Zope Corporation <http://es.wikipedia.org/wiki/Zope#Zope_Corporation>`_ a finales de los años 90.

-  Inicio como un simple sistema de `persistencia de
   Objetos <https://es.wikipedia.org/wiki/Persistencia_de_objetos>`_ (Persistent Object System -
   POS) durante el desarrollo de Principia (el cual posteriormente sería
   Zope).

-  ZODB 3 fue renombrada cuando un cambio significante de la
   arquitectura fue publicado.

-  ZODB 4 fue un proyecto de corta duración para volver a poner
   re-implementar todo el paquete de ZODB 3 usando 100% Python.

.. _que_es_zeo:

ZEO
===

ZEO *(Zope Enterprise Objects)*, es una implementación de almacenamiento de 
ZODB que permite varios procesos de clientes a la `persistencia de
objetos <https://es.wikipedia.org/wiki/Persistencia_de_objetos>`_ en un único servidor ZEO. Esto
permite la escalabilidad transparente, pero el servidor ZEO es todavía
un punto único de fallo.

.. _conector_almacenamiento:

Almacenes de datos basado en conectores
=======================================

-  `FileStorage <http://docs.zope.org/zope2/zdgbook/ZODBPersistentComponents.html>`_
   - Permite que un único proceso de Python para hablar con un archivo
   en el disco.
   
-  `BlobStorage <https://pypi.python.org/pypi/plone.app.blob>`_ -
   Permite a los grandes datos binarios ser gestionado por la ZODB, pero
   separado de su habitual base de datos *FileStorage*, es decir
   :file:`Data.fs`. Esto tiene varias ventajas, la más importante un archivo
   :file:`Data.fs` mucho más pequeños y un mejor rendimiento tanto en CPU,
   así como de la memoria.

-  `RelStorage <https://pypi.python.org/pypi/RelStorage>`_ - Permite el
   almacenamiento de respaldo persistencia para ser un
   `RDBMS <https://es.wikipedia.org/wiki/RDBMS>`_.

-  :ref:`NetworkStorage <que_es_zeo>` (también conocido como
   :ref:`ZEO <que_es_zeo>`) - Permite cargar varios procesos de Python y
   almacenar instancias persistentes al mismo tiempo.

-  `DirectoryStorage <http://dirstorage.sourceforge.net/>`_ - Cada dato
   persistente se almacena como un archivo separado en el sistema de
   archivos. Al igual que en FSFS en `Subversion`_.

-  `DemoStorage <http://docs.zope.org/zope3/Code/ZODB/DemoStorage/index.html>`_
   - Un fondo en memoria para el almacenamiento persistente. Proporcione
   un ejemplo de implementación de un almacenamiento completo sin
   distraer información acerca del almacenamiento, este tipo de
   almacenamiento es volátil lo cual es útil para dar demostraciones.

-  BDBStorage - que utiliza `Berkeley DB <https://es.wikipedia.org/wiki/Berkeley_DB>`_ back-end.
   Ahora abandonada.

Tecnologías de conmutación por error
====================================

-  `Servicios de replicación de Zope (ZRS) <https://pypi.python.org/pypi/zc.zrs>`_ 
   Es un producto que elimina el punto único de fallo, proporcionando copia de seguridad 
   en caliente de las escrituras y lecturas de balanceo de carga.

-  `ZEORaid <https://pypi.python.org/pypi/gocept.zeoraid>`_, es una
   solución de código abierto que proporciona un servidor proxy de red
   que distribuye el almacenamiento de objetos y la recuperación a
   través de una serie de servidores de red.

-  `RelStorage <https://pypi.python.org/pypi/RelStorage>`_, usa las
   tecnologías de `RDBMS <https://es.wikipedia.org/wiki/RDBMS>`_ así de esta 
   forma se evitas la necesidad de servidor :ref:`ZEO <que_es_zeo>`.

-  NEO - Distribuido (tolerancia a fallos, equilibrio de carga) la
   aplicación de almacenamiento. No está listo para su uso en producción
   todavía (a partir de 01/2011).

.. _directorios_zodb:

Directorios de ZODB
===================

La instalación de instancia Plone contendrá un directorio :file:`./var`
(en el mismo directorio donde esta el archivo :file:`buildout.cfg`) que
contiene los archivos de datos que cambian con frecuencia para la instancia.
Gran parte de lo que hay en el directorio :file:`./var`, sin embargo, no es
su base de datos de contenido real, más bien, contiene los archivos de registro,
identificación del proceso y socket.

La ZODB se ubica en varios directorios dependiendo de la
:ref:`estrategia de almacenamiento <conector_almacenamiento>`
usada, a continuación se describen las configuraciones por 
defecto estiladas a usar en Plone.

Los directorios que contienen realmente datos de contenido son:

Directorio filestorage
----------------------

En el directorio por defecto la ZODB se encuentran :file:`var/filestorage/`
en el cual contiene los siguientes archivos:

- El archivo :file:`Data.fs` es la base de datos como tal.

- El archivo :file:`Data.fs.lock` es para señalar que :file:`Data.fs` esta en uso.

- El archivo :file:`Data.fs.index` guarda una copia del índice.

- El archivo :file:`Data.fs.tmp` se usa para operaciones como `compactación`_.

- El archivo :file:`Data.fs.old` es un respaldo exacto de la ZODB generada automáticamente por
  tareas de `compactación`_ o `la actualización de catalogo`_.

.. note::
    Los otros archivos en :file:`var/filestorage/`, con extensiones como *.index*, *.lock*,
    *.tmp* son efímeros, y se volverán a crear por Zope si están ausentes.
    
    Solo el archivo  en :file:`var/filestorage/`, con extensión *.old*, se debe respaldar si
    requiere preservar en este directorio este respaldo, solo se genera de nuevo si se ejecuta 
    alguna tarea automática o manual de mantenimiento de la ZODB.

.. tip:: 
    Estos archivos deben ser respaldados a través de tareas de 
    :ref:`copias de seguridad <backup_zodb>`.

Directorio Blobstorage
----------------------

Este directorio contiene una jerarquía de directorios muy profundamente anidado que,
a su vez, contiene los BLOBs de su base de datos: PDFs, archivos de imágenes, archivos
de ofimática y entre otros.

.. tip:: 
    La clave sobre **filestorage** y **blobstorage** es que se mantengan de forma sincrónica.
    El **filestorage** tiene referencias a blobs en el directorio **blobstorage**. Si los dos
    estrategias de almacenamiento no están perfectamente sincronizados, obtendrá errores.

Desde la versión 4.0 en Plone los (*Binary large objects - Blob*) se almacenan en el
sistema de archivos. En el directorio por defecto del Blobstorage se encuentran 
:file:`var/blobstorage/`.

.. note:: 
    Este directorio contiene una serie de directorios con imágenes y archivos,
    los cuales puede :ref:`respaldarse con la ZODB <backup_zodb>` o por separado
    usando :program:`rsync` para `sincronizar los directorios`_.

.. _Subversion: http://plone-spanish-docs.readthedocs.org/es/latest/rcs/subversion.html#rcs-subversion
.. _compactación: https://plone-spanish-docs.readthedocs.org/es/latest/zope/zodb/compactar.html#compactar-zodb
.. _la actualización de catalogo: https://plone-spanish-docs.readthedocs.org/es/latest/zope/zodb/actualizar_catalog.html#actualizar-zcatalog
.. _sincronizar los directorios: https://plone-spanish-docs.readthedocs.org/es/latest/zope/zodb/respaldar.html#blob-storages