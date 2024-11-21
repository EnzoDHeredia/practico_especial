# Dynamic Selection and Decoupling of Route Optimization Algorithms

### Context and Problem Statement
El microservicio de Gestión de Rutas y Reparto debe gestionar el reparto de las flotas de transporte, optimizando rutas en función de los pedidos y clientes asignados. Según el enunciado, este servicio cuenta con dos algoritmos de optimización que se seleccionan dinámicamente en función de la demora de los camiones.  
Actualmente, los algoritmos no están desacoplados del flujo principal del servicio, lo que dificulta su mantenimiento, evolución y prueba independiente. Además, la selección dinámica no está claramente definida, lo que introduce complejidad en la lógica del servicio.  
**Pregunta clave**: ¿Cómo desacoplar e implementar dinámicamente la selección de algoritmos de optimización para mejorar la mantenibilidad y escalabilidad del servicio?

### Decision Drivers
- **Escalabilidad**: Garantizar que el servicio pueda manejar grandes volúmenes de datos (e.g., 500 camiones y 1000 pedidos simultáneos) sin degradación.
- **Mantenibilidad**: Desacoplar los algoritmos para permitir su evolución y prueba independiente.
- **Rendimiento**: Seleccionar dinámicamente el algoritmo más eficiente en función del contexto (e.g., retrasos en rutas).
- **Flexibilidad**: Permitir que se añadan nuevos algoritmos en el futuro sin modificar la lógica principal del servicio.

### Considered Options

1. **Implementar un patrón de estrategia (Strategy Pattern)**
   - Definir una interfaz común para los algoritmos de optimización, implementando cada uno como una estrategia independiente.
   - Usar una lógica central para seleccionar dinámicamente la estrategia adecuada según las métricas de demora.

2. **Usar un servicio externo de optimización**
   - Delegar la lógica de optimización a un servicio externo, como Google Maps API o Mapbox, que ofrezca rutas optimizadas basadas en datos de entrada.
   - El servicio manejaría la selección de rutas y algoritmos automáticamente.

3. **Crear una capa adicional de abstracción interna**
   - Desacoplar completamente la lógica de selección y ejecución de algoritmos en una capa dedicada dentro del microservicio.
   - La capa recibiría las métricas de entrada y decidiría qué algoritmo ejecutar, encapsulando esta decisión del resto del servicio.

### Decision Outcome
**Chosen option**: **Implementar un patrón de estrategia (Strategy Pattern)**, porque:
- Permite desacoplar los algoritmos, facilitando su mantenimiento y prueba independiente.
- Es una solución escalable que se alinea con la lógica interna del microservicio y no depende de servicios externos.
- Ofrece flexibilidad para incorporar nuevos algoritmos sin modificar el flujo principal del servicio.

### Consequences
**Good**, because:
- **Mantenibilidad**: Los algoritmos están desacoplados y pueden evolucionar de manera independiente.
- **Flexibilidad**: Nuevos algoritmos pueden añadirse fácilmente.
- **Rendimiento**: La selección dinámica asegura el uso del algoritmo más eficiente según las métricas de demora.

**Bad**, because:
- Introduce complejidad adicional en la lógica de selección y ejecución de algoritmos.
- Requiere una planificación cuidadosa para evitar que la lógica de selección se vuelva un cuello de botella.

### Confirmation
La implementación del patrón se validará mediante:
- **Pruebas unitarias**: Validar que cada algoritmo produce rutas óptimas para sus casos de uso específicos.
- **Pruebas de integración**: Asegurar que la selección dinámica funciona correctamente bajo diferentes escenarios de demora.
- **Monitoreo de rendimiento**: Medir el tiempo de cálculo de rutas para garantizar que se mantiene por debajo de los 2 segundos en promedio.

### Pros and Cons of the Options

- **Option 1: Strategy Pattern (Chosen)**
  - **Good**, because:
    - Simplifica el mantenimiento de algoritmos.
    - Alinea la implementación con principios de diseño modular y flexible.
  - **Bad**, because:
    - Requiere lógica adicional para la selección dinámica.

- **Option 2: Servicio Externo**
  - **Good**, because:
    - Reduce la carga de implementar y mantener algoritmos internamente.
    - Ofrece soluciones listas para usar con alta confiabilidad.
  - **Bad**, because:
    - Introduce dependencia de terceros, lo que puede impactar la disponibilidad del servicio.
    - Incrementa costos operativos si el proveedor es de pago.

- **Option 3: Abstracción Interna**
  - **Good**, because:
    - Encapsula completamente la lógica de selección y ejecución de algoritmos.
    - Facilita la evolución de la arquitectura interna.
  - **Bad**, because:
    - Puede complicar el diseño al añadir otra capa de abstracción.
    - No mejora significativamente sobre el patrón de estrategia en términos de resultados prácticos.

### More Information
**Tecnologías sugeridas**:
- **Algoritmos**: Dijkstra, Algoritmos Genéticos.
- **Frameworks**: Spring para la implementación del patrón de estrategia.

**Pasos futuros**:
- Implementar métricas de demora que alimenten la lógica de selección de algoritmos.
- Definir escenarios de prueba para evaluar el rendimiento y la escalabilidad de la solución.
