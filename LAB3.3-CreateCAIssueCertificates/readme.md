# Create a CA and issue certificates

Execute
```
openssl rsa -in Rainbow.key -noout -modulus
openssl x509 -in Rainbow.cert -noout -modulus
```
