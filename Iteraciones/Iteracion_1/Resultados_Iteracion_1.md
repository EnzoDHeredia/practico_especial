# Resultados de la Iteración 1

## Resumen de la Decisión
En esta iteración se implementó la separación de responsabilidades de comandos y consultas utilizando el patrón CQRS (Command Query Responsibility Segregation) para el microservicio de Gestión de Pedidos. Esto se realizó como un paso inicial hacia la optimización del rendimiento y la escalabilidad del sistema bajo alta carga concurrente.

El diseño implementado en esta etapa utiliza una base de datos común para comandos y consultas, lo que permitió reducir la complejidad inicial y centrarse en validar los beneficios de la arquitectura.

## Referencias a Documentación Inicial
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../documentacion_inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).

## Decisiones Tomadas
1. **Uso de CQRS**:  
   - Separar comandos (crear y actualizar pedidos) y consultas (consultar pedidos) para optimizar rendimiento y escalabilidad.  
2. **Modelado de Transiciones de Estado**:  
   - Definición de estados: Preprocesado, Autorización y Aceptación.  
   - Implementación de validaciones para garantizar transiciones válidas.  
3. **Persistencia**:  
   - Esquema relacional inicial para manejar pedidos y sus detalles en una base de datos SQL.  

## Puntos Clave
1. **Optimización de consultas**: Se observaron mejoras en los tiempos de respuesta para operaciones de lectura gracias a la separación de modelos de datos para lectura y escritura.
2. **Sincronización de eventos**: Se implementaron eventos básicos para mantener consistencia eventual entre los modelos de comandos y consultas.
3. **Flexibilidad tecnológica**: El diseño basado en CQRS habilita la posibilidad de escalar comandos y consultas de manera independiente en futuras iteraciones.

## Lecciones Aprendidas
- **Desafíos iniciales con eventos**: La sincronización de eventos, aunque funcional, introdujo una complejidad adicional en la validación de consistencia eventual.
- **Curva de aprendizaje**: El equipo necesitó tiempo para familiarizarse con los conceptos y herramientas relacionadas con CQRS.
- **Pruebas de carga**: Se comprobó que las consultas responden adecuadamente bajo carga concurrente, aunque la base de datos compartida limita el potencial completo de escalabilidad.

## Recomendaciones para la Siguiente Iteración
1. **Separar bases de datos**: Implementar bases de datos independientes para comandos y consultas, lo que mejorará aún más la escalabilidad y el rendimiento.
2. **Ampliar eventos de dominio**: Incorporar más eventos para manejar transiciones de estado complejas y optimizar la sincronización entre modelos.
3. **Evaluar herramientas adicionales**: Considerar tecnologías específicas para CQRS, como Event Sourcing, para manejar mejor la consistencia y el historial de cambios.

## Artefactos Generados
1. **ADR para el uso de CQRS en el microservicio de Gestión de Pedidos**: Documento que registra la decisión de diseño. [Ver ADR](ADR_Iteracion_1.md).  
