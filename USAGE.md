## Using self-signed certificates

### server certs

Configure your servers as usual.

### Trust ca certificate

- Windows

![1](./imgs/trust-ca-win-1.jpeg)
![2](./imgs/trust-ca-win-2.jpeg)
![3](./imgs/trust-ca-win-3.jpeg)
![4](./imgs/trust-ca-win-4.jpeg)

- Ubuntu

```
sudo cp ca/ca.pem /usr/local/share/ca-certificates/gitlifeca.crt
sudo update-ca-certificates
```
