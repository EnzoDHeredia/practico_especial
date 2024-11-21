# Resilience Pattern Selection for Payment Processing Service

## Context and Problem Statement

El microservicio de Procesamiento de Pagos debe integrarse con la pasarela de pago externa de MercadoLibre para procesar pagos de manera segura y eficiente. Sin embargo, las transacciones de pago pueden fallar debido a diversos factores, como problemas temporales de la pasarela de pago o caídas de red, lo que pone en riesgo la disponibilidad del sistema y la experiencia del cliente.

Para garantizar la resiliencia del sistema y la continuidad del servicio, es necesario implementar un patrón de diseño que permita gestionar de manera eficiente los fallos y asegurar que las transacciones sean procesadas de forma segura.

**Pregunta clave**: ¿Qué patrón de diseño debemos implementar para garantizar la resiliencia del microservicio de pagos frente a fallos y mantener la integridad de las transacciones?

---

## Decision Drivers

1. **Seguridad**: La solución debe garantizar que los pagos se procesen de manera segura, incluso en escenarios de fallos temporales.
2. **Resiliencia**: El sistema debe ser capaz de manejar fallos en la pasarela de pago y seguir funcionando correctamente sin afectar la experiencia del usuario.
3. **Escalabilidad**: La solución debe permitir manejar grandes volúmenes de pagos concurrentes sin degradar el rendimiento.
4. **Disponibilidad**: El sistema debe garantizar una alta disponibilidad del servicio, especialmente durante picos de tráfico y problemas temporales de la pasarela de pago.
5. **Rendimiento**: El sistema debe asegurar tiempos de respuesta rápidos y no agregar latencia significativa a las transacciones.

---

## Considered Options

### 1. Circuit Breaker Pattern
Implementar el patrón Circuit Breaker para gestionar fallos en la pasarela de pago externa. El Circuit Breaker se abriría automáticamente en caso de fallos recurrentes, evitando que el sistema siga intentando transacciones fallidas y afecte la disponibilidad.

**Pros**:
- Previene la sobrecarga del sistema debido a fallos continuos de la pasarela de pago.
- Mejora la resiliencia al permitir que el sistema se recupere automáticamente.

**Contras**:
- Puede introducir una pequeña latencia si no se configura correctamente.
- Requiere monitoreo para ajustar los umbrales de fallo.

---

### 2. Retry Pattern (Con Backoff Exponencial)
Implementar un patrón Retry con Backoff Exponencial para reintentar las transacciones fallidas, aumentando progresivamente el tiempo entre reintentos hasta un límite definido.

**Pros**:
- Mejora la tasa de éxito para pagos temporales fallidos.
- Es una solución sencilla de implementar.

**Contras**:
- No resuelve problemas de fallos persistentes en la pasarela de pago.
- Puede aumentar la latencia si los reintentos son demasiado frecuentes.

---

### 3. Event Sourcing
Usar Event Sourcing para registrar todas las transacciones de pago como eventos, lo que permite que los pagos fallidos sean reintentados o corregidos después, incluso si el proceso original falló.

**Pros**:
- Permite un historial completo y auditable de todas las transacciones.
- Proporciona una solución para los pagos fallidos, permitiendo reintentos de manera eficiente.

**Contras**:
- Aumenta la complejidad, ya que se necesita una infraestructura de eventos adicional.
- Puede afectar el rendimiento si no se maneja adecuadamente el almacenamiento y procesamiento de eventos.

---

## Decision Outcome

**Chosen option**: Circuit Breaker Pattern.

**Razones**:
- **Resiliencia**: Protege el sistema de fallos recurrentes en la pasarela de pago externa.
- **Escalabilidad y rendimiento**: Permite que el sistema continúe funcionando sin sobrecarga, incluso cuando la pasarela de pago está inoperativa temporalmente.
- **Seguridad**: Garantiza la integridad de las transacciones y evita intentos repetidos que puedan comprometer el servicio.

---

## Consequences

**Good**:
- Mejora la resiliencia del sistema, protegiéndolo de caídas masivas.
- Aumenta la disponibilidad del servicio al operar incluso durante fallos temporales.
- Reduce la carga del sistema al evitar intentos repetidos de pago fallidos.

**Bad**:
- Requiere monitoreo y ajustes finos para evitar problemas de latencia.
- Podría introducir complejidad adicional en la implementación y mantenimiento.

---

## Confirmation

La implementación del patrón se validará mediante:
1. **Pruebas de consistencia**: Verificar que las transacciones sean correctamente gestionadas, incluso si la pasarela de pago falla temporalmente.
2. **Pruebas de carga**: Medir el rendimiento del sistema bajo alta concurrencia.
3. **Monitoreo de eventos**: Supervisar los eventos del Circuit Breaker para ajustar dinámicamente los umbrales de fallo.

---

## Pros and Cons of the Options

### Option 1: Circuit Breaker Pattern (Chosen)
**Good**:
- Mejora la disponibilidad y resiliencia.
- Evita intentos fallidos repetidos, mejorando el rendimiento.

**Bad**:
- Requiere ajustes finos para evitar problemas.
- Puede necesitar soporte adicional para gestionar los fallos.

---

### Option 2: Retry Pattern with Backoff Exponential
**Good**:
- Incrementa la tasa de éxito en fallos temporales.
- Fácil de implementar.

**Bad**:
- No soluciona fallos persistentes.
- Puede introducir latencia por reintentos frecuentes.

---

### Option 3: Event Sourcing
**Good**:
- Trazabilidad completa de las transacciones.
- Facilita reintentos de pagos fallidos.

**Bad**:
- Incrementa la complejidad.
- Afecta el rendimiento si no se gestiona adecuadamente.

---

## More Information

**Herramientas sugeridas**:
- Spring Cloud Circuit Breaker
- Resilience4J
- Hystrix

**Pasos futuros**:
1. Implementar y probar el patrón Circuit Breaker con un servicio de pago de prueba.
2. Monitorear el impacto en el rendimiento y ajustar parámetros según los resultados.
