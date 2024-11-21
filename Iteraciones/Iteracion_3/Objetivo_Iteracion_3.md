# Objetivo de la Iteración 3

## Descripción

En la Iteración 3, el enfoque está en el diseño y desarrollo del microservicio de **Gestión de Rutas y Reparto**, abordando sus retos críticos relacionados con la escalabilidad, sincronización de estados y manejo de incidencias. Este microservicio es fundamental para optimizar las rutas de entrega, gestionar incidencias en tiempo real y mantener la consistencia de estados con otros servicios como **Pedidos**.

---

## Referencias a Documentación Inicial

1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).

---

## Objetivos Específicos

1. **Desacoplar y mejorar la selección de algoritmos de optimización de rutas:**
   - Implementar el patrón **Strategy** para permitir una selección dinámica de algoritmos en función de métricas como la demora de camiones.  
   - Facilitar la evolución y prueba independiente de los algoritmos.  

2. **Establecer un sistema centralizado para la gestión de incidencias en tiempo real:**
   - Usar **mensajería basada en eventos** para registrar, notificar y actuar sobre incidencias de manera eficiente.  
   - Reducir el impacto operativo de averías y retrasos en las rutas.  

3. **Sincronizar los estados de pedidos entre Gestión de Rutas y Pedidos:**
   - Implementar **Eventos de Dominio** para garantizar la consistencia eventual entre ambos servicios.  
   - Diseñar eventos como `PedidoEntregado` o `PedidoConIncidencia` para reflejar cambios de estado en tiempo real.  

---

## Drivers Clave

- **Escalabilidad:** Diseñar para manejar hasta 500 camiones y 1000 pedidos simultáneos.  
- **Rendimiento:** Asegurar tiempos de cálculo de rutas inferiores a 2 segundos y notificaciones de incidencias en menos de 1 segundo.  
- **Consistencia Eventual:** Mantener sincronizados los estados de los pedidos en todo momento con una latencia aceptable (<5 segundos).  
- **Resiliencia:** Garantizar que el sistema maneje fallos en infraestructura sin interrumpir operaciones críticas.  

---

## Artefactos a Generar

1. **ADR sobre el patrón Strategy para algoritmos de optimización de rutas:**  
   Documento que registra la decisión y su impacto en la mantenibilidad y escalabilidad del sistema.  [Ver ADR](../../ADRs/ADR_008_Route_Optimization_Algorithms.md)

2. **ADR sobre el sistema de mensajería basado en eventos para gestión de incidencias:**  
   Documento que detalla la solución para manejar incidencias en tiempo real.  [Ver ADR](../../ADRs/ADR_009_Real_Time_Incident_Management.md)

3. **ADR sobre sincronización de estados de pedidos mediante eventos de dominio:**  
   Documento que justifica el uso de eventos para mantener consistencia eventual.  [Ver ADR](../../ADRs/ADR_010_Synchronizing_Delivery_States.md)
