# Generate self-signed certs by cfssl

## create dirs

```
mkdir -p ca out
chmod 755 bin/*
```

## generate ca

```
cd ca
../bin/cfssl gencert -initca ../json/ca-csr.json|../bin/cfssljson -bare ca
```

## generate server-csr.json

```
export SELF_CN=atompi.cc
cat ../json/server-csr.json.tmpl | sed "s/SELF_CN/$SELF_CN/g" > ../json/$SELF_CN-server-csr.json
```

## create certs (If necessary, modify the certificate age in ca-config.json)

```
cd ../out
../bin/cfssl gencert -ca=../ca/ca.pem -ca-key=../ca/ca-key.pem -config=../json/ca-config.json -profile=peer ../json/$SELF_CN-server-csr.json | ../bin/cfssljson -bare $SELF_CN
```

## Usage

[USAGE](./USAGE.md)

## Tips

### get binary

```
mkdir -p bin
proxy wget https://github.com/cloudflare/cfssl/releases/download/v1.6.5/cfssl-certinfo_1.6.5_linux_amd64 -O bin/cfssl-certinfo
proxy wget https://github.com/cloudflare/cfssl/releases/download/v1.6.5/cfssljson_1.6.5_linux_amd64 -O bin/cfssljson
proxy wget https://github.com/cloudflare/cfssl/releases/download/v1.6.5/cfssl_1.6.5_linux_amd64 -O bin/cfssl
```

### generate default json

```
bin/cfssl print-defaults config > json/ca-config.json
bin/cfssl print-defaults csr > json/server-csr.json
```
