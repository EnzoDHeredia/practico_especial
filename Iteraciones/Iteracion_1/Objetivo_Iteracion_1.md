# Objetivo de la Iteración 1

## Descripción
En la Iteración 1, el enfoque estará en el diseño y desarrollo del microservicio de **Gestión de Pedidos**, priorizando los aspectos funcionales y no funcionales definidos en la documentación inicial. Este microservicio es crítico para el sistema, ya que maneja la creación, consulta y actualización de pedidos, y debe garantizar que las transiciones entre estados sean válidas y consistentes.

## Referencias a Documentación Inicial
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).

## Objetivos Específicos
1. Diseñar el microservicio de Gestión de Pedidos siguiendo el patrón CQRS, separando comandos y consultas en capas independientes.
2. Implementar las operaciones principales del servicio:  
   - Crear un pedido (comando).  
   - Consultar pedidos (consulta).  
   - Actualizar el estado de un pedido (comando).
3. Modelar las transiciones de estado del pedido: Preprocesado → Autorización → Aceptación.
4. Definir un esquema inicial para la persistencia de datos utilizando una base de datos SQL.
5. Establecer tácticas de resiliencia para manejar dependencias externas (e.g., Servicio de Clientes).
6. Crear artefactos que reflejen el diseño propuesto:
   - Diagramas de componentes y secuencia.
   - Esquema inicial de base de datos.

## Drivers Clave
1. **Escalabilidad**: Diseñar para soportar picos de carga y grandes volúmenes de datos.  
2. **Disponibilidad**: Garantizar un tiempo de actividad del 99.9%.  
3. **Rendimiento**: Tiempo de respuesta menor a 1 segundo para consultas frecuentes y creación de pedidos.  
4. **Consistencia**: Mantener datos coherentes, incluso en caso de fallos o latencia en la sincronización.  

## Artefactos a Generar
1. **ADR para el uso de CQRS en el microservicio de Gestión de Pedidos**: Documento que registra la decisión de diseño. [Ver ADR](ADR_Iteracion_1.md).  

