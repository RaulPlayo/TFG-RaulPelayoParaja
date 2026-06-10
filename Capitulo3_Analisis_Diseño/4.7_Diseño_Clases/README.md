# 4.7 Diseño de Clases

[Volver al capítulo 3](../README.md) | [Volver al índice principal](../../README.md)

---

## `AuthService`

**Atributos:**
- `token: string | null`
- `tokenExpiry: number | null`

**Métodos:**
- `login(credentials: LoginCredentials): Promise<AuthResponse>`
- `getToken(): string | null`
- `clearToken(): void`
- `isAuthenticated(): boolean`
- `getAuthHeader(): Record<string, string>`

---

## `WebSocketService`

**Atributos:**
- `client: Client | null`
- `subscriptions: StompSubscription[]`
- `statusHandlers: StatusHandler[]`
- `messageHandlers: MessageHandler[]`

**Métodos:**
- `connect(): void`
- `disconnect(): void`
- `onStatusChange(handler): () => void`
- `onMessage(handler): () => void`

---

## `WebSocketMessage`

**Atributos:**
- `operation: string`
- `type?: string`
- `message?: string`
- `payload?: object`
- `timestamp?: string`

---

## `NotificationItem`

**Atributos:**
- `id: string`
- `type: string`
- `title: string`
- `description: string`
- `operation: string`
- `timestamp: Date`
- `rawMessage: WebSocketMessage`
- `isRead?: boolean`

---

## `useWebSocket`

**Estado:**
- `status: ConnectionStatus`
- `notifications: NotificationItem[]`

**Métodos:**
- `removeNotification(id: string): void`
- `dismissNotification(id: string): void`
- `markAllAsRead(): void`
- `addLocalNotification(title: string, description: string, type?: string): void`
- `clearAll(): void`

---

## `ChatContext`

**Estado:**
- `isOpen: boolean`
- `attachedNotification: NotificationItem | null`
- `conversations: Record<string, ChatMessage[]>`

**Métodos:**
- `openChat(): void`
- `closeChat(): void`
- `openChatWithAttachment(notification: NotificationItem): void`
- `attachNotification(notification: NotificationItem): void`
- `removeAttachment(): void`
- `sendMessage(recipientId: string, text: string, attachment?: NotificationItem | null): void`

---

[Anterior: 4.6 Diseño de Casos de Uso](../4.6_Diseño_Casos_de_Uso/README.md) | [Siguiente: 4.8 Diseño de Paquetes](../4.8_Diseño_Paquetes/README.md) | [Presentación del trabajo](../PRESENTACION.md)
