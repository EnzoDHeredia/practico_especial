- **Diagrama General de Microservicios**: El siguiente diagrama representa la propuesta inicial de la arquitectura del sistema, mostrando una vista genérica en ejecución que destaca los servicios principales, las bases de datos asociadas y las relaciones de comunicación entre ellos mediante conexiones HTTP/REST. ![Ver diagrama](Imagenes/Diagrama_Microservicios_generico.jpg)

# Microservicios Propuestos

## Gestión de Clientes
- **Funcionalidad:** Manejo de datos personales de los clientes.
- **Base de datos asociada:** Base de datos de Clientes.
- **Restricciones:** Garantizar el acceso seguro y controlado a los datos sensibles.

## Gestión de Pedidos
- **Funcionalidad:** Manejo de pedidos (creación, intentos limitados, y flujo de procesamiento en las fases de preprocesado, autorización y aceptación).
- **Base de datos asociada:** Base de datos de Pedidos.
- **Restricciones:**
  - Implementar lógica de estado en el flujo del pedido.
  - Asegurar un máximo de tres intentos para cada cliente.

## Gestión de Reparto y Rutas
- **Funcionalidad:** Optimización de rutas para las flotas de transporte y asignación dinámica de algoritmos en función de la demora.
- **Base de datos asociada:** Base de datos de Pedidos (para relacionar con pedidos).
- **Restricciones:**
  - Dependencia con el microservicio de Pedidos para el seguimiento de entregas.

## Estadísticas
- **Funcionalidad:** Proveer información en tiempo real sobre pedidos y ubicación de camiones.
- **Base de datos asociada:** Base de datos de Clientes y Pedidos.
- **Restricciones:**
  - Información debe actualizarse en tiempo real.

## Gestión de Incidencias
- **Funcionalidad:** Registro y notificación de incidencias en el reparto.
- **Base de datos asociada:** Base de datos de Pedidos.
- **Restricciones:**
  - Notificar automáticamente a los gestores de ruta ante incidencias.
  - Dependencia con el microservicio de Reparto y Rutas.

## Procesamiento de Pagos
- **Funcionalidad:** Integración con la pasarela de pago de MercadoLibre para pagos seguros.
- **Base de datos asociada:** Base de datos de Clientes (para registro de transacciones).
- **Restricciones:**
  - Conexión segura con MercadoLibre.
  - No almacenar información sensible de pagos localmente.

## Notificaciones de Estado
- **Funcionalidad:** Enviar notificaciones a los clientes sobre el estado de sus pedidos.
- **Base de datos asociada:** Base de datos de Pedidos.
- **Restricciones:**
  - Integración con otros servicios como Pedidos, Reparto y Pagos para obtener datos actualizados.

## Auditoría y Registro
- **Funcionalidad:** Registrar y auditar acciones críticas en los módulos de Clientes, Pedidos y Pagos.
- **Restricciones:**
  - Centralizar logs de múltiples microservicios.

## Gestión de Usuarios y Roles
- **Funcionalidad:** Controlar acceso y roles de usuarios en el sistema.
- **Base de datos asociada:** Base de datos independiente o compartida para autenticación y roles.
- **Restricciones:**
  - Autenticación centralizada para todos los microservicios.
