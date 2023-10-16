# Interacting with blockchain

In W3bstream, Applets have the powerful ability to interact with blockchains using the `POST /system/send_tx` function provided by the [Applet Kit of your language of choice](w3bstream-applet-kits/). This functionality enables developers to send raw transactions to any supported blockchain.

By utilizing the `POST /system/send_tx` function, developers can specify essential details such as the chain ID, destination address, value, and encoded transaction data. This allows for various types of interactions with blockchains, including native token transfers, ERC20 transfers, and general smart contract interactions.

With this feature, Applets in W3bstream gain the capability to seamlessly integrate with different blockchains and perform a wide range of blockchain operations, interacting with the logic of your DePIN application to mint token rewards or execute custom transactions.

In the following sections, we will explore in detail how to utilize the `POST /system/send_tx` function and demonstrate its usage with various blockchain examples.

## The supported blockchains

| chainName | chainID |
| --------- | ------- |
| iotex-mainnet | 4689 |
| iotex-testnet | 4690 |
| ethereum-mainnet | 1 |
| goerli | 5 |
| polygon-mainnet | 137 |
| mumbai | 80001 |
| arbitrum-goerli | 421613 |
| arbitrum-one | 42161 |
| op-goerli | 420 |
| op-mainnet | 10 |
| base-goerli | 84531 |
| base-mainnet | 8453 |
| solana-devnet | |
| solana-testnet | |
| solana-mainnet-beta | |

## The supported SDK

| programming language | Supported API  | address |
| --------- | ------- | ------- |
| AssemblyScript | /system/read_tx<br> /system/send_tx | https://github.com/machinefi/w3bstream-wasm-assemblyscript-sdk |
| Go | /system/read_tx<br> /system/send_tx | https://github.com/machinefi/w3bstream-wasm-golang-sdk |
| Rust |  | https://github.com/machinefi/w3bstream-wasm-rust-sdk |

## The Operator Address

When you deploy a W3bstream Project from your Metamask account, a blockchain account called the "Operator Account" is automatically generated and assigned to your project. The operator account is managed by W3bstream, and plays a significant role, authorizing transactions sent from your projects.

{% hint style="info" %}
This process enables smart contracts to uniquely identify and trust the sender as the authorized W3bstream project, supposed to provide proofs to the blockchain layer of the DePIN application.
{% endhint %}

To access the address of your operator account, simply navigate to the Settings section of your Projects. There, you will find the specific address associated with your operator account. This information is essential for verifying the origin of transactions and maintaining the integrity of your project's interactions with the blockchain.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Please ensure that your W3bstream operator address is funded with the native token of the respective blockchain networks to enable successful transaction sending for your projects.**
{% endhint %}

## Sending native token transfers

The following example demonstrates how to send a native token transfer from your applet:  
First, need create a event routing on W3bstream Studio
<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (3).png" alt=""><figcaption></figcaption></figure>
The `start` function will called sync, and get a `transactionID`, and the `handle_result` function will called async, and get the transaction state  

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { GetDataByRID, JSON, JSONEncoder, Log, ApiCall } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";
import { encode, decode } from "as-base64/assembly/index";
import { utf8ArrayToString } from "@w3bstream/wasm-sdk/assembly/utility"
export function start(rid: i32): i32 {
  const message = GetDataByRID(rid);
  let bodyEncode = new JSONEncoder();
  bodyEncode.pushObject("");
  bodyEncode.setString('chainName', "iotex-testnet");
  bodyEncode.setString('operatorName', 'default');
  bodyEncode.setString('to', '0x9117f5EF4156709092f79740a97b1638cA399A00');
  bodyEncode.setString('value', '10000000000000000000');
  //send native token to address
  bodyEncode.setString('data', `0x`);
  bodyEncode.popObject();
  let encoder = new JSONEncoder();
  encoder.pushObject("");
  encoder.setString('Method', 'POST');
  encoder.setString('Url', 'w3bstream://w3bstream.com/system/send_tx');
  encoder.pushObject("Header");
  encoder.pushArray("Eventtype");
  encoder.setString("", "result");
  encoder.popArray();
  encoder.popObject();
  encoder.setString("Body", encode(bodyEncode.serialize()))
  encoder.popObject();
  Log('encoder:' + encoder.toString())
  let data = ApiCall(encoder.toString())
  Log(data)
  return 0;
}

export function handle_result(rid: i32): i32 {
  Log("handle_result");
  const message = GetDataByRID(rid);
  let messageJSON: JSON.Obj = JSON.parse(
    message
  ) as JSON.Obj;
  let body_base64: JSON.Str | null = messageJSON.getString("Body") as JSON.Str;
  if (body_base64) {
    let body = decode(body_base64.toString());
    let bodyString = utf8ArrayToString(body);
    Log("res:" + bodyString);
  }
  return 0;
}
```
{% endtab %}
{% endtabs %}

## Executing smart contract functions

It's also possible to use `POST /system/send_tx` to execute a smart contract function by providing the encoded transaction payload. The following example demonstrates this:  
First, need create a event routing on W3bstream Studio
<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (3).png" alt=""><figcaption></figcaption></figure>
The `start` function will called sync, and get a `transactionID`, and the `handle_result` function will called async, and get the transaction state  

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { GetDataByRID, JSON, JSONEncoder, Log, ApiCall } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";
import { encode, decode } from "as-base64/assembly/index";
import { utf8ArrayToString } from "@w3bstream/wasm-sdk/assembly/utility"

export function start(rid: i32): i32 {
  const message = GetDataByRID(rid);
  let bodyEncode = new JSONEncoder();
  bodyEncode.pushObject("");
  bodyEncode.setString('chainName', "iotex-testnet");
  bodyEncode.setString('operatorName', 'default');
  bodyEncode.setString('to', '0x659A60915F5f758A7886Fd2074f31B17Aa418B4c');
  bodyEncode.setString('value', '0');
  //Approve erc20 
  //need to send Operator Address gas fee
  bodyEncode.setString('data', `0x095ea7b3000000000000000000000000610cbda6f0037b4141a5b949f56479106becb1e900000000000000000000000000000000000000000000000000000000000186a0`);

  bodyEncode.popObject();

  let encoder = new JSONEncoder();
  encoder.pushObject("");
  encoder.setString('Method', 'POST');
  encoder.setString('Url', 'w3bstream://w3bstream.com/system/send_tx');
  encoder.pushObject("Header");
  encoder.pushArray("Eventtype");
  encoder.setString("", "result");
  encoder.popArray();
  encoder.popObject();
  encoder.setString("Body", encode(bodyEncode.serialize()))
  encoder.popObject();

  Log('encoder:' + encoder.toString())
  // > '{"Method":"GET","Url":"w3bstream://w3bstream.com/system/read_tx","Header":{"Eventtype":["result"]},"Body":"eyJjaGFpbklEIjogNDY5MCwiaGFzaCI6ICJmY2FmMzc3ZmYzY2M3ODVkNjBjNThkZTdlMTIxZDZhMmU3OWUxYzU4YzE4OWVhODY0MWYzZWE2MWY3NjA1Mjg1In0="}'
  let data = ApiCall(encoder.toString())
  Log(data)
  return 0;
}

export function handle_result(rid: i32): i32 {
  Log("handle_result");
  const message = GetDataByRID(rid);
  let messageJSON: JSON.Obj = JSON.parse(
    message
  ) as JSON.Obj;
  let body_base64: JSON.Str | null = messageJSON.getString("Body") as JSON.Str;
  if (body_base64) {
    let body = decode(body_base64.toString());
    let bodyString = utf8ArrayToString(body);
    Log("res:" + bodyString);
  }

  return 0;
}
```
{% endtab %}

{% tab title="Go" %}
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

## Reading Transaction

The `GET /system/read_tx` function in W3bstream allows you to read a transaction information. The following example demonstrates how this works:  
First, need create a event routing on W3bstream Studio
<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (3).png" alt=""><figcaption></figcaption></figure>
The `start` function will called sync. And the `handle_result` function will called async to get the transaction information  

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { GetDataByRID, JSON, JSONEncoder, Log, ApiCall } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";
import { encode, decode } from "as-base64/assembly/index";
import { utf8ArrayToString } from "@w3bstream/wasm-sdk/assembly/utility"

export function start(rid: i32): i32 {
  const message = GetDataByRID(rid);
  let bodyEncode = new JSONEncoder();
  bodyEncode.pushObject("");
  bodyEncode.setString('chainName', "iotex-testnet");
  bodyEncode.setString('hash', 'fcaf377ff3cc785d60c58de7e121d6a2e79e1c58c189ea8641f3ea61f7605285');
  bodyEncode.popObject();

  let encoder = new JSONEncoder();
  encoder.pushObject("");
  encoder.setString('Method', 'GET');
  encoder.setString('Url', 'w3bstream://w3bstream.com/system/read_tx');
  encoder.pushObject("Header");
  encoder.pushArray("Eventtype");
  encoder.setString("", "result");
  encoder.popArray();
  encoder.popObject();
  encoder.setString("Body", encode(bodyEncode.serialize()))
  encoder.popObject();

  Log('encoder:' + encoder.toString())
  // > '{"Method":"GET","Url":"w3bstream://w3bstream.com/system/read_tx","Header":{"Eventtype":["result"]},"Body":"eyJjaGFpbklEIjogNDY5MCwiaGFzaCI6ICJmY2FmMzc3ZmYzY2M3ODVkNjBjNThkZTdlMTIxZDZhMmU3OWUxYzU4YzE4OWVhODY0MWYzZWE2MWY3NjA1Mjg1In0="}'
  let data = ApiCall(encoder.toString())
  Log(data)
  return 0;
}

export function handle_result(rid: i32): i32 {
  Log("handle_result");
  const message = GetDataByRID(rid);
  let messageJSON: JSON.Obj = JSON.parse(
    message
  ) as JSON.Obj;
  let body_base64: JSON.Str | null = messageJSON.getString("Body") as JSON.Str;
  if (body_base64) {
    let body = decode(body_base64.toString());
    let bodyString = utf8ArrayToString(body);
    Log("res:" + bodyString);
  }
  return 0;
}
```
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
	"bytes"
	"fmt"
	"io"
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
	data := `{"chainName": "iotex-testnet","hash": "fcaf377ff3cc785d60c58de7e121d6a2e79e1c58c189ea8641f3ea61f7605285"}`

	req, err := http.NewRequest("GET", "/system/read_tx", strings.NewReader(data))
	if err != nil {
		return -1
	}
	req.Header.Set("eventType", "result")

	resp, err := api.Call(req)
	if err != nil {
		return -1
	}

	var buf bytes.Buffer
	if err := resp.Write(&buf); err != nil {
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
