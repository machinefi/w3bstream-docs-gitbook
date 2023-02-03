# Sending data to W3bstream

W3bstream provides two different network service endpoints that allow sending data messages to the various running projects.&#x20;

A W3bstream data message is a JSON object composed of two properties:&#x20;

* the W3bstream _**header**_ is a nested object containing W3bstream-related values, and&#x20;
* the message _**payload**_ is a string that contains the actual message to be processed by the target event handler in W3bstream.&#x20;

An example message is shown below:

```javascript
{
  "header": {
    "pub_id": "my_publisher_id",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJQYXlsb2FkIjoiNDUwNTI4NzAxMjc2NTcwMyIsImlzcyI6InNydi1hcHBsZXQtbWdyIiwiZXhwIjoxNjY4Mzk4MDYxfQ._Q5ZaBP5FSa09s0FCn7CBcMCty9hkM5TDu5q1wTvwB8",
    "event_type": "DEVICE_EVENT_0001",
    "pub_time": 1667343986249
  },
    "payload": "VGhpcyBpcyB0aGUgbWVzc2FnZSBwYXlsb2FkCg=="
}
```

### The header

The header nested object is intended for W3bstream to authorize the message and route it to the right handler.

<mark style="color:blue;">**`pub_id:`**</mark>`<string>` is the identifier of a valid Publisher defined in the destination W3bstream Project.

<mark style="color:blue;">**`token:`**</mark>`<string>` is the authorization token associated with the Publisher Identifier (`pub_id`)

<mark style="color:blue;">**`event_type:`**</mark>`<string>` this can be anything, as long as it's matched in an event strategy of the destination W3bstream Project

<mark style="color:blue;">**`pub_time`**</mark>`:<number>` this is the timestamp when the message was actually sent.

### The payload

The message payload must be a string encoded using the base64 scheme and it can be anything. Once the message reaches W3bstream and a strategy rule is matched for the event, then the decoded payload string can be accessed by the target handler function using the `GetData` W3bstream function. &#x20;

## Sending data using HTTP

The W3bstream HTTP API default port is `8888`.&#x20;

the `event/project_name` the endpoint of the HTTP API can be called to send data messages to a specific project:

{% swagger method="post" path="/srv-applet-mgr/v0/event/<PROJECT_NAME>" baseUrl="w3bstream_ip_address:8888" summary="Send a message to a specific W3bstream Project" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="ProjectName" required="true" %}
The name of the Project as it appears in W3bstream Studio 
{% endswagger-parameter %}

{% swagger-response status="201: Created" description="This is returned when a project with the specified name has been found and the message has been correctly routed to an applet" %}
```javascript
{
  "results": [
    {
      "instanceID": "6757168266330119",
      "code": 0,
      "errMsg": ""
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="This is returned when no project with the specified name is defined in the W3bstream node" %}
```javascript
{
  "key": "NotFound",
  "code": 404999001,
  "msg": "NotFound",
  "desc": "GetPublisherByPublisherKey:Sqlx [NotFound] record is not found",
  "canBeTalk": false,
  "id": "",
  "sources": [
    "srv-applet-mgr@0.0.1"
  ],
  "fields": null
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="This is returned when a project with the specified name has been found but the message could not be routed to an applet because the event_type did not match any strategy in the project" %}
```javascript
{
  "key": "NotFound",
  "code": 404999001,
  "msg": "NotFound",
  "desc": "not found strategy",
  "canBeTalk": false,
  "id": "",
  "sources": [
    "srv-applet-mgr@0.0.1"
  ],
  "fields": null
}
-
```
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
**Notice:** project names are case-sensitive in W3bstream
{% endhint %}

The example below uses curl to send a message over HTTP where the recipient project is called `NftMinter` and it's intended to raise an event called "MINT" inside W3bstream:

```bash
curl --location --request POST 'localhost:8888/srv-applet-mgr/v0/event/NftMinter' --header 'Content-Type: text/plain' --data-raw '{
    "header": {
        "event_type": "MINT",
        "pub_id": "my_publisher_id",
        "pub_time": 1666211451,
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.e"                                
    },
    "payload": "VGhpcyBpcyB0aGUgbWVzc2FnZSBwYXlsb2FkCg=="
}' 
```

## Sending data using MQTT

{% hint style="info" %}
**Notice:** Client authentication with MQTT certificates is not supported yet.&#x20;
{% endhint %}

The W3bstream MQTT broker default port is 1883.&#x20;

To send a message to a specific W3bstream Project using MQTT, **the recipient project name should be used as the topic** when publishing the MQTT message.&#x20;

The example below uses [mosquitto](https://mosquitto.org/) as an MQTT client to send a message to a local W3bstream node where the recipient project is called `NftMinter` in W3bstream:

{% hint style="info" %}
**Notice:** project names are case-sensitive in W3bstream
{% endhint %}

```bash
mosquitto_pub -h localhost -t PROJECT_NAME -m '{
  "header": {
    "pub_id": "my_publisher_id",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJQYXlsb2FkIjoiNDUwNTI4NzAxMjc2NTcwMyIsImlzcyI6InNydi1hcHBsZXQtbWdyIiwiZXhwIjoxNjY4Mzk4MDYxfQ._Q5ZaBP5FSa09s0FCn7CBcMCty9hkM5TDu5q1wTvwB8",
    "event_type": "DEVICE_EVENT_0001",
    "pub_time": 1667343986249
  },
    "payload": "VGhpcyBpcyB0aGUgbWVzc2FnZSBwYXlsb2FkCg=="
}' 
```
