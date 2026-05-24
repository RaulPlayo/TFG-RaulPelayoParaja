# 4.3 Análisis de Clases

[Volver al capítulo 3](../README.md) | [Volver al índice principal](../../README.md)

---

En la etapa de análisis definimos clases conceptuales, sin entrar todavía en detalles técnicos concretos. Estas clases no son aún componentes de React o servicios de TypeScript, sino entidades y roles lógicos del sistema.

![](../../imagenes/diagramaClases.svg)
[Código fuente](../../codigoFuente/diagramaClases.puml)

---

## Clases modelo

**Documento:** representa la información de negocio que hay en EMI Suite y cuyo cambio puede provocar un evento.

**Evento:** representa el mensaje que se genera después de una modificación importante.

**Notificación:** representa la adaptación de un evento a un formato que el usuario final pueda entender fácilmente.

**HistorialNotificaciones:** representa el conjunto de notificaciones que se han generado durante una sesión y las operaciones que se pueden hacer sobre ellas.

**ConexiónWebSocket:** representa el mecanismo de conexión que se mantiene siempre abierta con el servidor de eventos.

---

## Clases vista

**VistaLogin:** interfaz del actor responsable para iniciar sesión.

**VistaPanelPrincipal:** vista principal del sistema de monitorización.

**VistaHistorialNotificaciones:** vista para consultar el histórico.

**VistaNotificacion:** representación visual de una notificación individual.

**VistaChatIncidencias:** interfaz para redactar y enviar incidencias.

**VistaDocumento:** vista básica asociada a la representación de un documento de negocio.

**VistaEvento:** vista básica asociada a la representación de un evento recibido.

---

## Clases controlador

**ControladorAutenticación:** coordina el inicio y el cierre de sesión.

**ControladorRecepcionEventos:** coordina la suscripción y la recepción de eventos.

**ControladorHistorial:** coordina la consulta del historial.

**ControladorLecturaNotificacion:** coordina el cambio de estado a "leída".

**ControladorEliminacionNotificacion:** coordina la eliminación de avisos.

**ControladorChatIncidencias:** coordina el envío de mensajes de incidencia.

**ControladorSincronizacionDocumento:** coordina la reacción a los cambios que vienen de EMI Suite.

---

[Anterior: 4.2 Análisis de Casos de Uso](../4.2_Analisis_Casos_de_Uso/README.md) | [Siguiente: 4.4 Análisis de Paquetes](../4.4_Analisis_Paquetes/README.md)
