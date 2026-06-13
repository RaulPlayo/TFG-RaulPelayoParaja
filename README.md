# Diseño y desarrollo de un sistema modular de notificaciones mediante React y WebSockets

---

## Resumen
 
Este TFG consiste en la creación de un sistema web que permite la actualización en tiempo real de documentos almacenados en base de datos, evitando la recarga manual de la página por parte del usuario.
 
Para ello, se utiliza una API de la empresa Soincon que gestiona las operaciones de crear, modificar, eliminar y consultar documentos (CRUD). Cuando se produce una modificación en los datos, el servidor emite un evento que desencadena una notificación en la aplicación cliente. Estos eventos se transmiten mediante una conexión WebSocket, lo que permite una comunicación bidireccional e instantánea entre el servidor y el navegador.
 
El proyecto abarca el diseño de la arquitectura, el backend (en este caso propiedad de Soincon) y el frontend, además de pruebas para medir el rendimiento y facilidad de uso, comparando el comportamiento en tiempo real frente a un sistema tradicional basado en polling.
 
 
---
 
## Estructura del repositorio
 
```
/
├── README.md                          <- Este archivo
├── imagenes/                          <- Diagramas en PlantUML e imágenes
├── codigoFuente/                      <- Código fuente de los diagramas
│
├── Capitulo1_Introduccion/
│   └── README.md
│
├── Capitulo1_MarcoTeorico/
│   ├── README.md
│   ├── 2.1_Justificacion/
│   ├── 2.2_Estado_del_Arte/
│   ├── 2.3_Solucion_Propuesta/
│   ├── 2.4_Objetivos/
│   ├── 2.5_Alcance/
│   └── 2.6_Estructura/
│
├── Capitulo2_Requerimientos/
│   ├── README.md
│   ├── 3.1_Modelo_del_Dominio/
│   └── 3.2_Disciplina_de_Requisitos/
│
├── Capitulo3_Analisis_Diseño/
│   ├── README.md
│   ├── 4.1_Analisis_Arquitectura/
│   ├── 4.2_Analisis_Casos_de_Uso/
│   ├── 4.3_Analisis_Clases/
│   ├── 4.4_Analisis_Paquetes/
│   ├── 4.5_Diseño_Arquitectura/
│   ├── 4.6_Diseño_Casos_de_Uso/
│   ├── 4.7_Diseño_Clases/
│   ├── 4.8_Diseño_Paquetes/
│   └── 4.9_Diagrama_Despliegue/
│
├── Capitulo4_Descripcion_Solucion/
│   └── README.md
│
└── Capitulo5_Conclusiones/
    └── README.md
```
 
---

# Presentación

# Diseño y desarrollo de un sistema modular de notificaciones mediante React y WebSockets

### Raúl Pelayo Paraja — Trabajo de Fin de Grado

---

## Índice
1. [Introducción, el problema y su solución](#1-introducción)
2. [Objetivos](#2-objetivos)
3. [Modelo del dominio](#3-modelo-del-dominio)
4. [Requisitos , casos de uso y diagrama de contexto](#4-requisitos-,-casos-de-uso-y-diagrama-de-contexto)
5. [Diagramas de colaboración](#5-diagramas-de-colaboración)
6. [Diagrama MVC](#6-diagrama-modelo-vista-controlador)
7. [Diagramas de secuencia](#7-diagramas-de-secuencia)
8. [Diagrama de paquetes](#8-diagrama-de-paquetes)
9. [Diseño de la arquitectura](#9-diseño-de-la-arquitectura)
10. [Diagrama de despliegue](#10-diagrama-de-despliegue)
11. [Conclusiones y líneas futuras](#11-Conclusiones-y-líneas-futuras)



## 1. Introducción 

> - El TFG nace de una necesidad real durante las prácticas en Soincon.
> - Soincon tiene un producto llamado **EMI Suite 4.0** para la gestión industrial (MES - MOM).


## El problema

> - Los operarios tenían que recargar la página para ver si había novedades → pérdida de tiempo y de información crítica.

## Solución propuesta

> - Single Page Aplication
> - Arquitectura **cliente-servidor con doble canal**: REST (autenticación, consultas) + WebSocket (eventos en tiempo real).
> - 4 módulos principales: Gestor de conexión WS, integración API Soincon, componente de notificaciones React y una interfaz visual.

## 2. Objetivos

> - **Hipótesis**: WebSockets + React es más rápido y eficiente que polling para monitorización industrial.
> - **Objetivo**: crear un sistema de notificaciones en tiempo real, bidireccional, modular, con una buena experiencia para el usuario (UX).


## 3. Modelo del dominio

![Modelo del dominio](imagenes/modeloDominio.svg)
[Código fuente](/codigoFuente/modeloDominio.puml)
> - 3 partes: el chat y el sistema por parte del cliente + la gestión de planta que es parte de Soincon (aunque sin ella no podríamos entender este proyecto).
> - Flujo: en gestión de planta se actualiza el CRUD → se genera evento → aparece como notificación en el Sistema → podemos consultar historial o adjuntar al chat.

 ---

![Diagrama de objetos](/imagenes/conexionWebsocket.svg)
[Código fuente](/codigoFuente/conexionWebsocket.puml)


![Diagrama de objetos](/imagenes/cicloNotificacion.svg)
[Código fuente](/codigoFuente/cicloNotificacion.puml)

## 4. Requisitos , casos de uso y diagrama de contexto

> - Dos actores: Responsable y tiempo
> - "Tiempo" es un actor abstracto, representa el momento en el que la API de Soincon genera y envía un evento hacia la aplicación tras producirse una modificación en EmiSuite.
 * Operario : persona encargada de registrar o modificar eventos operativos en el sistema externo de producción, provocando la emisión de notificaciones. Al no interactuar directamente con este trabajo → no es actor.

![Diagrama de casos de uso](/imagenes/casosDeUso.svg)
[Código fuente](/codigoFuente/casosDeUso.puml)

![Consultar el historial](/imagenes/consultarHistorial.svg)
[Código fuente](/codigoFuente/consultarHistorial.puml)

![Ver notificación](/imagenes/verNotificacion.svg)
[Código fuente](/codigoFuente/verNotificacion.puml)

![Contexto](/imagenes/diagramaContextoSimple.svg)
[Código fuente](/codigoFuente/diagramaDeContextoSimple.puml)

## 5. Diagramas de colaboración

![](/imagenes/colabHistorial.svg)
[Código fuente](/codigoFuente/colabHistorial.puml)

![](/imagenes/colabLeidaVERTICAL.svg)
[Código fuente](/codigoFuente/colabLeida.puml)



## 6. Diagrama Modelo Vista Controlador
>- El sistema tiene tres capas lógicas: las Vistas para la interfaz de usuario, los Controladores que gestionan la lógica de interacción, y el Modelo que encapsula los datos, eventos y conexiones en tiempo real

![Diagrama de clases (análisis)](./imagenes/diagramaClases.svg)


## 7. Diagramas de secuencia

> - Diagramas de **secuencia**: flujo temporal paso a paso.
> - Ya no son clases conceptuales, son componentes reales del sistema.

### consultarHistorial()

> El responsable abre el historial → la vista pide el listado → se ordena → se muestra.

![Secuencia — Consultar historial](./imagenes/secuenciaHistorial.svg)

### enviarMensajeDeIncidencia()

> El responsable adjunta una notificación → abre chat → escribe mensaje → se crea `ChatMessage` → se entrega al destinatario.

![Secuencia — Enviar incidencia](./imagenes/secuenciaIncidencia.svg)


## 8. Diagrama de paquetes

> - Organización del sistema en paquetes funcionales.
> - **Presentación**: vistas y componentes (autenticación, panel, historial, chat).
> - **Control de aplicación**: hooks y contextos (`useWebSocket`, `useAuth`, `ChatContext`, `ThemeContext`).
> - **Servicios**: `auth.service` y `websocket.service` (STOMP/WebSocket).
> - **Configuración**: endpoints, broker, canales.
> - **Modelo y tipos**: `WebSocketMessage`, `NotificationItem`, `ConnectionStatus`, `ChatMessage`.
> - **Sistema externo**: EMI Suite + Broker STOMP.

![Diagrama de paquetes](./imagenes/diagramaPaquetes.png)


## 9. Diseño de la arquitectura

> - La arquitectura de análisis se concreta con tecnologías reales.
> - **SPA**: React 19 + TypeScript + Vite.
> - **Tiempo real**: WebSocket nativo + STOMP (`@stomp/stompjs`).
> - **Estado**: hooks personalizados + contextos React + componentes funcionales.
> - Canal REST reservado para autenticación. Canal WS dedicado a eventos. Navegador como contenedor de estado local.

![Arquitectura de diseño](./imagenes/arquitectura.svg)


## 10. Diagrama de despliegue

> - **Equipo del responsable**: navegador ejecuta la SPA + localStorage (token).
> - **Servidor web**: sirve `dist/` (archivos estáticos de Vite: HTML, JS, CSS).
> - **EMI Suite**: servicio de autenticación + Broker STOMP/WebSocket.
> - Topics: `/topic/notices`, `/topic/updateui`, `/topic/outputtrigger`.
> - Comunicaciones: carga inicial (HTTPS) → autenticación (HTTPS) → conexión WSS → recepción de eventos.
> - Reconexión automática cada 5000ms si se pierde la conexión.

![Diagrama de despliegue](./imagenes/despliegue.svg)

## 11. Conclusiones y líneas futuras

> - ✅ **Funciona**: recibe eventos al instante y los pinta sin recargar. Va más allá de una prueba de concepto.
> - ✅ **Objetivos cumplidos**: requisitos, análisis y diseño, MVP funcional, documentación reutilizable.
> - ✅ **React encaja perfecto**: cambio de estado → re-render automático. Hooks personalizados mantienen los componentes limpios.
> - ✅ **WebSockets vs Polling**: eliminamos tráfico innecesario, el servidor avisa solo cuando pasa algo.

> **Limitaciones :**
> - Seguridad bajo mínimos (login simulado, no JWT real).
> - Chat en memoria del navegador, sin persistencia en servidor.
> - Es un **prototipo funcional avanzado**, no un producto de producción cerrado.

> **Líneas futuras (por prioridad):**
> 1. 🔴 Conexión real con Soincon (quitar datos simulados).
> 2. 🔴 Experimento formal polling vs WebSocket (latencia, ancho de banda, CPU).
> 3. 🟡 Filtros y alertas inteligentes (agrupación, escalado a supervisores).
> 4. 🟡 Notificaciones push móvil, integración Microsoft Teams/email.
> 5. 🟡 Posibilidad de enviar documentos PDF a través de WebSocket.


> **Como conclusión:**
> - Lo más valioso no es solo el código, sino haber transformado una **necesidad real** de una empresa en un prototipo que funciona, se entiende y marca un camino claro para producción.




