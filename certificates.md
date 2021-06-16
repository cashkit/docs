<h1> Generate certificates. <h1>

<h2>Development</h2>

<h4> Auto Generation </h4>

- Post running the bchd on your local machine you should be able to find the certificate and key that are generated by bchd. You can use that for local development purpose.

See Sample bchd config: https://github.com/gcash/bchd/blob/master/sample-bchd.conf
`rpccert=~/.bchd/rpc.cert`
`rpckey=~/.bchd/rpc.key`


<h4> Custom generation </h4>


Output files
- ca.key: Certificate Authority private key file (this shouldn't be shared in real-life)
- ca.crt: Certificate Authority trust certificate (this should be shared with users in real-life)
- server.key: Server private key, password protected (this shouldn't be shared)
- server.csr: Server certificate signing request (this should be shared with the CA owner)
- server.crt: Server certificate signed by the CA (this would be sent back by the CA owner) - keep on server
- server.pem: Conversion of server.key into a format gRPC likes (this shouldn't be shared)


```sh
#!/bin/bash

# Changes these CN's to match your hosts in your environment if needed.
SERVER_CN=localhost
# Step 1: Generate Certificate Authority + Trust Certificate (ca.crt)
openssl genrsa -passout pass:1111 -des3 -out ca.key 4096
openssl req -passin pass:1111 -new -x509 -days 3650 -key ca.key -out ca.crt -subj "/CN=${SERVER_CN}"

# Step 2: Generate the Server Private Key (server.key)
openssl genrsa -passout pass:1111 -des3 -out server.key 4096

# Step 3: Get a certificate signing request from the CA (server.csr)
openssl req -passin pass:1111 -new -key server.key -out server.csr -subj "/CN=${SERVER_CN}" -config certs.cnf

# Step 4: Sign the certificate with the CA we created (it's called self signing) - server.crt
openssl x509 -req -passin pass:1111 -days 3650 -in server.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out server.crt -extensions req_ext -extfile certs.cnf

# Step 5: Convert the server certificate to .pem format (server.pem) - usable by gRPC
openssl pkcs8 -topk8 -nocrypt -passin pass:1111 -in server.key -out server.pem

# Addon: Generating unencrypted key for bchd server
# openssl rsa -in server.pem -out key.unencrypted.pem -passin pass:1111
```

`certs.cnf`
```json
[ req ]
default_bits = 4096
distinguished_name = dn
req_extensions = req_ext
prompt = no

[ dn ]
CN = localhost

[ req_ext ]
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
DNS.2 = 127.0.0.1
```