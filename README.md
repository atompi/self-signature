# Generate self-signed certs by cfssl

## create dirs

```
mkdir -p ca out
chmod 755 bin/*
```

## generate ca

```
cd ca
../bin/cfssl gencert -initca ../json/ca-csr.json|cfssljson -bare ca
```

## create certs

```
cd ../out
../bin/cfssl gencert -ca=../ca/ca.pem -ca-key=../ca/ca-key.pem -config=../json/ca-config.json -profile=peer ../json/server-csr.json | cfssljson -bare gitlife.com
```

## Usage

[USAGE](./USAGE.md)

## Tips

### get binary

```
mkdir -p bin
proxy wget https://github.com/cloudflare/cfssl/releases/download/v1.6.3/cfssl-certinfo_1.6.3_linux_amd64 -O bin/cfssl-certinfo
proxy wget https://github.com/cloudflare/cfssl/releases/download/v1.6.3/cfssljson_1.6.3_linux_amd64 -O bin/cfssljson
proxy wget https://github.com/cloudflare/cfssl/releases/download/v1.6.3/cfssl_1.6.3_linux_amd64 -O bin/cfssl
```

### generate default json

```
bin/cfssl print-defaults config > json/ca-config.json
bin/cfssl print-defaults csr > json/server-csr.json
```
