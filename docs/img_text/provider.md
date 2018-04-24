<div>
This figure consists of a cylinder labeled Provider C and a box. Dotted
lines are used to indicate that Provider C contains the contents of the
box. The box contains the following headers and Java code:

-   `provider.java`

    ``` {.oac_no_warn dir="ltr"}
    public class fooJCA extends Provider {
        .
        .
        .
        put("MessageDigest.SHA-256", "com.foo.SHA256");
        .
        .
        .
    {}
    ```

-   `com.foo.SHA256.java`

    ``` {.oac_no_warn dir="ltr"}
    package com.foo;
    public class SHA256 extends
    MessageDigestSpi {
       .
       .
       .
    }
    ```

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
