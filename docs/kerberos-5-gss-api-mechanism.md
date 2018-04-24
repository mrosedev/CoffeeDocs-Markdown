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

  ----------------------------------------------------------------------------- ---------------------------------------------------------------------------------------- --
                  [![Previous](../../dcommon/gifs/leftnav.gif)\                                        [![Next](../../dcommon/gifs/rightnav.gif)\                        
   <span class="icon">Previous</span>](appendix-setting-kerberos-accounts.htm)   <span class="icon">Next</span>](java-secure-socket-extension-jsse-reference-guide.htm)  
  ----------------------------------------------------------------------------- ---------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-23D30A4B-CC38-45ED-83D5-C59ABB72762E}<!-- End Header -->

The Kerberos 5 GSS-API Mechanism {#JSSEC-GUID-23D30A4B-CC38-45ED-83D5-C59ABB72762E .sect1}
================================

<div>
This section describes and lists security features regarding Java
Generic Security Services (Java GSS) for Kerberos 5. It also describes
the Object Identifier (OID) for the Kerberos V5 mechanism, the
encryption types, and the `krb5.conf`{.codeph} settings supported by
Java GSS.

<div class="section">
The Generic Security Services Application Program Interface (GSS-API)
mechanism is defined by [RFC 1964](http://tools.ietf.org/html/rfc1964)
and supplemented with [RFC 4121](http://tools.ietf.org/html/rfc4121)
under the Internet Standards process.

</div>
<!-- class="section" -->

<div class="section">
The OID for the Kerberos V5 Mechanism

According to RFC 1964 section 1, the OID for Java Generic Security
Services (Java GSS) for Kerberos 5 is defined as 1.2.840.113554.1.2.2;
see also [GSSAPI
Mechanisms](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html#gssapi-mechanisms)
in <cite>Java Security Standard Algorithm Names</cite>.

</div>
<!-- class="section" -->

<div class="section">
Java GSS/Kerberos Supported Encryption Types

The following table lists the preferred order of Java GSS/Kerberos
supported encryption types.

<div class="tblformal" id="GUID-23D30A4B-CC38-45ED-83D5-C59ABB72762E__GUID-32156CE3-DB74-499F-BC7D-BC765B0D851D">
Table 7-1 Java GSS/Kerberos Supported Encryption Types

  Name            etype Number
  --------------- --------------
  aes256-cts      18
  aes128-cts      17
  rc4-hmac        23
  des3-cbc-sha1   16
  des-cbc-md5     3
  des-cbc-crc     1

</div>
<!-- class="inftblhruleinformal" -->

<div class="infoboxnote" id="GUID-23D30A4B-CC38-45ED-83D5-C59ABB72762E__GUID-DB77CB65-36AB-4098-AD4A-3E4D99F886CF">
Note:

The AES-256 encryption type is enabled by default. The DES-based
encryption types, including `des-cbc-crc`{.codeph} and
`dec-cbc-md5`{.codeph}, are disabled by default.

</div>
</div>
<!-- class="section" -->

<div class="section">
A user can restrict the usage of encryption for various purposes in
`krb5.conf`{.codeph}, in the `[libdefaults]`{.codeph} section.

</div>
<!-- class="section" -->

<div class="section">
Supported krb5.conf Settings

The following parameters are supported:

``` {.oac_no_warn dir="ltr"}
include FILENAME
includedir DIRNAME

[libdefaults]
default_realm
allow_weak_crypto
 
dns_lookup_kdc
dns_lookup_realm
dns_fallback
 
default_checksum
safe_checksum_type
ap_req_checksum_type
default_keytab_name
 
default_tkt_enctypes
permitted_enctypes
default_tgs_enctypes
 
no_addresses
noaddresses
 
renewable
proxiable
forwardable
 
kdc_default_options
clockskew
 
kdc_timeout
udp_preference_limit

max_retries
renew_lifetime
ticket_lifetime
 
[realms]
  REALM.NAME = {
      kdc
      kdc_timeout
      udp_preference_limit
      max_retries
  }
 
[capaths]
  A = {
    I = .
    B = I
  }
 
[domain_realm]
  domain=REALM
```

The following are the defaults for the `krb5.conf`{.codeph} file
parameters:

``` {.oac_no_warn dir="ltr"}
no_addresses = true
noaddresses = true
dns_lookup_kdc = true 
dns_lookup_realm = false
allow_weak_crypto = false
kdc_timeout = 30s
max_retries = 3
udp_preference_limit = 1465
clockskew = 300
renewable = false
proxiable = false
forwardable = false
```

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
| -------------------  | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------- --          | L |             <span cl |
|                   [! | o | ass="icon">Contents< |
| [Previous](../../dco | g | /span>](toc.htm)     |
| mmon/gifs/leftnav.gi | o |   -- --------------- |
| f)\                  | ] | -------------------- |
|                      | ( | -------------------- |
|    [![Next](../../dc | . | ---                  |
| ommon/gifs/rightnav. | . |                      |
| gif)\                | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](a | / |                      |
| ppendix-setting-kerb | d |                      |
| eros-accounts.htm)   | c |                      |
|  <span class="icon"> | o |                      |
| Next</span>](java-se | m |                      |
| cure-socket-extensio | m |                      |
| n-jsse-reference-gui | o |                      |
| de.htm)              | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------  | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| -------- --          | a |                      |
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
