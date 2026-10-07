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
Para desarrollar el sitio, solo hay que instalar `hugo` y clonar el sitio:

.. code-block:: bash

   # instalar hugo
   dnf -y install hugo

   # clonarlo
   git clone https://gitlab.com/MxOS/sitio.git

Para más información sobre como hackearle a un sitio hecho en `hugo`, consulta su documentación en: https://gohugo.io/documentation/

.. note::
   Procuramos usar la versión más actual siempre.

Creación de contenido
---------------------
Para crear contenido nuevo, utilizamos el comando `hugo new`. Asegúrate de usar la extensión `.rst` para mantener el formato del
sitio.

Blog
~~~~
Para agregar una entrada al blog, ejecuta:

.. code-block:: bash

   hugo new posts/nombre-de-tu-entrada.rst

Noticias
~~~~~~~~
Para agregar una noticia, ejecuta:

.. code-block:: bash

   hugo new noticias/nombre-de-la-noticia.rst

Una vez creado el archivo, edítalo con tu editor de texto preferido para agregar el contenido.

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
