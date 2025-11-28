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
