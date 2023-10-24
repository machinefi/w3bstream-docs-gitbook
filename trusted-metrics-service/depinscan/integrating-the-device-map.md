# Integrating the Device Map

## Global Device Map in DePIN Projects

A global map of devices for a DePIN project is an invaluable tool, offering a clear visualization of the network's scale and reach. It promotes transparency for all stakeholders, highlighting areas of high device concentration and potential expansion zones.&#x20;

For decentralized systems where location affects performance or service availability, a global map aids in strategic planning and optimization.

## DePINscan's Device Map

Since a global device map crystallizes the decentralized nature of DePIN projects, DePINscan introduces an intuitive and visually appealing global device map that any DePIN project can integrate.

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Given that DePINscan operates on W3bstream's Trusted Metrics API, you need to transmit your device location data to a W3bstream project with a certain format. This ensures the data is published via the Trusted Metrics API and thereby becomes accessible to DePINscan.

To integrate your DePIN project's device locations with the DePINscan map, follow the steps below.

## Integration of Device Locations with the DePINscan Map

If your DePIN project isn't hosted on a W3bstream node, initiate by creating a W3bstream project using the provided link:

{% hint style="success" %}
[Create a new "_Hello World_" Project in W3bstream Studio](../../get-started/deploying-an-applet.md)
{% endhint %}

This project's sole function is to receive device location data and relay it to the Trusted Metrics API.

### Step 1: Activating device location data collection

Once your W3bstream project is up and running, you either have to [set up a new event routing](../../get-started/w3bstream-studio/creating-strategies.md) or select an existing one on the project's **Events** page. Regardless of your choice, remember to reference the event name when submitting the location data message as highlighted in the subsequent section.

For demonstration purposes, in the screenshot below we'll utilize the `DEFAULT` event. Proceed by clicking the `EDIT` button corresponding to the chosen routing, then activate the option to forward device location data to the Trusted Metrics API:

<figure><img src="../../.gitbook/assets/Screenshot 2023-09-01 alle 17.20.46.png" alt=""><figcaption></figcaption></figure>

### Step 2: Transmitting device location data

Once you've deployed your W3bstream project and set up an event routing to relay location data to the Trusted Metrics service, the final step is to embed the actual device location data within a W3bstream message directed at that specific event in your project.

{% hint style="success" %}
You can refer to the [**Sending Data to W3bstream**](broken-reference) section to learn how to send device data to your W3bstream project
{% endhint %}

The W3bstream [PC Client SDK](../../sending-data-to-w3bstream/pc-client-sdks/) simplifies the process of relaying messages to a W3bstream project from your backend. This SDK is compatible with Node JS, Python, and Go Lang.

Here's a sample of how to embed device location data into a W3bstream data message and transmit it to your W3bstream project using Node JS:

&#x20;

```typescript
import { W3bstreamClient } from "w3bstream-client-js";

// Retrieve your W3bstream Project route from the events page in W3bstream Studio
const URL = "http_route";
// Fetch your W3bstream API key from your profile settings in W3bstream Studio
const API_KEY = "api_key";

// Set up the client
const client = new W3bstreamClient(URL, API_KEY);

// The header for the W3bstream message should contain the device ID and the W3bstream
// event. If no event is specified, "DEFAULT" is assumed
const header = {
  device_id: "device_001",
  event_type: "DEFAULT"
};

// The W3bstream message's payload can be any object. This depends on 
// whether your DePIN project has logic operational on W3bstream.
// Ensure that the latitude and longitude fields are appropriately named
// and placed at the root level.
const payload = {
  latitude: 25.14,
  longitude: 116.32,
  data: { // sample data if your project operates on W3bstream
    temperature: 25.1,
    humidity: 47.5
  }
};

const main = async () => {
  try {
    const response = await client.publishSingle(header, payload);

    console.log(JSON.stringify(response.data, null, 2));
  } catch (error) {
    console.error(error);
  }
};

main();
```
