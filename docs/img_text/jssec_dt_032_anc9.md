<div>
The figure illustrates the Java SE security model. It consists of two
layers. The top layer is the JVM. This layer contains a sandbox icon. It
also contains three squares, which represent local code. This is because
there is no longer the built-in notion of trusted code. Local code is
subjected to the same security control as applets and can be run with
different permissions. The bottom layer contains an icon that represents
valuable resources such as files.

Three icons -- security policy, local or remote code (signed or not),
and class loader -- each have an arrow that points to a rectangle
labeled <span class="q">\"input\"</span>. An arrow points from the input
rectangle to each of the squares that represent local code. A fourth
arrow points from the input rectangle to the sandbox icon.

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
