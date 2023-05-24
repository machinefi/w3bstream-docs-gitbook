# Interact with blockchain

In W3bstream, Applets have the powerful ability to interact with blockchains using the `SendTx` function provided by the [Applet Kit of your language of choice](w3bstream-applet-kits/). This functionality enables developers to send raw transactions to any supported blockchain.

By utilizing the `SendTx` function, developers can specify essential details such as the chain ID, destination address, value, and encoded transaction data. This allows for various types of interactions with blockchains, including native token transfers, ERC20 transfers, and general smart contract interactions.

With this feature, Applets in W3bstream gain the capability to seamlessly integrate with different blockchains and perform a wide range of blockchain operations, interacting with the logic of your DePIN application to mint token rewards or execute custom transactions.

In the following sections, we will explore in detail how to utilize the `SendTx` function and demonstrate its usage with various blockchain examples.

## The Operator Address

When you deploy your first W3bstream Project from your Metamask account, a blockchain account called the "Operator Account" is automatically generated and associated with your login account. The operator account, managed by W3bstream, plays a significant role authorizing transactions sent from your projects.

This process enables smart contracts to uniquely identify and trust the sender as the authorized W3bstream project, supposed to provide proofs to the blockchain layer of the DePIN application.



To access the address of your operator account, simply navigate to the Settings section of your Projects. There, you will find the specific address associated with your operator account. This information is essential for verifying the origin of transactions and maintaining the integrity of your project's interactions with the blockchain.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Please ensure that your W3bstream operator address is funded with the native token of the respective blockchain networks to enable successful transaction sending for your projects.**
{% endhint %}

## Send native token transfers

The following example demonstrates how to send a native token transfer from your applet:

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { Log, SendTx } from "@w3bstream/wasm-sdk";
export { alloc } from "@w3bstream/wasm-sdk";

export function start(rid: i32): i32 {
  const RecipientAddress = `9117f5EF4156709092f79740a97b1638cA399A00`;
  const res = SendTx(4690, RecipientAddress, "10", "");
  Log("wasm send tx result:" + res);
  return 0;
}p
```
{% endtab %}
{% endtabs %}

## Execute smart contract functions

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
}m
```
{% endtab %}
{% endtabs %}
