# HTTP API

## Introduction

The HTTP API is the most suitable method for sending data to a W3bstream project when the data publisher is a server, mobile client, or smart device as these are typically always connected and not constrained in terms of data volume or bandwidth.

## Authentication

Please refer to the [Client Authentication Patterns](../introduction.md#client-authentication-patterns) section.

## Finding your Project's HTTP route

Before sending data to a specific project in W3bstream using the HTTP API, you will need to obtain the HTTP route of the project. You can find this information in W3bstream Studio on the Project's 'Events' page.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## Data API

### Sending from an individual publisher

{% swagger method="post" path="<PROJECT_NAME>" baseUrl="https://devnet-prod-api.w3bstream.com/event/" summary="Send Data to a W3bstream Project" %}
{% swagger-description %}
Sends a data payload to a specific W3bstream project for processing
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
The publisher authentication token (Bearer)
{% endswagger-parameter %}

{% swagger-parameter in="path" name="eventType" %}
The Project-defined event to be raised
{% endswagger-parameter %}

{% swagger-parameter in="path" name="timestamp" %}
The timestamp when the message was sent by the client
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}

{% endswagger-response %}
{% endswagger %}

<details>

<summary>Example Request</summary>

**URL**

[https://devnet-prod-api.w3bstream.com/event/eth\_0x2c37a2cbcfaccdd0625b4e3151d6260149ee866b\_energy\_sharing](https://devnet-prod-api.w3bstream.com/event/eth\_0x2c37a2cbcfaccdd0625b4e3151d6260149ee866b\_energy\_sharing)

**Header**

```json
{ Authorization: Bearer w3b_MV8 ... I8Jg}
```

**Body**

```json
{ 
    Temperature: 24.3,
    Latitude: 118.65789
    Longitude: 94.223321
}
```

**Response**

```json
{
  "channel": "eth_0x2c37a2cbcfaccdd0625b4e3151d6260149ee866b_energy_sharing",
  "publisherID": "1038110072263586821",
  "publisherKey": "001",
  "eventID": "31fed038-8f10-48d5-958e-f9131754c85b_w3b",
  "timestamp": 1695401468899,
  "results": [
    {
      "appletName": "299519632338498561",
      "instanceID": "299519632338509832",
      "handler": "start",
      "returnValue": null,
      "code": 0
    }
  ]
}
```



</details>

### Sending on behalf of publishers

This API facilitates the transmission of data from a single source (usually a cloud service receiving data from the actual devices/publishers) on behalf of individual publishers. In this scenario, the body of the HTTP request should be an array of JSON objects, where each object represents a data message associated with a specific device ID. These data messages must include the respective device ID and the event type that is intended to be triggered in W3bstream. The API URL will incorporate a unique `eventType`, designated as '`DA-TA_PU-SH`', to differentiate this request from those involving a single publisher sending a data message.

{% hint style="info" %}
&#x20;It's important to note that the body should be in an array format, even when sending just a single data message.
{% endhint %}

{% swagger method="post" path="<PROJECT_NAME>" baseUrl="https://devnet-prod-api.w3bstream.com/event/" summary="Send Data to a W3bstream Project" %}
{% swagger-description %}
Sends a data payload on behalf of publishers to a specific W3bstream project for processing
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
The API Key (Bearer) with read/write access permissions to publishers
{% endswagger-parameter %}

{% swagger-parameter in="path" name="eventType" %}
In this scenario the **eventType** in the URL must be equal to "`DA-TA_PU-SH`"
{% endswagger-parameter %}

{% swagger-parameter in="path" name="timestamp" %}
The timestamp when the message was sent by the client
{% endswagger-parameter %}

{% swagger-parameter in="body" name="device_id" required="true" %}
The unique id of the device you are sending data on behalf of. New devices will automatically be added to the target project.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="eventType" %}
The Project-defined event to be raised
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" %}
The timestamp when the message was sent by the client
{% endswagger-parameter %}

{% swagger-parameter in="body" name="payload" required="true" %}
A string field including the actual data to be sent to the target W3bstream project
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}

{% endswagger-response %}
{% endswagger %}

<details>

<summary>Example Request</summary>

**URL**

https://devnet-prod-api.w3bstream.com/event/eth\_0x2c37a2cbcfaccdd0625b4e3151d6260149ee866b\_energy\_sharing**?eventType=DA-TA\_PU-SH**

**Header**

```json
{ Authorization: Bearer w3b_MV8 ... I8Jg}
```

**Body**

```json
[
    { 
        device_id: "UNIQUE_DEVICE_ID_1",
        Temperature: 24.3,
        Latitude: 118.65789
        Longitude: 94.223321
    },
   { 
        device_id: "UNIQUE_DEVICE_ID_2",
        Temperature: 21.3,
        Latitude: 102.12345
        Longitude: 94.223321
    },
]
```

**Response**

```json
{
  "channel": "eth_0x2c37a2cbcfaccdd0625b4e3151d6260149ee866b_energy_sharing",
  "publisherID": "1038110072263586821",
  "publisherKey": "001",
  "eventID": "31fed038-8f10-48d5-958e-f9131754c85b_w3b",
  "timestamp": 1695401468899,
  "results": [
    {
      "appletName": "299519632338498561",
      "instanceID": "299519632338509832",
      "handler": "start",
      "returnValue": null,
      "code": 0
    }
  ]
}
```



</details>
