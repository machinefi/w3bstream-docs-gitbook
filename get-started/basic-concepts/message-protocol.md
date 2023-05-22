# Message Protocol

W3bstream provides HTTP and MQTT network endpoints that enable the transmission of data messages between running projects. Typically, you would utilize one of the available Client SDKs to encapsulate the W3bstream message protocol and provide the necessary information, such as the destination project and device token. However, if the SDK you are using lacks this functionality or if you are developing your own client, this section provides a detailed explanation of the W3bstream message format.

Each W3bstream message consists of a _header_ object, which contains fields related to the messaging protocol (e.g., authentication information and timestamp), and a _payload_ string that contains the actual message to be processed by the target handler. The target event handler is specified as the name of an event within the W3bstream project that will be triggered upon receiving the message.

The client is required to send a JSON object that includes a single array field called "_events_," which contains a batch of messages. This structure must be used even when sending a single message.

An example W3bstream message is provided below:

```javascript
{
  "events": [
    {
      "header": {
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJQYXlsb2FkIjoiNDUwNTI4NzAxMjc2NTcwMyIsImlzcyI6InNydi1hcHBsZXQtbWdyIiwiZXhwIjoxNjY4Mzk4MDYxfQ._Q5ZaBP5FSa09s0FCn7CBcMCty9hkM5TDu5q1wTvwB8",
        "event_type": "BINDING",
        "pub_time": 1667343986249
      },
      "payload": "Your DePIN application data"
    },
    ...
  ]
}
```

### The header

The header nested object is intended for W3bstream to authorize the message and route it to the right handler.

<mark style="color:blue;">**`token:`**</mark>`<string>` is a device authorization token generated inside the project to which the message is sent. The token is case sensitive.

<mark style="color:blue;">**`event_type:`**</mark>`<string>` this is the event type to be triggered by W3bstream once the message has been received and authenticated. It can be anything, as long as it's matched to an event strategy of the destination W3bstream Project. The event type is case sensitive.

<mark style="color:blue;">**`pub_time`**</mark>`:<number>` this is the timestamp when the message was actually sent.

### The payload

The message payload must be a string, and it can contain any type of data. Once the message reaches W3bstream and an event routing strategy for the message event type is matched, the target handler function can access the decoded payload using a specific W3bstream's dedicated function.&#x20;

The event routing determines how the message is handled, and it is defined within the W3bstream project that receives the message. The target handler function is a user-defined function within the project's applet that is responsible for processing the message payload.&#x20;
