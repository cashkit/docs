# Protos

[https://github.com/cashkit/protos](https://github.com/cashkit/protos) repo contains all proto files and generated code required by the `cashkit` org.

```text
#!/bin/bash

export PATH="$PATH:$(go env GOPATH)/bin"

protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative bchrpc/bchrpc.proto
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative kitrpc/kitrpc.proto
```

