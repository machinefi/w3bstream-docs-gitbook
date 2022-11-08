# Configuring W3bstream

{% hint style="info" %}
**🚧 Notice:** The settings below only apply when running w3bstream in Docker.

(local.yaml for binary in Readme)
{% endhint %}

W3bstream's configuration is included inside the **`docker-compose.yaml`** file used to start the docker images. However, the most relevant settings can be exported as environment variables, or inside a `.env` file.

## Chain Endpoint

This is the L1 blockchain W3bstream is connected to. This setting is used by any host function that interacts with the blockchain, such as `ws_send_tx.` It's also used by other w3bstream functionalities, such as the [contract event monitor](reacting-to-blockchain-events.md).

```bash
export CHAIN_ENDPOINT=https://babel-api.testnet.iotex.io
```

## W3bstream's Private Key

This is used as the account to send transactions from inside a W3bstream applet, using the `ws_send_tx` host function.

```bash
export PRIVATE_KEY=ceebc23d...918c
```
