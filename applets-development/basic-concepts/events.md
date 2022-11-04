# Events



While running, a W3bstream node emits internal **Event Messages** when something relevant happens. A W3bstream event can be currently generated  for one of the following reasons:

* A message is received on an HTTP API [_project_ _endpoint_](../sending-messages-to-w3bstream.md#http-project-endpoints)__
* A message is published on an MQTT [_project topic_](../sending-messages-to-w3bstream.md#mqtt-project-topics)__
* A smart contract event is detected by a [_blockchain monitor_](events.md#blockchain-monitor)__
* _A certain blockchain height is detected by a chain height monitor_

A W3bstream event message looks like the following:

```json
{
  "header": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJQYXlsb2FkIjoiNDUwNTI4NzAxMjc2NTcwMyIsImlzcyI6InNydi1hcHBsZXQtbWdyIiwiZXhwIjoxNjY4Mzk4MDYxfQ._Q5ZaBP5FSa09s0FCn7CBcMCty9hkM5TDu5q1wTvwB8",
    "event_type": "ANY",
    "pub_id": "my_publisher_id",
    "pub_time": 1667343986249
  },
    "payload": "This is the event payload data",
}
```

Once a W3bstream message is emitted, it's routed to the recipient [Project](events.md#projects) which, in turn, routes the event's **payload** to the corresponding [Applet](events.md#applets) handler.

#### &#x20;** **<mark style="color:purple;">**💡**</mark> <mark style="color:purple;"></mark><mark style="color:purple;">Learn more</mark>

{% content-ref url="../sending-messages-to-w3bstream.md" %}
[sending-messages-to-w3bstream.md](../sending-messages-to-w3bstream.md)
{% endcontent-ref %}

{% content-ref url="../reacting-to-blockchain-events.md" %}
[reacting-to-blockchain-events.md](../reacting-to-blockchain-events.md)
{% endcontent-ref %}
