# Capitulo 2 - Marco Teorico

[Volver al indice principal](../README.md)

---

El desarrollo de aplicaciones web ha evolucionado desde sitios estaticos hacia plataformas dinamicas donde la inmediatez es clave. Este capitulo explica las tecnologias empleadas para lograrlo.

## Contenidos del capitulo

- [2.1 Justificacion](./2.1_Justificacion/README.md)
- [2.2 Estado del Arte](./2.2_Estado_del_Arte/README.md)
- [2.3 Solucion Propuesta](./2.3_Solucion_Propuesta/README.md)
- [2.4 Objetivos General y Especificos](./2.4_Objetivos/README.md)
- [2.5 Alcance del Trabajo](./2.5_Alcance/README.md)
- [2.6 Estructura del Trabajo](./2.6_Estructura/README.md)

---

## Conceptos fundamentales

### Comunicación en tiempo real

Se entiende por comunicación en tiempo real aquel modelo en el que el servidor puede enviar datos al cliente en el instante en que se producen, sin esperar una solicitud previa por parte de este. Este paradigma ha ganado protagonismo a medida que los usuarios esperan que las aplicaciones web se comporten de forma similar a las aplicaciones nativas de escritorio o movil: de manera inmediata y sin necesidad de una interaccion manual para ver los cambios.

En el contexto de este proyecto, la comunicación en tiempo real es el eje central del sistema, ya que el objetivo es que cualquier modificacion producida en el servidor se refleje automaticamente en la interfaz del usuario sin que este tenga que realizar ninguna acción adicional.

---

### El protocolo HTTP

HTTP es el protocolo de transferencia de hipertexto sobre el que se construye la web. Fue definido por Tim Berners-Lee en 1989 y ha sido revisado en varias ocasiones desde entonces, siendo HTTP/1.1 (1997), HTTP/2 (2015) y HTTP/3 (2022) sus versiones mas relevantes.

Sigue un modelo de peticion-respuesta: el cliente (el navegador) envia una solicitud al servidor, el servidor la procesa y devuelve una respuesta, y la conexion se cierra. Este modelo es perfectamente valido para cargar paginas o consultar datos de forma puntual, pero presenta una limitacion clara cuando se necesita que el servidor informe al cliente de algo de forma proactiva: HTTP no lo permite.

Para intentar solucionar esto surgieron tecnicas como el **polling**, en la que el cliente realiza peticiones al servidor de forma periodica para comprobar si hay novedades, o el **long polling**, donde la conexion se mantiene abierta hasta que el servidor tiene algo que responder. Ambas tecnicas son poco eficientes: el polling genera trafico innecesario aunque no haya datos nuevos, y el long polling crea mucha latencia.

---

### WebSocket

WebSocket es un protocolo de comunicacion full-duplex (método de transmisión de datos en el que dos dispositivos pueden enviar y recibir informacion de forma simultanea y bidireccional) sobre una unica conexión TCP, estandarizado por la IETF en 2011 y definido como API en HTML5. Fue diseñado especificamente para superar las limitaciones de HTTP en escenarios de comunicacion en tiempo real, y hoy esta soportado de forma nativa por todos los navegadores modernos.

La principal caracteristica de WebSocket es que, una vez establecida la conexion, tanto el cliente como el servidor pueden enviarse mensajes en cualquier momento y en cualquier dirección, sin necesidad de que el otro extremo haya enviado una solicitud previa. La conexión permanece abierta mientras ambas partes lo deseen, lo que elimina la sobrecarga de establecer y cerrar conexiones repetidamente.

El proceso de establecimiento comienza con un **handshake HTTP**. El cliente envia una peticion HTTP especial con una cabecera `Upgrade: websocket`. Si el servidor acepta, responde con un codigo 101 "Switching Protocols" y a partir de ese momento la conexion pasa a ser WebSocket. Una vez establecida, los datos se transmiten en forma de **frames**: la cabecera de cada frame es de solo 2 bytes en el caso mas sencillo, frente a los cientos de bytes que puede ocupar una cabecera HTTP.

Estudios comparativos han demostrado reducciones de latencia de hasta un orden de magnitud respecto a las soluciones basadas en polling, además de una reducción drástica en el consumo de ancho de banda y en la carga del servidor.

---

### React

React es una biblioteca de JavaScript de codigo abierto desarrollada y mantenida por Meta (anteriormente Facebook). Fue publicada en 2013 y se ha convertido en la libreria frontend mas utilizada del mundo.

El concepto central de React es el **componente**: una unidad de interfaz de usuario autonoma y reutilizable que encapsula su propia logica, su propio estado y su propia representacion visual. Cuando el estado de un componente cambia, React se encarga automaticamente de actualizar la parte de la interfaz afectada de forma eficiente gracias al **Virtual DOM**.

Para este proyecto, React es la pieza que permite que la interfaz reaccione de forma inmediata a los eventos recibidos a traves de WebSocket. Los hooks mas relevantes son `useState`, que permite declarar y actualizar el estado de un componente, y `useEffect`, que permite ejecutar efectos secundarios como establecer una conexion WebSocket cuando el componente se monta y limpiarla cuando se desmonta.

---

### Vite

Vite es una herramienta de construcción y desarrollo para aplicaciones web modernas creada por Evan You. Su principal ventaja frente a soluciones anteriores como Webpack es la velocidad: utiliza modulos nativos del navegador durante el desarrollo, procesando solo lo estrictamente necesario en cada cambio. Esto se traduce en tiempos de arranque casi instantaneos.

Vite implementa ademas **Hot Module Replacement (HMR)**: actualiza los modulos modificados en el navegador sin necesidad de recargar la pagina completa, manteniendo el estado del resto de la aplicacion intacto. Para la fase de produccion, Vite utiliza Rollup internamente para generar un paquete optimizado.

---

### Node.js y backend

Aunque el foco principal de este proyecto es el frontend, el sistema requiere tambien de un servidor backend capaz de gestionar conexiones WebSocket y exponer una API REST. Para este proposito se utiliza Node.js, un entorno de ejecucion de JavaScript en el lado del servidor basado en el motor V8 de Chrome. Su modelo de concurrencia basado en un unico hilo y un bucle de eventos no bloqueante le permite gestionar miles de conexiones simultaneas con un consumo de recursos relativamente bajo.

Junto a Node.js se utiliza **Express**, un framework minimalista para la creacion de servidores HTTP, que simplifica la definición de rutas y la gestion de peticiones HTTP para la API REST del sistema.

---

[Anterior: Capitulo 1](../Capitulo1_Introduccion/README.md) | [Siguiente: 2.1 Justificacion](./2.1_Justificacion/README.md)
