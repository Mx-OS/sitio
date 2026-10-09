---
title: "Nace la red comunitaria de espejos de software libre sobre IPFS"
date: 2026-10-08T22:00:00-06:00
author: "Rénich Bon Ćirić y Gemini AI"
description: "Presentamos la iniciativa de espejos descentralizados de la Fundación MxOS, distribuyendo paquetes de Fedora y CentOS Stream 10 mediante IPFS y DNSLink para fortalecer la soberanía tecnológica en México."
cover: cover.jpg
---

Hoy damos un paso trascendental en la construcción de infraestructura digital soberana para México y Latinoamérica: inauguramos la red comunitaria de espejos de software libre de la Fundación MxOS sobre el Sistema de Archivos Interplanetario (IPFS), accesible bajo el dominio canónico `mirrors.mx-os.mx <https://mirrors.mx-os.mx>`_.

El problema de la centralización y la lejanía
=============================================
Durante décadas, los usuarios, universidades y centros de desarrollo en nuestra región han padecido una desventaja estructural al instalar y actualizar distribuciones de software libre. En México, la ausencia histórica de un espejo primario local para distribuciones clave como Fedora o CentOS Stream obliga a que cada paquete, imagen ISO y actualización descargada viaje a través de enlaces internacionales hacia servidores en Estados Unidos.

Esta dependencia genera latencia innecesaria, congestión de ancho de banda y una vulnerabilidad crítica ante contingencias de conectividad transfronteriza. La solución tradicional suele ser costosa: adquirir servidores dedicados de alto rendimiento en centros de datos con ancho de banda sobredimensionado y pagar tarifas exorbitantes por transferencia de datos saliente.

Un nuevo paradigma: Espejos de guerrilla sobre IPFS
===================================================
En la Fundación MxOS decidimos replantear el problema desde la raíz. En lugar de levantar un único servidor central vulnerable y costoso, diseñamos una arquitectura basada en IPFS que transforma la distribución de software en un esfuerzo cooperativo y distribuido:

1. **Direccionamiento por contenido inmutable:** Cada paquete RPM y metadato se divide en bloques criptográficos únicos (CIDs). Si dos versiones o distribuciones comparten archivos idénticos, estos se deduplican automáticamente.
2. **Distribución entre pares con Bitswap:** Al actualizar tu sistema con DNF apuntando a tu nodo local de IPFS (puerto 8080), los paquetes se descargan simultáneamente de todos los nodos guardianes disponibles en la red local o internet. Si un compañero de oficina o un vecino de red ya descargó una actualización, tu equipo la obtendrá a la velocidad del cable local sin salir a internet.
3. **Puntero mutable canónico mediante DNSLink:** Gracias al estándar DNSLink (``_dnslink.mirrors.mx-os.mx``), los clientes resuelven siempre el árbol de paquetes más reciente sin preocuparse por los hashes cambiantes de cada sincronización.
4. **Puente HTTP público y compatible:** Para quienes aún no ejecutan un nodo IPFS, implementamos un terminador web de alto rendimiento en ``https://mirrors.mx-os.mx/`` que conecta directamente con el enjambre, permitiendo el uso convencional de DNF y abriendo la puerta a la federación oficial en Fedora MirrorManager.

Modo guerrilla y fase experimental
==================================
Queremos ser transparentes con la comunidad: esta iniciativa arranca en **fase de experimentación activa**.

No contamos aún con patrocinio de centro de datos ni conectividad comercial para albergar servidores de producción masivos, por lo que estamos apostando por una auténtica arquitectura de guerrilla: la ingesta inicial y el almacenamiento residen en nuestras propias estaciones de trabajo y discos de respaldo locales, mientras que nuestro servidor público (``web0.mx-os.mx``) opera estrictamente como una pasarela efímera de retransmisión (gateway) con cuota mínima de 1 GB y recolección de basura continua, evitando comprometer los servicios existentes de la fundación como Forgejo.

El verdadero valor de este esquema reside en el enjambre: conforme más integrantes de la comunidad se sumen como nodos guardianes, más veloz, distribuida e indestructible será la red para toda la región.

Convocatoria: Conviértete en un nodo guardián
==============================================
La fortaleza de esta red radica enteramente en su comunidad. Invitamos a entusiastas, administradores de sistemas, universidades y empresas a donar una porción de su almacenamiento local y convertirse en **nodos guardianes** de la red MxOS.

Para facilitar la adopción, hemos empaquetado el demonio Kubo para Fedora y CentOS Stream en nuestro repositorio oficial de Copr:

.. code-block:: bash

   sudo dnf copr enable renich/kubo
   sudo dnf install kubo
   ipfs init
   systemctl --user enable --now ipfs.service

Pineo granular por cuota de disco
---------------------------------
No es necesario donar cientos de gigabytes; hemos estructurado el catálogo para que puedas respaldar ramas específicas según tu capacidad disponible:

* **Nivel 1: Imágenes ISO de Fedora (~15 GB)**

  .. code-block:: bash

     ipfs pin add /ipns/mirrors.mx-os.mx/fedora/iso

* **Nivel 2: Sistema Base de CentOS Stream 10 (~15 GB)**

  .. code-block:: bash

     ipfs pin add /ipns/mirrors.mx-os.mx/centos-stream/10-stream/BaseOS

* **Nivel 3: Paquetería completa Everything y AppStream (~80 a 150 GB)**

  .. code-block:: bash

     ipfs pin add /ipns/mirrors.mx-os.mx/fedora/releases/43/Everything
     ipfs pin add /ipns/mirrors.mx-os.mx/centos-stream/10-stream/AppStream

* **Nivel 4: Espejo maestro completo (~300 GB)**

  .. code-block:: bash

     ipfs pin add /ipns/mirrors.mx-os.mx

Consumo nativo desde tu equipo
==============================
Si deseas acelerar tus instalaciones locales, solo debes configurar un archivo de repositorio en ``/etc/yum.repos.d/fedora-mxos-ipfs.repo`` apuntando a tu gateway local:

.. code-block:: ini

   [fedora-mxos-ipfs]
   name=Fedora $releasever - $basearch (Espejo MxOS IPFS)
   baseurl=http://127.0.0.1:8080/ipns/mirrors.mx-os.mx/fedora/releases/$releasever/Everything/$basearch/os/
   enabled=1
   metadata_expire=6h
   gpgcheck=1
   gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-$releasever-$basearch

La seguridad criptográfica es absoluta: aunque los bloques viajen por pares comunitarios, DNF verifica obligatoriamente las firmas GPG oficiales del proyecto Fedora y CentOS contra las llaves públicas de tu sistema.

Soberanía técnica paso a paso
=============================
Toda la documentación técnica, especificaciones arquitectónicas, guías para operadores y herramientas de automatización están abiertas y disponibles en nuestro repositorio de `git.mx-os.mx <https://git.mx-os.mx/mxos/mirrors>`_ y en el manual público de `mirrors.mx-os.mx/README.rst <https://mirrors.mx-os.mx/README.rst>`_.

Los invitamos a sumarse a la conversación y coordinar el enjambre en nuestro canal de `Telegram <https://t.me/mx_os_mx>`_.

¡Construyamos juntos la infraestructura soberana de software libre para nuestra región!
