.. -*- coding: utf-8 -*-

.. highlight:: rest

.. _depuracion_website:

======================
Depuración de procesos
======================

En está sección se describe las diversas utilidades de depuración del sistema sobre 
este sistema en entornos de producción.

.. tip:: 
    Cada comando se ejecuta en una consola distinta, antes de iniciar los procesos 
    de cada servicio que desea depurar.

.. _consumo_recursos:

Consumo de recursos
===================

Mientras tiene los servicios ejecutándose en modo depuración o monitorizando 
los registro de eventos puede apoyarse con otras herramientas que analicen 
el consumo de recursos de hardware, como las siguientes:

.. _consumo_io:

Consumo de I/O
--------------

Para analizar posibles errores de I/O, use el comando :command:`iotop` con 
el siguiente comando:

.. code-block:: sh

  $ sudo iotop -o

.. _consumo_cpu:

Consumo de CPU
--------------

Para analizar el consumo de CPU por procesador, use el comando :command:`htop` con
el siguiente comando:

.. code-block:: sh

  $ htop -u plone

.. warning:: 
   El usuario **plone** es un demostrativo para esta instalación de este documento. 
   Usted debe remplazarlo con el usuario con el cual esta realizando esta instalación.

.. _consumo_ram:

Consumo de RAM
--------------

Para analizar el consumo de RAM por proceso ejecutado, use el comando :command:`htop` con
el siguiente comando:

.. code-block:: sh

  $ htop -u plone

.. warning:: 
   El usuario **plone** es un demostrativo para esta instalación de este documento. 
   Usted debe remplazarlo con el usuario con el cual esta realizando esta instalación.

.. _depuracion_servidor_zeo:

Depuración de servidor Zeo
==========================

Inicie manualmente el :ref:`servidor Zeo <servidor_zeo>`, con el siguiente comando:

.. code-block:: sh

  $ ./bin/zeoserver fg

.. tip::
    Cada comando se ejecuta en una consola distinta, así poder monitorear cualquier
    evento o novedad del servicio.

También puede iniciarlo bajo la administración del servicio de :ref:`Supervisor <que_es_supervisor>`, 
sin modo depuración con el siguiente comando: 

.. code-block:: sh

  $ ./bin/supervisorctl start zeo-cluster:zeoserver

Verifique el registro de eventos del :ref:`servidor Zeo <servidor_zeo>`, con el siguiente comando:

.. code-block:: sh

  $ tail -f ./var/log/zeoserver.log

.. _depuracion_clientes_zeo:

Depuración de clientes Zeo
==========================

Inicie manualmente el :ref:`cliente Zeo 1 <clientes_zeo>`, con el siguiente comando:

.. code-block:: sh

  $ ./bin/client1 fg

También puede iniciarlo bajo la administración del servicio de :ref:`Supervisor <que_es_supervisor>`, 
sin modo depuración con el siguiente comando: 

.. code-block:: sh

  $ ./bin/supervisorctl start zeo-clients:client1

Verifique el registro de eventos del :ref:`cliente Zeo 1 <clientes_zeo>`, con el siguiente comando:

.. code-block:: sh

  $ tail -f ./var/client1/event.log

Verifique el registro de acceso del :ref:`cliente Zeo 1 <clientes_zeo>`, con el siguiente comando:

.. code-block:: sh

  $ tail -f ./var/client1/Z2.log

Este procedimiento es repetible para cada :ref:`cliente Zeo <clientes_zeo>` como se muestra a continuación:

.. code-block:: sh

  $ ./bin/client2 fg
  $ tail -f ./var/client2/event.log
  $ tail -f ./var/client2/Z2.log

.. tip::
    Cada comando se ejecuta en una consola distinta, así poder monitorear cualquier evento
    o novedad del servicio.

.. _depuracion_balanceo_carga:

Depuración de balanceo de carga
===============================

Para depurar :ref:`HAProxy <que_es_haproxy>` asegúrese que el demonio este iniciado manualmente, 
con el siguiente comando:

.. code-block:: sh

  $ ./bin/haproxy -f /home/plone/sitioweb/etc/haproxy.conf -db

También puede iniciarlo bajo la administración del servicio de :ref:`Supervisor <que_es_supervisor>`, 
sin modo depuración con el siguiente comando: 

.. code-block:: sh

  $ ./bin/supervisorctl start others:haproxy

Verifique el registro de eventos de :ref:`HAProxy <que_es_haproxy>` generado por 
:ref:`Supervisor <que_es_supervisor>`, con el siguiente comando:

.. code-block:: sh

  $ tail -f /home/plone/sitioweb/var/log/haproxy-stderr---supervisor-XXdWqF.log

Verifique el registro de errores de :ref:`HAProxy <que_es_haproxy>` generado por 
:ref:`Supervisor <que_es_supervisor>`, con el siguiente comando:

.. code-block:: sh

  $ tail -f /home/plone/sitioweb/var/log/haproxy-stdout---supervisor-qHyow2.log

.. tip:: Cada comando se ejecuta en una consola distinta, así poder monitorear cualquier evento o novedad del servicio.

.. _depuracion_motor_cache:

Depuración de motor caché
==========================

Para depurar :ref:`Varnish <que_es_varnish>` asegúrese que el demonio este iniciado manualmente, 
con el siguiente comando:

.. code-block:: sh

  $ ./bin/varnish

También puede iniciarlo bajo la administración del servicio de :ref:`Supervisor <que_es_supervisor>`, 
sin modo depuración con el siguiente comando: 

.. code-block:: sh

  $ ./bin/supervisorctl start others:varnish

Luego puede iniciar el script ``varnishlog`` que le permitirá ver detalle de 
las operaciones del servicio de :ref:`Varnish <que_es_varnish>`, con el siguiente comando:

.. code-block:: sh

  $ ./bin/varnishlog

.. tip:: Cada comando se ejecuta en una consola distinta, así poder monitorear cualquier evento o novedad del servicio.

.. _depuracion_servidor_web:

Depuración de servidor web
==========================

Verifique si su configuración :ref:`Nginx <nginx_setup>` es correcta, con el siguiente comando:

.. code-block:: sh

  $ sudo nginx -t

Verifique el registro de acceso del virtual host ``preview.canaima.net.ve``, con 
el siguiente comando:

.. code-block:: sh

  $ tail -f /var/log/nginx/preview.canaima.net.ve.access.log;

Verifique el registro de eventos del virtual host ``preview.canaima.net.ve``, con 
el siguiente comando:

.. code-block:: sh

  $ tail -f /var/log/nginx/preview.canaima.net.ve.error.log;

.. tip::
    Cada comando se ejecuta en una consola distinta, así poder monitorear cualquier
    evento o novedad del servicio.

.. _depuracion_monitoreo:

Depuración del monitoreo
=========================

Reinicie los servicios de :command:`munin` y :command:`munin-node` y a su ves 
revise los registro de eventos de :command:`munin-node` y de la generación de 
gráficos, con el siguiente comando:

.. code-block:: sh

  $ sudo service munin restart
  $ sudo service munin-node restart

Verifique el registro de eventos del servicio :command:`munin-node`, con
el siguiente comando:

.. code-block:: sh

  $ sudo tail -f /var/log/munin/munin-node.log

Verifique el registro de eventos de la generación de gráficos, con el siguiente 
comando:

.. code-block:: sh

  $ sudo tail -f /var/log/munin/munin-graph.log

.. tip::
    Cada comando se ejecuta en una consola distinta, así poder monitorear cualquier
    evento o novedad del servicio.

De esta forma puedes hacer depuración de los procesos de cada servicio orquestado 
en la diversas capas de software utilizados.

----

.. _peticiones_http:

Peticiones HTTP
===============

Ya que tenemos un pilas de Software que deben estar orquestada en conjunto para su 
correcto funcionamiento.

`HTTPie`_, es un cliente HTTP de linea de comando como la famosa herramienta `cURL`_, 
haciendo mas amigable e humana la interacción con la linea de comando con los servicios Web.

Esta herramienta se recomienda usarla para probar, depurar y generalmente interactuar 
con el stack de servicios y su publicación hacia la Web mediante HTTP.

Para instalarla ejecute el siguiente comando: 

.. code-block:: sh

  $ sudo pip install httpie

Patrón de pruebas
-----------------

Primero pruebe el servicio :ref:`Nginx <nginx_setup>` con el siguiente comando: 

.. code-block:: sh

  $ http -phH GET http://127.0.0.1:80

Seguidamente pruebe el servicio :ref:`Varnish <que_es_varnish>` con el siguiente comando: 

.. code-block:: sh

  $ http -phH GET http://127.0.0.1:8101
  
Opcionalmente puede mostrar la respuesta completa de la petición hecha previamente con el 
siguiente comando:

.. code-block:: sh

  $ http GET http://127.0.0.1:8101

Pruebe el servicio :ref:`HAProxy <que_es_haproxy>` con el siguiente comando: 

.. code-block:: sh

  $ http -phH GET http://127.0.0.1:8201
  $ http GET http://127.0.0.1:8201

Pruebe el servicio :ref:`Servidor Zeo <servidor_zeo>`, con el siguiente comando:

.. code-block:: sh

  $ http -phH GET http://127.0.0.1:8009
  $ http GET http://127.0.0.1:8009

Pruebe el servicio de los diversos :ref:`clientes Zeo <clientes_zeo>` que tiene
creadas, en este caso dos (02), con los siguientes comandos:

.. code-block:: sh

  $ http -phH GET http://127.0.0.1:8080/
  $ http -phH GET http://127.0.0.1:8004/

.. note::
    Opcionalmente puede probar el servicio del *cliente Zeo de depuración*, 
    con los siguientes comandos:

    .. code-block:: sh

      $ http -phH GET http://127.0.0.1:8008
      $ http GET http://127.0.0.1:8008

Por ultimo pruebe el servicio de :ref:`supervisor <que_es_supervisor>`, con los 
siguientes comandos:

.. code-block:: sh

  $ http -phH GET http://127.0.0.1:9001
  $ http GET http://127.0.0.1:9001

.. _HTTPie: https://pypi.python.org/pypi/httpie
.. _cURL: http://es.wikipedia.org/wiki/CURL
