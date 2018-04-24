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

  ---------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------- --
                       [![Previous](../../dcommon/gifs/leftnav.gif)\                                                  [![Next](../../dcommon/gifs/rightnav.gif)\                             
   <span class="icon">Previous</span>](introduction-jaas-and-java-gss-api-tutorials1.htm)   <span class="icon">Next</span>](use-java-gss-api-secure-message-exchanges-jaas-programming.htm)  
  ---------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-51EAFD1C-7203-40C7-A295-61062D322E8C}<!-- End Header -->

When to Use Java GSS-API Versus JSSE {#JSSEC-GUID-51EAFD1C-7203-40C7-A295-61062D322E8C .sect1}
====================================

<div>
Java GSS-API and JSSE provide you with the same basic set of security
features:

1.  Client-server authentication
2.  Encryption and integrity protection of transmitted data

However, there are some key differences between the two. This document
lists some of them to help you decide which might be more appropriate in
your environment:

1.  <span class="bold">Kerberos Single Sign-On Support</span>

    GSS-API contains support for Kerberos as a mandatory security
    mechanism. This means that if your desktop has Kerberos support, you
    can write Java GSS-API based applications that never prompt the user
    for a password.

    [RFC 2712](https://tools.ietf.org/html/rfc2712) defined Kerberos
    Cipher Suites for TLS, but the document is out of date and does not
    support modern encryption types like AES.

2.  <span class="bold">Communications API</span>

    JSSE supports a socket-based API. JSSE sockets extend the socket
    classes found in `java.net`{.codeph} and JSSE socket factories
    extend the socket factories found in `javax.net`{.codeph}. Thus, if
    your application is written such that its security needs to be
    configured via a socket factory, then JSSE might be more appropriate
    for you. JSSE sockets need to use some reliable transport.
    Typically, implementations use TCP.

    Java GSS-API, on the other hand, is a token-based API that relies on
    the application to do the communication. This means that the
    application can use TCP sockets, UDP datagrams, or any other channel
    that will allow it to transport Java GSS-API generated tokens. If
    your application has varying communication protocol needs, then Java
    GSS-API might be more appropriate for you. Java GSS-API can read and
    write its tokens using input and output streams. However, you will
    need to set up the streams yourself.

3.  <span class="bold">Credential Delegation</span>

    Java GSS-API allows the client to delegate its credentials to the
    server when using Kerberos. If your application will be deployed in
    a multi-tier environment where intermediaries need to impersonate
    clients when talking to backend layers, Java GSS-API might be more
    appropriate for you.

4.  <span class="bold">Selective Encryption</span>

    Because Java GSS-API is token-based, you can choose to selectively
    encrypt certain messages but not all. If your application needs to
    intersperse plaintext and ciphertext messages, Java GSS-API might be
    more appropriate for you.

5.  <span class="bold">Protocol Requirements</span>

    JSSE provides an implementation of the TLS protocol defined in [RFC
    5246](https://tools.ietf.org/html/rfc5246). Java GSS-API provides an
    implementation of the GSS-API framework defined in [RFC
    5653](https://tools.ietf.org/html/rfc5653), as well as an
    implementation of the Kerberos Version 5 mechanism defined in [RFC
    1964](https://tools.ietf.org/html/rfc1964). (On Microsoft Windows
    platforms, this may be known as SSPI with Kerberos.) Some servers
    such as HTTPS servers will require you to use TLS, in which case
    JSSE will be appropriate for you. Other servers such as LDAP servers
    using SASL might need GSS-API with Kerberos, in which case Java
    GSS-API will be appropriate for you.

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
| ---------- --------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| -------- --          | o | ass="icon">Contents< |
|                      | g | /span>](toc.htm)     |
|    [![Previous](../. | o |   -- --------------- |
| ./dcommon/gifs/leftn | ] | -------------------- |
| av.gif)\             | ( | -------------------- |
|                      | . | ---                  |
|                   [! | . |                      |
| [Next](../../dcommon | / |                      |
| /gifs/rightnav.gif)\ | . |                      |
|                      | . |                      |
|                      | / |                      |
|    <span class="icon | d |                      |
| ">Previous</span>](i | c |                      |
| ntroduction-jaas-and | o |                      |
| -java-gss-api-tutori | m |                      |
| als1.htm)   <span cl | m |                      |
| ass="icon">Next</spa | o |                      |
| n>](use-java-gss-api | n |                      |
| -secure-message-exch | / |                      |
| anges-jaas-programmi | g |                      |
| ng.htm)              | i |                      |
|   ------------------ | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| ---------- --------- | r |                      |
| -------------------- | a |                      |
| -------------------- | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| -------- --          | . |                      |
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
