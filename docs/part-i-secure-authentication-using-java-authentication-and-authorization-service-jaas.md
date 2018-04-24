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

  ------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------- --
                                              [![Previous](../../dcommon/gifs/leftnav.gif)\                                                                       [![Next](../../dcommon/gifs/rightnav.gif)\                            
   <span class="icon">Previous</span>](advanced-security-programming-java-se-authentication-secure-communication-and-single-sign1.htm)   <span class="icon">Next</span>](part-ii-secure-communications-using-java-se-security-api.htm)  
  ------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-42416198-9AEE-428C-80EF-2A56488B5890}<!-- End Header -->

Part I : Secure Authentication using the Java Authentication and Authorization Service (JAAS) {#JSSEC-GUID-42416198-9AEE-428C-80EF-2A56488B5890 .sect1}
=============================================================================================

<div>
</div>
<div class="sect2">
[]{#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8}

Exercise 1: Using the JAAS API {#JSSEC-GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8 .sect2}
------------------------------

<div>
<div class="section">
Goal of This Exercise

The goal of this exercise is to learn how to use the Java Authentication
and Authorization (JAAS) API to perform authentication.

</div>
<!-- class="section" -->

<div class="section">
Background for This Exercise

JAAS provides a standard pluggable authentication framework (PAM) for
the Java platform.  An application uses the JAAS API to perform
<span class="italic">authentication</span> - the process of verifying
the identity of the user who is using the application and gathering his
identity information into a container called a
<span class="italic">subject</span>. The application can then use the
identity information in the subject along with the JAAS API to make
<span class="italic">authorization</span> decisions, to decide whether
the authenticated user is allowed to access protected resources or
perform restricted actions. This exercise demonstrates JAAS
Authentication. It does not demonstrate JAAS Authorization.

</div>
<!-- class="section" -->

<div class="section">
Resources for This Exercise

-   [Java Authentication and Authorization Service (JAAS) Reference
    Guide](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-2A935F5E-0803-411D-B6BC-F8C64D01A25C)
-   [JAAS
    Tutorials](jaas-tutorials.htm#GUID-272DB20A-B590-4B2E-BD60-7EF9EB54AB5A)
-   JAAS Javadoc API documentation
    -   [<span class="apiname">javax.security.auth</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/package-summary.html)
    -   [<span class="apiname">javax.security.auth.callback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/package-summary.html)
    -   [<span class="apiname">javax.security.auth.kerberos</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/kerberos/package-summary.html)
    -   [<span class="apiname">javax.security.auth.login</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/package-summary.html)
    -   [<span class="apiname">javax.security.auth.spi</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/package-summary.html)
    -   [<span class="apiname">javax.security.auth.x500</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/x500/package-summary.html)

</div>
<!-- class="section" -->

<div class="section">
Steps to Follow

-   Read the
    [`Jass.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JASS.JAVA-338B5916)
    sample code. The code performs the following tasks:

    1.  Define a callback handler or use a predefined one.
    2.  Create a <span class="apiname">LoginContext</span> with a name
        that identifies which JAAS configuration entry to use.
    3.  Perform the authentication.
    4.  Define the task that the authenticated user is to perform.
    5.  Perform the action as the authenticated user.
    6.  Log out.

    <span class="apiname">Subject.doAs</span> will run the code defined
    in `MyAction`{.codeph} as the authenticated user \[lines 14-15\].
    This serves two purposes. First, code in `MyAction`{.codeph} that
    requires identity information for authentication to a service could
    get it from the subject. This exercise demonstrates this use.
    Second, if `MyAction`{.codeph} accesses any protected
    resources/operations, the identity information in the current
    subject would be used to make the corresponding access control
    decision. This second aspect is not covered in this exercise.

-   Make sure that the `%JAVA_HOME%/bin`{.codeph} is in the PATH
    environment variable.

-   Compile the modified sample code. You will run this code in
    subsequent exercises after doing some set up. That ends this
    exercise.

</div>
<!-- class="section" -->

<div class="section">
Summary

This exercise introduced the main classes of the JAAS APIs:
<span class="apiname">LoginContext</span> and
<span class="apiname">Subject</span>. You learned how to use
<span class="apiname">LoginContext</span> to authenticate a user and
collect its identity information in a Subject. You then learned how to
use the Subject to perform an action as the authenticated user.

</div>
<!-- class="section" -->

<div class="section">
Next Steps

Proceed to [Exercise 2: Configuring JAAS for Kerberos
Authentication](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-2079DC72-5A2E-46FE-978F-42D113FFA41A)
to learn how to configure the sample application to use Kerberos for
authentication.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-2079DC72-5A2E-46FE-978F-42D113FFA41A}

Exercise 2: Configuring JAAS for Kerberos Authentication {#JSSEC-GUID-2079DC72-5A2E-46FE-978F-42D113FFA41A .sect2}
--------------------------------------------------------

<div>
<div class="section">
Goal of This Exercise

The goal of this exercise is to learn how to configure a JAAS
application to use Kerberos for authentication.

</div>
<!-- class="section" -->

<div class="section">
Kerberos Background for This Exercise

Kerberos is an Internet standard protocol for trusted-third party
authentication defined in [RFC
4120](http://www.ietf.org/rfc/rfc4120.txt). It is available on most
modern computing platforms today, including Solaris, Windows, and Linux.

The Kerberos architecture is centered around a trusted authentication
service called the key distribution center, or KDC. Users and services
in a Kerberos environment are referred to as principals; each principal
shares a secret (such as a password) with the KDC. A principal
 authenticates to Kerberos by proving to the KDC that it knows the
shared secret. If the authentication is successful, the KDC issues a
ticket-granting-ticket (TGT) to the principal. When the principal
subsequently wants to authenticate to a service on the network, such as
a directory service or a file service, (thereby, acting as a \"client\"
of the service), it gives the TGT to the KDC to obtain a service ticket
to communicate with the service. Not only does the service ticket
indicate the identities of the client and service principals, it also
contains a session key that can be used by the client and service to
subsequently establish secure communication. To authenticate to the
service, the client sends the service ticket to the service. When the
service receives the ticket, it decodes it using the secret it shares
with the KDC.

In this architecture, a principal only authenticates directly (once) to
the KDC. It authenticates indirectly to all other services via the use
of service tickets. Service tickets are how the KDC vouches for the
identity of a principal. The ability of a principal to access multiple
secure services by performing explicit authentication only once is
called single sign-on.

</div>
<!-- class="section" -->

<div class="section">
JAAS Background for This exercise

In JAAS, for a client principal, \"logging into Kerberos\" means
acquiring the TGT and placing it in the Subject, so that it can be used
for authentication with services that the client will access. For a
service principal, \"logging into Kerberos\" means obtaining the secret
keys that the service needs to decode incoming client authentication
requests.

</div>
<!-- class="section" -->

<div class="section">
Resources for This Exercise

-   [Java Authentication and Authorization Service (JAAS): LoginModule
    Developer\'s
    Guide](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A)
-   [The Kerberos Network Authentication Service
    (v5)](http://www.ietf.org/rfc/rfc4120.txt)
-   [Appendix B: JAAS Login Configuration
    File](appendix-b-jaas-login-configuration-file.htm#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)
-   Login module package Javadoc API
    documentation:[<span class="apiname">com.sun.security.auth.module</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/package-summary.html)
-   [Introduction to JAAS and Java GSS-API
    Tutorials](introduction-jaas-and-java-gss-api-tutorials1.htm)

</div>
<!-- class="section" -->

<div class="section">
Steps to Follow

1.  Examine the
    [<span class="apiname">jaas-krb5.conf</span>](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JASS-KRB5.CONF-338B5E8A)
    configuration file.

    This file contains two entries, one named
    <span class="italic">client</span> and one named
    <span class="italic">server</span>. The client entry indicates that
    the <span class="apiname">LoginContext</span> must use the
    <span class="bold"><span class="apiname">com.sun.security.auth.module.Krb5LoginModule</span></span>.
    The server entry indicates that the
    <span class="apiname">LoginContext</span> must use the same login
    module, and use keys from the `sample.keytab` file for the principal
    host/machineName.

2.  Determine the hostname of your machine by executing the hostname
    command.

3.  Edit this file and change the entry for server principal to use the
    name of your machine. For example, if your machine name is
    j1hol-001, this line in the configuration file should look like
    this:

    ``` {.oac_no_warn dir="ltr"}
    principal="host/j1hol-001"
    ```

4.  Perform client authentication by typing the following command:

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf Jaas client
    ```

    You will be prompted for a password. You should see the following
    output. Replace <span class="italic">password</span> with a password
    that is secure.

    ``` {.oac_no_warn dir="ltr"}
    Kerberos password for test: password
    Authenticated principal: [test@J1LABS.EXAMPLE.COM]
    Performing secure action...
    ```

5.  Perform server authentication by typing the following command:

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf Jaas server
    ```

    You should see the following output:

    ``` {.oac_no_warn dir="ltr"}
    Authenticated principal: [host/j1hol-001@J1LABS.EXAMPLE.COM] Performing secure action...
    ```

</div>
<!-- class="section" -->

<div class="section">
Summary

In this exercise, you learned how to configure a JAAS application to use
a Kerberos login module, both as a client principal who enters his/her
username/password interactively, and as a service principal who gets its
keys from a `keytab` file.

</div>
<!-- class="section" -->

<div class="section">
Next Steps

Proceed to [Part II : Secure Communications using the Java SE Security
API](part-ii-secure-communications-using-java-se-security-api.htm#GUID-98B02DB0-13DB-4175-9485-3449E1A241B5)
to learn how to establish secure communication channels using Java
security APIs.

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
| -------------------- | c |  Of Contents](../../ |
| --------------- ---- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| -------------------- | o | ass="icon">Contents< |
| -------------------- | g | /span>](toc.htm)     |
| ----------- --       | o |   -- --------------- |
|                      | ] | -------------------- |
|                      | ( | -------------------- |
|       [![Previous](. | . | ---                  |
| ./../dcommon/gifs/le | . |                      |
| ftnav.gif)\          | / |                      |
|                      | . |                      |
|                      | . |                      |
|                      | / |                      |
|   [![Next](../../dco | d |                      |
| mmon/gifs/rightnav.g | c |                      |
| if)\                 | o |                      |
|                      | m |                      |
|    <span class="icon | m |                      |
| ">Previous</span>](a | o |                      |
| dvanced-security-pro | n |                      |
| gramming-java-se-aut | / |                      |
| hentication-secure-c | g |                      |
| ommunication-and-sin | i |                      |
| gle-sign1.htm)   <sp | f |                      |
| an class="icon">Next | s |                      |
| </span>](part-ii-sec | / |                      |
| ure-communications-u | o |                      |
| sing-java-se-securit | r |                      |
| y-api.htm)           | a |                      |
|   ------------------ | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| -------------------- | . |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| --------------- ---- | f |                      |
| -------------------- | ) |                      |
| -------------------- | { |                      |
| -------------------- | . |                      |
| -------------------- | c |                      |
| ----------- --       | o |                      |
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
