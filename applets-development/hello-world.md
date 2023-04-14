# Hello World!

This guide will quickly take you through how to create a W3bstream applet that outputs the "Hello, World!" string to the W3bstream Project's console each time a new data message is received.

## Create the applet

1. First create a project for your applet using the programming language of your choice:

{% tabs %}
{% tab title="AssemblyScript" %}
Follow the instructions about how to create a AssemBliscript project and install the applet SDK for AssemblyScript:

[AssemblyScript requirements](applet-sdks/assemblyscript.md#requirements)
{% endtab %}

{% tab title="Rust" %}
Follow the instructions about how to create a Rust project and install the applet SDK for Rust:

[Rust requirements](applet-sdks/rust.md#requirements)
{% endtab %}

{% tab title="Go" %}
Follow the instructions about how to create a Go project and install the applet SDK for Go:

[Go requirements](applet-sdks/go.md#requirements)
{% endtab %}
{% endtabs %}

2. Create the "Hello, World!" code:

{% tabs %}
{% tab title="AssemblyScript" %}
Edit the file `index.ts` inside the `assembly` folder and copy paste the code below:

```typescript
import { Log } from "@w3bstream/wasm-sdk";

export function start(rid: i32): i32 {
    Log("Hello World!");
    return 0;
}
```
{% endtab %}

{% tab title="Rust" %}
Edit the file `main.rs` inside the `src` folder and copy paste the code below:

````rust
```
use ws_sdk::log::log_info;

#[no_mangle]
pub extern "C" fn start(_rid: i32) -> i32 {
    let _result = log_info("Hello, World!");
    return 0;
}
// main is required for R to compile to Wasm.
fn main() {}
```
````
{% endtab %}

{% tab title="Go" %}
Create and edit a `helloworld.go` file, and copy paste the following code:

```go
//go:build tinygo
package main

import (
	"github.com/machinefi/w3bstream-wasm-golang-sdk/log"
)

// main is required for TinyGo to compile to Wasm.
func main() {}

//export start
func _start(rid uint32) int32 {
	log.Log("Hello, World!")
	return 0
}

```
{% endtab %}
{% endtabs %}

<details>

<summary>Learn more: <strong>Default event handler</strong></summary>

The reason we created a function called `start` is that, when deploying an applet to a W3bstream project, a default route is created that connects any W3bstream event to a `start` handler function.

**AssemblyScript**

```typescript
export function start(rid: i32): i32
```

**Go**

```go
//export start
func _start(event_id uint32) int32
```

**Rust**

```rust
#[no_mangle]
pub extern "C" fn start(event_id: i32) -> i32
```

**C++**

```cpp
#EMSCRIPTEN_KEEPALIVE uint32_t _start(uint32_t event_id)
```

</details>

3. Build the applet

To build the w3bstream applet, you must generate the WASM module:

{% tabs %}
{% tab title="AssemblyScript" %}
Inside the main folder of your project, run:

```
npm run asbuild
```
{% endtab %}

{% tab title="Rust" %}
Inside the main folder of your project, run:

```
cargo build --target=wasm32-wasi --release
```
{% endtab %}

{% tab title="Go" %}
Inside the main folder of your project, run:

```
tinygo build  -o helloworld.wasm -scheduler=none --no-debug -target=wasi helloworld.go
```
{% endtab %}
{% endtabs %}

## Test Hello World in W3bstream!

{% hint style="info" %}
Work in progress
{% endhint %}
