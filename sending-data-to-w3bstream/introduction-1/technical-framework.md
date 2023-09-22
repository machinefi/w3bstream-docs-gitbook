# Technical Framework

## Components of the IoT SDK

The W3bstream IoT SDK provides a reference implementation of the ARM Platform Security Architecture API. It is assumed that the reader is familiar with the specification, which can be found at [Platform Security Architecture Resources](https://developer.arm.com/architectures/security-architectures/platform-security-architecture).

The SDK is made up of several main components: Communication and Messaging, Identity and Credential Services, and Cryptography Services and Primitives.

{% hint style="info" %}
The current version of the SDK only includes the Cryptography component, while the remaining components will be available in a future version.
{% endhint %}

## The Cryptography component

The Cryptography component of the WSIoTSDK consists of several modules that enable developers to build secure systems. These modules include:

1. **PSA Crypto API:** an implementation of the Platform Security Architecture Crypto API.
2. **Cryptographic primitives:** a set of cryptographic primitives such as TRNG, PRNG, AES, hash, RSA, ECC, KDF, and more.
3. **Cryptographic services:** a set of secure services such as secure storage, remote attestation, and audit logging.
4. **HAL:** a hardware abstraction layer that allows developers to access hardware-specific functions such as secure elements and hardware acceleration modules.
5. **Tooling:** a set of tools, scripts, and examples to configure, build, and test the SDK.
6. **Root of Trust:** a foundation of the SDK that ensures the integrity of the security services.

The Cryptographic component of the SDK is designed with modularity in mind, allowing developers to create custom configurations based on their specific hardware and application needs. Different modules can be selectively included in each configuration, providing developers with flexibility to tailor their solution while minimising unnecessary features. Each configuration is optimized for a particular type of board and application, offering a flexible and efficient approach to implementation.\
The SDK also includes configuration presets that are specifically designed for popular boards and applications, offering a quick and easy way for developers to get started without having to create a custom configuration from scratch. However, users have the flexibility to create their own configurations if the provided ones don't meet their specific needs.

Below are the some of the configuration presets that come with the SDK:

* TF-M or TF-A: for Cortex-M or Cortex-A series MCUs with TrustZone® support. Provides PSA API, cryptographic primitives, RoT, and HAL components managed by TF-A or TF-M using MbedTLS. Cryptographic services are also provided by TF-M or TF-A.
* Iotex-F + MbedTLS: for embedded platforms that do not support TrustZone®. For example, Raspberry Pi. Provides PSA API, cryptographic primitives, RoT, and HAL components managed by Iotex-F using MbedTLS. However, this configuration does not provide cryptographic services.
* Arduino: for resource-constrained devices that support the Arduino framework. Provides PSA API, cryptographic primitives, RoT, and HAL components managed by the Arduino PSA layer module. The cryptographic primitives used are from TinyCrypt. This configuration does not provide cryptographic services.
* Pebble Tracker: for the Pebble Tracker. Provides PSA API, cryptographic primitives, RoT, and HAL components managed by the Arduino PSA layer module. The cryptographic primitives used are from MbedTLS. This configuration does not provide cryptographic services. However, the user can access secure services exposed by Zephyr.

## The Communication component

The communication component will be provided in later versions of the SDK.&#x20;

## The Identity and Credentials component

The identity and credentials component will be provided in later versions of the SDK.&#x20;
