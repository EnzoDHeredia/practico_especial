# Objetivo de la Iteración 2

## Descripción
En la Iteración 2, el enfoque se centra en el diseño y la implementación del patrón **API Gateway** como punto de entrada único para el microservicio de Gestión de Clientes. Este componente es fundamental para mejorar la seguridad, escalabilidad y rendimiento del sistema, encapsulando la estructura interna de los microservicios y optimizando las solicitudes API.

El patrón API Gateway garantizará que las solicitudes hacia el microservicio de Gestión de Clientes sean gestionadas de forma centralizada, incluyendo autenticación, autorización y optimización del rendimiento mediante caching y balanceo de carga.

## Referencias
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md). 
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).
3. **ADR Iteración Cero**:  
   - [Migración a Microservicios](../Iteracion_0/ADR_Iteracion_0.md).
4. **ADR Iteración 1**:  
   - [CQRS para Gestión de Pedidos](../Iteracion_1/ADR_Iteracion_1.md).

## Objetivos Específicos
1. Diseñar e implementar un **API Gateway** que sirva como punto de entrada único para solicitudes al microservicio de Gestión de Clientes.
2. Centralizar la lógica de autenticación y autorización utilizando OAuth2 y tokens JWT.
3. Implementar caching selectivo para optimizar las consultas frecuentes hacia el microservicio de Gestión de Clientes.
4. Configurar descubrimiento de servicios y balanceo de carga dinámico para garantizar disponibilidad y escalabilidad.
5. Proveer una base para la integración futura de otros microservicios bajo el mismo gateway.

## Drivers Clave
1. **Seguridad**: Proteger las solicitudes mediante autenticación y autorización centralizadas.
2. **Escalabilidad**: Manejar hasta 500 solicitudes concurrentes con balanceo de carga dinámico.
3. **Rendimiento**: Reducir latencia en consultas frecuentes hacia el microservicio de Gestión de Clientes.
4. **Disponibilidad**: Mantener un tiempo de actividad del 99.9% mediante descubrimiento de servicios y políticas de reintento.

## Artefactos a Generar
1. **ADR**: Justificación para la implementación del patrón API Gateway.  
2. **Diagramas**:
   - Diagrama de componentes que muestre la interacción entre el gateway y los microservicios.  
   - Diagrama de secuencia para solicitudes desde el cliente hasta el microservicio de Gestión de Clientes.  
3. **Esquema inicial del API Gateway**: Configuración para autenticación, autorización, caching y balanceo de carga.  
