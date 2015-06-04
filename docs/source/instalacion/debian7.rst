.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _debian7:

Debian GNU/Linux 7
==================

Para instalar Plone 4.3.x en entornos de servidores usando 
el sistema operativo `Debian GNU/Linux 7`_, debe ejecutar 
los siguientes pasos con sus respectivos comandos a continuación:

.. _create_user:

Usuario efectivo
----------------

Zope y Plone requiere un `usuario efectivo`_ que ejecute sus servicios, 
debe crear un usuario llamado ``plone`` con una contraseña aleatoria 
generada por la utilidad ``mkpasswd``, con el siguiente comando:

.. code-block:: bash

    # adduser plone sudo

Luego inicie sesión con el usuario ``plone`` y la contraseña elegida, 
con el siguiente comando:

.. code-block:: bash

    # su plone

.. _upgrade_base:

Actualizaciones de seguridad
----------------------------

Primero, instale las últimas actualizaciones del *Debian GNU/Linux 7*, 
con el siguiente comando:

.. code-block:: bash

    $ sudo apt-get update
    $ sudo apt-get upgrade

.. _requerimientos_base:

Requerimientos base
-------------------

Se requiere instalar una serie de dependencias para el proceso de compilación, 
instalación y configuración de algunas dependencias de Plone 4.3.x, para esto 
debe ejecutar el siguiente comando:

.. code-block:: bash

    $ sudo apt-get install gcc g++ make tar unzip bzip2 libssl-dev libxml2-dev \
                   zlib1g-dev libjpeg62-dev libreadline6-dev readline-common wv \
                   xpdf-utils python2.7-dev libxslt1-dev

.. _requerimientos_instalacion_cliente_ldap:

Instalación de Cliente LDAP
---------------------------

Se requiere instalar el cliente para el servidor LDAP, para esto debe ejecutar 
el siguiente comando:

.. code-block:: bash
 
    $ sudo apt-get install python-ldap libsasl2-dev libldap2-dev

.. _requerimientos_instalacion_cvs:

Instalar control de versiones
-----------------------------

Para esta instalación se requiere el sistema de control de versiones Git, para 
esto debe ejecutar el siguiente comando:

.. code-block:: bash
 
    $ sudo apt-get install git etckeeper

git
    Es un sistema de control de versiones popular diseñado para manejar 
    proyectos muy grandes con velocidad y eficiencia; que se utiliza 
    para muchos proyectos de código abierto de alto perfil, la mayoría
    en particular el núcleo de Linux.

    Git cae en la categoría de herramientas de gestión de código fuente 
    distribuido. Cada directorio de trabajo Git es un repositorio de 
    pleno derecho con seguimiento revisión completa capacidades, que no 
    dependen de acceso a la red o en un servidor central.

etckeeper
    Es una herramienta para dejar el directorio :file:`/etc` almacenado en 
    un repositorio git, mercurial, bzr o darcs. Este hooks dentro de APT hace 
    de forma automática commits con cambios hecho al directorio :file:`/etc` 
    durante las actualizaciones de paquetes.

    Ese sigue la metadata del archivo que el sistema de control de versión no 
    soporta normalmente, pero eso es importante para el directorio :file:`/etc`, 
    como los permisos de :file:`/etc/shadow`. Este es modular y configurable, 
    mientras a su ves es simple de usar si usted entiende los conceptos básicos 
    de trabajar el con sistema de control de versión.

.. tip:: 
    Opcionalmente puede instalar el control de versiones *Subversion*, para esto 
    debe ejecutar el siguiente comando:

    .. code-block:: bash
     
        $ sudo apt-get install subversion

.. _requerimientos_instalacion_nginx:

Instalación de Nginx
--------------------
Se requiere instalar el :ref:`servidor Web Nginx <nginx_setup>`, para esto debe 
ejecutar el siguiente comando:

.. code-block:: console
 
    $ sudo apt-get install nginx-extras

.. _requerimientos_instalacion_consumo_recursos:

Herramientas de monitoreo
-------------------------

Se requiere instalar algunas utilidades para el monitoreo de 
:ref:`consumo de recursos <consumo_recursos>`, para esto debe 
ejecutar el siguiente comando:

.. code-block:: console
 
    $ sudo apt-get install iotop htop

.. _requerimientos_instalacion_munin:

Instalación de Munin
--------------------

Se requiere instalar el :ref:`servicio de monitoreo Munin <munin_setup>`, para esto debe 
ejecutar el siguiente comando:

.. code-block:: console
 
    $ sudo apt-get install munin munin-node
    $ sudo apt-get install curl socat coreutils libwww-perl #Haproxy munin plugins

.. _Debian GNU/Linux 7: http://es.wikipedia.org/wiki/Debian_GNU/Linux
.. _usuario efectivo: https://plone-spanish-docs.readthedocs.org/es/latest/instalacion/instalando_plone.html#instalacion-como-root-o-usuario-normal