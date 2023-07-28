# Querying the API

{% hint style="info" %}
**We are actively working to enhance and expand these pages. If you have any questions, feel free to reach out to us at** [**support@iotex.io**](mailto:support@iotex.io)**. We appreciate your patience and invite you to visit this page again soon!**
{% endhint %}

When you require access to Trusted Metrics data from your code, you can leverage the capability to query the Trusted Metrics API directly. This feature empowers you to create custom dashboards, seamlessly integrate with other tools or platforms, and conduct advanced data analysis.&#x20;

## Generating a Query API Endpoint

To interact with the W3bstream Trusted Metrics API, you need to follow a specific process. You first create an API key for your application, then you generate one or more queries using the Query Designer.&#x20;

Once your queries are defined and saved, you can generate unique API endpoints for each query, which allows you to fetch the results from your code by making API requests to the respective endpoint.

## Create a Client API Key

Before you can query Trusted Metrics from your client applications, you first need to create an API Key from your [profile settings page](https://metrics-staging.w3bstream.com/settings/api):&#x20;

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Notice that you only need a single API key to query multiple endpoints. However, it is advisable to create a different API key for each of your client applications that need to interact with Trusted Metrics.
{% endhint %}

## Find the Query API Endpoint

Once you have created an API Key for your client, you can access the API endpoint for your desired query directly from the [Trusted Metrics Query Designer](https://metrics-staging.w3bstream.com/queries).&#x20;

Follow these simple steps:

1. In the Queries List panel on the left side, select the query you want to access.
2. Click the API button.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

3. In the next dialog, copy the API Endpoint for the query

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

4. Make sure you edit the endpoint by adding your API Key.

By following these steps, you can easily obtain the specific API Key for your chosen query, enabling seamless access to the query results from your client application. This allows you to efficiently integrate with Trusted Metrics and retrieve the necessary data for your project analysis and visualization needs.
