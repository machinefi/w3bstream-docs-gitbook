# HTTP API

## Introduction

The HTTP API is the most suitable method for sending data to a W3bstream project when the data publisher is a server, mobile client, or smart device as these are typically always connected and not constrained in terms of data volume or bandwidth.

## Authentication

Please refer to the [Client Authentication Patterns](../introduction.md#client-authentication-patterns) section.

## Finding your Project's HTTP route

Before you can send data to a specific project in W3bstream using the HTTP API you will need the HTTP route of the project. It can be found in W3bstream Studio, in the Project's "Events" page:&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## Data API Endpoint

{% swagger method="post" path="<PROJECT_NAME>" baseUrl="https://devnet-prod-api.w3bstream.com/event/" summary="Send Data to a W3bstream Project" %}
{% swagger-description %}
Sends a data payload to a specific W3bstream project for processing
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" required="true" %}
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
{ Authentication: Bearer w3b_MV8 ... I8Jg}
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
