# Resultados de la Iteración 1

## Resumen de las Decisiones

En esta iteración se tomaron cuatro decisiones clave para el diseño del microservicio de Gestión de Pedidos, enfocadas en garantizar la escalabilidad, consistencia y resiliencia del sistema:

1. **Uso de CQRS:**  
   Separación de comandos y consultas para optimizar rendimiento y escalabilidad.  

2. **Sincronización de eventos de dominio:**  
   Implementación de eventos para mantener consistencia eventual entre los modelos de datos de comandos y consultas.  

3. **Máquina de estados para transiciones de pedidos:**  
   Definición de transiciones entre los estados Preprocesado → Autorización → Aceptación, y establecimiento de validaciones para garantizar consistencia.  

4. **Elección de Apache Kafka como middleware de mensajería:**  
   Selección de Kafka como solución escalable y persistente para manejar eventos entre microservicios.  

---

## Referencias a Documentación Inicial
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).

---

## Puntos Clave

1. **Optimización de consultas:**  
   Se observaron mejoras en los tiempos de respuesta para operaciones de lectura gracias a la separación de modelos de datos para lectura y escritura mediante CQRS.  

2. **Sincronización eficiente:**  
   Los eventos de dominio garantizan la consistencia eventual entre los modelos de comandos y consultas con una latencia aceptable.  

3. **Automatización de transiciones:**  
   La máquina de estados asegura que todas las transiciones de pedidos sean válidas y consistentes, incluso bajo carga.  

4. **Comunicación escalable:**  
   Kafka permite manejar grandes volúmenes de eventos distribuidos con baja latencia y alta disponibilidad.  

---

## Lecciones Aprendidas

1. **Desafíos iniciales con eventos:**  
   La sincronización de eventos introdujo una complejidad adicional, especialmente en la configuración inicial de Apache Kafka.  

2. **Curva de aprendizaje:**  
   Se necesitó tiempo para familiarizarse con los conceptos y herramientas relacionadas con CQRS, Kafka y máquinas de estados.  

3. **Pruebas de carga:**  
   Las consultas respondieron adecuadamente bajo carga concurrente, aunque la base de datos compartida para comandos y consultas limitó la escalabilidad completa.  

---

## Recomendaciones para la Siguiente Iteración

1. **Separar bases de datos:**  
   Implementar bases de datos independientes para comandos y consultas, mejorando la escalabilidad.  

2. **Refinar eventos de dominio:**  
   Incorporar más eventos para manejar transiciones complejas y optimizar la sincronización.  

3. **Expandir resiliencia:**  
   Evaluar más tácticas para manejar fallos en dependencias externas (e.g., servicio de clientes).  

---

## Artefactos Generados

1. **ADR sobre el uso de CQRS:**  
   Documento que registra la separación de comandos y consultas. [Ver ADR](../../ADRs/ADR_002_CQRS.md) 

2. **ADR sobre sincronización de eventos de dominio:**  
   Documento para garantizar consistencia eventual entre los modelos de datos.  [Ver ADR](../../ADRs/ADR_003_Domain_Event_Synchronization.md)

3. **ADR sobre máquina de estados para transiciones de pedidos:**  
   Documento que define las transiciones y resiliencia.  [Ver ADR](../../ADRs/ADR_004_State_Machine_and_Resilience_Tactics.md)

4. **ADR sobre la elección de Apache Kafka como middleware de mensajería:**  
   Documento que detalla la solución seleccionada para comunicación asincrónica.  [Ver ADR](../../ADRs/ADR_005_Kafka_Middleware_Mensajería.md) 

