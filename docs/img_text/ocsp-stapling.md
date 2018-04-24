<div>
This is a text description of the figure Client-driven OCSP.

The figure illustrates how client-driven OCSP fits into the TLS
Handshake. The sequence is:

1.  The client sends a ClientHello message with a status request
    extension to the server.

2.  The server receives this message and processes it.

3.  The server sends an OCSP request to the OCSP responder for this
    certificate.

4.  The OCSP responder receives the request, then returns an OCSP
    response to the server.

5.  The server sends a ServerHello message with a status request
    extension to the client.

6.  The server sends a certificate message to the client.

7.  The server sends a certificate status message to the client.

8.  The server sends additional ServerHello messages, followed by a
    ServerHello done messages to the client.

9.  The client validates the server certificate

10. The client checks the OCSP response in the certificate status
    message to determine if the certificate has been revoked.

11. The client and server complete the TLS handshake (this takes
    multiple additional messages).

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
