# Resultados de la Iteración 2

---

## Resumen de las Decisiones
En esta iteración, se tomaron tres decisiones clave para el rediseño del microservicio de **Gestión de Clientes** con el objetivo de mejorar la escalabilidad, trazabilidad y seguridad del sistema. Estas decisiones incluyen:

1. **Unificación de los microservicios de Estadísticas y Notificación de Estado de Pedido:**  
   - La decisión fue consolidar estos servicios, centralizando su lógica y reduciendo la redundancia en el sistema.  

2. **Implementación de una Base de Datos de Auditoría para la Gestión de Clientes y Sustitución del Microservicio de Gestión de Roles y Usuarios por un Servidor de Autenticación:**  
   - Se implementó una base de datos dedicada para auditar y registrar cambios en los datos de clientes, mejorando la trazabilidad.  
   - Se optó por sustituir el microservicio actual por un servidor especializado en autenticación y gestión de roles, centralizando y asegurando la validación de credenciales.  

---

## Referencias a Documentación Inicial
1. **Requerimientos del Sistema**:  
   - [Requerimientos, Atributos de Calidad y Restricciones](../../Doumentacion_Inicial/Requerimientos_Atributos_Calidad_Restricciones.md).  
2. **Tabla de Priorización**:  
   - [Tabla de Criticidad, Complejidad e Importancia](../../Doumentacion_Inicial/Tabala_Requerimientos_Atributos.md).
---

## Puntos Clave
1. **Mejora de la Escalabilidad:**  
   - La unificación de servicios facilita el mantenimiento del sistema y reduce la sobrecarga de infraestructura.  

2. **Trazabilidad de los Datos de Clientes:**  
   - La base de datos de auditoría asegura la trazabilidad de los cambios de datos del cliente, lo que mejora la transparencia.  

3. **Seguridad Mejorada:**  
   - El servidor de autenticación permite una mejor gestión de la seguridad y validación de credenciales, reduciendo la complejidad de los servicios existentes.  

---

## Lecciones Aprendidas
- **Desafíos de integración:**  
  - La integración de los servicios de Estadísticas y Notificación de Estado de Pedido presentó desafíos, pero la consolidación facilita el mantenimiento futuro.  

- **Complejidad inicial:**  
  - La implementación de la base de datos de auditoría y el servidor de autenticación introdujo complejidad adicional, pero mejoró la trazabilidad y la seguridad del sistema.  

- **Eficiencia operativa:**  
  - La centralización de roles y autenticación contribuye a una mejor gestión del sistema a largo plazo, aunque requiere alta disponibilidad para evitar puntos únicos de fallo.  

---

## Recomendaciones para la Siguiente Iteración
1. **Optimizar la infraestructura de auditoría:**  
   - Mejorar la escalabilidad de la base de datos de auditoría, considerando particionamiento o replicación.  

2. **Escalar el servidor de autenticación:**  
   - Implementar alta disponibilidad para el servidor de autenticación, evitando que se convierta en un cuello de botella.  

3. **Evaluar la integración de más servicios:**  
   - A medida que más servicios sean integrados al sistema, seguir un patrón similar de unificación y centralización para mejorar la eficiencia.  

---

## Artefactos Generados
1. **ADR sobre la Unificación de los Microservicios de Estadísticas y Notificación de Estado de Pedido:**  
   - [Ver ADR](../../ADRs/ADR_006_API_Gateway_Pattern.md)  

2. **ADR sobre la Implementación de una Base de Datos de Auditoría para la Gestión de Cliente y la Sustitución del Microservicio de Gestión de Roles y Usuarios por un Servidor de Autenticación:**  
   - [Ver ADR](../../ADRs/ADR_007_Unificacion_Servicios.md)  
