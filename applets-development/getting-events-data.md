---
description: fn ws_get_data(event_id i32, payload_ptr i32, payload_size i32) -> i32
---

# Getting Events Data

{% hint style="success" %}
Please check out the [hello-world.md](hello-world.md "mention") section to learn how to create a basic WASM module that can be executed in W3bstream
{% endhint %}

When a W3bstream event matches a Project [_event strategy_](../get-started/w3bstream-studio/creating-strategies.md), the respective applet's handler is called and the event ID is passed as an argument.

Inside an applet, you can access the event's payload using the `ws_get_data` W3bstream function. It is exported by the W3bstream WebAssembly VM and must be imported into your applet before it can be used:

{% tabs %}
{% tab title="Go" %}
```go
// go:wasm-module env
// export ws_get_data
func _ws_get_data(rid, ptr, size uint32) int32

// You may refer to https://github.com/machinefi/w3bstream/blob/main/_examples/wasm_common_go/imports.go#L38, or use the `GetDataByRID` defined in wasm_common_go to fetch event's payload.
```
{% endtab %}

{% tab title="Rust" %}
<pre class="language-rust"><code class="lang-rust">#[link(wasm_import_module = "env")]
<strong>extern "C" {
</strong>  fn ws_get_data(event_id: i32, payload_ptr: i32, payload_size: i32) -> i32
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

{% content-ref url="abi-functions-reference.md" %}
[abi-functions-reference.md](abi-functions-reference.md)
{% endcontent-ref %}
