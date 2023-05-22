# Device Accounts

Device accounts can be used as a basic way to authorize external sources to send data messages to W3bstream projects via one of the network service endpoints (HTTP or MQTT). As a result, a Device Account can be considered an "authorized entity" with its unique ID and authorization token that is permitted to send data messages to a particular project.

Each account is associated with one and only one project. The authorization token must be provided when sending a message to a W3bstream project.

{% hint style="success" %}
Messages that do not include in their header a valid _token_ that belong to the recipient project, will be discarded by W3bstream.
{% endhint %}
