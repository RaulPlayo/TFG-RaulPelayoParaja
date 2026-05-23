# 4.2 Análisis de Casos de Uso

[Volver al capítulo 3](../README.md) | [Volver al índice principal](../../README.md)

---

## consultarHistorial()

![](../../imagenes/colabHistorial.svg)
[Código fuente](../../codigoFuente/colabHistorial.puml)


Este diagrama muestra como el responsable solicita consultar el historial de notificaciones. La vista de historial envia la peticion al controlador, que recupera las notificaciones almacenadas desde `HistorialNotificaciones`. Finalmente, el listado se devuelve ordenado a la vista para que el responsable pueda visualizarlo.

## enviarMensajeDeIncidencia()

![](../../imagenes/colabIncidencia.svg)
[Código fuente](../../codigoFuente/colabIncidencia.puml)
   
[IMÁGEN EXTENDIDA](../../imagenes/colabIncidenciaPNG.png)


Este diagrama representa el envio de un mensaje de incidencia asociado a una notificacion. El responsable selecciona una notificacion, el controlador de chat la recupera del historial y abre la vista de chat con la notificacion adjunta. Despues, se crea el mensaje de incidencia, se envia al responsable tecnico y se actualiza la conversacion.

## verNotificacion()

![](../../imagenes/colabNotificacion.svg)
[Código fuente](../../codigoFuente/colabNotificacion.puml)

Este diagrama describe el proceso de visualizacion de una notificacion concreta. El responsable selecciona una notificacion del historial, la vista solicita sus datos al controlador y este recupera el detalle desde el historial. A continuacion, la notificacion se marca como leida y se muestra su informacion completa en la vista correspondiente.


[Anterior: 4.1 Análisis de la Arquitectura](../4.1_Analisis_Arquitectura/README.md) | [Siguiente: 4.3 Análisis de Clases](../4.3_Analisis_Clases/README.md)
