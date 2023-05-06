# Getting Events Data

{% hint style="success" %}
Please check out the [hello-world](../get-started/hello-world/ "mention") section to learn how to create a basic WASM module that can be executed in W3bstream
{% endhint %}

When a data message is sent to a W3bstream project and an event route within the project matches the event specified in the message, the corresponding applet's handler function is executed by W3bstream, with the event's resource ID passed as an argument.&#x20;

The applet's handler function is responsible for processing the event's payload, which can be accessed using the `GetData` function provided by the W3bstream Applet Kit in your preferred programming language.

{% tabs %}
{% tab title="Typescript" %}
```typescript
// W3bstream functions and types
import { GetDataByRID, JSON } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";

// W3bstream handler
export function handle_data(rid: i32): i32 {
  // Get the message payload from the resource id
  let payload_string = GetDataByRID(rid);
  // Parse the payload string into a JSON object
  let payload_json = JSON.parse(payload_string) as JSON.Obj;
  
  return 0;
}
```
{% endtab %}

{% tab title="Rust" %}
<pre class="language-rust"><code class="lang-rust">use ws_sdk::log::log_info;
use ws_sdk::stream::get_data;
<strong>
</strong><strong>#[no_mangle]
</strong>pub extern "C" fn data_handler(rid: i32) -> i32 {
    // Get the message payload from the resource id
    let payload_string = String::from_utf8(get_data(rid as _)?)?;
    // Parse the payload string into a JSON object
    let payload: Value = serde_json::from_str(payload_stringn_str)?;
    return 0;
};
</code></pre>
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
	"fmt"

	"github.com/machinefi/w3bstream-wasm-golang-sdk/stream"
	"github.com/tidwall/gjson"
)

// main is required for TinyGo to compile to Wasm.
func main() {}

//export start
func _start(rid uint32) int32 {
    // Get the message payload from the resource id
    message, err := stream.GetDataByRID(rid)
    // Parse the payload string into a JSON object
    res := gjson.Parse(message);
    
    return 0
}
```
{% endtab %}
{% endtabs %}

The example below shows how to obtain the event payload and log it to the console:

{% tabs %}
{% tab title="Go" %}
```go
// go:wasm-module env
// export ws_log
func _ws_log(logLevel, ptr, size uint32) int32

// go:wasm-module env
// export ws_get_data
func _ws_get_data(rid, ptr, size uint32) int32

//export start handler
func _start(event_id uint32) int32 {
        message, err := common.GetEventData(event_id)
        Log(fmt.Sprintf("Event id %v payload: `%s`", event_is, string(message)))
	return 0
}

func BytesToPointer(v []byte) (addr, size uint32) {
	ptr := &v[0]
	pptr := uintptr(unsafe.Pointer(ptr))
	return uint32(pptr), uint32(len(v))
}

func StringToPointer(v string) (addr, size uint32) {
	return BytesToPointer([]byte(v))
}

func Log(message string) {
	ptr, size := StringToPointer(message)
	_ = _ws_log(3, ptr, size) // logInfoLevel = 3
}
```
{% endtab %}

{% tab title="Rust" %}
<pre class="language-rust"><code class="lang-rust">#[link(wasm_import_module = "env")]
<strong>extern "C" {
</strong>  fn ws_log(log_level: i32, ptr: *const u8, size: i32) -> i32;
  fn ws_get_data(event_id: i32, payload_ptr: i32, payload_size: i32) -> i32
}

#[no_mangle]
// This handler will be matched by the default Project event strategy in W3bstream
pub extern "C" fn start(event_id: i32) -> i32 {
    log_info(
        &#x26;format!("Start handler called with event_id: {}", event_id));

    let payload = get_data_as_str(event_id).unwrap();
    log_info(&#x26;format!("event data as string: {}", payload));
    return 0;
}

// Returns the event payload as a string
fn get_data_as_str(event_id: i32) -> Option&#x3C;String> {
    let data_ptr = &#x26;mut (0 as i32) as *const _ as *const *mut u8;
    let data_size = &#x26;(0 as i32);
    match unsafe { ws_get_data(event_id, data_ptr, data_size) } {
        0 => Some(unsafe { String::from_raw_parts(*data_ptr, *data_size as _, *data_size as _) }),
        _ => None,
    }
}

// Logs an info message string to the W3bstream console
fn log_info(str: &#x26;str) {
    unsafe { ws_log(3, str.as_bytes().as_ptr(), str.len() as _) };
}
</code></pre>
{% endtab %}

{% tab title="C++" %}
```
// A C++ example is coming soon
```
{% endtab %}

{% tab title="Typescript" %}
```
// Typescript support is coming soon
```
{% endtab %}
{% endtabs %}

<mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../reference/abi-functions-reference.md" %}
[abi-functions-reference.md](../reference/abi-functions-reference.md)
{% endcontent-ref %}
