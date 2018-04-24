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

  -------------------------------------------------- -------------------------------------------------------------- --
    [![Previous](../../dcommon/gifs/leftnav.gif)\              [![Next](../../dcommon/gifs/rightnav.gif)\           
   <span class="icon">Previous</span>](preface.htm)   <span class="icon">Next</span>](java-security-overview1.htm)  
  -------------------------------------------------- -------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-04EC663E-8D01-43B8-8A93-5CB1B7BC60BF}<!-- End Header -->

<span class="enumeration_chapter">1 </span>General Security {#JSSEC-GUID-04EC663E-8D01-43B8-8A93-5CB1B7BC60BF .sect1}
===========================================================

<div>
[Java Security
Overview](java-security-overview1.htm#GUID-2EF91196-D468-4D0F-8FDC-DA2BEA165D10 "Java security includes a large set of APIs, tools, and implementations of commonly-used security algorithms, mechanisms, and protocols. The Java security APIs span a wide range of areas, including cryptography, public key infrastructure, secure communication, authentication, and access control. Java security technology provides the developer with a comprehensive security framework for writing applications, and also provides the user or administrator with a set of tools to securely manage applications.")
introduces you to cryptography, public key infrastructure,
authentication, secure communication, access control, and XML
signatures.

[Java Security
Architecture](java-se-platform-security-architecture.htm#GUID-C203D80F-C730-45C3-AB95-D4E61FD6D89C)
provides an overview of the motivation of major security features, an
introduction to security classes and their usage, a discussion of the
impact of the security architecture on code, and thoughts on writing
security-sensitive code.

[Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
describes the set of standard names for algorithms, certificate and
keystore types that Java SE requires and uses.

[Permissions in the
JDK](permissions-jdk1.htm#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.")
describes the built-in JDK permission types and discusses the risks of
granting each permission.

[Troubleshooting
Security](troubleshooting-security.htm "To monitor security access, you can set the java.security.debug system property, which determines what trace messages are printed during execution.")
lists options for the <span class="apiname">java.security.debug</span>
system property that enable you to monitor security access.

</div>
</div>
<!-- class="ind" --><!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   -- --------------- |
| -------------------- | [ | -------------------- |
| ------------ ------- | O | -------------------- |
| -------------------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| --------------- --   | c |  Of Contents](../../ |
|     [![Previous](../ | l | dcommon/gifs/toc.gif |
| ../dcommon/gifs/left | e | )\                   |
| nav.gif)\            | L |             <span cl |
|    [![Next](../../dc | o | ass="icon">Contents< |
| ommon/gifs/rightnav. | g | /span>](toc.htm)     |
| gif)\                | o |   -- --------------- |
|    <span class="icon | ] | -------------------- |
| ">Previous</span>](p | ( | -------------------- |
| reface.htm)   <span  | . | ---                  |
| class="icon">Next</s | . |                      |
| pan>](java-security- | / |                      |
| overview1.htm)       | . |                      |
|   ------------------ | . |                      |
| -------------------- | / |                      |
| ------------ ------- | d |                      |
| -------------------- | c |                      |
| -------------------- | o |                      |
| --------------- --   | m |                      |
|                      | m |                      |
|                      | o |                      |
|                      | n |                      |
|                      | / |                      |
|                      | g |                      |
|                      | i |                      |
|                      | f |                      |
|                      | s |                      |
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
