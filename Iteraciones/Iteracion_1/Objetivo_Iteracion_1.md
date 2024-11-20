# Objetivo de la Iteración 1

## Descripción

En la Iteración 1, el enfoque estará en el diseño y desarrollo del microservicio de Gestión de Pedidos, priorizando los aspectos funcionales y no funcionales definidos en la documentación inicial. Este microservicio es crítico para el sistema, ya que maneja la creación, consulta y actualización de pedidos, y debe garantizar que las transiciones entre estados sean válidas y consistentes.

---

## Referencias a Documentación Inicial

## Referencias a Documentación Inicial
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).

---

## Objetivos Específicos

1. **Diseñar el microservicio de Gestión de Pedidos** siguiendo el patrón **CQRS**, separando comandos y consultas en capas independientes.  
2. **Implementar las operaciones principales del servicio:**
   - Crear un pedido (**comando**).
   - Consultar pedidos (**consulta**).
   - Actualizar el estado de un pedido (**comando**).  
3. **Modelar las transiciones de estado del pedido:**  
   - Preprocesado → Autorización → Aceptación.  
4. **Definir un esquema inicial para la persistencia de datos** utilizando una base de datos SQL.  
5. **Establecer tácticas de resiliencia** para manejar dependencias externas (e.g., Servicio de Clientes).  
6. **Optimizar la comunicación de eventos entre microservicios** utilizando una solución de middleware adecuada.

---

## Drivers Clave

- **Escalabilidad:** Diseñar para soportar picos de carga y grandes volúmenes de datos.  
- **Disponibilidad:** Garantizar un tiempo de actividad del 99.9%.  
- **Rendimiento:** Tiempo de respuesta menor a 1 segundo para consultas frecuentes y creación de pedidos.  
- **Consistencia:** Mantener datos coherentes, incluso en caso de fallos o latencia en la sincronización.

---

## Artefactos a Generar

1. **ADR sobre el uso de CQRS:**  
   Documento que registra la separación de comandos y consultas. [Ver ADR](../../ADRs/ADR_002_CQRS.md) 

2. **ADR sobre sincronización de eventos de dominio:**  
   Documento para garantizar consistencia eventual entre los modelos de datos.  [Ver ADR](../../ADRs/ADR_003_Domain_Event_Synchronization.md)

3. **ADR sobre máquina de estados para transiciones de pedidos:**  
   Documento que define las transiciones y resiliencia.  [Ver ADR](../../ADRs/ADR_004_State_Machine_and_Resilience_Tactics.md)

4. **ADR sobre la elección de Apache Kafka como middleware de mensajería:**  
   Documento que detalla la solución seleccionada para comunicación asincrónica.  [Ver ADR](../../ADRs/ADR_005_Kafka_Middleware_Mensajería.md)
