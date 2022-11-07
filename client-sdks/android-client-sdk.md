# Android Client SDK

The Android Client SDK for W3bstream implements the message protocol to send data to a W3bstream node.&#x20;

{% hint style="info" %}
<img src="../.gitbook/assets/image (2).png" alt="" data-size="line"> <mark style="color:purple;"></mark> [**Checkout the SDK on GitHub**](https://github.com/machinefi/w3bstream-android-sdk)****
{% endhint %}

## Installation

Import `w3bstream` into your project and sync it:

```jsx
implementation 'com.w3bstream:w3bstream-android:1.0.0'
```

## Usage

### Initializing the instance

```jsx
private val w3bStream by lazy {
   W3bStream.build(HttpService())
}
```

### Sending data to a W3bstream node

```tsx
val response = w3bStream.publishEvent(url, payload, publisherKey, publisherToken)
```
