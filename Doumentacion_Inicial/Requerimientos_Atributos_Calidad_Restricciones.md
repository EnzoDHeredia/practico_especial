# Requerimientos Funcionales, Atributos de Calidad y Restricciones Técnicas

## Propósito
Este documento actúa como una referencia central de los requisitos drivers generales del sistema para todo el proyecto.

## Contenido
Este archivo contiene los detalles relevantes sobre los **requerimientos funcionales**, **atributos de calidad**, y **restricciones técnicas** del sistema.

---

# Requerimientos Funcionales

## Gestión de Clientes (Crítico):
- Acceso a datos personales de los clientes.

## Gestión de Pedidos (Semi-crítico):
- Permitir a los clientes realizar pedidos de productos, con un límite de 3 intentos.
- Control del flujo de procesamiento en tres fases: preprocesado, autorización y aceptación. Si o si se avanza de estado cuando se completa y se acepta el estado anterior.

## Gestión de Reparto y Rutas (Crítico):
- Optimización de rutas y gestión de reparto para flotas de transporte.
- Selección dinámica entre dos algoritmos de optimización en función de la demora de los camiones.

## Estadísticas (No crítico):
- Proveer información en tiempo real sobre el estado de los pedidos y la ubicación de camiones.

## Gestión de Incidencias (Semi-crítico):
- Notificar a los gestores de rutas sobre incidencias como averías o fallos en el reparto.

## Procesamiento de Pagos (Crítico):
- Integración con una pasarela de pago externa de MercadoLibre para pagos seguros y compatibles.

## Notificaciones de Estado (Semi-crítico):
- Notificar a los clientes sobre el estado de sus pedidos (e.g., confirmación, proceso de envío, entrega).

## Auditoría y Registro (No crítico):
- Registrar y auditar acciones importantes, especialmente en los módulos críticos como Clientes, Pedidos y Pagos, para rastrear y analizar cualquier problema de seguridad o cumplimiento.

## Gestión de Usuarios y Roles (No crítico):
- Control de acceso con roles para diferentes usuarios del sistema (e.g., administradores, gestores de ruta, usuarios finales), especialmente en módulos de clientes y estadísticas.

---

# Atributos de Calidad

## Escalabilidad:
- Durante temporadas pico, cuando el número de pedidos por hora aumenta significativamente, el sistema debe mantener un rendimiento estable sin degradación notable, escalando dinámicamente los microservicios de pedidos y pagos para satisfacer la demanda.

## Disponibilidad:
- Ante el fallo de un microservicio crítico, como el de Clientes o Pagos, el sistema debe redirigir o reintentar las solicitudes automáticamente, asegurando la continuidad del servicio sin interrupciones perceptibles para los usuarios.

## Seguridad:
- En el acceso a datos de clientes y en el procesamiento de pagos, el sistema debe proteger los datos sensibles mediante protocolos seguros y autenticación robusta, controlando y auditando el acceso a la información confidencial.

## Mantenibilidad:
- Al actualizar la lógica de negocio en el módulo de Reparto y Rutas, la arquitectura de microservicios debe permitir realizar despliegues sin afectar al resto del sistema, reduciendo al mínimo el tiempo de inactividad y los riesgos asociados.

## Usabilidad:
- Cuando los usuarios acceden desde dispositivos móviles o PC, la interfaz debe ser intuitiva y funcional en ambas plataformas, garantizando una experiencia fluida con latencias mínimas en las respuestas.

## Interoperabilidad:
- Al integrar el sistema con plataformas externas, como sistemas logísticos de terceros, debe garantizarse la interoperabilidad mediante estándares abiertos y APIs RESTful que faciliten una conexión sencilla y eficiente.

## Portabilidad:
- En caso de necesitar migrar el sistema a diferentes entornos de nube o servidores, la arquitectura debe estar diseñada para minimizar los cambios en la infraestructura, facilitando una transición ágil.

## Rendimiento:
- Durante eventos especiales, como Black Friday, en los que el módulo de Pedidos experimenta una alta carga, los microservicios críticos deben responder en menos de 1 segundo bajo carga máxima, evitando cuellos de botella.

## Confiabilidad:
- Si un servicio no crítico, como Estadísticas, experimenta una caída, el sistema debe ser resiliente y garantizar que los servicios críticos continúen operando sin interrupciones ni degradaciones.

---

# Restricciones Técnicas

## Compatibilidad con Dispositivos Móviles y PC:
- La interfaz debe adaptarse tanto a dispositivos móviles como de escritorio, lo que influirá en el diseño de la API y el front-end.

## Migración a Arquitectura Basada en Microservicios:
- La nueva arquitectura debe transformar el sistema monolítico actual en microservicios para mayor flexibilidad y capacidad de evolución.

## Bases de Datos SQL para Clientes y Pedidos:
- Las bases de datos actuales (Clientes y Pedidos) se deben mantener, siendo SQL el sistema de gestión de bases de datos.

## Soporte de Algoritmos de Optimización:
- Los algoritmos de optimización para el módulo de Reparto y Rutas deben seleccionarse según criterios de eficiencia y capacidad de adaptación a distintos escenarios de rutas y demoras.

## Protocolo de Comunicación HTTP/REST:
- El acceso a los datos debe realizarse mediante protocolos HTTP/REST, facilitando la comunicación desde aplicaciones en PC y móviles.

## Documentación de APIs y Módulos:
- Toda API debe estar documentada claramente (posiblemente usando Swagger u OpenAPI), dado que el sistema debe estar preparado para futuras expansiones y mantenibilidad.

## Uso de la Pasarela de Pagos de MercadoLibre:
- La integración de pagos requiere el uso de una pasarela externa proporcionada por MercadoLibre, asegurando seguridad y compatibilidad.

---
