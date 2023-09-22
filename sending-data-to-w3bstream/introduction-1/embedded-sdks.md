# Linux Embedded

{% hint style="info" %}
**Notice**: The Linux Embedded Client SDK does not include a W3bstream Client object. To create API calls, you will need to utilize the HTTP/MQTT clients directly. Detailed examples can be located within the SDK repository for your reference.

[Go to the examples folder...](https://github.com/machinefi/web3-iot-sdk/tree/main/examples)
{% endhint %}

## Set up the build environment

Iotex SDK officially supports a limited set of build environments and setups. In this context, official support means that the environments listed below are actively used by team members and active developers, hence users should be able to recreate the same configurations by following the instructions described below.\
In case of problems, the Iotex SDK team provides support only for these environments, but building in other environments can still be possible.

The following environments are supported:

### **Docker container (Ubuntu 22.04)**

Install the VS Code [Remote: Dev containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).\
Open the repository inside VS Code and click the "Open Workspace in Container" pop up that appears. More info on using dev containers in VS Code in the [VS Code documentation](https://code.visualstudio.com/docs/devcontainers/containers#\_open-an-existing-workspace-in-a-container).

### **Linux (Ubuntu 18.04 or 22.04)**

Run the following command to install the required dependencies:

```bash
sudo apt-get install -y cmake git curl wget build-essential libssl-dev python3
```

### **Windows 11 x64**

Install the following dependencies:

* Git client: [https://git-scm.com/download/win](https://git-scm.com/download/win)
* CMake: [https://cmake.org/download/](https://cmake.org/download/)
* MinGW32: [https://sourceforge.net/projects/mingw-w64/files/](https://sourceforge.net/projects/mingw-w64/files/)
* Python3 and pip (included by default): [https://www.python.org/downloads/](https://www.python.org/downloads/)

## Get the source code

Run the following command to clone the repository:

```bash
git clone https://github.com/machinefi/web3-iot-sdk.git
```

## Build

The build process is managed by CMake. The build can be customized by passing CMake options.\
For a full list of CMake options see the main [CMakeLists.tx](https://github.com/machinefi/w3bstream-iot-sdk/blob/main/CMakeLists.txt). Below is a description of the most common ones:

* **CRYPTO\_IMPL:** the crypto library to use. Possible values: "MbedTLS" or "TinyCrypt". Defaults to "MbedTLS". Note that TinyCrypt is not supported yet.
* **BUILD\_IOTEX\_F:** build the IoTeX Firmware component. Defaults to ON.
* **BUILD\_PSA\_TEST\_SUITE:** build the PSA Architecture test suite. Defaults to OFF.
* **BUILD\_EXAMPLE\_\<example\_name>:** build any of the examples in the examples directory. Defaults to OFF.
* **GIT\_SUBMODULE\_UPDATE:** download or update any dependencies specified as submodules. Defaults to ON.

For example, if you want to build the SDK using Iotex Firmware + MbedTLS + PSA test suite, you can run the following commands:

```bash
# Configure the build components and place the output in ./build-out
cmake -DGIT_SUBMODULE_UPDATE=ON -DBUILD_IOTEX_F=ON -DCRYPTO_IMPL="MbedTLS" -DBUILD_PSA_TEST_SUITE=ON -S ./ -B ./build-out
# Compile all targets
cmake --build build-out --target all
```

Once the build finishes, you can run the tests executable using the following command:

```bash
./build-out/test/psa-arch-tests-crypto
```

You should see output similar to the one below:

```bash
...
******************************************

TEST: 260 | DESCRIPTION: Testing crypto AEAD APIs | UT: psa_aead_abort
[Info] Executing tests from non-secure
[Check 1] Test psa_aead_abort - Encrypt - CCM - AES
[Check 2] Test psa_aead_abort - Encrypt - GCM - AES
[Check 3] Test psa_aead_abort - Decrypt - CCM - AES
[Check 4] Test psa_aead_abort - Decrypt - GCM - AES
[Check 5] Test psa_aead_abort with all initializations

TEST RESULT: PASSED

******************************************

......

************ Crypto Suite Report **********
TOTAL TESTS     : 63
TOTAL PASSED    : 61
TOTAL SIM ERROR : 0
TOTAL FAILED    : 0
TOTAL SKIPPED   : 2
******************************************
```

## Examples

Examples to demonstrate the usage of the SDK can be found in the [examples](https://github.com/machinefi/web3-iot-sdk/tree/main/examples) of the SDK. Each example contains a README file with usage instructions.
