# Event Routing Strategies

An event routing strategy is a rule that assigns a handler to a specific event, and it is used to determine the appropriate action to take when a particular event is emitted in W3bstream. Multiple event strategies can be defined for each W3bstream project, and they must include the name of the event to be handled, and the name of the event handler function defined in the Project's applet.

{% hint style="success" %}
If a message's header does not include an event\_type that matches an event strategy of its recipient project, the message will not trigger any logic execution. Instead, it will be logged in the console and then dropped by W3bstream.
{% endhint %}

&#x20; <mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../../get-started/w3bstream-studio/creating-strategies.md" %}
[creating-strategies.md](../../get-started/w3bstream-studio/creating-strategies.md)
{% endcontent-ref %}
