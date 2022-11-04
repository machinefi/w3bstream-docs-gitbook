# Projects

W3bstream Projects represent containers for the node logic. Each project also includes one or more [event strategy](projects.md#event-strategies) configurations, as well as [publisher](projects.md#publishers) authorizations.&#x20;

Every time a W3bstream event is emitted with a specific project as its recipient, the project's event strategy is evaluated. If a strategy is matched for the `event_type` field of the event, then the respective [Applet](projects.md#applets) handler is called with the event<mark style="color:purple;">'s</mark> `resource id` as the argument of the call.

&#x20; **  **<mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../../get-started/w3bstream-studio/creating-projects.md" %}
[creating-projects.md](../../get-started/w3bstream-studio/creating-projects.md)
{% endcontent-ref %}

{% content-ref url="../getting-events-data.md" %}
[getting-events-data.md](../getting-events-data.md)
{% endcontent-ref %}
