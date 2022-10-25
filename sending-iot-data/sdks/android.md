# Android

**W3streamKit** is the Android SDK of W3bstream. This is an alpha version, which may be changed over time.

{% embed url="https://github.com/machinefi/w3bstream-android-sdk" %}

{% hint style="warning" %}
**Please notice that the Android emulator does not support location service, please use a real device to test.**
{% endhint %}

### Quick Start

You can use AndroidStudio to open the project, then sync the project, and then run the demo on your Android phone or emulator. Notice. Android emulator does not support location service, please use a real machine to test.

### Integration

Import the module `w3bstream` into your project as a module, and add `implementation project(path: ':w3bstream')` in your `build.gradle` file. Then sync your project.

### Initialization

```java
private val config by lazy {
        W3bStreamKitConfig(
            SIGN_API,
            mutableListOf(SERVER_API),
        )
    }

    private val w3bStreamKit by lazy {
        W3bStreamKit.Builder(config).build()
    }
```

### Authentication

```java
    w3bStreamKit.authenticate(imei, sn, pubKey, signature)
```

### Get the public key

```java
  w3bStreamKit.getPublicKey()
```

### Sign data

```java
w3bStreamKit.sign(data)
```

### Send data to W3bstream

{% hint style="info" %}
Make sure the type for _data_ _string_
{% endhint %}

```java
w3bStreamKit.upload("{"imei":"126378", "latitude":34.09589161, "location":106.42410187}")
```

### Utility

#### Set the W3bstream endpoint

```java
// Non-secure
w3bStreamKit.addServerApi(api)
// Secure
w3bStreamKit.addServerApis(apis)
```

#### Remove the W3bstream endpoint

```javascript
javw3bStreamKit.removeServerApi(api)
```
