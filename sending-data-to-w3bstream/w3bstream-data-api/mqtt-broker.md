# MQTT Broker

{% hint style="info" %}
This section is work in progress and will be published soon
{% endhint %}

## Introduction

W3bstream's MQTT broker service is the ideal method for transmitting data to a W3bstream project when the data publisher is a constrained device with limitations on data volume or bandwidth, such as a cellular IoT device.

## Authentication

Please refer to the [Client Authentication Patterns](../introduction.md#client-authentication-patterns) section.

## Finding your Project's MQTT topic

Before sending data to a specific project in W3bstream using the MQTT Broker, you will need to obtain the MQTT topic of the project. You can find this information in W3bstream Studio on the Project's 'Events' page:

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## MQTT Message

The format of the MQTT message is as follows:

```json
{
  "events": [
    {
      "header": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJQYXlsb2FkIjoiNDUwNTI4NzAxMjc2NTcwMyIsImlzcyI6InNydi1hcHBsZXQtbWdyIiwiZXhwIjoxNjY4Mzk4MDYxfQ._Q5ZaBP5FSa09s0FCn7CBcMCty9hkM5TDu5q1wTvwB8",
        "event_type": "BINDING",
        "timestamp": 1667343986249
      },
      "payload": "Your application data"
    },
    ...
  ]
}
```

## Encoding

Given that MQTT protocol is often used for data transmission in situations where publishers may have hardware or network constraints, **the message must be Base64 encoded**. It serves to reduce the size of the data, making it more efficient to transmit.
