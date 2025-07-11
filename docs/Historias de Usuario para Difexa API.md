# **Historias de Usuario para Difexa API**

## **Módulo de Autenticación y Gestión de Usuarios**

### **H01: Registro de Usuario Invitado**

**COMO** usuario invitado **QUIERO** poder registrarme en el sistema **PARA QUE** pueda solicitar acceso para publicar contenido en los canales de la facultad.

**Criterios de aceptación:**

1. El formulario de registro debe solicitar al menos: nombre completo, dni, correo electrónico institucional, contraseña y confirmación de contraseña.
2. El sistema debe validar que el correo electrónico no esté registrado previamente.
3. La contraseña debe cumplir requisitos mínimos de seguridad (8 caracteres, combinación de letras y números).
4. Al completar el registro exitosamente, el usuario debe recibir un correo de confirmación.
5. El usuario debe quedar con rol "Registrado" en estado pendiente de aprobación.
6. El sistema debe informar al usuario que su solicitud está pendiente de aprobación.

### **H02: Autenticación de usuario**

**COMO** usuario registrado **QUIERO** poder iniciar sesión en el sistema **PARA QUE** pueda acceder a las funcionalidades según mi rol asignado.

**Criterios de aceptación:**

1. El sistema debe permitir el ingreso mediante correo electrónico y contraseña.
2. El sistema debe generar y devolver un token de autenticación (Bearer Token) con tiempo de expiración.
3. El sistema debe rechazar credenciales incorrectas con mensaje apropiado.
4. El sistema debe impedir el acceso a usuarios no aprobados, informando su estado.
5. El sistema debe registrar la fecha y hora del inicio de sesión exitoso.

### **H03: Gestión de usuarios por administrador**

**COMO** administrador **QUIERO** poder gestionar las cuentas de usuario **PARA QUE** pueda controlar quién tiene acceso al sistema y con qué permisos.

**Criterios de aceptación:**

1. El administrador debe poder ver un listado paginado de todos los usuarios registrados.
2. El administrador debe poder filtrar usuarios por rol, estado y correo electrónico.
3. El administrador debe poder aprobar o rechazar solicitudes de registro pendientes.
4. El administrador debe poder asignar o revocar roles a usuarios (Publicador, Administrador).
5. El administrador debe poder habilitar o deshabilitar cuentas de usuario existentes.
6. El sistema debe enviar notificación por correo cuando cambia el estado de aprobación de un usuario.

## **Módulo de Gestión de Canales**

### **Historia 4: Creación de canal de difusión**

**COMO** administrador **QUIERO** poder crear canales temáticos de difusión **PARA QUE** las publicaciones puedan categorizarse y dirigirse al público adecuado.

**Criterios de aceptación:**

1. El sistema debe permitir ingresar nombre, descripción y tipo de canal (cátedra, departamento, instituto, etc.).
2. El sistema debe permitir asociar uno o múltiples medios de publicación al canal (pantallas, redes sociales, plataformas).
3. El sistema debe permitir añadir un texto contextual para guiar al modelo de IA en la generación de contenido.
4. El sistema debe validar que el nombre del canal sea único.
5. El canal creado debe estar disponible inmediatamente para asignación a publicadores.

### **H05: Asignación de canales a publicadores**

**COMO** administrador **QUIERO** poder asignar canales específicos a usuarios publicadores **PARA QUE** solo puedan gestionar contenido en las áreas autorizadas.

**Criterios de aceptación:**

1. El sistema debe mostrar una lista de canales disponibles y usuarios con rol publicador.
2. El sistema debe permitir seleccionar múltiples canales para un mismo publicador.
3. El sistema debe permitir revocar acceso a canales previamente asignados.
4. El publicador debe recibir una notificación cuando se le asigna o revoca acceso a un canal.
5. Los cambios en asignaciones deben aplicarse inmediatamente sin necesidad de reiniciar sesión.

### **H06: Modificación de canal**

**COMO** administrador **QUIERO** poder modificar la configuración de los canales **PARA QUE** pueda adaptar su funcionamiento según necesidades cambiantes.

**Criterios de aceptación:**

1. El sistema debe permitir editar nombre, descripción y tipo de canal existente.
2. El sistema debe permitir actualizar el texto contextual para el modelo de IA.
3. El sistema debe permitir modificar los medios de publicación asociados.
4. El sistema debe registrar quién realizó la última modificación y cuándo.
5. Los cambios deben aplicarse a todas las publicaciones futuras, no a las ya procesadas.

## **Módulo de Gestión de Publicaciones**

### **H07: Creación de publicación**

**COMO** publicador **QUIERO** poder crear una nueva publicación **PARA QUE** pueda compartir información relevante en los canales autorizados.

**Criterios de aceptación:**

1. El sistema debe permitir ingresar título, contenido, y adjuntar archivos multimedia (imágenes, videos).
2. El sistema debe permitir seleccionar uno o varios canales (solo entre los autorizados al publicador).
3. El sistema debe permitir seleccionar los medios de publicación específicos para cada canal seleccionado.
4. El sistema debe permitir programar la fecha y hora de publicación.
5. El sistema debe guardar la publicación en estado "borrador" hasta que se solicite el enriquecimiento por IA.

### **H08: Edición de publicación**

**COMO** publicador **QUIERO** poder editar mis publicaciones existentes **PARA QUE** pueda corregir errores o actualizar información antes de su difusión.

**Criterios de aceptación:**

1. El sistema debe permitir editar todos los campos de una publicación en estado "borrador".
2. El sistema debe permitir modificar canales y medios seleccionados.
3. El sistema debe permitir cambiar la fecha programada si aún no ha sido publicada.
4. El sistema debe permitir edición limitada de publicaciones ya enriquecidas pero no difundidas.
5. El sistema debe registrar el historial de cambios incluyendo usuario, fecha y modificaciones realizadas.

### **H09: Eliminación de publicación**

**COMO** publicador **QUIERO** poder eliminar publicaciones **PARA QUE** pueda descartar contenido obsoleto o incorrecto.

**Criterios de aceptación:**

1. El sistema debe permitir eliminar publicaciones en cualquier estado excepto "difundido".
2. El sistema debe solicitar confirmación antes de eliminar definitivamente.
3. El sistema debe permitir a los**administradores** eliminar cualquier publicación.
4. El sistema debe mantener un registro de publicaciones eliminadas para auditoría.
5. El sistema debe notificar si la eliminación no es posible por restricciones del estado actual.

## **Módulo de Enriquecimiento por IA**

### **H10: Solicitud de enriquecimiento por IA**

**COMO** publicador **QUIERO** poder solicitar el enriquecimiento automático de mi contenido **PARA QUE** se generen versiones adaptadas a cada medio de publicación seleccionado.

**Criterios de aceptación:**

1. El sistema debe enviar el contenido original junto con el texto contextual del canal al servicio externo de IA.
2. El sistema debe indicar claramente el estado de procesamiento de la solicitud.
3. El sistema debe notificar al usuario cuando el enriquecimiento esté completo y listo para revisión.
4. El sistema debe manejar errores de conexión con el servicio externo, notificando apropiadamente.
5. El sistema debe permitir cancelar el proceso de enriquecimiento mientras esté en curso.

### **H11: Revisión de contenido enriquecido**

**COMO** publicador **QUIERO** poder revisar las versiones enriquecidas generadas por IA **PARA QUE** pueda aprobarlas, modificarlas o rechazarlas antes de su difusión.

**Criterios de aceptación:**

1. El sistema debe mostrar claramente la versión original y cada versión generada por la IA.
2. El sistema debe permitir aprobar, rechazar o solicitar regeneración individual de cada versión.
3. El sistema debe permitir editar manualmente el contenido generado antes de aprobar.
4. El sistema debe permitir aprobar todas las versiones con una sola acción si el usuario lo desea.
5. El sistema debe guardar un historial de las diferentes versiones generadas para cada publicación.

## **Módulo de Distribución de Contenido**

### **H12: Programación de publicaciones**

**COMO** publicador **QUIERO** poder programar la fecha y hora de publicación **PARA QUE** el contenido se difunda en el momento más oportuno.

**Criterios de aceptación:**

1. El sistema debe permitir seleccionar fecha y hora específicas para la difusión automática.
2. El sistema debe validar que la fecha programada sea futura.
3. El sistema debe permitir programar publicaciones pendientes.
4. El sistema debe ejecutar automáticamente la difusión en el momento programado.
5. El sistema debe mostrar claramente el estado de programación de cada publicación.

### **H13: Difusión manual de contenido**

**COMO** publicador **QUIERO** poder difundir inmediatamente una publicación aprobada **PARA QUE** el contenido urgente llegue sin demora a los medios seleccionados.

**Criterios de aceptación:**

1. El sistema debe permitir difundir manualmente una publicación que tenga todas sus versiones aprobadas.
2. El sistema debe confirmar la acción antes de proceder con la difusión inmediata.
3. El sistema debe notificar el éxito o fallo en cada medio de difusión seleccionado.
4. El sistema debe registrar la hora exacta de difusión y el usuario que la ejecutó.
5. El sistema debe actualizar el estado de la publicación a "difundido" tras completar el proceso.

### **H14: Consulta de publicaciones para dispositivos**

**COMO** dispositivo cliente **QUIERO** poder obtener las publicaciones correspondientes a mi pantalla **PARA QUE** pueda mostrarlas en los espacios físicos de la facultad.

**Criterios de aceptación:**

1. El sistema debe autenticar al dispositivo mediante su token único.
2. El sistema debe devolver solo publicaciones en estado "difundido" asignadas al dispositivo.
3. El sistema debe filtrar las publicaciones según los canales configurados para el dispositivo.
4. El sistema debe incluir todos los recursos multimedia necesarios o sus URLs de acceso.
5. El sistema debe registrar las consultas exitosas para análisis de disponibilidad.

## **Módulo de Seguridad y Permisos**

### **H15: Gestión de permisos por rol**

**COMO** administrador **QUIERO** poder definir permisos específicos para cada rol **PARA QUE** pueda implementar un control de acceso granular según responsabilidades.

**Criterios de aceptación:**

1. El sistema debe mostrar una matriz de roles y permisos disponibles.
2. El sistema debe permitir asignar o revocar permisos específicos a cada rol.
3. El sistema debe aplicar los cambios de permisos inmediatamente a todos los usuarios con ese rol.
4. El sistema debe impedir que se eliminen permisos críticos para el funcionamiento del sistema.
5. El sistema debe registrar quién realizó cambios en los permisos y cuándo.

### **H16: Cierre de sesión**

**COMO** usuario autenticado **QUIERO** poder cerrar sesión en el sistema **PARA QUE** mi sesión no quede activa en dispositivos compartidos.

**Criterios de aceptación:**

1. El sistema debe invalidar el token de autenticación actual al cerrar sesión.
2. El sistema debe confirmar visualmente que la sesión se cerró correctamente.
3. El sistema debe redireccionar al usuario a la pantalla de inicio de sesión.
4. El sistema debe registrar la fecha y hora del cierre de sesión.
5. El sistema debe impedir el acceso a recursos protegidos con el token invalidado.

## **Requisitos No Funcionales Importantes**

Además de las historias de usuario, los siguientes requisitos no funcionales son esenciales:

1. **Seguridad**: El sistema debe implementar autenticación robusta mediante Bearer Token y protección contra vulnerabilidades comunes (XSS, CSRF, inyección SQL).
2. **Rendimiento**: La API debe responder a las solicitudes en menos de 500ms en condiciones normales y manejar al menos 100 solicitudes concurrentes.
3. **Disponibilidad**: El sistema debe estar disponible al menos el 99.5% del tiempo durante el horario operativo de la facultad.
4. **Escalabilidad**: La arquitectura debe permitir escalar horizontalmente para acomodar crecimiento en usuarios y publicaciones.
5. **Integración**: Debe existir documentación clara para la integración con sistemas de frontend y dispositivos externos.
6. **Auditoría**: Todas las acciones críticas deben ser registradas para permitir auditorías de seguridad y cumplimiento.
