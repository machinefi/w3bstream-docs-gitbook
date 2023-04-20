# Monitoring Blockchain Height

The **Blockchain Height Monitor** is designed to trigger a W3bstream event when a specific block height is reached on the monitored chain. This can be particularly advantageous, for example, in the context of an Initial Coin Offering (ICO), where early users may be rewarded with tokens based on their off-chain data, starting at a designated block height.

To configure the monitor, you will need to provide three parameters:

1. **Event Type**: This represents the name of the W3bstream event that will be emitted upon reaching the desired block height.
2. **Chain ID**: This unique identifier corresponds to the blockchain on which the contract being monitored resides. Currently, the monitor exclusively supports the IoTeX Testnet, featuring a Chain ID of 4690.
3. **Height**: This value specifies the block height that, once reached, will trigger the W3bstream event.

{% embed url="https://youtu.be/dl8TpeOlHQE" %}
