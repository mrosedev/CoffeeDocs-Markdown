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

  ------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------- --
                                  [![Previous](../../dcommon/gifs/leftnav.gif)\                                                [![Next](../../dcommon/gifs/rightnav.gif)\                 
   <span class="icon">Previous</span>](part-iv-secure-communications-using-stronger-encryption-algorithms.htm)   <span class="icon">Next</span>](part-vi-http-spnego-authentication.htm)  
  ------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-B51B4169-BD5D-4A19-BC2B-7F6B3ABB9B7A}<!-- End Header -->

Part V : Secure Authentication Using SPNEGO Java GSS Mechanism {#JSSEC-GUID-B51B4169-BD5D-4A19-BC2B-7F6B3ABB9B7A .sect1}
==============================================================

<div>
</div>
<div class="sect2">
[]{#GUID-47C377A7-68D9-4B16-86AF-5AE89BCB2845}

Exercise 8: Using the Java Generic Security Services (GSS) API with SPNEGO {#JSSEC-GUID-47C377A7-68D9-4B16-86AF-5AE89BCB2845 .sect2}
--------------------------------------------------------------------------

<div>
Java GSS is a framework that can support multiple security mechanisms; a
way to negotiate a security mechanism underneath GSS-API is needed. This
is available via SPNEGO.

SPNEGO is standardized at IETF in [RFC
4178.](http://www.ietf.org/rfc/rfc4178.txt) It is a pseudo-security
mechanism used to negotiate an underlying security mechanism. It
provides the flexibility for client and server to securely negotiate a
common GSS security mechanism.

Microsoft makes heavy use of SPNEGO. SPNEGO can be used to inter-operate
with Microsoft Server over HTTP, to support HTTP-based cross-platform
authentication via the Negotiate Protocol.

Currently, when using Java GSS with Kerberos, we specify the Kerberos
OID as follows:

``` {.oac_no_warn dir="ltr"}
Oid krb5Oid = new Oid("1.2.840.113554.1.2.2");
```

In order to use SPNEGO, you only need to specify the SPNEGO OID as
follows:

``` {.oac_no_warn dir="ltr"}
Oid spnegoOid = new Oid("1.3.6.1.5.5.2");
```

Then you can use the SPNEGO OID when creating a
<span class="apiname">GSSCredential</span>,
<span class="apiname">GSSContext</span>, etc.

<div class="section">
Goal of This Exercise

Currently the only security mechanism available with Java GSS is
Kerberos. The goal of this exercise is to learn how to use other Java
GSS mechanisms, such as the Simple and Protected GSS-API Negotiation
Mechanism (SPNEGO), to secure the association.

</div>
<!-- class="section" -->

<div class="section">
Steps to Follow

1.  Read the
    [`GssSpNegoClient.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.html#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__GSSSPNEGOCLIENT.JAVA-338B7C31)
    code.

2.  Compile the sample code:

    ``` {.oac_no_warn dir="ltr"}
    % javac GssSpNegoClient.java
    ```

3.  Read the
    [`GssSpNegoServer.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.html#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__GSSSPNEGOSERVER.JAVA-338B7F93)
    code.

4.  Compile the sample code:

    ``` {.oac_no_warn dir="ltr"}
    % javac GssSpNegoServer.java
    ```

5.  Launch a new window and start the server:

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf GssSpNegoServer
    ```

6.  Run the client application. `GssSpNegoClient`{.codeph} takes two
    parameters: the service name and the name of the server that the
    service is running on. For example, if the service is host running
    on the machine j1hol-001, use the following (provide a secure
    password when prompted):

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf \
    GssSpNegoClient host j1hol-001
    ```

    Sample output for running `GssSpNegoServer`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    Authenticated principal: [host/j1hol-001@J1LABS.EXAMPLE.COM]
    Waiting for incoming connections...
    Got connection from client /129.145.128.102
    SPNEGO Negotiated Mechanism = 1.2.840.113554.1.2.2 Kerberos V5
    Context Established!
    Client principal is test@J1LABS.EXAMPLE.COM
    Server principal is
    host/j1hol-001@J1LABS.EXAMPLE.COM
    Mutual authentication took place!
    Received data "Hello There!" of length 12
    Confidentiality applied: true
    Sending: Hello There! Thu May 06 12:11:15 PDT 2005
    ```

    Sample output for running `GssSpNegoClient`{.codeph}
    (`password`{.codeph} is replaced with the password you provided
    before):

    ``` {.oac_no_warn dir="ltr"}
    Kerberos password for test: password
    Authenticated principal: [test@J1LABS.EXAMPLE.COM]
    Connected to address j1hol-001/129.145.128.102
    SPNEGO Negotiated Mechanism = 1.2.840.113554.1.2.2 Kerberos V5
    Context Established!
    Client principal is test@J1LABS.EXAMPLE.COM
    Server principal is host@j1hol-001
    Mutual authentication took place!
    Sending message: Hello There!
    Will read token of size 93
    Received message: Hello There! Thu May 06 12:11:15 PDT 2005
    ```

</div>
<!-- class="section" -->

<div class="section">
Summary

In this exercise, you learned how to write a client-server application
that uses the Java GSS API with SPNEGO to negotiate an underlying
security mechanism, such as Kerberos, and communicate securely using
Kerberos as the underlying authentication system.

<div class="infoboxnote" id="GUID-47C377A7-68D9-4B16-86AF-5AE89BCB2845__GUID-587C7F7F-0122-4137-863F-1A662A547BCA">
Note:

Microsoft has implemented certain variations of the SPNEGO protocol,
hence to inter-operate with Microsoft, we have added a separate mode via
a new system property `sun.security.spnego.msinterop`{.codeph}. This
property is enabled to true by default. To disable it, you need to
explicitly set this property to false. To enable SPNEGO debugging, you
can set the system property `sun.security.spnego.debug=true`{.codeph}.

</div>
</div>
<!-- class="section" -->

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
| -------------------- | a |       [![Go To Table |
| ----------- -------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| ----- --             | o | ass="icon">Contents< |
|                      | g | /span>](toc.htm)     |
|               [![Pre | o |   -- --------------- |
| vious](../../dcommon | ] | -------------------- |
| /gifs/leftnav.gif)\  | ( | -------------------- |
|                      | . | ---                  |
|                      | . |                      |
|        [![Next](../. | / |                      |
| ./dcommon/gifs/right | . |                      |
| nav.gif)\            | . |                      |
|                      | / |                      |
|    <span class="icon | d |                      |
| ">Previous</span>](p | c |                      |
| art-iv-secure-commun | o |                      |
| ications-using-stron | m |                      |
| ger-encryption-algor | m |                      |
| ithms.htm)   <span c | o |                      |
| lass="icon">Next</sp | n |                      |
| an>](part-vi-http-sp | / |                      |
| nego-authentication. | g |                      |
| htm)                 | i |                      |
|   ------------------ | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| ----------- -------- | a |                      |
| -------------------- | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| ----- --             | . |                      |
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
