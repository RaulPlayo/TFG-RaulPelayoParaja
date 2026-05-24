# 4.8 Diseño de Paquetes

[Volver al capítulo 3](../README.md) | [Volver al índice principal](../../README.md)

---

La estructura de mi proyecto se divide en 2 carpetas nuevas (`src` y `scripts`), además de los archivos que están tanto en la raíz del proyecto como en la propia raíz de `src`. Las carpetas y sus respectivos módulos son:

| Paquete | Módulos incluidos |
|---|---|
| `src/config/` | `api.config.ts`, `socket.config.ts` |
| `src/types/` | `socket.types.ts` |
| `src/context/` | `ChatContext.tsx`, `ThemeContext.tsx` |
| `src/hooks/` | `useWebSocket.ts`, `useAuth.ts` |
| `src/services/` | `websocket.service.ts`, `auth.service.ts` |
| `src/components/Auth/` | `LoginForm.tsx` |
| `src/components/Dashboard/` | `Dashboard.tsx`, `index.ts` |
| `src/components/Chat/` | `ChatPanel.tsx` |
| `src/components/Notifications/` | `NotificationsContainer.tsx`, `NotificationItem.tsx` |
| `src/sound/` | `notificacion.mp3`, `warning.mp3` |
| `src/images/` | `notifications.png` |
| `src/` | `App.tsx`, `custom.d.ts`, `index.css` y `main.tsx` |
| `scripts/` | `dev-mobile.mjs` |
| `dist/` | Salida del build (Vite) |
| **Raíz del proyecto** | `index.html`, `package-lock.json`, `package.json`, `postcss.config.js`, `README.md`, `tailwind.config.js`, `tsconfig.json`, `tsconfig.app.json`, `tsconfig.node.json`, `tsconfig.node.tsbuildinfo`, `tsconfig.tsbuildinfo`, `vite.config.d.ts`, `vite.config.js` |

---

[Anterior: 4.7 Diseño de Clases](../4.7_Diseño_Clases/README.md) | [Siguiente: 4.9_Diagrama_Despliegue](../4.9_Diagrama_Despliegue/README.md)
 
