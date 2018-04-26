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

  ----------------------------------------------------------------- ---------------------------------------------------------------------------------- --
            [![Previous](../../dcommon/gifs/leftnav.gif)\                               [![Next](../../dcommon/gifs/rightnav.gif)\                     
   <span class="icon">Previous</span>](kerberos-requirements1.htm)   <span class="icon">Next</span>](source-code-jaas-and-java-gss-api-tutorials.htm)  
  ----------------------------------------------------------------- ---------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE}<!-- End Header -->

Troubleshooting {#JSSEC-GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE .sect1}
===============

<div>
Below are listed some problems that may occur when attempting a login,
and suggestions for solving them.

-   <span class="bold">Configurable Kerberos Settings:</span> The
    Kerberos Key Distribution Center (KDC) name and realm settings are
    provided in the Kerberos configuration file or via the system
    properties `java.security.krb5.kdc`{.codeph} and
    `java.security.krb5.realm.`{.codeph} A boolean option
    `refreshKrb5Config`{.codeph} can be specified in the entry for
    `Krb5LoginModule`{.codeph} in the JAAS configuration file. If this
    option is set to `true`{.codeph}, then the configuration values will
    be refreshed before the login method of the
    `Krb5LoginModule`{.codeph} is called.

    <div class="infoboxnote" id="GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE__GUID-52651645-B786-41A8-87BE-347554DBA801">
    Note:

    When switching Kerberos configurations, it is REQUIRED that
    `refreshKrb5Config`{.codeph} should be set to `true.`{.codeph}
    Failure to set this value can lead to unexpected results.

    </div>
-   <span class="bold">java.lang.SecurityException at
    javax.security.auth.login.Configuration.getConfiguration</span>

    <span class="variable">Cause</span>: There was a problem processing
    the JAAS login configuration file, possibly due to a syntax error in
    the file.

    <span class="variable">Solution</span>: Check the configuration file
    carefully for errors. See [Appendix B: JAAS Login Configuration
    File](appendix-b-jaas-login-configuration-file.html#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)
    for information about the syntax required in the login configuration
    file.

-   <span class="bold">javax.security.auth.login.LoginException:
    KrbException: Pre-authentication information was invalid (24) -
    Preauthentication failed</span>

    <span class="variable">Cause 1:</span> The password entered is
    incorrect.

    <span class="variable">Solution 1</span>: Verify the password.

    <span class="variable">Cause 2:</span> If you are using the keytab
    to get the key (e.g., by setting the `useKeyTab`{.codeph} option to
    `true`{.codeph} in the Krb5LoginModule entry in the JAAS login
    configuration file), then the key might have changed since you
    updated the keytab.

    <span class="variable">Solution 2</span>: Consult your Kerberos
    documentation to generate a new keytab and use that keytab.

    <span class="variable">Cause 3:</span> Clock skew - If the time on
    the KDC and on the client differ significantly (typically 5
    minutes), this error can be returned.

    <span class="variable">Solution 3</span>: Synchronize the clocks (or
    have a system administrator do so).<span class="variable">Cause
    4:</span> The Kerberos realm name is not all uppercase.

    <span>Solution 4</span>: Make the Kerberos realm name all uppercase.
    <span class="bold">Note</span>: It is recommended to have all
    uppercase realm names. See [Naming Conventions for Realm Names and
    Hostnames](kerberos-requirements1.html#GUID-E73CCEA1-E94F-4E8D-9C42-403AF825658A).

-   <span class="bold">GSSException: No valid credentials provided
    (Mechanism level: Attempt to obtain new INITIATE credentials failed!
    (null)) . . . Caused by: javax.security.auth.login.LoginException:
    Clock skew too great</span>

    <span class="variable">Cause</span>: Kerberos requires the time on
    the KDC and on the client to be loosely synchronized. (The default
    is within 5 minutes.) If that\'s not the case, you will get this
    error.

    <span class="variable">Solution</span>: Synchronize the clocks (or
    have a system administrator do so).

-   <span class="bold">javax.security.auth.login.LoginException:
    KrbException: Null realm name (601) - default realm not
    specified</span>

    <span class="variable">Cause</span>: The default realm is not
    specified in the Kerberos configuration file `krb5.conf`{.codeph}
    (if used), provided as a part of the user name, or specified via the
    `java.security.krb5.realm`{.codeph} system property.

    <span class="variable">Solution</span>: Verify that your Kerberos
    configuration file (if used) contains an entry specifying the
    default realm, or directly specify it by setting the value of the
    `java.security.krb5.realm`{.codeph} system property and/or including
    it in your user name when authenticating using Kerberos.

-   <span class="bold">javax.security.auth.login.LoginException:
    java.net.SocketTimeoutException: Receive timed out</span>

    <span class="variable">Solution</span>: Verify that the Kerberos KDC
    is up and running.

-   <span class="bold">GSSException: No valid credentials provided
    (Mechanism level: Failed to find any Kerberos Ticket)</span>

    <span class="variable">Cause</span>: This may occur if no valid
    Kerberos credentials are obtained. In particular, this occurs if you
    want the underlying mechanism to obtain credentials but you forgot
    to indicate this by setting the
    `javax.security.auth.useSubjectCredsOnly`{.codeph} system property
    value to `false`{.codeph} (for example via
    `-Djavax.security.auth.useSubjectCredsOnly=false`{.codeph} in your
    execution command).

    <span class="variable">Solution</span>: Be sure to set the
    `javax.security.auth.useSubjectCredsOnly`{.codeph} system property
    value to `false`{.codeph} if you want the underlying mechanism to
    obtain credentials, rather than your application or a wrapper
    program (such as the Login utility used by some of the tutorials)
    performing authentication using JAAS.

-   <span class="bold">javax.security.auth.login.LoginException: Could
    not load configuration file \<krb5.conf\> (No such file or
    directory)</span>

    <span class="variable">Cause</span>: The tutorials\' sample
    execution commands specify the default Kerberos realm and KDC by
    setting values for the `java.security.krb5.realm`{.codeph} and
    `java.security.krb5.kdc`{.codeph} system properties. If you like,
    you can instead have a `krb5.conf`{.codeph} Kerberos configuration
    file used. Such a file includes information about what the default
    realm and KDC are. To use a `krb5.conf`{.codeph} file, you either
    set the system property `java.security.krb5.conf`{.codeph} (instead
    of the `realm`{.codeph} and `kdc`{.codeph} properties) to specify
    the location of the file or you don\'t set any of these properties
    and therefore an attempt is made to locate the `krb5.conf`{.codeph}
    file in a default location. You will get the error \"Could not load
    configuration file \<krb5.conf\> (No such file or directory)\" if
    the file could not be found.

    <span class="variable">Solution</span>: Verify that the Kerberos
    configuration file `krb5.conf`{.codeph} is available and readable.
    Check [Kerberos
    Requirements](kerberos-requirements1.html#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998)
    for information about how to specify the location of the
    `krb5.conf`{.codeph} file and where such a file is searched for by
    default if you don\'t explicitly indicate the location.

-   <span class="bold">javax.security.auth.login.LoginException:
    KrbException: KDC has no support for encryption type (14) - KDC has
    no support for encryption type</span>

    <span class="variable">Cause 1</span>: Your KDC does not support the
    encryption type requested.

    <span class="variable">Solution 1</span>: Oracle's implementation of
    Kerberos supports the following encryption types:
    `aes256-cts-hmac-sha1-96`{.codeph},
    `aes128-cts-hmac-sha1-96`{.codeph}, `des3-cbc-sha1`{.codeph},
    `arcfour-hmac-md5`{.codeph}, `des-cbc-crc`{.codeph}, and
    `des-cbc-md5`{.codeph}.

    Applications can select the desired encryption type by specifying
    following tags in the Kerberos Configuration file
    `krb5.conf`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    [libdefaults]
    default_tkt_enctypes = des-cbc-md5 des-cbc-crc des3-cbc-sha1
    default_tgs_enctypes = des-cbc-md5 des-cbc-crc des3-cbc-sha1
    permitted_enctypes = des-cbc-md5 des-cbc-crc des3-cbc-sha1  
    ```

    If not specified, then the default value is:

    ``` {.oac_no_warn dir="ltr"}
    aes256-cts-hmac-sha1-96 aes128-cts-hmac-sha1-96 des3-cbc-sha1 arcfour-hmac-md5
    ```

    If `allow_weak_crypto`{.codeph} in `krb5.conf` is set to true, then
    `des-cbc-crc`{.codeph} and `des-cbc-md5`{.codeph} are also
    supported.

    <span class="variable">Cause 2</span>: This exception is thrown when
    using native ticket cache on some Windows platforms. Microsoft has
    added a new feature in which they no longer export the session keys
    for Ticket-Granting Tickets (TGTs). As a result, the native TGT
    obtained on Windows has an \"empty\" session key and null EType.

    <span class="variable">Solution 2:</span> You need to update the
    Windows registry to disable this new feature. The registry key
    `allowtgtsessionkey`{.codeph} should be added -- and set correctly
    -- to allow session keys to be sent in the Kerberos Ticket-Granting
    Ticket.

    See [Registry Key to Allow Session Keys to Be Sent in Kerberos
    Ticket-Granting-Ticket](http://support.microsoft.com/kb/308339) from
    Microsoft Support for more information. Usually, the following is
    the required registry setting:

    ``` {.oac_no_warn dir="ltr"}
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\Kerberos\Parameters
    Value Name: allowtgtsessionkey
    Value Type: REG_DWORD
    Value: 0x01  ( default is 0 )
    ```

    By default, the value is 0; setting it to \"0x01\" allows a session
    key to be included in the TGT.

<!-- -->

-   <span class="bold">KDC reply did not match expectations</span>

    <span class="variable">Cause</span>: The KDC sent a response that
    cannot be understood by the client.

    <span class="variable">Solution</span>: Verify that you have set
    correctly all the `krb5.conf`{.codeph} file configuration parameters
    and consult your KDC vendor\'s guide.

    <div class="infoboxnote" id="GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE__GUID-3A1E7B18-F8D7-494F-B449-FF94E5B9C72C">
    Note:

    A debugging mode can be enabled by setting the system property
    `sun.security.krb5.debug`{.codeph} to \"true\". This setting allows
    you to follow the program\'s execution of the Kerberos V5 protocol.

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
| ------- ------------ | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ---------- --        | e | )\                   |
|             [![Previ | L |             <span cl |
| ous](../../dcommon/g | o | ass="icon">Contents< |
| ifs/leftnav.gif)\    | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|         [![Next](../ | ] | -------------------- |
| ../dcommon/gifs/righ | ( | -------------------- |
| tnav.gif)\           | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](k | . |                      |
| erberos-requirements | . |                      |
| 1.htm)   <span class | / |                      |
| ="icon">Next</span>] | d |                      |
| (source-code-jaas-an | c |                      |
| d-java-gss-api-tutor | o |                      |
| ials.htm)            | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| ------- ------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ---------- --        | s |                      |
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
