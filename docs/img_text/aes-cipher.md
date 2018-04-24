<div>
This figure consists of five boxes:

-   Application: This box contains the following pseudocode:

    ``` {.oac_no_warn dir="ltr"}
    c:Cipher.getInstance("AES");
    ```

-   JCA/JCE: This box contains the following list:

    -   Signature
    -   Message Digest
    -   Key Script Generator
    -   Key Factory
    -   Algorithm Parameters
    -   Cipher
    -   Key Agreement
    -   Key Generator
    -   Secret Key Factory
    -   MAC

-   CSP, CSP2, CSP3: These boxes represent cryptographic service
    providers

-   The fifth box represents CSP3. It contains the following headers and
    pseudocode:

    -   Provider.class

        ``` {.oac_no_warn dir="ltr"}
        "Cipher.AES" -> "com.foo.AESCipher"
        ```

    -   com.foo.AESCipher.class

        ``` {.oac_no_warn dir="ltr"}
        package com.foo:
          class AESCipher extends CipherSPi {
            .
            .
            .
          }
        ```

Arrows connect the boxes as follows:

-   From Application to JCA/JCE
-   From JCA/JCE to CSP1, CSP2, and CSP3 (the arrow branches)

A dotted line connects CSP3 to the headings Provider.class and
com.foo.AESCipher.class

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
