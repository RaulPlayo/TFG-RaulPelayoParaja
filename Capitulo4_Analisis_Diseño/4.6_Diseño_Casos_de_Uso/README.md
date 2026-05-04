# 4.6 Diseño de Casos de Uso

[Volver al capítulo 4](../README.md) | [Volver al índice principal](../../README.md)

---

En esta fase bajamos al nivel de diseño concreto, identificando los módulos reales que implementan cada caso de uso. A diferencia del análisis, aquí ya usamos los nombres de las clases, hooks y servicios que hay en el proyecto.

---

## CU-01: Iniciar sesión

Participan `LoginForm`, `useAuth`, `AuthService` y `App`. `LoginForm` recoge las credenciales; `useAuth` coordina el flujo; `AuthService` gestiona la sesión; `App` elige la interfaz que hay que renderizar.

---

## CU-02: Modificar documento en EMI Suite

Participan `Dashboard`, `SocketOperation`, `useWebSocket` y `NotificationItem`. En este proyecto no hay un módulo que edite directamente documentos de EMI Suite; la modificación se representa mediante las acciones de simulación de la página principal, que lanzan un `CustomEvent` con una operación como `COMMENT`, `MATERIAL` o `OUTPUT`. `useWebSocket` captura ese evento, lo transforma en una notificación interna y genera el objeto que luego mostrará `NotificationItem`. Es decir, el sistema no modifica EMI Suite, sino que modela y visualiza el evento que resultaría de esa modificación.

---

## CU-03: Recibir notificación en tiempo real

Participan `useWebSocket`, `websocket.service`, `SOCKET_CONFIG`, `NotificationsContainer` y `NotificationItem`. `websocket.service` establece la conexión STOMP con el broker y se suscribe a los temas configurados en `SOCKET_CONFIG`; cuando llega un mensaje, lo normaliza y se lo pasa al hook `useWebSocket`. Este hook construye la notificación funcional y actualiza el estado. `NotificationsContainer` renderiza la pila de avisos y `NotificationItem` presenta cada notificación individual, incluyendo sonido, estilo visual y acciones rápidas.

---

## CU-04: Consultar historial de notificaciones

Participan `NotificationsContainer`, `useWebSocket` y `NotificationItem`. `useWebSocket` mantiene en memoria la colección `notifications`, que actúa como historial de eventos recibidos. `NotificationsContainer` controla la apertura del panel de historial mediante `showHistory` y recupera esa lista para mostrarla entera. Cada elemento del historial se representa con `NotificationItem`, reutilizando la misma estructura visual de las notificaciones emergentes.

---

## CU-05: Marcar notificación como leída

Participan `NotificationsContainer`, `NotificationItem` y `useWebSocket`. En la vista de avisos, `NotificationItem` permite descartar una notificación visible y llama a `dismissNotification`, que en `useWebSocket` marca el campo `isRead` de esa notificación. Desde `NotificationsContainer` se puede ejecutar `markAllAsRead` para marcar todo el historial como leído de una sola vez. El cambio afecta al contador de no leídas y a la lista de toasts activos.

---

## CU-06: Eliminar notificación

Cuando el usuario borra una notificación desde el historial, `NotificationItem` invoca la acción que recibe por props y `NotificationsContainer` delega en `removeNotification`. Esa operación se implementa en `useWebSocket`, donde se filtra la notificación por id y se actualiza la colección guardada. También existe el borrado masivo mediante `clearAll`, que se puede hacer desde el panel de historial.

---

## CU-07: Enviar mensaje de incidencia mediante chat

Participan `NotificationItem`, `NotificationsContainer`, `ChatContext`, `ChatPanel` y `useWebSocket`. El flujo puede empezar desde una notificación concreta: `NotificationItem` usa `openChatWithAttachment` para abrir el chat adjuntando la incidencia seleccionada. `ChatContext` mantiene el estado global del chat, el adjunto activo y las conversaciones. `ChatPanel` permite elegir destinatario, redactar el mensaje y enviarlo mediante `sendMessage`; además, puede adjuntar manualmente notificaciones recientes obtenidas desde `useWebSocket`. El envío queda registrado en la conversación y el contexto genera una respuesta simulada.

---

## CU-08: Cerrar sesión

Participan `Dashboard`, `useAuth`, `AuthService`, `websocket.service` y `App`. El usuario inicia el cierre desde el botón de salida en `Dashboard`. `useAuth` coordina el proceso llamando a `AuthService.clearToken` para borrar la sesión y a `websocket.service.disconnect` para cerrar la conexión en tiempo real. Después, `App` vuelve a comprobar el estado de autenticación y deja de renderizar el panel principal, mostrando otra vez `LoginForm`.

---

[Anterior: 4.5 Diseño de la Arquitectura](../4.5_Diseno_Arquitectura/README.md) | [Siguiente: 4.7 Diseño de Clases](../4.7_Diseno_Clases/README.md)
