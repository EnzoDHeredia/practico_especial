# Resultados de la Iteración 2

## Resumen de la Iteración
En esta iteración se diseñó e implementó el patrón **API Gateway** como punto de entrada único para el microservicio de Gestión de Clientes. Este componente mejora significativamente la seguridad, escalabilidad y rendimiento del sistema, y establece una base sólida para la integración futura de otros microservicios.

La decisión de implementar el patrón API Gateway quedó documentada en un **ADR**, destacando cómo aborda los drivers clave del sistema. Además, se generaron diagramas y configuraciones iniciales que soportan esta implementación.

## Referencias
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).
3. **ADR Iteración Cero**:  
   - [Migración a Microservicios](../Iteracion_0/ADR_Iteracion_0.md).
4. **ADR Iteración 1**:  
   - [CQRS para Gestión de Pedidos](../Iteracion_1/ADR_Iteracion_1.md).

## Decisiones Tomadas
1. **Implementación del API Gateway**:
   - Punto de entrada único para gestionar solicitudes hacia el microservicio de Gestión de Clientes.
   - Centralización de autenticación y autorización con OAuth2 y tokens JWT.
2. **Optimización del Rendimiento**:
   - Uso de caching selectivo para solicitudes frecuentes, como validación de clientes activos.
   - Configuración de balanceo de carga dinámico para manejar picos de solicitudes.
3. **Alta Disponibilidad**:
   - Configuración inicial de descubrimiento de servicios usando Consul/Eureka.
   - Implementación de políticas de reintento para fallos temporales en los microservicios.

## Artefactos Generados
1. **ADR**:
   - [API Gateway para Gestión de Clientes](../iteracion_2/ADR_iteracion_2.md).
2. **Diagramas**:
   - **Diagrama de componentes**: Representa la interacción entre el gateway y los microservicios de Clientes y Pedidos.  
   - **Diagrama de secuencia**: Flujo desde una solicitud del cliente hasta el microservicio de Gestión de Clientes.  
3. **Configuración inicial del API Gateway**:
   - Configuración para autenticación, autorización y caching.  

## Recomendaciones para Iteraciones Futuras
1. **Extender el API Gateway**:
   - Incorporar nuevos microservicios bajo el mismo gateway para centralizar la gestión de solicitudes.
2. **Optimización de Monitoreo**:
   - Implementar herramientas avanzadas como Prometheus y Grafana para rastrear métricas clave (latencia, errores).
3. **Pruebas de Resiliencia**:
   - Simular fallos en el gateway para validar los mecanismos de recuperación automática.
4. **Despliegues Incrementales**:
   - Usar blue-green deployment o canary releases para futuras actualizaciones del gateway.

## Lecciones Aprendidas
- La centralización de la lógica de autenticación y autorización reduce significativamente la complejidad en los microservicios individuales.
- La configuración inicial del API Gateway puede ser compleja, pero una vez establecida, facilita el manejo de solicitudes a gran escala.
- La integración de caching mejora el rendimiento en consultas frecuentes y reduce la carga en los microservicios dependientes.
