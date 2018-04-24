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

  --------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------- --
                 [![Previous](../../dcommon/gifs/leftnav.gif)\                                                         [![Next](../../dcommon/gifs/rightnav.gif)\                                          
   <span class="icon">Previous</span>](single-sign-using-kerberos-java1.htm)   <span class="icon">Next</span>](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm)  
  --------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-5DEF0954-0AB3-4AEB-9981-C2A172D5EDE9}<!-- End Header -->

Advanced Security Programming in Java SE Authentication, Secure Communication and Single Sign-On {#JSSEC-GUID-5DEF0954-0AB3-4AEB-9981-C2A172D5EDE9 .sect1}
================================================================================================

<div>
Java SE offers a rich set of APIs and features for developing secure
Java applications and services. The exercise sessions listed here can
help you to use the Java SE GSS APIs to build applications that
authenticate their users, to communicate securely with other
applications and services, and help you to configure your applications
in a Kerberos environment to achieve Single Sign-On. In addition, you
will also learn how to use stronger encryption algorithms in a Kerberos
environment, and how to use Java GSS mechanisms such as SPNEGO to secure
the association.

<div class="section">
Setting up your Development Environment

Set up your development environment as follows before proceeding to the
first exercise:

1.  Install and set up a Solaris machine (required for [Exercise 7:
    Configuring to Use Stronger Encryption Algorithms in a Kerberos
    Environment, to Secure the
    Communication](part-iv-secure-communications-using-stronger-encryption-algorithms.htm#GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212)).
2.  Configure a Kerberos server on a Solaris machine with accounts used
    by the exercises. See [Appendix A: Setting up Kerberos
    Accounts](appendix-setting-kerberos-accounts.htm#GUID-D1F41B0A-E756-49CB-828A-422DC23E572B).
3.  Set up the Key Distribution Center (KDC) on your Solaris machine and
    start the Kerberos server.
4.  Set up the Kerberos configuration on your client machine.
5.  Set up the JDK environment:
    -   Set up the `JAVA_HOME`{.codeph} environment variable to point to
        the JDK installation directory

    -   Place `%JAVA_HOME%\bin`{.codeph} (Windows) or
        `$JAVA_HOME/bin`{.codeph} (Solaris/Linux) in the `PATH`{.codeph}
        environment variable.

</div>
<!-- class="section" -->

<div class="section">
Exercises

This session includes six lessons. Each part contains one or more coding
exercises. Work through the exercises in sequence:

-   [Part I : Secure Authentication using the Java Authentication and
    Authorization Service
    (JAAS)](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-42416198-9AEE-428C-80EF-2A56488B5890)
    -   [Exercise 1: Using the JAAS
        API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8)
    -   [Exercise 2: Configuring JAAS for Kerberos
        Authentication](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-2079DC72-5A2E-46FE-978F-42D113FFA41A)
-   [Part II : Secure Communications using the Java SE Security
    API](part-ii-secure-communications-using-java-se-security-api.htm#GUID-98B02DB0-13DB-4175-9485-3449E1A241B5)
    -   [Exercise 3: Using the Java Generic Security Service (GSS)
        API](part-ii-secure-communications-using-java-se-security-api.htm#GUID-1E4E43BA-EC38-435E-A426-7A88E52F34DF)
    -   [Exercise 4: Using the Java SASL
        API](part-ii-secure-communications-using-java-se-security-api.htm#GUID-727C5CDB-8701-40B3-8355-00C8314590A3)
    -   [Exercise 5: Using the Java Secure Socket Extension with
        Kerberos](part-ii-secure-communications-using-java-se-security-api.htm#GUID-9AAFC7BB-8562-4E3E-B5EF-E33F30E779D1)
-   [Part III : Deploying for Single Sign-On in a Kerberos
    Environment](part-iii-deploying-single-sign-kerberos-environment.htm#GUID-549EA363-62DD-4819-BC92-4C8B23D01A1F)
    -   [Exercise 6: Deploying for Single
        Sign-On](part-iii-deploying-single-sign-kerberos-environment.htm#GUID-5D0B8FD9-FF12-44E7-B7E9-7620E95E784C)
-   [Part IV : Secure Communications Using Stronger Encryption
    Algorithms](part-iv-secure-communications-using-stronger-encryption-algorithms.htm#GUID-49820DF7-0DED-4C63-8DB8-89718501ADB1)
    -   [Exercise 7: Configuring to Use Stronger Encryption Algorithms
        in a Kerberos Environment, to Secure the
        Communication](part-iv-secure-communications-using-stronger-encryption-algorithms.htm#GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212)
-   [Part V : Secure Authentication Using SPNEGO Java GSS
    Mechanism](part-v-secure-authentication-using-spnego-java-gss-mechanism.htm#GUID-B51B4169-BD5D-4A19-BC2B-7F6B3ABB9B7A)
    -   [Exercise 8: Using the Java Generic Security Services (GSS) API
        with
        SPNEGO](part-v-secure-authentication-using-spnego-java-gss-mechanism.htm#GUID-47C377A7-68D9-4B16-86AF-5AE89BCB2845)
-   [Part VI: HTTP/SPNEGO
    Authentication](part-vi-http-spnego-authentication.htm#GUID-996F729E-5FEA-4E29-A32A-78FB510B2D80)
    -   [Exercise 9: Using HTTP/SPNEGO
        Authentication](part-vi-http-spnego-authentication.htm#GUID-2978DB58-6217-4E29-95EF-2C1F25F7C37F)

</div>
<!-- class="section" -->

</div>
</div>
<!-- class="ind" --><!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   -- --------------- |
| -------------------- | [ | -------------------- |
| -------------------- | O | -------------------- |
| ----------------- -- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| -------------------- | o | ass="icon">Contents< |
| -- --                | g | /span>](toc.htm)     |
|                  [![ | o |   -- --------------- |
| Previous](../../dcom | ] | -------------------- |
| mon/gifs/leftnav.gif | ( | -------------------- |
| )\                   | . | ---                  |
|                      | . |                      |
|                    [ | / |                      |
| ![Next](../../dcommo | . |                      |
| n/gifs/rightnav.gif) | . |                      |
| \                    | / |                      |
|                      | d |                      |
|                      | c |                      |
|    <span class="icon | o |                      |
| ">Previous</span>](s | m |                      |
| ingle-sign-using-ker | m |                      |
| beros-java1.htm)   < | o |                      |
| span class="icon">Ne | n |                      |
| xt</span>](part-i-se | / |                      |
| cure-authentication- | g |                      |
| using-java-authentic | i |                      |
| ation-and-authorizat | f |                      |
| ion-service-jaas.htm | s |                      |
| )                    | / |                      |
|   ------------------ | o |                      |
| -------------------- | r |                      |
| -------------------- | a |                      |
| ----------------- -- | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| -------------------- | . |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| -- --                | ) |                      |
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
