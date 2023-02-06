# Hello World!

{% hint style="info" %}
**Notice:** W3bstream is under development.&#x20;

The current documentation refers to _<mark style="color:blue;">W3bstream 1.0.0-rc2</mark>_
{% endhint %}

## Supported languages

SDKs to build W3bstream applets are available for the following languages:

* [AssemblyScript](https://github.com/machinefi/w3bstream-wasm-ts-sdk)
* [Go](https://github.com/machinefi/w3bstream-wasm-golang-sdk)

## Event handlers

When creating an applet for W3bstream, you must export at least one function inside the resulting WASM module, to serve as an _**event handler**_ in W3bstream.&#x20;

This handler can then be linked to a W3bstream event by configuring a _**strategy**_ in the project's [event strategies](basic-concepts/#event-strategies) configuration.&#x20;

<mark style="color:purple;">**💡 Learn more**</mark>

<details>

<summary>Default event handler</summary>

When [deploying an applet](../get-started/deploying-an-applet.md#deploy-the-logic) to a W3bstream project, W3bstream creates a default event strategy that connects **any** W3bstream event to a default `_start()` handler function with the following signature:

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

## The W3bstream Console

W3bstream provides a text console for applets to output text to, which can be accessed through the Log function of the SDK:

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { Log } from "../../assembly/index";
...
Log("Some text");

```
{% endtab %}

{% tab title="Golang" %}
```go
import 	"github.com/machinefi/w3bstream-wasm-golang-sdk/log"
...
log.Log("Some text");

```
{% endtab %}
{% endtabs %}

## Your first W3bstream "Hello World!"

Creating a “_Hello World!_” example for W3bstream is now very simple:

{% tabs %}
{% tab title="AssemblyScript" %}
### Get the project ready

Let's start with creating a new folder for the project

```bash
mkdir helloworld && cd helloworld
```

Initialize the project with `npm`

```bash
npm init -y
```

Install the AssemblyScript compiler

```bash
npm install --save-dev assemblyscript
```

Scaffold a new AssemblyScript project:

```bash
npx asinit .
```

Add the W3bstream AssemblyScript SDK package:

```bash
npm install @w3bstream/wasm-sdk
```

edit the `scripts` field in `package.json` and replace it with the following:

```json
"scripts": {
    "asbuild:release": "asc assembly/index.ts --use abort=assembly/index/abort --target release",
  },
```



### Create helloworld.ts

Edit `assembly/index.ts`, paste the following code and save it:

```typescript
import { Log } from "@w3bstream/wasm-sdk";
// Export alloc() is needed for w3bstream vm
export { alloc } from "@w3bstream/wasm-sdk";

export function start(rid: i32): i32 {
    Log("Hello World!");
    return 0;
}

// The abort method will be exposed inside w3bstream
// in a later release. For now, you can use it to log errors:
export function abort(
  message: string | null,
  fileName: string | null,
  lineNumber: u32,
  columnNumber: u32
): void { 
  if (message == null) message = "unknown error";
  if (fileName == null) fileName = "unknown file";
  Log("ABORT: " + message
    + " at " + fileName
    + ":" + lineNumber.toString() 
    + ":" + columnNumber.toString());
}
```

###

### Build the WASM module

Finally, build the wasm module with:

```bash
npm run asbuild
```

At the end of the building process, the W3bstream module can be found in `build/release.wasm`
{% endtab %}

{% tab title="Go" %}
### Get the project ready

Let's start with creating a new folder for the project

```bash
mkdir helloworld && cd helloworld
```

Initialize the project with `go mod`

```
go mod init helloworld
```



### Create helloworld.go

create `helloworld.go` with the current code and save it:o

```go
package main

import "github.com/machinefi/w3bstream-wasm-golang-sdk/log"

// main is required for TinyGo to compile to WASM
func main() {}

//export start
func _start(rid uint32) int32 {
	log.Log("Hello World!")
	return 0
}
```



### Build the WASM module for W3bstream

install required imports (in this case, the W3bstream Go SDK):

```
go mod tidy
```

make sure [you have TinyGo installed](https://tinygo.org/getting-started/install/) in your system, then buuild the module with:

```
tinygo build -o helloworld.wasm -scheduler=none --no-debug -target=wasi helloworld.go
```

At the end of the building process, the file `helloworld.wasm` can be found in the current folder.
{% endtab %}
{% endtabs %}

## Test Hello World in W3bstream!

Once you built the Hello World! example as a WASM module, you can upload and deploy it to the W3bstream node as explained in the Get Started section of this documentation:

{% content-ref url="../get-started/deploying-an-applet.md" %}
[deploying-an-applet.md](../get-started/deploying-an-applet.md)
{% endcontent-ref %}

then use the W3bstream Studio to send any message to your project (make sure the applet is running!):

{% content-ref url="../get-started/w3bstream-studio/testing-events.md" %}
[testing-events.md](../get-started/w3bstream-studio/testing-events.md)
{% endcontent-ref %}

finally, check the log of your W3bstream node: you should see the "Hello World!" string printed:

```json
...
// W3bstream calling the "start" handler upon message received
{
  "@lv": "info",
  "@prj": "srv-applet-mgr",
  "@ts": "20221102-140006.340Z",
  "msg": "call handler:start"
}
// This is the log from the start function
{
  "@applet": "MyApplet",
  "@lv": "info",
  "@namespace": "HelloWorldProject",
  "@prj": "srv-applet-mgr",
  "@src": "wasm",
  "@ts": "20221102-140006.340Z",
  "msg": "Hello World!"
}
```
