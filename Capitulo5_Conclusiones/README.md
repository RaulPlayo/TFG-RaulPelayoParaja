# Capítulo 5. Conclusiones, discusión de resultados, recomendaciones y futuras líneas de actuación

[Volver al índice principal](../README.md) 

## Contenido

- [5.1. Qué hemos conseguido (Cumplimiento de objetivos)](#51-qué-hemos-conseguido-cumplimiento-de-objetivos)
- [5.2. Discusión: Lo que ha funcionado y lo que se ha quedado corto](#52-discusión-lo-que-ha-funcionado-y-lo-que-se-ha-quedado-corto)
- [5.3. Recomendaciones para el futuro](#53-recomendaciones-para-el-futuro)
- [5.4. Próximos pasos y líneas de actuación](#54-próximos-pasos-y-líneas-de-actuación)
- [5.5. Cierre del trabajo](#55-cierre-del-trabajo)

Con este capítulo cerramos el documento. La idea aquí es volver a mirar la hipótesis y los objetivos que vimos en el **apartado 2.4 - Objetivos** y poner sobre la mesa lo que se ha conseguido de verdad, basándonos en el prototipo real. 

La hipótesis de la que partíamos era clara: *demostrar que usar React junto a WebSockets es una combinación sólida y eficiente para crear pantallas de monitorización en tiempo real en la industria, superando los problemas del polling tradicional*. 

Además, la estructura de: Escenario (Cap. 1) → Requisitos (Cap. 2) → Análisis y diseño (Cap. 3) → Descripción de la solución (Cap. 4) → Conclusiones (Cap. 5) ha sido realizada correctamente cómo se organizó en el **apartado 2.6 - Estructura del trabajo.**



## 5.1. Qué hemos conseguido (Cumplimiento de objetivos)

La conclusión principal es que la aplicación funciona y cumple de sobra con el objetivo central del TFG: recibe los avisos del servidor al instante y los pinta en la pantalla del usuario sin necesidad de que este tenga que recargar la página a mano. Pero además, el proyecto ha ido un paso más allá de una simple prueba técnica de concepto. Se ha construido un prototipo que incluye control de acceso, un historial para revisar eventos pasados, niveles de importancia para los avisos, un indicador visual de si la conexión está activa, guardado de preferencias del usuario y hasta un chat integrado para hablar de las incidencias. 

Así es como ha respondido el proyecto a los objetivos que hemos especificado **(apartado 2.4 - Objetivos)**:

### 5.1.1. Gestión de requisitos y diseño estructurado
Se ha logrado aterrizar una necesidad real de una planta industrial en una estructura de software limpia y modular. Toda la separación que se detalla en el **apartado 4.4 - Análisis de paquetes** (servicios, hooks propios, contextos y componentes) no se hizo por rellenar, sino para que el código sea fácil de entender, mantener y ampliar el día de mañana por cualquier otro desarrollador.

También, tanto los actores como los casos de uso han sido detallados fieles a lo que puede hacer la aplicación **(apartado 3.2 - Disciplina de requisitos).**


### 5.1.2. Desarrollo del Producto Mínimo Viable (MVP)
El prototipo es totalmente functional. La aplicación escucha el canal de WebSockets, procesa los mensajes, los clasifica según su urgencia y permite al operario interactuar con ellos. Además, haber montado un sistema para simular eventos ha sido un acierto total, ya que ha permitido probar decenas de situaciones distintas en minutos sin necesidad de estar conectados a una máquina real en la fábrica.

### 5.1.3. WebSockets frente al Polling tradicional
Al usar WebSockets nos olvidamos de estar preguntando al servidor cada pocos segundos si hay algo nuevo. Eliminamos tráfico absurdo en la red y es el servidor el que avisa a la aplicación solo cuando pasa algo. Para entornos industriales donde la información cambia de golpe y de forma impredecible, este enfoque es, sin duda, el correcto.


## 5.2. Discusión: Lo que ha funcionado y lo que se ha quedado corto

Hacer ingeniería también significa ser crítico con lo que uno programa. Aquí analizo los aciertos del desarrollo y también los puntos donde el proyecto contiene limitaciones.

### Por qué React ha encajado bien
Elegir React para este tipo de proyectos ha sido una de las mejores decisiones. La forma en que maneja la interfaz se lleva de maravilla con los flujos de datos en tiempo real. En cuanto el servicio de WebSockets caza un evento del servidor, el estado de la aplicación cambia y la pantalla se actualiza sola al milisegundo. Además, meter toda la lógica de la conexión dentro de *hooks* personalizados ayudó un montón a mantener los componentes visuales limpios y ordenados **(Apartado 4.2 - Arquitectura final del sistema)**.

### Las limitaciones reales del prototipo
Como es lógico en un proyecto de esta envergadura, el prototipo tiene puntos que necesitan mejorar antes de pensar en un entorno real:
* **La seguridad está bajo mínimos:** El sistema de login actual es una simulación local. Para producción, esto es inviable y habría que rehacerlo de cero.
* **El chat funciona "con pinzas":** Los mensajes del chat se gestionan en la memoria del navegador. Funciona genial para la demo, pero no hay una base de datos real detrás guardando esas conversaciones en el servidor.

Siendo realistas, lo que tenemos entre manos es un **prototipo funcional muy avanzado**, no un producto cerrado y listo para vender a una gran empresa.


## 5.3. Recomendaciones para el futuro

Si mañana llega otro programador, coge este repositorio y se pone a trabajar en él, mis consejos directos después de haber estado meses picando este código serían estos:

* **Sellar la seguridad:** Quitar cuanto antes el login de local y conectarlo a la API corporativa real usando tokens seguros (JWT) ya que la seguridad en planta es un tema muy serio.
* **Fijar el formato de los mensajes:** Hay que definir un contrato cerrado y estricto para los datos que viajan por WebSockets. Si el backend cambia una coma del mensaje, el frontend no debería romperse.
* **Empezar a guardar los datos:** Si la empresa necesita saber qué pasó hace tres días, no podemos dejar los avisos en la memoria del navegador. Hay que implementar una base de datos en el servidor para almacenar el histórico.


## 5.4. Próximas líneas de actuación

Gracias a que la aplicación se pensó como un puzle de piezas independientes (arquitectura modular), añadir nuevas funciones es bastante agradecido. Si el proyecto continuara, estos serían los pasos lógicos a seguir, ordenados por importancia:

### 5.4.1. Conexión real con Soincon (Prioridad: Alta)
La prioridad absoluta sería quitar todos los datos simulados y conectar el frontend con los servicios e infraestructura real de Soincon: operarios de verdad, alertas reales de las máquinas y sistemas de mensajería internos de la empresa.

### 5.4.2. El experimento pendiente con el Polling (Prioridad: Alta)
Para darle un respaldo científico incuestionable a este trabajo, lo ideal sería montar una prueba de laboratorio limpia. Consistiría en poner a funcionar a la vez este sistema de WebSockets y uno tradicional de polling bajo la misma cantidad de alertas, midiendo con datos reales cosas como:

* El retraso real en recibir el aviso (Latencia).
* Cuántos datos consume cada opción en la red.
* Cuánto sufre el procesador del ordenador del operario.

### 5.4.3. Filtros y alertas inteligentes (Prioridad: Media)
En una fábrica de verdad pueden saltar cientos de avisos pequeños a la vez. Sería muy útil añadir un sistema que agrupe las alertas para no volver loco al usuario, además de programar alertas visuales más agresivas o que avisen a un responsable superior si un operario no atiende una incidencia grave en un tiempo límite.

### 5.4.4. Notificaciones en el móvil e industrialización (Prioridad: Media)
Llevar los avisos fuera de la pantalla del ordenador: configurar alertas push en el móvil, correos automáticos o mensajes directos por Microsoft Teams. Por último, automatizar las subidas de código con herramientas de despliegue continuo (CI/CD) para que actualizar la aplicación en la fábrica sea pulsar un botón.

## 5.5. Cierre del trabajo

En resumen, lo más valioso de este proceso no es solo el código que se ha escrito, sino haber transformado una necesidad real de una empresa en un prototipo que funciona, se entiende y marca un camino clarísimo para convertirse en un producto de producción.

---

[Anterior: Capítulo 4 - Descripcion de la solución](../Capitulo4_Descripcion_Solucion/README.md) | [Presentación del trabajo](../PRESENTACION.md)