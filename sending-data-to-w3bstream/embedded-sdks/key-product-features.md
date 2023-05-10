# Key Product Features

#### Unified Framework

_WSIoTSDK_ provides a unified code implementation and standardised interface abstraction. As a result, developers only need to call the standard PSA APIs when using _WSIoTSDK_ for performing cryptographic operations, thereby significantly reducing the maintenance costs for interacting with various cryptographic libraries. Moreover, _WSIoTSDK_ supports multiple operating systems such as Windows, Linux, and macOS, which facilitates developers to complete fast development and integration.

#### Flexible Configuration

The design and development of _WSIoTSDK_ adopt a "layer-component-subcomponent" methodology in which communications among components are based on standard interfaces. Such an approach effectively reduces coupling between layers and components and enables developers to choose sub-components via configuration files to meet the requirements of various applications and development environments.

#### High Reliability

The rich sub-components in _WSIoTSDK_ are popular open-source software and the updates of which are maintained by IoTeX. Hence developers do not need to update those sub-components separately and just recompile _WSIoTSDK_ to get the latest version. Moreover, _WSIoTSDK_ provides complete test cases for PSA APIs and integrates PSA Certified APIs Architecture Test Suite for testing on multiple operating system platforms and embedded devices.

### File Structure

The following figure is an example of the current _WSIoTSDK_ file structure:

| Directory | Sub directory | Description                                           |
| --------- | ------------- | ----------------------------------------------------- |
| component | crypto        | The cryptographic primitive sub-component             |
|           | layer         | The code for the Pebble Tracker PSA abstraction layer |
|           | services      | The cryptographic service sub-component               |
| doc       |               | The documentation of _WSIoTSDK_                       |
| include   |               | The user facing header files                          |
| test      |               | The complete PSA API test routines                    |
| examples  |               | _WSIoTSDK_ usage examples                             |

