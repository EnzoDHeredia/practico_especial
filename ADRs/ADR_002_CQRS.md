# Microservicio de Gestión de Pedidos: Uso de CQRS

## Context and Problem Statement
El microservicio de Gestión de Pedidos es una pieza crítica del sistema, responsable de manejar la creación, consulta y actualización de pedidos. El sistema debe garantizar que las transiciones entre estados sean válidas y registrar cualquier cambio en el estado de los pedidos.
Además, se espera un crecimiento continuo en el volumen de datos y una alta carga de consultas concurrentes. Esto plantea desafíos en términos de rendimiento y escalabilidad.

La pregunta clave es: **¿cómo podemos diseñar un servicio que maneje eficientemente comandos y consultas, garantizando consistencia eventual, escalabilidad y rendimiento bajo alta carga?**

---

## Decision Drivers

- La necesidad de manejar un volumen creciente de pedidos y consultas concurrentes.
- La importancia de garantizar transiciones válidas entre estados del pedido.
- La flexibilidad para escalar comandos y consultas de manera independiente.
- La capacidad de optimizar el rendimiento de consultas frecuentes y de gran volumen.

---

## Considered Options

1. **CQRS (Command Query Responsibility Segregation)**
2. **Repository Pattern Tradicional**
3. **Repository Pattern con Cache (e.g., Redis)**

---

## Decision Outcome

**Chosen option:** **CQRS (Command Query Responsibility Segregation)**, porque permite separar las responsabilidades de comandos y consultas, optimizando ambas operaciones y facilitando la escalabilidad a medida que aumenta la carga del sistema. Es la única opción que aborda adecuadamente todos los drivers clave.

---

## Consequences

### Good:
- **Escalabilidad óptima:** Las consultas pueden manejarse con bases de datos optimizadas para lectura, mientras que los comandos permanecen consistentes en una base de datos SQL.
- **Consultas rápidas y eficientes:** Los datos de consulta se estructuran específicamente para operaciones de lectura intensiva.
- **Separación de responsabilidades:** Facilita mantener comandos y consultas desacoplados.
- **Flexibilidad tecnológica:** Permite usar diferentes tecnologías para lectura y escritura.

### Bad:
- **Complejidad adicional:** La arquitectura requiere sincronización entre modelos de datos para comandos y consultas.
- **Latencia para datos consistentes:** Las consultas pueden reflejar datos desactualizados debido a la consistencia eventual.
- **Curva de aprendizaje:** El equipo necesita familiarizarse con el diseño y sincronización de eventos de dominio.

---

## Confirmation

Para validar esta decisión, se implementará inicialmente una versión simplificada de CQRS:

1. **Comandos y consultas usarán una base de datos común** durante la primera iteración.
2. Se medirán **tiempos de respuesta y manejo de carga** para determinar si es necesario separar las bases de datos en futuras iteraciones.
3. Se implementarán **pruebas automáticas** para asegurar que las transiciones de estado son válidas y que los datos son consistentes.
4. **Revisiones de diseño y código** confirmarán la correcta separación de responsabilidades y la implementación de eventos de sincronización.

---

## Pros and Cons of the Options

### Option 1: CQRS (Chosen)
**Good, because:**
- Proporciona escalabilidad al manejar comandos y consultas de manera independiente.
- Optimiza las consultas al estructurar datos específicamente para lecturas.
- Facilita la evolución tecnológica permitiendo diferentes herramientas para lectura y escritura.

**Bad, because:**
- Introduce complejidad adicional y un aprendizaje inicial para el equipo.
- Puede ser innecesariamente complejo si el volumen de datos o consultas no crece significativamente.

### Option 2: Repository Pattern Tradicional
**Good, because:**
- Sencillo de implementar, con lógica centralizada y consistente.
- Garantiza consistencia en todas las operaciones al usar un único modelo de datos.

**Bad, because:**
- Menor escalabilidad: Puede convertirse en un cuello de botella bajo alta carga.
- Consultas menos optimizadas: Todas las operaciones comparten la misma base de datos y estructura.

### Option 3: Repository Pattern con Cache
**Good, because:**
- Optimiza consultas frecuentes usando sistemas de cache (e.g., Redis).
- Es más simple que CQRS, con un equilibrio razonable entre rendimiento y consistencia.

**Bad, because:**
- Consistencia eventual: Las consultas pueden devolver datos desactualizados del cache.
- Puede no ser suficiente si las consultas se vuelven intensivas y los datos crecen rápidamente.

---

## More Information

Este diseño será revisado cada 6 meses para evaluar su efectividad frente al crecimiento del sistema. La decisión se puede reexaminar si:
- El volumen de datos o consultas no aumenta como se esperaba.
- Las consultas no requieren optimización significativa.
- Los costos de mantenimiento de CQRS superan los beneficios obtenidos.
