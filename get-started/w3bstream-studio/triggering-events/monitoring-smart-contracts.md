# Monitoring Smart Contracts

The **Smart Contract Monitor** needs some parameters to work, and it allows you to trigger a W3bstream event when a certain on-chain condition is met, e.g. an event is triggered in the smart contract you're monitoring.&#x20;

1. **Event Type**: The W3bstream event name refers to the specific event that will be triggered by the monitor when a certain condition on the blockchain is met.
2. **Chain ID**: The Chain ID is a unique identifier for the blockchain where the monitored contract resides. Currently, the monitor supports only the IoTeX Testnet, which has a Chain ID of 4690.
3. **Contract Address**: This is the unique address of the smart contract you want to monitor on the blockchain.
4. **Block Start**: The Block Start is the specific block number where the monitoring process will begin. Typically, this is the block number where the monitored contract was deployed.
5. **Block End**: The Block End is the block number at which the monitoring process will stop. If you set this value to 0, the monitor will continue to run indefinitely.
6. **Topic0**: Topic0 refers to the hashed signature of the event you're monitoring within the target smart contract. To calculate this hash, you can use an online tool, such as the one below 👇 .

{% hint style="info" %}
To use the tool, input the event signature you want to monitor (for example, "Transfer(address,address,uint256)") and click on the "Hash" button. The resulting hash will be the Topic0 value you should use in your monitor configuration.
{% endhint %}

{% embed url="https://emn178.github.io/online-tools/keccak_256.html" %}

{% embed url="https://youtu.be/PdaskquJk3k" %}
