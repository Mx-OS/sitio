Bitácora de Cambios
===================

Todos los cambios notables en este proyecto serán documentados en este archivo.

El formato está basado en `Keep a Changelog <https://keepachangelog.com/es-ES/1.1.0/>`_,
y este proyecto se adhiere a `Semantic Versioning <https://semver.org/spec/v2.0.0.html>`_.

[Unreleased]
============

[0.1.0] - 2026-06-16
--------------------

Añadido
~~~~~~~

- Nuevo tema local basado en Pico CSS v2 (``themes/mxos``), optimizado para móviles y semántico.
- Alternador interactivo de tema claro y oscuro (Sun/Moon SVG) con persistencia en ``localStorage`` y prevención de parpadeos de carga (FOUC).
- Soporte para configurar el tema de forma forzada a través de parámetros de URL (``?theme=light`` o ``?theme=dark``).
- Sumatoria automatizada de columnas numéricas en la tabla de cuentas de transparencia.
- Archivo ``GNUmakefile`` para compilar la web localmente y agilizar tareas comunes.
- Nuevo artículo de noticias: "Rediseño del sitio y avances de infraestructura".

Cambiado
~~~~~~~~

- Reemplazo completo del tema minimalista ``terminal`` por el tema propio ``mxos``.
- Estilo y estructura de la página de contacto a tarjetas interactivas de canales, removiendo enlaces planos y caracteres redundantes.
- Enlace del botón de "Acerca" para que apunte directamente a la sección de organización de la documentación.
- Título y descripción meta de la página de inicio para mejorar el posicionamiento SEO.
- Configuración de GitLab CI/CD (``.gitlab-ci.yml``) optimizada:
  - Renombrado el trabajo de compilación principal a ``pages`` para disparar la publicación correctamente.
  - Centralizada la instalación de dependencias en un ``before_script`` global.
  - Eliminado el soporte inactivo de submódulos recursivos.
- Formato de los créditos del pie de página a una estructura minimalista con tuberías (``|``).

Quitado
~~~~~~~

- Carpeta del tema git submodule ``themes/terminal``.
