# Using the Key-Value DB

The key-value storage in W3bstream is specifically designed for storing data that can be retrieved using a unique key. This functionality proves useful for various purposes, such as storing application settings and maintaining status information.

To store an object called "`myObj`" in the key-value database, a W3bstream applet can utilize the `SetDB` function.&#x20;

The example below demonstrates how you can store and retrieve an integer value from the key-value storage:

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { GetDB, SetDB } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";

export function my_habdler(rid: i32): i32 {
  
  let value = GetDB("users_count");

  let users_count = value ? parseInt(value) : 0;

  let result = SetDB("users_count", (i32(users_count) + 1));

  return 0;
}
```
{% endtab %}

{% tab title="Rust" %}
```rust
use ws_sdk::database::kv::{get, set};
use ws_sdk::log::log_info;

#[no_mangle]
pub extern "C" fn my_handler(_rid: i32) -> i32 {
    // Read the data stored under the key "users_count"
    let value = get("users_count").unwrap_or("0".into());
    // Convert the value to string and parse it to i32
    let int_value = String::from_utf8(value).unwrap().parse::<i32>().unwrap();
    // Log the value
    log_info(&format!("Current users count: {}", int_value));
    // Increment and store the incremented the value
    let result = set("users_count", (int_value + 1).to_string().into_bytes());

    0
}

// Add a main() if required by the compiler
fn main() { }

```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
	"fmt"

	"github.com/machinefi/w3bstream-wasm-golang-sdk/database"
	"github.com/machinefi/w3bstream-wasm-golang-sdk/log"
)

func my_handle(rid int32) int32 {
	value, _ := database.Get("users_count")

	usersCount, _ := strconv.Atoi(string(value))

	w3bstream.Set("users_count", []byte(strconv.Itoa(usersCount+1)))

	return 0
}

func main() {}

```
{% endtab %}
{% endtabs %}
