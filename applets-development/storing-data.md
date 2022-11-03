---
description: >-
  fn ws_set_db(key_ptr: *const u8, key_size: i32, value_ptr: *const u8,
  value_size: i32) -> i32;
---

# Storing Data

{% hint style="info" %}
**Notice:** W3bstream Alpha release only includes a storage interface implementation in the form of a simple _key-value_ database. Later releases of W3bstream will provide further storage options, both centralized and decentralized.
{% endhint %}

A W3bstream applet can store an object in the key-value host storage using the `ws_set_db` W3bstream function. As any other W3bstream exported functions, it must be imported before it can be used in an applet:

{% tabs %}
{% tab title="Rust" %}
```rust
#[link(wasm_import_module = "env")] 
extern "C" { 
 fn ws_set_db(
     key_ptr: *const u8, 
     key_size: i32, 
     value_ptr: *const u8, 
     value_size: i32) 
     -> i32;
}
```
{% endtab %}
{% endtabs %}

The example below shows how you can store a string in the key-value storage:

<pre class="language-rust"><code class="lang-rust">#[link(wasm_import_module = "env")] 
extern "C" { 
 fn ws_set_db(key_ptr: *const u8, key_size: i32, value_ptr: *const u8, value_size: i32) -> i32;
}

#[no_mangle]
// This handler will be matched by the default Project event strategy in W3bstream
pub extern "C" fn start(event_id: i32) -> i32 {
    // Storing some strings in the key-value storage
    set_db("first_name","Vitalik");
    set_db("last_name","Buterin");
    set_db("age","23");
    return 0;
}
<strong>
</strong><strong>pub fn set_db(key: &#x26;String, value: String) -> Result&#x3C;()> { 
</strong>  match unsafe { 
    ws_set_db( 
      key.as_ptr(), 
      key.len() as _, 
      value.as_ptr(), 
      value.len() as _, ) 
    } { 
        0 => Ok(()), 
        _ => bail!("Error while storing the value"), 
      } 
}</code></pre>

<mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="abi-functions-reference.md" %}
[abi-functions-reference.md](abi-functions-reference.md)
{% endcontent-ref %}
