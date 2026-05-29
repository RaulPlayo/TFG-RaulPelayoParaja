# Diagrama de despliegue

[Volver al capítulo 3](../README.md) | [Volver al índice principal](../../README.md)


Este documento describe el despliegue de la aplicacion de notificaciones desarrollada para EMI Suite. El sistema es una aplicacion web React construida con Vite que se ejecuta en el navegador del responsable y se comunica con servicios externos de EMI Suite mediante HTTPS y WebSocket seguro.

![](../../imagenes/despliegue.svg)
[Código fuente](../../codigoFuente/despliegue.puml)

## Objetivo del diagrama

El diagrama de despliegue muestra donde se ejecuta cada parte del sistema y como se comunican los nodos entre si. En este caso, la aplicacion no necesita un backend propio dentro del proyecto: el frontend se despliega como ficheros estaticos y consume servicios externos de EMI Suite.

## Nodos principales

### Equipo del Responsable

Representa el ordenador desde el que el usuario accede a la aplicacion. Dentro de este nodo se encuentra el navegador web, que ejecuta la aplicacion React ya compilada.

En el navegador se despliegan:

- `Aplicacion React SPA`: interfaz principal del sistema.
- `localStorage`: almacenamiento local donde se conserva el token de sesion utilizado por la aplicacion.

La aplicacion renderiza el dashboard, el historial de notificaciones, los avisos emergentes y el chat de incidencias.

### Servidor Web / Hosting Estatico

Representa el servidor encargado de entregar los archivos generados por el build de Vite. Al ejecutar `npm run build`, el proyecto genera la carpeta `dist`, que contiene los artefactos listos para desplegar.

Artefactos principales:

- `dist/index.html`: punto de entrada de la aplicacion.
- `dist/assets/*.js`: codigo JavaScript compilado.
- `dist/assets/*.css`: estilos compilados.
- `dist/icons.svg`, `favicon.svg`, `notifications.png`: recursos estaticos de la interfaz.

El servidor web solo sirve archivos estaticos. La logica de negocio del lado cliente se ejecuta en el navegador.

### Entorno de Desarrollo

El diagrama tambien incluye el entorno local usado durante el desarrollo:

- `npm run dev`: levanta Vite en el puerto `5173`.
- `npm run preview`: sirve la version compilada en el puerto `4173`.

Estos nodos no forman parte obligatoria del despliegue final, pero ayudan a documentar como se prueba la aplicacion antes de publicarla.

### EMI Suite

Representa el sistema externo con el que se integra la aplicacion. 

Dentro de EMI Suite aparecen dos elementos relevantes:

- Servicio de autenticacion.
- Broker STOMP/WebSocket.

El frontend usa estos servicios para autenticarse y recibir eventos en tiempo real.

### Broker STOMP WebSocket

El broker es el canal que permite recibir eventos sin recargar la pagina. La aplicacion se conecta mediante WSS y se suscribe a los topics definidos en `src/config/socket.config.ts`:

- `/topic/notices`
- `/topic/updateui`
- `/topic/outputtrigger`

Cuando EMI Suite publica un evento en alguno de estos canales, el navegador lo recibe, lo normaliza y lo transforma en una notificacion visible para el responsable.

## Comunicaciones

### Carga inicial de la aplicacion

El responsable abre la aplicacion desde el navegador. El servidor web entrega `index.html`, JavaScript, CSS y recursos estaticos. A partir de ese momento, la aplicacion funciona como una SPA.

### Autenticacion

La aplicacion realiza la autenticacion contra EMI Suite mediante HTTPS. Cuando obtiene un token valido, lo guarda en `localStorage` para reutilizarlo durante la sesion.

### Conexion WebSocket

Una vez autenticado el usuario, la aplicacion abre una conexion segura con el entorno de desarrollo de la empresa.

El token se adjunta a la conexion y el cliente STOMP se suscribe a los topics configurados. Si la conexion se interrumpe, la configuracion contempla un retardo de reconexion de `5000 ms`.

### Recepcion de eventos

Los eventos generados por EMI Suite llegan al broker y despues al navegador. El servicio WebSocket del frontend normaliza cada mensaje y `useWebSocket` lo convierte en un `NotificationItem`. Esa notificacion se muestra como aviso emergente y tambien queda disponible en el historial.

## Responsabilidades por nodo

| Nodo | Responsabilidad |
| --- | --- |
| Navegador Web | Ejecutar la SPA, mostrar la interfaz, guardar token y abrir WebSocket |
| Servidor Web / Hosting Estatico | Servir los archivos compilados de `dist` |
| Vite Dev Server | Ejecutar la aplicacion en desarrollo |
| Vite Preview | Probar la version compilada localmente |
| EMI Suite | Proporcionar autenticacion y origen de eventos |
| Broker STOMP WebSocket | Distribuir eventos en tiempo real a los clientes suscritos |

## Flujo resumido

1. El responsable accede a la aplicacion desde el navegador.
2. El servidor web entrega los archivos estaticos generados en `dist`.
3. La aplicacion verifica o solicita autenticacion.
4. El token se guarda en `localStorage`.
5. El cliente abre una conexion WSS con el broker STOMP.
6. La aplicacion se suscribe a los topics de EMI Suite.
7. Los eventos recibidos se transforman en notificaciones.
8. El responsable consulta el historial, ve notificaciones o envia mensajes de incidencia desde la interfaz.

## Consideraciones de despliegue

Para produccion, basta con:

```text
npm run dev
```

El servidor debe entregar correctamente `index.html` y los assets generados. Si se configura routing del lado cliente en el futuro, sera necesario redirigir las rutas no encontradas hacia `index.html`.

La aplicacion requiere acceso de red a su pagina de desarrollo y a su enlace desde mandan los WebSockets.

Tambien debe permitirse la conexion WebSocket segura desde el navegador del responsable hacia el broker externo.

 [Anterior : 4.8 Diseño de Paquetes](../4.8_Diseño_Paquetes/README.md)
| [Siguiente: Capítulo 4 - Descripcion de la solución](../../Capitulo4_Descripcion_Solucion/README.md)