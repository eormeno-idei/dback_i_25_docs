@workspace Genera una vista Blade para Laravel 12 que incluya:

1. Un formulario con los siguientes elementos:
   - Un campo de texto para el nombre de la invocación (para guardar en historial)
   - Un selector (dropdown) para elegir el método HTTP (GET, POST, PUT, DELETE, PATCH)
   - Un campo de texto para ingresar la URL/ruta del endpoint
   - Un textarea para el cuerpo de la petición (JSON)
   - Un botón para ejecutar la llamada

2. Sistema de historial de invocaciones:
   - Una lista desplegable que muestre todas las consultas guardadas, ordenadas por fecha (más reciente primero)
   - Un botón con icono de eliminar al lado de la lista para borrar consultas del historial
   - Almacenamiento automático en localStorage cuando se realiza una invocación
   - Actualización automática del localStorage cuando se modifican los campos
   - Carga automática de datos al seleccionar una consulta del historial

3. Un área de respuesta que muestre:
   - El JSON de respuesta formateado y con syntax highlighting
   - El código de estado HTTP
   - Headers de respuesta

4. Documentación integrada:
   - Sección de documentación con ejemplos de uso en formato Markdown
   - Visualización de la documentación directamente en la página
   - Ejemplos prácticos de diferentes tipos de peticiones API

5. Archivos separados:
   - CSS en archivo independiente (public/css/api-tester.css)
   - JavaScript principal en archivo independiente (public/js/api-tester.js)
   - JavaScript del historial en archivo separado (public/js/api-history.js)
   - Archivo de documentación Markdown renderizable

6. Funcionalidades JavaScript:
   - Realizar peticiones HTTP usando fetch API
   - Manejar diferentes métodos HTTP
   - Mostrar loading states
   - Formatear respuesta JSON de manera legible
   - Gestión completa del historial con localStorage
   - Validación del formulario y manejo de errores

7. Estilos con tema oscuro (dark theme):
   - Paleta de colores oscura profesional (grises, azules oscuros)
   - Diseño limpio y moderno adaptado al tema oscuro
   - Responsive design con media queries
   - Efectos hover y focus optimizados para tema oscuro
   - Layout flexible con flexbox o grid
   - Syntax highlighting para JSON adaptado al tema oscuro
   - Contrastes apropiados para buena legibilidad

El componente debe ser una vista Blade independiente que pueda ser incluida en cualquier layout de Laravel 12. Incluye comentarios explicativos en todos los archivos generados. Usa una paleta de colores profesional para el tema oscuro.