# Same-Network Data Transfer

A real-time data transfer application that enables instant communication between devices on the same network using WebSockets. Built with Vue 3 frontend and Node.js backend, containerized with Docker for seamless deployment.

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Running the Project](#running-the-project)
- [Project Structure](#project-structure)
- [Features](#features)
- [Technologies](#technologies)
- [Development](#development)
- [Troubleshooting](#troubleshooting)

## Overview

This project provides a simple yet powerful solution for transferring data between devices on the same local network. It uses WebSocket technology to establish persistent, bidirectional communication channels, enabling real-time message broadcasting across all connected clients.

Perfect for:
- Local network file sharing
- Real-time collaboration tools
- IoT device communication
- Local development and testing

## Architecture

```
┌─────────────────────────────────────────┐
│         Vue 3 Frontend (Port 5173)       │
│  - Vite development server               │
│  - Real-time UI updates                  │
│  - Router & State Management (Pinia)     │
└──────────────────┬──────────────────────┘
                   │ WebSocket
                   ▼
┌─────────────────────────────────────────┐
│    Node.js WebSocket Server (Port 3000) │
│  - Message broadcasting                  │
│  - Client connection management          │
└─────────────────────────────────────────┘
```

## Prerequisites

- **Docker & Docker Compose** (recommended)
  - Docker Engine 20.10+
  - Docker Compose 2.0+
  
OR

- **Node.js** 20.19.0 or 22.12.0+
- **npm** or **yarn**

## Installation

### Option 1: Using Docker (Recommended)

1. **Clone the repository**
   ```bash
   cd Same-network-data-transfer
   ```

2. **Build and run with Docker Compose**
   ```bash
   docker-compose up --build
   ```

   The application will be available at:
   - Frontend: http://localhost:5173
   - WebSocket Server: ws://localhost:3000

### Option 2: Local Development (Without Docker)

#### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start development server**
   ```bash
   npm run dev
   ```
   
   Access at: http://localhost:5173

#### WebSocket Server Setup

1. **Navigate to websocket-server directory**
   ```bash
   cd websocket-server
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the server**
   ```bash
   node server.js
   ```
   
   Server runs on: ws://localhost:3000

## Project Structure

```
.
├── docker-compose.yml          # Docker Compose configuration
├── README.md                   # This file
│
├── docker/
│   └── node/
│       └── Dockerfile         # Node.js Docker image
│
├── frontend/                   # Vue 3 + Vite application
│   ├── src/
│   │   ├── components/        # Vue components
│   │   │   ├── HelloWorld.vue
│   │   │   ├── TheWelcome.vue
│   │   │   └── icons/         # Icon components
│   │   ├── views/             # Page components
│   │   │   ├── HomeView.vue
│   │   │   ├── AboutView.vue
│   │   │   └── MessagesView.vue
│   │   ├── stores/            # Pinia state management
│   │   │   └── counter.js
│   │   ├── router/            # Vue Router configuration
│   │   │   └── index.js
│   │   ├── assets/            # CSS and static assets
│   │   ├── App.vue            # Root component
│   │   └── main.js            # Entry point
│   ├── package.json
│   └── vite.config.js
│
└── websocket-server/           # Node.js WebSocket server
    ├── server.js              # Main server file
    ├── Dockerfile
    └── package.json
```

## Features

- **Real-time Communication**: Instant message delivery via WebSockets
- **Message Broadcasting**: Messages are sent to all connected clients
- **Persistent Connections**: Maintains connection state across sessions
- **Containerized**: Easy deployment with Docker
- **Modern Frontend**: Vue 3 with reactive state management
- **Responsive Design**: Works across different device types

## Technologies

### Frontend
- **Vue 3** - Progressive JavaScript framework
- **Vite** - Next-generation frontend build tool
- **Vue Router** - Official router for Vue
- **Pinia** - Store management library
- **JavaScript (ES Modules)** - Modern JavaScript

### Backend
- **Node.js** - JavaScript runtime
- **ws** - WebSocket library for Node.js

### DevOps
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration

## Development

### Available Scripts

#### Frontend
```bash
npm run dev       # Start development server with HMR
npm run build     # Build for production
npm run preview   # Preview production build
npm run format    # Format code with Prettier
```

#### WebSocket Server
```bash
node server.js    # Start the server
```

### Code Formatting

The frontend uses Prettier for code formatting:
```bash
cd frontend
npm run format
```

## Troubleshooting

### Issue: WebSocket connection refused
- **Solution**: Ensure WebSocket server is running on port 3000
- Check firewall settings allowing port 3000

### Issue: Frontend can't reach WebSocket server
- **Docker**: Ensure both containers are on the same network
- **Local**: Verify WebSocket server URL in frontend matches (ws://localhost:3000)

### Issue: Port already in use
```bash
# Find process using port
lsof -i :5173    # Frontend
lsof -i :3000    # WebSocket server

# Kill process (if needed)
kill -9 <PID>
```

### Issue: Docker build fails
```bash
# Clean Docker artifacts
docker-compose down
docker system prune -a

# Rebuild
docker-compose up --build
```

## Network Configuration

### Accessing from Another Device on the Same Network

1. Find your machine's IP address:
   ```bash
   # Windows
   ipconfig
   
   # Linux/Mac
   ifconfig
   ```

2. Connect from another device using:
   - Frontend: `http://<YOUR_IP>:5173`
   - WebSocket: `ws://<YOUR_IP>:3000`

## License

This project is open source and available under the ISC License.

## Contributing

Contributions are welcome! Feel free to:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---
