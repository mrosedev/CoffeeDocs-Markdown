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

  ---------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------- --
                          [![Previous](../../dcommon/gifs/leftnav.gif)\                                                      [![Next](../../dcommon/gifs/rightnav.gif)\                              
   <span class="icon">Previous</span>](part-iii-deploying-single-sign-kerberos-environment.htm)   <span class="icon">Next</span>](part-v-secure-authentication-using-spnego-java-gss-mechanism.htm)  
  ---------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-49820DF7-0DED-4C63-8DB8-89718501ADB1}<!-- End Header -->

Part IV : Secure Communications Using Stronger Encryption Algorithms {#JSSEC-GUID-49820DF7-0DED-4C63-8DB8-89718501ADB1 .sect1}
====================================================================

<div>
</div>
<div class="sect2">
[]{#GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212}

Exercise 7: Configuring to Use Stronger Encryption Algorithms in a Kerberos Environment, to Secure the Communication {#JSSEC-GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212 .sect2}
--------------------------------------------------------------------------------------------------------------------

<div>
<div class="section">
Goal of This Exercise

The goal of this exercise is to learn how to use various Kerberos
encryption algorithms to secure the communication. Java GSS/Kerberos
provides a wide range of encryption algorithms, including AES256,
AES128, 3DES, RC4-HMAC, and DES.

<div class="infoboxnote" id="GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212__GUID-534CA619-6431-4AF6-9EAF-9097B1DB13C7">
Note:

DES-based encryption types are disabled by default.

</div>
The following is a list of all the encryption types supported by the
Java GSS/Kerberos provider in Java SE:

-   AES256-CTS

-   AES128-CTS

-   RC4-HMAC

-   DES3-CBC-SHA1

-   DES-CBC-MD5

-   DES-CBC-CRC

</div>
<!-- class="section" -->

<div class="section">
Steps to Follow

1.  Configure the Key Distribution Center (KDC) and update the Kerberos
    database.

    First, you need to update to use the KDC that supports the required
    Kerberos encryption types, such as the latest version of Solaris or
    the latest version of Kerberos from the MIT distribution. If you are
    using Active Directory on a Windows platform, the latest version
    also supports RC4-HMAC and AES encryption types.

    You need to update the Kerberos database to generate the new keys
    with stronger encryption algorithms. By default, Solaris 10 KDC will
    generate the keys for all the above encryption types listed. You can
    now create a keytab that will include all the keys for all the above
    encryption types.

    <div class="infoboxnote" id="GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212__GUID-91B456EC-8C26-4BBE-AE61-9229EAC72F4B">
    Note:

    If you want to use Windows 2000 KDC, you can configure to use the
    DES and RC4-HMAC encryption types that are available on Windows.

    </div>
2.  Edit the Kerberos configuration file
    ([`krb5.conf`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__KRB5.CONF-338B7967)).

    You will need to edit the Kerberos configuration file in order to
    select the desired encryption types used. The required parameters
    that you will need to insert under the `libdefaults`{.codeph}
    section of the Kerberos configuration file are listed below. For the
    purpose of this exercise, all the required entries have been added
    to a sample Kerberos configuration file included with the exercise,
    and the entries have been commented out. To enable the desired
    encryption type, you only need to uncomment the required entries.

    -   To enable AES256-CTS encryption type, add the following:

        ``` {.oac_no_warn dir="ltr"}
        [libdefaults]
        default_tkt_enctypes = aes256-cts
        default_tgs_enctypes = aes256-cts
        permitted_enctypes = aes256-cts
        ```

        <div class="infoboxnote" id="GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212__GUID-03ECE450-E293-48CF-BD38-E899E97BFACB">
        Note:

        Solaris 10 11/06 and earlier does not support AES256 by default.
        You will need to install the following packages: SUNWcry,
        SUNWcryr, SUNWcryptoint.

        </div>
    -   To enable AES128-CTS encryption type, add the following:

        ``` {.oac_no_warn dir="ltr"}
        [libdefaults]
        default_tkt_enctypes = aes128-cts
        default_tgs_enctypes = aes128-cts
        permitted_enctypes = aes128-cts
        ```

    -   To enable RC4-HMAC encryption type, add the following:

        ``` {.oac_no_warn dir="ltr"}
        [libdefaults]
        default_tkt_enctypes = rc4-hmac
        default_tgs_enctypes = rc4-hmac
        permitted_enctypes = rc4-hmac
        ```

    -   To enable DES3-CBC-SHA1 encryption type, add the following:

        ``` {.oac_no_warn dir="ltr"}
        [libdefaults]
        default_tkt_enctypes = des3-cbc-sha1
        default_tgs_enctypes = des3-cbc-sha1
        permitted_enctypes = des3-cbc-sha1
        ```

    <div class="infoboxnote" id="GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212__GUID-39D4BD8C-479F-40D7-81DB-7540B045316E">
    Note:

    -   If the above parameters are not added to the Kerberos
        configuration file, Solaris 10 11/06 and earlier will default to
        use AES128 enctype. If the exportable crypto packages have been
        installed, it will default to use AES256 enctype.

    -   Destroy any pre-existing Kerberos TGT in the ticket cache from
        the previous exercise as follows:

        ``` {.oac_no_warn dir="ltr"}
        % kdestroy
        ```

    </div>
3.  Launch a new window and start the server using the updated
    `krb5.conf` as follows:

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf \
    -Djava.security.krb5.conf=krb5.conf GSSServer
    ```

4.  Run the client application using the updated `krb5.conf`. The
    <span class="apiname">GSSClient</span> class takes two parameters:
    the service name and the name of the server that the service is
    running on. For example, if the service is host running on the
    machine j1hol-001, use the following (provide a secure password when
    prompted):

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf \
    -Djava.security.krb5.conf=krb5.conf \
    GSSClient host j1hol-001
    ```

</div>
<!-- class="section" -->

<div class="section">
Summary

In this exercise, you learned how to write a client-server application
that uses Java GSS API to authenticate and communicate securely using
stronger Kerberos encryption algorithms. You can enable Kerberos
debugging (`-Dsun.security.krb5.debug=true`{.codeph}), to obtain
information about the Kerberos encryption type used.

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
| ---------------- --- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| ---------------- --  | o | ass="icon">Contents< |
|                      | g | /span>](toc.htm)     |
|       [![Previous](. | o |   -- --------------- |
| ./../dcommon/gifs/le | ] | -------------------- |
| ftnav.gif)\          | ( | -------------------- |
|                      | . | ---                  |
|                      | . |                      |
|      [![Next](../../ | / |                      |
| dcommon/gifs/rightna | . |                      |
| v.gif)\              | . |                      |
|                      | / |                      |
|    <span class="icon | d |                      |
| ">Previous</span>](p | c |                      |
| art-iii-deploying-si | o |                      |
| ngle-sign-kerberos-e | m |                      |
| nvironment.htm)   <s | m |                      |
| pan class="icon">Nex | o |                      |
| t</span>](part-v-sec | n |                      |
| ure-authentication-u | / |                      |
| sing-spnego-java-gss | g |                      |
| -mechanism.htm)      | i |                      |
|   ------------------ | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| ---------------- --- | r |                      |
| -------------------- | a |                      |
| -------------------- | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| ---------------- --  | . |                      |
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
