# Objetivo de la Iteración 4

## Descripción

En la Iteración 4, el enfoque estará en el **microservicio de Procesamiento de Pagos**, un componente crítico que se integra con la pasarela de pagos externa de MercadoLibre. Los objetivos principales son:

1. Mejorar la resiliencia del sistema frente a fallos temporales de la pasarela.
2. Garantizar la seguridad de las transacciones.
3. Optimizar la auditoría y el monitoreo de los pagos.

Para lograr estos objetivos, se tomarán decisiones clave relacionadas con patrones de resiliencia, integración con la pasarela de pago y la estrategia de auditoría y monitoreo.

---

## Referencias a Documentación Inicial

## Referencias a Documentación Inicial
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).

---

## Objetivos Específicos

1. **Implementar el patrón Circuit Breaker para resiliencia en el microservicio de pagos**:
   - Garantizar que el sistema de pagos maneje fallos temporales de la pasarela de pago externa.
   - Asegurar que las transacciones sean procesadas de manera segura incluso ante fallos.

2. **Integración con la pasarela de pagos de MercadoLibre**:
   - Integrar el microservicio con la API RESTful de MercadoLibre para procesar pagos de manera eficiente.
   - Cumplir con los estándares de seguridad requeridos.

3. **Implementar un sistema de auditoría y monitoreo**:
   - Registrar todas las transacciones para auditorías y análisis forenses.
   - Monitorear el sistema en tiempo real para detectar problemas de rendimiento.

---

## Drivers Clave

1. **Resiliencia**:
   - Garantizar que el sistema continúe operando frente a fallos temporales de la pasarela de pago.
2. **Seguridad**:
   - Cumplir con estándares como PCI DSS para procesar transacciones de forma segura.
3. **Escalabilidad**:
   - Manejar un alto volumen de pagos concurrentes sin comprometer el rendimiento.
4. **Trazabilidad**:
   - Permitir una auditoría completa y eficiente de todas las transacciones.
5. **Disponibilidad**:
   - Asegurar que el sistema de pagos esté operativo 24/7, incluso en condiciones de alta carga.

---

## Artefactos a Generar

1. **ADR sobre la selección del patrón Circuit Breaker para el microservicio de pagos**:
   - Documento que justifica la implementación del patrón Circuit Breaker como mecanismo de resiliencia.

2. **ADR sobre la integración con la pasarela de pagos de MercadoLibre**:
   - Documento que registra la decisión de usar la API RESTful de MercadoLibre para procesar pagos.

3. **ADR sobre la implementación de auditoría y monitoreo para el microservicio de pagos**:
   - Documento que detalla la estrategia de auditoría y monitoreo en tiempo real.

---

## Artefactos Generados

1. **ADR sobre la selección del patrón Circuit Breaker para el microservicio de pagos**:
   - [Ver ADR](../../ADRs/ADR_011_Resilience%20Pattern.md).

2. **ADR sobre la integración con la pasarela de pagos de MercadoLibre**:
   - [Ver ADR](../../ADRs/ADR_012_Integration_MercadoLibre.md).

3. **ADR sobre la implementación de auditoría y monitoreo para el microservicio de pagos**:
   - [Ver ADR](../../ADRs/ADR_013_Auditing_Monitoring.md).
