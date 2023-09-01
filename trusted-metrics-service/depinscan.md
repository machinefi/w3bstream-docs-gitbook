# DePINscan

Built on top of W3bstream's [Trusted Metrics API](http://127.0.0.1:5000/o/-MQ9LhchTp7\_QJr-AYG0/s/f2s3zCHPO4kfjqwDZ9Gw/), [DePINscan.io](https://depinscan.io/) offers a ready-to-use dashboard that provides essential visualizations tailored for DePIN projects **that have their off-chain logic deployed on W3bstream**. It provides community users with verifiable insights into a project's data flow, device count, data volume, and token-related specifics, further accelerating the time to market for DePIN builders.

{% embed url="https://depinscan.io" %}
Click to Visit depinscan.io
{% endembed %}

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>DePINscan Global Map of devices and Projects List</p></figcaption></figure>

Beyond serving as a dynamic visualization tool, DePINscan is also a centralized hub for any DePIN project, enthusiasts, developers, and investors, ensuring they remain updated with sector advancements. Furthermore, DePINscan exemplifies what can be achieved using the Trusted Metrics API service from W3bstream.

### For DePIN Projects deployed on W3bstream

If your DePIN project's off-chain logic is deployed on W3bstream, then you can get the maximum benefit out of DePINscan.

<figure><img src="../.gitbook/assets/trusted-metrics-auto.png" alt=""><figcaption><p>Allow Trusted Metrics Service to collect your event data for it to be displayed in DePINscan</p></figcaption></figure>

{% hint style="info" %}
**What if my DePIN project doesn't use W3bstream yet? 🤔**\
If your DePIN project is not leveraging W3bstream yet, but you'd still like your off-chain data to be displayed in the DePINscan dashboard, and you'd like your devices to show on the global map, you'll have to simply create a new [W3bstream Project](../applets-development/creating-the-project.md). \
\
Once created, you'll have to generate a new API key in your [account settings](https://devnet.w3bstream.com/setting) and use it, together with your W3bstream project's HTTPS endpoint and your device ID to send data via one of our [client SDKs](../client-sdks/pc-client-sdks/).&#x20;
{% endhint %}

### Showing Your Devices in the DePINscan Global Map

In order to show your devices in the DePINscan Global Map you'll have to construct the **JSON payload** sent by your device to your W3bstream Project to also include a "_latitude_" and "_longitude_" fields, such as `{"`**`latitude": 37.751, "longitude": -97.822}`.**

Once that is done, you'll have to enable the "_Auto Collect Metric_" as seen above.&#x20;
