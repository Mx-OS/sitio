---
title: "Koji"
date: 2025-11-28T07:33:32-06:00
author: Rénich Bon Ćirić
authorTwitter: "renich"
tags:
    - koji
    - infraestructura
cover: 20251126-cover.png
---

Estoy trabajando arduamente en el proyecto de Koji: https://git.mx-os.mx/MxOS/ansible-koji.

¡Nada que ver con Kabuto! Aunque soy fan. :)

Koji es un proyecto muy interesante, pero bastante complejo. Tienen muy buena documentación (https://docs.pagure.org/koji/), pero,
aun así, no me quedaban del todo claros los pasos para lograr un despliegue correcto.

Finalmente, creo tenerlo en orden.

Lo bueno del repositorio es que te permite aprovisionar tu propio Koji localmente (si usas Fedora moderno o CentOS Stream 10).
Usamos `OpenTofu` para generar las máquinas virtuales, tomando una imagen mínima (en CentOS Stream 10) como base y replicándola para
proveer una infraestructura de desarrollo completa.

.. figure:: 20251126-libvirt_con_koji.png
    :alt: Ventana de libvirt mostrando máquinas virtuales apagadas de koji y una imagen base.
    :loading: lazy

    Ventana de `virt-manager` mostrando a los huéspedes (guests) para Koji en el anfitrión (host) local.

La idea es que puedas modificar tu propia versión de nuestro despliegue en caso de que quieras aportar algo, o simplemente usarlo
para fines propios.

El despliegue local realiza varias configuraciones críticas que replican lo que haremos en producción:

CA y certificados auto-firmados
-------------------------------
El playbook de `ansible` genera una CA para firmar nuestros propios certificados: `koji_ca_cert.crt`. Con esto, generamos
certificados para todos los servicios participantes, asegurando que se comuniquen de manera cifrada internamente.

Si quieres confiar en estos certificados en tu equipo local, coloca el certificado CA (`koji_ca_cert.crt`) en:
``/etc/pki/ca-trust/source/anchors/`` y ejecuta el comando ``update-ca-trust`` (como root) para actualizar tu conjunto ("bundle") de certificados.

Cuando ya no quieras confiar en el certificado, simplemente bórralo de esa ruta y vuelve a ejecutar ``update-ca-trust``.

.. note::
   Existe el comando ``trust anchor certs/koji_ca_cert.crt``, pero es más difícil de administrar. Para remover el certificado
   tendrías que usar ``trust anchor --remove='Koji Certificate Authority'`` (o el CN específico), lo cual se vuelve engorroso si no
   tienes claro el origen del certificado. El método manual es más transparente.

   Para ver el CN de un certificado, puedes usar: ``openssl x509 -noout -text -in <ruta_al_certificado>``.

Servicios separados
-------------------
Decidimos integrar los servicios de manera modular desde el principio. No es solo por orden; separar roles nos permite escalar
horizontalmente (añadir más builders sin tocar la DB) y proteger el rendimiento de cada componente.

cs10-koji-00.mx-os:
   El Cerebro: Alberga dos servicios críticos:

   * kojihub: Es el centro de operaciones. Toda comunicación (CLI, Web, Builders) pasa por aquí mediante XML-RPC. Es "stateless", lo
     que significa que depende totalmente de la base de datos y el sistema de archivos.
   * kojira: Es el encargado de mantener el orden. Regenera los repositorios `yum`/`dnf` internos cada vez que se construye un
     paquete nuevo, asegurando que las dependencias estén frescas para la siguiente compilación.

cs10-koji-01.mx-os:
   La Memoria (PostgreSQL): Separamos la base de datos para garantizar la integridad transaccional (ACID). Koji realiza miles de
   consultas por segundo durante las construcciones masivas. Si la DB viviera en el mismo disco que un compilador escribiendo
   gigabytes de objetos, la latencia de disco (I/O Wait) colapsaría el sistema. Aquí vive el estado de toda la infraestructura.

cs10-koji-02.mx-os:
   El Almacén (NFS): Este es el puente físico entre los servicios. Koji requiere una estructura de directorios compartida
   (`/mnt/koji`).

   * Los `builders` montan este volumen para escribir los logs y los RPMs resultantes.
   * El `hub` lo monta para leer esos resultados e indexarlos.
   * Al tenerlo separado, podemos crecer el almacenamiento independientemente del cómputo.

cs10-koji-03.mx-os:
   El Músculo (Kojid): Aquí ocurre la magia. Este servidor ejecuta el demonio `kojid`, el cual instancia entornos de construcción
   limpios y aislados (chroots) usando **Mock**. Al estar aislado en su propia VM, si una compilación se cuelga o consume toda la
   RAM, no afecta al Hub ni a la Base de Datos.

cs10-koji-04.mx-os:
   Lookaside Cache: Aunque Koji suele usar `dist-git` completo, nosotros mantenemos nuestras fuentes (SPECS) en
   https://git.mx-os.mx/RPMs/.

   Este servidor solo se usa para almacenar los archivos binarios grandes (tarballs de código fuente) que no deben ir en git. El
   sistema descarga de aquí los `.tar.gz` necesarios antes de empezar a compilar.

   Más información sobre dist-git: https://github.com/release-engineering/dist-git

Conclusión
----------
¡Fiuf! Es bastante infraestructura para un entorno local, ¿no? Pero la separación de servicios y el manejo de CA son vitales para
entender cómo opera Koji realmente.

El objetivo es documentar el procedimiento tan bien que tú, o cualquier entidad interesada, pueda instalar su propio `Koji` y
empezar a construir paquetes sin perderse en el intento.

El chiste es que te metas al código y veas cómo está armado el playbook.

Si te quieres apuntar, únete a nuestro Telegram: https://t.me/mx_os_mx y ahí cotorreamos en el canal de `Infraestructura`.

Referencias
-----------
Repositorio del proyecto (Ansible Koji):
   https://git.mx-os.mx/MxOS/ansible-koji

Documentación oficial de Koji:
   https://docs.pagure.org/koji/

Repositorio de fuentes (MxOS RPMs):
   https://git.mx-os.mx/RPMs/

Proyecto dist-git (Upstream):
   https://github.com/release-engineering/dist-git

Comunidad MxOS (Telegram):
   https://t.me/mx_os_mx
