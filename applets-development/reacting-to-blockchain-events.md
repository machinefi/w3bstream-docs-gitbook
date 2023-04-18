# Reacting to blockchain events

Thanks to W3bstream blockchain monitoring capabilities, it's very easy to run specific logics when an event is emitted by a smart contract, or when something else happens on a blockchain.

This document describes the different options to monitor and react to blockchain events.

{% hint style="success" %}
Make sure you have correctly [configured the blockchain endpoint](configuring-w3bstream.md#chain-endpoint) before createing blockchain monitors.
{% endhint %}

## Smart Contract Event Monitor&#x20;

This is an internal W3bstream module that can emit W3bstream events when a certain blockchain event is emitted by a smart contract.&#x20;

Learn how to create a Smart Contract Monitor:

{% content-ref url="../get-started/w3bstream-studio/monitoring-smart-contracts.md" %}
[monitoring-smart-contracts.md](../get-started/w3bstream-studio/monitoring-smart-contracts.md)
{% endcontent-ref %}

## Blockchain Height Monitor

This is an internal W3bstream module that can emit a W3bstream event when a certain height is reached on the blockchain.

Learn how to create a Blockchain Height Monitor:

{% content-ref url="../get-started/w3bstream-studio/monitoring-blockchain-height.md" %}
[monitoring-blockchain-height.md](../get-started/w3bstream-studio/monitoring-blockchain-height.md)
{% endcontent-ref %}

&#x20;
