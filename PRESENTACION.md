# Diseño y desarrollo de un sistema modular de notificaciones mediante React y WebSockets

### Raúl Pelayo Paraja — Trabajo de Fin de Grado

---

## Índice de la presentación
1. [Introducción, el problema y su solución](#1-introducción-y-motivación)
2. [Objetivos](#2-objetivos)
3. [Modelo del dominio](#3-modelo-del-dominio)
4. [Requisitos , casos de uso y diagrama de contexto](#4-requisitos-y-casos-de-uso)
5. [Diagramas de secuencia](#14-diseño-de-casos-de-uso-secuencia)
6. [Diagrama MVC]()
7. [Prototipos de interfaz](#7-prototipos-de-interfaz)
8. [Análisis y diseño de la arquitectura](#13-diseño-de-la-arquitectura)
9. [Descripción de la solución](#16-demostración-de-la-solución)
10. [Conclusiones y líneas futuras](#17-conclusiones-y-líneas futuras)



## 1. Introducción 

> - El TFG nace de una necesidad real durante las prácticas en Soincon.
> - Soincon tiene un producto llamado **EMI Suite 4.0** para la gestión industrial.


## El problema

> - Los operarios tenían que recargar la página para ver si había novedades → pérdida de tiempo y de información crítica.
> - Objetivo: construir un sistema de notificaciones en **tiempo real** usando **React** y **WebSockets**, eliminando la recarga manual.



## Solución propuesta

> - Single Page Aplication
> - Arquitectura **cliente-servidor con doble canal**: REST (autenticación, consultas) + WebSocket (eventos en tiempo real).
> - 4 módulos principales: Gestor de conexión WS, Integración API Soincon, Componente de notificaciones React, Interfaz visual.
> - Flujo: cliente se conecta → servidor detecta cambio en EMI Suite → emite evento por WebSocket → React actualiza la pantalla automáticamente.
---

## 2. Objetivos

> - **Hipótesis**: WebSockets + React es más rápido y eficiente que polling para monitorización industrial.
> - **Objetivo**: crear un sistema de notificaciones en tiempo real, bidireccional, modular, con una buena experiencia para el usuario (UX).


---

## 3. Modelo del dominio

[Modelo del dominio](./Capitulo2_Requerimientos/3.1_Modelo_del_Dominio/README.md)

---

## 4. Requisitos , casos de uso y diagrama de contexto

[Requisitos y casos de uso](./Capitulo2_Requerimientos/3.2_Disciplina_de_Requisitos/README.md)

---

## 5. Diagramas de secuencia

[Diagramas de secuencia](./Capitulo3_Analisis_Diseño/4.6_Diseño_Casos_De_Uso/README.md)

---

## 6. Diagrama Modelo Vista Controlador

[Modelo Vista Controlador (MVC)](./Capitulo3_Analisis_Diseño/4.3_Analisis_Clases/README.md)

---

## 11. Análisis de clases

> **De qué hablar:**
> - Clases conceptuales, aún no son componentes técnicos.
> - **Modelo**: Documento, Evento, Notificación, HistorialNotificaciones, ConexiónWebSocket.
> - **Vista**: Login, Panel, Historial, Notificación, Chat, Documento, Evento.
> - **Controlador**: Autenticación, RecepciónEventos, Historial, Lectura, Eliminación, Chat, Sincronización.

![Diagrama de clases (análisis)](./imagenes/diagramaClases.svg)

---

## 12. Análisis de paquetes

> **De qué hablar:**
> - Organización del sistema en paquetes funcionales.
> - **Presentación**: vistas y componentes (autenticación, panel, historial, chat).
> - **Control de aplicación**: hooks y contextos (`useWebSocket`, `useAuth`, `ChatContext`, `ThemeContext`).
> - **Servicios**: `auth.service` y `websocket.service` (STOMP/WebSocket).
> - **Configuración**: endpoints, broker, canales.
> - **Modelo y tipos**: `WebSocketMessage`, `NotificationItem`, `ConnectionStatus`, `ChatMessage`.
> - **Sistema externo**: EMI Suite + Broker STOMP.

![Diagrama de paquetes](./imagenes/diagramaPaquetes.png)

---

## 13. Diseño de la arquitectura

> **De qué hablar:**
> - La arquitectura de análisis se concreta con tecnologías reales.
> - **SPA**: React 19 + TypeScript + Vite.
> - **Tiempo real**: WebSocket nativo + STOMP (`@stomp/stompjs`).
> - **Estado**: hooks personalizados + contextos React + componentes funcionales.
> - **Demo móvil**: Node.js para scripts de arranque en red local.
> - Canal REST reservado para autenticación. Canal WS dedicado a eventos. Navegador como contenedor de estado local.

![Arquitectura de diseño](./imagenes/arquitectura.svg)

---

## 14. Diseño de casos de uso (secuencia)

> **De qué hablar:**
> - Diagramas de **secuencia**: flujo temporal paso a paso.
> - Ya no son clases conceptuales, son componentes reales del sistema.

### consultarHistorial()

> El responsable abre el historial → la vista pide el listado → se ordena → se muestra.

![Secuencia — Consultar historial](./imagenes/secuenciaHistorial.svg)

### enviarMensajeDeIncidencia()

> El responsable adjunta una notificación → abre chat → escribe mensaje → se crea `ChatMessage` → se entrega al destinatario.

![Secuencia — Enviar incidencia](./imagenes/secuenciaIncidencia.svg)

### verNotificacion()

> El responsable selecciona notificación → se busca en el historial → se marca como leída → se muestra el detalle.

![Secuencia — Ver notificación](./imagenes/secuenciaNotificacion.svg)

---

## 15. Diagrama de despliegue

> **De qué hablar:**
> - **Equipo del responsable**: navegador ejecuta la SPA + localStorage (token).
> - **Servidor web**: sirve `dist/` (archivos estáticos de Vite: HTML, JS, CSS).
> - **EMI Suite**: servicio de autenticación + Broker STOMP/WebSocket.
> - Topics: `/topic/notices`, `/topic/updateui`, `/topic/outputtrigger`.
> - Comunicaciones: carga inicial (HTTPS) → autenticación (HTTPS) → conexión WSS → recepción de eventos.
> - Reconexión automática cada 5000ms si se pierde la conexión.

![Diagrama de despliegue](./imagenes/despliegue.svg)

---


---

## 17. Conclusiones y líneas futuras

> **De qué hablar:**
> - ✅ **Funciona**: recibe eventos al instante y los pinta sin recargar. Va más allá de una prueba de concepto.
> - ✅ **Objetivos cumplidos**: requisitos, análisis y diseño, MVP funcional, documentación reutilizable.
> - ✅ **React encaja perfecto**: cambio de estado → re-render automático. Hooks personalizados mantienen los componentes limpios.
> - ✅ **WebSockets vs Polling**: eliminamos tráfico innecesario, el servidor avisa solo cuando pasa algo.

> **Limitaciones honestas:**
> - Seguridad bajo mínimos (login simulado, no JWT real).
> - Chat en memoria del navegador, sin persistencia en servidor.
> - Es un **prototipo funcional avanzado**, no un producto de producción cerrado.

> **Líneas futuras (por prioridad):**
> 1. 🔴 Conexión real con Soincon (quitar datos simulados).
> 2. 🔴 Experimento formal polling vs WebSocket (latencia, ancho de banda, CPU).
> 3. 🟡 Filtros y alertas inteligentes (agrupación, escalado a supervisores).
> 4. 🟡 Notificaciones push móvil, integración Teams/email, CI/CD.

> **Cierre:**
> - Lo más valioso no es solo el código, sino haber transformado una **necesidad real** de una empresa en un prototipo que funciona, se entiende y marca un camino claro para producción.

---