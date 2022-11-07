# iOS Client SDK

The iOS Client SDK for W3bstream implements the message protocol to send data to a W3bstream node.&#x20;

{% hint style="info" %}
<img src="../.gitbook/assets/image (2).png" alt="" data-size="line"> <mark style="color:purple;"></mark> [**Checkout the SDK on GitHub**](https://github.com/machinefi/w3bstream-ios-sdk)
{% endhint %}

## Installation

This SDK is built with Xcode 14 and supports both arm and x86 platforms. If you installed a previous version of Xcode, please run the `makeframework.sh script` included in the repository.

To install the SDK, just clone the repository, locate `MFW3bStream.xcframework`  in the `out` folder, and drop it into your project. When releasing, make sure to select **`Copy`** option.&#x20;

## Usage

### Initialize the instance

```swift
let w3bStream = W3bStream(urls: [URL(string: "https://example")!])
```

### Sending data to a W3bstream node

```swift
w3bStream.upload(payload: "payload", publisherKey:"key", publisherToken:"token") { data, err in
}
```
