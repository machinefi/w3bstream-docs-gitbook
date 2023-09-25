# Introduction

W3bstream offers HTTP and MQTT network endpoints designed to streamline the transmission of data messages for processing within deployed projects.

## Client Authentication Patterns

When transmitting data to a W3bstream project, two distinct authentication methods come into play. The choice between them depends on whether the data publisher is sending data directly to W3bstream or if it's being transmitted by a cloud server on behalf of the original publishers. The second approach is frequently employed when **integrating W3bstream into an existing cloud** architecture. For a more in-depth understanding, additional details will be presented in the following sections

### Sending data from individual Publishers

When sending data from individual Publishers you need to first "register" a new publisher to your W3bstream project. You can do this either manually, from the "Publishers" section [in W3bstream Studio](../applets-development/configuring-devices.md#creating-devices-using-w3bstream-studio), or programmatically from the publisher itself through W3bstream's [Publisher API](../applets-development/configuring-devices.md#creating-devices-using-the-publisher-api).&#x20;

Once a publisher is authorized, an authentication token is assigned to it, that should be used when sending any data to that project.

### Sending data form a backend server

When your architecture involves a cloud server or any backend where data publishers are already sending their data and you want to leverage W3bstream for verifiable processing in this scenario, you should use the API Key functionality.

W3bstream Studio allows you to create multiple API Keys with dedicated permissions, enabling the integration of an existing cloud/backend with your W3bstream projects and, among other things, send events on behalf of the actual publishers.

{% hint style="success" %}
See the [**Create API Key section**](../get-started/w3bstream-studio/create-api-keys.md) of the W3bstream Studio tutorial to learn how to generate an API Key
{% endhint %}

By authenticating your API call using an API Key with the appropriate permissions to manage publishers, you can indicate the ID of the publisher to which the data belongs. W3bstream will automatically create new publishers when necessary.



{% hint style="info" %}
It's important to note that API Keys are only supported when sending data through the HTTPS API.
{% endhint %}

## Client SDKs

Typically, when sending data to a W3bstream project, you would use one of the available Client SDKs to encapsulate the W3bstream data API. With an SDK, you only need to initialize the client connection and use it to send your payload to the recipient project, without caring about the underlying API.

### Available SDKs

Depending on the nature of your publishers, which can include IoT, mobile, or PC-based systems, one of the W3bstream Client SDKs may offers compatibility with your specific system. Currently, the W3bstream Client SDKs are available for the following platforms:

**Mobile:** [iOS](mobile-client-sdks.md#ios-client-sdk), [Android](mobile-client-sdks.md#android-client-sdk)

**IoT:** [Arduino](introduction-1/arduino.md), [ESP32](introduction-1/esp32.md), [RaspberryPi & Linux](introduction-1/embedded-sdks.md)

**PC-based:** [Node.js](pc-client-sdks/node-js.md), [Python](pc-client-sdks/python.md), [Go](pc-client-sdks/go-lang.md)

By selecting the appropriate SDK based on your device type, you can streamline the integration of W3bstream capabilities into your application, ensuring seamless data transmission and processing.
