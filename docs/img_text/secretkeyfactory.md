<div>
This figure consists of boxes labeled as follows:

-   Key Spec: Two boxes are labeled this
-   Secret Key Factory (AES): This box has a sublabel,
    <span class="apiname">generateSecret()</span>
-   Secret Key: Two boxes are labeled this
-   Secret Key Factory (AES): This box has a sublabel,
    <span class="apiname">getKeySpec()</span>

Unlabeled arrows connect these boxes:

-   From Key Spec \#1 to Secret Key Factory (AES),
    <span class="apiname">generateSecret()</span>
-   From Secret Key Factory (AES),
    <span class="apiname">generateSecret()</span> to Secret Key \#1
-   From Secret Key \#2 to Secret Key Factory (AES),
    <span class="apiname">getKeySpec()</span>
-   From Secret Key Factory (AES),
    <span class="apiname">getKeySpec()</span> to Key Spec \#2

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
