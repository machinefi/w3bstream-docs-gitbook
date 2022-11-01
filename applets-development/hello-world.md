# Hello World!

{% hint style="info" %}
**Notice:** W3bstream is under development.&#x20;

The current documentation refers to _W3bstream 1.0 Alpha release,_ and is subject to frequent changes.Prerequisites
{% endhint %}

A W3bstream applet is supposed to contain event handlers associated to the various events supported by the W3bstream runtime. <mark style="background-color:red;">(TODO: Document WS events).</mark> When creating a W3bstream applet in the language of your choice, you will have to follow a few simple rules:

#### Memory allocation

You need to declare an implementation of the `malloc` function for the WebAssembly machine to be able to allocate memory in the host. This depends on the programming language you are using:

{% tabs %}
{% tab title="Golang" %}
In Rust you don't need to provide a malloc implementation as it's automatically added by the tiniGo compiler
{% endtab %}

{% tab title="C/C++" %}
In C you are supposed to provide an implementation of malloc and make sure it's exported:

```cpp
EMSCRIPTEN_KEEPALIVE uint32_t malloc(uint32_t size) { return malloc(size); } 
```
{% endtab %}

{% tab title="Rust" %}
In Rust you don't need to provide a malloc implementation as it's automatically added by the  compiler
{% endtab %}
{% endtabs %}

#### The start function

It's assumed that you have at least one event handler defined in your applet. This handler should be linked to a W3bstream event in the node configuration (<mark style="background-color:red;">TODO: document and add link to project configuration</mark>). However, if you have not configured any event handler for your W3bstream project (<mark style="background-color:red;">TODO: introduce the concept of "projects" before</mark>) W3bstream expects you included a `_start()` function to serve as a default event handler, with the following signature:

{% tabs %}
{% tab title="Golang" %}
```go
func _start(rid uint32) int32
```
{% endtab %}

{% tab title="C/C++" %}
```cpp
EMSCRIPTEN_KEEPALIVE uint32_t _start(uint32_t resId = 0)
```
{% endtab %}

{% tab title="Rust" %}
```rust
func _start(rid uint32) int32uThe log function
```
{% endtab %}
{% endtabs %}

W3bstream provides applets with a text console to output text to. Since WebAssembly is independent of the availability of a console on the host, you will have to declare a `_log()` function that is exported by W3bstream and gives you access to the console.&#x20;

So if you want to access the W3bstream console in your applet, you must declare this `_log()` function as an _`extern`_ function in your code:

{% tabs %}
{% tab title="Golang" %}
```go
func _log(ptr uint32, size uint32)
```
{% endtab %}

{% tab title="C/C++" %}
<pre class="language-c"><code class="lang-c"><strong>extern void _log(const char* msg, uint32_t size);</strong></code></pre>
{% endtab %}

{% tab title="Rust" %}
<mark style="background-color:red;">TODO</mark>
{% endtab %}
{% endtabs %}

Where `msg` is a pointer to the string you want to output, and `size` is the size in bytes of the string.

### Hello World!

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

func _log(ptr uint32, size uint32)

func _start(rid uint32) int32 {
  	ptr, size := stringToPtr(message)
  	_log(ptr, size)
  	return 0
}

func stringToPtr(s string) (uint32, uint32) {
	buf := []byte(s)
	ptr := &buf[0]
	unsafePtr := uintptr(unsafe.Pointer(ptr))
	return uint32(unsafePtr), uint32(len(buf))
}

```

Use the TiniGo compiler to build this module:

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

extern EM_IMPORT(log) void _log(int, int);

EMSCRIPTEN_KEEPALIVE int start(int)
{
    char str[] = "Hello IoTeX!";
    _log((int)str, strlen(str));
    return 0;
}

EMSCRIPTEN_KEEPALIVE int malloc(int size)
{
    return malloc(size);
}
```



Use the emscripten compiler to build this module:

```bash
emcc -o helloworld.wasm -O2 --no-entry -s LLD_REPORT_UNDEFINED -s ERROR_ON_UNDEFINED_SYMBOLS=0 helloworld2.c
```
{% endtab %}

{% tab title="Rust" %}
```rust
#[link(wasm_import_module = "env")]
extern "C" {
    fn log(ptr: *const u8, size: i32);
}

#[no_mangle]
pub extern "C" fn start(resource_id: i32) -> i32 {
    let str = String::from("hello world");
    unsafe { log(str.as_bytes().as_ptr(), str.len() as _) };
    return 0;
}
```

Use cargo-wasi to build the module:

```
cargo wasi build
```
{% endtab %}
{% endtabs %}
