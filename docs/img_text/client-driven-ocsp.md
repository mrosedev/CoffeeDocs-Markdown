<div>
This is a text description of the figure Client-driven OCSP.

The figure illustrates how client-driven OCSP fits into the TLS
Handshake. The sequence is:

1.  The client sends a ClientHello message to the server.

2.  The server receives this message and processes it.

3.  The server sends a ServerHello message, followed by additional
    ServerHello messages, followed by a ServerHello done message to the
    client.

4.  The client validates the server certificate. The client sends an
    OCSP request to the OCSP responder for this certificate.

5.  The OCSP responder receives the request, then returns an OCSP
    response to the client.

6.  The client checks the OCSP response to determine if the certificate
    has been revoked.

7.  The client and server complete the TLS handshake (this takes
    multiple additional messages).

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
