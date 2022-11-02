# iOS

{% embed url="https://github.com/machinefi/w3bstream-ios-sdk" %}

### Build the framework

Clone the iOS W3bstream SDK then build it with:

```
./makeframework.sh
```

The framework will be generated in the build directory for both ARM and x86 platforms.

### Integration

{% tabs %}
{% tab title="Simulator" %}
Drag `build/Release-iphonesimulator/W3bStream.framework` into your project.

Make sure you select the `Copy` option.
{% endtab %}

{% tab title="Device" %}
Import `build/Release-iphoneos/W3bStream.framework`.&#x20;

If you encounter private key-related exceptions, in the `General` tab, open the _Frameworks/_ _Libraries, then Embedded Content_ section, and change `Do Not Embed` to `Embed & Sign. For more`More details refer to [Embedding Frameworks In An App](https://developer.apple.com/library/archive/technotes/tn2435/\_index.html)
{% endtab %}
{% endtabs %}

### Initialization

```swift
let httpsurl1 = URL(string: "https://xxxxx")!
let httpsurl2 = URL(string: "https://xxxxx")!
let httpsurl3 = URL(string: "https://xxxxx")!
let wsurl = URL(string: "wss://xxxxx")!
let urls = [httpsurl1, httpsurl2, httpsurl3, wsurl]
let w3bStream = W3bStream(urls: urls)
```

### Sending data to W3bstream

```swift
//prepare the data
let jsonString = "{\"latitude\":\"36.652061\",\"longitude\":\"117.120144\",\"shakeCount\": 4,\"timestamp\":1660027882, \"imei\":\"100558946403437\"}"
//upload
w3bStream.upload(data: jsonString) { data, err in } 
```
