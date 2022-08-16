---
description: Getting Started with development on the Stateset Commerce Network
---

# Get Started

In order to start developing your own project on the Stateset Network you will need to have the following tools installed and setup properly on your machine:

First we need to install Git, Node.js, Go and Rust:

**Install Git**

```
$ sudo apt-get update
```

```
$ sudo apt-get install git
```

**Install Node.js with NVM**

`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash`

Currently, Stateset uses Go 1.18 to compile the code.

**Install GO**

Install [Go 1.18 (opens new window)](https://go.dev/doc/install) by following instructions there.

Verify the installation by typing `go version` in your terminal.

`$ go version`&#x20;

`go version go1.18.1 darwin/amd64`



**Install Rust**

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh



**Docker and Docker Compose**

You will also need to install docker and docker-compose if you plan on running containerized version of stateset network.



