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

  --------------------------------------------------------------------------------------- -------------------------------------------------------------------- --
                       [![Previous](../../dcommon/gifs/leftnav.gif)\                                   [![Next](../../dcommon/gifs/rightnav.gif)\              
   <span class="icon">Previous</span>](java-generic-security-services-java-gss-api1.htm)   <span class="icon">Next</span>](when-use-java-gss-api-vs-jsse.htm)  
  --------------------------------------------------------------------------------------- -------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-202DE2FD-E2CA-44D1-9391-50127913538E}<!-- End Header -->

Introduction to JAAS and Java GSS-API Tutorials {#JSSEC-GUID-202DE2FD-E2CA-44D1-9391-50127913538E .sect1}
===============================================

<div>
This page links to a series of tutorials demonstrating various aspects
of the use of JAAS (Java Authentication and Authorization Service) and
Java GSS-API.

<span class="bold">JAAS</span> can be used for two purposes:

-   for <span class="variable">authentication</span> of users, to
    reliably and securely determine who is currently executing Java
    code, and
-   for <span class="variable">authorization</span> of users to ensure
    they have the access control rights (permissions) required to do
    security-sensitive operations.

<span class="bold">Java GSS-API</span> is used for
<span class="variable">securely exchanging messages</span> between
communicating applications. The Java GSS-API contains the Java bindings
for the Generic Security Services Application Program Interface
(GSS-API) defined in [RFC 5653](https://tools.ietf.org/html/rfc5653).
GSS-API offers application programmers uniform access to security
services atop a variety of underlying security mechanisms, including
Kerberos.

Note: JSSE is another API that can be used for secure communication. For
the differences between the two, see [When to Use Java GSS-API Versus
JSSE](when-use-java-gss-api-vs-jsse.htm#GUID-51EAFD1C-7203-40C7-A295-61062D322E8C).

The reason both JAAS and Java GSS-API tutorials are presented together
is because JAAS authentication is typically performed prior to secure
communication using Java GSS-API. Thus JAAS and Java GSS-API are related
and often used together. However, it is possible for applications to use
JAAS without Java GSS-API, and it is also possible to use Java GSS-API
without JAAS. Furthermore, JAAS itself can be used simply for
authentication or for both authentication and authorization.

The following tutorials provide working examples for all of the
scenarios described above.

1.  [Use of Java GSS-API for Secure Message Exchanges Without JAAS
    Programming](use-java-gss-api-secure-message-exchanges-jaas-programming.htm#GUID-42A2B80C-90CD-4C7A-8EED-8BFFE83CAF56)

    Demonstrates the use of the Java GSS-API for secure message
    exchanges between a client application and a server application.

2.  [JAAS
    Authentication](jaas-authentication.htm#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)

    Explains how an application can authenticate users using JAAS.

3.  [JAAS
    Authorization](jaas-authorization.htm#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F)

    Explains how to enforce user-based access controls using JAAS.

4.  [Use of JAAS Login
    Utility](use-jaas-login-utility.htm#GUID-F41E74DF-EE54-4EB1-8609-49C6D324ADF5)

    Describes a utility program that authenticates a user using JAAS and
    executes any application as that user. The appropriate user-based
    access controls are enforced while the application executes. This
    utility, as a convenience, essentially performs the operations
    described in the JAAS Authentication and JAAS Authorization
    tutorials on your behalf. Therefore it is possible to skip directly
    to this tutorial if you do not need to know how to perform JAAS
    authentication and authorization directly.

5.  [Use of JAAS Login Utility and Java GSS-API for Secure Message
    Exchanges](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8)

    The most comprehensive tutorial. The Login utility is used to
    authenticate a service user and to start up a server application as
    that user. The Login utility is also used to authenticate a client
    user and to start up a client application as that user. Finally the
    client and server applications, on behalf of their authenticated
    client and service users, exchange secure messages using the Java
    GSS-API.

6.  [More Things You Can Do with Java GSS-API and
    JAAS](more-things-you-can-do-java-gss-api-and-jaas.htm#GUID-B69758E7-D7B9-4860-BFA2-0429618374E8)

    Shows additional operations the server application in the previous
    tutorial can perform once communication has been established with
    the client application.

All applications in all tutorials in this series utilize Kerberos
Version 5 as the underlying technology for authentication and secure
communication. See [Kerberos
Requirements](kerberos-requirements1.htm#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998).
The term \"Kerberos\" used throughout the tutorials is meant to refer to
Kerberos Version 5.

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
| --------- ---------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ------------------ - | e | )\                   |
| -                    | L |             <span cl |
|                      | o | ass="icon">Contents< |
|    [![Previous](../. | g | /span>](toc.htm)     |
| ./dcommon/gifs/leftn | o |   -- --------------- |
| av.gif)\             | ] | -------------------- |
|                      | ( | -------------------- |
|    [![Next](../../dc | . | ---                  |
| ommon/gifs/rightnav. | . |                      |
| gif)\                | / |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](j | . |                      |
| ava-generic-security | / |                      |
| -services-java-gss-a | d |                      |
| pi1.htm)   <span cla | c |                      |
| ss="icon">Next</span | o |                      |
| >](when-use-java-gss | m |                      |
| -api-vs-jsse.htm)    | m |                      |
|   ------------------ | o |                      |
| -------------------- | n |                      |
| -------------------- | / |                      |
| -------------------- | g |                      |
| --------- ---------- | i |                      |
| -------------------- | f |                      |
| -------------------- | s |                      |
| ------------------ - | / |                      |
| -                    | o |                      |
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
