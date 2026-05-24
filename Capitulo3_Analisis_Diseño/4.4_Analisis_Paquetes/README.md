# 4.4 Análisis de Paquetes

[Volver al capítulo 3](../README.md) | [Volver al índice principal](../../README.md)

---

![](../../imagenes/diagramaPaquetes.png)
[Código fuente](../../codigoFuente/diagramaPaquetes.puml)

# Descripcion del diagrama de paquetes

El diagrama de paquetes representa la organizacion principal del sistema de notificaciones desarrollado para EMI Suite. La aplicacion se estructura como un cliente web React dividido en paquetes funcionales, separando la interfaz de usuario, el control de estado, los servicios de comunicacion, la configuracion, los tipos de datos y los recursos multimedia.

El paquete **Presentacion** contiene las vistas y componentes visibles de la aplicacion: autenticacion, panel principal, historial de notificaciones y chat de incidencias. Estos componentes no gestionan directamente la conexion con el exterior, sino que delegan esa responsabilidad en el paquete **Control de aplicacion**, formado por hooks y contextos como `useWebSocket`, `useAuth`, `ChatContext` y `ThemeContext`.

El paquete **Servicios** encapsula la logica de comunicacion. `auth.service` gestiona la autenticacion y el token de sesion, mientras que `websocket.service` establece la conexion STOMP/WebSocket, se suscribe a los topics configurados y normaliza los mensajes recibidos. Este paquete depende de **Configuracion**, donde se definen los endpoints, el broker WebSocket y los canales de suscripcion.

El paquete **Modelo y tipos** agrupa las estructuras principales que circulan por la aplicacion, como `WebSocketMessage`, `NotificationItem`, `ConnectionStatus` y `ChatMessage`. Estas estructuras permiten transformar los eventos recibidos desde EMI Suite en notificaciones, historial y mensajes de incidencia.

Por ultimo, el paquete **Sistema externo** representa EMI Suite y el broker STOMP/WebSocket. EMI Suite publica eventos en el broker, y la aplicacion los recibe mediante `websocket.service` para mostrarlos como notificaciones en tiempo real.

---

[Anterior: 4.3 Análisis de Clases](../4.3_Analisis_Clases/README.md) | [Siguiente: 4.5 Diseño de la Arquitectura](../4.5_Diseño_Arquitectura/README.md)
