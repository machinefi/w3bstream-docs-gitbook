# Hello World!

{% hint style="info" %}
**Notice:** W3bstream is under development.&#x20;

The current documentation refers to _<mark style="color:blue;">W3bstream 1.0 Alpha</mark> release,_ and is subject to frequent changes.
{% endhint %}

## Prerequisites

When creating a W3bstream applet in the [language of your choice](basic-concepts/#applets), you will have to follow a few simple rules:

#### Provide a malloc() implementation

You need to provide an implementation of the `malloc()` function for the WebAssembly virtual machine to be able to allocate memory in the host. This depends on the programming language you are using:

{% tabs %}
{% tab title="Golang" %}
In Go you don't need to provide a malloc implementation as it's automatically added by the tiniGo compiler
{% endtab %}

{% tab title="C/C++" %}
In C you are supposed to provide an implementation of `malloc` and make sure it's exported:

```cpp
EMSCRIPTEN_KEEPALIVE uint32_t malloc(uint32_t size) { return malloc(size); } 
```
{% endtab %}

{% tab title="Rust" %}
In Rust you don't need to provide a malloc implementation as it's automatically added by the  compiler
{% endtab %}
{% endtabs %}

#### Event handlers

It's assumed that you have at least one function publicly exported in your applet to serve as an _event handler_ in W3bstream. This handler should be linked to a W3bstream _event type_ in the project's [event strategies](basic-concepts/#event-strategies) configuration.&#x20;

Notice that, by default, when [deploying an applet](../get-started/deploying-an-applet.md#deploy-the-logic) to a project, W3bstream creates a default event strategy that connects **any** node event to a default `_start()` handler function with the following signature:

{% tabs %}
{% tab title="Golang" %}
```go
func _start(resource_id uint32) int32
```
{% endtab %}

{% tab title="C/C++" %}
```cpp
EMSCRIPTEN_KEEPALIVE uint32_t _start(uint32_t resource_id = 0)
```
{% endtab %}

{% tab title="Rust" %}
```rust
func _start(resource_id uint32) int32uThe log function
```
{% endtab %}
{% endtabs %}

**Accessing the W3bstream console**

W3bstream provides a text console for applets to output text to. In order to be able to send output to the W3bstream console, you'll have to declare an external `_log()` function that is exported by the W3bstream node, giving you access to the console:

{% tabs %}
{% tab title="Golang" %}
```go
//go:wasm-module env 
//export ws_log 
func _ws_log(logLevel, ptr, size uint32) int32
```
{% endtab %}

{% tab title="C/C++" %}
```cpp
#include <emscripten.h>

extern EM_IMPORT(ws_log) int ws_log(int, int, int);
```
{% endtab %}

{% tab title="Rust" %}
```rust
#[link(wasm_import_module = "env")]
extern "C" fn ws_log(log_level: i32, ptr: *const u8, size: i32) -> i32;
```
{% endtab %}
{% endtabs %}

## Create Hello World!

Creating a “_Hello World!_” example for W3bstream is now very simple:

{% tabs %}
{% tab title="Golang" %}
```go
// log.go
package main

import (
	"fmt"
	"reflect"
	"unsafe"
)

// main is required for TinyGo to compile to Wasm.
func main() {}

func _log(uint32 logLevel, strPtr uint32, strSize uint32)

func _start(rid uint32) int32 {
  	ptr, size := stringToPtr("Hello World!)
  	const LOG_LEVEL_INFO = 3
  	_log(LOG_LEVEL_INFO, ptr, size)
  	return 0
}

func stringToPtr(s string) (uint32, uint32) {
	buf := []byte(s)
	ptr := &buf[0]
	unsafePtr := uintptr(unsafe.Pointer(ptr))
	return uint32(unsafePtr), uint32(len(buf))
}

```

Use the TinyGo to build the WASM module

```bash
tinygo build -o log.wasm -scheduler=none --no-debug -target=wasi log.go
```
{% endtab %}

{% tab title="C/C++" %}
```cpp
// helloworld.c
#include <emscripten.h>
#include <string.h>
#include <stdio.h>

extern EM_IMPORT(ws_log) int ws_log(int logLevel, int strPtr, int strSize);

const LOG_LEVEL_INFO = 3;

EMSCRIPTEN_KEEPALIVE int start(int)
{
    char str[] = "Hello World!";
    ws_log(LOG_LEVEL_INFO, (int)str, strlen(str));
    return 0;
}

EMSCRIPTEN_KEEPALIVE int malloc(int size)
{
    return malloc(size);
}
```



Use the emscripten compiler to build the WASM module:

```bash
emcc -o helloworld.wasm -O2 --no-entry -s LLD_REPORT_UNDEFINED -s ERROR_ON_UNDEFINED_SYMBOLS=0 helloworld.c
```
{% endtab %}

{% tab title="Rust" %}
```rust
#[link(wasm_import_module = "env")]
extern "C" {
    fn ws_log(log_level: i32, ptr: *const u8, size: i32) -> i32;
}

#[no_mangle]
pub extern "C" fn start(resource_id: i32) -> i32 {
    let log_level_info: i32 = 3;
    let str = String::from("hello world");
    unsafe { ws_log(log_level_info, str.as_bytes().as_ptr(), str.len() as _) };
    return 0;
}

pub fn main() {}
```

Use cargo-wasi to build the WASM module:

```
cargo wasi build
```
{% endtab %}
{% endtabs %}

## Test Hello World!

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
  "msg": "hello world"
}
```
