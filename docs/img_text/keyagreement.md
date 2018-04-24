<div>
This figure is divided into halves by a dashed line. The top half is
labeled Alice, and the bottom half is labeled Bob. The figure consists
of boxes labeled as follows:

-   These boxes are in Alice\'s half:
    -   Key: This box contains a box labeled Alice\'s Private
    -   Key: This box contains a box labeled Bob\'s Public
    -   Key Agreement (DH)
    -   Bytes: This box has another label, Bytes
-   These boxes are in Bob\'s half:
    -   Key: This box contains a box labeled Bob\'s Private
    -   Key: This box contains a box labeled Alice\'s Public
    -   Key Agreement (DH)
    -   Bytes: This box has another label, Bytes

Labeled arrows connect these boxes:

-   These arrows are in Alice\'s half:
    -   `init()`{.codeph}: From Alice\'s Private Key to Key Agreement
        (DH)
    -   `doPhase()`{.codeph}: From Bob\'s Public Key to Key Agreement
        (DH)
    -   `generateSecret()`{.codeph}: From Key Agreement (DH) to Bytes
-   These arrows are in Bob\'s half:
    -   `init()`{.codeph}: From Bob\'s Private Key to Key Agreement (DH)
    -   `doPhase()`{.codeph}: From Alice\'s Public Key to Key Agreement
        (DH)
    -   `generateSecret()`{.codeph}: From Key Agreement (DH) to Bytes

A double-headed arrow joins the Bytes boxes in Alice\'s and Bob\'s
halves. This arrow is labeled \"Should be the same.\"

-   `init()`{.codeph}: From key length to Key Generator (AES)
-   `init()`{.codeph}: From AlgorithmParameterSpec to Key Generator
    (AES)
-   `generateKey()`{.codeph}: From Key Generator (AES) to Secret Pair

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
