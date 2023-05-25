# Defining the message protocol

When creating a W3bstream project, it's important to define the messaging protocol between the devices that send the data, and your W3bstream project. Currently, there are two ways to send data messages to a W3bstream project: over HTTP or MQTT. During the development phase of your project, you can also simulate data messages from the "**Log**" section in W3bstream Studio.

Here's an overview of how it works.

## Using W3bstream Client SDKs

In the previous section [message-api.md](../get-started/basic-concepts/message-api.md "mention") we discussed the messaging format specified by the W3bstream API. Each W3bstream message contains a payload string field, which is intended to hold the actual data sent by a smart device to our project and to be processed by a handler.

To simplify the process of sending data to your W3bstream project, we recommend utilizing a W3bstream Client SDK tailored for your specific device. By doing so, you won't need to concern yourself with the intricacies of the W3bstream messaging protocol. Instead, you can focus on providing the relevant data for your application, including the target project name, event type, and device authentication token.

If you're unsure which W3bstream Client SDK is suitable for your device, please refer to our documentation for additional guidance and information.

{% content-ref url="../client-device-sdks/introduction/" %}
[introduction](../client-device-sdks/introduction/)
{% endcontent-ref %}

## Example message

As an example, let's consider a weather station device that periodically contributes climate data. The payload for such a device could be structured as follows:

```javascript
{
  "data": {
     "temperature": 16.5,
     "timestamp": "1683744240"
  },
  "device_id": "WS1209ABC"
} 
```
