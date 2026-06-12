# 3.1 Modelo del Dominio

[Volver al capítulo 2](../README.md) | [Volver al índice principal](../../README.md)

---

![Modelo del dominio](../../imagenes/modeloDominio.svg)
[Código fuente](../../codigoFuente/modeloDominio.puml)


## 3.1.1 Descripción del modelo de dominio

El sistema parte de que existen documentos que se manejan a través de la API de Soincon. Se pueden crear o modificar estos documentos, y en cada una de esas acciones el servidor genera un evento que explica qué ha cambiado y qué documento se ha alterado. Ese evento se le manda, a través de la conexión WebSocket, a todos los clientes que estén conectados en ese momento. Cuando el cliente recibe el evento, lo convierte en un aviso visual que se añade al historial de notificaciones y aparece en la interfaz del responsable.

El responsable puede interactuar con las notificaciones de tres formas: puede verlas cuando llegan, puede marcarlas como leídas para indicar que ya las ha procesado, y puede borrarlas cuando ya no le hacen falta. Además, el responsable puede ver en todo momento el estado de la conexión WebSocket para saber si el sistema está recibiendo eventos o si hay algún problema de conexión.


## 3.1.2 Diagrama de estados

Aquí están los diagramas de estados de los dos elementos del sistema que tienen un ciclo de vida propio: la notificación y la conexión WebSocket.

### Diagrama de estados: Conexión WebSocket

La conexión WebSocket puede estar en tres estados: **Desconectado**, **Conectando** (internamente) , **Conectado** y **Error**.

- Estado inicial: Desconectado.
- Al cargar la aplicación, se inicia el handshake de WebSocket y pasa a **Conectando**.
- Si el servidor acepta la conexión, pasa a **Conectado**. En estado conectado, los eventos que llegan se procesan como notificaciones (la conexión se queda igual).
- Si hay timeout o falla el handshake, vuelve a **Desconectado**.
- Si se pierde la red o el servidor se cierra, vuelve a **Desconectado**.
- Si el broker o "intermediario" no está disponible, aparecerá el estado **Error**.
- Cuando el responsable cierra la aplicación, se cierra la conexión de forma ordenada y se llega al estado final.

![Diagrama de objetos](../../imagenes/conexionWebsocket.svg)
[Código fuente](../../codigoFuente/conexionWebsocket.puml)

### Diagrama de estados: Ciclo de vida de la Notificación

La notificación puede estar en dos estados: **NoLeída** (`leida = false`) y **Leída** (`leida = true`).

- Estado inicial: NoLeída (se crea así cuando llega un evento).
- Transición a **Leída**: el responsable pulsa "marcar como leída".
- Desde cualquiera de los dos estados, el responsable puede borrar la notificación, y eso la lleva al estado final (eliminada del historial).


![Ciclo de una notificacion](../../imagenes/cicloNotificacion.svg)
[Código fuente](../../codigoFuente/cicloNotificacion.puml)

---
## 3.1.3 Glosario de términos

| Término | Definición |
|---|---|
| Documento | Unidad de información que maneja la API de Soincon. Puede ser cualquier registro de datos guardado en la plataforma EMI Suite 4.0: una orden de trabajo, una incidencia de calidad, un registro de mantenimiento, etc. |
| Evento | Notificación interna que genera el servidor cuando se produce un cambio en los datos. Un evento contiene información sobre el tipo de cambio (creación, modificación) y sobre el documento afectado. |
| Notificación | Mensaje visual que se le muestra al responsable en la interfaz como consecuencia de un evento recibido. Tiene un título, un mensaje descriptivo, un tipo (información, éxito, advertencia) y una marca de tiempo. |
| Conexión WebSocket | Canal de comunicación bidireccional y que se mantiene abierto entre el cliente web y el servidor. Permite que el servidor envíe eventos al cliente en tiempo real sin que el cliente tenga que pedírselos. |
| Cliente | Aplicación web hecha en React que se ejecuta en el navegador del responsable. Es la encargada de mantener la conexión WebSocket y de mostrar las notificaciones que llegan. |
| Servidor | Componente backend que ofrece la API REST y gestiona las conexiones WebSocket. Lanza eventos a los clientes que estén conectados cuando se producen cambios en los datos. |
| API REST de Soincon | Interfaz de programación que da Soincon para consultar y modificar los documentos guardados en EMI Suite 4.0 mediante peticiones HTTP estándar. |
| Historial de notificaciones | Colección ordenada por fecha de todas las notificaciones recibidas durante la sesión activa del usuario. Se guarda en el estado de React y se pierde al cerrar el navegador. |
| Estado de la conexión | Indicador que dice si el canal WebSocket está activo y funcionando bien. Los posibles valores son: conectado, conectando (internamente), desconectado y error. |
| Sesión | Periodo de tiempo durante el cual un usuario autenticado tiene acceso activo a la aplicación, desde que inicia sesión hasta que la cierra o se le acaba el tiempo. |

---

## 3.1.4 Descripción del diagrama de objetos

El diagrama de objetos muestra una instancia concreta del sistema en un momento determinado, representando objetos reales y sus relaciones durante el flujo de recepción de una notificación. En este caso, el servidor de Soincon gestiona una conexión WebSocket activa y un documento modificado, que genera un evento de tipo modificación. Dicho evento se transforma posteriormente en una notificación visible para el usuario.

El diagrama también refleja cómo las notificaciones se almacenan en el historial, diferenciando entre avisos pendientes de leer y notificaciones ya leídas. Además, se incluye la interacción con un responsable mediante una conversación de chat, donde una notificación puede dar lugar a mensajes asociados para consultar o resolver el aviso recibido.

En conjunto, el diagrama permite ver cómo los elementos principales del sistema se relacionan en tiempo de ejecución: servidor externo, conexión WebSocket, documento, evento, notificación, historial y conversación de chat.

![Diagrama de objetos](../../imagenes/diagramaObjetos.svg)
[Código fuente](../../codigoFuente/diagramaObjetos.puml)

---

[Anterior: Capítulo 2 (intro)](../README.md) | [Siguiente: 3.2 Disciplina de Requisitos](../3.2_Disciplina_de_Requisitos/README.md) | [Presentación del trabajo](../PRESENTACION.md)
