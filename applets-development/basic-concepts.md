# Basic concepts

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

## Projects

A W3bstream project implements the logic of a MachineFi dApp at the W3bstream node level. During its normal execution, W3bstream emits internal events, projects configured in W3bstream respond to such events by running specific "event handlers".&#x20;

Since W3bstream runtime's _execution engine_ is based on a [WebAssembly](https://webassembly.org/) virtual machine, the project's logic must be compiled as WASM modules.&#x20;

<details>

<summary>About WebAssembly</summary>

WebAssembly provides a way to create safe and portable code written in multiple languages that can run at near native speed. The full WebAssembly documentation is available at [https://developer.mozilla.org/en-US/docs/WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly)&#x20;

</details>

In this document, we will use [W3bstream Studio](../get-started/w3bstream-studio.md), accessible on port :3000, that allows you to perform applets deployment.

## Events



## Strategies
