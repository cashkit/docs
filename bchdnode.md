<h1> BCHD Node </h1>


<h3> Configs </h3>

Mac:

|  Executable | Config path  | Executable path
| ------------|------------- |----------------|
|  Bchd/      |  /Users/user-name/Library/Application\ Support/Bchd/bchd.conf | /Users/user-name/go/bin/bchd  |
| Bchwallet/ | /Users/user-name/Library/Application\ Support/Bchwallet/bchwallet.conf | /Users/user-name/go/bin/bchwallet  |
| Bchctl/  |  /Users/user-name/Library/Application\ Support/Bchctl/bchctl.conf |  /Users/user-name/go/bin/bchctl |

---


<h3> Certificates. </h3>

See `certificates.md`


<h3> bchwallet config </h3>

File: `bchwallet.conf`

```
username=<your-rpc-user-name>
password=<your-rpc-password>
bchdusername=<your-rpc-user-name>
bchdpassword=<your-rpc-password>
rpccert=./rpc.crt # See certificates.md
rpckey=./rpc.key # See certificates.md
```

<h3> bchctl config </h3>

File: `bchctl.conf`

```
rpcuser=<your-rpc-user-name>
rpcpass=<your-rpc-password>
rpccert=./rpc.crt # See certificates.md
```

<h3> bchd config </h3>

File: `bchd.conf`

```
[Application Options]
rpcuser=<your-rpc-user-name>
rpcpass=<your-rpc-password>
rpclisten=:8334
rpccert=./rpc.crt
rpckey=./rpc.key
grpclisten=[::]:8335
prunedepth=300
txindex=1
addrindex=1
debuglevel=info
```