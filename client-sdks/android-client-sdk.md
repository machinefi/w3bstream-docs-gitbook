# Android Client SDK

The Android Client SDK for W3bstream implements the message protocol to send data to a W3bstream node.&#x20;

> **The Android SDK is a Work in Progress.**
>
> [Checkout the repository on GitHub](https://github.com/machinefi/w3bstream-android-sdk)

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
