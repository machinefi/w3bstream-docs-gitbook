# Go

The W3bstream Applet KIT for Go is a set of tools and libraries that enable developers to create W3bstream applets using the Go programming language. The KIT provides wrappers for W3bstream's host functions, allowing Go developers to interact with the W3bstream network and build decentralized applications that leverage the power and flexibility of the IoTeX blockchain.

## Requirements

Before you can use the W3bstream Applet KIT for Go, you need to have the following tools installed on your system:

* Go (version 1.18 or later)
* TinyGo (0.25.0 or later)

<details>

<summary>Create a Go project</summary>

1. Install Go using by following the official instructions: [https://go.dev/doc/install](https://go.dev/doc/install)
2. Create a new folder for your project

```
mkdir my-w3bstream-applet 
cd my-w3bstream-applet
```

3. Initialize the project with `go mod`:

```
go mod init my-w3bstream-applet
```

</details>

## Installation

To use the W3bstream Applet KIT in your Go projects, just import the module with:

```go
package main

import "github.com/machinefi/w3bstream-wasm-golang-sdk/log"
...
```

## Build

When it's time to build your applet, follow these steps:

1. Run the following to download all required packages, including the W3bstream KIT:

```
go mod tidy
```

2. Build the applet as a WASM module with:

```
tinygo build -o my-w3bstream-applet.wasm -scheduler=none --no-debug -target=wasi my-w3bstream-applet.go
```

## Contribute

The source code of the W3bstream Applet KIT for Go, including examples, can be found on GitHub at:

{% embed url="https://github.com/machinefi/w3bstream-wasm-golang-sdk" %}
