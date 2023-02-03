# Applets and Handlers

A W3bstream Applet is a container for the actual logic of a W3bstrem node. Since W3bstream's execution engine is based on a WebAssembly virtual machine, Applets must be compiled as WASM modules:

{% hint style="success" %}
**W3bstream Applets must be compiled as WASM modules**
{% endhint %}

## Exporting event handlers

An Applet must export at least one public function to be called by the W3bstream Virtual Machine. Exported functions in an Applet are also called _Event Handlers_ and they can be used as the target _Handler_ in a Project's [event strategy.](applets-and-handlers.md#event-strategies)

Event Handlers in an applet must have the following signature:

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

## **Calling W3bstream host functions**

Using available SDKs, W3bstream applets can call several _host functions_, that give access to W3bstream's functionalities.&#x20;

Typical host functions that you'll want to call from an applet range from logging functions to, data storage to blockchain transactions.&#x20;

<mark style="color:purple;">**💡 Learn more**</mark>

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

{% content-ref url="../abi-functions-reference.md" %}
[abi-functions-reference.md](../abi-functions-reference.md)
{% endcontent-ref %}
