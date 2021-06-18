---
description: All Protos used by Cashkit. ⚙️
---

# Protos

[This](https://github.com/cashkit/protos) repo contains all proto files and generated code used by the `cashkit` org.

[https://github.com/cashkit/protos/tree/main/bchrpc](https://github.com/cashkit/protos/tree/main/bchrpc)

```text
#!/bin/bash

export PATH="$PATH:$(go env GOPATH)/bin"

protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative bchrpc/bchrpc.proto
protoc --go_out=. --go_opt=paths=source_relative --go-grpc_out=. --go-grpc_opt=paths=source_relative kitrpc/kitrpc.proto
```

