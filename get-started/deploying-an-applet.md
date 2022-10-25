# Deploying an Applet

A W3bstream applet implements the logic of a MachineFi dApp at the data level: it responds to W3bstream events by running a specific handler according to the W3bstream configuration.&#x20;

Since W3bstream runtime's _execution engine_ is based on a [WebAssembly](https://webassembly.org/) virtual machine, W3bstream applets must be compiled as WASM modules.&#x20;

{% hint style="info" %}
WebAssembly provides a way to create safe and portable code written in multiple languages that can run at near native speed. The full WebAssembly documentation is available at [https://developer.mozilla.org/en-US/docs/WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly)&#x20;
{% endhint %}

In this document, we will use the W3bstream command-line client, however w3bstream also provides a web interface called [W3bstream Studio](w3bstream-studio.md), accessible on port :3000, that allows you to perform applets deployment.

### Deploy with W3bstream Studio

The easiest way to deploy an applet to W3bstream is by using [W3bstream Studio](w3bstream-studio.md). Unless you configured a reverse proxy on your server, or you changed the port manually, the Studio interface can be accessed by pointing your browser to your W3bstream server IP on port `3000`.

{% hint style="info" %}
To learn more about W3bstream Studio, checkout the [W3bstream Studio](deploying-an-applet.md#w3bstream-studio) page.&#x20;
{% endhint %}

#### Login to W3bstream

Make sure the [W3bstream node is running](running-a-node.md#start-the-w3bstream-node-with), and you took note of the admin password. Open W3bstream Studio at **https://localhost:3000** and use the admin password to login. For a newly installed W3bstream node, you will see something like this:

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

#### Create a Project

The first step is to create a _W3bstream Project_, that will act as a container for those WASM applets that belong to a specific application. Let's call our project “`MyMachineFiProject`”. We can leave the version unchanged. Click the Submit button to create the project:

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

#### &#x20;Upload the Applet

Once we have a project ready to host our applets, we can now deploy our example applet. Any high-level language that can compile to WebAssembly and target the WASI interface can be used to [create a W3bstream applet](../applets-development/basic-concepts.md).

Here, we will deploy a simple wasm applet called "**Log**" that will just echo to the w3bstream console any message incoming into our w3bstream http endpoint. You can download the `log.wasm` file from the link below, and save it in a known location on your W3bstream server:

{% embed url="https://github.com/iotexproject/w3bstream/raw/main/examples/log/log.wasm" %}

In W3bstream Studio, select the file using the upload file button, select the project you want to upload the applet to, name this app `LogExample` and finally hit `Submit` to upload the applet to the project. You will find the new applet in the Project Management section, listed under the project:&#x20;

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



#### Deploy the applet

The applet is currently loaded in the W3bstream internal storage, ready to be deployed to the WASM Virtual Machine (W3bstream's execution engine). To do so, just click the `Deploy` button next to the applet:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

