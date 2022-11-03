# Monitoring Smart Contracts

## Blockchain Monitor

Thanks to W3bstream blockchain monitoring capabilities, it's very easy toThe blockchain monitor is an internal W3bstream module that can emit W3bstream events when a certain blockchain event is emitted by a smart contract.

You can configure and start one monitor for each smart contract event you are interested in.&#x20;

Make sure you login to the W3bstream node using the API first:

```bash
export TOK=$(echo '{"username":"admin","password":"iotex.W3B.admin"}' | http put :8888/srv-applet-mgr/v0/login | jq .token -r)To configure and start a blockchain monitor, make sure your W3bstream node is running, then type the command below. Make sure you replace: 
```

then you can start a blockchain event monitor typing the commend below (please notice it's using the [httpie](https://httpie.io/) client), after replacing:

* `chainID` with 4690 for the IoTeX Testnet, 4689 for the IoTeX Mainnet; &#x20;
* `contractAddress` with the actual address of the contract you want to monitor;&#x20;
* `topic0` with the topic of the smart contract event that you want to detect
* `eventType` with the event type code that matches your [Project strategy](monitoring-smart-contracts.md#event-strategies) for this specific event

```bash
echo '{\
  "contractLog": {\
    "chainID": 4690,\ 
    "contractAddress": "0x6a0BFf625A70C43bcEEFAC51aF928ae545941b4A",\
    "blockStart": 17058530,\
    "blockEnd": 100000000,\
    "topic0":"0x766e6460a49ca518797200f8d2b455a80962f1e6acdcda61000fc3dc2004db88",\
    "eventType":"EXAMP1"\
  }\
}' | http :8888/srv-applet-mgr/v0/project/monitor/<PROJECT_ID> -A bearer -a $TOK
```

💡 <mark style="color:purple;">**Learn more**</mark>

{% content-ref url="monitoring-smart-contracts.md" %}
[monitoring-smart-contracts.md](monitoring-smart-contracts.md)
{% endcontent-ref %}

