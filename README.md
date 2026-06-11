# Sistema de Gestión de riesgos en faenas

**Descripción del proyecto**

El proyecto consiste en la creación de un sistema  integral para la gestión de riesgos faenas. Para contextualizar, existen muchos entornos de trabajo en que los trabajadores están expuestos a riesgos que puedan dañar su integridad, generalmente riesgos físicos. Pueden ser varios escenarios, como inundaciones, cortes de luz, incendios, derrame de químicos, incluso asaltos. Para poder registrar estos incidentes, lo que hace el trabajador que trabaja en esos entornos es registrar los hechos a mano. Es decir, los reportes que ellos elaboran lo realizan a papel, ya sea en blanco o con un formato de reporte otorgado por la empresa. Una vez hecho el reporte, el trabajador debe enviarlo a su correspondiente supervisor (presencialmente) para que éste pueda analizar el caso y resolverlo. 
¿Cuál es el problema con esto? Que todo este proceso consume tiempo, requiere logística y que la trazabilidad no es del todo seguro. Asimismo, el proceso descrito depende de objetos fisicos como los registros en papel, y no hay una base de datos que albergue dichos registros, y a la vez, consultar, actualizar, seleccionar o eliminar. Al haber dependencia de objetos físicos, ello requiere salvaguardarlos de una forma más engorrosa, y al acumularse con el tiempo, resulta más dificil consultar en un futuro un determinado reporte.

## Características Principales

### Módulos Funcionales 


- **Reporte de Peligros de Seguridad**: Los trabajadores pueden reportar actos inseguros y condiciones inseguras mediante fotografías, ubicación geográfica y descripciones detalladas.

- **Seguimiento de Estado en Tiempo Real**: Permite monitorear el estado de un reporte durante todo su ciclo de vida (enviado → en revisión → acción asignada → cerrado).

- **Monitoreo de SLA**: Indicadores visuales que muestran si los reportes están dentro del plazo, en riesgo de incumplimiento o vencidos.

- **Estadísticas Personales de Seguridad**: Permite visualizar tasas de efectividad, rachas de participación y métricas relacionadas con el reporte de Incidentes y Actos Peligrosos (IAP).

- **Notificaciones**: Los usuarios reciben alertas en tiempo real sobre cambios en el estado de sus reportes y avisos de seguridad específicos de su área de trabajo.

- **Soporte Offline**: Los reportes se almacenan localmente cuando no hay conexión a Internet y se sincronizan automáticamente una vez que se restablece la conectividad.

### Funcionalidades Adicionales

- **Integración con IAP**: Gestión especializada para reportes de IAP (Incidentes y Actos Peligrosos u Oportunidades de Mejora, según la definición de la organización).
- **Acciones Correctivas**: Permite asignar, monitorear y dar seguimiento a acciones correctivas, incluyendo fechas límite y estado de cumplimiento.
- **Comentarios y Discusión**: Facilita la colaboración entre los miembros del equipo mediante comentarios asociados a cada reporte.
- **Clasificación Jerárquica de Reportes**: Los reportes pueden clasificarse como actos inseguros o condiciones inseguras para mejorar su análisis y tratamiento.
- **Soporte para Múltiples Turnos**: Permite registrar incidentes y observaciones correspondientes a turnos de mañana, tarde o noche.
- **Tema Industrial Oscuro**: Interfaz diseñada específicamente con una temática oscura y acentos en color naranja de seguridad, optimizando la visibilidad y la experiencia de uso en entornos industriales.


## Stack Tecnológico <detallar el stack tecnológico utilizado>



### Backend
![Pantalla de Login](images/stack2.png)
- 
- 
- 
- 

### Frontend (Página web)
![Pantalla de Login](images/stack3.png)

### Frontend (App móvil)
![Pantalla de Login](images/stack4.png) 


### Base de Datos
- La solución propuesta utiliza Cloud Firestore como sistema de gestión de bases de datos. Firestore es una base de datos NoSQL orientada a documentos que forma parte del ecosistema de Google Cloud Platform (GCP). Su adopción responde a la necesidad de contar con una plataforma altamente escalable, capaz de soportar grandes volúmenes de reportes de seguridad, actualizaciones en tiempo real y una arquitectura basada en servicios desacoplados.

Una de las principales ventajas de Firestore es su capacidad de escalamiento horizontal automático, permitiendo aumentar la capacidad del sistema sin requerir configuraciones manuales de infraestructura. Esto resulta especialmente relevante para una aplicación de gestión de riesgos laborales, donde el volumen de reportes puede variar significativamente según la cantidad de empresas, faenas y usuarios conectados.

Adicionalmente, Firestore ofrece integración nativa con servicios de Google Cloud, simplificando los mecanismos de autenticación y autorización mediante cuentas de servicio utilizadas por los microservicios desplegados en Cloud Run. Asimismo, dispone de soporte para operaciones asíncronas a través del SDK oficial de Python, facilitando su integración con servicios desarrollados en FastAPI y ejecutados mediante Uvicorn.

La plataforma también incorpora capacidades de sincronización en tiempo real mediante listeners, permitiendo que los cambios en los reportes, alertas o acciones correctivas se reflejen instantáneamente en las interfaces de usuario sin necesidad de consultas periódicas al servidor.


## Modelos de Datos

La estructura de Firestore se organiza utilizando un esquema jerárquico basado en colecciones y subcolecciones. En el nivel superior se encuentra la colección clients, donde cada documento representa una organización cliente del sistema. Este enfoque permite implementar un modelo multi-tenant, asegurando la separación lógica de los datos entre distintas empresas.

Dentro de cada cliente se almacenan diversas subcolecciones que representan las entidades funcionales del sistema:

users: contiene la información de los usuarios registrados, incluyendo nombre, correo electrónico, rol, áreas asignadas y estado.
zones: almacena información de las zonas o áreas de trabajo, incluyendo procesos asociados, colores de visualización y coordenadas utilizadas para representar polígonos en mapas de planta.
reports: registra los reportes de riesgos, actos inseguros, condiciones inseguras e IAP, junto con información sobre responsables, fotografías, turnos y estado del reporte.
report_events: mantiene un historial completo de cambios de estado, implementando un enfoque de auditoría basado en eventos.
actions: almacena las acciones correctivas derivadas de los reportes, incluyendo responsables, fechas de vencimiento y estado de cumplimiento.
comments: permite registrar conversaciones y comentarios asociados a cada reporte.
alerts: administra las notificaciones y alertas generadas por el sistema.
exports: conserva el historial de exportaciones de información y reportes generados por los usuarios.

Este diseño favorece la organización lógica de los datos, reduce la complejidad de las consultas y facilita la escalabilidad de la plataforma.


## Seguridad <describir las medidas y tecnologías de seguridad utilizadas, abajo ejemplos>

- Autenticación JWT con tokens seguros
- Hash de contraseñas con bcryptjs
- Middleware de autenticación y autorización
- Validación de roles (admin/consultor)
- CORS configurado
- Validación de datos con express-validator

## Integrantes

**CAPSTONE_001D - Grupo 1**

- Sean Parker
- Tomás Figueroa
- Cristóbal Zapata

## Documentación Adicional <especificar la documentación adicional que se incorpora, abajo son ejemplos>

- **ERS**
- **Diagrama de Clases**
- **Modelo de Datos**
- **Carta Gantt**

## Arquitectura <especificar la arquitectura de la solución, abajo son ejemplos>

El sistema sigue una **arquitectura en capas**:

- **Capa de Presentación**: Next.js con componentes React
- **Capa de Controladores**: Express routes y controllers
- **Capa de Servicios**: Lógica de negocio y validaciones
- **Capa de Datos**: Sequelize ORM con PostgreSQL
- **Capa de Auditoría**: Triggers de base de datos para trazabilidad

## Metodología <especificar la metodología de la solución, abajo son ejemplos>

El proyecto fue desarrollado siguiendo la **metodología Cascada (Waterfall)**, con fases bien definidas:

1. **Fase 1**: Planificación y Análisis
2. **Fase 2**: Diseño
3. **Fase 3**: Desarrollo
4. **Fase 4**: Pruebas y Despliegue
5. **Fase 5**: Cierre


## Licencia

Este proyecto fue desarrollado como parte del proyecto APT (Aplicación de Proyecto Tecnológico) para <nombre de la empresa>.

**Versión**: #####  
**Última actualización**: ########
