# Applets and Handlers

A W3bstream Applet is essentially a <mark style="color:purple;">WebAssembly Module (WASM)</mark> that exports one or more functions, referred to as "_Handlers_." These Handlers are executed by W3bstream's Execution Engine in response to specific events triggered within W3bstream, and each event is linked to a particular handler.

W3bstream Applets have the capability to access various functionalities of W3bstream, including storing and fetching IoT data, or executing smart contracts on supported blockchains.

<details>

<summary>About WebAssembly</summary>

WebAssembly is a binary instruction format that offers a secure and portable method for executing code written in various languages at nearly native speeds. For more comprehensive information on WebAssembly, you can refer to the official documentation available at [https://developer.mozilla.org/en-US/docs/WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly).

W3bstream is built on the WebAssembly System Interface (WASI), which establishes a standard interface between WebAssembly modules and their host environments. If you wish to learn more about WASI, you can visit [https://github.com/bytecodealliance/wasmtime/blob/main/docs/WASI-intro.md](https://github.com/bytecodealliance/wasmtime/blob/main/docs/WASI-intro.md).

W3bstream supports multiple toolchains, including AssemblyScript and Rust, which are natively supported. Go lang is also supported through TinyGo. Furthermore, WebAssembly Text Format is natively supported, while Emscripten is utilized to support C/C++ toolchains.

For additional resources, you may find the following helpful:

**More resources**

* [WebAssembly Developer Guide](https://webassembly.org/getting-started/developers-guide/)
* [WebAssembly Tutorial](https://marcoselvatici.github.io/WASM\_tutorial/)

</details>
