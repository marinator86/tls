# Certificate Revocation

Check the lab-4-2-certificate-revocation.pdf.pdf file for details.

## CRL

Download:
```
wget http://crl3.digicert.com/ssca-sha2-g6.crl 
```

Grep the CRL:
```
➜  LAB4.2-CertRevocation git:(master) ✗ openssl crl -in ssca-sha2-g6.crl -inform DER -text -noout | grep 0B2CA2D96523D62A0077D0FCC5B46300 -C 2
    Serial Number: 02194C81D3D6811C0D82AD62B5C29BC5
        Revocation Date: Aug 20 19:59:35 2020 GMT
    Serial Number: 0B2CA2D96523D62A0077D0FCC5B46300
        Revocation Date: Aug 20 21:24:42 2020 GMT
    Serial Number: 0E0AFE059D617D7D51ED1C31696F3EEC
```

Show the common reasons, if available:
```
openssl crl -in ssca-sha2-g6.crl -inform DER -text -noout | grep Reason -A1 | sort | uniq -c | sort -n
```