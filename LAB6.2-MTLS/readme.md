# Inspecting Session Resumption Handshake and mTLS Handshake

Check the lab-6-2-inspecting-tls-handshake-variants.pdf file for details.

See the textual representations of the TLS records in the wireshark files:
1. Find a Ephemeral Diffie-Hellman Key Exchange in wireshark_dhe.txt
2. Find a Mutual TLS (Server also requires Client to present a certificate) in wireshark_mtls.txt
3. Find a session resumption in wireshark_session_resumption.txt