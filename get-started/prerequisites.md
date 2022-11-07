# Prerequisites

{% hint style="info" %}
**Notice:** W3bstream is under development.&#x20;

The current documentation refers to _<mark style="color:blue;">W3bstream 1.0 Alpha</mark> release,_ and is subject to frequent changes.
{% endhint %}

This document contains the requirements and instructions to run a W3bstream node.

## Supported Blockchains

Currently, W3bstream supports the IoTeX, Ethereum, and any EVM-compatible blockchain.

## Requirements

### Tokens and Staking Requirements

Currently, there are no token balance or staking requirements to run a W3bstream node.

### Hardware requirements

Because your W3bstream node will act as a network endpoint for devices to send their data, you should run it on a serve that has a fixed IP address, publicly accessible from the Internet.

The minimum hardware requirements to run a W3bstream node are:

* 2 Cores, 2 GB RAM, 10 GB storage, 100 Mbps network

Recommended requirements to get started running a W3bstream node are:

* 4 Cores, 4 GB RAM, 20 GB storage, 100 Mbps network

{% hint style="info" %}
**Notice**

The performances and storage requirements of your node are closely related to the number of client devices, the volumes of IoT data, the data retention policy, and the complexity of the application logic. It's recommended to  accurately evaluate the hardware configuration based on the application specific requirements.
{% endhint %}

&#x20;

## Supported OS

The W3bstream runtime supports Linux and MacOS systems.&#x20;

## Blockchain client

For your W3bstream node to be able to interact with a blockchain application (e.g., react to smart contract events, send proofs of real-world events to smart contracts), you will also need access to a blockchain gateway.&#x20;

#### Use existing RPCs

You can use official gateways or third-party's gateways to access the blockchain of your choice:

{% embed url="https://docs.iotex.io/dapp-development/web3-development/rpc-endpoints" %}
List of IoTeX's RPC endpoints
{% endembed %}

{% embed url="https://ethereumnodes.com/" %}
List of Ethereum's RPC endpoints
{% endembed %}

#### Run your own blockchain gateway

If you decide to run your own gateway, it's highly recommended that you run it on a separate server, to avoid affecting W3bstream's performances. Below, you can find links to the instructions on how to run your blockchain gateway for IoTeX and Ethereum:

{% embed url="https://delegates.iotex.io/get-started/node-configuration" %}
Run an IoTeX gateway node
{% endembed %}

{% embed url="https://ethereum.org/en/run-a-node/" %}
Run an Ethereum gateway node
{% endembed %}
