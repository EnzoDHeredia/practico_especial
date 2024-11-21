# Resultados de la Iteración 3

## Resumen de las Decisiones
En esta iteración, se tomaron tres decisiones clave para el diseño del microservicio de Gestión de Rutas y Reparto, enfocadas en mejorar la escalabilidad, resiliencia y consistencia del sistema:

1. **Dynamic Selection and Decoupling of Route Optimization Algorithms**:
   - Implementación del patrón Strategy para desacoplar y seleccionar dinámicamente algoritmos de optimización de rutas en función de métricas como la demora de camiones.

2. **Real-Time Incident Management for Route and Delivery Optimization**:
   - Uso de mensajería basada en eventos (e.g., RabbitMQ, Kafka) para manejar incidencias en tiempo real, minimizando su impacto operativo.

3. **Synchronizing Delivery States Between Gestión de Rutas and Pedidos**:
   - Implementación de eventos de dominio (PedidoEntregado, PedidoConIncidencia) para sincronizar estados entre servicios y garantizar consistencia eventual.

## Referencias a Documentación Inicial
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).

## Puntos Clave
- **Optimización de rutas**: Se desacoplaron los algoritmos existentes y se implementó una lógica dinámica para su selección, reduciendo la complejidad del mantenimiento y facilitando la incorporación de nuevos algoritmos.
- **Gestión de incidencias**: El sistema ahora puede registrar, notificar y reasignar rutas en tiempo real, mejorando la resiliencia operativa.
- **Consistencia entre servicios**: Los estados de los pedidos se sincronizan eficientemente con el microservicio de Pedidos, manteniendo la experiencia del cliente intacta.

## Lecciones Aprendidas
- **Evolución de algoritmos**: Desacoplar la lógica de optimización permite probar y evolucionar los algoritmos de manera independiente.
- **Mensajería distribuida**: Aunque potente, la infraestructura de mensajería requiere monitoreo constante para evitar puntos únicos de fallo.
- **Sincronización de eventos**: La latencia en la sincronización de estados (aunque aceptable) debe ser monitoreada continuamente para evitar inconsistencias prolongadas.

## Recomendaciones para la Siguiente Iteración
- **Escalar la infraestructura de mensajería**: Implementar clústeres redundantes para garantizar alta disponibilidad.
- **Refinar la selección de algoritmos**: Incorporar métricas adicionales, como el tráfico en tiempo real, para mejorar la precisión de las rutas.
- **Ampliar la gestión de incidencias**: Permitir que los gestores modifiquen manualmente rutas asignadas en escenarios complejos.

## Artefactos Generados
- **ADR sobre el patrón Strategy para algoritmos de optimización de rutas**: [Ver ADR](../../ADRs/ADR_008_Route_Optimization_Algorithms.md)
- **ADR sobre el sistema de mensajería para gestión de incidencias**: [Ver ADR](../../ADRs/ADR_009_Real_Time_Incident_Management.md)
- **ADR sobre sincronización de estados de pedidos mediante eventos de dominio**: [Ver ADR](../../ADRs/ADR_010_Synchronizing_Delivery_States.md)
