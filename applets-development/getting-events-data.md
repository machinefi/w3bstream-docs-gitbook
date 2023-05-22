# Receiving data

When a data message is sent to a W3bstream Project, W3bstream checks if there's an event route that matches the `event_type` specified in the message. If there's a match, W3bstream executes the corresponding applet's handler function and passes the event's resource ID as an argument. The applet's handler function is responsible for processing the event's payload.

To access the payload, you can use the `GetData` function provided by the W3bstream Applet Kit in your preferred programming language. The following example demonstrates how to obtain the event payload, parse it as a JSON object, and log it to the console:

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
// W3bstream functions and types
import { GetDataByRID, JSON, Log } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";

// W3bstream handler
export function handle_data(rid: i32): i32 {
  // Get the message payload from the resource id
  let payload_string = GetDataByRID(rid);
  // Parse the payload string into a JSON object
  let payload_json = JSON.parse(payload_string) as JSON.Obj;
  // Log to the console
  Log("Received message: " + payload_string);
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
    // Log to the console
    log_info(&#x26;format!("Received message: `{}`", payload_string))?;
    return 0;
};
</code></pre>
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
	"fmt"
        "github.com/machinefi/w3bstream-wasm-golang-sdk/log"
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
    // Log to the console
    message_string := string(message)
    log.Log("Message received: " + message_string)
    return 0
}
```
{% endtab %}
{% endtabs %}
