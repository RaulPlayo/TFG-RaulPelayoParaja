# 2.2 Estado del Arte

[Volver al capítulo 2](./Capitulo2_MarcoTeorico) | [Volver al índice principal](../README.md)

## 2.2.1 La evolución de la comunicación en la web
Para entender el estado actual de la comunicación en tiempo real en la web, es necesario hacer un recorrido por su evolución histórica. Cada etapa ha respondido a necesidades concretas y ha sentado las bases de la siguiente.

En los primeros años de la web, entre mediados de los 90 y principios de los 2000, las páginas eran fundamentalmente estáticas. El modelo de uso era simple: el usuario navegaba a una URL, el servidor devolvía un documento HTML y el navegador lo mostraba. No había actualización automática de contenidos, y cualquier cambio requería recargar la página completa. En este contexto, la latencia no era un problema porque no había expectativa de inmediatez.

A medida que la web fue ganando complejidad y los primeros servicios de correo web y mensajería empezaron a aparecer, surgió la necesidad de simular actualizaciones en tiempo real. La primera solución ampliamente adoptada fue el *polling*: el cliente enviaba peticiones al servidor de forma continua para preguntar si había novedades. Esta técnica era funcional pero enormemente ineficiente, ya que la gran mayoría de las peticiones obtenía una respuesta vacía. Para un sistema con miles de usuarios conectados, el volumen de peticiones innecesarias generaba una carga significativa en los servidores.

La llegada de AJAX (*Asynchronous JavaScript and XML*) a mediados de los 2000 no resolvió el problema de fondo, pero sí mejoró la experiencia de usuario al permitir actualizar partes de la página sin recargarla por completo. Esto, combinado con técnicas de *long polling*, permitió construir aplicaciones más responsivas, aunque a costa de una mayor complejidad en el código.

El gran punto de inflexión llegó con la estandarización de HTML5 y la introducción del protocolo WebSocket en 2011. Por primera vez, la web disponía de un mecanismo nativo y eficiente para mantener comunicaciones bidireccionales en tiempo real. La adopción de WebSocket fue progresiva pero constante, y hoy es el estándar de referencia para este tipo de comunicaciones.

Aplicaciones como Slack, Discord, Trello, Notion o Figma han popularizado el uso de WebSockets como base de su arquitectura en tiempo real. Slack, por ejemplo, utiliza WebSockets para la entrega instantánea de mensajes y notificaciones a sus más de 20 millones de usuarios activos diarios. Discord maneja millones de conexiones WebSocket simultáneas para la comunicación de voz, texto y estado en sus servidores.

## 2.2.2 Tecnologías y métodos actuales
El ecosistema actual de desarrollo frontend está dominado por tres grandes frameworks y librerías basadas en componentes:

* **React:** Desarrollado por Meta, es actualmente la opción más popular. Su principal fortaleza es la flexibilidad: React se describe a sí mismo como una librería, no como un *framework*, lo que significa que solo se ocupa de la capa de vista y deja al desarrollador la libertad de elegir cómo gestionar el estado, el enrutamiento y las peticiones de red. React ha apostado en los últimos años por los componentes funcionales y los *hooks* como modelo principal de desarrollo, simplificando considerablemente el código.
* **Vue.js:** Creado por Evan You, es conocido por su curva de aprendizaje más suave y su sintaxis más cercana al HTML tradicional, lo que lo hace especialmente atractivo para desarrolladores que vienen del desarrollo web más clásico.
* **Angular:** Mantenido por Google, es el más completo de los tres *frameworks*. Proporciona una solución para todos los aspectos del desarrollo *frontend*, desde la gestión del estado hasta las pruebas, el enrutamiento o la comunicación con el servidor. Sin embargo, tiene una curva de aprendizaje significativamente más pronunciada, lo que lo hace más habitual en proyectos empresariales de gran escala.

#### Protocolos y herramientas adicionales
* **STOMP:** (*Simple Text Oriented Messaging Protocol*) es un protocolo de mensajería basado en texto, ligero e interoperable, diseñado para la comunicación asíncrona entre clientes y *brokers* de mensajes. Es ampliamente utilizado para habilitar la mensajería entre diferentes lenguajes y plataformas, a menudo sobre WebSockets.
* **Socket.io:** Es la biblioteca más popular para la implementación de WebSockets. No es solo un *wrapper*: incorpora soporte para salas (*rooms*), reconexión automática, *namespaces* y *fallback* para navegadores antiguos. *Nota: En este proyecto se ha optado por la API nativa para evitar dependencias.*
* **Vite vs Webpack:** En el ámbito de las herramientas de construcción, Vite se ha consolidado como la opción preferida por su rapidez frente al tradicional Webpack, especialmente en combinación con React y Vue.

> ![Gráfico de popularidad](imagenes/popularidad_frameworks.png)
> *Gráfico de popularidad de React VS Vue.js VS Angular.*

## 2.2.3 Diferenciación del proyecto
Este proyecto no pretende competir con Slack o con Discord. El objetivo es demostrar que se puede construir un sistema de notificaciones en tiempo real funcional con tecnologías accesibles y sin montar una infraestructura enorme. Por eso se eligió **React + Vite + WebSockets** y no soluciones más pesadas como Angular.

Se diferencia de otros trabajos académicos en:
1.  **Integración completa:** No se limita a la conexión aislada, sino que integra el sistema con una API *backend* y CRUD.
2.  **Modularidad:** El énfasis está en crear un componente que pueda añadirse fácilmente a otros proyectos.
3.  **Ligereza:** La elección deliberada de la API nativa de WebSockets en lugar de Socket.io.

## 2.2.4 Proyectos y trabajos similares
La mayoría de trabajos académicos se enfocan en chats, demostrando que la comunicación bidireccional es factible, pero rara vez tratan sobre componentes reutilizables. 

Existen librerías de código abierto como `react-use-websocket` o `use-socket.io` que gestionan la conexión, pero no ofrecen una interfaz visual. Por otro lado, plataformas como **Knock** o **Novu** ofrecen notificaciones como servicio (NaaS), pero son soluciones de terceros que pueden implicar costes y dependencias externas.

## 2.2.5 Por qué podría servir este TFG en Soincon
**Soincon** (Guarnizo, Cantabria) se dedica a la integración de sistemas e industria 4.0. Su plataforma **EMI Suite 4.0** es un sistema MES-MOM que monitoriza plantas productivas en tiempo real.

El problema que resuelve este TFG es crítico para ellos: actualmente, un responsable de planta suele enterarse de eventos críticos recargando la página o esperando una consulta periódica. Un componente de notificaciones basado en WebSockets permitiría:

* **Avisar al instante** de fallos en máquinas.
* **Notificar desviaciones** de calidad en el momento exacto.
* **Sincronizar dashboards** de varios usuarios sin intervención manual.

Al ser modular, su integración en EMI Suite no requeriría reescribir código existente, sino simplemente configurarlo y conectarlo al servidor.

---
**Anterior:** [2.1 Justificación](#) | **Siguiente:** [2.3 Solución Propuesta](#)
