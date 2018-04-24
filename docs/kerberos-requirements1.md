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

  --------------------------------------------------------------------------------------- ------------------------------------------------------ --
                       [![Previous](../../dcommon/gifs/leftnav.gif)\                            [![Next](../../dcommon/gifs/rightnav.gif)\       
   <span class="icon">Previous</span>](more-things-you-can-do-java-gss-api-and-jaas.htm)   <span class="icon">Next</span>](troubleshooting.htm)  
  --------------------------------------------------------------------------------------- ------------------------------------------------------ --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998}<!-- End Header -->

Kerberos Requirements {#JSSEC-GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998 .sect1}
=====================

<div>
Kerberos Version 5 is used for both the authentication and secure
communication aspects of the client and server applications developed in
this tutorial. The reader is assumed to already be familiar with
Kerberos. See the [Kerberos reference
documentation](http://web.MIT.edu/kerberos/www/index.html).

The JAAS framework, and the Kerberos mechanism required by the Java
GSS-API methods, are built into JDKs from all vendors. The Kerberos
LoginModule required for the JAAS authentication in this tutorial may
not be available in all vendors\' JDKs. We will be using the LoginModule
for Kerberos provided by Oracle\'s JDK.

In order to run the sample programs, you will need access to a Kerberos
installation. As described in the following sections, you may also need
a `krb5.conf`{.codeph} Kerberos configuration file and an indication as
to where that file is located.

As with all Kerberos installations, a Kerberos Key Distribution Center
(KDC) is required. It needs to contain the user name and password you
will use to be authenticated to Kerberos.

<div class="infoboxnote" id="GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998__GUID-4FC2940F-C2B5-4760-98EC-C22375CB0C22">
Note:

A KDC implementation is part of a Kerberos installation and not a part
of the JDK.

</div>
As with most Kerberos installations, a Kerberos configuration file
`krb5.conf`{.codeph} is consulted to determine such things as the
default realm and KDC. If you are using a Kerberos implementation that
does not include a `krb5.conf`{.codeph} file (such as one from Windows),
you will either need to create one or use system properties as described
in [Setting Properties to Indicate the Default Realm and
KDC](kerberos-requirements1.htm#GUID-8B30CD5C-64B6-48DE-9CD5-0E44D3A434A7).

</div>
<div class="sect2">
[]{#GUID-8B30CD5C-64B6-48DE-9CD5-0E44D3A434A7}

Setting Properties to Indicate the Default Realm and KDC {#JSSEC-GUID-8B30CD5C-64B6-48DE-9CD5-0E44D3A434A7 .sect2}
--------------------------------------------------------

<div>
Typically, the default realm and the KDC for that realm are indicated in
the Kerberos `krb5.conf`{.codeph} configuration file. However, if you
like, you can instead specify these values by setting the following
system properties to indicate the realm and KDC, respectively:

``` {.oac_no_warn dir="ltr"}
java.security.krb5.realm
java.security.krb5.kdc
```

If you set one of these properties you must set them both.

Also note that if you set these properties, then no cross-realm
authentication is possible unless a `krb5.conf`{.codeph} file is also
provided from which the additional information required for cross-realm
authentication may be obtained.

If you set values for these properties, then they override the default
realm and KDC values specified in `krb5.conf`{.codeph} (if such a file
is found). The `krb5.conf`{.codeph} file is still consulted if values
for items other than the default realm and KDC are needed. If no
`krb5.conf`{.codeph} file is found, then the default values used for
these items are implementation-specific.

</div>
</div>
<div class="sect2">
[]{#GUID-0C6413BA-417B-493D-BC89-F9FB90D5E641}

Locating the krb5.conf Configuration File {#JSSEC-GUID-0C6413BA-417B-493D-BC89-F9FB90D5E641 .sect2}
-----------------------------------------

<div>
The essential Kerberos configuration information is the default realm
and the default KDC. As shown in [Setting Properties to Indicate the
Default Realm and
KDC](kerberos-requirements1.htm#GUID-8B30CD5C-64B6-48DE-9CD5-0E44D3A434A7),
if you set properties to indicate these values, they are not obtained
from a `krb5.conf`{.codeph} configuration file.

If these properties do not have values set, or if other Kerberos
configuration information is needed, an attempt is made to find the
required information in a `krb5.conf`{.codeph} file. The algorithm to
locate the `krb5.conf`{.codeph} file is the following:

-   If the system property `java.security.krb5.conf`{.codeph} is set,
    its value is assumed to specify the path and file name.

-   If that system property value is not set, then the configuration
    file is looked for in the directory

    -   `<java-home>\conf\security`{.codeph} (Windows)
    -   `<java-home>/conf/security`{.codeph} (Solaris, Linux, and macOS)

    Here `<java-home>`{.codeph} refers to the directory where the JDK is
    installed.

-   If the file is still not found, then an attempt is made to locate it
    as follows:

    -   `/etc/krb5/krb5.conf`{.codeph} (Solaris)
    -   `C:\Windows\krb5.ini`{.codeph} (Windows)
    -   `/etc/krb5.conf`{.codeph} (Linux)
    -   `~/Library/Preferences/edu.mit.Kerberos`,
        `/Library/Preferences/edu.mit.Kerberos`, or `/etc/krb5.conf`
        (macOS)

-   If the file is still not found, and the configuration information
    being searched for is <span class="variable">not</span> the default
    realm and KDC, then implementation-specific defaults are used. If,
    on the other hand, the configuration information being searched for
    is the default realm and KDC because they weren\'t specified in
    system properties, and the `krb5.conf`{.codeph} file is not found
    either, then an exception is thrown.

-   On Windows, if a `krb5.conf` file cannot be found or it does not
    contain settings for the default realm and its KDC, then the
    environment variables `USERDNSDOMAIN`{.codeph} and
    `LOGONSERVER`{.codeph} are used as the default realm and its KDC.

</div>
</div>
<div class="sect2">
[]{#GUID-E73CCEA1-E94F-4E8D-9C42-403AF825658A}

Naming Conventions for Realm Names and Hostnames {#JSSEC-GUID-E73CCEA1-E94F-4E8D-9C42-403AF825658A .sect2}
------------------------------------------------

<div>
By convention, all Kerberos realm names are uppercase and all DNS
hostname and domain names are lowercase. On Windows, domains are also
Kerberos realms; however, the realm name is always the uppercase version
of the domain name.

Hostnames are case insensitive and by convention they are all lowercase.
They must resolve to the same hostname on the client and server by their
respective naming services.

However, in the Kerberos database hostnames are case sensitive. In all
host-based Kerberos service principals in the KDC, hostnames are
case-sensitive. The hostnames used in the Kerberos service principal
names must exactly match the hostnames returned by the naming service.
For example, if the naming service returns a fully qualified lowercased
DNS hostname, such as `raven.example.com`{.codeph}, then the
administrator must use the same fully qualified lowercased DNS hostname
when creating host-based principal names in the KDC:
`host/raven.example.com`{.codeph}.

</div>
</div>
<div class="sect2">
[]{#GUID-9D76C533-8EF4-4417-884A-37C60FA233FC}

Cross-Realm Authentication {#JSSEC-GUID-9D76C533-8EF4-4417-884A-37C60FA233FC .sect2}
--------------------------

<div>
In cross-realm authentication, a principal in one realm can authenticate
to principals in another realm.

In Kerberos, cross-realm authentication is implemented by sharing an
encryption key between two realms. The KDCs in two different realms
share a special cross-realm secret; this secret is used to prove
identity when crossing the boundary between realms.

The key that is shared is the Ticket Granting Service principal\'s key.
Here\'s a typical Ticket Granting Service principal for a single realm:

``` {.oac_no_warn dir="ltr"}
ktbtgt/EXAMPLE.COM@EXAMPLE.COM
```

In cross realm authentication, two principals are created on each
participating realm. For two realms, `ENG.EAST.EXAMPLE.COM`{.codeph} and
`SALES.WEST.EXAMPLE.COM`{.codeph}, these principals would be:

``` {.oac_no_warn dir="ltr"}
krbtgt/ENG.EAST.EXAMPLE.COM@SALES.WEST.EXAMPLE.COM
krbtgt/SALES.WEST.EXAMPLE.COM@ENG.EAST.EXAMPLE.COM
```

These principals, known as remote Ticket Granting Server principals,
must be created on both realms.

For a Windows KDC, the `krbtgt`{.codeph} account is created
automatically when a Windows domain is created. This account cannot be
deleted and renamed.

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
| --------- ---------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ---- --              | e | )\                   |
|                      | L |             <span cl |
|    [![Previous](../. | o | ass="icon">Contents< |
| ./dcommon/gifs/leftn | g | /span>](toc.htm)     |
| av.gif)\             | o |   -- --------------- |
|                 [![N | ] | -------------------- |
| ext](../../dcommon/g | ( | -------------------- |
| ifs/rightnav.gif)\   | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](m | . |                      |
| ore-things-you-can-d | . |                      |
| o-java-gss-api-and-j | / |                      |
| aas.htm)   <span cla | d |                      |
| ss="icon">Next</span | c |                      |
| >](troubleshooting.h | o |                      |
| tm)                  | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| -------------------- | / |                      |
| --------- ---------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ---- --              | s |                      |
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
