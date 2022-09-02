# Inspecting a TLS Handshake

Check the lab-6-1-inspecting-a-tls-handshake-with-wireshark.pdf file for details.

The traffic between a simple web server and a TLS client is as follows:

```bash
No.     Time           Source                Destination           Protocol Length Info
      1 0.000000       127.0.0.1             127.0.0.99            TCP      74     5555 → 443 [SYN] Seq=0 Win=65495 Len=0 MSS=65495 SACK_PERM=1 TSval=2748636071 TSecr=0 WS=128

Frame 1: 74 bytes on wire (592 bits), 74 bytes captured (592 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 0, Len: 0

No.     Time           Source                Destination           Protocol Length Info
      2 0.000008       127.0.0.99            127.0.0.1             TCP      74     443 → 5555 [SYN, ACK] Seq=0 Ack=1 Win=65483 Len=0 MSS=65495 SACK_PERM=1 TSval=1035290446 TSecr=2748636071 WS=128

Frame 2: 74 bytes on wire (592 bits), 74 bytes captured (592 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 0, Ack: 1, Len: 0

No.     Time           Source                Destination           Protocol Length Info
      3 0.000015       127.0.0.1             127.0.0.99            TCP      66     5555 → 443 [ACK] Seq=1 Ack=1 Win=65536 Len=0 TSval=2748636071 TSecr=1035290446

Frame 3: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 1, Ack: 1, Len: 0

No.     Time           Source                Destination           Protocol Length Info
      4 0.000293       127.0.0.1             127.0.0.99            TLSv1.2  317    Client Hello

Frame 4: 317 bytes on wire (2536 bits), 317 bytes captured (2536 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 1, Ack: 1, Len: 251
Transport Layer Security
    TLSv1.2 Record Layer: Handshake Protocol: Client Hello
        Content Type: Handshake (22)
        Version: TLS 1.0 (0x0301)
        Length: 246
        Handshake Protocol: Client Hello
            Handshake Type: Client Hello (1)
            Length: 242
            Version: TLS 1.2 (0x0303)
            Random: 8377f1ca4c689ee40355e16ac3a399e3aef664b6ef11f3f8c329821055adc158
            Session ID Length: 32
            Session ID: 0b2745de0a1b08641adcd0fe61cbc499a6080a059f24feac3393703f151c4b2a
            Cipher Suites Length: 34
            Cipher Suites (17 suites)
            Compression Methods Length: 1
            Compression Methods (1 method)
            Extensions Length: 135
            Extension: ec_point_formats (len=4)
            Extension: supported_groups (len=12)
            Extension: encrypt_then_mac (len=0)
            Extension: extended_master_secret (len=0)
            Extension: signature_algorithms (len=42)
            Extension: supported_versions (len=5)
            Extension: psk_key_exchange_modes (len=2)
            Extension: key_share (len=38)
            [JA3 Fullstring: 771,4866-4867-4865-159-52394-158-107-103-57-51-157-156-61-60-53-47-255,11-10-22-23-13-43-45-51,29-23-30-25-24,0-1-2]
            [JA3: 7fa3ca2ca6346a9432112165ab2053e4]

No.     Time           Source                Destination           Protocol Length Info
      5 0.000315       127.0.0.99            127.0.0.1             TCP      66     443 → 5555 [ACK] Seq=1 Ack=252 Win=65280 Len=0 TSval=1035290446 TSecr=2748636071

Frame 5: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 1, Ack: 252, Len: 0

No.     Time           Source                Destination           Protocol Length Info
      6 0.000799       127.0.0.99            127.0.0.1             TLSv1.2  2820   Server Hello, Certificate, Server Hello Done

Frame 6: 2820 bytes on wire (22560 bits), 2820 bytes captured (22560 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 1, Ack: 252, Len: 2754
Transport Layer Security
    TLSv1.2 Record Layer: Handshake Protocol: Server Hello
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 89
        Handshake Protocol: Server Hello
            Handshake Type: Server Hello (2)
            Length: 85
            Version: TLS 1.2 (0x0303)
            Random: 11af0830db7584bf7aad505d16e370dc703fdc544b159adb30dbf9c463af852b
            Session ID Length: 32
            Session ID: 0f1cf50d513bddaef88c040e7400afc4e07bbc6c16c0fa28d2dd5545b4f2163c
            Cipher Suite: TLS_RSA_WITH_AES_128_CBC_SHA256 (0x003c)
            Compression Method: null (0)
            Extensions Length: 13
            Extension: renegotiation_info (len=1)
            Extension: encrypt_then_mac (len=0)
            Extension: extended_master_secret (len=0)
            [JA3S Fullstring: 771,60,65281-22-23]
            [JA3S: 5766872c4c46974ad7234b63e1ab69ce]
    TLSv1.2 Record Layer: Handshake Protocol: Certificate
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 2646
        Handshake Protocol: Certificate
            Handshake Type: Certificate (11)
            Length: 2642
            Certificates Length: 2639
            Certificates (2639 bytes)
    TLSv1.2 Record Layer: Handshake Protocol: Server Hello Done
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 4
        Handshake Protocol: Server Hello Done
            Handshake Type: Server Hello Done (14)
            Length: 0

No.     Time           Source                Destination           Protocol Length Info
      7 0.000824       127.0.0.1             127.0.0.99            TCP      66     5555 → 443 [ACK] Seq=252 Ack=2755 Win=63616 Len=0 TSval=2748636071 TSecr=1035290446

Frame 7: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 252, Ack: 2755, Len: 0

No.     Time           Source                Destination           Protocol Length Info
      8 0.001717       127.0.0.1             127.0.0.99            TLSv1.2  424    Client Key Exchange, Change Cipher Spec, Encrypted Handshake Message

Frame 8: 424 bytes on wire (3392 bits), 424 bytes captured (3392 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 252, Ack: 2755, Len: 358
Transport Layer Security
    TLSv1.2 Record Layer: Handshake Protocol: Client Key Exchange
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 262
        Handshake Protocol: Client Key Exchange
            Handshake Type: Client Key Exchange (16)
            Length: 258
            RSA Encrypted PreMaster Secret
                Encrypted PreMaster length: 256
                Encrypted PreMaster: 2188f86a3ab4a6c555e2e6a7ebdf8e095a698f677c125ddcfd0db3e874113e5a627bb9cc…
    TLSv1.2 Record Layer: Change Cipher Spec Protocol: Change Cipher Spec
        Content Type: Change Cipher Spec (20)
        Version: TLS 1.2 (0x0303)
        Length: 1
        Change Cipher Spec Message
    TLSv1.2 Record Layer: Handshake Protocol: Encrypted Handshake Message
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 80
        Handshake Protocol: Encrypted Handshake Message

No.     Time           Source                Destination           Protocol Length Info
      9 0.001738       127.0.0.99            127.0.0.1             TCP      66     443 → 5555 [ACK] Seq=2755 Ack=610 Win=65280 Len=0 TSval=1035290447 TSecr=2748636072

Frame 9: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 2755, Ack: 610, Len: 0

No.     Time           Source                Destination           Protocol Length Info
     10 0.003411       127.0.0.99            127.0.0.1             TLSv1.2  157    Change Cipher Spec, Encrypted Handshake Message

Frame 10: 157 bytes on wire (1256 bits), 157 bytes captured (1256 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 2755, Ack: 610, Len: 91
Transport Layer Security
    TLSv1.2 Record Layer: Change Cipher Spec Protocol: Change Cipher Spec
        Content Type: Change Cipher Spec (20)
        Version: TLS 1.2 (0x0303)
        Length: 1
        Change Cipher Spec Message
    TLSv1.2 Record Layer: Handshake Protocol: Encrypted Handshake Message
        Content Type: Handshake (22)
        Version: TLS 1.2 (0x0303)
        Length: 80
        Handshake Protocol: Encrypted Handshake Message

No.     Time           Source                Destination           Protocol Length Info
     11 0.003433       127.0.0.1             127.0.0.99            TCP      66     5555 → 443 [ACK] Seq=610 Ack=2846 Win=65536 Len=0 TSval=2748636074 TSecr=1035290449

Frame 11: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 610, Ack: 2846, Len: 0

No.     Time           Source                Destination           Protocol Length Info
     12 16.011200      127.0.0.1             127.0.0.99            TLSv1.2  151    Application Data

Frame 12: 151 bytes on wire (1208 bits), 151 bytes captured (1208 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 610, Ack: 2846, Len: 85
Transport Layer Security
    TLSv1.2 Record Layer: Application Data Protocol: http-over-tls
        Content Type: Application Data (23)
        Version: TLS 1.2 (0x0303)
        Length: 80
        Encrypted Application Data: 822c3a4b40c42ce511272c3f827e43efe55d63f6bafbafaa7eb6c63b6d7be12b03b809fa…
        [Application Data Protocol: http-over-tls]

No.     Time           Source                Destination           Protocol Length Info
     13 16.011234      127.0.0.99            127.0.0.1             TCP      66     443 → 5555 [ACK] Seq=2846 Ack=695 Win=65536 Len=0 TSval=1035306457 TSecr=2748652082

Frame 13: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 2846, Ack: 695, Len: 0

No.     Time           Source                Destination           Protocol Length Info
     14 16.018751      127.0.0.99            127.0.0.1             TLSv1.2  951    Application Data

Frame 14: 951 bytes on wire (7608 bits), 951 bytes captured (7608 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 2846, Ack: 695, Len: 885
Transport Layer Security
    TLSv1.2 Record Layer: Application Data Protocol: http-over-tls
        Content Type: Application Data (23)
        Version: TLS 1.2 (0x0303)
        Length: 880
        Encrypted Application Data: 35d3513da1608c8e8b4992248d118b082fad55fd81039b22cfb19369b6dcd35d222f643b…
        [Application Data Protocol: http-over-tls]

No.     Time           Source                Destination           Protocol Length Info
     15 16.018779      127.0.0.1             127.0.0.99            TCP      66     5555 → 443 [ACK] Seq=695 Ack=3731 Win=64768 Len=0 TSval=2748652089 TSecr=1035306464

Frame 15: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 695, Ack: 3731, Len: 0

No.     Time           Source                Destination           Protocol Length Info
     16 16.018806      127.0.0.99            127.0.0.1             TCP      66     443 → 5555 [FIN, ACK] Seq=3731 Ack=695 Win=65536 Len=0 TSval=1035306464 TSecr=2748652089

Frame 16: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 3731, Ack: 695, Len: 0

No.     Time           Source                Destination           Protocol Length Info
     17 16.018931      127.0.0.1             127.0.0.99            TLSv1.2  135    Encrypted Alert

Frame 17: 135 bytes on wire (1080 bits), 135 bytes captured (1080 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 695, Ack: 3732, Len: 69
Transport Layer Security
    TLSv1.2 Record Layer: Encrypted Alert
        Content Type: Alert (21)
        Version: TLS 1.2 (0x0303)
        Length: 64
        Alert Message: Encrypted Alert

No.     Time           Source                Destination           Protocol Length Info
     18 16.018957      127.0.0.99            127.0.0.1             TCP      66     443 → 5555 [ACK] Seq=3732 Ack=764 Win=65536 Len=0 TSval=1035306465 TSecr=2748652090

Frame 18: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 3732, Ack: 764, Len: 0

No.     Time           Source                Destination           Protocol Length Info
     19 16.018990      127.0.0.1             127.0.0.99            TCP      66     5555 → 443 [FIN, ACK] Seq=764 Ack=3732 Win=65536 Len=0 TSval=2748652090 TSecr=1035306465

Frame 19: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.99
Transmission Control Protocol, Src Port: 5555, Dst Port: 443, Seq: 764, Ack: 3732, Len: 0

No.     Time           Source                Destination           Protocol Length Info
     20 16.019013      127.0.0.99            127.0.0.1             TCP      66     443 → 5555 [ACK] Seq=3732 Ack=765 Win=65536 Len=0 TSval=1035306465 TSecr=2748652090

Frame 20: 66 bytes on wire (528 bits), 66 bytes captured (528 bits)
Ethernet II, Src: 00:00:00_00:00:00 (00:00:00:00:00:00), Dst: 00:00:00_00:00:00 (00:00:00:00:00:00)
Internet Protocol Version 4, Src: 127.0.0.99, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 443, Dst Port: 5555, Seq: 3732, Ack: 765, Len: 0

```