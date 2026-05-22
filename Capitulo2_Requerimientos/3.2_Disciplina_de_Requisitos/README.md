# 3.2 Disciplina de Requisitos

[Volver al capítulo 2](../README.md) | [Volver al índice principal](../../README.md)

---

## 3.2.1 Actores del sistema

| Actor | Descripción |
|---|---|
| Responsable del centro de control | La persona que accede a la aplicación web desde el navegador. Consulta las notificaciones que llegan, las marca como leídas, las borra cuando le parece oportuno y también puede contactar con otros operarios mediante el chat. |


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

Aquí se encuentran unos prototipos de cómo me gustaría que quedara la aplicación. Validan la correspondencia entre los casos de uso detallados y la interfaz del sistema.

### Prototipo de la página principal
Aquí podemos observar lo que podrá ser el 'main dashboard'. Se pueden ver los botones de simulación de los diferentes eventos que podrán llegar mediante los WebSocket, un resumen del número de notificaciones que han llegado a la página, y en la parte superior un apartado de historial y el botón de Cerrar sesión.

![Prototipo de la página](../../imagenes/prototipoPagina.svg)
[Código fuente](../../codigoFuente/prototipoPagina.puml)

Aquí podemos ver cual es la información y de qué manera va a llegar a la aplicación. Contiene el tipo de incidencia, operación, descripción, fecha y hora. Además se podrá marcar como leída o mandarsela a algún operario a través de un chat.

![Prototipo de una notificación](../../imagenes/prototipoNotificacion.svg)
[Código fuente](../../codigoFuente/prototipoNotificacion.puml)

Finalmente aquí se puede ver cómo será el chat. Contendrá un contacto al que mandar la información, un mensaje y se le podrá adjuntar dicha información para un mejor contexto de la situación.

![Prototipo de chat](../../imagenes/prototipoChat.svg)
[Código fuente](../../codigoFuente/prototipoChat.puml)

---

## 3.2.4 Diagrama de contexto

El diagrama de contexto representa el sistema del TFG como una maquina de estados orientada a la recepcion de eventos procedentes de EmiSuite. `SESION_CERRADA` es el estado inicial y `SISTEMA_DISPONIBLE` actua como hub principal de la aplicacion, desde el que el usuario puede conectar el WebSocket, abrir el dashboard, consultar el historial, usar el chat o cambiar el tema visual. EmiSuite no se modela como una vista navegable del sistema, sino como el entorno externo donde se modifican documentos y se generan los eventos que posteriormente llegan a la aplicacion mediante los topics WebSocket.

El flujo principal comienza con la conexion al WebSocket, la suscripcion a los topics (`notices`, `updateui` y `outputtrigger`) y la recepcion de mensajes. Cada evento recibido se normaliza y se transforma en una notificacion, que puede mostrarse como toast, guardarse en el historial o adjuntarse a una conversacion de chat. El dashboard permite visualizar el estado de la informacion recibida, mientras que el historial y el chat completan la gestion de las notificaciones.

De esta forma, el diagrama resume como la aplicacion del TFG recibe eventos generados en EmiSuite y los convierte en informacion visible y gestionable para el usuario.

![Diagrama de contexto](../../imagenes/diagramaContextoSimple.svg)
[Código fuente](../../codigoFuente/diagramaDeContextoSimple.puml)


---

[Anterior: 3.1 Modelo del Dominio](../3.1_Modelo_del_Dominio/README.md) | [Siguiente: 3.3 Requisitos No Funcionales](../3.3_Requisitos_No_Funcionales/README.md)
