# Configuring W3bstream

{% hint style="info" %}
**🚧 This document is a work in progress**
{% endhint %}

W3bstream's configuration is included inside the `docker-compose.yaml` file used to start the docker images. However, the most relevant settings can be exported as environment variables, or inside a `.env` file.

## Chain Endpoint

This is the L1 blockchain W3bstream is connected to. This setting is used by any host function that interacts with the blockchain, such as `ws_send_tx.` It's also used by other w3bstream functionalities, such as the [contract event monitor](reacting-to-blockchain-events.md).

```bash
export CHAIN_ENDPOINT=https://babel-api.testnet.iotex.io
```

## W3bstream's Private Key

This is used as the account to send transactions from inside a W3bstream applet, using the `ws_send_tx` host function.

```bash
export PRIVATE_KEY=ceebc23d...918c
```

## All settings

```yaml
# MQTT client settings

## Set the maximum time interval allowed between messages before being disconnected
SRV_APPLET_MGR__BROKER__Keepalive: 3h
## Set the MQTT Quality of Service 
SRV_APPLET_MGR__BROKER__QoS: ONCE
## Ask the MQTT server to retain the most recent message for a topic
SRV_APPLET_MGR__BROKER__RetainPublish: "false"
## Specifyi a retry Interval for failed connections to the MQTT broker
SRV_APPLET_MGR__BROKER__Retry_Interval: 3s
## Specify the maximum number of connection retries
SRV_APPLET_MGR__BROKER__Retry_Repeats: "3"
## MQTT broker endpoint
SRV_APPLET_MGR__BROKER__Server: mqtt://127.0.0.1:1883
## Connection timeout
SRV_APPLET_MGR__BROKER__Timeout: 3s

# W3bstream settings

## 
SRV_APPLET_MGR__CONFIG__ResourceRoot: ./asserts
## 
SRV_APPLET_MGR__CONFIG__UploadLimit: "104857600"

# Blockchain settings

## Blockchain gateway endpoint
SRV_APPLET_MGR__ETHCLIENTCONFIG__ChainEndpoint: "https://babel-api.testnet.iotex.io/"
## Private key used for transactions sent by the host
SRV_APPLET_MGR__ETHCLIENTCONFIG__PrivateKey: ""

# Login token settings

## Login token expiration time
SRV_APPLET_MGR__JWT__ExpIn: 1h
## Login token issuer
SRV_APPLET_MGR__JWT__Issuer: "srv-applet-mgr"
## 
SRV_APPLET_MGR__JWT__SignKey: "xxxx"

# Log settings

## Log format
SRV_APPLET_MGR__LOG__Format: JSON
## Log level
SRV_APPLET_MGR__LOG__Level: DEBUG
## Log name
SRV_APPLET_MGR__LOG__Name: "srv-applet-mgr"
## 
SRV_APPLET_MGR__LOG__ReportCaller: "false"
## 
SRV_APPLET_MGR__LOG__Output: ALWAYS

# DB settings

## 
SRV_APPLET_MGR__PGCLI__ConnMaxLifetime: 1h
## DB connection string
SRV_APPLET_MGR__PGCLI__Master: postgres://test_user:test_passwd@127.0.0.1:5432/test?sslmode=disable
## 
SRV_APPLET_MGR__PGCLI__PoolSize: "10"
## 
SRV_APPLET_MGR__PGCLI__Retry_Interval: 3s
## 
SRV_APPLET_MGR__PGCLI__Retry_Repeats: "3"
## 
SRV_APPLET_MGR__PGCLI__Slave: ""

# API server settings

## Enable debug log 
SRV_APPLET_MGR__SERVER__Debug: "true"
## API server port
SRV_APPLET_MGR__SERVER__Port: "8888"
## API specs
SRV_APPLET_MGR__SERVER__Spec: ./swagger.json

## 
SRV_APPLET_MGR__UPLOADCONFIG__FileSizeLimit: "104857600"
## 
SRV_APPLET_MGR__UPLOADCONFIG__Root: ./asserts
```
