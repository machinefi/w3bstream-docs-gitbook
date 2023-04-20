# Rust

The W3bstream Applet KIT for Rust is a set of tools and libraries that enable developers to create W3bstream applets using the Rust programming language. The KIT provides wrappers for W3bstream's host functions, allowing Rust developers to interact with the W3bstream network and build decentralized applications that leverage the power and flexibility of the IoTeX blockchain.

## Requirements

Before you can use the W3bstream Applet KIT for Rust, you need to have the following tools installed on your system:

* Rust (version 1.55 or later)
* Cargo (version 1.55 or later)

<details>

<summary>Create a Rust project</summary>

1. Install Rust using the `rustup` tool by following the official instructions: [https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)

<!---->

2. Install the `cargo-wasi` crate with:

```
cargo install cargo-wasi
```

3. Add the wasm32-wasi target for Rust with:

```
rustup target add wasm32-wasi
```

4. Create a new Rust project with cargo:

```
cargo new my-w3bstream-applet
cd my-w3bstream-applet
```

</details>

## Installation

You can install the W3bastream Applet KIT for Rust using cargo inside your project's folder:

```
cargo add ws-sdk 
```

## Build

When it's time to build your applet, run the following:

```
cargo build --target=wasm32-wasi --release
```

The applet, in the form of a WASM file, is saved to `target/wasm32-wasi/release`

## Contribute

The source code of the W3bstream Applet KIT for Rust, including examples, can be found on GitHub at:

{% embed url="https://github.com/machinefi/w3bstream-wasm-rust-sdk" %}
