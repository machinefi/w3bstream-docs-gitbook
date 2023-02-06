# Technical Framework

## Layers of the framework

The design of _WSIoTSDK_ follows a layered approach, comprising **five layers**, from top to bottom:&#x20;

* _DID Communication_ _messaging_
* _Identity_ _and_ _credential_
* _Cryptographic service_
* _Cryptographic primitive_
* _Root of trust_

Each layer consists of multiple components in the _WSIoTSDK_, enabling developers to customize the SDK flexibly to meet hardware constraints and application requirements.

## Cryptographic Service & Primitives&#x20;

In particular, the _Cryptographic Service_ and _Cryptographic Primitive_ layers can be split into five different components, shown in the image. Each component contains a number of sub-components.

#### Cryptographic Services Layer

These sub-components implement services such as key management, secure storage, audit logging, etc.

#### Cryptographic Primitives

These sub-components contain cryptography libraries suitable for various embedded devices.

#### PSA Abstraction (PSA\_AL)

This sub-layer provides the PSA abstraction and API-level support.

#### Hardware Abstraction (HAL)

This sub-layer provides hardware abstraction for various embedded platforms.

#### Support

These sub-components, highlighted in the pink rectangle below) provide functionalities for configuration, compilation and testing of the entire SDK.

<figure><img src="../../.gitbook/assets/SDK.png" alt=""><figcaption><p>Cryptographic service &#x26; Criptographic primitive layers</p></figcaption></figure>

In practice, developers can customize _WSIoTSDK_ to meet their requirements by selecting proper sub-components from all available components. Note that sub-components in the image above are grouped by color and those within the same color group could be used as a specific customization of _WSIoTSDK_.&#x20;

Here we provide some customization examples:

IoTeX Firmware + MbedTLS + Hardware Acceleration

This combination is suitable for embedded platforms that do not support TrustZone®, e.g., Raspberry Pi. In this mode, users can use the complete PSA APIs to implement cryptographic operations.

TF-M + MbedTLS + Hardware CryptoLib

This combination is suitable for Cortex-M series MCUs with TrustZone® support (e.g., Cortex-M23/M33/M55).

IoTeX Firmware + TinyCrypt

This combination is suitable for embedded platforms with highly constrained hardware resources (e.g., low-end Arduino boards). In this case, users need to customize _WSIoTSDK_ for addressing specific hardware resource challenges.

## The PSA Abstraction Layer

_WSIoTSDK_ has been designed to be modular and easily expandable through the use of different cryptographic libraries. To facilitate this, the cryptographic functions used in the SDK have been encapsulated in a cryptographic module. All interaction with the cryptographic module should be done via the industry standardised PSA API. This allows for decoupling the crypto backend and the rest of the components of the SDK.

Sub-components in the PSA abstraction layer (PSA\_AL) are shown in the image below:

<figure><img src="../../.gitbook/assets/PAL.png" alt=""><figcaption><p>PSA layer</p></figcaption></figure>

Currently, the only supported cryptographic library by the SDK is [MbedTLS 3.2.1](https://www.trustedfirmware.org/projects/mbed-tls/). However, other libraries are planned to be supported in the near future, such as [TinyCrypt](https://docs.zephyrproject.org/3.2.0/services/crypto/tinycrypt.html).&#x20;

In the case of TinyCrypt, the library will need to be integrated with the SDK through a PSA abstraction layer. IoTeX will provide this PSA abstraction layer. Theoretically, any other cryptographic library could be integrated with _WSIoTSDK_, as long as a PSA abstraction layer is provided for it.&#x20;

Contributions from third party to port other libraries to _WSIoTSDK_ are also highly appreciated.
