# Create a Project

W3bstream's logic is organized into _Projects_ and _Handlers._

The first step is to **create** a new _W3bstream Project:_ click the <mark style="color:blue;background-color:blue;">**`Create a project now`**</mark> button to create a new W3bstream project.

Assign the "_HelloW3bstream_" name to the project and click the <mark style="color:blue;">**`Submit`**</mark> button to confirm. The new project will show up on the left side panel, under the **Project Management** section.

## Upload the logic

Once we have a project ready to host our W3bstream logic, we are ready to deploy a logic module, also called [Applet](../applets-development/basic-concepts/#applets).&#x20;

{% hint style="success" %}
Check out the[ Applets Development](../applets-development/basic-concepts/) section to learn more about how to create an Applet:
{% endhint %}

In this guide, we will deploy a simple wasm applet called "**Log**": it will simply echo to the w3bstream console any data that is sent to our node over the HTTP or MQTT network endpoints.&#x20;

Download the `log.wasm` file from the link below, and save it in a known location on your system:

{% embed url="https://github.com/machinefi/w3bstream/blob/main/_examples/log/log.wasm" %}

In W3bstream Studio, select the HelloW3bstream project, and click the <mark style="color:blue;">**`Add Applet`**</mark> button:

<figure><img src="../.gitbook/assets/image (11) (2).png" alt=""><figcaption></figcaption></figure>

Select the `log.wasm` file you just downloaded, select the _HelloWebstream_ project from the Project ID dropdown, name this applet "_LogExample"_ and finally hit the **`Submit`** button to upload the applet to the _HelloW3bstream_ project:

<div>

<figure><img src="../.gitbook/assets/image (1) (2) (1).png" alt=""><figcaption></figcaption></figure>

 

<figure><img src="../.gitbook/assets/Schermata 2022-11-01 alle 16.02.37.png" alt=""><figcaption></figcaption></figure>

</div>

## Deploy the logic

Now that the logic module is uploaded to the project, we can deploy it to the Webstream VM by clicking the <mark style="color:blue;">**`Deploy`**</mark> button. If the module is correct, it will be successfully deployed, and you will be able to start/stop the module from the dashboard:

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
