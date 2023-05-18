# Message API

W3bstream provides HTTP and MQTT network endpoints that allow data messages to be sent between running projects. Each W3bstream message consists of a **header** object, which contains fields related to the messaging protocol (such as authentication information and the target event handler), and a **payload** string that contains the message to be processed. The target event handler is specified as the name of an event within the W3bstream project that will be raised when the message is received.

An example message is shown below:

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
    }
  ]
}
```

### The header

The header nested object is intended for W3bstream to authorize the message and route it to the right handler.

<mark style="color:blue;">**`pub_id:`**</mark>`<string>` is the identifier of a valid Publisher defined in the destination W3bstream Project.

<mark style="color:blue;">**`token:`**</mark>`<string>` is the authorization token associated with the Publisher Identifier (`pub_id`)

<mark style="color:blue;">**`event_type:`**</mark>`<string>` this can be anything, as long as it's matched in an event strategy of the destination W3bstream Project

<mark style="color:blue;">**`pub_time`**</mark>`:<number>` this is the timestamp when the message was actually sent.

### The payload

The message payload must be a string that has been encoded using the base64 scheme, and it can contain any type of data. Once the message reaches W3bstream and a rule for the message event type is matched, the target handler function can access the decoded payload using a specific W3bstream's dedicated function.&#x20;

The event rule determines how the message is handled, and it is defined within the W3bstream project that receives the message. The target handler function is a user-defined function within the project's applet that is responsible for processing the message payload once it has been decoded.
