# Capitulo 1 - Introduccion

[Volver al indice principal](../README.md)

---

Hoy en dia, nuestra forma de interactuar con la web ha cambiado radicalmente: ya no tenemos paciencia para esperar. Si estamos usando una aplicación de mensajeria o trabajando en equipo sobre un documento, esperamos que las cosas pasen al instante. La idea de tener que pulsar un botón en el que pone "actualizar" para ver si nos ha llegado un aviso se siente totalmente anticuada. Por eso, la comunicación en tiempo real se ha vuelto un pilar fundamental en el desarrollo moderno.

Durante años, el modelo de la web fue sencillo y unidireccional: el usuario pedia algo, el servidor lo entregaba y la conversacion terminaba ahi. Este método fue suficiente para los primeros sitios web, que no eran más que documentos estáticos enlazados entre sí. Sin embargo, a medida que las aplicaciones web fueron ganando complejidad, este modelo empezó a mostrar sus limitaciones. Hoy, plataformas como Google Docs permiten que varios usuarios editen el mismo documento simultaneamente y vean los cambios de los demás en tiempo real. Aplicaciones como Slack o Discord entregan mensajes rápidamente. Los paneles de monitorizacion de sistemas actualizan métricas cada segundo sin que el operador tenga que hacer nada. Todo esto es posible gracias a una evolución profunda en la forma en que cliente y servidor se comunican.

Este trabajo de fin de grado nace precisamente de esa necesidad de inmediatez. El objetivo es diseñar y construir un sistema de notificaciones en tiempo real utilizando las herramientas que hoy lideran el sector: React y Vite. Para ello se implementa el protocolo de WebSockets, que permite mantener una conexion abierta y fluida en todo momento con el servidor.

El desarrollo se ha estructurado de forma modular para cubrir los siguientes puntos clave:

**Gestion de conexion:** establecimiento de un enlace con el servidor mediante WebSockets.

**Procesamiento de eventos:** implementacion de una logica capaz de "escuchar" y reaccionar a los datos emitidos por el servidor en el momento exacto.

**Interfaz dinamica:** creación de componentes visuales que gestionen el estado de las notificaciones de manera fluida para el usuario.

---

## Por qué es importante

Mas allá de lo técnico, este trabajo tiene una relevancia practica directa. Para un desarrollador, entender como funcionan las arquitecturas orientadas a eventos es un gran salto a nivel profesional. Este trabajo aporta valor al validar una metodologia de desarrollo incremental para la integracion de procesos en tiempo real. Ademas, el énfasis en la creación de componentes reutilizables responde a la necesidad de la industria de generar software escalable y mantenible.

Segun el informe State of JavaScript 2023, React sigue siendo la libreria frontend mas utilizada por los desarrolladores, con mas de un 80% de adopción entre los encuestados. Este dato refleja que las tecnologias elegidas en este proyecto son un acierto.

---

[Siguiente: Capitulo 2 - Marco Teorico](../Capitulo2_MarcoTeorico/README.md)
