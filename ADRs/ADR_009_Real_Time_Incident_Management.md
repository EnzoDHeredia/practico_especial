# Real-Time Incident Management for Route and Delivery Optimization

### Context and Problem Statement
El microservicio de Gestión de Rutas y Reparto debe gestionar incidencias que ocurren durante el proceso de entrega, como averías de vehículos o retrasos en rutas. Estas incidencias pueden impactar la experiencia del cliente y la eficiencia operativa, por lo que es crítico detectarlas y manejarlas en tiempo real.  
Actualmente, no existe un mecanismo centralizado para registrar, notificar y actuar sobre las incidencias. Las decisiones operativas se toman manualmente, lo que retrasa las respuestas y afecta la eficiencia del servicio.  
**Pregunta clave**: ¿Cómo gestionar incidencias en tiempo real, asegurando que el sistema sea resiliente y minimizando el impacto en el reparto?

### Decision Drivers
- **Disponibilidad**: Asegurar que las incidencias no paralicen las operaciones del servicio.
- **Escalabilidad**: Manejar un volumen creciente de incidencias (hasta 500 camiones operativos).
- **Tiempo de Respuesta**: Detectar y notificar incidencias en menos de 1 segundo desde su ocurrencia.
- **Flexibilidad**: Permitir que el sistema evolucione para soportar nuevos tipos de incidencias en el futuro.

### Considered Options

1. **Sistema de Mensajería Basado en Eventos**
   - Usar una herramienta de mensajería como RabbitMQ o Kafka para registrar incidencias en tiempo real y disparar notificaciones automáticas.
   - Permitir la reasignación dinámica de rutas mediante la emisión de eventos a consumidores interesados.

2. **Registro Centralizado de Incidencias con API**
   - Almacenar las incidencias en una base de datos centralizada, exponiendo una API que permita consultas y actualizaciones.
   - Notificar a los gestores de rutas a través de una integración con un módulo de notificaciones.

3. **Notificación Manual y Gestión Reactiva**
   - Registrar las incidencias en tiempo real pero delegar la decisión de respuesta al gestor de rutas, quien ajustaría manualmente las asignaciones.

### Decision Outcome
**Chosen option**: **Sistema de Mensajería Basado en Eventos**, porque:
- Ofrece la capacidad de manejar incidencias en tiempo real de manera eficiente y escalable.
- Desacopla la lógica de detección, notificación y reasignación de rutas, lo que facilita la evolución del sistema.
- Es compatible con las arquitecturas de microservicios existentes y permite integrar consumidores adicionales en el futuro (e.g., sistemas de monitoreo).

### Consequences
**Good**, because:
- **Escalabilidad asegurada**: Maneja un alto volumen de incidencias sin afectar el rendimiento del sistema.
- **Tiempo de respuesta optimizado**: Las incidencias se procesan en tiempo real mediante eventos.
- **Flexibilidad**: Nuevos tipos de incidencias o procesos relacionados pueden añadirse sin afectar el flujo principal.

**Bad**, because:
- Introduce complejidad adicional en la gestión de eventos y su monitoreo.
- Requiere infraestructura adicional (e.g., servidores RabbitMQ o Kafka) y monitoreo para evitar puntos únicos de fallo.

### Confirmation
La implementación del sistema se validará mediante:
- **Pruebas de carga**: Evaluar la capacidad del sistema para manejar hasta 1000 incidencias concurrentes.
- **Pruebas de tiempo de respuesta**: Medir el tiempo desde que se registra una incidencia hasta que se notifica a los gestores de rutas.
- **Pruebas de resiliencia**: Simular fallos en el sistema de mensajería y verificar que las incidencias se procesan correctamente al restaurar el servicio.

### Pros and Cons of the Options

- **Option 1: Sistema de Mensajería Basado en Eventos (Chosen)**
  - **Good**, because:
    - Desacopla los procesos de registro, notificación y reasignación.
    - Facilita la integración con nuevos sistemas de monitoreo o análisis de datos.
    - Soporta escenarios de alta concurrencia.
  - **Bad**, because:
    - Complejidad adicional en la implementación y mantenimiento.
    - Requiere monitoreo constante para garantizar su disponibilidad.

- **Option 2: Registro Centralizado de Incidencias con API**
  - **Good**, because:
    - Es más simple de implementar y operar inicialmente.
    - Centraliza los datos para su análisis histórico.
  - **Bad**, because:
    - No procesa incidencias en tiempo real, lo que aumenta el tiempo de respuesta.
    - Escalabilidad limitada si el volumen de incidencias crece rápidamente.

- **Option 3: Notificación Manual y Gestión Reactiva**
  - **Good**, because:
    - Minimiza la complejidad técnica inicial.
  - **Bad**, because:
    - Retrasos significativos en la respuesta a incidencias.
    - Dependencia excesiva de la intervención humana, lo que reduce la eficiencia operativa.

### More Information
**Herramientas sugeridas**:
- **RabbitMQ**, **Kafka** para mensajería; **Prometheus** y **Grafana** para monitoreo.

**Pasos futuros**:
- Configurar colas de mensajería para los tipos de incidencias más comunes (e.g., CamionAveriado, RetrasoEnRuta).
- Integrar un sistema de notificaciones para alertar a los gestores de rutas.
