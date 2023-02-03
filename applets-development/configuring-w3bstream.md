# Configuring W3bstream

W3bstream's default configuration is included inside the **`docker-compose.yaml`** file used to start the docker images. However, the most relevant settings can be exported as environment variables, or inside a `.env` file:

```bash
cp .env.tmpl > .env
```

The content of .env looks like the following:

```ini
WS_WORKING_DIR=./
WS_BACKEND_IMAGE=ghcr.io/machinefi/w3bstream:main
WS_STUDIO_IMAGE=ghcr.io/machinefi/w3bstream-studio:main
POSTGRES_USER=w3badmin
POSTGRES_PASSWORD=PaSsW0Rd
POSTGRES_DB=w3bstream
NEXT_PUBLIC_API_URL=http://localhost:8888
CHAIN_ENDPOINT="https://babel-api.testnet.iotex.io/"
PRIVATE_KEY=""
JWT_ISSUER="w3bstream"
JWT_SIGN_KEY="xxxx"
```

`WS_WORKING_DIR`

This is where al W3bstream data is stored. By default, it's the current directory from where the service is started.

`CHAIN_ENDPOINT`

This is the L1 blockchain W3bstream is connected. This setting is used by any W3bstream function that interacts with the blockchain, such as `ws_send_tx.` It's also used by other w3bstream functionalities, such as the [contract event monitor](reacting-to-blockchain-events.md).

`PRIVATE_KEY`

This is the private key of the blockchain account to be used by W3bstream when sending blockchain transactions. Functions that read Blockchain status can still be used, but any attempt to send blockchain transactions will fail with a "missing private key" error in the W3bstream console.

`POSTGRES_DB`

If your applet reads or stores data to the W3bstream SQL database, you must set the database name here.

`POSTGRES_USER` and `POSTGRES_PASSWORD`

If your applet reads or stores data to the W3bstream SQL database, you must set valid database username and password.

`WS_BACKEND_IMAGE`

This setting allows you to run an alternate version of W3bstream. E.g., you can test a development release:

```
WS_BACKEND_IMAGE=ghcr.io/machinefi/w3bstream:v1.0.0-rc1
```

`WS_STUDIO_IMAGE`

This setting allows you to run an alternate version of W3bstream Studio. E.g., you can test a development release:

```
WS_STUDIO_IMAGE=ghcr.io/machinefi/w3bstream-studio:v1.0.0-rc1
```
