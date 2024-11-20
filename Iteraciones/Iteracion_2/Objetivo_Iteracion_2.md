# Objetivo de la Iteración 2

---

## Descripción
En la Iteración 2, el enfoque se centrará en el microservicio de **Gestión de Clientes**, donde se abordarán aspectos críticos relacionados con la eficiencia, seguridad, escalabilidad y consistencia de los datos. En esta etapa, se tomaron decisiones clave sobre la unificación de servicios y el diseño de la arquitectura para mejorar la trazabilidad, la gestión de roles y la autenticación de usuarios.

---

## Referencias a Documentación Inicial
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).

---

## Objetivos Específicos
1. **Unificación de los microservicios de Estadísticas y Notificación de Estado de Pedido:**  
   - Consolidar ambos servicios para reducir redundancias y sobrecarga en la infraestructura.  

2. **Implementación de una Base de Datos de Auditoría y Sustitución del Microservicio de Gestión de Roles y Usuarios por un Servidor de Autenticación:**  
   - Crear una base de datos centralizada que registre todos los cambios relevantes en los datos del cliente, garantizando trazabilidad.  
   - Delegar la gestión de roles y autenticación a un servidor especializado para mejorar la seguridad y simplificar la arquitectura.  

---

## Drivers Clave
- **Reducción de la complejidad:** Simplificar la infraestructura unificando servicios similares.  
- **Escalabilidad:** Permitir la expansión del sistema sin introducir cuellos de botella.  
- **Trazabilidad de datos:** Asegurar que cualquier cambio en la información de clientes sea auditado adecuadamente.  
- **Seguridad:** Centralizar la autenticación y gestión de roles para mejorar la seguridad del sistema.  

---

## Artefactos a Generar
1. **ADR sobre la Unificación de los Microservicios de Estadísticas y Notificación de Estado de Pedido:**  
   - Documento que justifica la consolidación de ambos servicios.  

2. **ADR sobre la Implementación de una Base de Datos de Auditoría para la Gestión de Clientes y la Sustitución del Microservicio de Gestión de Roles y Usuarios por un Servidor de Autenticación:**  
   - Documento que registra la decisión de auditar, rastrear cambios en los datos de clientes, y de delegar autenticación y gestión de roles a un servidor dedicado.  

---

## Artefactos Generados
1. **ADR sobre la Unificación de los Microservicios de Estadísticas y Notificación de Estado de Pedido:**  
   - [Ver ADR](../../ADRs/ADR_006_API_Gateway_Pattern.md)  

2. **ADR sobre la Implementación de una Base de Datos de Auditoría para la Gestión de Cliente y la Sustitución del Microservicio de Gestión de Roles y Usuarios por un Servidor de Autenticación:**  
   - [Ver ADR](../../ADRs/ADR_007_Unificacion_Servicios.md)  
