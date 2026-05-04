# 2.5 Alcance del Trabajo

[Volver al capítulo 2](../README.md) | [Volver al índice principal](../../README.md)

---

El mundo del software para la gestión industrial está viviendo un momento de expansión. Se estima que el mercado mundial de plataformas MES (donde se incluye EMI Suite 4.0) llegará a los 41.780 millones de dólares en 2032, después de haber rondado los 14.890 millones en 2024. Eso es un crecimiento anual del 14,1%. En este contexto, las interfaces web que muestran datos de la industria en tiempo real son cada vez más importantes, y poder recibir notificaciones al instante sin tener que estar recargando la página a mano se convierte en algo básico que el sistema tiene que ofrecer.

Este trabajo de fin de grado nace justo de esa necesidad concreta. No se trata de crear una plataforma MES entera, sino de desarrollar y probar un componente específico que solucione uno de los problemas más típicos en este tipo de sistemas: que la interfaz web y el servidor se comuniquen en tiempo real.

---

## 2.5.1 Lo que sí incluye este trabajo

### Conexión WebSocket

El proyecto incluye un módulo gestor de conexión WebSocket que funciona de verdad. Este módulo se encarga de abrir y mantener el enlace entre el cliente y el servidor, estar a la escucha de los eventos que lleguen por ese canal y pasárselos al componente de notificaciones para que los procese y los pinte en pantalla.

Para ello se usa la API nativa de WebSocket que traen los navegadores modernos, sin depender de librerías externas como Socket.io. Usar el protocolo directamente hace que entendamos mejor cómo va la comunicación en tiempo real y que la solución sea más liviana.

### Integración con la API de Soincon

Para acceder a la información de EMI Suite 4.0, el sistema usa la API REST que me ha dado Soincon. Eso significa que el proyecto trabaja con datos reales de un entorno industrial. La integración cubre las operaciones de modificar y consultar documentos, y cada vez que se escribe algo se lanza el evento WebSocket correspondiente.

### Componente React de notificaciones

El corazón del proyecto es un componente de React pensado para que se pueda reutilizar. El componente se las apaña solo para gestionar la conexión WebSocket, procesar los eventos que llegan, guardar el historial de notificaciones en el estado de React y actualizar la interfaz automáticamente. Que sea reutilizable no es solo un objetivo bonito, sino algo práctico: este TFG deja en el ecosistema un componente específico para notificaciones en tiempo real con WebSocket nativo.

### Interfaz visual de notificaciones

El proyecto incluye una interfaz de usuario que funciona y muestra las notificaciones que llegan de forma clara y sencilla. Desde la interfaz se puede ver el historial de notificaciones, distinguir entre las leídas y las no leídas, y borrar notificaciones de una en una o todas de golpe.

### Chat para avisar a diferentes operarios

El proyecto también incluye un chat integrado para mandar un mensaje a distintos operarios de la empresa y avisarles de alguna incidencia. Al mensaje se le puede adjuntar una notificación que haya llegado al centro de control, para darle a la otra persona algo de contexto sobre el aviso que se ha recibido.

---

## 2.5.2 Lo que no incluye este trabajo

### Notificaciones fuera del navegador

El sistema de notificaciones solo funciona dentro del navegador web. No incluye notificaciones de escritorio del sistema operativo, ni integración con otros canales como el correo o el SMS. El foco del proyecto está en la comunicación en tiempo real en interfaces web, que es el caso de uso más directo y habitual en plataformas como EMI Suite 4.0, donde los operarios trabajan con paneles web en ordenadores de sobremesa o tablets.

### Soporte para navegadores antiguos

El proyecto asume que el usuario tiene un navegador moderno que soporte WebSocket y los módulos ES de JavaScript. No se han preparado parches para navegadores como Internet Explorer o versiones muy viejas de Chrome o Firefox. Según StatCounter de 2024, Internet Explorer tiene menos del 0.5% de cuota de mercado en todo el mundo, y los navegadores que van bien con WebSocket superan el 97%.

---

[Anterior: 2.4 Objetivos](../2.4_Objetivos/README.md) | [Siguiente: 2.6 Estructura](../2.6_Estructura/README.md)
