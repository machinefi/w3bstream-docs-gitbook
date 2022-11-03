# Configuring W3bstream



{% hint style="info" %}
**🚧 This document is a work in progress**
{% endhint %}



```yaml
# MQTT Broker settings
SRV_APPLET_MGR__BROKER__Keepalive: 3h
SRV_APPLET_MGR__BROKER__QoS: ONCE
SRV_APPLET_MGR__BROKER__RetainPublish: "false"
SRV_APPLET_MGR__BROKER__Retry_Interval: 3s
SRV_APPLET_MGR__BROKER__Retry_Repeats: "3"
SRV_APPLET_MGR__BROKER__Server: mqtt://127.0.0.1:1883
SRV_APPLET_MGR__BROKER__Timeout: 3s

# W3bstream settings
SRV_APPLET_MGR__CONFIG__ResourceRoot: ./asserts
SRV_APPLET_MGR__CONFIG__UploadLimit: "104857600"

# Blockchain settings
SRV_APPLET_MGR__ETHCLIENTCONFIG__ChainEndpoint: "https://babel-api.testnet.iotex.io/"
SRV_APPLET_MGR__ETHCLIENTCONFIG__PrivateKey: ""

# Login token settings
SRV_APPLET_MGR__JWT__ExpIn: 1h
SRV_APPLET_MGR__JWT__Issuer: "srv-applet-mgr"
SRV_APPLET_MGR__JWT__SignKey: "xxxx"

# Log settings
SRV_APPLET_MGR__LOG__Format: JSON
SRV_APPLET_MGR__LOG__Level: DEBUG
SRV_APPLET_MGR__LOG__Name: "srv-applet-mgr"
SRV_APPLET_MGR__LOG__ReportCaller: "false"
SRV_APPLET_MGR__LOG__Output: ALWAYS

# DB settings
SRV_APPLET_MGR__PGCLI__ConnMaxLifetime: 1h
SRV_APPLET_MGR__PGCLI__Master: postgres://test_user:test_passwd@127.0.0.1:5432/test?sslmode=disable
SRV_APPLET_MGR__PGCLI__PoolSize: "10"
SRV_APPLET_MGR__PGCLI__Retry_Interval: 3s
SRV_APPLET_MGR__PGCLI__Retry_Repeats: "3"
SRV_APPLET_MGR__PGCLI__Slave: ""

# API server settings
SRV_APPLET_MGR__SERVER__Debug: "true"
SRV_APPLET_MGR__SERVER__Port: "8888"
SRV_APPLET_MGR__SERVER__Spec: ./swagger.json

# 
SRV_APPLET_MGR__UPLOADCONFIG__FileSizeLimit: "104857600"
SRV_APPLET_MGR__UPLOADCONFIG__Root: ./asserts
```
