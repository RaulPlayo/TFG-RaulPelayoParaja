# 3.2 Disciplina de Requisitos

[Volver al capítulo 2](../README.md) | [Volver al índice principal](../../README.md)

---

La disciplina de requisitos es el proceso en el que identificamos y describimos de forma clara lo que tiene que hacer el sistema. En este proyecto hemos seguido el enfoque de casos de uso, que es una técnica estándar en ingeniería del software para describir el sistema desde el punto de vista de quienes interactúan con él.

---

## 3.2.1 Actores del sistema

| Actor | Descripción |
|---|---|
| Responsable del centro de control | La persona que accede a la aplicación web desde el navegador. Consulta las notificaciones que llegan, las marca como leídas, las borra cuando le parece oportuno y también puede contactar con otros operarios mediante el chat. |
| Operario del servidor de Soincon | La persona que trabaja con EMI Suite 4.0 de Soincon y hace operaciones sobre los documentos del sistema (crear o modificar registros). No interactúa directamente con la aplicación de este TFG, pero sus acciones son el origen de los eventos que provocan las notificaciones que recibe el responsable. |

---

## 3.2.2 Encontrar casos de uso

### Casos de uso

| ID | Nombre | Actor principal| Descripción breve |
|----|--------|-------|-------------------|
| CU-01 | Iniciar sesión | Responsable | El Responsable introduce credenciales para acceder al sistema. |
| CU-02 | Crear Herramienta | Operario | El Operario registra una nueva herramienta en el sistema. Genera notificación. |
| CU-03 | Consultar Herramientas | Operario | El Operario consulta la lista de herramientas registradas. |
| CU-04 | Editar Herramienta | Operario | El Operario modifica los datos de una herramienta existente. Genera notificación. |
| CU-05 | Eliminar Herramienta | Operario | El Operario elimina una herramienta del sistema. Genera notificación. |
| CU-06 | Crear Incidencia | Operario | El Operario registra una nueva incidencia en la planta. Genera notificación. |
| CU-07 | Consultar Incidencias | Operario | El Operario consulta la lista de incidencias registradas. |
| CU-08 | Editar Incidencia | Operario | El Operario actualiza el estado o los datos de una incidencia. Genera notificación. |
| CU-09 | Eliminar Incidencia | Operario | El Operario elimina una incidencia resuelta. Genera notificación. |
| CU-10 | Crear Actividad | Operario | El Operario registra una nueva actividad en la planta. Genera notificación. |
| CU-11 | Consultar Actividades | Operario | El Operario consulta la lista de actividades registradas. |
| CU-12 | Editar Actividad | Operario | El Operario modifica los datos de una actividad existente. Genera notificación. |
| CU-13 | Eliminar Actividad | Operario | El Operario elimina una actividad completada. Genera notificación. |
| CU-14 | Crear Operario | Operario | El Operario registra un nuevo operario en el sistema. Genera notificación. |
| CU-15 | Consultar Operarios | Operario | El Operario consulta la lista de operarios registrados. |
| CU-16 | Editar Operario | Operario | El Operario modifica los datos de un operario existente. Genera notificación. |
| CU-17 | Eliminar Operario | Operario | El Operario elimina un operario del sistema. Genera notificación. |
| CU-18 | Recibir notificación en tiempo real | Responsable | El sistema muestra automáticamente al Responsable una notificación cuando el Operario realiza una operación de escritura. |
| CU-19 | Consultar historial de notificaciones | Responsable | El Responsable visualiza todas las notificaciones recibidas en la sesión activa. |
| CU-20 | Marcar notificación como leída | Responsable | El Responsable indica que ya ha procesado una notificación concreta. |
| CU-21 | Eliminar notificación | Responsable | El Responsable elimina una notificación del historial. |
| CU-22 | Enviar mensaje de incidencia | Responsable | El Responsable envía un mensaje a un operario, pudiendo adjuntar una notificación del historial. |
| CU-23 | Cerrar sesión | Responsable | El Responsable cierra su sesión activa en la aplicación. |

### Casos de uso del actor Responsable

![Diagrama de casos de uso](../../imagenes/diagramaCasosDeUso1.svg)

### Casos de uso del actor Operario

![Diagrama de casos de uso](../../imagenes/diagramaCasosDeUso2.png)


---

## 3.2.3 Priorizar casos de uso

| ID | Nombre | Prioridad | Justificación |
|----|--------|-----------|----------------|
| CU-01 | Iniciar sesión | **Alta** | Puerta de entrada al sistema. Sin autenticación no es posible acceder a nada. |
| CU-06 | Crear Incidencia | **Alta** | Es la operación más crítica y frecuente. Las incidencias son el principal motivo de notificación y de uso del chat. |
| CU-18 | Recibir notificación en tiempo real | **Alta** | Caso de uso central del proyecto. El sistema existe para este propósito. |
| CU-19 | Consultar historial de notificaciones | **Alta** | El Responsable necesita ver las notificaciones para que el sistema tenga utilidad. |
| CU-07 | Consultar Incidencias | **Alta** | Necesario para que el Operario pueda gestionar el estado de las incidencias activas. |
| CU-08 | Editar Incidencia | **Alta** | Permite actualizar el estado de una incidencia, lo que genera notificación inmediata al Responsable. |
| CU-02 | Crear Herramienta | **Media** | Necesario para el control de recursos, pero de menor urgencia que las incidencias. |
| CU-04 | Editar Herramienta | **Media** | Permite actualizar el estado de una herramienta. |
| CU-05 | Eliminar Herramienta | **Media** | Permite limpiar recursos obsoletos. |
| CU-03 | Consultar Herramientas | **Media** | Necesario para la gestión básica de herramientas. |
| CU-09 | Eliminar Incidencia | **Media** | Permite cerrar incidencias resueltas. |
| CU-10 | Crear Actividad | **Media** | Necesario para la planificación operativa de la planta. |
| CU-11 | Consultar Actividades | **Media** | Necesario para el seguimiento de actividades en curso. |
| CU-12 | Editar Actividad | **Media** | Permite actualizar el estado o asignación de una actividad. |
| CU-13 | Eliminar Actividad | **Media** | Permite cerrar actividades completadas. |
| CU-14 | Crear Operario | **Media** | Necesario para dar de alta nuevas personas en el sistema. |
| CU-15 | Consultar Operarios | **Media** | Necesario para la gestión del equipo de planta. |
| CU-16 | Editar Operario | **Media** | Permite actualizar datos de un operario existente. |
| CU-20 | Marcar notificación como leída | **Media** | Mejora la usabilidad del historial pero no es crítico para el flujo principal. |
| CU-21 | Eliminar notificación | **Media** | Permite gestionar el historial pero no afecta al flujo principal. |
| CU-22 | Enviar mensaje de incidencia | **Media** | Añade valor comunicativo pero el sistema de notificaciones funciona sin él. |
| CU-17 | Eliminar Operario | **Baja** | Operación poco frecuente y con mayor riesgo de impacto en datos asociados. |
| CU-23 | Cerrar sesión | **Baja** | Importante para la seguridad pero no afecta al flujo principal de uso. |
---

## 3.2.4 Detallar casos de uso

### CU-02: Crear herramienta

| Campo | Descripción |
|-------|-------------|
| **Identificador** | CU-02 |
| **Nombre** | Crear Herramienta |
| **Actor principal** | Operario |
| **Actor secundario** | Responsable (recibe la notificación resultante) |
| **Descripción** | El Operario registra una nueva herramienta en EMI Suite 4.0. El sistema almacena los datos y emite automáticamente un evento WebSocket que el Responsable recibe como notificación. |
| **Precondiciones** | El Operario tiene acceso a EMI Suite. Al menos un Responsable tiene la conexión WebSocket activa. |
| **Flujo principal** | 1. El Operario accede al módulo de herramientas. 2. Selecciona la opción de nueva herramienta. 3. Rellena los datos: nombre, tipo, estado y ubicación. 4. Confirma el registro. 5. El sistema almacena la herramienta y emite un evento WebSocket (CU-18). |
| **Flujo alternativo A** | Si algún campo obligatorio está vacío, el sistema muestra un aviso y no permite confirmar hasta completarlo. |
| **Flujo alternativo B** | Si no hay ningún Responsable conectado, el evento se emite igualmente pero no es recibido. No se produce error. |
| **Postcondiciones** | La herramienta queda registrada en el sistema. El Responsable ha recibido la notificación correspondiente. |


![DIAGRAMA CREAR HERRAMIENTA](../../imagenes/CrearHerramienta.png)

---

### CU-09: Eliminar Incidencia

| Campo | Descripción |
|-------|-------------|
| **Identificador** | CU-09 |
| **Nombre** | Eliminar Incidencia |
| **Actor principal** | Operario |
| **Actor secundario** | Responsable (recibe la notificación resultante) |
| **Descripción** | El Operario elimina una incidencia ya resuelta del sistema. El sistema elimina el registro y emite un evento WebSocket. |
| **Precondiciones** | Existe al menos una incidencia registrada. |
| **Flujo principal** | 1. El Operario selecciona la incidencia resuelta. 2. El sistema solicita confirmación. 3. El Operario confirma. 4. El sistema elimina el registro y emite un evento WebSocket (CU-18). |
| **Flujo alternativo A** | Si la incidencia tiene actividades asociadas aún activas, el sistema muestra un aviso antes de permitir la eliminación. |
| **Postcondiciones** | La incidencia ha sido eliminada. El Responsable ha recibido la notificación. |

![Eliminar incidencia](../../imagenes/EliminarIncidencia.png)

---

### CU-11: Consultar Actividades

| Campo | Descripción |
|-------|-------------|
| **Identificador** | CU-11 |
| **Nombre** | Consultar Actividades |
| **Actor principal** | Operario |
| **Descripción** | El Operario visualiza la lista de actividades registradas, con su estado, asignación y fecha. Esta operación no genera notificaciones. |
| **Precondiciones** | El Operario tiene acceso a EMI Suite. |
| **Flujo principal** | 1. El Operario accede al módulo de actividades. 2. El sistema muestra la lista con descripción, operario asignado, fecha y estado. 3. El Operario puede filtrar por fecha, estado o asignación. |
| **Flujo alternativo A** | Si no hay actividades registradas, el sistema muestra un mensaje informativo. |
| **Postcondiciones** | El Operario puede ver el listado actualizado de actividades. No se generan notificaciones. |

![Consultar Actividades](../../imagenes/ConsultarActividades.png)

---

### CU-05: Gestionar actividades

| Campo | Descripción |
|---|---|
| Identificador | CU-05 |
| Nombre | Gestionar actividades |
| Actor principal | Operador |
| Actor secundario | Responsable (le llega la notificación). |
| Descripción | El Operario puede crear, consultar, editar y eliminar actividades asignadas en la planta. Cada operación de escritura genera una notificación en tiempo real para el Responsable. |
| Precondiciones | El Operario tiene acceso a EMI Suite 4.0. Al menos un Responsable tiene la conexión WebSocket activa. |
| Flujo principal - crear | 1. El Operario accede al módulo de actividades. <br>2. Selecciona crear nueva actividad. <br>3. Rellena los datos (descripción, operario asignado, fecha, herramientas necesarias). <br>4. Confirma. <br>5. El sistema registra la actividad y emite un evento WebSocket (CU-06). |
| Flujo principal – consultar | 1. El Operario accede al módulo de actividades. <br>2. El sistema muestra la lista de actividades con su estado y asignación. |
| Flujo principal – editar | 1. El Operario selecciona una actividad. <br>2. Modifica los datos. <br>3. Confirma. <br>4. El sistema actualiza la actividad y emite un evento WebSocket (CU-06). |
| Flujo principal – eliminar | 1. El Operario selecciona una actividad completada. <br>2. Confirma la eliminación. <br>3. El sistema elimina el registro y emite un evento WebSocket (CU-06). |
| Flujo alternativo A | Si en el momento de la emisión no hay ningún cliente conectado mediante WebSocket, el servidor genera el evento igualmente, pero no es recibido por ningún cliente. La operación de creación o modificación del documento no se ve afectada. |
| Postcondiciones | La actividad ha sido creada, editada o eliminada. El Responsable ha recibido la notificación correspondiente. |

---

### CU-07: Consultar historial de notificaciones

| Campo | Descripción |
|---|---|
| Identificador | CU-07 |
| Nombre | Consultar historial de notificaciones |
| Actor principal | Responsable |
| Descripción | El usuario visualiza la lista de todas las notificaciones recibidas durante la sesión activa, ordenadas de más reciente a más antigua. |
| Precondiciones | La aplicación está cargada en el navegador. Puede haber cero o más notificaciones en el historial. |
| Flujo principal | 1. El responsable accede a la interfaz de la aplicación. <br>2. El sistema muestra la lista de notificaciones almacenadas en el historial. <br>3. Cada notificación muestra su título, descripción, marca de tiempo y estado (leída/no leída). <br>4. Las notificaciones no leídas se distinguen visualmente de las ya leídas. |
| Flujo alternativo A | Si el historial está vacío, el sistema muestra un mensaje informativo indicando que no hay notificaciones. |
| Postcondiciones | El usuario puede ver el estado actual de todas sus notificaciones. |

![Consultar historial](../../imagenes/ConsultarHistorial.png)


---

## 3.2.5 Prototipar casos de uso

| Caso de uso | Elemento en la interfaz | Descripción visual |
|---|---|---|
| CU-01 (Iniciar sesión) | Panel de login | Una interfaz simple en donde el responsable de la aplicación deberá iniciar sesión para utilizarla. |
| CU-02 (Gestionar operarios) | Módulo de operarios en EMI Suite | Lista de operarios con botones de crear, editar y eliminar. Formulario emergente para crear o editar con campos de nombre, rol y datos de contacto. |
| CU-03 (Gestionar herramientas) | Módulo de herramientas en EMI Suite | Lista de herramientas con nombre, tipo y estado. Botones de crear, editar y eliminar. Formulario emergente para crear o editar. |
| CU-04 (Gestionar incidencias) | Módulo de incidencias en EMI Suite | Lista de incidencias con descripción, gravedad y estado. Las de gravedad alta se destacan visualmente. Botones de crear, editar y eliminar. |
| CU-05 (Gestionar actividades) | Módulo de actividades en EMI Suite | Lista de actividades con descripción, operario asignado y fecha. Botones de crear, editar y eliminar. |
| CU-06 (Recibir notificación en tiempo real) | Tarjeta emergente | Aparece en la esquina inferior derecha al llegar una notificación nueva. Muestra título, mensaje y timestamp. |
| CU-07 (Consultar historial de notificaciones) | Panel del historial | Lista vertical ordenada de más reciente a más antigua. Cada tarjeta muestra título, mensaje, timestamp y estado leída/no leída con diferenciación visual clara. |
| CU-08 (Marcar notificación como leída) | Botón de “leídas” | Visible al entrar en el historial. Al pulsarlo, las demás notificaciones desaparecen y sale una tarjeta emergente informando de que se han leído. |
| CU-09 (Eliminar notificación) | Botón de “limpiar” | También visible solo en el historial. Al pulsar, todas las notificaciones se borrarán. |
| CU-10 (Enviar mensaje de incidencia mediante chat) | Ventana/panel de chat | Área de mensajes con listado de conversaciones, campo de texto para escribir, selector de destinatarios (operarios) y opción para adjuntar una notificación existente como referencia. |
| CU-11 (Cerrar sesión) | Botón | Botón en el que está escrito cerrar sesión. Una vez pulsado, te dirige al CU-01 (Panel del login). |

Además, fuera de los casos de uso, hay un **indicador de conexión**, en el que si estás conectado sale de color verde, mientras que si estás conectando o desconectado sale gris.

---

## 3.2.6 Estructurar casos de uso

| ID | Nombre | Actor principal | Incluye | Extiende a |
|---|---|---|---|---|
| CU-01 | Iniciar sesión | Responsable | — | — |
| CU-02 | Gestionar operarios | Operador | CU-06 | — |
| CU-03 | Gestionar herramientas | Operador | CU-06 | — |
| CU-04 | Gestionar incidencias | Operador | CU-06 | — |
| CU-05 | Gestionar actividades | Operador | CU-06 | — |
| CU-06 | Recibir notificación en tiempo real | Responsable | — | — |
| CU-07 | Consultar historial de notificaciones | Responsable | — | — |
| CU-08 | Marcar notificación como leída | Responsable | — | CU-07 |
| CU-09 | Eliminar notificación | Responsable | — | CU-07 |
| CU-10 | Enviar mensaje de incidencia | Responsable | CU-07 (si se adjunta una notificación del historial) | — |
| CU-11 | Cerrar sesión | Responsable | — | — |

[Anterior: 3.1 Modelo del Dominio](../3.1_Modelo_del_Dominio/README.md) | [Siguiente: 3.3 Requisitos No Funcionales](../3.3_Requisitos_No_Funcionales/README.md)
