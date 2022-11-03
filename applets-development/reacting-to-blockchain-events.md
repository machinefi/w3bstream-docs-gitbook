# Reacting to blockchain events

{% hint style="info" %}
**🚧 This document is a work in progress**
{% endhint %}

## Blockchain Monitor

Thanks to W3bstream blockchain monitoring capabilities, it's very easy to run specific logics when an event is emitted by a smart contract, or when something else happens on chain.\
This document describes the different options to monitor and react to blockchain events.

## Smart Contract Event Monitor&#x20;

This is an internal W3bstream module that can emit W3bstream events when a certain blockchain event is emitted by a smart contract. You can use W3bstream Studio to configure a monitor for each smart contract event you are interested in:

&#x20;<img src="../.gitbook/assets/image (26).png" alt="" data-size="original">

* `Project Id` is the recipient project for the W3bstream event &#x20;
* `eventType` is the event code that matches your [Project strategy](reacting-to-blockchain-events.md#event-strategies) for this event
* `chainID` the chain ID of the network where the contract is deployed. This depends on the actual chain endpoint set for [SRV\_APPLET\_MGR\_\_ETHCLIENTCONFIG\_\_ChainEndpoint](configuring-w3bstream.md). If you are using an IoTeX endpoint, then  you can set 4690 for the IoTeX Testnet, 4689 for the IoTeX Mainnet.
* `contractAddress` is the actual address of the contract you want to monitor
* `Block Start` the height when the monitor should start indexing the contract (it's usually the contract's deployment height)
* `Block End` the height when the monitor should stop indexing the contract (i.e. stop monitoring the smart contract event)
* `topic0` with the topic of the smart contract event that you want to detect
