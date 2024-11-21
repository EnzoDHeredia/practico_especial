# Synchronizing Delivery States Between Gestión de Rutas and Pedidos

### Context and Problem Statement
El microservicio de Gestión de Rutas y Reparto es responsable de asignar y ejecutar rutas para la entrega de pedidos. Durante este proceso, los estados de los pedidos (e.g., En Reparto, Entregado, Incidencia Detectada) cambian y deben sincronizarse con el microservicio de Pedidos para mantener consistencia en todo el sistema.  
Actualmente, no existe un mecanismo claro para propagar estos cambios de estado. Sin sincronización adecuada, los pedidos pueden quedar en estados desactualizados, lo que afecta la experiencia del cliente y la interoperabilidad entre microservicios.  
**Pregunta clave**: ¿Cómo sincronizar los estados de los pedidos entre los microservicios de Gestión de Rutas y Pedidos de manera eficiente y consistente?

### Decision Drivers
- **Consistencia Eventual**: Los estados actualizados deben reflejarse en Pedidos con una latencia aceptable (<5 segundos).
- **Escalabilidad**: La solución debe soportar miles de actualizaciones concurrentes sin comprometer el rendimiento.
- **Rendimiento**: Evitar retrasos significativos en el proceso de entrega debido a la sincronización.
- **Interoperabilidad**: Garantizar que el microservicio de Pedidos pueda consumir y procesar los cambios de estado de manera eficiente.

### Considered Options

1. **Eventos del Dominio (Domain Events)**
   - Generar eventos como PedidoEntregado o PedidoConIncidencia desde el microservicio de Gestión de Rutas.
   - Publicar los eventos en un sistema de mensajería (e.g., RabbitMQ, Kafka) para que Pedidos los consuma y actualice su estado.

2. **API Síncrona**
   - Exponer un endpoint REST en Pedidos que el microservicio de Gestión de Rutas llame para actualizar directamente el estado del pedido al finalizar cada entrega.

3. **Base de Datos Compartida**
   - Usar una tabla compartida entre ambos microservicios donde Gestión de Rutas escriba directamente los cambios de estado y Pedidos los lea para sincronizarse.

### Decision Outcome
**Chosen option**: **Eventos del Dominio (Domain Events)**, porque:
- Desacopla la lógica de actualización de estados entre los microservicios.
- Es más escalable que las APIs síncronas y evita el impacto de latencias en llamadas directas.
- Permite manejar actualizaciones de estado en tiempo real, cumpliendo con los requisitos de consistencia eventual.
- Facilita la integración de futuros consumidores (e.g., microservicios de Notificaciones o Estadísticas).

### Consequences
**Good**, because:
- **Consistencia asegurada**: Los eventos garantizan que los estados de los pedidos se actualicen en Pedidos con baja latencia.
- **Escalabilidad**: El sistema de mensajería soporta miles de actualizaciones concurrentes sin impactar la carga del microservicio de Gestión de Rutas.
- **Desacoplamiento**: La arquitectura es más modular, lo que facilita cambios futuros.

**Bad**, because:
- **Complejidad adicional**: Requiere infraestructura de mensajería (RabbitMQ, Kafka) y monitoreo de eventos.
- **Latencia eventual**: Aunque baja (<5 segundos), puede ser un problema en casos con requerimientos de consistencia estricta.

### Confirmation
La implementación se validará mediante:
- **Pruebas de consistencia**: Verificar que los eventos sincronizan correctamente los estados en el microservicio de Pedidos.
- **Pruebas de rendimiento**: Evaluar que la latencia de sincronización no exceda los 5 segundos bajo carga máxima.
- **Simulación de fallos**: Probar que el sistema maneja correctamente eventos perdidos o duplicados.

### Pros and Cons of the Options

- **Option 1: Domain Events (Chosen)**
  - **Good**, because:
    - Desacopla completamente la lógica entre los microservicios.
    - Es adecuado para escenarios de alta concurrencia y escalabilidad.
  - **Bad**, because:
    - Introduce complejidad en el manejo de eventos y su monitoreo.

- **Option 2: API Síncrona**
  - **Good**, because:
    - Es más simple de implementar inicialmente.
    - Permite control directo sobre las actualizaciones de estado.
  - **Bad**, because:
    - Es menos escalable debido a las llamadas directas.
    - Introduce una dependencia fuerte entre los microservicios.

- **Option 3: Base de Datos Compartida**
  - **Good**, because:
    - Simplifica la sincronización al usar una única fuente de verdad.
  - **Bad**, because:
    - Va en contra de los principios de microservicios al acoplarlos mediante una base de datos compartida.
    - Es difícil de escalar y mantener.

### More Information
**Herramientas sugeridas**:
- **RabbitMQ**, **Kafka** para mensajería; **ElasticSearch** para rastreo de eventos.

**Pasos futuros**:
- Diseñar eventos PedidoEntregado y PedidoConIncidencia.
- Configurar colas específicas para sincronización con el microservicio de Pedidos.
