# Running a Node

## Run using Docker

The recommended way of running a W3bstream node is by using [Docker](https://www.docker.com/). With docker, you can easily fetch new releases and update the W3bstream runtime, you won't have to configure a development environment to build the runtime from the source code yourself.

Make sure you have Docker and Docker-Compose installed in your system:

{% embed url="https://www.docker.com/" %}
Install Docker
{% endembed %}

Once you have Docker installed in your system, make sure your user is allowed to run the docker command with:

```bash
 sudo usermod -aG docker $USER
```

Log out and log back in so that your group membership is re-evaluated, then verify that you can run `docker` commands without `sudo`

```bash
docker run hello-world
```

### Pull the Docker image

Pull the W3bstream runtime docker image with:

```bash
docker pull w3bstream/w3bstream:latest
```

### Prepare docker-compose.yaml

To start the node, create a `docker-compose.yaml` file with the following content to quickly start the node with required services using _docker-compose_:

_See the file on GitHub**:**_ [docker-compose.yaml](https://github.com/machinefi/w3bstream/blob/82b1537711f4d89b9a3802ecc464d5988aa2970e/docker-compose.yaml)

```yaml
version: '3.6'
services:
  w3bapp:
    image: iotex/w3bstream:v3
    container_name: w3bstream
    restart: always
    ports:
    - "5432:5432"
    - "8888:8888"
    - "1883:1883"
    - "3000:3000"
    command: ["/bin/sh","/init.sh"]
    volumes:
    - $PWD/build_image/pgdata:/var/lib/postgresql_data
    - $PWD/build_image/asserts:/w3bstream/cmd/srv-applet-mgr/asserts
    - $PWD/build_image/conf/srv-applet-mgr/config/local.yml:/w3bstream/cmd/srv-applet-mgr/config/local.yml
    environment:
      DATABASE_URL: "postgresql://test_user:test_passwd@127.0.0.1/test?schema=applet_management"
      NEXT_PUBLIC_API_URL: "http://127.0.0.1:8888"
  graphql-engine:
    image: hasura/graphql-engine:v2.2.0
    depends_on:
    - "w3bapp"
    restart: always
    ports:
    - "8080:8080"
    environment:
      ## postgres database to store Hasura metadata
      HASURA_GRAPHQL_METADATA_DATABASE_URL: postgresql://test_user:test_passwd@w3bapp/test
      ## enable the console served by server
      HASURA_GRAPHQL_ENABLE_CONSOLE: "true" # set "false" to disable console
      ## enable debugging mode. It is recommended to disable this in production
      HASURA_GRAPHQL_DEV_MODE: "true"
      ## enable debugging mode. It is recommended to disable this in production
      HASURA_GRAPHQL_DEV_MODE: "true"
      HASURA_GRAPHQL_ENABLED_LOG_TYPES: startup, http-log, webhook-log, websocket-log, query-log
      ## uncomment next line to run console offline (i.e load console assets from server instead of CDN)
      # HASURA_GRAPHQL_CONSOLE_ASSETS_DIR: /srv/console-assets
      ## uncomment next line to set an admin secret
      HASURA_GRAPHQL_ADMIN_SECRET: w3baAdmiNsecrEtkey
```

### Start the node

Start the W3bstream node with:

```bash
docker-compose -f docker-compose.yaml up
```

You will see a log similar to the one below:

```bash
Creating network "conf_default" with the default driver
Creating w3bstream ... done
Creating conf_graphql-engine_1 ... done
Attaching to w3bstream, conf_graphql-engine_1
w3bstream         | PG data does not exsit!
graphql-engine_1  | {"type":"startup","timestamp":"2022-11-01T14:27:57.754+0000","level":"info","detail":{"kind":"server_configuration","info":{"live_query_options":{"batch_size":100,"refetch_delay":1},
...

w3bstream         | [Kit] PUT /srv-applet-mgr/v0/strategy/{projectName}/{strategyID}
w3bstream         | [Kit] 	jwt.Auth middleware.ContextAccountAuth strategy.UpdateStrategy
w3bstream         | [Kit] srv-applet-mgr@0.0.1 listen on :8888
w3bstream         | {"@lv":"info","@prj":"srv-applet-mgr","@ts":"20221101-142810.513Z","msg":"admin created"}
w3bstream         | Listening on port 3000 url: http://localhost:3000
Notice at the end of the log, you will find the admin credentials to log in and interact with the W3bstream runtime:
```

You can now access the [W3bstream Studio ](w3bstream-studio/)admin dashboard by pointing a browser to port `3000` for the W3bstream node server:

```
https://localhost:3000
```

<figure><img src="../.gitbook/assets/image (6) (2).png" alt=""><figcaption></figcaption></figure>

### Run using the command line client

{% hint style="info" %}
**🚧 The W3bstream client feature will be available soon.**
{% endhint %}
