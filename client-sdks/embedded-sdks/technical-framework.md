# Technical Framework

<div>

<img src="https://github.com/machinefi/w3bstream-iot-sdk/blob/main/doc/img/SDK.png" alt="">

 

<figure><img src="../../.gitbook/assets/Overview.png" alt=""><figcaption><p>SDK layers</p></figcaption></figure>

</div>

The design of _WSIoTSDK_ follows a layered approach, comprising of five layers, from top to bottom: the DIDComm messaging layer, the identity and credential layer, the cryptographic service layer, the cryptographic primitive layer, and the root of trust layer. Each layer consists of multiple components in the _WSIoTSDK_, enabling developers to customise the SDK flexibly to meet hardware constraints and application requirements.

The five components in the cryptographic service layer and cryptographic primitive layer are shown below and each component may contain a number of sub-components.

<figure><img src="../../.gitbook/assets/SDK.png" alt=""><figcaption><p>SDK components</p></figcaption></figure>

* Cryptographic Services：These sub-components implement services such as key management, secure storage, audit logging, etc.
* Cryptographic Primitives：These sub-components contain cryptography libraries suitable for various embedded devices.
* PSA Abstraction Layer (PSA\_AL)：This sub-layer provides the PSA abstraction and API-level support.
* Hardware Abstraction Layer (HAL)：This sub-layer provides hardware abstraction for various embedded platforms.
* Support Components (pink area)：These sub-components provide functionalities for configuration, compilation and testing of the entire SDK.

In practice, developers are able to customise _WSIoTSDK_ to meet their requirements by selecting proper sub-components from one or multiple components above. Note that each sub-component in the above figure is marked with a colour and sub-components with the same colour could be used as a specific costomisation of _WSIoTSDK_. Here we provide some customisation examples below.

1. IoTeX Firmware + MbedTLS + Hardware Acceleration: This combination is suitable for embedded platforms that do not support TrustZone®, e.g., Raspberry Pi. In this mode, users can use the complete PSA APIs to implement cryptographic operations.
2. TF-M + MbedTLS + Hardware CryptoLib: This combination is suitable for Cortex-M series MCUs with TrustZone® support (e.g., Cortex-M23/M33/M55).
3. IoTeX Firmware + TinyCrypt: This combination is suitable for embedded platforms with highly constrained hardware resources (e.g., low-end Arduino boards). In this case, users need to customise _WSIoTSDK_ for addressing specific hardware resource challenges.

In _WSIoTSDK_, the components in the PSA abstraction layer (PSA\_AL) are shown in the figure below.

<figure><img src="../../.gitbook/assets/PAL.png" alt=""><figcaption><p>PSA layer</p></figcaption></figure>

_WSIoTSDK_ has been designed to be modular and easily expandable through the use of different cryptographic libraries. To facilitate this, the cryptographic functions used in the SDK have been encapsulated in a cryptographic module. All interaction with the cryptographic module should be done via the industry standardised PSA API. This allows for decoupling between the crypto backend and the rest of the components of the SDK.\
Currently the only supported cryptographic library by IoTeX Firmware is MbedTLS 3.2.1. However, other libraries are planned to be supported in the near future, such as TinyCrypt. In the case of TinyCrypt, the library will need to be integrated with the SDK through a PSA abstraction layer. IoTeX will provide this PSA abstraction layer. Theoretically, any other cryptographic library could be integrated with _WSIoTSDK_, as long as a PSA abstraction layer is provided for it. If any third party contributors are willing to port other libraries to _WSIoTSDK_, their contribution will be highly appreciated.
