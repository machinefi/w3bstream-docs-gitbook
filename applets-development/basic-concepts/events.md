# Events



While running, a W3bstream node emits internal **Event Messages** when something relevant happens. A W3bstream event can be currently generated  for one of the following reasons:

* A data message is received on an HTTP API [_project_ _endpoint_](../sending-messages-to-w3bstream.md#sending-data-using-http)
* A data message is published on an MQTT [_project topic_](../sending-messages-to-w3bstream.md#sending-data-using-mqtt)
* A smart contract event is detected by a [_blockchain monitor_](../reacting-to-blockchain-events.md)
* _A certain blockchain height is detected by a chain height monitor_

Once a W3bstream event is emitted, if a matching strategy is found for that event, it will be routed to the respective [Project](events.md#projects)'s applet that contains the destination handler function.

#### &#x20;<mark style="color:purple;">**💡**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Learn more</mark>

{% content-ref url="../sending-messages-to-w3bstream.md" %}
[sending-messages-to-w3bstream.md](../sending-messages-to-w3bstream.md)
{% endcontent-ref %}

{% content-ref url="../reacting-to-blockchain-events.md" %}
[reacting-to-blockchain-events.md](../reacting-to-blockchain-events.md)
{% endcontent-ref %}
