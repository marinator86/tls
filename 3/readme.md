# x509 Certificates

1 What's in a certificate?
```
openssl s_client -connect reddit.com:443
```
Extract the certificate in pem format from the answer -> `cert.pem`
```
openssl x509 -in cert.pem -text
```