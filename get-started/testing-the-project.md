# Testing the Project

Before we can send messages to the W3bstream node, we should make sure a Publisher Account is set, and an Event Strategy is in place.

## Create a Publisher account

To create a publisher account, just go to the **`Publishers`** section on the left side panel and click the  **`Add Publisher`** button:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Select the Project, give a name to the publisher and assign it a unique key like in the image below. Then click the <mark style="color:blue;">**`Submit Button`**</mark> to confirm:

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## Default event strategy

When deploying a logic module to a project, W3bstream configures a default event strategy that just routes any event to the module's start handler. To learn more about event strategies, check out the [#strategies](../applets-development/basic-concepts.md#strategies "mention") section. &#x20;

## Test the project logic

To test this simple logic, we can use the W3bstream Studio interface itself to send a message to the node over HTTP.&#x20;

Click the HelloW3bstream project in the side panel, and click the <mark style="color:blue;">**`Send Event`**</mark> button:

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

In the Send Event dialog, select the publisher account, then edit the message payload value and make it "Hello W3bstream!"

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Click the Submit Button to send the event to the W3bstream node, then check the W3bstream docker log to see that the event has been detected by the node and routed to the HelloW3bstream project:

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>
