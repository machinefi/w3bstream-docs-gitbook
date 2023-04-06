# Publishers

Publishers can be used as a basic way of authorizing external sources to send data messages to W3bstream projects through one of the network service endpoints (HTTP or MQTT).&#x20;

Therefore, a publisher can be considered an "authorized entity", with its unique _id_ and _authorization_ _token_, that is allowed to send data messages to a specific project.&#x20;

Each publisher belongs to one and only one project_._ The publisher _id_ and _authorization token_ must be included in the message header when [sending a message to a W3bstream project](../sending-messages-to-w3bstream.md), respectively in the `pub_id` and `token` fields.

{% hint style="success" %}
Messages that do not include in their header a recipient project, or a valid _publisher_ _id_ and _token_ for their recipient project, will be discarded by W3bstream.
{% endhint %}

&#x20; <mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../../get-started/w3bstream-studio/adding-publishers.md" %}
[adding-publishers.md](../../get-started/w3bstream-studio/adding-publishers.md)
{% endcontent-ref %}

{% content-ref url="../sending-messages-to-w3bstream.md" %}
[sending-messages-to-w3bstream.md](../sending-messages-to-w3bstream.md)
{% endcontent-ref %}
