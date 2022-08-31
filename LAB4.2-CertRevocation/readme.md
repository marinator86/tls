# Certificate Revocation

Check the lab-4-2-certificate-revocation.pdf file for details.

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

## OCSP

Get the URI
```bash
➜  LAB4.2-CertRevocation git:(master) ✗ openssl x509 -in grc.com.cert -noout -ocsp_uri
http://ocsp.digicert.com
```
Reading the CA Issuers field
```bash
...
            Authority Information Access: 
                OCSP - URI:http://ocsp.digicert.com
                CA Issuers - URI:http://cacerts.digicert.com/DigiCertSHA2SecureServerCA.crt
...
```
After issuer cert is downloaded:
```bash
➜  LAB4.2-CertRevocation git:(master) ✗ openssl ocsp -url http://ocsp.digicert.com -issuer ocsp/ica.grc.com.crt -cert grc.com.cert
WARNING: no nonce in response
Response Verify Failure
4368238124:error:27FFF076:OCSP routines:CRYPTO_internal:signer certificate not found:/AppleInternal/Library/BuildRoots/b6051351-c030-11ec-96e9-3e7866fcf3a1/Library/Caches/com.apple.xbs/Sources/libressl/libressl-2.8/crypto/ocsp/ocsp_vfy.c:89:
grc.com.cert: revoked
	This Update: Aug 30 21:57:02 2022 GMT
	Next Update: Sep  6 21:12:02 2022 GMT
	Revocation Time: Aug 20 21:24:42 2020 GMT
```

## OCSP Stapling

One example for either revoked and good certs (shortened):

```bash
➜  LAB4.2-CertRevocation git:(master) ✗ openssl s_client -connect revoked.grc.com:443 -tls1_2 -status
...
OCSP response: 
======================================
OCSP Response Data:
    OCSP Response Status: successful (0x0)
    Response Type: Basic OCSP Response
    Version: 1 (0x0)
    Responder Id: 0F80611C823161D52F28E78D4638B42CE1C6D9E2
    Produced At: Aug 28 22:12:54 2022 GMT
    Responses:
    Certificate ID:
      Hash Algorithm: sha1
      Issuer Name Hash: 105FA67A80089DB5279F35CE830B43889EA3C70D
      Issuer Key Hash: 0F80611C823161D52F28E78D4638B42CE1C6D9E2
      Serial Number: 0B2CA2D96523D62A0077D0FCC5B46300
    Cert Status: revoked
    Revocation Time: Aug 20 21:24:42 2020 GMT
    This Update: Aug 28 21:57:02 2022 GMT
    Next Update: Sep  4 21:12:02 2022 GMT

    Signature Algorithm: sha256WithRSAEncryption
         76:2a:42:4c:30:6a:9a:b3:ec:72:de:02:a2:e1:85:6a:bc:eb:
         0a:70:71:f0:2d:68:0b:e2:f3:a9:f9:35:dc:e5:73:26:c7:6b:
         81:f9:27:86:de:eb:d8:ed:ad:a6:87:b4:f7:cf:fd:13:f6:23:
         aa:6a:ae:2a:dd:a6:fb:1b:58:b8:46:37:5e:ed:a8:49:33:3b:
         75:0e:62:1d:ba:1e:71:92:fe:72:c6:37:d4:a0:cd:fe:6b:d8:
         40:07:83:8a:b0:b5:6c:4a:5f:f0:23:46:5b:4d:03:ef:fb:f6:
         2c:98:53:a3:71:3d:dd:09:b5:2f:b6:07:f9:40:e2:d8:13:0c:
         c5:88:82:33:01:fc:5c:2d:ac:84:5a:4d:7e:b1:a8:d5:5a:6f:
         75:71:af:76:6b:ee:40:65:41:50:99:f6:c8:ef:19:6e:5c:8f:
         d1:17:49:57:b0:65:72:09:39:1a:1c:c9:62:d5:7b:a6:2e:21:
         ac:70:43:aa:76:23:78:68:b8:a7:18:7f:84:a2:2e:37:a9:35:
         90:8c:2c:d1:7c:dd:99:10:fe:b6:24:7b:25:36:04:bd:03:b9:
         9f:fe:21:7b:c9:df:f2:b7:aa:2a:87:d6:97:7c:cd:61:df:c7:
         27:b5:8b:ab:63:9b:1e:b1:50:ec:b7:ec:54:bc:61:89:49:2f:
         ec:ad:88:f8
======================================
---
➜  LAB4.2-CertRevocation git:(master) ✗ openssl s_client -connect example.com:443 -tls1_2 -status
...
OCSP response: 
======================================
OCSP Response Data:
    OCSP Response Status: successful (0x0)
    Response Type: Basic OCSP Response
    Version: 1 (0x0)
    Responder Id: B76BA2EAA8AA848C79EAB4DA0F98B2C59576B9F4
    Produced At: Aug 30 05:24:51 2022 GMT
    Responses:
    Certificate ID:
      Hash Algorithm: sha1
      Issuer Name Hash: E4E395A229D3D4C1C31FF0980C0B4EC0098AABD8
      Issuer Key Hash: B76BA2EAA8AA848C79EAB4DA0F98B2C59576B9F4
      Serial Number: 0FAA63109307BC3D414892640CCD4D9A
    Cert Status: good
    This Update: Aug 30 05:09:02 2022 GMT
    Next Update: Sep  6 04:24:02 2022 GMT

    Signature Algorithm: sha256WithRSAEncryption
         00:cf:86:1d:95:e9:4f:92:4a:d4:c4:5f:f6:68:30:ac:37:94:
         fd:b4:53:81:26:36:b9:03:82:c6:50:5e:b7:de:4c:78:53:6d:
         90:74:89:fd:70:1f:1d:9d:af:fb:b2:64:c2:b8:5b:20:11:73:
         5e:94:48:64:8c:eb:bf:13:59:10:a2:14:e6:eb:cf:5f:79:d9:
         bf:42:1e:20:4d:73:0c:52:b9:bc:65:4e:1f:6b:f7:24:97:b7:
         30:c7:35:2d:07:a8:cb:15:58:be:7b:87:60:2c:ce:2f:1a:31:
         48:4f:68:bb:0d:2b:5b:a4:91:75:b6:b4:f2:8a:98:dd:30:a2:
         70:59:40:41:e2:0c:c1:7c:b2:63:92:af:72:e0:7c:f9:c4:77:
         4b:ea:41:c7:2e:6d:b4:a6:4e:83:31:52:7e:2b:46:eb:a8:b5:
         b6:04:9f:bf:a2:73:87:89:4e:6c:8c:a4:56:cc:3f:3d:32:fc:
         7b:28:23:e5:aa:47:bb:fd:48:bf:d7:d1:e6:09:0c:06:1e:3e:
         89:25:57:3a:4f:ff:7f:99:b7:31:73:4e:2e:c5:84:33:f9:7f:
         02:f0:b2:67:23:0f:db:6d:66:ce:64:6d:85:97:65:d4:6f:c6:
         6f:78:8c:a6:f6:79:f1:41:51:90:1e:cf:9c:30:25:65:2f:9b:
         bc:1b:a0:17
======================================
---
```