# Running a Node

This document contains the requirements and instructions to run a W3bstream node.

{% hint style="warning" %}
**Notice**: W3bstream is under development. The current deocumentation refers to the **W3bstream Code Preview**, and is subject to frequent changes.
{% endhint %}

### Supported Blockchains

Currently, W3bstream supports the IoTeX Blockchain, Ethereum 2.0, and any Ethereum-compatible chain.

### Requirements

#### Tokens and Staking Requirements

Currently, there are no token balance or staking requirements to run a W3bstream node.

#### Hardware requirements

Because your W3bstream node will act as a network endpoint for devices to send their data, you should run it on a serve that has a fixed IP address, publicly accessible from the Internet.

The minimum hardware requirements to run a W3bstream node are:

* 2 Cores, 2 GB RAM, 10 GB storage, 100 Mbit network

Recommended requirements to get started running a W3bstream node are:

* 4 Cores, 4 GB RAM, 20 GB storage, 100 Mbit network

Since the performances of your node are closely linked to the number of client devices, the volumes of IoT data, and the complexity of the application logic, it's recommended to  accurately evaluate hardware requirements.&#x20;

#### Supported OS

The W3bstream runtime supports Linux and MacOS systems.&#x20;

#### Blockchain client

For your W3bstream node to be able to interact with a blockchain application (e.g., react to smart contract events, send proofs to smart contracts), you will also need access to a blockchain gateway. You can use official or third-party gateways to access the blockchain of your choice:

[IoTeX Blockchain public RPC gateways](https://docs.iotex.io/dapp-development/web3-development/rpc-endpoints)

[Ethereum Blockchain public RPC gateways](https://ethereumnodes.com/)

If you decide to run your own gateway, it's highly recommended that you run it on a separate server. Below, you find links to the instructions on how to run your blockchain gateway for IoTeX and Ethereum:

**Run an IoTeX full-node**

{% embed url="https://delegates.iotex.io/get-started/node-configuration" %}
Configure and run your own IoTeX Gateway
{% endembed %}

**Run an Ethereum full-node**

{% embed url="https://ethereum.org/en/run-a-node/" %}

### Run using Docker

The recommended way to run a W3bstream node is by using [Docker](https://www.docker.com/). With docker, you can easily fetch new releases and update the W3bstream runtime, you won't have to configure a development environment to build the runtime from the source code yourself.

Make sure you have Docker and Docker-Compose installed in your system:

{% embed url="https://www.docker.com/" %}
Install Docker
{% endembed %}

#### Pull the Docker image

Once you have Docker installed in your system, make sure your user is allowed to run the docker command with:

```bash
 sudo usermod -aG docker $USER
```

Log out and log back in so that your group membership is re-evaluated, then verify that you can run `docker` commands without `sudo`

```bash
docker run hello-world
```

Pull the W3bstream runtime docker image with:

```bash
docker pull w3bstream/w3bstream:latest
```

Use a `docker-compose.yaml` file with the following content to quickly start the node using the _docker-compose_ command:

```yaml
version: '3.0'
services:
  w3bstream:
    image: iotex/w3bstream:v3
    container_name: w3bstreamapp
    restart: always
    command: sh -c "/init.sh"
    environment:
      POSTGRES_USER: test_user
      POSTGRES_PASSWORD: test_passwd
    ports:
      - "5432:5432"
      - "8888:8888"
      - "3000:3000"
    healthcheck:
      test: [ "CMD-SHELL", "pg_isready -U test_user" ]
      interval: 5s
      timeout: 5s
      retries: 5
```

#### Start the W3bstream node with:

```bash
docker-compose -f docker-compose.yaml up
```

You will see a log similar to the one below:

```bash
Creating w3bstreamapp ... done
Attaching to w3bstreamapp
w3bstreamapp | Starting PostgreSQL 13 database server: main.
w3bstreamapp | Starting network daemon:: mosquitto.
w3bstreamapp | {"@lv":"debug","@prj":"srv-applet-mgr","@ts":"20221008-150651.409Z","cost":"89.40725ms","msg":"SELECT table_schema,table_name,column_name,data_type,is_nullable,column_default,character_maximum_length,numeric_precision,numeric_scale FROM information_schema.columns WHERE (table_schema = 'applet_management') AND (table_name IN ('t_account','t_applet','t_event_log','t_instance','t_project','t_publisher'))"}
...
w3bstreamapp | [Kit] 	jwt.Auth middleware.ContextAccountAuth project.GetProjectByProjectID
w3bstreamapp | [Kit] srv-applet-mgr@0.0.1 listen on :8888
w3bstreamapp | username: admin
w3bstreamapp | password: TB12gkOm
w3bstreamapp | please remember it
w3bstreamapp | > iotex-dapp-sample@0.1.0 start /w3bstream/frontend
w3bstreamapp | > next start
w3bstreamapp | 
w3bstreamapp | ready - started server on 0.0.0.0:3000, url: http://localhost:3000
w3bstreamapp | info  - Loaded env from /w3bstream/frontend/.env

```

Notice at the end of the log, you will find the admin credentials to log in and interact with the W3bstream runtime:

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### Run using the CLI

<mark style="background-color:red;">TODO</mark>
