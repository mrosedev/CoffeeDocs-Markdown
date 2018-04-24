<div>
The figure illustrates the JDK 1.1 security model, which introduces the
concept of a <span class="q">\"signed applet\"</span>. It consists of
two layers. The top layer is the JVM. This layer contains a sandbox
icon. The bottom layer contains an icon that represents valuable
resources such as files.

An arrow points from a local code icon to the JVM layer; local code is
trusted to have full access to vital system resources (such as the file
system). An arrow points from a remote code icon. This arrow points to
two arrows. One arrow points to the sandbox icon. The other arrow points
to the JVM layer; this branch is labeled
<span class="q">\"trusted\"</span>. The trusted arrow represents a
correctly digitally signed applet, which is treated as if it is trusted
local code. The arrow that points to the sandbox icon represents
untrusted code, such as an unsigned applet.

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
