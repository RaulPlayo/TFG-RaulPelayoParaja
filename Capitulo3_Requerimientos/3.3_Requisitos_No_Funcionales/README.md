# 3.3 Requisitos No Funcionales

[Volver al capítulo 3](../README.md) | [Volver al índice principal](../../README.md)

---

Los requisitos no funcionales describen las propiedades de calidad que debe cumplir el sistema más allá de lo que hace. No cuentan qué hace el sistema, sino cómo lo hace.

---

## Requisitos funcionales (RF)

| ID | Nombre | Tipo | Prioridad | Descripción |
|---|---|---|---|---|
| RF01 | Autenticación de administrador | Funcional | Alta | Solo los usuarios con rol de administrador pueden acceder a la aplicación con usuario y contraseña. |
| RF02 | Recepción de eventos en tiempo real | Funcional | Alta | El sistema mantiene una conexión permanente con el servidor y muestra notificaciones automáticamente al detectar cambios en EMI Suite. |
| RF03 | Consulta del historial | Funcional | Alta | El sistema le muestra al administrador todas las notificaciones de la sesión activa, ordenadas de la más reciente a la más antigua. |
| RF04 | Marcar notificación como leída | Funcional | Media | El administrador puede marcar cualquier notificación como leída, y su apariencia en el historial cambia. |
| RF05 | Eliminar notificación | Funcional | Media | El administrador puede borrar notificaciones del historial de una en una, y la lista se actualiza al instante. |
| RF06 | Envío de mensaje de incidencia | Funcional | Media | El administrador puede escribir y enviar mensajes a operarios desde el chat integrado, con opción de adjuntar una notificación como contexto. |

---

## Requisitos no funcionales (RNF)

| ID | Nombre | Tipo | Prioridad | Descripción |
|---|---|---|---|---|
| RNF01 | Latencia de notificaciones | Rendimiento | Alta | El tiempo que pasa desde que se emite un evento en el servidor hasta que se ve en pantalla no será mayor de 200 ms en condiciones normales de red. |
| RNF02 | Capacidad de procesamiento | Rendimiento | Media | El sistema podrá procesar varios eventos por segundo sin que el administrador note que la interfaz se resiente. |
| RNF03 | Tiempo de carga inicial | Rendimiento | Media | La aplicación estará lista para usarse en menos de 3 segundos con una conexión de banda ancha normal. |
| RNF04 | Usabilidad sin formación técnica | Usabilidad | Alta | La interfaz seguirá las convenciones visuales estándar para que el administrador pueda usarla sin que le tengan que explicar nada. |
| RNF05 | Indicador de estado de conexión | Usabilidad | Media | El estado de la conexión WebSocket (conectado / desconectado) se verá siempre en la interfaz. |
| RNF06 | Modularidad del componente | Mantenibilidad | Media | El componente de notificaciones estará desacoplado del resto de la aplicación y seguirá las convenciones de React. |
| RNF07 | Compatibilidad con navegadores | Compatibilidad | Alta | La aplicación funcionará bien en las versiones actuales de Chrome, Firefox, Safari y Edge, con un diseño responsive que se adapte a tablets. |
| RNF08 | Gestión de fallos de conexión | Confiabilidad | Alta | Ante una pérdida de conexión o mensajes mal formados, el sistema avisará al administrador sin que se bloquee la interfaz. |

---

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

[Anterior: 3.2 Disciplina de Requisitos](../3.2_Disciplina_de_Requisitos/README.md) | [Siguiente: 3.4 Mockups](../3.4_Mockups/README.md)
