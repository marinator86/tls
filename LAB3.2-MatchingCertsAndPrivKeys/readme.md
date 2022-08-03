# Matching Certificates to Private Keys

Execute
```
openssl rsa -in Rainbow.key -noout -modulus
openssl x509 -in Rainbow.cert -noout -modulus
```
the moduli match -> The certificate matches this private key!

Match the private key files to certs:

| File        | Modulus   |
|-------------|-----------|
| Blue.cert   | B62...C5D |
| Green.cert  | E2D...4A1 |
| Orange.cert | CD3...511 |
| Violet.cert | EAA...333 |
| Yellow.cert | BE8...16D |
| key1.key    | CD3...511 |
| key2.key    | B62...C5D |
| key3.key    | BE8...16D |
| key4.key    | E2D...4A1 |
| key5.key    | EAA...333 |

The pairs are obvious.