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
use anyhow::Result;
use ws_sdk::database::kv::*;

#[no_mangle]
pub extern "C" fn my_handler(rid: i32) -> i32 {
    let value = match get("users_count") {
        Ok(data) => String::from_utf8_lossy(&data).to_string(),
        Err(_) => String::new(),
    };

    let users_count = value.parse::<i32>().unwrap_or(0);

    let result = set("users_count", (users_count + 1).to_string().into_bytes());

    0
}


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
