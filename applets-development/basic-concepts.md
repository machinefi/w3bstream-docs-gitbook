# Basic concepts

{% hint style="info" %}
**🚧 This document is a work in progress**
{% endhint %}

## Event Messages

While running, a W3bstream node emits internal **Event Messages** when something relevant happens. A W3bstream event can be currently generated  for the following reasons:

* A call to an HTTP API _project_ _endpoint_
* A message published on the MQTT broker
* A smart contract event detected by a _blockchain monitor_

A W3bstream event message looks like the following:

```json
{
  "header": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJQYXlsb2FkIjoiNDUwNTI4NzAxMjc2NTcwMyIsImlzcyI6InNydi1hcHBsZXQtbWdyIiwiZXhwIjoxNjY4Mzk4MDYxfQ._Q5ZaBP5FSa09s0FCn7CBcMCty9hkM5TDu5q1wTvwB8",
    "event_type": "ANY",
    "pub_id": "my_publisher_id",
    "pub_time": 1667343986249
  },
    "payload": "This is the event payload data",
}
```

Once a W3bstream message is emitted, it's routed to the recipient [Project](basic-concepts.md#projects) which, in turn, routes the event **payload** to the corresponding [Applet](basic-concepts.md#applets) handler.

To learn more about how to send messages to a W3bstream node check out [sending-messages-to-w3bstream.md](sending-messages-to-w3bstream.md "mention")

## Projects

A W3bstream Project is a container for node logic, events configuration and authorizations.  Each event has a recipient project to which the event will be routed A W3bstream event can be currently generated in one of the following ways:

* Sending a message to the W3bstream node to an HTTP API endpoint
* Sending a message to the W3bstream node to the MQTT endpoint
* Configuring a blockchain monitor&#x20;

&#x20;projects configured in W3bstream respond to such events by running specific "event handlers".&#x20;

Since W3bstream runtime's _execution engine_ is based on a [WebAssembly](https://webassembly.org/) virtual machine, the project's logic must be compiled as WASM modules.&#x20;

<details>

<summary>About WebAssembly</summary>

WebAssembly provides a way to create safe and portable code written in multiple languages that can run at near native speed. The full WebAssembly documentation is available at [https://developer.mozilla.org/en-US/docs/WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly)&#x20;

</details>

In this document, we will use [W3bstream Studio](../get-started/w3bstream-studio.md), accessible on port :3000, that allows you to perform applets deployment.

A W3bstream Event represents a notification&#x20;

## Applets

W3bstream's execution engine is based on a WebAssembly virtual machine, therefore W3bstream applets must be compiled as WebAssembly Modules (WASM). WASM is a binary instruction format designed for the WebAssembly abstract, stack-based machine.

WASM binaries can be generated from multiple high-level languages, including:

* WebAssembly Text Format ([natively supported](https://developer.mozilla.org/en-US/docs/WebAssembly/Understanding\_the\_text\_format))
* AssemblyScript [(natively supported)](https://www.assemblyscript.org/introduction.html)
* Rust ([natively supported)](https://rustwasm.github.io/docs/book/introduction.html)
* C/C++ (supported through [emscripten](https://emscripten.org/index.html))
* Golang (supported through [tiny go](https://tinygo.org/docs/))

Other resources to learn WebAssembly are:

* [WebAssembly Full Documentation](https://developer.mozilla.org/en-US/docs/WebAssembly)
* [WebAssembly Developer Guide](https://webassembly.org/getting-started/developers-guide/)
* [WebAssembly Tutorial](https://marcoselvatici.github.io/WASM\_tutorial/)

## Blockchain Monitor



## Strategies
