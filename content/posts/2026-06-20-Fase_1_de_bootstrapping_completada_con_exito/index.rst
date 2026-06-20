---
title: "Fase 1 de bootstrapping completada con éxito"
date: 2026-06-20T12:30:00-06:00
author: "Rénich Bon Ćirić y Gemini AI"
description: "Anunciamos la culminación exitosa de la primera fase de compilación en Koji, logrando el bootstrap completo de 336 paquetes base para la soberanía de MxOS."
cover: cover.jpg
---

¡Excelentes noticias para la comunidad de MxOS!

Nos entusiasma compartir que hemos completado al 100% la **Fase 1** de la estrategia de bootstrapping y empaquetamiento de nuestra distribución, logrando un hito clave hacia la soberanía tecnológica.

Fase 1 completada: 336 paquetes base listos
===========================================
Gracias al esfuerzo conjunto y a la optimización de nuestra infraestructura de construcción en Koji, logramos compilar, firmar (con la llave oficial de Siguldry) y etiquetar exitosamente los **336 paquetes base** (etiquetados bajo ``mxos0`` / Generación 1) provenientes de CentOS Stream 10. 

Este conjunto constituye el núcleo básico y las herramientas de desarrollo esenciales para levantar nuestro sistema. Cabe destacar que, hasta el momento, todo este esfuerzo de desarrollo de infraestructura ha sido realizado exclusivamente por nosotros dos (Rénich y la IA Gemini como copiloto de ingeniería), colaborando de manera estrecha y sin ayuda externa en esta etapa inicial.

El reto técnico: Parcheando de forma limpia
===========================================
Durante esta fase, nos enfrentamos a diversos retos técnicos de gran interés. El más notable de ellos fue un fallo en la suite de pruebas unitarias de ``libssh`` dentro de los chroots de Mock, debido a la falta de permisos para la asignación de pseudoterminales (PTY) en entornos de construcción aislados y restrictivos.

En lugar de desactivar las pruebas a nivel global de forma descuidada, procedimos a diseñar un parche que consulta la disponibilidad de ``openpty()`` en tiempo de ejecución. Si el entorno no soporta la creación de PTY, la prueba se omite de forma elegante utilizando las macros de CMocka (``skip()``), lo que nos permitió mantener la suite de pruebas activa e íntegra. Este parche ya ha sido documentado para ofrecerse formalmente a la comunidad upstream de ``libssh``.

Nuestra infraestructura actual y el siguiente paso
==================================================
Actualmente, todo este ecosistema de compilación y pruebas está corriendo y validándose dentro de nuestro entorno local de desarrollo. 

El proyecto cuenta con dos servidores físicos de alto rendimiento que nos fueron generosamente donados para la infraestructura de producción. Sin embargo, en este momento **no tenemos un espacio de hospedaje (data center) ni conectividad adecuada para instalarlos**, por lo que estamos buscando activamente patrocinadores o un centro de datos interesado en darles un hogar y sumarse a esta iniciativa por la soberanía tecnológica.

Con la Fase 1 concluida con éxito en desarrollo, estamos listos para iniciar la **Fase 2 (Generación 2 / ``mxos10``)**. En esta etapa, el sistema de construcción Koji cortará la herencia de los repositorios externos de CentOS Stream y se abastecerá exclusivamente de los 336 paquetes que acabamos de compilar. Esto nos llevará al auto-hospedaje (self-hosting) absoluto.

Si conoces a alguien que pueda apoyarnos con el hospedaje de los servidores, o si deseas colaborar con el desarrollo y empaquetamiento, te invitamos a unirte a nuestro canal de `Telegram <https://t.me/mx_os_mx>`_.

¡Sigamos avanzando firmes en la construcción de MxOS!
