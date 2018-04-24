<div>
This figure consists of boxes labeled as follows:

-   Generated by a Key Pair Generator: Contains a box labeled Private
    Key/Public Key
-   Data
-   These two boxes are attached to each other:
    -   Signature (SHA256withRSA): Box 1 of 2
    -   Sign
-   Signature Bytes
-   These two boxes are attached to each other:
    -   Signature (SHA256withRSA): Box 2 of 2
    -   Verify
-   Yes/No

Labeled arrows connect the following boxes:

-   `update()`{.codeph}: From Data to Signature (SHA256withRSA) \#1
-   `update()`{.codeph}: From Data to Signature (SHA256withRSA) \#2
-   `sign()`{.codeph}: From Signature (SHA256withRSA) \#1 to Signature
    Bytes
-   `verify()`{.codeph}: From Signature Bytes Data to Signature
    (SHA256withRSA) \#2

Unlabeled arrows connect these boxes:

-   From Generated by a Key Pair Generator to Signature (SHA256withRSA)
    \#1 and Signature (SHA256withRSA) \#2 (the arrow branches)
-   From Signature (SHA256withRSA) \#2 to Yes/No

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>