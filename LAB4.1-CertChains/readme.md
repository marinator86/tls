# Follow Certificate Chains

Check the lab-4-1-certificate-chains.pdf.pdf file for details.

Task 1:
```
➜  Task1 git:(master) ✗ for f in ./*; do openssl x509 -in $f -noout -issuer; done
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=olive.net
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=cyan.net
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=cyan.net
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=yellow.net
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=magenta.net
```

Task 2:
```
➜  Task2 git:(master) ✗ for f in ./*; do openssl x509 -in $f -noout -issuer -subject; done
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=professorX.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=batman.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=thor.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=End Entity/CN=ironman.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=professorX.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=professorX.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=professorX.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=spiderman.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=batman.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=End Entity/CN=superman.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=spiderman.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=thor.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=professorX.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=wolverine.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=wolverine.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=End Entity/CN=wonder.woman.com
```
* professorX.com
  * spiderman.com
    * thor.com
      * ironman.com (end)
  * batman.com
    * superman.com (end)
  * wolverine.com
    * wonder.woman.com (end)

Task 3:
```
➜  Task3 git:(master) ✗ for f in ./*; do openssl x509 -in $f -noout -issuer -subject; done
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=magneto.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=apocalypse.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=joker.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=bane.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=magneto.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=End Entity/CN=dark.phoenix.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=thanos.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=joker.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=thanos.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=loki.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=thanos.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=magneto.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=apocalypse.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=End Entity/CN=psylocke.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=thanos.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Root CA/CN=thanos.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=loki.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=End Entity/CN=ultron.com
issuer= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=Intermediate CA/CN=bane.com
subject= /C=US/ST=Practical TLS/O=Practical Networking .net/OU=End Entity/CN=venom.com
```

* thanos.com
  * joker.com
    * bane.com
      * venom.com (end)
  * loki.com
    * ultron.com (end)
  * magento.com
    * apocalypse.com
      * psylocke.com (end)
    * dark.phoenix.com (end)