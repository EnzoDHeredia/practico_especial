# Rediseño del Sistema para Unificación de Servicios y Mejora en la Gestión de Información de Clientes

---

### Context and Problem Statement
El sistema actual presenta varios microservicios que manejan funcionalidades similares, lo que provoca redundancia y sobrecarga en la infraestructura. Además, los servicios de Gestión de Roles y Usuarios y de Autenticación no están desacoplados adecuadamente, lo que genera una complejidad innecesaria.

Los siguientes retos clave deben ser abordados en el rediseño:

- **Redundancia en los servicios de estadísticas y notificación de estado de pedidos:** Ambos servicios realizan tareas similares relacionadas con la consulta y el procesamiento de eventos de pedidos.
- **Falta de trazabilidad de cambios en la información del cliente:** Los cambios en los datos del cliente no están siendo auditados y almacenados de manera centralizada.
- **Dependencia entre gestión de usuarios y autenticación:** El microservicio de gestión de roles y usuarios realiza tareas que pueden ser delegadas a un servidor de autenticación especializado.

---

### Decision Drivers
- **Reducción de la complejidad:** Unificar servicios similares y reducir dependencias innecesarias.
- **Escalabilidad:** Mantener una infraestructura que sea fácilmente escalable, especialmente para servicios de consultas y auditoría.
- **Trazabilidad de datos:** Asegurar que cualquier cambio en la información de clientes sea auditado correctamente.
- **Seguridad:** Mejorar la seguridad mediante un servidor dedicado para la autenticación de usuarios.

---

### Considered Options
1. **Unificación de los microservicios de Estadísticas y Notificación de Estado de Pedido (Elegida):**
   - Unificar ambos microservicios, ya que manejan eventos relacionados con el estado de los pedidos y estadísticas asociadas.
   - Crear un servicio único para procesar eventos y manejar consultas de estado de pedidos y estadísticas.

2. **Uso de una Base de Datos de Auditoría para Registrar Cambios en los Datos del Cliente (Elegida):**
   - Implementar una base de datos centralizada de auditoría que registre cualquier cambio realizado sobre los datos del cliente, especialmente aquellos que afecten a pedidos o pagos.
   - Utilizar eventos o cambios de datos para alimentar esta base de datos, mejorando la trazabilidad.

3. **Sustitución del Microservicio de Gestión de Roles y Usuarios por un Servidor de Autenticación (Elegida):**
   - Eliminar el microservicio de gestión de roles y usuarios y sustituirlo por un servidor de autenticación especializado.
   - Delegar la validación de credenciales y gestión de roles al servidor de autenticación.

---

### Decision Outcome
**Chosen option:**

- Unificación de los microservicios de Estadísticas y Notificación de Estado de Pedido.
- Uso de una Base de Datos de Auditoría para registrar cambios.
- Sustitución del microservicio de Gestión de Roles y Usuarios por un servidor de autenticación.

#### Consequences
**Good, because:**
- **Mejora la escalabilidad:** El sistema ahora tiene menos servicios especializados, lo que facilita su escalabilidad y mantenimiento.
- **Reducción de redundancias:** Unificar servicios elimina tareas duplicadas y mejora la eficiencia.
- **Mejor trazabilidad:** La base de datos de auditoría garantiza que cualquier cambio en los datos del cliente sea registrado de manera adecuada.
- **Mejor gestión de seguridad:** El servidor de autenticación proporciona un mecanismo centralizado para la validación de usuarios, mejorando la seguridad.

**Bad, because:**
- **Mayor complejidad inicial:** El rediseño requiere trabajo adicional en la integración y configuración de los servicios unificados y nuevos componentes.
- **Dependencia del servidor de autenticación:** La dependencia de un único servidor para la autenticación puede convertirse en un punto único de falla si no se gestiona adecuadamente la alta disponibilidad.

---

### Confirmation
La implementación del rediseño se validará mediante:

- **Pruebas de integración:** Asegurarse de que la unificación de servicios y la nueva base de datos de auditoría no introduzcan errores en los flujos de datos y operaciones de otros microservicios.
- **Pruebas de carga:** Evaluar que la unificación de servicios mantenga la escalabilidad bajo cargas elevadas.
- **Pruebas de seguridad:** Verificar que el servidor de autenticación maneje correctamente la validación de usuarios y la gestión de roles.

---

### Pros and Cons of the Options
**Option 1:** Unificación de los microservicios de Estadísticas y Notificación de Estado de Pedido  
- **Good:**  
  - Mejora la eficiencia y simplificación de la infraestructura.  
  - Centraliza la lógica relacionada con pedidos y estadísticas.  
- **Bad:**  
  - Puede ser más difícil de gestionar al principio debido a la integración de ambas funcionalidades.  

**Option 2:** Uso de una Base de Datos de Auditoría  
- **Good:**  
  - Mejora la trazabilidad de los datos.  
  - Permite una auditoría detallada de los cambios en los datos del cliente.  
- **Bad:**  
  - Puede generar una sobrecarga adicional si no se gestiona correctamente el almacenamiento y la propagación de eventos.  

**Option 3:** Sustitución del Microservicio de Gestión de Roles y Usuarios por un Servidor de Autenticación  
- **Good:**  
  - Mejora la seguridad y delega responsabilidades.  
  - Centraliza la gestión de autenticación y roles.  
- **Bad:**  
  - Introduce un punto de dependencia adicional (el servidor de autenticación).  

---

### More Information
**Herramientas sugeridas:**
- Para la base de datos de auditoría: **PostgreSQL** o **MongoDB** para almacenamiento de eventos.  
- Para el servidor de autenticación: **OAuth 2.0**, **OpenID Connect**, **Keycloak**.  
- Para la unificación de servicios: **Kafka** o **RabbitMQ** para gestión de eventos.
