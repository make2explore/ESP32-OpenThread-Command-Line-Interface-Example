# OpenThread CLI – TCP & UDP Messaging Demo (ESP32)

<p align="center">
  <img src="docs/images/openthread-banner.png" alt="OpenThread CLI Banner" width="720" />
</p>

<p align="center">
  <a href="https://github.com/espressif/esp-idf">
    <img src="https://img.shields.io/badge/ESP–IDF-v5.x-blue?style=for-the-badge" alt="ESP-IDF">
  </a>
  <img src="https://img.shields.io/badge/Platform-ESP32C6%20%7C%20ESP32H2-green?style=for-the-badge" alt="Platform">
  <img src="https://img.shields.io/badge/Protocol-Thread%20(OpenThread)-orange?style=for-the-badge" alt="Thread">
  <img src="https://img.shields.io/badge/License-MIT-purple?style=for-the-badge" alt="License">
</p>

---

## 🌐 Overview

This repository demonstrates how to use **OpenThread CLI** on ESP32 devices to send messages between Thread nodes using **TCP** and **UDP** sockets.

It is based on the official ESP-IDF example:

```text
examples/openthread/ot_cli
```

With just CLI commands, you can:

- Form a Thread mesh network 🕸️  
- Bring multiple ESP32 nodes online  
- Open TCP and UDP sockets  
- Exchange messages between nodes  
- Inspect and debug Thread behavior in real time  

---


## 🕸️ Thread Topology

A simple two-node setup:

```text
        +-------------------+
        |   ESP32 Node #1   |
        |   Thread Leader   |
        |   TCP Server      |
        +---------+---------+
                  |
                  |  Thread Mesh
                  |
        +---------+---------+
        |   ESP32 Node #2   |
        |   Router / Child  |
        |   TCP/UDP Client  |
        +-------------------+
```
  
---
## 📶 Setup the Thread network    
Please first refer our [This Guide](https://github.com/make2explore/ESP32-OpenThread-Command-Line-Example/tree/main/OT-CLI-TCP-UDP-demo) to setup the ESP devices for Thread Network TCP/UDP communication  
  
---
  
## 🔁 TCP Messaging Demo

### 1️⃣ Start TCP Server (Leader Node)

```text
> tcpsockserver open
> tcpsockserver bind :: 12345
```

This opens a TCP socket server on port **12345**.

### 2️⃣ Start TCP Client (Child Node)

```text
> tcpsockclient connect <IP> <Port>
```

Example:

```text
> tcpsockclient connect fd11:22::abcd 12345
```

### 3️⃣ Exchange Messages

Client → Server:

```text
> tcpsockclient send hello
```

Server → Client:

```text
> tcpsockserver send hi
```

### 4️⃣ Close the Connection

Client:

```text
> tcpsockclient close
```

Server:

```text
> tcpsockserver close
```

### 📊 TCP Flow Diagram
  
```mermaid
sequenceDiagram
    participant Client as ESP32 TCP Client
    participant Server as ESP32 TCP Server
    Client->>Server: Connect
    Client->>Server: send "hello"
    Server->>Client: send "hi"
    Client->>Server: Close
```

---

## 📡 UDP Messaging Demo

### 1️⃣ Node 1 – UDP Listener

```text
> udp open
> udp bind :: 1234
```

### 2️⃣ Node 2 – UDP Sender

```text
> udp open
> udp send <A_mesh_local_EID> 1234 hello
```

Example:

```text
> udp send fd11:22::abcd 1234 hello
```

### 📊 UDP Flow Diagram
  
  
```mermaid
sequenceDiagram
    participant Sender as ESP32 UDP Sender
    participant Listener as ESP32 UDP Listener
    Sender->>Listener: send "hello" (UDP)
```

---

## 🧰 OpenThread CLI Quick Reference

Some handy commands:

```text
help
state
ipaddr
dataset active
thread start
scan
neighbor table
child table
```

- `state` – shows if node is leader/router/child  
- `ipaddr` – lists IPv6 addresses (Mesh-local, Link-local, RLOC, etc.)  
- `scan` – scans for nearby Thread networks  

---

## 🧱 Building & Flashing (ESP-IDF)

```bash
idf.py set-target esp32c6
idf.py build
idf.py flash monitor
```

Make sure OpenThread is enabled and you are using an ESP32 variant with Thread (802.15.4) support.

---

## 💡 Future Ideas

- Add Matter-over-Thread demo (On/Off Light, for example)  
- Add MQTT-over-Thread bridge  
- Integrate with OTBR (OpenThread Border Router)  
- Add Python scripts to automate CLI testing  

---

## 📜 License

This project is released under the **MIT License**.  
Feel free to use it as a starting point for your own Thread + ESP32 demos, talks, and YouTube videos.

---
