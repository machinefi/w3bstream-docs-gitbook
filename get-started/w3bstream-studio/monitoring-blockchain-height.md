# Monitoring Blockchain Height

{% hint style="success" %}
To configure a Blockchain Height Monitor in W3bstream, make sure you have [created a Project first](creating-projects.md).
{% endhint %}

Monitoring the blockchain height allows generating a W3bstream event when a specific height is reached on the blockchain.&#x20;

Click the "**`Chain Height Monitor`**" in the left navigation panel, then click the <mark style="color:blue;">**`Create blockchain height monitor`**</mark><mark style="color:blue;">** **</mark><mark style="color:blue;">****</mark> button**:**

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Configure the _Create blockchain height_ _monitor_ dialog with the correct settings for the blockchain height you want to use as the trigger:

**`Project ID`**: select the W3bsytream project the monitor belongs to.

**`Event Type`**: set a code for the W3bstream event that will be generated by the monitor (it can be anything, just match whatever you use here when configuring the respective [event strategy](creating-strategies.md)).

**`Chain ID`**: Input the Chain ID of the network where you want to monitor the height. This depends on the actual chain endpoint set in the [W3bstream configuration](../../applets-development/configuring-w3bstream.md).

**`Height`**: input here the chain height that should trigger the event once it's reached.

****![](<../../.gitbook/assets/image (5) (3).png>)****
