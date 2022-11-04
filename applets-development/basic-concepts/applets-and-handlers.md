# Applets and Handlers

A W3bstream Applet is a container for the actual logic of a W3bstrem node. Since W3bstream's execution engine is based on a W3bAssembly virtual machine, Applets must be compiled as WASM modules.

> _**W3bstream Applets must be compiled as WASM modules**_

An Applet must export at least one public function to be called by the W3bstream Virtual Machine. Exported functions in an Applet are also called _Event Handlers_ and they can be used as the target _Handler_ in a Project's [event strategy.](applets-and-handlers.md#event-strategies)

Event Handlers in an applet must have the following signature:

{% tabs %}
{% tab title="Rust" %}
```rust
// A W3bstream Event handler defined in an Applet
pub extern "C" fn do_something(eventt_id: i32) -> i32 { ... }
```
{% endtab %}
{% endtabs %}

&#x20; **  **<mark style="color:purple;">**💡 Learn more**</mark>

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
