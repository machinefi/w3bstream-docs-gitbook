# AssemblyScript

The W3bstream Applet AssemblyScript SDK is a set of tools and libraries that enable developers to create W3bstream applets using the AssemblyScript programming language.&#x20;

## Requirements

Before you can use the W3bstream Applet SDK for AssemblyScript, you need to have the following tools installed on your system:

* Node.js (version 16 or later)
* AssemblyScript (version 0.26.0 or later)

<details>

<summary>Create an AssemblyScript project</summary>

To create an AssemblyScript project, follow these steps:

1. **Create a new directory for your project:**

```
mkdir my-w3bstream-applet
cd my-w3bstream-applet
```

2. **Initialize a new Node.js project:**

```
npm init -y
```

3. **Install AssemblyScript as a development dependency:**

```
npm install --save-dev assemblyscript
```

4. initialize the AssemblyScript project:

```
npx asinit . -y
```

</details>

## Installation

Once you have created your AssemblyScript project, you can install the W3bstream WASM SDK by running the following command:

```
npm install @w3bstream/wasm-sdk
```

## Contribute

The source code of the W3bstream WASM AssemblyScript SDK, including examples, can be found on GitHub at:

{% embed url="https://github.com/machinefi/w3bstream-wasm-assemblyscript-sdk" %}
