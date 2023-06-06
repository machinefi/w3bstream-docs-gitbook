# Storing Device Data

Currently, as part of W3bstream's DevNet release, each W3bstream project is equipped with a dedicated SQL database. This database serves as a valuable resource for storing machine data, application status, and more.

{% hint style="info" %}
However, it's important to note that the SQL database solution is temporary and intended for the W3bstream DevNet phase. In the future, developers will have more options to store IoT data in a variety of locations, including decentralized storage systems. W3bstream will provide storage modules that enable applets to seamlessly access and interact with data stored in these storage environments.

\
This future enhancement will empower developers to leverage the benefits of the different storage solutions, while maintaining the flexibility and scalability needed for IoT applications.
{% endhint %}

## Using the SQL database

When you create a project in W3bstream, a dedicated SQL database is automatically created and made accessible to the project. This SQL database allows you to store and retrieve structured data for your project. To interact with the SQL database from your Applet, the SDKs provide two functions: `ExecSQL` and `QuerySQL`.

#### ExecSQL

The `ExecSQL` function is designed for executing queries that modify the database rows, such as inserting, deleting, or altering rows. It returns an error code or 0 on success. You can use `ExecSQL` to perform operations that modify the database structure or content.

#### QuerySQL

On the other hand, the `QuerySQL` function is suitable for running queries that retrieve data from the database. It is used when you expect the query to return a certain number of rows. You can use `QuerySQL` to fetch data from the SQL database based on specific conditions or criteria.

#### Example: Storing and Retrieving Data

Before you can start using the database, it's important to create the necessary tables to store your data. In our example, we'll be using the payload discussed in the previous section[sending-messages-to-w3bstream.md](sending-messages-to-w3bstream.md "mention"). From the Data section of the project editor in W3bstream Studio, we'll create a database table named "`iot_data`" with three columns: "`device_id`" (string), "`temperature`" (float64), and "`timestamp`" (string).

To learn how to create database tables, you can watch the short video tutorial in the how-to section:

{% content-ref url="../get-started/w3bstream-studio/create-database-tables.md" %}
[create-database-tables.md](../get-started/w3bstream-studio/create-database-tables.md)
{% endcontent-ref %}

Let's look at an example that demonstrates storing a record in the SQL database and reading data back from it:

{% tabs %}
{% tab title="AssemblyScript" %}
```typescript
import { GetDataByRID, JSON, ExecSQL, QuerySQL, Log } from "@w3bstream/wasm-sdk";
import { Float64, String } from "@w3bstream/wasm-sdk/assembly/sql";
export { alloc } from "@w3bstream/wasm-sdk";

export function my_handler(rid: i32): i32 {
  // F the message payload
  const payload_str = GetDataByRID(rid);
  const payload_obj = JSON.parse(payload_str) as JSON.Obj;
  // Read the device_id from the payload object
  const device_id = payload_obj.getString("device_id");
  if (device_id == null) return 1;
  // Get the data nested object from the payload
  const data_obj = payload_obj.getObj("data") as JSON.Obj;
  // Read data.temperature
  const temperature = data_obj.getFloat("temperature");
  if (temperature == null) return 1;
  // Read data.timestamp
  const timestamp = data_obj.getString("timestamp");
  if (timestamp == null) return 1;
  // Save the record in the SQL database
  const value = ExecSQL(`INSERT INTO "iot_data" (device_id, timestamp, temperature) VALUES (?,?,?);`, 
                        [ new String(device_id.valueOf()), 
                          new Float64(temperature.valueOf()), 
                          new String(timestamp.valueOf())
                        ]
                        );
  // Read back device ids for which temperature is less than 20
  const results = QuerySQL(`SELECT device_id FROM "iot_data" WHERE temperature < 20;`);
  // Log the results
  Log("Device ids where temperature < 20");
  Log(results),
  return 0;
}
```
{% endtab %}

{% tab title="Rust" %}
```rust
use ws_sdk::log::log_info;
use ws_sdk::stream::get_data;
use ws_sdk::database::sql::*;

use anyhow::Result;
use serde::Serialize;
use serde_json::Value;

pub fn my_handler(rid: i32) -> i32 {
    // Fetch the message payload
    let payload_str = get_data(rid).unwrap();
    let payload_obj: JSONValue = serde_json::from_str(&payload_str).unwrap().into();

    // Read the device_id from the payload object
    let device_id = payload_obj["device_id"].as_str().unwrap();
    if device_id.is_empty() {
        return 1;
    }

    // Get the data nested object from the payload
    let data_obj = payload_obj["data"].as_object().unwrap();

    // Read data.temperature
    let temperature = data_obj["temperature"].as_f64().unwrap();
    if temperature.is_nan() {
        return 1;
    }

    // Read data.timestamp
    let timestamp = data_obj["timestamp"].as_str().unwrap();
    if timestamp.is_empty() {
        return 1;
    }

    // Save the record in the SQL database
    let _ = execute(
        "INSERT INTO \"iot_data\" (device_id, timestamp, temperature) VALUES (?,?,?);",
        &[&String(device_id.to_owned()), &Float64(temperature), &String(timestamp.to_owned())],
    ).unwrap();

    // Read back device ids for which temperature is less than 20
    let results = query(
        "SELECT device_id FROM \"iot_data\" WHERE temperature < 20;",
        &[],
    ).unwrap();

    // Log the results
    Log("Device ids where temperature < 20").unwrap();
    Log(&results).unwrap();

    0
}
```
{% endtab %}

{% tab title="Go" %}

{% endtab %}
{% endtabs %}
