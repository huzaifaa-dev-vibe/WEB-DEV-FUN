# WebSockets

> Real-time, bidirectional communication over a single TCP connection.

---

## Purpose

Master WebSockets for real-time apps: chat, collaboration, live dashboards, notifications.

## Prerequisites

- [JavaScript/](../JavaScript/), [Backend/](../Backend/).

## Learning Outcome

You can build a real-time WebSocket server and client, scale it, and handle edge cases.

## Dependencies

- WebSocket server library.

## Related Files

- [Backend/](../Backend/) · [NodeJS/](../NodeJS/) · [WebSockets/scaling.md](scaling.md) · [WebSockets/rooms.md](rooms.md)

## AI Instructions

When using WebSockets:
1. **Use a library** (`ws`, Socket.IO, or framework-specific).
2. **Authenticate** the connection (token in query or header).
3. **Heartbeat** (ping/pong) to detect dead connections.
4. **Reconnect** on client (exponential backoff).
5. **Scale** with Redis pub/sub (multiple servers).
6. **Don't send everything** — only what changed.
7. **Compress** large messages (permessage-deflate).

## Human Notes

### WebSocket vs SSE vs Long polling

| | WebSocket | SSE | Long polling |
|---|---|---|---|
| Direction | Bidirectional | Server → client | Bidirectional |
| Protocol | WS | HTTP | HTTP |
| Best for | Chat, collaboration, games | Notifications, live updates | Legacy |

Default: WebSocket for bidirectional, SSE for server push.

### Server (Node + ws)
```js
import { WebSocketServer } from 'ws';

const wss = new WebSocketServer({ port: 8080 });

wss.on('connection', (ws, req) => {
  // Authenticate
  const token = new URL(req.url, 'http://x').searchParams.get('token');
  if (!verifyToken(token)) return ws.close();

  ws.on('message', (data) => {
    const msg = JSON.parse(data);
    // broadcast, etc.
  });

  // Heartbeat
  ws.isAlive = true;
  ws.on('pong', () => { ws.isAlive = true; });
});

// Heartbeat check
setInterval(() => {
  wss.clients.forEach((ws) => {
    if (!ws.isAlive) return ws.terminate();
    ws.isAlive = false;
    ws.ping();
  });
}, 30000);
```

### Client
```js
const ws = new WebSocket('wss://api.example.com/socket?token=...');

ws.onopen = () => console.log('connected');
ws.onmessage = (e) => console.log('message:', e.data);
ws.onerror = (e) => console.error('error:', e);
ws.onclose = () => {
  // Reconnect with backoff
  setTimeout(() => connect(), Math.min(1000 * 2 ** retries, 30000));
};
```

### Socket.IO (higher-level)
```js
// Server
import { Server } from 'socket.io';
const io = new Server(3000, { cors: { origin: '*' } });

io.on('connection', (socket) => {
  socket.join('room-123');
  socket.on('message', (msg) => {
    io.to('room-123').emit('message', msg);
  });
});

// Client
import { io } from 'socket.io-client';
const socket = io('https://api.example.com');
socket.emit('message', 'hello');
socket.on('message', (msg) => console.log(msg));
```

### Rooms
Group connections (e.g., per chat room, per user).
- `socket.join('room-123')`.
- `io.to('room-123').emit('event', data)`.

→ [WebSockets/rooms.md](rooms.md)

### Scaling
Single server: easy. Multiple servers: need Redis pub/sub.

```js
import { createAdapter } from '@socket.io/redis-adapter';
import { createClient } from 'redis';

const pubClient = createClient({ url: 'redis://localhost:6379' });
const subClient = pubClient.duplicate();
await Promise.all([pubClient.connect(), subClient.connect()]);
io.adapter(createAdapter(pubClient, subClient));
```

Now messages broadcast across servers.

→ [WebSockets/scaling.md](scaling.md)

### Authentication
- Token in query string (works but logs leak).
- Better: token in `Sec-WebSocket-Protocol` header or auth handshake.

### Heartbeat
- Send ping every 30s.
- If no pong in 10s, close connection.
- Detects dead TCP connections.

### Reconnection
- Client-side: exponential backoff.
- Cap at 30s.
- Don't reconnect if `close` was intentional.

### Message format
- JSON is fine for most cases.
- MessagePack / Protocol Buffers for high-throughput.

### Backpressure
- If client is slow, server can buffer.
- Track queue size, drop or close if too big.

## Common Mistakes

- ❌ No heartbeat (dead connections linger).
- ❌ No auth on socket connection.
- ❌ No reconnection logic.
- ❌ Not scaling beyond one server.
- ❌ Sending entire state on every change (send diffs).
- ❌ No backpressure handling.

## Tools

- ws: https://github.com/websockets/ws
- Socket.IO: https://socket.io/
- Ably: https://ably.com/ (managed)
- Pusher: https://pusher.com/ (managed)
- Supabase Realtime: https://supabase.com/realtime
- PartyKit (Cloudflare): https://partykit.io/
- Liveblocks: https://liveblocks.io/ (collaboration)
- Yjs (CRDTs): https://github.com/yjs/yjs

## References

- MDN WebSocket: https://developer.mozilla.org/en-US/docs/Web/API/WebSocket
- WebSocket protocol: https://www.rfc-editor.org/rfc/rfc6455
- Socket.IO docs: https://socket.io/docs/v4/

## Exercises

1. Build a chat app with Socket.IO + Redis for scaling.
2. Build a real-time dashboard with SSE.
3. Add reconnection with backoff.

## Projects

- Build a collaborative editor (Yjs + WebSocket).
- Build a multiplayer game.

---

**Previous:** [GraphQL/](../GraphQL/) · **Next:** [Backend/](../Backend/) · **Related:** [NodeJS/](../NodeJS/)
