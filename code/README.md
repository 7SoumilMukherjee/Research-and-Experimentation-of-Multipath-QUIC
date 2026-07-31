# Multipath QUIC (MPQUIC)

CoNEXT'17 Multipath QUIC (MPQUIC) implementation based on the `qdeconinck/mp-quic` repository.

## Overview

This directory contains the source code for the CoNEXT'17 Multipath QUIC (MPQUIC) implementation developed by Quentin De Coninck et al. The implementation extends the original **quic-go** project to support communication over multiple network paths.

The implementation was built and validated using the historical dependency versions required by the original CoNEXT'17 implementation.

---

## Software Requirements

| Requirement | Version |
|------------|---------|
| Operating System | Ubuntu Linux |
| Go | 1.9.7 |
| Build System | GOPATH |

> **Note:** Modern Go versions are not compatible with this implementation. The project should be built using **Go 1.9.7**.

---

# Build Instructions

## 1. Install Go 1.9.7

```bash
mkdir -p ~/sdk
cd ~/sdk

wget https://go.dev/dl/go1.9.7.linux-amd64.tar.gz

tar -xzf go1.9.7.linux-amd64.tar.gz

mv go go1.9.7
```

---

## 2. Configure Go

```bash
export GOROOT=$HOME/sdk/go1.9.7
export GOPATH=$HOME/go
export PATH=$GOROOT/bin:$PATH
```

Verify the installation:

```bash
go version
```

Expected output:

```text
go version go1.9.7 linux/amd64
```

To make the configuration permanent:

```bash
source ~/.bashrc
```

---

## 3. Create the GOPATH Structure

```bash
mkdir -p ~/go/src/github.com/lucas-clemente
mkdir -p ~/go/src/github.com/bifurcation
mkdir -p ~/go/src/github.com/hashicorp
mkdir -p ~/go/src/golang.org/x
```

---

## 4. Clone the Repository

```bash
cd ~/go/src/github.com/lucas-clemente

git clone https://github.com/qdeconinck/mp-quic.git quic-go

cd quic-go
```

Verify the branch:

```bash
git rev-parse --abbrev-ref HEAD
```

Expected output:

```text
conext17
```

---

## 5. Install Dependencies

### mint

```bash
cd ~/go/src/github.com/bifurcation

git clone https://github.com/bifurcation/mint.git

cd mint

git checkout a6080d464fb57a9330c2124ffb62f3c233e3400e
```

### golang-lru

```bash
cd ~/go/src/github.com/hashicorp

git clone https://github.com/hashicorp/golang-lru.git

cd golang-lru

git checkout db219ec
```

### aes12

```bash
cd ~/go/src/github.com/lucas-clemente

git clone https://github.com/lucas-clemente/aes12.git
```

### fnv128a

```bash
git clone https://github.com/lucas-clemente/fnv128a.git
```

### quic-go-certificates

```bash
git clone https://github.com/lucas-clemente/quic-go-certificates.git
```

### x/crypto

```bash
cd ~/go/src/golang.org/x

git clone https://github.com/golang/crypto.git

cd crypto

git checkout 0fcca48
```

---

## 6. Build the Library

```bash
cd ~/go/src/github.com/lucas-clemente/quic-go

go build .
```

---

## 7. Build the ReqRes Application

### Server

```bash
go build -o reqres-server ./example/reqres
```

### Client

```bash
go build -o reqres-client ./example/reqres/client
```

---

## 8. Verify the Build

List the generated binaries:

```bash
ls
```

Expected executables:

```text
reqres-server
reqres-client
```

Verify the binaries:

```bash
file reqres-server
file reqres-client
```

Both executables should be reported as Linux ELF binaries.

---

# Repository Structure

```text
.
├── ackhandler/          ACK processing and loss recovery
├── congestion/          Congestion control algorithms
├── example/             Example applications
│   └── reqres/          Request–Response application
├── h2quic/              HTTP/2 over QUIC
├── integrationtests/    Integration tests
├── internal/            Internal protocol implementation
├── qerr/                QUIC error definitions
├── server.go            QUIC server implementation
├── client.go            QUIC client implementation
├── session.go           Session management
├── scheduler.go         Packet scheduler
├── path.go              MPQUIC path abstraction
├── path_manager.go      Path management
├── pconn_manager.go     Interface discovery and packet connections
└── ...
```

---

## Reference

Q. De Coninck and O. Bonaventure, *Multipath QUIC: Design and Evaluation*, Proceedings of the 13th International Conference on Emerging Networking EXperiments and Technologies (CoNEXT), 2017.
