# Interacting with blockchain

In W3bstream, Applets have the powerful ability to interact with blockchains using the `SendTx` function provided by the [Applet Kit of your language of choice](w3bstream-applet-kits/). This functionality enables developers to send raw transactions to any supported blockchain.

By utilizing the `SendTx` function, developers can specify essential details such as the chain ID, destination address, value, and encoded transaction data. This allows for various types of interactions with blockchains, including native token transfers, ERC20 transfers, and general smart contract interactions.

With this feature, Applets in W3bstream gain the capability to seamlessly integrate with different blockchains and perform a wide range of blockchain operations, interacting with the logic of your DePIN application to mint token rewards or execute custom transactions.

In the following sections, we will explore in detail how to utilize the `SendTx` function and demonstrate its usage with various blockchain examples.

## The Operator Address

When you deploy a W3bstream Project from your Metamask account, a blockchain account called the "Operator Account" is automatically generated and assigned to your project. The operator account is managed by W3bstream, and plays a significant role, authorizing transactions sent from your projects.

{% hint style="info" %}
This process enables smart contracts to uniquely identify and trust the sender as the authorized W3bstream project, supposed to provide proofs to the blockchain layer of the DePIN application.
{% endhint %}

To access the address of your operator account, simply navigate to the Settings section of your Projects. There, you will find the specific address associated with your operator account. This information is essential for verifying the origin of transactions and maintaining the integrity of your project's interactions with the blockchain.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Please ensure that your W3bstream operator address is funded with the native token of the respective blockchain networks to enable successful transaction sending for your projects.**
{% endhint %}

## Sending native token transfers

The following example demonstrates how to send a native token transfer from your applet:

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { Log, SendTx } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";

const RECIPIENT_ADDRESS = `0x9117f5EF4156709092f79740a97b1638cA399A00`;
  
export function start(rid: i32): i32 {
  // Send 10 IOTX from the opeartor account
  const hash = SendTx(4690, RECIPIENT_ADDRESS, "10", "");
  Log("Tx Hash: " + hash);
  return 0;
}
```
{% endtab %}
{% endtabs %}

## Executing smart contract functions

It's also possible to use `SendTx` to execute a smart contract function by providing the encoded  transaction payload. The following example demonstrates this:

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { SendTx, Log } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";

export function my_handler(rid: i32): i32 {
  const ContractAddress = `0xb73eE6EB5b1984c78CCcC49eA7Ad773E71d74F51`;
  const Hash = SendTx(
    4690,
    ContractAddress,
    "0",
    `40c10f1900000000000000000000000000000000000000000000000000000000000f4240`
  );
  Log("Transaction Hash" + Hash);
  return 0;
}
```
{% endtab %}

{% tab title="Rust" %}
```rust
use ws_sdk::blockchain::*;
use ws_sdk::log::log_info;

pub extern "C" fn start(rid: i32) -> i32 {
    const CONTRACT_ADDR = `0xb73eE6EB5b1984c78CCcC49eA7Ad773E71d74F51`;
    const hash = send_tx(
        4690, 
        CONTRACT_ADDR, 
        "0",
        "40c10f1900000000000000000000000000000000000000000000000000000000000f4240")?;

    log_info(&format!("Transaction hash: {}, hash))?;

    return 0;
}
```
{% endtab %}

{% tab title="Rust" %}
```go
package main

import (
	"bytes"
	"fmt"
	"io"
	"math/big"
	"net/http"
	"strings"

	"github.com/machinefi/w3bstream-wasm-golang-sdk/api"
	"github.com/machinefi/w3bstream-wasm-golang-sdk/common"
	"github.com/machinefi/w3bstream-wasm-golang-sdk/log"
	"github.com/machinefi/w3bstream-wasm-golang-sdk/stream"
)

func main() {}

//export start
func _start(rid uint32) int32 {
	value := big.NewInt(0)
	valueStr := value.String()
	data := fmt.Sprintf(`{"chainName": "iotex-testnet","operatorName": "default","to": "0x1ED83F5AD999262eC06Ed8f3B801e108024b3e9c","value": "%s","data": "40c10f19000000000000000000000000%s0000000000000000000000000000000000000000000000000de0b6b3a7640000"}`, valueStr, "97186a21fa8e7955c0f154f960d588c3aca44f14")

	req, err := http.NewRequest("POST", "/system/send_tx", strings.NewReader(data))
	if err != nil {
		log.Log(err.Error())
		return -1
	}
	req.Header.Set("eventType", "result")

	resp, err := api.Call(req)
	if err != nil {
		log.Log(err.Error())
		return -1
	}

	var buf bytes.Buffer
	if err := resp.Write(&buf); err != nil {
		log.Log(err.Error())
		return -1
	}

	log.Log(string(buf.Bytes()))

	return 0
}

//export handle_result
func _handle_result(rid uint32) int32 {
	log.Log(fmt.Sprintf("start rid: %d", rid))

	message, err := stream.GetDataByRID(rid)
	if err != nil {
		log.Log(err.Error())
		return -1
	}

	defer func() {
		if common.FreeResource(rid) {
			log.Log(fmt.Sprintf("resource %v released", rid))
		}
	}()

	resp, err := api.ConvResponse(message)
	if err != nil {
		log.Log(err.Error())
		return -1
	}
	body, err := io.ReadAll(resp.Body)
	if err != nil {
		log.Log(err.Error())
		return -1
	}

	log.Log(fmt.Sprintf("get result: %v, status: %v, information: %v", rid, resp.Status, string(body)))
	return 0
}
```
{% endtab %}

{% endtabs %}

## Reading smart contracts

The `CallContract` function in W3bstream allows you to call smart contract _view_ or _pure_ functions and read the return value. The following example demonstrates how this works:

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { CallContract, GetDataByRID, Log, SendTx } from "@w3bstream/wasm-sdk";
import { hexToAddress, hexToBool, hexToUtf8 } from "@w3bstream/wasm-sdk/assembly/utility";

export { alloc } from "@w3bstream/wasm-sdk";

export function stmy_handler(rid: i32): i32 {
  const ERC20Addr = "0xa00744882684c3e4747faefd68d283ea44099d03";
  const BalanceOfHex = CallContract(4690, ERC20Addr, `0x70a082310000000000000000000000009117f5ef4156709092f79740a97b1638ca399a00`);

  Log("ERC20 Balance of address is:" + parseInt(balanceOfHex, 16).toString());

  const SymbolHex = CallContract(4689, ERC20Addr, `0x95d89b41`);
  Log("Token Symbol is:" + hexToUtf8(symbolHex));
  
  return 0;
}
```
{% endtab %}
{% endtabs %}
