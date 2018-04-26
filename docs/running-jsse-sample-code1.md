<div class="header">
[]{#top}

<div class="zz-skip-header">
[Go to primary content](#BEGIN)

</div>
+-----------------------------------+----------------------------------:+
| **Java Platform, Standard Edition |   -- ---------------------------- |
| Security Developer's Guide**\     | ------------------------------    |
| **<span>Release 11</span>**\      |       [![Go To Table Of Contents] |
| E94828-01                         | (../../dcommon/gifs/toc.gif)\     |
|                                   |             <span class="icon">Co |
|                                   | ntents</span>](toc.htm)           |
|                                   |   -- ---------------------------- |
|                                   | ------------------------------    |
+-----------------------------------+-----------------------------------+

------------------------------------------------------------------------

  -------------------------------------------------------------------------------------------- --------------------------------------------------------- --
                         [![Previous](../../dcommon/gifs/leftnav.gif)\                                [![Next](../../dcommon/gifs/rightnav.gif)\         
   <span class="icon">Previous</span>](java-secure-socket-extension-jsse-reference-guide.htm)   <span class="icon">Next</span>](sample-truststores.htm)  
  -------------------------------------------------------------------------------------------- --------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-593BCDF6-1F66-4B7E-AED3-759A68111109}<!-- End Header -->

<span class="enumeration_chapter">9 </span>Running the JSSE Sample Code {#JSSEC-GUID-593BCDF6-1F66-4B7E-AED3-759A68111109 .sect1}
=======================================================================

<div>
The following JSSE sample programs illustrate how to use JSSE:

-   [Sample Code Illustrating a Secure Socket Connection Between a
    Client and a
    Server](sample-code-illustrating-secure-socket-connection-client-and-server.html#GUID-A4D59ABB-62AF-4FC0-900E-A795FDC84E41 "These samples illustrate how to set up a secure socket connection between a client and a server.")
-   [Sample Code Illustrating HTTPS
    Connections](sample-code-illustrating-https-connections.html#GUID-54F1F19F-0F93-4877-A4A1-46ACD03FD7CB)
-   [Sample Code Illustrating a Secure RMI
    Connection](sample-code-illustrating-secure-rmi-connection.html#GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87)
-   [Sample Code Illustrating the Use of an
    SSLEngine](sample-code-illustrating-use-sslengine.html#GUID-EDE915F0-427B-48C7-918F-23C44384B862)

When you use the sample code, be aware that the sample programs are
designed to illustrate how to use JSSE. They are not designed to be
robust applications.

<div class="p">
<div class="infoboxnote" id="GUID-593BCDF6-1F66-4B7E-AED3-759A68111109__GUID-D989BF26-8A0F-46AD-A2E6-83C41C9642B3">
Note:

Setting up secure communications involves complex algorithms. The sample
programs provide no feedback during the setup process. When you run the
programs, be patient: you may not see any output for a while. If you run
the programs with the `javax.net.debug`{.codeph} system property set to
`all`{.codeph}, you will see more feedback. For an introduction to
reading this debug information, see [Debugging SSL/TLS
Connections](java-secure-socket-extension-jsse-reference-guide.html#GUID-4D421910-C36D-40A2-8BA2-7D42CCBED3C6 "Understanding SSL/TLS connection problems can sometimes be difficult, especially when it is not clear what messages are actually being sent and received. JSSE has a built-in debug facility and is activated by the System property javax.net.debug.").

</div>
</div>
</div>
</div>
<!-- class="ind" --><!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   -- --------------- |
| -------------------- | [ | -------------------- |
| -------------------- | O | -------------------- |
| -------------------- | r | ---                  |
| -------------- ----- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ------------ --      | e | )\                   |
|                      | L |             <span cl |
|      [![Previous](.. | o | ass="icon">Contents< |
| /../dcommon/gifs/lef | g | /span>](toc.htm)     |
| tnav.gif)\           | o |   -- --------------- |
|                      | ] | -------------------- |
|   [![Next](../../dco | ( | -------------------- |
| mmon/gifs/rightnav.g | . | ---                  |
| if)\                 | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](j | . |                      |
| ava-secure-socket-ex | . |                      |
| tension-jsse-referen | / |                      |
| ce-guide.htm)   <spa | d |                      |
| n class="icon">Next< | c |                      |
| /span>](sample-trust | o |                      |
| stores.htm)          | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| -------------------- | / |                      |
| -------------- ----- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ------------ --      | s |                      |
|                      | / |                      |
|                      | o |                      |
|                      | r |                      |
|                      | a |                      |
|                      | c |                      |
|                      | l |                      |
|                      | e |                      |
|                      | . |                      |
|                      | g |                      |
|                      | i |                      |
|                      | f |                      |
|                      | ) |                      |
|                      | { |                      |
|                      | . |                      |
|                      | c |                      |
|                      | o |                      |
|                      | p |                      |
|                      | y |                      |
|                      | r |                      |
|                      | i |                      |
|                      | g |                      |
|                      | h |                      |
|                      | t |                      |
|                      | l |                      |
|                      | o |                      |
|                      | g |                      |
|                      | o |                      |
|                      | } |                      |
|                      | [ |                      |
|                      | \ |                      |
|                      | < |                      |
|                      | s |                      |
|                      | p |                      |
|                      | a |                      |
|                      | n |                      |
|                      |   |                      |
|                      | c |                      |
|                      | l |                      |
|                      | a |                      |
|                      | s |                      |
|                      | s |                      |
|                      | = |                      |
|                      | " |                      |
|                      | c |                      |
|                      | o |                      |
|                      | p |                      |
|                      | y |                      |
|                      | r |                      |
|                      | i |                      |
|                      | g |                      |
|                      | h |                      |
|                      | t |                      |
|                      | l |                      |
|                      | o |                      |
|                      | g |                      |
|                      | o |                      |
|                      | " |                      |
|                      | > |                      |
|                      | C |                      |
|                      | o |                      |
|                      | p |                      |
|                      | y |                      |
|                      | r |                      |
|                      | i |                      |
|                      | g |                      |
|                      | h |                      |
|                      | t |                      |
|                      |   |                      |
|                      | © |                      |
|                      |   |                      |
|                      | 1 |                      |
|                      | 9 |                      |
|                      | 9 |                      |
|                      | 3 |                      |
|                      | , |                      |
|                      | 2 |                      |
|                      | 0 |                      |
|                      | 1 |                      |
|                      | 8 |                      |
|                      | , |                      |
|                      | O |                      |
|                      | r |                      |
|                      | a |                      |
|                      | c |                      |
|                      | l |                      |
|                      | e |                      |
|                      |   |                      |
|                      | a |                      |
|                      | n |                      |
|                      | d |                      |
|                      | / |                      |
|                      | o |                      |
|                      | r |                      |
|                      |   |                      |
|                      | i |                      |
|                      | t |                      |
|                      | s |                      |
|                      |   |                      |
|                      | a |                      |
|                      | f |                      |
|                      | f |                      |
|                      | i |                      |
|                      | l |                      |
|                      | i |                      |
|                      | a |                      |
|                      | t |                      |
|                      | e |                      |
|                      | s |                      |
|                      | . |                      |
|                      |   |                      |
|                      | A |                      |
|                      | l |                      |
|                      | l |                      |
|                      |   |                      |
|                      | r |                      |
|                      | i |                      |
|                      | g |                      |
|                      | h |                      |
|                      | t |                      |
|                      | s |                      |
|                      |   |                      |
|                      | r |                      |
|                      | e |                      |
|                      | s |                      |
|                      | e |                      |
|                      | r |                      |
|                      | v |                      |
|                      | e |                      |
|                      | d |                      |
|                      | . |                      |
|                      | < |                      |
|                      | / |                      |
|                      | s |                      |
|                      | p |                      |
|                      | a |                      |
|                      | n |                      |
|                      | > |                      |
|                      | ] |                      |
|                      | ( |                      |
|                      | . |                      |
|                      | . |                      |
|                      | / |                      |
|                      | . |                      |
|                      | . |                      |
|                      | / |                      |
|                      | d |                      |
|                      | c |                      |
|                      | o |                      |
|                      | m |                      |
|                      | m |                      |
|                      | o |                      |
|                      | n |                      |
|                      | / |                      |
|                      | h |                      |
|                      | t |                      |
|                      | m |                      |
|                      | l |                      |
|                      | / |                      |
|                      | c |                      |
|                      | p |                      |
|                      | y |                      |
|                      | r |                      |
|                      | . |                      |
|                      | h |                      |
|                      | t |                      |
|                      | m |                      |
|                      | ) |                      |
+----------------------+---+----------------------+

</div>
<!-- class="footer" -->
