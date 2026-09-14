# PeerSend

A zero-knowledge, peer-to-peer (P2P) file-sharing web app. Files stream directly between browsers using WebRTC without ever touching a server.

## Features

- **End-to-End Encrypted:** Direct P2P transfer via WebRTC (DTLS/SCTP).
- **Zero Server Storage:** Files are chunked and streamed in memory.
- **Ephemeral Room Codes:** Pair devices quickly with 6-digit codes.

---

## Architecture

```
[ Sender ] <--- WebSockets (Room Codes / SDP) ---> [ Signaling Server ]
    |                                                      |
    +============== Direct WebRTC P2P Tunnel ==============+
                     (Encrypted Transfer)
```

1. **Signaling:** Peers pair via WebSocket and exchange SDP/ICE metadata.
2. **Tunneling:** A direct WebRTC `RTCDataChannel` connection is established.
3. **Transfer:** Sender streams chunked binary data directly to the receiver.

---

## Quick Start

### 1. Run Signaling Server
```bash
cd server
npm install
npm run dev # Runs on ws://localhost:8080
```

### 2. Run Frontend
```bash
cd client
npm install
echo "NEXT_PUBLIC_SIGNALING_SERVER_URL=ws://localhost:8080" > .env.local
npm run dev # Opens at http://localhost:3000
```

---
