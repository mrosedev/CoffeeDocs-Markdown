<div>
The figure illustrates the original Java platform security model. It
consists of two layers. The top layer is the JVM. The bottom layer
contains an icon that represents valuable resources such as files.

The top layer contains a a sandbox icon. An arrow points from a local
code icon to the JVM layer; local code is trusted to have full access to
vital system resources (such as the file system). An arrow points from a
remote code icon to the sandbox icon; downloaded remote code is not
trusted and can access only the limited resources provided inside the
sandbox.

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
