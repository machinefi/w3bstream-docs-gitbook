# Device Accounts

Device accounts can be used as a basic way to authorize external sources to send data messages to W3bstream projects via one of the network service endpoints (HTTP or MQTT). As a result, a Device Account can be considered an "authorized entity" with its unique ID and authorization token that is permitted to send data messages to a particular project.

Each publisher is associated with one and only one project. The publisher ID and authorization token must be included in the message header when sending a message to a W3bstream project, specifically in the pub\_id and token fields.

{% hint style="success" %}
Messages that do not include in their header a valid _publisher_ _id_ and _token_ for their recipient project, will be discarded by W3bstream.
{% endhint %}

&#x20; <mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../w3bstream-studio/adding-publishers.md" %}
[adding-publishers.md](../w3bstream-studio/adding-publishers.md)
{% endcontent-ref %}

{% content-ref url="../../applets-development/sending-messages-to-w3bstream.md" %}
[sending-messages-to-w3bstream.md](../../applets-development/sending-messages-to-w3bstream.md)
{% endcontent-ref %}
