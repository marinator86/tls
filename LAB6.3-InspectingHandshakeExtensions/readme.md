# Inspecting Handshake Extensions

Check the lab-6-3-inspecting-tls-handshake-extensions.pdf file for details.

1. In wireshark_ocsp_stapling.txt we are shown how OCSP Stapling is requested and fulfilled
by the server.
2. In wireshark_sni.txt, we are shown how Client and Server negotiate Session Ticket & Server Name
Indication and how it is used to request the certificate for facebook.com from the server. 
Moreover, a **Session Ticket** is issued from the server before Change Cipher Spec.
3. In wireshark_session_resumption.txt, we are shown how the previously generated session ticket
is used to resume the session.