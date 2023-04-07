# Events

## Events and Triggers

W3bstream is a powerful event-driven system that generates _Event Messages_ based on specific triggers. It is designed to help developers handle high-volume, real-time data processing and event-driven workflows efficiently.

W3bstream supports several event triggers, including:

* Receiving data messages on an HTTP API endpoint
* Receiving data messages on an MQTT topic
* Detecting smart contract events through a _Blockchain Monitor_, and&#x20;
* Detecting a certain blockchain height through a _Chain Height Monitor_.

## Event payload

Every W3bstream event has a Payload attached to it: when a W3bstream event is emitted, and a matching Routing Strategy exists for that event, the event is sent to the appropriate Project's applet that contains the destination handler function. This allows developers to process the event and take necessary actions quickly and efficiently.

With W3bstream, developers can build event-driven applications that are scalable, robust, and efficient. The system's flexibility and ease of use make it an ideal choice for businesses of all sizes, from startups to large enterprises.

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
