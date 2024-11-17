# Objetivo de la Iteración 0

## Descripción
En la Iteración 0 se establece la base arquitectónica del sistema, tomando la decisión fundamental de migrar de una arquitectura monolítica a una arquitectura de microservicios. Esta decisión considera todos los requerimientos funcionales, atributos de calidad y restricciones técnicas documentados en el archivo de referencia general.

## Objetivos Específicos
1. **Identificar las limitaciones del sistema monolítico actual**: Se revisan las limitaciones actuales en términos de escalabilidad, disponibilidad y mantenibilidad.
2. **Evaluar alternativas arquitectónicas**: Consideración de las opciones arquitectónicas, incluyendo la posibilidad de mantener la arquitectura monolítica o migrar a una arquitectura de microservicios.
3. **Definir los criterios de decisión**: Seleccionar los drivers clave (escalabilidad, disponibilidad, mantenibilidad, desempeño, modularidad e interoperabilidad) que influyen en la decisión final.
4. **Tomar una decisión de diseño**: Decidir si se migrará a microservicios y documentar los motivos y consecuencias de esta decisión en un ADR (Architecture Decision Record).

## Artefactos Generados
- **ADR de la Migración a Microservicios**: Documento que registra la decisión de adoptar una arquitectura de microservicios. [Ver ADR](ADR_Iteracion_0.md).
- **Documento de Requerimientos, Atributos de Calidad y Restricciones**: Documento de referencia general que detalla los requisitos, atributos de calidad y restricciones técnicas que guiarán el proceso de diseño. [Ver documento](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).
- **Diagrama General de Microservicios**: Representa la propuesta inicial de la arquitectura, mostrando los servicios principales y sus interacciones. [Ver diagrama](artefacto_iteracion_0_diagrama_general_microservicios.png).
