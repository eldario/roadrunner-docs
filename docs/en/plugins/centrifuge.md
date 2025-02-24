# Centrifuge plugin

The Centrifuge plugin `[since 2.12.0]` replaces our deprecated `Websockets` and `Broadcast` plugins.
Centrifuge is a robust library with several clients (JS, Dart, Go, Python) that are actively supported.
Our previous JS client had weak support and was not updated for a long time.

RR exposes all available APIs, including a `gRPC` proxy and the client API.

## PHP client

- [link](https://github.com/roadrunner-php/centrifugo)

## Proxy interface

- [Docs](https://centrifugal.dev/docs/server/proxy#grpc-proxy)

RR follows the [proxy.proto](https://github.com/centrifugal/centrifugo/blob/master/internal/proxyproto/proxy.proto) specifications and proxies these events to the PHP worker.
To determine what proxy method was called inside the PHP, RR adds a `type` : `endpoint` metadata. For example, if the `Subscribe` method was called, RR will add `type`:`subscribe` metadata to the worker's context.

## RPC 

You may also use RPC methods to communicate with centrifugo server. RR follows the official [centrifugo proto API](https://github.com/centrifugal/centrifugo/blob/master/internal/apiproto/api.proto).
Official documentation available [here](https://centrifugal.dev/docs/server/server_api#grpc-api)


## Configuration

```yaml
# Centrifugo server plugin
#
# Docs: https://centrifugal.dev/
centrifuge:
  # Centrifugo server proxy address (docs: https://centrifugal.dev/docs/server/proxy#grpc-proxy)
  #
  # Optional, default: tcp://127.0.0.1:30000
  proxy_address: "tcp://127.0.0.1:30000"

  # gRPC server API address (docs: https://centrifugal.dev/docs/server/server_api#grpc-api)
  #
  # Optional, default: tcp://127.0.0.1:30000. Centrifugo: `grpc_api` should be set to true and `grpc_port` should be the same as in the RR's config.
  grpc_api_address: tcp://127.0.0.1:30000

  # Use gRPC gzip compressor
  #
  # Optional, default: false
  use_compressor: true

  # Your application version
  #
  # Optional, default: v1.0.0
  version: "v1.0.0"

  # Your application name
  #
  # Optional, default: roadrunner
  name: "roadrunner"

  # TLS configuration
  #
  # Optional, default: null
  tls:
    # TLS key
    #
    # Required
    key: /path/to/key.pem

    # TLS certificate
    #
    # Required
    cert: /path/to/cert.pem
```
