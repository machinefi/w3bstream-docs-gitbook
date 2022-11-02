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

{% content-ref url="../get-started/w3bstream-studio/creating-projects.md" %}
[creating-projects.md](../get-started/w3bstream-studio/creating-projects.md)
{% endcontent-ref %}

{% content-ref url="getting-events-data.md" %}
[getting-events-data.md](getting-events-data.md)
{% endcontent-ref %}

## Publishers

Publishers can be used as a basic way of authorizing external sources to send data to W3bstream projects through one of the network service endpoints (HTTP or MQTT). Therefore, a publisher represents an "account", with its unique _id_ and _auth_ _token, that belong to a specific project._ The publisher id and auth token must be included in the message header when sending a message to a W3bstream project, in the `pub_id` and `token` fields, respectively.

{% hint style="success" %}
Messages that do not include in their header a _publisher_ _id_ and _token that are_ valid for their recipient project, will be ignored by W3bstream.
{% endhint %}

&#x20;**** [<mark style="color:purple;">**💡**</mark>](https://emojipedia.org/light-bulb/) <mark style="color:purple;">**Learn more**</mark>

{% content-ref url="../get-started/w3bstream-studio/adding-publishers.md" %}
[adding-publishers.md](../get-started/w3bstream-studio/adding-publishers.md)
{% endcontent-ref %}

{% content-ref url="sending-messages-to-w3bstream.md" %}
[sending-messages-to-w3bstream.md](sending-messages-to-w3bstream.md)
{% endcontent-ref %}

## Event Strategies

Event strategies can be used to define "_what to do"_ when a certain event is emitted in W3bstream. Therefore, an event strategy represents a _rule_ that assigns an applet's function (aka "_event handler_") to a certain _event type_. The event type must be specified in the message header when sending a message to a w3bstream project, using the `event_type` field. The event type can be any string, as long as it's matched by an event strategy.

{% hint style="success" %}
Messages that do not include in their header an _event\_type_ _that is_ matched by an event strategy of their recipient project, will not trigger any logic exectution. Instead they will just be logged in the console, before being dropped by W3bstream.
{% endhint %}

&#x20;**** [<mark style="color:purple;">**💡**</mark>](https://emojipedia.org/light-bulb/) <mark style="color:purple;">**Learn more**</mark>

{% content-ref url="../get-started/w3bstream-studio/creating-strategies.md" %}
[creating-strategies.md](../get-started/w3bstream-studio/creating-strategies.md)
{% endcontent-ref %}

## Applets

A W3bstream Applet is a container for the actual logic of a W3bstrem node. Since W3bstream's execution engine is based on a W3bAssembly virtual machine, Applets must be compiled as WASM modules.

An applet can include one or more functions, however, at least one of them must be publicly exported to be called by the W3bstream VM. Exported functions in an Applet are also called _event handlers_, since they can be used as a target function in a Project's [event strategy.](basic-concepts.md#event-strategies)

Event Handlers in an applet must have the following signature:

```rust
// An applet's event handler
pub extern "C" fn do_something(resource_id: i32) -> i32 
```

&#x20;**** [<mark style="color:purple;">**💡**</mark>](https://emojipedia.org/light-bulb/) <mark style="color:purple;">**Learn more**</mark>

<details>

<summary>About WebAssembly</summary>

WebAssembly provides a way to create safe and portable code written in multiple languages that can run at near native speed. The full WebAssembly documentation is available at [https://developer.mozilla.org/en-US/docs/WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly)&#x20;

W3bstream is based on the WASI interface. To learn more about WASI, check out [https://github.com/bytecodealliance/wasmtime/blob/main/docs/WASI-intro.md](https://github.com/bytecodealliance/wasmtime/blob/main/docs/WASI-intro.md)

**Supported toolchains**

* WebAssembly Text Format ([natively supported](https://developer.mozilla.org/en-US/docs/WebAssembly/Understanding\_the\_text\_format))
* Rust ([natively supported)](https://rustwasm.github.io/docs/book/introduction.html)
* C/C++ (supported through [emscripten](https://emscripten.org/index.html))
* Golang (supported through [tiny go](https://tinygo.org/docs/))

**More resources**

* [WebAssembly Developer Guide](https://webassembly.org/getting-started/developers-guide/)
* [WebAssembly Tutorial](https://marcoselvatici.github.io/WASM\_tutorial/)

</details>

## Blockchain Monitor

{% hint style="info" %}
**Notice**

* The current implementation of the blockchain monitor is experimental, and will be replaced soon.&#x20;
* Only the IoTeX blockchain is currently supported by the blockchain monitor.&#x20;
* Only the HTTP API can be used to enable the monitor.
{% endhint %}

The blockchain monitor is an internal W3bstream module that can emit W3bstream events when a certain blockchain event is emitted by a smart contract.

You can configure and start one monitor for each smart contract event you are interested in.&#x20;

Make sure you log in using the API first:

```bash
export TOK=$(echo '{"username":"admin","password":"iotex.W3B.admin"}' | http put :8888/srv-applet-mgr/v0/login | jq .token -r)To configure and start a blockchain monitor, make sure your W3bstream node is running, then type the command below. Make sure you replace: 
```

then you can start a blockchain event monitor typing the commend below (please notice it's using the [httpie](https://httpie.io/) client), after replacing:

* `chainID` with 4690 for the IoTeX Testnet, 4689 for the IoTeX Mainnet; &#x20;
* `contractAddress` with the actual address of the contract you want to monitor;&#x20;
* `topic0` with the topic of the smart contract event that you want to detect
* `eventType` with the event type code that matches your [Project strategy](basic-concepts.md#event-strategies) for this specific event

```bash
echo '{\
  "contractLog": {\
    "chainID": 4690,\ 
    "contractAddress": "0x6a0BFf625A70C43bcEEFAC51aF928ae545941b4A",\
    "blockStart": 17058530,\
    "blockEnd": 100000000,\
    "topic0":"0x766e6460a49ca518797200f8d2b455a80962f1e6acdcda61000fc3dc2004db88",\
    "eventType":"EXAMP1"\
  }\
}' | http :8888/srv-applet-mgr/v0/project/monitor/<PROJECT_ID> -A bearer -a $TOK
```

&#x20;**** [<mark style="color:purple;">**💡**</mark>](https://emojipedia.org/light-bulb/) <mark style="color:purple;">**Learn more**</mark>

{% content-ref url="monitoring-contracts.md" %}
[monitoring-contracts.md](monitoring-contracts.md)
{% endcontent-ref %}
