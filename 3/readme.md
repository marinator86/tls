# x509 Certificates

## What's in a certificate?
```
openssl s_client -connect reddit.com:443
```
Extract the certificate in pem format from the answer -> `cert.pem`
```
openssl x509 -in cert.pem -text
```

### Look at DigiCert chain

```
curl http://cacerts.digicert.com/DigiCertTLSRSASHA2562020CA1-1.crt -o digi.crt
```
```
openssl x509 -in digi.crt -inform der -text
```
```
curl http://cacerts.digicert.com/DigiCertGlobalRootCA.crt -o digi-root.crt
```
```
openssl x509 -in digi-root.crt -inform der -text
```

The root certificate is self-signed, one can see this by comparing the Authority Key Identifier and the Subject Key
Identifier extensions.