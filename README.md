# 🔌 TCP Client-Server Authentication and File Transfer

**CPSC 441 – Computer Networks (Winter 2023)**
Author: Ryan Loi

## 📚 Project Overview

This project demonstrates robust **TCP socket programming in C** by building a client-server system that performs:

* **User authentication** computed via a custom protocol using a UCID and server timestamp.
* **Secure file transfer** from the server to the client only upon successful authentication of the created passcode.

This assignment showcases understanding of TCP networking fundamentals, system calls (`socket`, `bind`, `listen`, `accept`, `connect`, `send`, `recv`), error handling, string parsing, and basic protocol design.

---

## 🧠 Protocol Summary

1. **Client connects** to the server on a given port.
2. **Client inputs an 8-digit UCID**, which is validated and sent to the server.
3. **Server sends current datetime** string back to client.
4. Both sides **generate a PASSCODE**:

   * `PASSCODE = <seconds from datetime> + <last 4 digits of UCID>`
5. **Client sends its PASSCODE** to the server.
6. If PASSCODEs match, the **server streams contents of `data.txt`**.
7. **Client saves** this data into a file `savefile.txt`.
8. **A unique EOF flag** is used to signal the end of file transmission.

---

## 📁 Directory Structure

```
Assignment1/
├── client/
│   └── client.c         # Client code
├── server/
│   ├── server.c         # Server code
│   └── data.txt         # File sent to the client on success
```

---

## 🛠️ How to Compile and Run

> Tested and built for Linux (this code may not run properly on windows or MacOS). Requires GCC or any C compiler.

### 1. Compile

#### Server

from the root directory

```bash
cd "Server directory"
gcc server.c -o server
```

#### Client

from the root directory

```bash
cd "client directory"
gcc client.c -o client
```

### 2. Run

Note: the server must be started before the client, otherwise the connection will fail.

#### Start the Server

Give the server an unused port number to run, typically I use port 8080, if this doesn't work choose a port between: 2000 and 65535

```bash
./server <PORT>
```

Example:

```bash
./server 8080
```

The server will run forever so you can connect a client side as many times as you desire, to stop use:

```bash
ctrl + c
```

#### Start the Client

Give the client the same port number you gave the server.

```bash
./client <PORT>
```

Example:

```bash
./client 8080
```

---

After the client connects to the server enter a UCID, you can just use 123456789. After it is authenticated the file in the server directory will be transferred to the client directory via TCP.

## 📸 Screenshot

Below is a screenshot of the client output after successful authentication and file transfer:

![Screenshot](https://i.imgur.com/HUZ3Cje.png)

---


## 📌 Features & Highlights

* ✅ **Full error handling** for user input, connection failures, and file operations.
* 🔐 **PASSCODE-based validation** for a custom lightweight authentication protocol.
* 📄 **Server logs UCID** and interaction status.
* 📂 **Client writes file output** to `savefile.txt` after receiving chunks.
* 📢 **Logging for each key action**, including number of bytes received.
* 🧪 **Robust input validation** for UCID (must be 8 digits) and port number range (2000–65535).
* 📛 **Graceful handling of SIGPIPE** and other network errors.


## 🧠 Learning Outcomes

* Designed and implemented a TCP client-server model from scratch.
* Practiced input validation, file I/O, and string parsing in C.
* Gained confidence in systems programming, error handling, and network protocols.