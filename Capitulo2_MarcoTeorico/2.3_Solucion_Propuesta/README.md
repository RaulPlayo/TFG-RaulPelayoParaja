# 2.3 Solución Propuesta

[Volver al capítulo 2](../README.md) | [Volver al índice principal](../../README.md)

---

La solución sugerida en este trabajo es el diseño y la implementación de un sistema de notificaciones en tiempo real que consta de dos componentes principales: una aplicación cliente construida en React, que recibe los eventos y los muestra al usuario inmediatamente; y un servidor backend, que se encarga de gestionar la información y generar dichos eventos.

La eliminación del modelo de actualización manual es el comienzo del diseño. El sistema sostiene una conexión activa con el servidor en vez de que el usuario tenga que refrescar la página o hacer clic en un botón para ver los datos más recientes. Esta conexión se implementa mediante el protocolo WebSocket.

---

## 2.3.1 Arquitectura general del sistema

El sistema sigue una arquitectura cliente-servidor con un canal de comunicación dual. Por un lado, el cliente puede interactuar con el servidor a través de una API REST (la API de la empresa Soincon) para realizar las operaciones de consulta y modificación de datos. Por otro lado, existe una conexión WebSocket persistente que el servidor utiliza para notificar al cliente los cambios en tiempo real.

Esta separación entre la API REST y el canal WebSocket es una decisión de diseño deliberada. La API REST es adecuada para operaciones puntuales donde el cliente solicita algo y espera una respuesta concreta: consultar un documento, crearlo o modificarlo. El WebSocket, en cambio, se reserva para el flujo de eventos asíncronos que el servidor necesita comunicar al cliente en el momento en que se producen. Esta separación de responsabilidades hace el sistema más claro, más fácil de mantener y más fácil de extender.

---

## 2.3.2 Componentes principales

El sistema se compone de cuatro módulos primordiales, cada uno con una responsabilidad claramente definida:

**Gestor de conexión WebSocket:** módulo encargado de crear el vínculo con el servidor, mantenerlo en funcionamiento a través del envío regular de mensajes keepalive, identificar las desconexiones y manejar la reconexión automática con un backoff exponencial para evitar que el servidor quede colapsado si se produce una caída.

**Integración con la API de Soincon:** en vez de crear un backend propio desde el principio, el sistema utiliza la API REST de Soincon para obtener información de EMI Suite 4.0. Esto posibilita que el proyecto se base en datos auténticos de un ambiente industrial, sumando valor práctico al desarrollo.

**Componente de notificaciones React:** componente reutilizable que se suscribe al administrador de conexión WebSocket y gestiona los eventos recibidos, guardándolos en el estado local de React.

**Interfaz visual:** capa de presentación que enseña las notificaciones al usuario de manera explícita y no invasiva, utilizando animaciones de entrada y salida y distinciones visuales en función del tipo de evento recibido.

---

## 2.3.3 Flujo de datos

1. El cliente web se abre y se conecta con el servidor a través de WebSocket. Durante toda la sesión del usuario, esta conexión se mantiene activa.

2. Si se da un cambio en los datos (ya sea porque lo realice el mismo usuario u otro usuario del sistema), el servidor actualiza la base de datos y manda un evento WebSocket con la información pertinente sobre el cambio.

3. El cliente recibe ese evento por medio de la conexión WebSocket activa, lo procesa y renueva el estado del componente de notificaciones.

4. React detecta el cambio de estado y vuelve a mostrar el componente que ha sido modificado, sin que sea necesario que el usuario realice ninguna acción ni que la página tenga que recargarse.

Este flujo es fundamentalmente diferente al modelo antiguo del polling, ya que aquí no se envía una solicitud al servidor para saber si hubo cambios.

---

## 2.3.4 Criterios de diseño

**Reutilización:** el componente de notificaciones está diseñado para funcionar de forma independiente del resto del sistema, con una interfaz de configuración simple que permite adaptarlo a diferentes proyectos con cambios mínimos.

**Simplicidad:** se ha buscado la solución más directa para cada problema, evitando añadir capas de abstracción o dependencias externas que no estén justificadas por las necesidades concretas del sistema.

**Robustez:** el gestor de conexión incluye lógica de reconexión automática y manejo de errores para que el sistema sea resiliente ante problemas de red.

**Observabilidad:** el sistema incluye logging detallado de los eventos de conexión y desconexión, lo que facilita el diagnóstico de problemas en producción.

---

[Anterior: 2.2 Estado del Arte](../2.2_Estado_del_Arte/README.md) | [Siguiente: 2.4 Objetivos](../2.4_Objetivos/README.md)
