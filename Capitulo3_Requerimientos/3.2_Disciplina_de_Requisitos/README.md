# 3.2 Disciplina de Requisitos

[Volver al capítulo 3](../README.md) | [Volver al índice principal](../../README.md)

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

| ID | Nombre | Actor principal | Descripción |
|---|---|---|---|
| CU-01 | Iniciar sesión | Responsable | El administrador mete sus credenciales para entrar al sistema. Solo los usuarios con rol de administrador pueden acceder. |
| CU-02 | Gestionar operarios | Operador | El operario puede crear, consultar, editar y eliminar operarios del sistema. Cada operación genera una notificación en tiempo real.  |
| CU-03 | Gestionar herramientas | Operador | El operario puede crear, consultar, editar y eliminar herramientas de la planta. Cada operación genera una notificación en tiempo real.  |
| CU-04 | Gestionar incidencias | Operador | El operario puede crear, consultar, editar y eliminar incidencias registradas en la planta. Cada operación genera una notificación en tiempo real.  |
| CU-05 | Gestionar actividades | Operador | El operario puede crear, consultar, editar y eliminar actividades asignadas en la planta. Cada operación genera una notificación en tiempo real. |
| CU-06 | Recibir notificación en tiempo real | Responsable | El sistema recibe el evento que ha lanzado el servidor y lo muestra como notificación al usuario de forma automática, sin que él tenga que hacer nada. |
| CU-07 | Consultar historial de notificaciones | Responsable | El responsable puede ver la lista de todas las notificaciones que han llegado durante la sesión activa. |
| CU-08 | Marcar notificación como leída | Responsable | El responsable indica que ya ha visto y procesado una notificación concreta. |
| CU-19 | Eliminar notificación | Responsable | El responsable borra una notificación concreta del historial. |
| CU-10 | Enviar mensaje de incidencia | Responsable | El responsable envía un mensaje a uno o varios operarios para avisarles de una incidencia, y puede adjuntar una notificación recibida para dar contexto. |
| CU-11 | Cerrar sesión | Responsable | Cuando termina el trabajo, el responsable cierra su sesión en la aplicación. |

![Diagrama de casos de uso](../../imagenes/diagramaCasosDeUso.png)

---

## 3.2.3 Priorizar casos de uso

| ID | Nombre | Prioridad | Justificación |
|---|---|---|---|
| CU-01 | Iniciar sesión | Alta | Sin autenticación no hay acceso al sistema. |
| CU-02 – CU-05 | Gestionar operarios, herramientas, incidencias y actividades | Alta | Son las entidades centrales del sistema. Las incidencias son el principal origen de notificaciones y el motivo de uso del chat. |
| CU-06 | Recibir notificación en tiempo real | Alta | Es el caso de uso central del proyecto. El sistema existe para este propósito. |
| CU-07 | Consultar historial de notificaciones | Alta | El responsable necesita poder ver las notificaciones recibidas para que el sistema sea útil. |
| CU-08 | Marcar notificación como leída | Media | Mejora la usabilidad del sistema pero no es imprescindible para el funcionamiento básico. |
| CU-09 | Eliminar notificación | Media | Permite al responsable gestionar su historial pero no afecta al flujo principal. |
| CU-10 | Enviar mensaje de incidencia mediante chat | Media | Mejora la gestión de incidencias permitiendo comunicación directa entre usuarios y operarios, pero el sistema de notificaciones en tiempo real funciona sin este chat. |
| CU-11 | Cerrar sesión | Media | Permite al usuario cerrar la sesión. Una vez cerrada, se renuevan las notificaciones que lleguen y el contador de ellas se pone en 0. |

---

## 3.2.4 Detallar casos de uso

### CU-01: Iniciar sesión

| Campo | Descripción |
|---|---|
| Identificador | CU-01 |
| Nombre | Iniciar sesión. |
| Actor principal | Responsable |
| Descripción | El administrador introduce sus credenciales (usuario y contraseña) para acceder a la aplicación. El sistema solo permite el acceso a usuarios con rol de administrador. |
| Precondiciones | La aplicación está disponible y accesible desde el navegador. El usuario dispone de credenciales de administrador válidas. |
| Flujo principal | 1. El usuario accede a la página de inicio de sesión. <br>2. El usuario introduce su nombre de usuario y contraseña. <br>3. El sistema verifica que las credenciales corresponden a un administrador. <br>4. El sistema inicia la sesión y redirige al administrador al panel principal. |
| Flujo alternativo | Si las credenciales son incorrectas o el usuario no tiene permisos, el sistema muestra el mensaje “Acceso restringido al personal autorizado”. |
| Postcondiciones | El administrador tiene acceso al sistema y puede interactuar con todas sus funcionalidades. |

---

### CU-02: Gestionar operarios

| Campo | Descripción |
|---|---|
| Identificador | CU-02 |
| Nombre | Gestionar operarios |
| Actor principal | Operador |
| Actor secundario | Responsable (le llega la notificación). |
| Descripción | El operario puede crear, consultar, editar y eliminar operarios del sistema a través de EMI Suite 4.0. Cualquier operación de escritura (crear, editar, eliminar) genera automáticamente un evento WebSocket que el responsable recibe como notificación en tiempo real. |
| Precondiciones | El Operario tiene acceso a EMI Suite 4.0. Al menos un Responsable tiene la conexión WebSocket activa. |
| Flujo principal - crear | 1. El Operario accede al módulo de operarios en EMI Suite. <br>2. Selecciona la opción de crear nuevo operario. <br>3. Confirma la creación. <br>4. El sistema registra el nuevo operario y emite un evento WebSocket (CU-06). |
| Flujo principal – consultar | 1. El Operario accede al módulo de operarios. <br>2. El sistema muestra la lista de operarios registrados. <br>3. El Operario puede filtrar o buscar por nombre o rol. |
| Flujo principal – editar | 1. El Operario selecciona un operario de la lista. <br>2. Modifica los datos necesarios. <br>3. Confirma los cambios. <br>4. El sistema actualiza el registro y emite un evento WebSocket (CU-06). |
| Flujo principal – eliminar | 1. El Operario selecciona un operario de la lista. <br>2. Selecciona la opción de eliminar. <br>3. El sistema solicita confirmación. <br>4. El Operario confirma. <br>5. El sistema elimina el registro y emite un evento WebSocket (CU-06). |
| Flujo alternativo A | Si en el momento de la emisión no hay ningún cliente conectado mediante WebSocket, el servidor genera el evento igualmente, pero no es recibido por ningún cliente. La operación de creación o modificación del documento no se ve afectada. |
| Flujo alternativo B | Si el operador no guarda los cambios realizados, no se registra ninguna operación en la base de datos y no se emite ningún evento WebSocket. |
| Postcondiciones | El operario ha sido creado, editado o eliminado en el sistema. Se ha emitido un evento WebSocket que el Responsable ha recibido como notificación. |

---

### CU-03: Gestionar herramientas

| Campo | Descripción |
|---|---|
| Identificador | CU-03 |
| Nombre | Gestionar herramientas |
| Actor principal | Operador |
| Actor secundario | Responsable (le llega la notificación). |
| Descripción | El operario puede crear, consultar, editar y eliminar herramientas de la planta a través de EMI Suite 4.0. Cualquier operación de escritura genera automáticamente un evento que el Responsable recibe como notificación en tiempo real. |
| Precondiciones | El Operario tiene acceso a EMI Suite 4.0. Al menos un responsable tiene la conexión WebSocket activa. |
| Flujo principal - crear | 1. El Operario accede al módulo de herramientas. <br>2. Selecciona crear nueva herramienta. <br>3. Rellena los datos (nombre, tipo, estado, ubicación). <br>4. Confirma. <br>5. El sistema registra la herramienta y emite un evento WebSocket (CU-06). |
| Flujo principal – consultar | 1. El Operario accede al módulo de herramientas. <br>2. El sistema muestra la lista de herramientas con su estado actual. |
| Flujo principal – editar | 1. El Operario selecciona una herramienta. <br>2. Modifica los datos (estado, ubicación, etc.). <br>3. Confirma. <br>4. El sistema actualiza el registro y emite un evento WebSocket (CU-06). |
| Flujo principal – eliminar | 1. El Operario selecciona una herramienta. <br>2. Confirma la eliminación. <br>3. El sistema elimina el registro y emite un evento WebSocket (CU-06). |
| Flujo alternativo A | Si en el momento de la emisión no hay ningún cliente conectado mediante WebSocket, el servidor genera el evento igualmente, pero no es recibido por ningún cliente. No se produce ningún error. |
| Postcondiciones | La herramienta ha sido creada, editada o eliminada. Se ha emitido un evento WebSocket que el Responsable ha recibido como notificación. |

---

### CU-04: Gestionar incidencias

| Campo | Descripción |
|---|---|
| Identificador | CU-04 |
| Nombre | Gestionar incidencias |
| Actor principal | Operador |
| Actor secundario | Responsable (le llega la notificación). |
| Descripción | El Operario puede crear, consultar, editar y eliminar incidencias registradas en la planta. |
| Precondiciones | El Operario tiene acceso a EMI Suite 4.0. Al menos un Responsable tiene la conexión WebSocket activa. |
| Flujo principal - crear | 1. El Operario accede al módulo de incidencias. <br>2. Selecciona crear nueva incidencia. <br>3. Rellena los datos (descripción, tipo, gravedad, herramienta o actividad afectada). <br>4. Confirma. <br>5. El sistema registra la incidencia y emite un evento WebSocket de tipo "advertencia" (CU-06). |
| Flujo principal – consultar | 1. El Operario accede al módulo de incidencias. <br>2. El sistema muestra la lista de incidencias con su estado y gravedad. |
| Flujo principal – editar | 1. El Operario selecciona una incidencia. <br>2. Modifica los datos. <br>3. Confirma. <br>4. El sistema actualiza la incidencia y emite un evento WebSocket (CU-06). |
| Flujo principal – eliminar | 1. El Operario selecciona una incidencia resuelta. <br>2. Confirma la eliminación. <br>3. El sistema elimina el registro y emite un evento WebSocket (CU-06). |
| Flujo alternativo A | Si en el momento de la emisión no hay ningún cliente conectado mediante WebSocket, el servidor genera el evento igualmente, pero no es recibido por ningún cliente. No aparecen errores. |
| Postcondiciones | La incidencia ha sido creada, editada o eliminada. El Responsable ha recibido la notificación correspondiente. |

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

### CU-06: Recibir notificaciones en tiempo real

| Campo | Descripción |
|---|---|
| Identificador | CU-06 |
| Nombre | Recibir notificación en tiempo real |
| Actor principal | Responsable |
| Descripción | El servidor de Soincon emite un evento a través del canal WebSocket cuando se produce un cambio en los datos de EMI Suite 4.0. El cliente recibe ese evento y lo transforma en una notificación visual que se muestra al usuario de forma automática. |
| Precondiciones | La conexión WebSocket entre el cliente y el servidor está activa. |
| Flujo principal | 1. El servidor detecta un cambio en los datos (creación o modificación de un documento). <br>2. El servidor construye un mensaje de evento con el tipo de cambio, el identificador del documento afectado y una descripción. <br>3. El servidor emite el evento a través del canal WebSocket. <br>4. El cliente recibe el mensaje a través de la conexión WebSocket activa. <br>5. El componente de notificaciones procesa el mensaje y crea una nueva notificación con título, descripción, tipo y marca de tiempo. <br>6. La notificación se añade al inicio del historial de notificaciones. <br>7. La interfaz se actualiza automáticamente mostrando la nueva notificación al usuario. |
| Flujo alternativo A | Si el formato del mensaje recibido no es válido o está incompleto, el sistema descarta el evento y registra un error en el log sin interrumpir el funcionamiento del resto del sistema. |
| Postcondiciones | El historial de notificaciones contiene una nueva entrada. La notificación está marcada como no leída. El usuario puede verla en la interfaz. |

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

---

### CU-08: Marcar notificación como leída

| Campo | Descripción |
|---|---|
| Identificador | CU-08 |
| Nombre | Marcar notificación como leída |
| Actor principal | Responsable |
| Descripción | El usuario marca una notificación concreta como leída para indicar que ya la ha visto y procesado, cambiando su estado visual en el historial. |
| Precondiciones | Existe al menos una notificación en estado no leído en el historial. |
| Flujo principal | 1. El usuario localiza la notificación que desea marcar como leída en el historial. <br>2. El usuario interactúa con el control correspondiente en esa notificación (botón o click). <br>3. El sistema actualiza el estado de la notificación a leída. <br>4. La interfaz refleja el cambio de estado visualmente de forma inmediata. |
| Flujo alternativo A | Si la notificación ya estaba marcada como leída, el sistema no realiza ningún cambio. |
| Postcondiciones | La notificación queda marcada como leída en el historial. Su apariencia visual refleja el nuevo estado. |

---

### CU-09: Eliminar notificación

| Campo | Descripción |
|---|---|
| Identificador | CU-09 |
| Nombre | Eliminar notificación |
| Actor principal | Responsable |
| Descripción | El usuario elimina una notificación concreta del historial cuando ya no la necesita. |
| Precondiciones | Existe al menos una notificación en el historial. |
| Flujo principal | 1. El usuario localiza la notificación que desea eliminar en el historial. <br>2. El usuario interactúa con el control de eliminación de esa notificación. <br>3. El sistema elimina la notificación del historial. <br>4. La interfaz actualiza la lista de notificaciones mostrando el historial sin la notificación eliminada. |
| Flujo alternativo A | Si tras la eliminación el historial queda vacío, el sistema muestra el mensaje de historial vacío descrito en CU-03. |
| Postcondiciones | La notificación ya no aparece en el historial. El cambio es permanente durante la sesión activa. |

---

### CU-10: Enviar mensaje de incidencia mediante chat

| Campo | Descripción |
|---|---|
| Identificador | CU-10 |
| Nombre | Enviar mensaje de incidencia mediante chat |
| Actor principal | Responsable |
| Actor secundario | Operario de Soincon |
| Descripción | El usuario redacta un mensaje de incidencia y lo envía a uno o varios operarios de Soincon a través del chat integrado, pudiendo adjuntar una notificación recibida para aportar contexto sobre el evento que ha ocurrido. |
| Precondiciones | El responsable tiene acceso a la interfaz del chat. Existe al menos un operario de Soincon disponible como destinatario. Opcionalmente, existe al menos una notificación en el historial para adjuntarla al mensaje. |
| Flujo principal | 1. El usuario abre el chat. <br>2. El usuario selecciona uno o varios operarios destinatarios. <br>3. El usuario escribe el mensaje de incidencia. <br>4. El usuario, si lo desea, selecciona una notificación del historial para adjuntarla al mensaje. <br>5. El usuario envía el mensaje. <br>6. El sistema registra el mensaje y lo entrega a los operarios seleccionados. <br>7. Los operarios pueden visualizar el mensaje en su interfaz correspondiente. |
| Postcondiciones | La incidencia queda registrada y enviada a los operarios seleccionados. Los operarios pueden consultar el contenido del mensaje y, si se adjuntó, la notificación asociada. |

---

### CU-11: Cerrar sesión

| Campo | Descripción |
|---|---|
| Identificador | CU-11 |
| Nombre | Cerrar sesión |
| Actor principal | Responsable |
| Descripción | El Responsable cierra su sesión activa en la aplicación. El sistema elimina la sesión y redirige al usuario a la pantalla de inicio de sesión, impidiendo el acceso a cualquier funcionalidad sin volver a autenticarse. |
| Precondiciones | El Responsable tiene una sesión activa iniciada en la aplicación. |
| Flujo principal | 1. El Responsable pulsa el botón de cerrar sesión. <br>2. El sistema invalida la sesión activa del usuario. <br>3. El sistema cierra la conexión WebSocket asociada a esa sesión. <br>4. El sistema redirige al usuario a la pantalla de inicio de sesión. |
| Flujo alternativo | Si se pierde la conexión con el servidor durante el cierre de sesión, el sistema elimina igualmente los datos de sesión locales y redirige al usuario a la pantalla de inicio de sesión. |
| Postcondiciones | La sesión del Responsable ha sido eliminada. No es posible acceder a ninguna funcionalidad de la aplicación sin volver a iniciar sesión. La conexión WebSocket ha sido cerrada correctamente. |

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
