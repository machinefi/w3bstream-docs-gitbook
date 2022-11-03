---
description: >-
  fn ws_get_db(key_ptr: *const u8, key_size: i32, return_ptr: *const *mut u8,
  return_size: *const i32) -> i32;
---

# Querying Stored Data



{% hint style="info" %}
**Notice:** W3bstream Alpha release only includes a storage interface implementation in the form of a simple _key-value_ database. Later releases of W3bstream will provide further storage options, both centralized and decentralized.
{% endhint %}

A W3bstream applet can read an object from the key-value host storage using the `ws_get_db` W3bstream function. As any other W3bstream exported functions, it must be imported before it can be used in an applet:

{% tabs %}
{% tab title="Rust" %}
```rust
#[link(wasm_import_module = "env")] 
extern "C" { 
fn ws_get_db(
        key_ptr: *const u8,
        key_size: i32,
        return_ptr: *const *mut u8,
        return_size: *const i32,
    ) -> i32;
}
```
{% endtab %}
{% endtabs %}

The example below shows how you can read a string from the key/value storage:

```rust
#[link(wasm_import_module = "env")] 
extern "C" { 
 fn ws_set_db(key_ptr: *const u8, key_size: i32, value_ptr: *const u8, value_size: i32) -> i32;
}

#[no_mangle]
// This handler will be matched by the default Project event strategy in W3bstream
pub extern "C" fn start(event_id: i32) -> i32 {
    // Storing some strings in the key/value storage
    let first_name = get_db("first_name");
    let last_name = get_db("last_name");
    let age = get_db("age");

    return 0;
}

pub fn get_db(key: &String) -> Option<String> {
    let data_ptr = &mut (0 as i32) as *const _ as *const *mut u8;
    let data_size = &(0 as i32);
    match unsafe { ws_get_db(key.as_ptr(), key.len() as _, data_ptr, data_size) } {
        0 => Some(unsafe { String::from_raw_parts(*data_ptr, *data_size as _, *data_size as _) }),
        _ => None,
    }
}
```

<mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="abi-functions-reference.md" %}
[abi-functions-reference.md](abi-functions-reference.md)
{% endcontent-ref %}
