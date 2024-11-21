# Prioridad de Requerimientos y Atributos de Calidad

## Introducción
Este documento presenta una tabla de priorización que evalúa los requerimientos funcionales y los atributos de calidad en términos de criticidad, complejidad e importancia. Su propósito es guiar el proceso de diseño, priorizando servicios y atributos clave para las iteraciones.

---

## Tabla de Requerimientos Funcionales

| **Requerimiento Funcional**     | **Criticidad** | **Complejidad** | **Importancia** | **Dependencias** | **Justificación**                                                                                  |
|---------------------------------|----------------|-----------------|-----------------|------------------|--------------------------------------------------------------------------------------------------|
| Gestión de Clientes             | Alta           | Media           | Alta            | Alta             | Es la base de datos utilizada por otros módulos, como Pedidos y Reparto. Funcionalidad crítica para el sistema.                                       |
| Gestión de Pedidos              | Alta           | Alta            | Alta            | Alta             | Servicio clave que requiere transiciones de estado y validaciones externas (Clientes, Inventario).|
| Procesamiento de Pagos          | Alta           | Alta            | Alta            | Baja             | Involucra integración segura con MercadoLibre. Es fundamental para la transacción de negocio.                                                   |
| Gestión de Reparto y Rutas      | Alta           | Alta            | Alta            | Media            | Crucial para la entrega de productos; depende de Pedidos.                                       |
| Estadísticas                    | Media          | Media           | Media           | Baja             | Provee información útil pero no crítica.                                                        |
| Gestión de Incidencias          | Media          | Media           | Media           | Media            | Apoya la Gestión de Reparto y Rutas, pero no es esencial para la operación del sistema en tiempo real.                                                    |
| Notificaciones de Estado        | Media          | Media           | Media           | Baja             | Mejora la experiencia del cliente, pero no afecta operaciones críticas.                         |
| Auditoría y Registro            | Alta           | Media           | Alta            | Media            | Esencial para cumplimiento de regulaciones y seguridad del sistema, pero no afecta la operación directa del sistema.                                          |
| Gestión de Usuarios y Roles     | Baja           | Baja            | Media           | Baja             | Importante para acceso seguro pero no afecta operaciones críticas.                              |


## Tabla de Atributos de Calidad

| **Atributo de Calidad**         | **Criticidad** | **Complejidad** | **Importancia** | **Justificación**                                                                                  |
|---------------------------------|----------------|-----------------|-----------------|--------------------------------------------------------------------------------------------------|
| Escalabilidad                   | Alta           | Alta            | Alta            | Fundamental para soportar aumentos de carga, especialmente en Pedidos y Pagos.                                                       |
| Disponibilidad                  | Alta           | Alta            | Alta            | Esencial para garantizar que los servicios críticos (Pagos, Pedidos) estén operativos ante fallas.                                   |
| Seguridad                       | Alta           | Alta            | Alta            | Crítica para proteger los datos de clientes y pagos, y asegurar la autenticidad de las transacciones.                                |
| Mantenibilidad                  | Media          | Media           | Alta            | Facilita la evolución del sistema y reduce el riesgo de errores en despliegues y actualizaciones.                                   |
| Rendimiento                     | Alta           | Alta            | Alta            | Esencial para asegurar tiempos de respuesta bajos en servicios como Pedidos y Pagos.                                                |
| Usabilidad                      | Media          | Media           | Media           | Mejora la experiencia del usuario, pero no afecta directamente la operación principal del sistema.                                  |
| Interoperabilidad               | Media          | Alta            | Alta            | Necesaria para la integración con servicios externos como MercadoLibre y herramientas de optimización de rutas.                     |
| Portabilidad                    | Baja           | Baja            | Baja            | Útil para adaptarse a cambios de infraestructura en el futuro, pero no afecta la operación actual.                                  |
| Confiabilidad                   | Alta           | Media           | Alta            | Reduce los riesgos de interrupciones en servicios críticos si un servicio secundario falla.                                          |


# Criterios de Evaluación

## Criticidad: 
- Evalúa el impacto que un módulo o atributo tiene en el sistema si no está disponible o falla. Puede ser:
    - **Alta**: Impacta directamente en el éxito del sistema (funcionalidad central o driver clave).
    - **Media**: Importante para el soporte de funcionalidades críticas, pero no afecta directamente el éxito.
    - **Baja**: No afecta la operación directa del sistema, pero aporta valor agregado.

## Complejidad:
- Mide la dificultad técnica de implementar el requerimiento o atributo. Puede ser:
    - **Alta**: Requiere lógica avanzada, múltiples dependencias, o integra sistemas externos.
    - **Media**: Requiere una implementación estándar con cierta lógica adicional.
    - **Baja**: Sencillo de implementar, sin dependencias complejas.

## Importancia:
- Evalúa qué tan relevante es el requerimiento o atributo para alcanzar los objetivos del negocio. Puede ser:
    - **Alta**: Necesario para cumplir con los objetivos del negocio y los drivers arquitectónicos.
    - **Media**: Apoya el cumplimiento de los objetivos, pero no es crucial.
    - **Baja**: Su ausencia no pone en riesgo el éxito del sistema.

## Dependencias:
- Reflejan cómo un requerimiento funcional necesita otros módulos, servicios o sistemas para funcionar correctamente. Ayudan a priorizar según el impacto de estas relaciones en el desarrollo y la operación. Puede ser:
    - **Alta**: Requiere múltiples módulos o integraciones críticas. Su falta bloquea la funcionalidad.
    - **Media**: Tiene algunas dependencias importantes, pero no son críticas.
    - **Baja**: Pocas o ninguna dependencia. Puede funcionar de forma autónoma.
