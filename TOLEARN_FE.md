
## FRONTEND COMMUNICATION METHODS
Here’s an updated list of frontend communication methods, including **Web Workers** and **Server-Sent Events (SSE)**, along with a brief example for each:

---

### 1. **AJAX (XMLHttpRequest / fetch)**
**Example:**
```javascript
fetch('/api/data')
  .then(response => response.json())
  .then(data => console.log(data));
```

---

### 2. **WebSockets**
**Example:**
```javascript
const socket = new WebSocket('ws://example.com/socket');
socket.onmessage = (event) => console.log(event.data);
```

---

### 3. **Server-Sent Events (SSE)**
**Example:**
```javascript
const evtSource = new EventSource('/events');
evtSource.onmessage = (event) => console.log(event.data);
```

---

### 4. **Web Workers**
**Example:**
```javascript
// worker.js
self.onmessage = (e) => self.postMessage(e.data * 2);

// main.js
const worker = new Worker('worker.js');
worker.onmessage = (e) => console.log(e.data);
worker.postMessage(10);
```

---

### 5. **REST APIs**
**Example:**
```javascript
fetch('/api/users', { method: 'GET' })
  .then(res => res.json())
  .then(users => console.log(users));
```

---

### 6. **GraphQL**
**Example:**
```javascript
fetch('/graphql', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ query: '{ users { id name } }' })
})
.then(res => res.json())
.then(data => console.log(data));
```

---

### 7. **gRPC-Web**
**Example:**  
*(Requires gRPC-Web client library; usage is more involved, so refer to [gRPC-Web docs](https://github.com/grpc/grpc-web) for setup.)*

---

### 8. **Long Polling**
**Example:**
```javascript
function poll() {
  fetch('/poll').then(res => res.json()).then(data => {
    console.log(data);
    poll(); // Call again for next update
  });
}
poll();
```

---

### 9. **MessageChannel**
**Example:**
```javascript
const channel = new MessageChannel();
channel.port1.onmessage = (e) => console.log(e.data);
channel.port2.postMessage('Hello from port2');
```

---

### 10. **Broadcast Channel API**
**Example:**
```javascript
const bc = new BroadcastChannel('test_channel');
bc.onmessage = (event) => console.log(event.data);
bc.postMessage('Hello, other tabs!');
```

---

### 11. **Shared Workers**
**Example:**
```javascript
// shared-worker.js
self.onconnect = (e) => {
  const port = e.ports[0];
  port.onmessage = (event) => port.postMessage('Hello from SharedWorker');
};

// main.js
const worker = new SharedWorker('shared-worker.js');
worker.port.onmessage = (e) => console.log(e.data);
worker.port.postMessage('Hello');
```

---

### 12. **IndexedDB / LocalStorage Events**
**Example:**
```javascript
window.addEventListener('storage', (event) => {
  console.log('Storage changed:', event.key, event.newValue);
});
localStorage.setItem('key', 'value');
```

---

### 13. **Push Notifications (Web Push)**
**Example:**  
*(Requires Service Worker registration and push subscription; see [MDN Web Push Guide](https://developer.mozilla.org/en-US/docs/Web/API/Push_API).)*

---

### 14. **WebRTC Data Channels**
**Example:**  
*(Requires peer connection setup; see [MDN WebRTC Data Channel Example](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel).)*

---

If you want code samples for gRPC-Web, Push Notifications, or WebRTC Data Channels, let me know! Would you like a comparison table or more details on any of these methods?