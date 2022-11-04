# Event strategies

Event strategies can be used to define "_what to do"_ when a certain event is emitted in W3bstream. Therefore, an event strategy represents a _rule_ that assigns an applet's function (aka "_event handler_") to a certain _event type_. The event type must be specified in the message header when sending a message to a w3bstream project, using the `event_type` field. The event type can be any string, as long as it's matched by an event strategy.

{% hint style="success" %}
Messages that do not include in their header an _event\_type_ _that is_ matched by an event strategy of their recipient project, will not trigger any logic exectution. Instead they will just be logged in the console, before being dropped by W3bstream.
{% endhint %}

&#x20; **  **<mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../../get-started/w3bstream-studio/creating-strategies.md" %}
[creating-strategies.md](../../get-started/w3bstream-studio/creating-strategies.md)
{% endcontent-ref %}
