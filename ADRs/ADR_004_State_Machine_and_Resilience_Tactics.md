# State Machine for Pedido Transitions and Resilience Tactics  
### **Context and Problem Statement**  
El microservicio de Gestión de Pedidos gestiona pedidos a través de tres estados principales: **Preprocesado → Autorización → Aceptación**. Actualmente, las transiciones entre estos estados no están modeladas explícitamente, lo que introduce el riesgo de que los pedidos avancen a estados inválidos.  
Además, el microservicio depende del **Servicio de Clientes** para validar información esencial, como el estado del cliente. Las fallas o tiempos de respuesta prolongados en este servicio podrían interrumpir el flujo de procesamiento, impactando negativamente en la disponibilidad y confiabilidad del sistema.  

**Pregunta clave:**  
1. ¿Cómo garantizar que los pedidos solo avancen entre estados válidos?  
2. ¿Cómo manejar la resiliencia ante fallos en dependencias externas?

---

#### **Decision Drivers**  
1. **Consistencia:** Evitar transiciones inválidas o inconsistentes entre los estados del pedido.  
2. **Disponibilidad:** Asegurar que el microservicio siga funcionando incluso cuando el Servicio de Clientes esté temporalmente inactivo o lento. 

---

#### **Considered Options**  
1. **Modelar transiciones con State Machine**  
   - Implementar un patrón de máquina de estados para gestionar las transiciones de estado del pedido.  
   - Validar las reglas de negocio antes de permitir cambios de estado.  
2. **Implementar Circuit Breaker y Retries con Backoff**  
   - Utilizar tácticas de resiliencia para manejar fallos en el Servicio de Clientes, permitiendo reintentos controlados y cortocircuitos ante fallos persistentes.  
3. **Flujos de Validación Manuales**
    - En lugar de automatizar las transiciones de estado con una máquina de estados, las validaciones podrían realizarse manualmente en el código, mediante funciones independientes que comprueban las reglas de negocio.

---

#### **Decision Outcome**  
**Chosen option:**  
1. **State Machine for Pedido Transitions**:  
   - Se implementará un patrón de máquina de estados para modelar y controlar las transiciones entre **Preprocesado → Autorización → Aceptación**, validando las reglas de negocio en cada transición.  
2. **Circuit Breaker and Retries**:  
   - Se utilizará Resilience4j para implementar un Circuit Breaker y reintentos con backoff exponencial para manejar dependencias externas como el Servicio de Clientes.  
#### **Consequences**  
**Good, because:**  
- **Consistencia mejorada:** Los pedidos solo avanzan entre estados válidos, evitando errores lógicos.  
- **Resiliencia asegurada:** El microservicio puede manejar fallos en dependencias externas sin interrumpir su funcionamiento.  

**Bad, because:**  
- **Complejidad adicional:** Implementar y mantener una máquina de estados y tácticas de resiliencia introduce más complejidad en el sistema.  
- **Latencia potencial:** Retrasos en reintentos podrían impactar el tiempo total de procesamiento del pedido.  


#### **Confirmation**  
La implementación se validará mediante:  
1. **Pruebas unitarias:** Validar que las transiciones de estado respetan las reglas de negocio definidas.  
2. **Simulación de fallos:** Probar que el Circuit Breaker y los reintentos manejan correctamente los fallos en el Servicio de Clientes.  

#### **Pros and Cons of the Options**  
**Option 1: State Machine for Pedido Transitions**  
- **Good, because:**  
  - Simplifica la gestión de estados y reduce errores lógicos.  
  - Hace explícitas las reglas de negocio para cada transición.  

- **Bad, because:**  
  - Introduce una capa adicional de lógica que debe ser documentada y mantenida.  
**Option 2: Circuit Breaker and Retries**  
- **Good, because:**  
  - Permite manejar fallos en servicios externos de manera controlada.  
  - Mejora la disponibilidad general del microservicio.  
- **Bad, because:**  
  - Requiere monitoreo activo para garantizar que las políticas de resiliencia funcionen como se espera.  
**Option 3: Flujos de Validación Manuales**
- **Good, because***
    - Simplicidad inicial en términos de diseño.
    - No requiere integrar una biblioteca o framework adicional.
- **Bad, because**
    - Propenso a errores, ya que no hay un mecanismo explícito que controle las transiciones.
    - Dificultad para mantener reglas de negocio complejas.
    - Incrementa el riesgo de inconsistencias si las validaciones no están centralizadas.

#### **More Information**  
- **Herramientas sugeridas:**  
   - State Machine: Spring State Machine, XState.  
   - Circuit Breaker: Resilience4j, Hystrix.  
   - Monitoreo: Prometheus, Grafana.  
- **Pruebas futuras:**  
   - Validar transiciones de estado mediante casos de prueba exhaustivos. 
   - Simular fallos del Servicio de Clientes y medir el impacto en tiempos de procesamiento.  