# Event strategies

An event strategy is a _rule_ that assigns an _event handler_ to a certain _event,_ and are used to define "_what to do"_ when a certain event is emitted in W3bstream.&#x20;

Multiple event strategies can be defined for each W3bstream project, and it must include the name of the event to be handled, the name of the event handler function, and the project's applet that exports the handler.

{% hint style="success" %}
Messages that do not include in their header an _event\_type_ _that is_ matched by an event strategy of their recipient project, will not trigger any logic execution. Instead, they will just be logged in the console, before being dropped by W3bstream.
{% endhint %}

&#x20; <mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../../get-started/w3bstream-studio/creating-strategies.md" %}
[creating-strategies.md](../../get-started/w3bstream-studio/creating-strategies.md)
{% endcontent-ref %}
