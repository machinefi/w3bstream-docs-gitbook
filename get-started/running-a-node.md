# Running a Node

## Run using Docker

The recommended way of running a W3bstream node is by using [Docker](https://www.docker.com/). With docker, you can easily fetch new releases and update the W3bstream runtime, you won't have to configure a development environment to build the runtime from the source code yourself.

<details>

<summary>Make sure you have Docker and Docker-Compose installed in your system</summary>

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

### Start the W3bstream docker image

```
curl https://raw.githubusercontent.com/machinefi/w3bstream/main/docker-compose.yaml > w3bstream/docker-compose.yaml
docker-compose -p w3bstream -f ./docker-compose.yaml up -d
```

<details>

<summary><img src="../.gitbook/assets/image (6).png" alt="" data-size="original"> Change W3bstream's working directory</summary>

By default, W3bstream will store data in the current folder. If required, you can set the working directory by exporting the following before running the image:&#x20;

`export WS_WORKING_DIR=path_to_the_w3bstream_folder`

</details>

Once you started W3bstream, you can see the log with:

```bash
docker container logs w3bstream -f

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

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

### Run using the command line client

{% hint style="info" %}
****<img src="../.gitbook/assets/image (7) (2).png" alt="" data-size="original">**The W3bstream command line client will be available soon.**
{% endhint %}
