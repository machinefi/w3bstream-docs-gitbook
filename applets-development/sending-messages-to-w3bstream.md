# Sending messages to W3bstream

W3bstream provides two different network service endpoints that allow sending messages to the various projects running in the node.

### Sending messages using HTTP

The W3bstream HTTP API default port is `8888`, and it can be used to both manage the node and send to data messages to it.&#x20;

#### Command HTTP API

The suggested way to manage W3bstream is to use the integrated [W3bstream Studio](../get-started/w3bstream-studio/) web app. However, if you want to build your own management tools, the API below allows you to login into W3bstream and manage projects and applets. We are using [httpie](https://httpie.io) in the examples below.

**Login**

```
srv-applet-mgr/v0/login

Example:
echo '{"username":"admin","password":"${password}"}' | http put :8888/srv-applet-mgr/v0/login
```

#### TODO

### MQTT Project Topics

TODO
