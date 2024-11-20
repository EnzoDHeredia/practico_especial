# Domain Event Synchronization for Data Consistency in Gestión de Pedidos

## Context and Problem Statement
El microservicio de **Gestión de Pedidos** utiliza el patrón **CQRS** para separar las operaciones de comandos y consultas. Sin embargo, ambas operaciones comparten actualmente la misma base de datos, lo que limita la capacidad de escalar y mantener consistencia eventual entre modelos separados. 

La separación física de las bases de datos para comandos y consultas es necesaria, pero introduce el desafío de sincronizar ambos modelos para garantizar datos consistentes en el modelo de consultas.

**Pregunta clave:**  
¿Cómo sincronizar los datos entre las bases de datos de comandos y consultas de manera eficiente y consistente?

---

## Decision Drivers
- **Consistencia Eventual:**  
  Los datos del modelo de consultas deben reflejar los cambios realizados en comandos con una latencia aceptable (<5 segundos).
- **Escalabilidad:**  
  La solución debe permitir que los modelos de comandos y consultas escalen de forma independiente, soportando alta concurrencia.

---

## Considered Options
1. **Domain Event Synchronization (Elegida):**  
   Usar eventos del dominio para sincronizar cambios entre los modelos de comandos y consultas.
2. **Event Sourcing:**  
   Utilizar eventos como la fuente de verdad para reconstruir ambos modelos.
3. **Read-Write Split sin Sincronización Activa:**  
   Separar las bases de datos sin implementar un mecanismo activo de sincronización.

---

## Decision Outcome
### **Opción elegida:** Domain Event Synchronization
Esta opcion fue seleccionada porque:  
- Garantiza **consistencia eventual** entre los modelos de comandos y consultas.  
- Se integra fácilmente con el patrón CQRS existente.  
- Permite escalar cada modelo de manera independiente.

---

## Consequences
### **Good, because:**
- **Consistencia eventual asegurada:**  
  Los eventos del dominio sincronizan los modelos de datos con latencia aceptable.
- **Escalabilidad mejorada:**  
  Los modelos de comandos y consultas pueden escalar de forma independiente. 
- **Flexibilidad:**  
  Permite usar tecnologías especializadas para cada modelo de datos (e.g., PostgreSQL para comandos, ElasticSearch para consultas).

### **Bad, because:**
- **Complejidad adicional:**  
  Introduce complejidad en la gestión de eventos y monitoreo de sincronización.
- **Latencia en la sincronización:**  
  Podría ser problemático en casos de uso con requerimientos de consistencia estricta.

---

## Confirmation
La implementación del patrón se validará mediante:  
1. **Pruebas de consistencia:**  
   Verificar que los eventos sincronizan los datos en un tiempo máximo de 5 segundos.
2. **Pruebas de escalabilidad:**  
   Evaluar el rendimiento bajo carga concurrente alta.   
3. **Monitoreo de eventos:**  
   Usar herramientas de trazabilidad distribuida para garantizar que los eventos se procesan correctamente.

---

## Consequences of Other Options
### Opción 2: Event Sourcing
#### Ventajas:
- **Historial completo de cambios:**  
  Facilita la reconstrucción de los modelos desde los eventos, asegurando consistencia perfecta.  
- **Auditoría robusta:**  
  Ideal para escenarios que requieren un historial detallado de cada cambio.

#### Desventajas:
- **Complejidad significativa:**  
  Requiere rediseñar completamente la arquitectura actual para que los eventos sean la única fuente de verdad.  
- **Impacto en el rendimiento:**  
  El procesamiento adicional necesario para reconstruir estados puede afectar la latencia.  

### Opción 3: Read-Write Split sin Sincronización Activa
#### Ventajas:
- **Simplicidad:**  
  Es fácil de implementar, lo que mantiene bajo el nivel de complejidad del sistema.  
- **Reducción de carga:**  
  Reduce la carga en la base de datos principal al separar físicamente las operaciones de lectura y escritura.

#### Desventajas:
- **Inconsistencias de datos:**  
  No asegura consistencia entre los modelos de comandos y consultas.  
- **Procesos ineficientes:**  
  Depender de sincronización manual o por lotes no es práctico en entornos de alta concurrencia.  

---

## More Information
### Herramientas sugeridas:
- **RabbitMQ, Kafka** (para gestión de eventos).  
- **Prometheus, Grafana** (para monitoreo y trazabilidad).  
- **ElasticSearch** (para optimización del modelo de consultas).

### Pruebas futuras:
Configurar un pipeline para manejar eventos como **PedidoCreado**, **EstadoActualizado**, y verificar que sincronizan los datos correctamente en el modelo de consultas.
