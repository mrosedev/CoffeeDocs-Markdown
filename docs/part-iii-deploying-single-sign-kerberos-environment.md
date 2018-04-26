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

  --------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------- --
                             [![Previous](../../dcommon/gifs/leftnav.gif)\                                                           [![Next](../../dcommon/gifs/rightnav.gif)\                                 
   <span class="icon">Previous</span>](part-ii-secure-communications-using-java-se-security-api.htm)   <span class="icon">Next</span>](part-iv-secure-communications-using-stronger-encryption-algorithms.htm)  
  --------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-549EA363-62DD-4819-BC92-4C8B23D01A1F}<!-- End Header -->

Part III : Deploying for Single Sign-On in a Kerberos Environment {#JSSEC-GUID-549EA363-62DD-4819-BC92-4C8B23D01A1F .sect1}
=================================================================

<div>
</div>
<div class="sect2">
[]{#GUID-5D0B8FD9-FF12-44E7-B7E9-7620E95E784C}

Exercise 6: Deploying for Single Sign-On {#JSSEC-GUID-5D0B8FD9-FF12-44E7-B7E9-7620E95E784C .sect2}
----------------------------------------

<div>
<div class="section">
Goal of This Exercise

The goal of this exercise is to learn how to configure a JAAS
application that uses Kerberos for authentication to achieve single
sign-on. Single sign-on means that the user needs only authenticate once
to a system or a collection of services. After the initial
authentication, the user can access other services in the system using
the same identity as he used for the initial authentication.

Single sign-on can be used to describe different types of
authentication. There are HTTP-based network single sign-on protocols.
There is Kerberos-based single sign-on for network services. In this
particular exercise, we show how to achieve single sign-on in
Kerberos-based systems by showing how to import already-acquired
Kerberos credentials from the underlying native operating system.

</div>
<!-- class="section" -->

<div class="section">
Background and Resources for This Exercise

See [Single Sign-on Using Kerberos in
Java](single-sign-using-kerberos-java1.html#GUID-D4230975-A28B-4532-B1DD-3C7219A4867F).
In addition, see the information provided in [Exercise 2: Configuring
JAAS for Kerberos
Authentication](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.html#GUID-2079DC72-5A2E-46FE-978F-42D113FFA41A)
and [Exercise 4: Using the Java SASL
API](part-ii-secure-communications-using-java-se-security-api.html#GUID-727C5CDB-8701-40B3-8355-00C8314590A3)
for background information about Kerberos and Java GSS.

</div>
<!-- class="section" -->

<div class="section">
Steps to Follow

1.  Edit the
    [`jaas-krb5.conf`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.html#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JASS-KRB5.CONF-338B5E8A)
    configuration file.

    This file contains two entries: one named
    <span class="italic">client</span> and one named
    <span class="italic">server</span>. Add the line
    `useTicketCache=true`{.codeph} to the client entry.

2.  Perform Kerberos login to the native operating system. To login to
    Kerberos, use kinit command as follows:

    ``` {.oac_no_warn dir="ltr"}
    % kinit test
    ```

    Provide a secure password.

3.  Run the client and server programs in Exercises 1 through 5 and you
    will note that the client applications no longer ask you to enter a
    password.

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
| - ------------------ | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| -------------------- | o | ass="icon">Contents< |
| ------- --           | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|          [![Previous | ] | -------------------- |
| ](../../dcommon/gifs | ( | -------------------- |
| /leftnav.gif)\       | . | ---                  |
|                      | . |                      |
|                      | / |                      |
|              [![Next | . |                      |
| ](../../dcommon/gifs | . |                      |
| /rightnav.gif)\      | / |                      |
|                      | d |                      |
|                      | c |                      |
|    <span class="icon | o |                      |
| ">Previous</span>](p | m |                      |
| art-ii-secure-commun | m |                      |
| ications-using-java- | o |                      |
| se-security-api.htm) | n |                      |
|    <span class="icon | / |                      |
| ">Next</span>](part- | g |                      |
| iv-secure-communicat | i |                      |
| ions-using-stronger- | f |                      |
| encryption-algorithm | s |                      |
| s.htm)               | / |                      |
|   ------------------ | o |                      |
| -------------------- | r |                      |
| -------------------- | a |                      |
| -------------------- | c |                      |
| -------------------- | l |                      |
| - ------------------ | e |                      |
| -------------------- | . |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ------- --           | ) |                      |
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
