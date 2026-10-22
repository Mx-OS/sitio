Bitácora de Cambios
===================

Todos los cambios notables en este proyecto serán documentados en este archivo.

El formato está basado en `Keep a Changelog <https://keepachangelog.com/es-ES/1.1.0/>`_,
y este proyecto se adhiere a `Semantic Versioning <https://semver.org/spec/v2.0.0.html>`_.

[Unreleased]
============

[0.2.0] - 2026-10-22
--------------------

.. rubric:: Añadido

- Página dedicada **Acerca** (``content/acerca.rst``) con misión, visión, principios fundamentales, gobernanza, modelo operativo, impacto estratégico, equipo impulsor y enlaces a la documentación oficial.
- Sección y pilar fundacional de **Replicabilidad al 100% y Aprendizaje Abierto** tanto en la portada como en ``Acerca``, explicando el proceso colectivo de estudio y descifrado de CentOS Stream 10.
- Página dedicada **Colabora** (``content/colabora.rst``) en el menú principal con el llamado a la acción estructurado en seis áreas de apoyo: Infraestructura y Hospedaje, Ingeniería y Documentación, Sitio Web Comunidad y Redes, Gestión y Procuración de Fondos, Academia e Investigación, y Apoyo Económico.
- Sistema de distintivos visuales (``.post-badge``) y barra de filtrado estático (``Todos``, ``Noticias``, ``Blog``) en ``layouts/partials/post-filters.html`` utilizando la taxonomía nativa ``categories`` de Hugo.
- Procesamiento automático de imágenes de portada a formato **WebP responsivo** (``640w``, ``1024w``, ``1600w`` con ``srcset``, ``sizes``, ``fetchpriority`` y ``loading="lazy"``) en ``layouts/partials/cover.html`` y generación WebP ``1200x630`` para ``og:image`` en ``layouts/partials/head.html``.

.. rubric:: Cambiado

- Unificación de las secciones ``Blog`` y ``Noticias`` dentro de ``content/posts/`` con redirecciones automáticas (``aliases``) desde las rutas anteriores de ``/noticias/``.
- Fusión de la página ``Gracias`` dentro de ``Cuentas`` (``content/cuentas.rst``) con redirección desde ``/gracias/`` y presentación responsiva en tarjetas apiladas con etiquetas ``data-label`` para vista móvil.
- Actualización de la denominación oficial a ``Fundación MxOS, A.C. (en formación)`` en todo el sitio y el pie de página.
- Consolidación de hojas de estilo en ``assets/css/mxos-theme.css`` aprovechando las clases semánticas de Pico CSS v2 (``.overflow-auto``, ``table.striped``, ``role="button"``) y eliminando todos los atributos ``style`` en línea.
- Optimización sin pérdida perceptual de todas las imágenes rasterizadas del repositorio (reducción de ``~8.34 MB`` a ``~1.18 MB``).
- Distribución de tarjetas en cuadrícula balanceada de 2 columnas en escritorio y 1 columna en dispositivos móviles para ``Visión y Enfoque``, ``Misión y Visión``, ``Principios Fundamentales`` y ``Áreas en las que Necesitamos Apoyo``.

.. rubric:: Corregido

- Reemplazo de las claves obsoletas ``languageCode`` y ``languageName`` por ``locale`` y ``label`` en ``hugo.yaml`` para compatibilidad con Hugo v0.158.0+ (cierra #1).
- Corrección de especificidad CSS en ``.main-logo`` que causaba que el logotipo principal se expandiera al 100% del contenedor en escritorio.
- Corrección de desbordamientos horizontales en vista móvil para el encabezado, tablas, imágenes de portada y objetos SVG incrustados.
- Corrección del enlace al Manual de Replicación e Ingeniería hacia la ruta ``dirhtml`` válida en ``docs.mx-os.mx``.

.. rubric:: Quitado

- Referencia a ``EU OS`` en la página de inicio.
- Archivo redundante ``assets/css/mxos.css``, página separada ``content/gracias.rst`` y directorio separado ``content/noticias/``.

[0.1.0] - 2026-06-16
--------------------

.. rubric:: Añadido

- Nuevo tema local basado en Pico CSS v2 (``themes/mxos``), optimizado para móviles y semántico.
- Alternador interactivo de tema claro y oscuro (Sun/Moon SVG) con persistencia en ``localStorage`` y prevención de parpadeos de carga (FOUC).
- Soporte para configurar el tema de forma forzada a través de parámetros de URL (``?theme=light`` o ``?theme=dark``).
- Sumatoria automatizada de columnas numéricas en la tabla de cuentas de transparencia.
- Archivo ``GNUmakefile`` para compilar la web localmente y agilizar tareas comunes.
- Nuevo artículo de noticias: "Rediseño del sitio y avances de infraestructura".

.. rubric:: Cambiado

- Reemplazo completo del tema minimalista ``terminal`` por el tema propio ``mxos``.
- Estilo y estructura de la página de contacto a tarjetas interactivas de canales, removiendo enlaces planos y caracteres redundantes.
- Enlace del botón de "Acerca" para que apunte directamente a la sección de organización de la documentación.
- Título y descripción meta de la página de inicio para mejorar el posicionamiento SEO.
- Configuración de GitLab CI/CD (``.gitlab-ci.yml``) optimizada:

  - Renombrado el trabajo de compilación principal a ``pages`` para disparar la publicación correctamente.
  - Centralizada la instalación de dependencias en un ``before_script`` global.
  - Eliminado el soporte inactivo de submódulos recursivos.

- Formato de los créditos del pie de página a una estructura minimalista con tuberías (``|``).

.. rubric:: Quitado

- Carpeta del tema git submodule ``themes/terminal``.
