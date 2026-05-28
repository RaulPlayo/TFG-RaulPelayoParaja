# Capítulo 5. Conclusiones, discusión de resultados, recomendaciones y futuras líneas de actuación

[Volver al índice principal](../README.md) 

## 5.1 Conclusiones

El desarrollo realizado permite concluir que el uso conjunto de React y WebSockets constituye una base adecuada para construir interfaces web de monitorización en tiempo real dentro de un contexto industrial. La solución obtenida cumple el objetivo fundamental del TFG: recibir eventos generados por el servidor y reflejarlos en la interfaz del usuario sin recarga manual, de manera inmediata y comprensible.

Asimismo, el trabajo no se ha limitado a una prueba técnica mínima, sino que ha derivado en un prototipo con valor funcional real. La aplicación integra autenticación de acceso, historial de eventos, categorización de avisos, indicador de conexión, persistencia de preferencias visuales y un canal de chat contextual. Esto demuestra que la incorporación de tiempo real no tiene por qué quedar aislada como una característica técnica, sino que puede estructurar una experiencia de usuario completa alrededor de la gestión de incidencias.

## 5.2 Discusión de resultados

Desde la perspectiva de los objetivos definidos al inicio del trabajo, los resultados son positivos.

En relación con la disciplina de requisitos y diseño, se ha conseguido traducir una necesidad empresarial concreta en una arquitectura modular clara. La separación entre servicios, hooks, contextos y componentes facilita el mantenimiento y deja una base razonable para ampliaciones futuras.

Respecto al objetivo de construir un producto mínimo viable, el resultado puede considerarse satisfactorio. La aplicación recibe mensajes, los interpreta, los muestra de forma visual y permite al usuario actuar sobre ellos. Además, el uso de eventos simulados ha hecho posible validar con rapidez numerosos escenarios.

En cuanto al objetivo comparativo frente al polling, aunque en el estado actual del proyecto no se ha incorporado una batería experimental extensa con métricas automatizadas, sí se constata una mejora conceptual y operativa clara. El modelo WebSocket evita consultas periódicas innecesarias, reduce tráfico redundante y desplaza la lógica desde la pregunta continua del cliente hacia la notificación directa por parte del servidor. En sistemas donde la información cambia de forma irregular pero crítica, este enfoque resulta especialmente adecuado.

No obstante, los resultados también dejan ver algunas limitaciones. La autenticación actual es local y simplificada; el chat todavía no está conectado a una infraestructura real de mensajería; y el análisis estático del código evidencia aspectos de calidad interna pendientes de refactorización. Esto no invalida la solución, pero sí sitúa correctamente su grado de madurez: se trata de un prototipo funcional avanzado, no de un producto corporativo totalmente cerrado.

## 5.3 Recomendaciones

De cara a una evolución real del sistema, se recomienda:

1. Sustituir la autenticación simulada por un flujo real contra la API corporativa, con gestión segura de tokens, expiración y renovación de sesión.
2. Formalizar el contrato de mensajes WebSocket con un esquema estable compartido entre backend y frontend, reduciendo la necesidad de normalización ad hoc en cliente.
3. Reforzar la calidad interna del código eliminando usos de `any`, corrigiendo advertencias de lint y endureciendo el tipado de payloads.
4. Incorporar pruebas automáticas unitarias e integradas sobre servicios, hooks y componentes críticos.
5. Persistir el historial de notificaciones en backend o almacenamiento duradero cuando el caso de uso requiera trazabilidad más allá de la sesión local.
6. Evaluar la incorporación de observabilidad más completa, con métricas de reconexión, errores y latencia real de extremo a extremo.

## 5.4 Futuras líneas de actuación

Las líneas de evolución más naturales del trabajo son las siguientes.

### 5.4.1 Integración corporativa completa

La primera línea de actuación consiste en sustituir las piezas simuladas por integración real con los servicios corporativos de Soincon. Esto incluye autenticación contra backend, recuperación de operarios desde API y mensajería de incidencias conectada a servicios internos o canales empresariales.

### 5.4.2 Persistencia y trazabilidad

Actualmente el historial de notificaciones se mantiene en memoria durante la sesión. Una ampliación lógica sería almacenar los eventos en una base de datos o servicio de auditoría, permitiendo búsquedas, filtros, exportación y trazabilidad histórica para análisis operativos.

### 5.4.3 Comparativa experimental con polling

Sería recomendable diseñar una evaluación formal que compare WebSockets y polling bajo una misma carga de eventos, midiendo latencia, consumo de red, uso de CPU y experiencia percibida por el usuario. Esta línea reforzaría empíricamente una hipótesis que en el presente trabajo ha quedado demostrada sobre todo desde el plano funcional y arquitectónico.

### 5.4.4 Gestión avanzada de alertas

Otra evolución interesante sería incorporar reglas de prioridad, agrupación de eventos, filtrado por criticidad, confirmación explícita de incidencias y escalado automático a distintos perfiles cuando una alerta no haya sido atendida en un tiempo determinado.

### 5.4.5 Notificaciones multicanal

Aunque el alcance del TFG se ha centrado en el navegador, en un contexto industrial podría resultar muy útil extender el sistema hacia notificaciones push, correo electrónico, mensajería móvil o integración con herramientas corporativas como Microsoft Teams o similares.

### 5.4.6 Preparación para producción

Finalmente, una línea imprescindible para consolidar el trabajo sería la industrialización del prototipo: revisión de seguridad, pruebas de carga, endurecimiento del proceso de build, despliegue continuo, control de errores y monitorización operativa.

## 5.5 Cierre final

En conjunto, el trabajo demuestra que es viable construir un sistema modular de notificaciones en tiempo real para entornos industriales utilizando tecnologías web actuales. La solución desarrollada no solo valida la hipótesis de partida, sino que deja una base práctica y extensible sobre la que seguir construyendo. El principal valor del proyecto radica en haber transformado una necesidad real de comunicación inmediata en un prototipo funcional con aplicación directa, mostrando además un camino claro de evolución hacia escenarios de uso más completos y próximos a producción.

[Anterior: Capítulo 4 - Descripcion de la solución](../Capitulo4_Descripcion_Solucion/README.md)