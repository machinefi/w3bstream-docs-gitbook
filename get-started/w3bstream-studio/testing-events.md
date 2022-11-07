# Testing Events

W3bstream Studio allows manually sending messages to the W3bstream node over HTTP from the Studio UI. This is useful when you want to test the logic of the node by simulating different types of events.&#x20;

{% hint style="success" %}
Before you can test this feature, make sure that

* you have already [created a Publisher account](adding-publishers.md)
* you have [deployed an Applet](deploying-applets.md)
* the [Applet is running](managing-applets-execution.md)
* you have [created an event strategy](creating-strategies.md) for the message you want to test
{% endhint %}

To manually generate a W3bstream event, select the project in the left navigation panel, then click the <mark style="color:blue;">**`Send Event`**</mark> button:

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Configure the **Publish Event** **dialog** as follows:&#x20;

**`Project ID`**: select the W3bsytream project the event should be sent to (make sure the applet containing the handler for the event **is running**).

**`Publisher`**: select the Publisher intended to be the message sender.

**`Payload`**: In the payload box, the header of the event is already filled in with the event type, publisher authorization data, and timestamp. Just edit the Payload of the event with the actual data object that should be sent to the handler.

![](<../../.gitbook/assets/image (4) (1).png>)h

<details>

<summary><img src="../../.gitbook/assets/image (33).png" alt=""> Escaping double quotes</summary>

Please notice that if the payload must be a JSON object. If it's something more complex than just a string, you will have to manually escape double quotes. If your payload is for example:

`{ "temperature": 22.3, "status": "ON" }`

then your payload would look like:

`"payload": "{ \"temperature\": 22.3, \"status\": \"ON\" }"`

Check out this online tool to automatically escaping double quotes:&#x20;

[tools.knowledgewalls.com](https://tools.knowledgewalls.com/online-escape-single-or-double-quotes-from-string)



</details>

