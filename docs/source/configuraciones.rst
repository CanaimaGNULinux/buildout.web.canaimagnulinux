.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _configuraciones_generales:

Configuraciones generales
=========================

Plone 4 ofrece varios niveles de configuración a continuación 
se describen cada uno:

.. _configuraciones_buildout:

Configuraciones Buildout
------------------------

A continuación se describen las configuraciones de zc.buildout 
obtenidas tras la descarga previa realizada en la sección llamada 
:ref:`Archivos y directorios obtenidos <archivos_directorios_obtenidos>`:

.. glossary::

   ``buildout.d/buildout.cfg.example``
      Esta configuración zc.buildout ofrece una plantilla del 
      archivo ``buildout.cfg`` que puede usar para la construcción 
      del proyecto Plone.

   ``buildout.d/base.cfg``
      Esta configuración zc.buildout define las extensiones básicas 
      para la construcción del proyecto, además de la inclusión del 
      perfil de instalación básico de Plone 4.3.4.

   ``buildout.d/base-versions.cfg``
      Esta configuración zc.buildout se extiende de la configuración 
      ``base.cfg``, la cual define el conjunto de versiones de paquetes 
      a usar para la construcción.

   ``buildout.d/plone-4.3.4.cfg``
      Esta configuración zc.buildout define como construir un Plone 4.3.4.

   ``buildout.d/plone-4.3.4-versions.cfg``
      Esta configuración zc.buildout se extiende de la configuración 
      ``plone-4.3.4.cfg``, la cual define el conjunto de versiones de 
      paquetes a usar para la construcción.

   ``buildout.d/hotfix.cfg``
      Esta configuración zc.buildout define los paquetes y las versiones 
      actualizaciones de seguridad de la Plone.

   ``buildout.d/development.cfg``
      Esta configuración zc.buildout define todas las tareas para construir 
      y ensamblar la Plone con el conjunto de herramientas para entornos de 
      desarrollo.

   ``buildout.d/development-versions.cfg``
      Esta configuración zc.buildout se extiende de la configuración 
      ``development.cfg``, la cual define el conjunto de versiones de 
      paquetes a usar para la construcción.

   ``buildout.d/production.cfg``
      Esta configuración zc.buildout define todas las tareas para construir 
      y ensamblar la Plone con el conjunto de servicios necesario para que esta 
      funcione bajo un esquema de alta disponibilidad.

   ``buildout.d/production-kgv.cfg``
      Esta configuración zc.buildout se extiende de la configuración ``production.cfg``,
      la cual define el conjunto de versiones de paquetes a usar para la construcción.

   ``buildout.d/munin-install.cfg``
      Esta configuración zc.buildout genera las configuraciones de los plugins del servicio 
      :ref:`Munin <que_es_munin>` para los servicios la Plone.

   .. _profile_munin_zope:

   ``buildout.d/munin-zope.cfg``
      Esta configuración zc.buildout genera los plugins de :ref:`Munin <que_es_munin>` para 
      monitorear varios aspectos de Zope usando el paquete ``munin.zope``.
      
   ``buildout.d/munin-plone.cfg``
      Esta configuración zc.buildout genera un plugin de :ref:`Munin <que_es_munin>` para 
      monitorear varios aspectos de Plone usando el paquete ``munin.plone``.

   ``buildout.d/munin-haproxy.cfg``
      Esta configuración zc.buildout genera un plugin de :ref:`Munin <que_es_munin>` 
      llamado ``haproxy_backend`` para monitorear mínimamente 
      :ref:`HAProxy <que_es_haproxy>`.

   ``buildout.d/munin-varnish.cfg``
      Esta configuración zc.buildout genera los plugins de :ref:`Munin <que_es_munin>` para monitorear varios
      aspectos de Zope usando el recipe ``munin.varnish`` para :ref:`Varnish <que_es_varnish>`.

      Este genera los siguientes scripts:

      - **varnish_sitioweb_expunge**, analiza los objetos purgados.

      - **varnish_sitioweb_transfer_rates**, analiza las tasas de transferencia.

      - **varnish_sitioweb_objects**, analiza números de objetos en los encabezados.

      - **varnish_sitioweb_uptime**, analiza el tiempo de funcionamiento al aire del servicio.

      - **varnish_sitioweb_request_rate**, analiza las tasas de peticiones.

      - **varnish_sitioweb_memory_usage**, analiza el uso de memoria.

      - **varnish_sitioweb_hit_rate**, analiza las tasas de Hit.

      - **varnish_sitioweb_threads**, analiza el estatus de Thread.

      - **varnish_sitioweb_backend_traffic**, analiza el trafico del Backend.

   ``buildout.d/munin-nginx.cfg``
      Esta configuración zc.buildout genera un plugin de :ref:`Munin <que_es_munin>` 
      llamado ``nginx_memory`` para monitorear el consumo de memoria de 
      :ref:`Nginx <nginx_setup>`.

   ``buildout.d/checkouts.cfg``
      Esta configuración zc.buildout define los recursos de paquetes eggs en desarrollo 
      que se agregaran al proyecto usando la extensión de zc.buildout llamada ``mr.developer``.
      Esta especifica los nombres de los paquetes los cuales deben ser comprobados durante 
      la ejecución del buildout, los paquetes ya comprobados son esquivados. Usted puede usar * 
      como un comodín para todos los paquetes en la sección ``[sources]``.

   ``buildout.d/sources.cfg``
      Esta configuración zc.buildout le permite definir los origenes de paquetes Egg 
      a usar, los cuales se define en la sección ``[sources].

   ``buildout.d/maintenance.cfg``
      Esta configuración zc.buildout le permite definir tareas de actualización y 
      mantenimiento de Plone.

----

.. _configuraciones_generadas:

Configuraciones generadas
-------------------------

A continuación se describen las configuraciones para los servicios como :ref:`Nginx <nginx_setup>`,
:ref:`Varnish <que_es_varnish>`, :ref:`HAProxy <que_es_haproxy>`, tareas de mantenimiento entre otros
más que fueron generadas tras la construcción del proyecto realizada en la sección llamada 
:ref:`Inicie la construcción <inicio_construccion>`:

.. glossary::
    :sorted:

    ``etc/nginx.conf``
        Contiene las configuraciones para el servicio :ref:`Nginx <nginx_setup>`.

    ``etc/nginx-vhost.conf``
        Contiene las configuraciones para el virtual host de :ref:`Nginx <nginx_setup>`.

    ``etc/varnish.vcl``
        Contiene las configuraciones para el servicio :ref:`Varnish <que_es_varnish>`.
        
    ``etc/haproxy.conf``
        Contiene las configuraciones para el servicio :ref:`HAProxy <que_es_haproxy>`.

    ``etc/logrotate.conf``
        Contiene las configuraciones para rotar los archivos .log usando la herramienta ``logrotate``.

    ``etc/munin-plugin-sitioweb.conf``
        Contiene las configuraciones de los plugins de :ref:`Munin <que_es_munin>` para Plone.
