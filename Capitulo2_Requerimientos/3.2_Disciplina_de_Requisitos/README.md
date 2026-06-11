# 3.2 Disciplina de Requisitos

[Volver al capítulo 2](../README.md) | [Volver al índice principal](../../README.md)

---

## 3.2.1 Actores del sistema

| Actor | Descripción |
|---|---|
| Responsable del centro de control | La persona que accede a la aplicación web desde el navegador. Consulta las notificaciones que llegan, las marca como leídas, las borra cuando le parece oportuno y también puede contactar con otros operarios mediante el chat. |
| Tiempo | Actor abstracto que representa el disparador automático externo al sistema. No es un usuario humano, sino el momento en el que la API de Soincon genera y envía un evento hacia la aplicación tras producirse una modificación en EmiSuite. Por ello, activa la recepción de notificaciones de forma automática. |


 * Operario del sistema de producción: persona encargada de registrar o modificar eventos operativos en el sistema externo de producción, provocando la emisión de notificaciones que son recibidas por la aplicación mediante WebSocket. Al no interactuar directamente con la aplicación, no es considerado un actor.
---

## 3.2.2 Casos de uso

![Diagrama de casos de uso](../../imagenes/casosDeUso.svg)
[Código fuente](../../codigoFuente/casosDeUso.puml)

### Casos de uso más representativos

Se detallan a continuación cuatro casos de uso que cubren los flujos más representativos del sistema: ver una notificación, eliminar dicha notificación, consultar el historial y enviar mensaje de incidencia.

![Ver notificación](../../imagenes/verNotificacion.svg)
[Código fuente](../../codigoFuente/verNotificacion.puml)

![Eliminar notificación](../../imagenes/eliminarNotificacion.svg)
[Código fuente](../../codigoFuente/eliminarNotificacion.puml)

![Consultar el historial](../../imagenes/consultarHistorial.svg)
[Código fuente](../../codigoFuente/consultarHistorial.puml)

![Enviar mensaje de incidencia](../../imagenes/enviarMensajeDeIncidencia.svg)
[Código fuente](../../codigoFuente/enviarMensajeDeIncidencia.puml)

---

## 3.2.3 Prototipos de interfaz

Los prototipos de baja fidelidad validan la correspondencia entre los casos de uso detallados y la interfaz del sistema. Se presentan como wireframes funcionales centrados en la estructura de la pantalla y el flujo de interacción, no en el diseño visual final.

### "Main dashboard"

Vista principal orientada al seguimiento del sistema. Presenta las acciones de simulación de eventos que pueden recibirse mediante WebSocket, un resumen del volumen de notificaciones recibidas y los accesos necesarios para consultar el historial o finalizar la sesión.

![Prototipo de la página](../../imagenes/prototipoPagina.svg)  
[Código fuente](../../codigoFuente/prototipoPagina.puml)

### Notificación

Vista centrada en el detalle de una notificación recibida. Muestra la información principal asociada al evento, como el tipo de incidencia, la operación, la descripción, la fecha y la hora. Desde esta vista se contempla la posibilidad de actualizar el estado de lectura de la notificación o iniciar la comunicación con un operario aportando el contexto del aviso.

![Prototipo de una notificación](../../imagenes/prototipoNotificacion.svg)  
[Código fuente](../../codigoFuente/prototipoNotificacion.puml)

### Chat

Vista destinada a la comunicación con un operario a partir de una incidencia. Permite seleccionar el destinatario, redactar el mensaje y asociar la información de la notificación para facilitar el contexto de la situación comunicada.

![Prototipo de chat](../../imagenes/prototipoChat.svg)  
[Código fuente](../../codigoFuente/prototipoChat.puml)
## 3.2.4 Diagrama de contexto

El diagrama de contexto representa el sistema del TFG como una maquina de estados orientada a la recepcion de eventos procedentes de EmiSuite. `SESION_CERRADA` es el estado inicial y `SISTEMA_DISPONIBLE` actua como hub principal de la aplicacion, desde el que el usuario puede conectar el WebSocket, abrir el dashboard, consultar el historial, usar el chat o cambiar el tema visual. EmiSuite no se modela como una vista navegable del sistema, sino como el entorno externo donde se modifican documentos y se generan los eventos que posteriormente llegan a la aplicacion mediante los topics WebSocket.

El flujo principal comienza con la conexion al WebSocket, la suscripcion a los topics (`notices`, `updateui` y `outputtrigger`) y la recepcion de mensajes. Cada evento recibido se normaliza y se transforma en una notificacion, que puede mostrarse como toast, guardarse en el historial o adjuntarse a una conversacion de chat. El dashboard permite visualizar el estado de la informacion recibida, mientras que el historial y el chat completan la gestion de las notificaciones.

De esta forma, el diagrama resume como la aplicacion del TFG recibe eventos generados en EmiSuite y los convierte en informacion visible y gestionable para el usuario.

![Diagrama de contexto](../../imagenes/diagramaContextoSimple.svg)
[Código fuente](../../codigoFuente/diagramaDeContextoSimple.puml)

## 3.2.5 Requisitos no funcionales

Los requisitos no funcionales describen las propiedades de calidad que debe cumplir el sistema más allá de lo que hace. No cuentan qué hace el sistema, sino cómo lo hace.

| ID | Nombre | Tipo | Prioridad | Descripción |
|---|---|---|---|---|
| RNF01 | Latencia de notificaciones | Rendimiento | Alta | El tiempo que pasa desde que se emite un evento en el servidor hasta que se ve en pantalla no será mayor de 200 ms en condiciones normales de red. |
| RNF02 | Capacidad de procesamiento | Rendimiento | Media | El sistema podrá procesar varios eventos por segundo sin que el administrador note que la interfaz se resiente. |
| RNF03 | Tiempo de carga inicial | Rendimiento | Media | La aplicación estará lista para usarse en menos de 3 segundos con una conexión de banda ancha normal. |
| RNF04 | Usabilidad sin formación técnica | Usabilidad | Alta | La interfaz seguirá las convenciones visuales estándar para que el administrador pueda usarla sin que le tengan que explicar nada. |
| RNF05 | Indicador de estado de conexión | Usabilidad | Media | El estado de la conexión WebSocket (conectado / desconectado / error) se verá siempre en la interfaz. |
| RNF06 | Modularidad del componente | Mantenibilidad | Media | El componente de notificaciones estará desacoplado del resto de la aplicación y seguirá las convenciones de React. |
| RNF07 | Compatibilidad con navegadores | Compatibilidad | Alta | La aplicación funcionará bien en las versiones actuales de Chrome, Firefox, Safari y Edge, con un diseño responsive que se adapte a tablets. |
| RNF08 | Gestión de fallos de conexión | Confiabilidad | Alta | Ante una pérdida de conexión o mensajes mal formados, el sistema avisará al administrador sin que se bloquee la interfaz. |

## Detalle por categoría

### Rendimiento

- La latencia entre que se emite un evento en el servidor y se ve la notificación correspondiente en el cliente no debería pasar de 200 milisegundos con una red normal.
- El sistema tiene que poder recibir y procesar al menos 10 eventos por segundo sin que la interfaz se degrade demasiado.
- La aplicación no debería tardar más de 3 segundos en cargar la primera vez con una conexión de banda ancha estándar.

### Usabilidad

- La interfaz debe seguir las convenciones visuales típicas de las notificaciones web, para que un usuario sin formación específica pueda usarla sin que le tengan que explicar nada.
- El estado de la conexión WebSocket tiene que verse siempre, para que el usuario sepa si el sistema está recibiendo eventos o no.

### Mantenibilidad

- El componente de notificaciones tiene que estar desacoplado del resto de la aplicación, de forma que se pueda actualizar o cambiar sin que afecte a otros módulos.
- El código debe seguir los estilos de React que se usan hoy en día (componentes funcionales, hooks) y estar lo suficientemente comentado para que otro desarrollador pueda entenderlo sin tener que preguntar.

### Compatibilidad

- La aplicación tiene que funcionar bien en las versiones actuales de Chrome, Firefox, Safari y Edge.
- El diseño será responsive y se adaptará bien a pantallas de distintos tamaños, incluyendo tablets.
- El componente debe ser compatible con React 18 o superior.

### Confiabilidad

- Si se pierde la conexión WebSocket, el sistema debe avisar al usuario claramente de que está desconectado.
- Que falle la conexión WebSocket no debe provocar errores inesperados que bloqueen la interfaz o impidan al usuario seguir usando la aplicación.
- El sistema debe manejar con seguridad los mensajes mal formados o raros que pueda mandar el servidor, descartándolos sin que se pare el funcionamiento.

---

[Anterior: 3.1 Modelo del Dominio](../3.1_Modelo_del_Dominio/README.md) | [Siguiente: Capítulo 3 - Análisis y Diseño](../../Capitulo3_Analisis_Diseño/README.md) | [Presentación del trabajo](../PRESENTACION.md)

