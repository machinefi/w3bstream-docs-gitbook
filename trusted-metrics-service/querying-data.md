# Querying Data

## Endpoints

The public endpoint of the Trusted Metrics API is the following:

[http://devnet.w3bstream.com](http://devnet-prod.w3bstream.com:9090/)

## Querying the API

The Trusted Metrics provided by W3bstream can be accessed either through the Prometheus UI or via API requests.

### Prometeus UI

The Prometheus UI offers a user-friendly interface accessible at /graph on the Prometheus server. It allows you to input any expression and view the corresponding results in either a table format or graphed over time. The documentation for the `PromQL` expression is available to guide you in constructing queries effectively.

Query Examples:

1. Total Number of Events:&#x20;

```promql
sum by (account, project) (inbound_events_metrics)
```

1. Daily Active Devices

```promql
count(count_over_time(inbound_events_metrics[1d])) by (account, project
```

1. Device Growth

```promql
sum by (account, project) (publishers_metrics)
```

By utilizing the Prometheus UI and crafting the appropriate queries, developers can gain valuable insights into their project's performance and make informed decisions.&#x20;

{% hint style="info" %}
The [Prometheus documentation](https://prometheus.io/docs/prometheus/latest/querying/basics/) provides further details on how to effectively leverage the `PormQL` expression language for querying metrics.
{% endhint %}

### API requests

The Prometheus Server provided by the Trusted Metrics Center supports instant and range queries through its API, accessible at `/api/v1`.&#x20;

Here are examples of API queries:

1.  Total Number of Events:

    ```bash
    curl -g 'https://prometheus-devnet-staging.w3bstream.com/api/v1/query?query=sum%20by%20%28account%2C%20project%29%20%28inbound_events_metrics%29'
    ```
2.  Daily Active Devices:

    ```bash
    curl -g 'https://prometheus-devnet-staging.w3bstream.com/api/v1/query?query=count%28count_over_time%28inbound_events_metrics%5B1d%5D%29%29%20by%20%28account%2C%20project%29'
    ```
3.  Device Growth:

    ```bash
    curl -g 'https://prometheus-devnet-staging.w3bstream.com/api/v1/query?query=sum%20by%20%28account%2C%20project%29%20%28publishers_metrics%29'
    ```

These example queries demonstrate how to retrieve specific metrics using the API. By making the appropriate API request, developers can obtain information such as the total number of events, daily active devices, and device growth.&#x20;

{% hint style="info" %}
The [Prometheus documentation](https://prometheus.io/docs/prometheus/latest/querying/api/) provides further guidance on constructing queries and understanding the response format for effective analysis of the metrics.
{% endhint %}
