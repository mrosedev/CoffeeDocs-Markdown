<div>
This figure consists of boxes labeled as follows:

-   These boxes are joined by the word \"or\":
    -   key length
    -   AlgorithmParameterSpec
-   Key Pair Generator (DH)
-   Key Pair
-   Private Key
-   Public Key

Labeled arrows connect these boxes:

-   `init()`{.codeph}: From key length to Key Pair Generator (DH)
-   `init()`{.codeph}: From AlgorithmParameterSpec to Key Pair Generator
    (DH)
-   `genKeyPair()`{.codeph}: From Key Pair Generator (DH) to Key Pair
-   `getPrivate()`{.codeph}: From Key Pair to Private Key
-   `getPublic()`{.codeph}: From Key Pair to Public Key

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
