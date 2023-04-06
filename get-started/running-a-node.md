# Accessing W3bstream

Although W3bstream is still under development, you can already start building and testing DePIN projects using the W3bstream DevNet release.&#x20;

## Access the public DevNet

The easiest way to access the W3bstream DevNet is to open a Metamask-enabled browser and navigate to the public W3bstream service officially deployed and maintained by the IoTeX team, accessible at:

{% hint style="success" %}
[**https://dev.w3bstream.com**](https://dev.w3bstream.com)
{% endhint %}

Just log in with a Metamask account to access your projects page:

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## &#x20;Run your W3bstream node

The recommended way to run W3bstream DevNet on your machine is by using Docker. Docker enables you to effortlessly fetch new releases and update W3bstream's runtime without having to configure a development environment and build the runtime from source code manually.

<details>

<summary>Install Docker-Compose </summary>

Install Docker from the official website:

[https://www.docker.com](https://www.docker.com)

Once you have Docker installed in your system, make sure your user is allowed to run the docker command with:

```bash
 sudo usermod -aG docker $USER
```

Log out and log back in so that your group membership is re-evaluated, then verify that you can run `docker` commands without `sudo`

```bash
docker run hello-world
```

</details>

<details>

<summary>Prerequisites</summary>

#### Supported Blockchains

Currently, W3bstream supports IoTeX, Ethereum, and any EVM-compatible blockchain.

#### Tokens and Staking Requirements

Currently, there are no token balance or staking requirements to run a W3bstream node.

#### Hardware requirements

Because your W3bstream node will act as a network endpoint for devices to send their data, you should run it on a server that has a fixed IP address, publicly accessible from the Internet.

The minimum hardware requirements to run a W3bstream node are:

* 2 Cores, 2 GB RAM, 10 GB storage, 100 Mbps network

Recommended requirements to get started running a W3bstream node are:

* 4 Cores, 4 GB RAM, 100 GB storage, 100 Mbps network

**Notice**

<mark style="color:purple;">The performances and storage requirements of your node are closely related to the number of client devices, the volumes of IoT data, the data retention policy, and the complexity of the application logic. It's recommended to accurately evaluate the hardware configuration based on the application-specific requirements.</mark>

#### &#x20;Supported OS

The W3bstream runtime supports Linux, MacOS systems, and Windows (WSL).&#x20;

#### Blockchain client

For your W3bstream node to be able to interact with a blockchain application (e.g., react to smart contract events, send proofs to smart contracts), you will also need access to a blockchain gateway.&#x20;

You can use official gateways or third-party's gateways to access the blockchain of your choice.\
\
<mark style="color:purple;">IoTeX public gateways</mark>\
You can find a list of public IoTeX RPC endpoints at:\
[https://docs.iotex.io/dapp-development/web3-development/rpc-endpoints](https://docs.iotex.io/dapp-development/web3-development/rpc-endpoints)

<mark style="color:purple;">Ethereum public gateways</mark>\
You can find a list of public Ethereum RPC endpoints at:\
[https://ethereumnodes.com](https://ethereumnodes.com)

<mark style="color:purple;">Run your own blockchain gateway</mark>\
If you decide to run your own gateway, it's highly recommended that you run it on a separate server, to avoid affecting W3bstream's performance. Below, you can find links to the instructions on how to run your blockchain gateway for IoTeX and Ethereum:

Run an IoTeX full node\
[https://delegates.iotex.io/get-started/node-configuration](https://delegates.iotex.io/get-started/node-configuration)\
\
Run an Ethereum full node\
[https://ethereum.org/en/run-a-node/](https://ethereum.org/en/run-a-node/)

</details>

### Start W3bstream docker images

```
mkdir w3bstream && cd w3bstream

curl https://raw.githubusercontent.com/machinefi/w3bstream-studio/main/docker-compose.yaml > docker-compose.yaml

docker-compose -p w3bstream -f ./docker-compose.yaml up -d
```

If needed, you can see the logs in a terminal with the following command:

```bash
docker container logs w3bstream -f
```

which will give you something like:

```
{"@lv":"debug","@prj":"srv-applet-mgr","@ts":"20230406-172018.514Z","cost":"6.610291ms","msg":"SELECT table_schema,table_name,column_name,data_type,is_nullable,column_default,character_maximum_length,numeric_precision,numeric_scale FROM information_schema.columns WHERE (table_schema = 'applet_management') AND (table_name IN ('t_account','t_account_identity','t_account_password','t_applet','t_config','t_event_log','t_instance','t_project','t_publisher','t_resource','t_strategy','t_wasm_log'))"}
{"@lv":"debug","@prj":"srv-applet-mgr","@ts":"20230406-172018.520Z","cost":"1.227583ms","msg":"SELECT schemaname,tablename,indexname,indexdef FROM pg_indexes WHERE (schemaname = 'applet_management') AND (tablename IN ('t_account','t_account_identity','t_account_password','t_applet','t_config','t_event_log','t_instance','t_project','t_publisher','t_resource','t_strategy','t_wasm_log'))"}
{"@lv":"debug","@prj":"srv-applet-mgr","@ts":"20230406-172018.522Z","cost":"1.552334ms","msg":"CREATE SCHEMA IF NOT EXISTS applet_management;"}
{"@lv":"debug","@prj":"srv-applet-mgr","@ts":"20230406-172018.531Z","cost":"7.552458ms","msg":"CREATE TABLE IF NOT EXISTS applet_management.t_account ( \tf_account_id bigint NOT NULL, \tf_role integer NOT NULL DEFAULT '2'::integer, \tf_state integer NOT NULL DEFAULT '1'::integer, \tf_avatar character varying(255) NOT NULL DEFAULT ''::character varying, \tf_meta text NOT NULL DEFAULT '{}'::text, \tf_prvkey character varying(255) NOT NULL DEFAULT ''::character varying, \tf_created_at bigint NOT NULL DEFAULT '0'::bigint, \tf_updated_at bigint NOT NULL DEFAULT '0'::bigint, \tf_deleted_at bigint NOT NULL DEFAULT '0'::bigint, \tPRIMARY KEY (f_account_id,f_deleted_at) );"}
{"@lv":"debug","@prj":"srv-applet-mgr","@ts":"20230406-172018.536Z","cost":"4.184ms","msg":"CREATE TABLE IF NOT EXISTS applet_management.t_account_identity ( \tf_id bigserial NOT NULL, \tf_account_id bigint NOT NULL, \tf_type integer NOT NULL, \tf_identity_id character varying(255) NOT NULL, \tf_source integer NOT NULL, \tf_meta text NOT NULL DEFAULT ''::text, \tf_created_at bigint NOT NULL DEFAULT '0'::bigint, \tf_updated_at bigint NOT NULL DEFAULT '0'::bigint, \tf_deleted_at bigint NOT NULL DEFAULT '0'::bigint, \tPRIMARY KEY (f_id) );"}
{"@lv":"debug","@prj":"srv-applet-mgr","@ts":"20230406-172018.539Z","cost":"1.853292ms","msg":"CREATE UNIQUE INDEX t_account_identity_ui_account_identity ON applet_management.t_account_identity (f_account_id,f_type,f_deleted_at);"}
{"@lv":"debug","@prj":"srv-applet-mgr","@ts":"20230406-172018.541Z","cost":"2.094416ms","msg":"CREATE UNIQUE INDEX t_account_identity_ui_identity_id ON applet_management.t_account_identity (f_type,f_identity_id,f_deleted_at);"}

...

[Kit] POS /srv-applet-mgr/v0/register/admin
[Kit] 	account.CreateAccountByUsernameAndPassword
[Kit] GET /srv-applet-mgr/v0/resource
[Kit] 	jwt.Auth middleware.ContextAccountAuth resource.ListResources
[Kit] DEL /srv-applet-mgr/v0/resource/{resourceID}
[Kit] 	jwt.Auth middleware.ContextAccountAuth resource.RemoveResource
[Kit] POS /srv-applet-mgr/v0/strategy/{projectName}
[Kit] 	jwt.Auth middleware.ContextAccountAuth strategy.CreateStrategy
[Kit] GET /srv-applet-mgr/v0/strategy/{projectName}
[Kit] 	jwt.Auth middleware.ContextAccountAuth strategy.ListStrategy
[Kit] DEL /srv-applet-mgr/v0/strategy/{projectName}
[Kit] 	jwt.Auth middleware.ContextAccountAuth strategy.RemoveStrategy
[Kit] GET /srv-applet-mgr/v0/strategy/{projectName}/{strategyID}
[Kit] 	jwt.Auth middleware.ContextAccountAuth strategy.GetStrategy
[Kit] PUT /srv-applet-mgr/v0/strategy/{projectName}/{strategyID}
[Kit] 	jwt.Auth middleware.ContextAccountAuth strategy.UpdateStrategy
[Kit] srv-applet-mgr listen on :8888
```

### Access the DevNet dashboard

To access your local W3bstream DevNet, open a Metamask-enabled browser and navigate to port 3000 of the W3bstream node server. If W3bstream is running on your local machine, use 'localhost' instead of the server's IP address:

```
https://localhost:3000
```

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



## Build W3bstream from the source

If you wish to build the W3bstream binary or Docker image from the source code on your local machine, you can clone the W3bstream repository and follow the instructions provided in the README file.

{% embed url="https://github.com/machinefi/w3bstream#build-docker-image-from-code" %}
