# Projects

W3bstream Projects represent containers for the node logic. This logic is implemented in the form of functions (called _event handlers_) exported inside WASM modules (called _applets_) that are deployed to W3bstream projects.

Multiple applets can be deployed to a project, and multiple handlers can be exported in the same applet. For each W3bstream project, one or more [event strategies](projects.md#event-strategies) can be configured, as well as several [publishers](projects.md#publishers) can be authorized to send data messages to the project.&#x20;

&#x20; <mark style="color:purple;">**💡 Learn more**</mark>

{% content-ref url="../../get-started/w3bstream-studio/creating-projects.md" %}
[creating-projects.md](../../get-started/w3bstream-studio/creating-projects.md)
{% endcontent-ref %}

{% content-ref url="../getting-events-data.md" %}
[getting-events-data.md](../getting-events-data.md)
{% endcontent-ref %}
