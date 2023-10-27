# ssl-tls-pfx
Create pfx file using private key and crt file

```
openssl pkcs12 -export -out test.pfx -inkey tls.key -in tls.crt
```

Extract the private key and crt from pfx file and create the Kubernetes tls secret

```
openssl pkcs12 -in test.pfx -nocerts -out key-filename.key
openssl rsa -in key-filename.key -out key-filename-decrypted.key
openssl pkcs12 -in test.pfx -clcerts -nokeys -out crt-filename.crt
kubectl -n default create secret tls test-tls-secret --cert crt-filename.crt --key key-filename-decrypted.key
```
