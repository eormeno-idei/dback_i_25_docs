# **Descripción General del Software**

El sistema, denominado *Difexa API*, es un backend desarrollado como una **API REST** orientada a la gestión y automatización de la difusión de información académica, institucional y de interés general producida por diversas áreas de la Facultad de Ciencias Exactas, Físicas y Naturales. Su diseño responde a una arquitectura desacoplada, segura y escalable, en la que el frontend y los dispositivos consumidores serán clientes externos que interactúan exclusivamente a través de endpoints públicos y autenticados.

![Difexa API](difexa-api-arch.png)

El propósito principal del sistema es permitir que usuarios autorizados gestionen publicaciones multimediales —de tipo textual, visual o audiovisual— y seleccionen sus **Canales** de difusión. Los **Canales** representan categorías temáticas como cátedras, centros, institutos o departamentos, y están asociados a uno o más medios de publicación:

* Pantallas distribuidas en espacios físicos de la facultad.  
* Redes sociales institucionales.  
* Plataformas editoriales u otros medios digitales.

Cada publicación será enriquecida automáticamente mediante un **modelo de lenguaje externo**, el cual generará versiones adaptadas del contenido según el medio seleccionado. Esta interacción se realizará mediante **servicios externos orquestados por n8n**, y podrá incluir también generación de imágenes o vídeos a demanda. El usuario podrá aprobar, solicitar modificaciones o rechazar las respuestas generadas, repitiendo este proceso hasta quedar conforme. Una vez aprobada, la publicación será enviada al o los medios correspondientes.

Cada Canal podrá tener asociado un **texto contextual** que será enviado junto con los prompts al modelo de lenguaje. Este contexto semántico servirá para asegurar que las respuestas generadas por la IA sean coherentes con el enfoque, estilo y objetivos comunicacionales del área académica correspondiente.

El sistema contempla distintos tipos de usuarios, cuyos accesos y permisos estarán definidos mediante un sistema robusto de roles:

* **Invitados:** Pueden registrarse y solicitar autorización para publicar.  
* **Registrados:** Usuarios pendientes de aprobación, con acceso limitado.  
* **Publicadores:** Usuarios autorizados para crear y administrar publicaciones en sus **canales** habilitados.  
* **Administradores:** Encargados de gestionar usuarios, roles, **canales** y dispositivos de publicación.  
* **Dispositivos:** Clientes que consumen publicaciones específicas y las proyectan en pantallas físicas.

Toda la interacción con el sistema se realiza a través de llamadas a endpoints autenticados, utilizando el estándar **Bearer Token** para el control de acceso y validación de identidad. La autenticación y el manejo de sesiones están implementados con tecnologías como **Laravel Breeze** y **Laravel Sanctum o Passport**, complementadas con la librería **Spatie Laravel Permission** para la administración avanzada de roles y permisos.

En resumen, *Difexa API* es un sistema backend moderno, orientado a servicios, que centraliza la gestión de contenidos académicos y su difusión automatizada en múltiples medios, integrando IA generativa, clasificación temática inteligente y un modelo de seguridad robusto basado en tokens de autenticación. La API está diseñada para ser consumida por interfaces web, apps móviles y dispositivos físicos, dentro de un ecosistema distribuido, seguro y escalable.