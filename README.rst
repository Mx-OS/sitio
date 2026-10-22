==================================
Sitio oficial de la Fundación MxOS
==================================

Descripción
===========
El sitio está implementado usando `hugo <https://gohugo.io/>`_.

Instrucciones
=============

Desarrollo
----------
Para desarrollar el sitio localmente, instala ``hugo`` junto con el soporte de reStructuredText (``python3-docutils`` y
``python3-pygments``) y clona el repositorio:

.. code-block:: bash

   # instalar dependencias en Fedora
   sudo dnf -y install hugo python3-docutils python3-pygments

   # clonar el repositorio
   git clone https://gitlab.com/MxOS/sitio.git
   cd sitio

   # iniciar el servidor de desarrollo con recarga automática
   make dev

Para más información sobre cómo trabajar con un sitio hecho en ``hugo``, consulta su documentación oficial en:
https://gohugo.io/documentation/

.. note::
   Procuramos usar siempre la versión más actual de Hugo.

Creación de contenido
---------------------
Todas las publicaciones (tanto artículos técnicos de **Blog** como anuncios de **Noticia**) viven unificadas dentro de
``content/posts/`` y se distinguen mediante los campos ``category`` y ``categories`` en el encabezado YAML (frontmatter). Asegúrate
de usar siempre el formato ``.rst`` (reStructuredText).

Para agregar una nueva publicación, crea un paquete de página (o ejecuta ``hugo new posts/AAAA-MM-DD-titulo/index.rst``) con el
siguiente encabezado:

.. code-block:: yaml

   ---
   title: "Título de la publicación"
   date: 2026-10-22T12:00:00-06:00
   category: "Blog" # Usa "Blog" o "Noticia"
   categories:
     - Blog # Usa "Blog" o "Noticia"
   author: "Nombre del Autor"
   description: "Resumen breve del artículo o noticia."
   cover: cover.jpg
   ---

Una vez creado el archivo, edítalo con tu editor de texto preferido para redactar el contenido en reStructuredText.

Publicación
-----------
El flujo de trabajo para colaborar es:

* Bifurca (fork) el repositorio.
* Clona tu bifurcación localmente.
* Crea tu contenido siguiendo las instrucciones de arriba.
* Sube los cambios (push) a tu bifurcación.
* Abre una petición de cambios (merge request) y avísanos en `Telegram <https://t.me/mx_os_mx>`_.

Tu colaboración será publicada una vez que aprobemos la petición.

Licencia
========

Este proyecto implementa una estructura de licenciamiento dual para proteger tanto el software del portal web como su acervo documental y editorial:

* **Motor del sitio, plantillas y automatización:** El código fuente de las plantillas Hugo, estructuras de diseño, hojas de estilo y scripts de compilación se distribuyen bajo los términos de la `GNU Affero General Public License v3.0 o posterior`_ (AGPL-3.0-or-later).
* **Contenido textual, notas y publicaciones:** Todo el material editorial, textos del blog y noticias se distribuyen bajo la licencia `Creative Commons Attribution-ShareAlike 4.0 International`_ (CC-BY-SA-4.0).
* **Fragmentos de código en artículos:** Los ejemplos de código, configuraciones y fragmentos incluidos dentro de los artículos y publicaciones están licenciados de forma paralela bajo la `Licencia MIT`_.

Consulta el archivo `LICENSE`_ para el texto íntegro de la licencia principal y el directorio ``LICENSES/`` para los textos canónicos de cumplimiento REUSE.

..
   Referencias y Enlaces:
.. _GNU Affero General Public License v3.0 o posterior: https://www.gnu.org/licenses/agpl-3.0.html
.. _Creative Commons Attribution-ShareAlike 4.0 International: https://creativecommons.org/licenses/by-sa/4.0/
.. _Licencia MIT: https://opensource.org/license/mit
.. _LICENSE: LICENSE
