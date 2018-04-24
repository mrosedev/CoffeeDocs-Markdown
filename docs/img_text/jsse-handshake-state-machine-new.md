<div>
This image illustrates DTLS handshake statuses and different messages
during the DTLS handshake. The following steps are performed before the
status of the handshake is determined:

-   Create SSL/TLS SSLEngines
-   Create Buffers
-   Set Client of Server mode
-   Begin Handshake
-   Set Maximum Fragment Size

This image illustrates some of the possible handshake statuses. The
section [Understanding SSLEngine Operation
Statuses](../java-secure-socket-extension-jsse-reference-guide.htm#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744 "The status of the SSLEngine is represented by SSLEngineResult.Status.")
describes these statuses in more detail:

-   `NEED_TASK`{.codeph}
-   `NEED_WRAP`{.codeph}
-   `NEED_UNWRAP`{.codeph}
-   `NEED_UNWRAP_AGAIN`{.codeph}
-   `FINISHED`{.codeph}

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
