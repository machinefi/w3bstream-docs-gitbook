# Basic concepts

{% hint style="info" %}
**🚧 This document is a work in progress**
{% endhint %}

## Event Messages

While running, a W3bstream node emits internal **Event Messages** when something relevant happens. A W3bstream event can be currently generated  for one of the following reasons:

* A message sent to an HTTP API [_project_ _endpoint_](sending-messages-to-w3bstream.md#http-project-endpoints)__
* A message published to an MQTT [_project topic_](sending-messages-to-w3bstream.md#mqtt-project-topics)__
* A smart contract event detected by a [_blockchain monitor_](basic-concepts.md#blockchain-monitor)__

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

Once a W3bstream message is emitted, it's routed to the recipient [Project](basic-concepts.md#projects) which, in turn, routes the event's **payload** to the corresponding [Applet](basic-concepts.md#applets) handler.

#### <mark style="color:purple;"></mark>[<mark style="color:purple;">💡</mark>](https://emojipedia.org/light-bulb/) <mark style="color:purple;">Learn more</mark>

{% content-ref url="sending-messages-to-w3bstream.md" %}
[sending-messages-to-w3bstream.md](sending-messages-to-w3bstream.md)
{% endcontent-ref %}

{% content-ref url="monitoring-contracts.md" %}
[monitoring-contracts.md](monitoring-contracts.md)
{% endcontent-ref %}

## Projects

W3bstream Projects represent containers for the node logic. Each project also includes one or more [event strategy](basic-concepts.md#event-strategies) configurations, as well as [publisher](basic-concepts.md#publishers) authorizations.&#x20;

Every time a W3bstream event is emitted with a specific project as its recipient, the project's event strategy is evaluated. If a strategy is matched for the `event_type` field of the event, then the respective [Applet](basic-concepts.md#applets) handler is called with the event<mark style="color:purple;">'s</mark> `resource id` as the argument of the call.

&#x20;**** [<mark style="color:purple;">**💡**</mark>](https://emojipedia.org/light-bulb/) <mark style="color:purple;">**Learn more**</mark>

{% content-ref url="getting-events-data.md" %}
[getting-events-data.md](getting-events-data.md)
{% endcontent-ref %}

## Publishers

Publishers can be used as a basic way of authorizing external sources to send data to W3bstream projects through one of the network service endpoints (HTTP or MQTT). Therefore, a publisher represents an "account", with its unique _id_ and _auth_ _token,_ which are supposed to be included in the message header sent to W3bstream.&#x20;

{% hint style="success" %}
Messages that do not include in their header a _publisher_ _id_ and _token, that are_ valid for their recipient project, will be ignored by W3bstream.
{% endhint %}

##

## Event Strategies



## Applets

<details>

<summary>About WebAssembly</summary>

WebAssembly provides a way to create safe and portable code written in multiple languages that can run at near native speed. The full WebAssembly documentation is available at [https://developer.mozilla.org/en-US/docs/WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly)&#x20;

</details>

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

