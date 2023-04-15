# Applets and Handlers

A W3bstream Applet is essentially a WebAssembly Module (WASM) that exports one or more functions, known as "Handlers". These Handlers are executed by W3bstream's Virtual Machine in response to specific events triggered within W3bstream, which are linked to a particular handler.

W3bstream Applets can access various functionalities of W3bstream, such as storing data in its database or executing smart contracts on supported blockchains.

<details>

<summary>About WebAssembly</summary>

WebAssembly is a binary instruction format that provides a safe and portable way to execute code written in multiple languages at near-native speeds. For more detailed information on WebAssembly, you can refer to the official documentation available at [https://developer.mozilla.org/en-US/docs/WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly).

W3bstream is built on the WebAssembly System Interface (WASI), which provides a standard interface between WebAssembly modules and their host environments. If you want to learn more about WASI, you can visit [https://github.com/bytecodealliance/wasmtime/blob/main/docs/WASI-intro.md](https://github.com/bytecodealliance/wasmtime/blob/main/docs/WASI-intro.md).

W3bstream supports multiple toolchains, including AssemblyScript, Rust and C/C++, which are natively supported, and Golang, which is supported through Tiny Go. Additionally, WebAssembly Text Format is also natively supported. Emscripten is used to support C/C++ toolchains.

**More resources**

* [WebAssembly Developer Guide](https://webassembly.org/getting-started/developers-guide/)
* [WebAssembly Tutorial](https://marcoselvatici.github.io/WASM\_tutorial/)

</details>

## Creating applets

To create a W3bstream Applet, you can build a WebAssembly module using one of the programming languages supported by the W3bstream SDKs. At a minimum, the Applet must export one function that can be executed by W3bstream's Virtual Machine. Additionally, Event Handlers in an Applet must have the following signature:

{% tabs %}
{% tab title="Typescript" %}
```typescript
// A W3bstream Event handler defined in an Applet written in AssemblyScript
export function start(rid: i32): i32
```
{% endtab %}

{% tab title="Go" %}
```go
// A W3bstream Event handler defined in an Applet written in Go
func do_something(event_id uint32) int32 
```
{% endtab %}

{% tab title="Rust" %}
```rust
// A W3bstream Event handler defined in an Appletwritten in Rust
pub extern "C" fn do_something(event_id: i32) -> i32 { ... }
```
{% endtab %}

{% tab title="C++" %}
```cpp
// A W3bstream Event handler defined in an Applet written in C++
EMSCRIPTEN_KEEPALIVE uint32_t do_something(uint32_t event_id)
```
{% endtab %}
{% endtabs %}
