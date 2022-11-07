# Sending blockchain actions

{% hint style="info" %}
**This functionality needs a host private key to be set in the** [**W3bstream configuration**](configuring-w3bstream.md)****
{% endhint %}

An applet can send any blockchain action using the `ws_send_tx` function provided by W3nstream.

## Send a transfer

The example below shows how to send a native token transfer from the W3bstream host account:

{% tabs %}
{% tab title="Rust" %}
```rust
#[link(wasm_import_module = "env")] 
extern "C" { 
    fn ws_send_tx(ptr: *const u8, size: i32) -> i32;
}

#[no_mangle]
pub extern "C" fn start(event_id: i32) -> i32 {
 
  let tx = #r"{
              to: "0x46fF054D4275A4aB9d42179C3bcA59f938e658C8",
              value: "110",
              data: "",
            }"#,
    
    match unsafe { ws_send_tx(tx.as_ptr(), tx.len() as _) } {
        0 => Ok(()),
        _ => bail!("Error while sending the transaction"),
    }
}
```
{% endtab %}
{% endtabs %}

## Execute a contract function

It's also possible to use `ws_send_tx` to execute a smart contract function by encoding the call inside the transaction payload. The example below shows  an example:

```rust
#[link(wasm_import_module = "env")] 
extern "C" { 
    fn ws_send_tx(ptr: *const u8, size: i32) -> i32;
}

#[no_mangle]
pub extern "C" fn start(event_id: i32) -> i32 {
  let tx = 
    r#"{
       // The recipient is supposed to be a smart contract address
       "to": "0xb73eE6EB5b1984c78CCcC49eA7Ad773E71d74F51",
	"value": "0",
	// The payload encodes a smart contract function call
	"data": "40c10f190000000000000000000000000x4c123380CA640a146D803f844E0D9c90b52C5C970000000000000000000000000000000000000000000000000de0b6b3a7640000"
    }"#;
  
    unsafe { ws_send_tx(tx.as_ptr(), tx.len() as _) };

    return 0;
}
```
