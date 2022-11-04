# Publishers

Publishers can be used as a basic way of authorizing external sources to send data to W3bstream projects through one of the network service endpoints (HTTP or MQTT). Therefore, a publisher represents an "account", with its unique _id_ and _auth_ _token, that belong to a specific project._ The publisher id and auth token must be included in the message header when sending a message to a W3bstream project, in the `pub_id` and `token` fields, respectively.

{% hint style="success" %}
Messages that do not include in their header a _publisher_ _id_ and _token that are_ valid for their recipient project, will be ignored by W3bstream.
{% endhint %}

&#x20; **  **<mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../../get-started/w3bstream-studio/adding-publishers.md" %}
[adding-publishers.md](../../get-started/w3bstream-studio/adding-publishers.md)
{% endcontent-ref %}

{% content-ref url="../sending-messages-to-w3bstream.md" %}
[sending-messages-to-w3bstream.md](../sending-messages-to-w3bstream.md)
{% endcontent-ref %}
