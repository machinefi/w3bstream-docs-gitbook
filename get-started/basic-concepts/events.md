# Event Triggers

W3bstream is a powerful event-driven system that generates _Event Messages_ based on specific _triggers_. It is designed to help developers handle high-volume, real-time data processing and event-driven workflows efficiently.

W3bstream supports several event triggers, including:

* Receiving data messages on an HTTP API endpoint
* Receiving data messages on an MQTT topic
* Detecting smart contract events through a _Blockchain Monitor_, and&#x20;
* Detecting a certain blockchain height through a _Chain Height Monitor_.

## Event payload

Every W3bstream event has a Payload attached to it: when a W3bstream event is emitted, and a matching Event Routing strategy exists for that event, the event is sent to the appropriate Project that contains the destination handler function. This enables developers to efficiently process the payload of the event and take the necessary actions.
