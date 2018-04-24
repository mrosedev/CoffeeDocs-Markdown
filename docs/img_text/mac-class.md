<div>
This figure consists of boxes labeled as follows:

-   Data: Two boxes are labeled this
-   MAC (HmacSHA256): Two boxes are labeled this
-   Shared Secret Key
-   Signal Digest Hash: Two boxes are labeled this
-   If data was the same, the hash is the same

Labeled arrows connect these boxes:

-   `update()`{.codeph}: From Data \#1 to MAC (HmacSHA256) \#1
-   `doFinal()`{.codeph}: From Data \#1 to MAC (HmacSHA256) \#1
-   `update()`{.codeph}: From Data \#2 to MAC (HmacSHA256) \#2
-   `doFinal()`{.codeph}: From Data \#2 to MAC (HmacSHA256) \#2

Unlabeled arrows connect these boxes:

-   From Shared Secret Key to MAC (HmacSHA256) (two separate arrows)
-   From MAC (HmacSHA256) \#1 to Signed Digest Hash \#1
-   From MAC (HmacSHA256) \#2 to Signed Digest Hash \#2
-   From Signed Digest Hash \#1 to If data was the same, the hash is the
    same
-   From Signed Digest Hash \#2 to If data was the same, the hash is the
    same

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
