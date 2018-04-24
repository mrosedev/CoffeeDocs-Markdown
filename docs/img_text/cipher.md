<div>
This figure consists of boxes labeled as follows:

-   Key: Contains a box labeled Secret Key
-   Plaintext
-   These two boxes are attached to each other:
    -   Cipher (AES): Box 1 of 2
    -   Encrypt
-   Algorithm Parameters
-   Ciphertext
-   These two boxes are attached to each other:
    -   Cipher (AES): Box 2 of 2
    -   Decrypt
-   Plaintext

Labeled arrows connect these boxes:

-   `update()`{.codeph}: From Plaintext to the Cipher (AES) \#1
-   `doFinal()`{.codeph}: From Plaintext to Encrypt
-   `update()`{.codeph}: From Ciphertext to the Cipher (AES) \#2
-   `doFinal()`{.codeph}: From Ciphertext to Decrypt

Unlabeled arrows connect these boxes:

-   From Key to the Cipher (AES) \#1 and Cipher (AES) \#2 (the arrow
    branches)
-   From Cipher (AES) \#1 to Algorithm Parameters
-   From Algorithm Parameters to the Cipher (AES) compartment of the
    Decrypt box
-   From Cipher (AES) \#2 to Plaintext
-   From Decrypt to Plaintext

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
