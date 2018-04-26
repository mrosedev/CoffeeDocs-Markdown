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

  ------------------------------------------------------------- -------------------------------------------------------------- --
          [![Previous](../../dcommon/gifs/leftnav.gif)\                   [![Next](../../dcommon/gifs/rightnav.gif)\           
   <span class="icon">Previous</span>](howtoimplaprovider.htm)   <span class="icon">Next</span>](pkcs11-reference-guide1.htm)  
  ------------------------------------------------------------- -------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313}<!-- End Header -->

<script type="text/javascript">
window.name='oracle-providers'
</script>
<script type="text/javascript">
    function footdisplay(footnum,footnote) {
    var msg = window.open('about:blank', 'NewWindow' + footnum,
        'directories=no,height=100,location=no,menubar=no,resizable=yes,' +
        'scrollbars=yes,status=no,toolbar=no,width=598');
    msg.document.open('text/html');
    msg.document.write('<!DOCTYPE html ');
    msg.document.write('PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" ');
    msg.document.write('"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">'); 
    msg.document.write('<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en-us" lang="en-us" dir="ltr"><head><title>');
   
    msg.document.write('Footnote&amp;nbsp; ' + footnum);
    msg.document.write('<\/title><meta http-equiv="Content-Type" ');
    msg.document.write('content="text/html; charset=utf-8" />');
    msg.document.write('<meta http-equiv="Content-Script-Type" ');
    msg.document.write('content="text/javascript" />');
    msg.document.write('<style type="text/css"> <![CDATA[ ');
    msg.document.write('h1 {text-align: center; font-size: 14pt;}');
    msg.document.write('fieldset {border: none;}');
    msg.document.write('form {text-align: center;}');
    msg.document.write(' ]]\u003e <\/style>');
    msg.document.write('<\/head><body><div id="footnote"><h1>Footnote&nbsp; ' + footnum + '<\/h1><p>');
    msg.document.write(footnote);
    msg.document.write('<\/p><form action="" method="post"><fieldset>');
    msg.document.write('<input type="button" value="OK" ');
    msg.document.write('onclick="window.close();" />');
    msg.document.write('<\/fieldset><\/form><\/div><\/body><\/html>');
    msg.document.close();
    setTimeout(function() {
        var height = msg.document.getElementById('footnote').offsetHeight;
        msg.resizeTo(598, height + 100);
    }
    , 100);
    msg.focus();
}
            </script>
<noscript>
The script content on this page is for navigation purposes only and does
not alter the content in any way.

</noscript>
<span class="enumeration_chapter">4 </span>JDK Providers Documentation {#JSSEC-GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313 .sect1}
======================================================================

<div>
This document contains the technical details of the providers that are
included in the JDK. It is assumed that readers have a strong
understanding of the Java Cryptography Architecture and Provider
Architecture.

<div class="infoboxnote" id="GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313__GUID-D14F4574-125A-48DF-80D9-1C0F7F853122">
Note:

The [Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
contains more information about the standard names used in this
document.

</div>
<div class="section">
Topics

[Introduction to JDK
Providers](oracle-providers.html#GUID-F41EE1C9-DD6A-4BAB-8979-EB7654094029 "The Java platform defines a set of APIs spanning major security areas, including cryptography, public key infrastructure, authentication, secure communication, and access control. These APIs enable developers to easily integrate security mechanisms into their application code.")

[Import Limits on Cryptographic
Algorithms](oracle-providers.html#GUID-9224B90B-7B2F-41F9-BB96-C0A1B6A0FEAA)

[Cipher
Transformations](oracle-providers.html#GUID-BC92B7F1-D15C-432A-B725-9BBA9FEF61DB "The javax.crypto.Cipher.getInstance(String transformation) factory method generates Cipher objects using transformations of the form algorithm/mode/padding. If the mode/padding are omitted, the SunJCE and SunPKCS11 providers use ECB as the default mode and PKCS5Padding as the default padding for many symmetric ciphers.")

[SecureRandom
Implementations](oracle-providers.html#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453 "The following table lists the default preference order of the available SecureRandom implementations.")

[The SunPKCS11
Provider](oracle-providers.html#GUID-C4706FFE-D08F-4E29-B0BE-CCE8C93DD940)

[The SUN
Provider](oracle-providers.html#GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D "JDK 1.1 introduced the Provider architecture. The first JDK provider was named SUN, and contained two types of cryptographic services (MessageDigestand Signature). In later releases, other mechanisms were added (SecureRandom, KeyPairGenerator, KeyFactory, and so on).")

[The SunRsaSign
Provider](oracle-providers.html#GUID-17E3589E-E4BA-4881-9B12-9880DD2D128D "The SunRsaSign provider was introduced in JDK 1.3 as an enhanced replacement for the RSA signature in the SunJSSE provider.")

[The SunJSSE
Provider](oracle-providers.html#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2)

[The SunJCE
Provider](oracle-providers.html#GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7 "As described briefly in The SUN Provider, US export regulations at the time restricted the type of cryptographic functionality that could be available in the JDK. A separate API and reference implementation was developed that allowed applications to encrypt/decrypt date. The Java Cryptographic Extension (JCE) was released as a separate ”Optional Package” (also briefly known as a “Standard Extension”), and was available for JDK 1.2x and 1.3x. During the development of JDK 1.4, regulations were relaxed enough that JCE (and SunJSSE) could be bundled as part of the JDK.")

[The SunJGSS
Provider](oracle-providers.html#GUID-9CAAC18D-CFF0-4602-A1B7-53C9FAA98C9F "The following algorithms are available in the SunJGSS provider:")

[The SunSASL
Provider](oracle-providers.html#GUID-EB759F08-B8D8-424A-9357-10F9002AE177 "The following algorithms are available in the SunSASL provider:")

[The XMLDSig
Provider](oracle-providers.html#GUID-D09DE3FE-237F-4B7B-A323-0A370137E0F3 "The following algorithms are available in the XMLDSig provider:")

[The SunPCSC
Provider](oracle-providers.html#GUID-DEAD6543-FB59-46F3-B4E7-EE1AFE246EA0)

[The SunMSCAPI
Provider](oracle-providers.html#GUID-4F1737D6-1569-4340-B140-678C70E63CD5 "The SunMSCAPI provider enables applications to use the standard JCA/JCE APIs to access the native cryptographic libraries, certificates stores and key containers on the Microsoft Windows platform. The SunMSCAPI provider itself does not contain cryptographic functionality, it is simply a conduit between the Java environment and the native cryptographic services on Windows.")

[The SunEC
Provider](oracle-providers.html#GUID-091BF58C-82AB-4C9C-850F-1660824D5254 "The SunEC provider implements Elliptical Curve Cryptography (ECC). Compared to traditional cryptosystems such as RSA, ECC offers equivalent security with smaller key sizes, which results in faster computations, lower power consumption, and memory and bandwidth savings.")

[The OracleUcrypto
Provider](oracle-providers.html#GUID-B1F2B3F3-F2A4-4FF5-8887-3B3335343B2A "The Solaris-only security provider OracleUcrypto leverages the Solaris Ucrypto library to offload and delegate cryptographic operations supported by the Oracle SPARC T4 based on-core cryptographic instructions. The OracleUcrypto provider itself does not contain cryptographic functionality; it is simply a conduit between the Java environment and the Solaris Ucrypto library.")

[The Apple
Provider](oracle-providers.html#GUID-3185649A-C316-45F2-A70E-2B3FF6BDC34F "The Apple provider implements a java.security.KeyStore that provides access to the macOS Keychain.")

[The JdkLDAP
Provider](oracle-providers.html#GUID-67D4652C-2551-4BBE-9941-50A9348AEA84 "The JdkLDAP provider was introduced in JDK 9 as a replacement for the LDAP CertStore implementation in the SUN provider.")

[The JdkSASL
Provider](oracle-providers.html#GUID-D08B5350-6653-4FC6-B350-2B009A9E7FD6 "The following algorithms are available in the JdkSASL provider:")

</div>
<!-- class="section" -->

</div>
<div class="sect2">
[]{#GUID-F41EE1C9-DD6A-4BAB-8979-EB7654094029}

Introduction to JDK Providers {#JSSEC-GUID-F41EE1C9-DD6A-4BAB-8979-EB7654094029 .sect2}
-----------------------------

<div>
The Java platform defines a set of APIs spanning major security areas,
including cryptography, public key infrastructure, authentication,
secure communication, and access control. These APIs enable developers
to easily integrate security mechanisms into their application code.

The [Java Cryptography Architecture
(JCA)](java-cryptography-architecture-jca-reference-guide.html#GUID-815542FE-CF3D-407A-9673-CAE9840F6231 "The Java platform strongly emphasizes security, including language safety, cryptography, public key infrastructure, authentication, secure communication, and access control.")
and its [Provider
Architecture](java-cryptography-architecture-jca-reference-guide.html#GUID-EAB9FF73-4C69-4FD5-8A0C-5CF48211A859 "Providers contain a package (or a set of packages) that supply concrete implementations for the advertised cryptographic algorithms.")
are core concepts of the Java Development Kit (JDK). It is assumed that
readers have a solid understanding of this architecture.

<span class="bold">Reminder:</span> Cryptographic implementations in the
JDK are distributed through several different providers (\"SUN\",
\"SunJSSE\", \"SunJCE\", \"SunRsaSign\") for both historical reasons and
by the types of services provided. General purpose applications
<span class="bold">SHOULD NOT</span> request cryptographic services from
specific providers. That is:

``` {.oac_no_warn dir="ltr"}
getInstance("...", "SunJCE");  // not recommended
```

versus

``` {.oac_no_warn dir="ltr"}
getInstance("...");            // recommended
```

Otherwise, applications are tied to specific providers that may not be
available on other Java implementations. They also might not be able to
take advantage of available optimized providers (for example, hardware
accelerators via PKCS11 or native OS implementations such as
Microsoft\'s MSCAPI) that have a higher preference order than the
specific requested provider.

The following table lists the modules and the supported Java
Cryptographic Service Providers:

<div class="tblformal" id="GUID-F41EE1C9-DD6A-4BAB-8979-EB7654094029__GUID-5A03EFB6-97B8-486D-8ECA-8850B80DA513">
Table 4-1 Modules and the Java Cryptographic Service Providers

+-----------------------------------+-----------------------------------+
| Module                            | Provider(s)                       |
+:==================================+:==================================+
| java.base                         | SUN, SunRsaSign, SunJSSE,         |
|                                   | SunJCE[^Foot 1^](#GUID-F41EE1C9-D |
|                                   | D6A-4BAB-8979-EB7654094029__INDIC |
|                                   | ATESJCECRYPTOPROVIDERSPREVIOUS-29 |
|                                   | F12786){#GUID-F41EE1C9-DD6A-4BAB- |
|                                   | 8979-EB7654094029__INDICATESJCECR |
|                                   | YPTOPROVIDERSPREVIOUS-29F12786},  |
|                                   | Apple                             |
+-----------------------------------+-----------------------------------+
| java.naming                       | JdkLDAP                           |
+-----------------------------------+-----------------------------------+
| java.security.jgss                | SunJGSS                           |
+-----------------------------------+-----------------------------------+
| java.security.sasl                | SunSASL                           |
+-----------------------------------+-----------------------------------+
| java.smartcardio                  | SunPCSC                           |
+-----------------------------------+-----------------------------------+
| java.xml.crypto                   | XMLDSig                           |
+-----------------------------------+-----------------------------------+
| jdk.crypto.cryptoki               | SunPKCS11[^Footref 1^](#fnsrc_d52 |
|                                   | 441e297){#fnsrc_d52441e297}       |
+-----------------------------------+-----------------------------------+
| jdk.crypto.ec                     | SunEC[^Footref 1^](#fnsrc_d52441e |
|                                   | 306){#fnsrc_d52441e306}           |
+-----------------------------------+-----------------------------------+
| jdk.crypto.mscapi                 | SunMSCAPI[^Footref 1^](#fnsrc_d52 |
|                                   | 441e315){#fnsrc_d52441e315}       |
+-----------------------------------+-----------------------------------+
| jdk.crypto.ucrypto                | OracleUcrypto[^Footref 1^](#fnsrc |
|                                   | _d52441e324){#fnsrc_d52441e324}   |
+-----------------------------------+-----------------------------------+
| jdk.security.jgss                 | JdkSASL                           |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

^Footnote 1^ Indicates JCE crypto providers previously distributed as
signed JAR files (JCE providers contain
`Cipher/KeyAgreement/KeyGenerator/Mac/SecretKeyFactory`{.codeph}
implementations).

</div>
</div>
<div class="sect2">
[]{#GUID-9224B90B-7B2F-41F9-BB96-C0A1B6A0FEAA}

Import Limits on Cryptographic Algorithms {#JSSEC-GUID-9224B90B-7B2F-41F9-BB96-C0A1B6A0FEAA .sect2}
-----------------------------------------

<div>
<div class="section">
By default, an application can use cryptographic algorithms of any
strength. However, due to import regulations in some locations, you may
have to limit the strength of those algorithms. The JDK provides two
different sets of jurisdiction policy files in the directory
`<java-home>/conf/security/policy` that determine the strength of
cryptographic algorithms. Information about jurisdiction policy files
and how to activate them is available in [Cryptographic Strength
Configuration](java-cryptography-architecture-jca-reference-guide.html#GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1).

Consult your export/import control counsel or attorney to determine the
exact requirements for your location.

For the \"limited\" configuration, the following table lists the maximum
key sizes allowed by the \"limited\" set of jurisdiction policy files:

</div>
<!-- class="section" -->

<div class="tblformal" id="GUID-9224B90B-7B2F-41F9-BB96-C0A1B6A0FEAA__GUID-006A1477-5038-4A83-99DC-23B0D69AFF49">
Table 4-2 Maximum Keysize of Cryptographic Algorithms

  Algorithm    Maximum Keysize
  ------------ -----------------
  DES          64
  DESede       \*
  RC2          128
  RC4          128
  RC5          128
  RSA          \*
  all others   128

</div>
<!-- class="inftblhruleinformal" -->

</div>
</div>
<div class="sect2">
[]{#GUID-BC92B7F1-D15C-432A-B725-9BBA9FEF61DB}

Cipher Transformations {#JSSEC-GUID-BC92B7F1-D15C-432A-B725-9BBA9FEF61DB .sect2}
----------------------

<div>
The `javax.crypto.Cipher.getInstance(String transformation)`{.codeph}
factory method generates `Cipher`{.codeph} objects using transformations
of the form <span class="bold">algorithm/mode/padding</span>. If the
mode/padding are omitted, the SunJCE and SunPKCS11 providers use ECB as
the default mode and PKCS5Padding as the default padding for many
symmetric ciphers.

It is recommended to use transformations that fully specify the
algorithm, mode, and padding instead of relying on the defaults. The
defaults are provider specific and can vary among providers.

<div class="infoboxnote" id="GUID-BC92B7F1-D15C-432A-B725-9BBA9FEF61DB__GUID-D633DB9E-D0F2-469A-91D7-ABD905E7C157">
Note:

ECB works well for single blocks of data and can be parallelized, but
absolutely should not be used for multiple blocks of data.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453}

SecureRandom Implementations {#JSSEC-GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453 .sect2}
----------------------------

<div>
The following table lists the default preference order of the available
`SecureRandom`{.codeph} implementations.

<div class="section">
<div class="tblformal" id="GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__GUID-7EA67F86-3611-44DA-B52F-2031BEFA26E7">
Table 4-3 Default SecureRandom Implementations

<table cellpadding="4" cellspacing="0" class="Formal" title="Default SecureRandom Implementations" summary="Lists the default preference order of the available SecureRandom implementations." width="100%" frame="hsides" border="1" rules="rows">
<thead>
<tr align="left" valign="top">
<th align="left" valign="bottom" width="33%" id="d52441e456">
OS

</th>
<th align="left" valign="bottom" width="34%" id="d52441e458">
Algorithm Name

</th>
<th align="left" valign="bottom" width="33%" id="d52441e460">
Provider Name

</th>
</tr>
</thead>
<tbody>
<tr align="left" valign="top">
<td rowspan="6" colspan="1" align="left" valign="top" id="d52441e464" headers="d52441e456 ">
Solaris

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e458 ">
1.
PKCS11[^Foot 2^](#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__THESUNPKCS11PROVIDERISAVAILABLEONAL-29E707BF){#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__THESUNPKCS11PROVIDERISAVAILABLEONAL-29E707BF}[^Foot 3^](#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__THEPKCS11SECURERANDOMIMPLEMENTATION-29E70DC1){#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__THEPKCS11SECURERANDOMIMPLEMENTATION-29E70DC1}

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e460 ">
SunPKCS11

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e458 ">
2.
NativePRNG[^Foot 4^](#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__ONSOLARISLINUXANDOSXIFTHEENTROPYGAT-29E70988){#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__ONSOLARISLINUXANDOSXIFTHEENTROPYGAT-29E70988}

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td align="left" valign="top" width="34%" headers="d52441e464 d52441e458 ">
3\. DRBG

</td>
<td align="left" valign="top" width="33%" headers="d52441e464 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e458 ">
4\. SHA1PRNG[^Footref 4^](#fnsrc_d52441e513){#fnsrc_d52441e513}

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e458 ">
5\. NativePRNGBlocking

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e458 ">
6\. NativePRNGNonBlocking

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e464 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="5" colspan="1" align="left" valign="top" id="d52441e529" headers="d52441e456 ">
Linux

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e529 d52441e458 ">
1\. NativePRNG[^Footref 4^](#fnsrc_d52441e533){#fnsrc_d52441e533}

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e529 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td align="left" valign="top" width="34%" headers="d52441e529 d52441e458 ">
2\. DRGB

</td>
<td align="left" valign="top" width="33%" headers="d52441e529 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e529 d52441e458 ">
3\. SHA1PRNG[^Footref 4^](#fnsrc_d52441e546){#fnsrc_d52441e546}

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e529 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e529 d52441e458 ">
4\. NativePRNGBlocking

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e529 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e529 d52441e458 ">
5\. NativePRNGNonBlocking

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e529 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="5" colspan="1" align="left" valign="top" id="d52441e563" headers="d52441e456 ">
macOS

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e563 d52441e458 ">
1\. NativePRNG[^Footref 4^](#fnsrc_d52441e567){#fnsrc_d52441e567}

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e563 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td align="left" valign="top" width="34%" headers="d52441e563 d52441e458 ">
2\. DRGB

</td>
<td align="left" valign="top" width="33%" headers="d52441e563 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e563 d52441e458 ">
3\. SHA1PRNG[^Footref 4^](#fnsrc_d52441e580){#fnsrc_d52441e580}

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e563 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e563 d52441e458 ">
4\. NativePRNGBlocking

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e563 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e563 d52441e458 ">
5\. NativePRNGNonBlocking

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e563 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="3" colspan="1" align="left" valign="top" id="d52441e596" headers="d52441e456 ">
Windows

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e596 d52441e458 ">
1\. DRGB

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e596 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td align="left" valign="top" width="34%" headers="d52441e596 d52441e458 ">
2\. SHA1PRNG

</td>
<td align="left" valign="top" width="33%" headers="d52441e596 d52441e460 ">
SUN

</td>
</tr>
<tr align="left" valign="top">
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e596 d52441e458 ">
3.
Windows-PRNG[^Foot 5^](#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__THEREISCURRENTLYNONATIVEPRNGONWINDO-29E70B4F){#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453__THEREISCURRENTLYNONATIVEPRNGONWINDO-29E70B4F}

</td>
<td rowspan="1" colspan="1" align="left" valign="top" headers="d52441e596 d52441e460 ">
SunMSCAPI

</td>
</tr>
</tbody>
</table>
</div>
<!-- class="inftblhruleinformal" -->

^Footnote 2^ The SunPKCS11 provider is available on all platforms, but
is only enabled by default on Solaris as it is the only OS with a native
PKCS11 implementation automatically installed and configured. On other
platforms, applications or deployers must specifically install and
configure a native PKCS11 library, and then configure and enable the
SunPKCS11 provider to use it.

^Footnote 3^ The PKCS11 `SecureRandom`{.codeph} implementation for
Solaris has been disabled due to the performance overhead of small-sized
requests (see [JDK-8098581: SecureRandom.nextBytes() hurts performance
with small size
requests](https://bugs.openjdk.java.net/browse/JDK-8098581)). Edit
`sunpkcs11-solaris.cfg` to reenable.

^Footnote 4^ On Solaris, Linux, and OS X, if the
<span class="variable">entropy gathering device</span> in
`java.security`{.codeph} is set to `file:/dev/urandom`{.codeph} or
`file:/dev/random`{.codeph}, then NativePRNG is preferred to SHA1PRNG.
Otherwise, SHA1PRNG is preferred.

^Footnote 5^ There is currently no NativePRNG on Windows. Access to the
equivalent functionality is via the SunMSCAPI provider.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-C4706FFE-D08F-4E29-B0BE-CCE8C93DD940}

The SunPKCS11 Provider {#JSSEC-GUID-C4706FFE-D08F-4E29-B0BE-CCE8C93DD940 .sect2}
----------------------

<div>
<div class="section">
The Cryptographic Token Interface Standard
([PKCS\#11](http://india.emc.com/emc-plus/rsa-labs/standards-initiatives/pkcs-11-cryptographic-token-interface-standard.htm))
provides native programming interfaces to cryptographic mechanisms, such
as hardware cryptographic accelerators and Smart Cards. When properly
configured, the `SunPKCS11`{.codeph} provider enables applications to
use the standard JCA/JCE APIs to access native PKCS\#11 libraries.
<span class="bold">The `SunPKCS11`{.codeph} provider itself does not
contain cryptographic functionality</span>, it is simply a conduit
between the Java environment and the native PKCS11 providers. The [Java
PKCS\#11 Reference
Guide](pkcs11-reference-guide1.html#GUID-6DA72F34-6C6A-4F7D-ADBA-5811576A9331 "The SunPKCS11 provider, in contrast to most other providers, does not implement cryptographic algorithms itself. Instead, it acts as a bridge between the Java JCA and JCE APIs and the native PKCS#11 cryptographic API, translating the calls and conventions between the two.")
has a much more detailed treatment of this provider.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D}

The SUN Provider {#JSSEC-GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D .sect2}
----------------

<div>
JDK 1.1 introduced the `Provider`{.codeph} architecture. The first JDK
provider was named `SUN`{.codeph}, and contained two types of
cryptographic services (`MessageDigest`{.codeph}and
`Signature`{.codeph}). In later releases, other mechanisms were added
(`SecureRandom`{.codeph}, `KeyPairGenerator`{.codeph},
`KeyFactory`{.codeph}, and so on).

<div class="section">
United States export regulations in effect at the time placed
significant restrictions on the type of cryptographic functionality that
could be made available internationally in the JDK. For this reason, the
`SUN`{.codeph} provider has historically contained cryptographic engines
that did not directly encrypt or decrypt data.

The following algorithms are available in the `SUN`{.codeph} provider:

<div class="tblformal" id="GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D__GUID-44F15A48-44CB-4160-957D-5CAC7AA7CA74">
Table 4-4 Algorithms in SUN provider

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Names                   |
+:==================================+:==================================+
| `AlgorithmParameterGenerator`{.co | DSA                               |
| deph}                             |                                   |
+-----------------------------------+-----------------------------------+
| `AlgorithmParameters`{.codeph}    | DSA                               |
+-----------------------------------+-----------------------------------+
| `CertificateFactory`{.codeph}     | X.509                             |
+-----------------------------------+-----------------------------------+
| `CertPathBuilder`{.codeph}        | PKIX                              |
+-----------------------------------+-----------------------------------+
| `CertPathValidator`{.codeph}      | PKIX                              |
+-----------------------------------+-----------------------------------+
| `CertStore`{.codeph}              | Collection                        |
+-----------------------------------+-----------------------------------+
| `Configuration`{.codeph}          | JavaLoginConfig                   |
+-----------------------------------+-----------------------------------+
| `KeyFactory`{.codeph}             | DSA                               |
+-----------------------------------+-----------------------------------+
| `KeyPairGenerator`{.codeph}       | DSA                               |
+-----------------------------------+-----------------------------------+
| `KeyStore`{.codeph}               | PKCS12[^Foot 6^](#GUID-3A80CC46-9 |
|                                   | 1E1-4E47-AC51-CB7B782CEA7D__THEPK |
|                                   | CS12KEYSTOREIMPLEMENTATIONDOES-2C |
|                                   | 70192F){#GUID-3A80CC46-91E1-4E47- |
|                                   | AC51-CB7B782CEA7D__THEPKCS12KEYST |
|                                   | OREIMPLEMENTATIONDOES-2C70192F}   |
|                                   |                                   |
|                                   | JKS                               |
|                                   |                                   |
|                                   | DKS                               |
|                                   |                                   |
|                                   | CaseExactJKS                      |
+-----------------------------------+-----------------------------------+
| `MessageDigest`{.codeph}          | MD2                               |
|                                   |                                   |
|                                   | MD5                               |
|                                   |                                   |
|                                   | SHA-1                             |
|                                   |                                   |
|                                   | SHA-224                           |
|                                   |                                   |
|                                   | SHA-256                           |
|                                   |                                   |
|                                   | SHA-384                           |
|                                   |                                   |
|                                   | SHA-512                           |
|                                   |                                   |
|                                   | SHA-512/224                       |
|                                   |                                   |
|                                   | SHA-512/256                       |
|                                   |                                   |
|                                   | SHA3-224                          |
|                                   |                                   |
|                                   | SHA3-256                          |
|                                   |                                   |
|                                   | SHA3-384                          |
|                                   |                                   |
|                                   | SHA3-512                          |
+-----------------------------------+-----------------------------------+
| `Policy`{.codeph}                 | JavaPolicy                        |
+-----------------------------------+-----------------------------------+
| `SecureRandom`{.codeph}           | DRBG                              |
|                                   |                                   |
|                                   | (The following mechanisms and     |
|                                   | algorithms are supported:         |
|                                   | Hash\_DRBG and HMAC\_DRBG with    |
|                                   | SHA-224, SHA-512/224, SHA-256,    |
|                                   | SHA-512/256, SHA-384 and SHA-512. |
|                                   | CTR\_DRBG (both use derivation    |
|                                   | function and not use) with        |
|                                   | AES-128, AES-192 and AES-256.     |
|                                   | Prediction resistance and         |
|                                   | reseeding supported for each      |
|                                   | combination, and security         |
|                                   | strength can be requested from    |
|                                   | 112 up to the highest strength    |
|                                   | one supports.)                    |
|                                   |                                   |
|                                   | SHA1PRNG                          |
|                                   |                                   |
|                                   | (Initial seeding is currently     |
|                                   | done via a combination of system  |
|                                   | attributes and the                |
|                                   | `java.security`{.codeph} entropy  |
|                                   | gathering device.)                |
|                                   |                                   |
|                                   | NativePRNG                        |
|                                   |                                   |
|                                   | (`nextBytes()`{.codeph} uses      |
|                                   | `/dev/urandom`{.codeph},          |
|                                   | `generateSeed()`{.codeph} uses    |
|                                   | `/dev/random`{.codeph})           |
|                                   |                                   |
|                                   | NativePRNGBlocking                |
|                                   |                                   |
|                                   | (`nextBytes()`{.codeph} and       |
|                                   | `generateSeed()`{.codeph} use     |
|                                   | `/dev/random`{.codeph})           |
|                                   |                                   |
|                                   | NativePRNGNonBlocking             |
|                                   |                                   |
|                                   | (`nextBytes()`{.codeph} and       |
|                                   | `generateSeed()`{.codeph} use     |
|                                   | `/dev/urandom`{.codeph})          |
+-----------------------------------+-----------------------------------+
| `Signature`{.codeph}              | NONEwithDSA                       |
|                                   |                                   |
|                                   | SHA1withDSA                       |
|                                   |                                   |
|                                   | SHA224withDSA                     |
|                                   |                                   |
|                                   | SHA256withDSA                     |
|                                   |                                   |
|                                   | NONEwithDSAinP1363Format          |
|                                   |                                   |
|                                   | SHA1withDSAinP1363Format          |
|                                   |                                   |
|                                   | SHA224withDSAinP1363Format        |
|                                   |                                   |
|                                   | SHA256withDSAinP1363Format        |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

^Footnote 6^ The PKCS12 <span class="apiname">KeyStore</span>
implementation does not support the <span class="apiname">KeyBag</span>
type.

The following table lists OIDs associated with SHA Message Digests:

<div class="tblformal" id="GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D__GUID-7C3B53BC-BFD3-4AD7-AC12-B55255948556">
Table 4-5 OIDs associated with SHA Message Digests

  SHA Message Digest   OID
  -------------------- -------------------------
  SHA-224              2.16.840.1.101.3.4.2.4
  SHA-256              2.16.840.1.101.3.4.2.1
  SHA-384              2.16.840.1.101.3.4.2.2
  SHA-512              2.16.840.1.101.3.4.2.3
  SHA-512/224          2.16.840.1.101.3.4.2.5
  SHA-512/256          2.16.840.1.101.3.4.2.6
  SHA3-224             2.16.840.1.101.3.4.2.7
  SHA3-256             2.16.840.1.101.3.4.2.8
  SHA3-384             2.16.840.1.101.3.4.2.9
  SHA3-512             2.16.840.1.101.3.4.2.10

</div>
<!-- class="inftblhruleinformal" -->

The following table lists OIDs associated with DSA Signatures:

<div class="tblformal" id="GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D__GUID-9D4E5B7E-1E05-4D04-A2EB-1FAAE33E536C">
Table 4-6 OIDs associated with DSA Signatures

+-----------------------------------+-----------------------------------+
| DSA Signature                     | OID                               |
+:==================================+:==================================+
| SHA1withDSA                       | 1.2.840.10040.4.3                 |
|                                   |                                   |
|                                   | 1.3.14.3.2.13                     |
|                                   |                                   |
|                                   | 1.3.14.3.2.27                     |
+-----------------------------------+-----------------------------------+
| SHA224withDSA                     | 2.16.840.1.101.3.4.3.1            |
+-----------------------------------+-----------------------------------+
| SHA256withDSA                     | 2.16.840.1.101.3.4.3.2            |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Keysize Restrictions

The `SUN`{.codeph} provider uses the following default keysizes (in
bits) and enforces the following restrictions:

<span class="bold">KeyPairGenerator</span>

<div class="tblformal" id="GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D__GUID-A1D286EF-8BE6-49FF-BD0A-079AB8E32A3E">
  Alg. Name   Default Keysize   Restrictions/Comments
  ----------- ----------------- ---------------------------------------------------------------------------------
  DSA         1024              Keysize must be a multiple of 64, ranging from 512 to 1024, plus 2048 and 3072.

</div>
<!-- class="inftblhruleinformal" -->

<span class="bold">AlgorithmParameterGenerator</span>

<div class="tblformal" id="GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D__GUID-1AAB9D55-B839-4DC8-9637-8325388B091D">
  Alg. Name   Default Keysize   Restrictions/Comments
  ----------- ----------------- ---------------------------------------------------------------------------------
  DSA         1024              Keysize must be a multiple of 64, ranging from 512 to 1024, plus 2048 and 3072.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
CertificateFactory/CertPathBuilder/CertPathValidator/CertStore
Implementations

Additional details on the `SUN`{.codeph} provider implementations for
`CertificateFactory`{.codeph}, `CertPathBuilder`{.codeph},
`CertPathValidator`{.codeph} and `CertStore`{.codeph} are documented in
[Appendix B: CertPath Implementation in SUN
Provider](java-pki-programmers-guide.html#GUID-EB250086-0AC1-4D60-AE2A-FC7461374746)
of the PKI Programmer\'s Guide.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-17E3589E-E4BA-4881-9B12-9880DD2D128D}

The SunRsaSign Provider {#JSSEC-GUID-17E3589E-E4BA-4881-9B12-9880DD2D128D .sect2}
-----------------------

<div>
The `SunRsaSign`{.codeph} provider was introduced in JDK 1.3 as an
enhanced replacement for the RSA signature in the `SunJSSE`{.codeph}
provider.

<div class="section">
The following algorithms are available in the `SunRsaSign`{.codeph}
provider:

<div class="tblformal" id="GUID-17E3589E-E4BA-4881-9B12-9880DD2D128D__GUID-244A1C15-C97D-447C-AF41-B92C14A8ED20">
Table 4-7 The SunRsaSign Provider Algorithm Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Names                   |
+:==================================+:==================================+
| `KeyFactory`{.codeph}             | RSA                               |
+-----------------------------------+-----------------------------------+
| `KeyPairGenerator`{.codeph}       | RSA                               |
+-----------------------------------+-----------------------------------+
| `Signature`{.codeph}              | MD2withRSA                        |
|                                   |                                   |
|                                   | MD5withRSA                        |
|                                   |                                   |
|                                   | SHA1withRSA                       |
|                                   |                                   |
|                                   | SHA224withRSA                     |
|                                   |                                   |
|                                   | SHA256withRSA                     |
|                                   |                                   |
|                                   | SHA384withRSA                     |
|                                   |                                   |
|                                   | SHA512withRSA                     |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Keysize Restrictions

The `SunRsaSign`{.codeph} provider uses the following default keysize
(in bits) and enforces the following restriction:

KeyPairGenerator

<div class="tblformal" id="GUID-17E3589E-E4BA-4881-9B12-9880DD2D128D__GUID-9AD6A1F3-7AD5-48C0-B6D0-FED06FF653BD">
Table 4-8 The SunRsaSign Provider Keysize Restrictions

  Alg. Name   Default Keysize   Restrictions/Comments
  ----------- ----------------- -------------------------------------------------------------------------------------------------------------------------------------
  RSA         2048              Keysize must range between 512 and 16384 bits. If the key size exceeds 3072, then the public exponent length cannot exceed 64 bits.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2}

The SunJSSE Provider {#JSSEC-GUID-7093246A-31A3-4304-AC5F-5FB6400405E2 .sect2}
--------------------

<div>
<div class="section">
Algorithms

The Java Secure Socket Extension (JSSE) was originally released as a
separate \"Optional Package\" (also briefly known as a \"Standard
Extension\"), and was available for JDK
1.2.<span class="variable">n</span> and
1.3.<span class="variable">n</span>. The `SunJSSE`{.codeph} provider was
introduced as part of this release.

In earlier JDK releases, there were no RSA signature providers available
in the JDK, therefore `SunJSSE`{.codeph} had to provide its own RSA
implementation in order to use commonly available RSA-based
certificates. JDK 5 introduced the `SunRsaSign`{.codeph} provider, which
provides all the functionality (and more) of the `SunJSSE`{.codeph}
provider. Applications targeted at JDK 5.0 and later should request
instances of the `SunRsaSign`{.codeph} provider instead. For backward
compatibility, the RSA algorithms are still available through this
provider, but are actually implemented in the `SunRsaSign`{.codeph}
provider.

The following algorithms are available in the `SunJSSE`{.codeph}
provider:

<div class="tblformal" id="GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__GUID-58EB24A8-0520-44C5-B54A-1FA0E437F203">
+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Name(s)                 |
+:==================================+:==================================+
| `KeyFactory`{.codeph}             | RSA                               |
|                                   |                                   |
|                                   | <span class="bold">Note:</span>   |
|                                   | The SunJSSE provider is for       |
|                                   | backwards compatibility with      |
|                                   | older releases, and should no     |
|                                   | longer be used for                |
|                                   | `KeyFactory`{.codeph}.            |
+-----------------------------------+-----------------------------------+
| `KeyManagerFactory`{.codeph}      | PKIX: A factory for               |
|                                   | `X509ExtendedKeyManager`{.codeph} |
|                                   | instances that manage X.509       |
|                                   | certificate-based key pairs for   |
|                                   | local side authentication         |
|                                   | according to the rules defined by |
|                                   | the IETF PKIX working group in    |
|                                   | [RFC                              |
|                                   | 5280](http://www.ietf.org/rfc/rfc |
|                                   | 5280.txt).                        |
|                                   | This `KeyManagerFactory`{.codeph} |
|                                   | currently supports initialization |
|                                   | using a `KeyStore`{.codeph}       |
|                                   | object or                         |
|                                   | `javax.net.ssl.KeyStoreBuilderPar |
|                                   | ameters`{.codeph}.                |
|                                   |                                   |
|                                   | SunX509: A factory for            |
|                                   | `X509ExtendedKeyManager`{.codeph} |
|                                   | instances that manage X.509       |
|                                   | certificate-based key pairs for   |
|                                   | local side authentication, but    |
|                                   | with less strict checking of      |
|                                   | certificate usage/validity and    |
|                                   | chain verification. This          |
|                                   | `KeyManagerFactory`{.codeph}      |
|                                   | supports initialization using a   |
|                                   | `Keystore`{.codeph} object, but   |
|                                   | does not currently support        |
|                                   | initialization using the class    |
|                                   | `javax.net.ssl.ManagerFactoryPara |
|                                   | meters`{.codeph}.                 |
|                                   |                                   |
|                                   | <span class="bold">Note:</span>   |
|                                   | The SunX509 factory is for        |
|                                   | backwards compatibility with      |
|                                   | older releases, and should no     |
|                                   | longer be used.                   |
+-----------------------------------+-----------------------------------+
| `KeyPairGenerator`{.codeph}       | RSA                               |
|                                   |                                   |
|                                   | <span class="bold">Note:</span>   |
|                                   | The SunJSSE provider is for       |
|                                   | backwards compatibility with      |
|                                   | older releases, and should no     |
|                                   | longer be used for                |
|                                   | `KeyPairGenerator`{.codeph}.      |
+-----------------------------------+-----------------------------------+
| `KeyStore`{.codeph}               | PKCS12                            |
|                                   |                                   |
|                                   | <span class="bold">Note:</span>   |
|                                   | The SunJSSE provider is for       |
|                                   | backwards compatibility with      |
|                                   | older releases, and should no     |
|                                   | longer be used for                |
|                                   | `KeyStore`{.codeph}.              |
+-----------------------------------+-----------------------------------+
| `Signature`{.codeph}              | MD2withRSA                        |
|                                   |                                   |
|                                   | MD5withRSA                        |
|                                   |                                   |
|                                   | SHA1withRSA                       |
|                                   |                                   |
|                                   | <span class="bold">Note:</span>   |
|                                   | The SunJSSE provider is for       |
|                                   | backwards compatibility with      |
|                                   | older releases, and should no     |
|                                   | longer be used for                |
|                                   | `Signature`{.codeph}.             |
+-----------------------------------+-----------------------------------+
| `SSLContext`{.codeph}             | SSLv3                             |
|                                   |                                   |
|                                   | TLSv1                             |
|                                   |                                   |
|                                   | TLSv1.1                           |
|                                   |                                   |
|                                   | TLSv1.2                           |
|                                   |                                   |
|                                   | DTLSv1.0                          |
|                                   |                                   |
|                                   | DTLSv1.2                          |
+-----------------------------------+-----------------------------------+
| `TrustManagerFactory`{.codeph}    | PKIX: A factory for               |
|                                   | `X509ExtendedTrustManager`{.codep |
|                                   | h}                                |
|                                   | instances that validate           |
|                                   | certificate chains according to   |
|                                   | the rules defined by the IETF     |
|                                   | PKIX working group in [RFC        |
|                                   | 5280](http://www.ietf.org/rfc/rfc |
|                                   | 5280.txt).                        |
|                                   | This                              |
|                                   | `TrustManagerFactory`{.codeph}    |
|                                   | currently supports initialization |
|                                   | using a `KeyStore`{.codeph}       |
|                                   | object or                         |
|                                   | `javax.net.ssl.CertPathTrustManag |
|                                   | erParameters`{.codeph}.           |
|                                   |                                   |
|                                   | SunX509: A factory for            |
|                                   | `X509ExtendedTrustManager`{.codep |
|                                   | h}                                |
|                                   | instances that validate           |
|                                   | certificate chains, but with less |
|                                   | strict checking of certificate    |
|                                   | usage/validity and chain          |
|                                   | verification. This                |
|                                   | `TrustManagerFactory`{.codeph}    |
|                                   | supports initialization using a   |
|                                   | `Keystore`{.codeph} object, but   |
|                                   | does not currently support        |
|                                   | initialization using the class    |
|                                   | `javax.net.ssl.ManagerFactoryPara |
|                                   | meters`{.codeph}.                 |
|                                   |                                   |
|                                   | <span class="bold">Note:</span>   |
|                                   | The SunX509 factory is for        |
|                                   | backwards compatibility with      |
|                                   | older releases, and should no     |
|                                   | longer be used.                   |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section" id="GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__SUNJSSEPROVIDERPROTOCOLPARAMETERS-BBF75009">
SunJSSE Provider Protocol Parameters

The `SunJSSE`{.codeph} provider supports the following
`protocol`{.codeph} parameters:

<div class="tblformal" id="GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__SUNJSSEPROVIDERPROTOCOLPARAMETERS-61B2BFC2">
Table 4-9 SunJSSE Provider Protocol Parameters

  Protocol                                                                                                                                                                                                   Enabled by Default for Client                                                                                                                                                                                     Enabled by Default for Server
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -----------------------------------------------------------------------
  SSLv3                                                                                                                                                                                                      No (Unavailable[^Foot 7^](#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__SSLV3ISENABLEDSTARTINGWITHJDK8U31TH-29F18ACA){#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__SSLV3ISENABLEDSTARTINGWITHJDK8U31TH-29F18ACA} )   No (Unavailable[^Footref 7^](#fnsrc_d52441e1475){#fnsrc_d52441e1475})
  TLSv1                                                                                                                                                                                                      Yes                                                                                                                                                                                                               Yes
  TLSv1.1                                                                                                                                                                                                    Yes                                                                                                                                                                                                               Yes
  TLSv1.2                                                                                                                                                                                                    Yes                                                                                                                                                                                                               Yes
  SSLv2Hello[^Foot 8^](#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__THESSLV3TLSV1TLSV1.1ANDTLSV1.2PROTO-66271D36){#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__THESSLV3TLSV1TLSV1.1ANDTLSV1.2PROTO-66271D36}   No                                                                                                                                                                                                                Yes
  DTLSv1.0                                                                                                                                                                                                   Yes                                                                                                                                                                                                               Yes
  DTLSv1.2[^Foot 9^](#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__BOTHDTLSV1.0ANDDTLSV1.2AREENABLED.-661D7983){#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__BOTHDTLSV1.0ANDDTLSV1.2AREENABLED.-661D7983}       Yes                                                                                                                                                                                                               Yes

</div>
<!-- class="inftblhruleinformal" -->

^Footnote 7^ SSLv3 is enabled:

-   Starting with JDK 8u31, the SSLv3 protocol (Secure Socket Layer) has
    been deactivated and is not available by default. See the
    `java.security.Security`{.codeph} property
    `jdk.tls.disabledAlgorithms`{.codeph} in the
    `<java_home>/conf/security/java.security`{.codeph} file.

-   If SSLv3 is absolutely required, the protocol can be reactivated by
    removing \"SSLv3\" from the `jdk.tls.disabledAlgorithms`{.codeph}
    property in the `java.security` file or by dynamically setting this
    Security Property before JSSE is initialized.

-   To enable SSLv3 protocol at deploy level, after following the above
    steps, edit the `deployment.properties` file and add the following:
    `deployment.security.SSLv3=true`{.codeph}

</p>
^Footnote 8^ The SSLv3, TLSv1, TLSv1.1 and TLSv1.2 protocols allow you
to send SSLv3, TLSv1, TLSv1.1 and TLSv1.2 ClientHellos encapsulated in
an SSLv2 format hello by using the SSLv2Hello psuedo-protocol.

^Footnote 9^ Both DTLSv1.0 and DTLSv1.2 are enabled.

The following table illustrates which connection combinations are
possible when using SSLv2Hellos:

<div class="tblformal" id="GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__CONNECTIONSPOSSIBLEUSINGSSLV2HELLOS-61B2CF09">
Table 4-10 Connections Possible Using SSLv2Hellos

  Client        Server        Connection Possible?
  ------------- ------------- -------------------------------------------
  Enabled       Enabled       Yes
  Not enabled   Enabled       Yes (most interoperable: SunJSSE default)
  Enabled       Not enabled   No
  Not enabled   Not enabled   Yes

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Cipher Suites

`SunJSSE`{.codeph} supports a large number of cipher suites. [Table
4-11](oracle-providers.html#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__CIPHERSUITESSUPPORTEDBYSUNJSSE-29E460FE "List of cipher suites supported by SunJSSE, whether they are enabled or disabled by default, and the release in which they were introduced")
lists the cipher suites supported by `SunJSSE`{.codeph}, whether they
are enabled or disabled by default, and the release in which they were
introduced. A value of N/A means that the cipher suite hasn\'t been
implemented for that release.

<div class="infoboxnote" id="GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__ACCORDINGTODTLSVERSION1.0ANDDTLSVER-29DE2569">
Note:

According to [DTLS Version 1.0](http://tools.ietf.org/html/rfc4347) and
[DTLS Version 1.2](http://tools.ietf.org/html/rfc6347), RC4 cipher
suites must not be used with DTLS connections.

Cipher suites that use Elliptic Curve Cryptography (ECDSA, ECDH, ECDHE,
ECDH\_anon) require a JCE cryptographic provider that meets the
following requirements:

-   The provider must implement ECC as defined by the classes and
    interfaces in the packages `java.security.spec`{.codeph} and
    `java.security.interfaces`{.codeph}. The `getAlgorithm()`{.codeph}
    method of elliptic curve key objects must return the string \"EC\".

-   The provider must support the `Signature`{.codeph} algorithms
    SHA1withECDSA and NONEwithECDSA, the `KeyAgreement`{.codeph}
    algorithm ECDH, and a `KeyPairGenerator`{.codeph} and a
    `KeyFactory`{.codeph} for algorithm EC. If one of these algorithms
    is missing, SunJSSE does not allow EC cipher suites to be used.

-   The provider must support all the SECG curves referenced in [RFC
    4492](http://www.ietf.org/rfc/rfc4492.txt) specification, section
    5.1.1 (see also Appendix A, \"Equivalent Curves (Informative)\"). In
    certificates, points should be encoded using the uncompressed form
    and curves should be encoded using the `namedCurve`{.codeph} choice,
    that is, using an object identifier.

If these requirements are not met, EC cipher suites may not be
negotiated correctly.

</div>
<div class="tblformalwide" id="GUID-7093246A-31A3-4304-AC5F-5FB6400405E2__CIPHERSUITESSUPPORTEDBYSUNJSSE-29E460FE">
Table 4-11 Cipher Suites Supported by SunJSSE

+-------------+-------------+-------------+-------------+-------------+
| Cipher      | JDK 6       | JDK 7       | JDK 8       | JDK 9       |
| Suite       |             |             |             |             |
+:============+:============+:============+:============+:============+
| SSL\_DH\_an | Disabled    | Disabled[^F | Disabled    | Disabled    |
| on\_EXPORT\ |             | oot 10^](#G |             |             |
| _WITH\_DES4 |             | UID-7093246 |             |             |
| 0\_CBC\_SHA |             | A-31A3-4304 |             |             |
|             |             | -AC5F-5FB64 |             |             |
|             |             | 00405E2__RF |             |             |
|             |             | C4346TLS1.1 |             |             |
|             |             | FORBIDSTHEU |             |             |
|             |             | SEOFTHESESU |             |             |
|             |             | -29D7AD3A){ |             |             |
|             |             | #GUID-70932 |             |             |
|             |             | 46A-31A3-43 |             |             |
|             |             | 04-AC5F-5FB |             |             |
|             |             | 6400405E2__ |             |             |
|             |             | RFC4346TLS1 |             |             |
|             |             | .1FORBIDSTH |             |             |
|             |             | EUSEOFTHESE |             |             |
|             |             | SU-29D7AD3A |             |             |
|             |             | }           |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DH\_an | Disabled    | Disabled[^F | Disabled    | Disabled    |
| on\_EXPORT\ |             | ootref 10^] |             |             |
| _WITH\_RC4\ |             | (#fnsrc_d52 |             |             |
| _40\_MD5    |             | 441e1707){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e1707}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DH\_an | Disabled    | Disabled    | Disabled    | Disabled    |
| on\_WITH\_3 |             |             |             |             |
| DES\_EDE\_C |             |             |             |             |
| BC\_SHA     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DH\_an | Disabled    | Disabled[^F | Disabled    | Disabled    |
| on\_WITH\_D |             | oot 11^](#G |             |             |
| ES\_CBC\_SH |             | UID-7093246 |             |             |
| A           |             | A-31A3-4304 |             |             |
|             |             | -AC5F-5FB64 |             |             |
|             |             | 00405E2__RF |             |             |
|             |             | C5246TLS1.2 |             |             |
|             |             | FORBIDSTHEU |             |             |
|             |             | SEOFTHESESU |             |             |
|             |             | -29D6DCA9){ |             |             |
|             |             | #GUID-70932 |             |             |
|             |             | 46A-31A3-43 |             |             |
|             |             | 04-AC5F-5FB |             |             |
|             |             | 6400405E2__ |             |             |
|             |             | RFC5246TLS1 |             |             |
|             |             | .2FORBIDSTH |             |             |
|             |             | EUSEOFTHESE |             |             |
|             |             | SU-29D6DCA9 |             |             |
|             |             | }           |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DH\_an | Disabled    | Disabled    | Disabled    | Disabled    |
| on\_WITH\_R |             |             |             |             |
| C4\_128\_MD |             |             |             |             |
| 5           |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DHE\_D | Disabled    | Disabled[^F | Disabled    | Disabled    |
| SS\_EXPORT\ |             | ootref 10^] |             |             |
| _WITH\_DES4 |             | (#fnsrc_d52 |             |             |
| 0\_CBC\_SHA |             | 441e1779){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e1779}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DHE\_D | Enabled     | Enabled     | Enabled     | Enabled     |
| SS\_WITH\_3 |             |             |             |             |
| DES\_EDE\_C |             |             |             |             |
| BC\_SHA     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DHE\_D | Disabled    | Disabled[^F | Disabled    | Disabled    |
| SS\_WITH\_D |             | ootref 11^] |             |             |
| ES\_CBC\_SH |             | (#fnsrc_d52 |             |             |
| A           |             | 441e1813){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e1813}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DHE\_R | Disabled    | Disabled[^F | Disabled    | Disabled    |
| SA\_EXPORT\ |             | ootref 10^] |             |             |
| _WITH\_DES4 |             | (#fnsrc_d52 |             |             |
| 0\_CBC\_SHA |             | 441e1832){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e1832}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DHE\_R | Enabled     | Enabled     | Enabled     | Enabled     |
| SA\_WITH\_3 |             |             |             |             |
| DES\_EDE\_C |             |             |             |             |
| BC\_SHA     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_DHE\_R | Disabled    | Disabled[^F | Disabled    | Disabled    |
| SA\_WITH\_D |             | ootref 11^] |             |             |
| ES\_CBC\_SH |             | (#fnsrc_d52 |             |             |
| A           |             | 441e1866){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e1866}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_RSA\_E | Disabled    | Disabled[^F | Disabled    | Disabled    |
| XPORT\_WITH |             | ootref 10^] |             |             |
| \_DES40\_CB |             | (#fnsrc_d52 |             |             |
| C\_SHA      |             | 441e1886){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e1886}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_RSA\_E | Disabled    | Disabled[^F | Disabled    | Disabled    |
| XPORT\_WITH |             | ootref 10^] |             |             |
| \_RC4\_40\_ |             | (#fnsrc_d52 |             |             |
| MD5         |             | 441e1904){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e1904}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_RSA\_W | Enabled     | Enabled     | Enabled     | Enabled     |
| ITH\_3DES\_ |             |             |             |             |
| EDE\_CBC\_S |             |             |             |             |
| HA          |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_RSA\_W | Disabled    | Disabled[^F | Disabled    | Disabled    |
| ITH\_DES\_C |             | ootref 11^] |             |             |
| BC\_SHA     |             | (#fnsrc_d52 |             |             |
|             |             | 441e1938){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e1938}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_RSA\_W | Disabled    | Disabled    | Disabled    | Disabled    |
| ITH\_NULL\_ |             |             |             |             |
| MD5         |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_RSA\_W | Disabled    | Disabled    | Disabled    | Disabled    |
| ITH\_NULL\_ |             |             |             |             |
| SHA         |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_RSA\_W | Enabled     | Enabled     | Enabled     | Disabled    |
| ITH\_RC4\_1 |             |             |             |             |
| 28\_MD5     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| SSL\_RSA\_W | Enabled     | Enabled     | Enabled     | N/A         |
| ITH\_RC4\_1 |             |             |             |             |
| 28\_SHA     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DH\_an | Disabled    | Disabled    | Disabled    | Disabled    |
| on\_WITH\_A |             |             |             |             |
| ES\_128\_CB |             |             |             |             |
| C\_SHA      |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DH\_an | N/A         | Disabled    | Disabled    | Disabled    |
| on\_WITH\_A |             |             |             |             |
| ES\_128\_CB |             |             |             |             |
| C\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DH\_an | N/A         | N/A         | Disabled    | Disabled    |
| on\_WITH\_A |             |             |             |             |
| ES\_128\_GC |             |             |             |             |
| M\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DH\_an | Disabled    | Disabled    | Disabled    | Disabled    |
| on\_WITH\_A |             |             |             |             |
| ES\_256\_CB |             |             |             |             |
| C\_SHA      |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DH\_an | N/A         | Disabled    | Disabled    | Disabled    |
| on\_WITH\_A |             |             |             |             |
| ES\_256\_CB |             |             |             |             |
| C\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DH\_an | N/A         | N/A         | Disabled    | Disabled    |
| on\_WITH\_A |             |             |             |             |
| ES\_256\_GC |             |             |             |             |
| M\_SHA384   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | Enabled     | Enabled     | Enabled     | Enabled     |
| SS\_WITH\_A |             |             |             |             |
| ES\_128\_CB |             |             |             |             |
| C\_SHA      |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| SS\_WITH\_A |             | ot 12^](#GU |             |             |
| ES\_128\_CB |             | ID-7093246A |             |             |
| C\_SHA256   |             | -31A3-4304- |             |             |
|             |             | AC5F-5FB640 |             |             |
|             |             | 0405E2__CIP |             |             |
|             |             | HERSUITESWI |             |             |
|             |             | THSHA384AND |             |             |
|             |             | SHA256AREA- |             |             |
|             |             | 29D6CF3B){# |             |             |
|             |             | GUID-709324 |             |             |
|             |             | 6A-31A3-430 |             |             |
|             |             | 4-AC5F-5FB6 |             |             |
|             |             | 400405E2__C |             |             |
|             |             | IPHERSUITES |             |             |
|             |             | WITHSHA384A |             |             |
|             |             | NDSHA256ARE |             |             |
|             |             | A-29D6CF3B} |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | N/A         | N/A         | Enabled     | Enabled     |
| SS\_WITH\_A |             |             |             |             |
| ES\_128\_GC |             |             |             |             |
| M\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | Enabled     | Enabled     | Enabled     | Enabled     |
| SS\_WITH\_A |             |             |             |             |
| ES\_256\_CB |             |             |             |             |
| C\_SHA      |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | N/A         | N/A         | N/A         | Enabled     |
| SS\_WITH\_A |             |             |             |             |
| ES\_256\_CB |             |             |             |             |
| C\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | N/A         | N/A         | N/A         | Enabled     |
| SS\_WITH\_A |             |             |             |             |
| ES\_256\_CB |             |             |             |             |
| C\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | N/A         | N/A         | N/A         | Enabled     |
| SS\_WITH\_A |             |             |             |             |
| ES\_256\_CB |             |             |             |             |
| C\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | N/A         | N/A         | N/A         | Enabled     |
| SS\_WITH\_A |             |             |             |             |
| ES\_256\_CB |             |             |             |             |
| C\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_D | N/A         | N/A         | Enabled     | Enabled     |
| SS\_WITH\_A |             |             |             |             |
| ES\_256\_GC |             |             |             |             |
| M\_SHA384   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_R | Enabled     | Enabled     | Enabled     | Enabled     |
| SA\_WITH\_A |             |             |             |             |
| ES\_128\_CB |             |             |             |             |
| C\_SHA      |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_R | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| SA\_WITH\_A |             | otref 12^]( |             |             |
| ES\_128\_CB |             | #fnsrc_d524 |             |             |
| C\_SHA256   |             | 41e2281){#f |             |             |
|             |             | nsrc_d52441 |             |             |
|             |             | e2281}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_R | N/A         | N/A         | Enabled     | Enabled     |
| SA\_WITH\_A |             |             |             |             |
| ES\_128\_GC |             |             |             |             |
| M\_SHA256   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_R | Enabled     | Enabled     | Enabled     | Enabled     |
| SA\_WITH\_A |             |             |             |             |
| ES\_256\_CB |             |             |             |             |
| C\_SHA      |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_R | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| SA\_WITH\_A |             | otref 12^]( |             |             |
| ES\_256\_CB |             | #fnsrc_d524 |             |             |
| C\_SHA256   |             | 41e2331){#f |             |             |
|             |             | nsrc_d52441 |             |             |
|             |             | e2331}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_DHE\_R | N/A         | N/A         | Enabled     | Enabled     |
| SA\_WITH\_A |             |             |             |             |
| ES\_256\_GC |             |             |             |             |
| M\_SHA384   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| anon\_WITH\ |             |             |             |             |
| _3DES\_EDE\ |             |             |             |             |
| _CBC\_SHA   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| anon\_WITH\ |             |             |             |             |
| _AES\_128\_ |             |             |             |             |
| CBC\_SHA    |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| anon\_WITH\ |             |             |             |             |
| _AES\_256\_ |             |             |             |             |
| CBC\_SHA    |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| anon\_WITH\ |             |             |             |             |
| _NULL\_SHA  |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| anon\_WITH\ |             |             |             |             |
| _RC4\_128\_ |             |             |             |             |
| SHA         |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Enabled     | Enabled     | Enabled     | Enabled     |
| ECDSA\_WITH |             |             |             |             |
| \_3DES\_EDE |             |             |             |             |
| \_CBC\_SHA  |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Enabled     | Enabled     | Enabled     | Enabled     |
| ECDSA\_WITH |             |             |             |             |
| \_AES\_128\ |             |             |             |             |
| _CBC\_SHA   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| ECDSA\_WITH |             | otref 12^]( |             |             |
| \_AES\_128\ |             | #fnsrc_d524 |             |             |
| _CBC\_SHA25 |             | 41e2478){#f |             |             |
| 6           |             | nsrc_d52441 |             |             |
|             |             | e2478}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | N/A         | N/A         | Enabled     | Enabled     |
| ECDSA\_WITH |             |             |             |             |
| \_AES\_128\ |             |             |             |             |
| _GCM\_SHA25 |             |             |             |             |
| 6           |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Enabled     | Enabled     | Enabled     | Enabled     |
| ECDSA\_WITH |             |             |             |             |
| \_AES\_256\ |             |             |             |             |
| _CBC\_SHA   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| ECDSA\_WITH |             | otref 12^]( |             |             |
| \_AES\_256\ |             | #fnsrc_d524 |             |             |
| _CBC\_SHA38 |             | 41e2528){#f |             |             |
| 4           |             | nsrc_d52441 |             |             |
|             |             | e2528}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | N/A         | N/A         | Enabled     | Enabled     |
| ECDSA\_WITH |             |             |             |             |
| \_AES\_256\ |             |             |             |             |
| _GCM\_SHA38 |             |             |             |             |
| 4           |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| ECDSA\_WITH |             |             |             |             |
| \_NULL\_SHA |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Enabled     | Enabled     | Enabled     | Enabled     |
| ECDSA\_WITH |             |             |             |             |
| \_RC4\_128\ |             |             |             |             |
| _SHA        |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Enabled     | Enabled     | Enabled     | Enabled     |
| RSA\_WITH\_ |             |             |             |             |
| 3DES\_EDE\_ |             |             |             |             |
| CBC\_SHA    |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Enabled     | Enabled     | Enabled     | Enabled     |
| RSA\_WITH\_ |             |             |             |             |
| AES\_128\_C |             |             |             |             |
| BC\_SHA     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| RSA\_WITH\_ |             | otref 12^]( |             |             |
| AES\_128\_C |             | #fnsrc_d524 |             |             |
| BC\_SHA256  |             | 41e2627){#f |             |             |
|             |             | nsrc_d52441 |             |             |
|             |             | e2627}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | N/A         | N/A         | Enabled     | Enabled     |
| RSA\_WITH\_ |             |             |             |             |
| AES\_128\_G |             |             |             |             |
| CM\_SHA256  |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Enabled     | Enabled     | Enabled     | Enabled     |
| RSA\_WITH\_ |             |             |             |             |
| AES\_256\_C |             |             |             |             |
| BC\_SHA     |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| RSA\_WITH\_ |             | otref 12^]( |             |             |
| AES\_256\_C |             | #fnsrc_d524 |             |             |
| BC\_SHA384  |             | 41e2677){#f |             |             |
|             |             | nsrc_d52441 |             |             |
|             |             | e2677}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | N/A         | N/A         | Enabled     | Enabled     |
| RSA\_WITH\_ |             |             |             |             |
| AES\_256\_G |             |             |             |             |
| CM\_SHA384  |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| RSA\_WITH\_ |             |             |             |             |
| NULL\_SHA   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDH\_ | Enabled     | Enabled     | Enabled     |             |
| RSA\_WITH\_ |             |             |             |             |
| RC4\_128\_S |             |             |             |             |
| HA          |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Enabled     | Enabled     | Enabled     | Enabled     |
| _ECDSA\_WIT |             |             |             |             |
| H\_3DES\_ED |             |             |             |             |
| E\_CBC\_SHA |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Enabled     | Enabled     | Enabled     | Enabled     |
| _ECDSA\_WIT |             |             |             |             |
| H\_AES\_128 |             |             |             |             |
| \_CBC\_SHA  |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| _ECDSA\_WIT |             | otref 12^]( |             |             |
| H\_AES\_128 |             | #fnsrc_d524 |             |             |
| \_CBC\_SHA2 |             | 41e2775){#f |             |             |
| 56          |             | nsrc_d52441 |             |             |
|             |             | e2775}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | N/A         | Enabled     | Enabled     |
| _ECDSA\_WIT |             |             |             |             |
| H\_AES\_128 |             |             |             |             |
| \_GCM\_SHA2 |             |             |             |             |
| 56          |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Enabled     | Enabled     | Enabled     | Enabled     |
| _ECDSA\_WIT |             |             |             |             |
| H\_AES\_256 |             |             |             |             |
| \_CBC\_SHA  |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| _ECDSA\_WIT |             | otref 12^]( |             |             |
| H\_AES\_256 |             | #fnsrc_d524 |             |             |
| \_CBC\_SHA3 |             | 41e2826){#f |             |             |
| 84          |             | nsrc_d52441 |             |             |
|             |             | e2826}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | N/A         | N/A         | Enabled     |
| _ECDSA\_WIT |             |             |             |             |
| H\_AES\_256 |             |             |             |             |
| \_CBC\_SHA3 |             |             |             |             |
| 84          |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | N/A         | N/A         | Enabled     |
| _ECDSA\_WIT |             |             |             |             |
| H\_AES\_256 |             |             |             |             |
| \_CBC\_SHA3 |             |             |             |             |
| 84          |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | N/A         | Enabled     | Enabled     |
| _ECDSA\_WIT |             |             |             |             |
| H\_AES\_256 |             |             |             |             |
| \_GCM\_SHA3 |             |             |             |             |
| 84          |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Disabled    | Disabled    | Disabled    | Disabled    |
| _ECDSA\_WIT |             |             |             |             |
| H\_NULL\_SH |             |             |             |             |
| A           |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Enabled     | Enabled     | Enabled     | Disabled    |
| _ECDSA\_WIT |             |             |             |             |
| H\_RC4\_128 |             |             |             |             |
| \_SHA       |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Enabled     | Enabled     | Enabled     | Enabled     |
| _RSA\_WITH\ |             |             |             |             |
| _3DES\_EDE\ |             |             |             |             |
| _CBC\_SHA   |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Enabled     | Enabled     | Enabled     | Enabled     |
| _RSA\_WITH\ |             |             |             |             |
| _AES\_128\_ |             |             |             |             |
| CBC\_SHA    |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| _RSA\_WITH\ |             | otref 12^]( |             |             |
| _AES\_128\_ |             | #fnsrc_d524 |             |             |
| CBC\_SHA256 |             | 41e2956){#f |             |             |
|             |             | nsrc_d52441 |             |             |
|             |             | e2956}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | N/A         | Enabled     | Enabled     |
| _RSA\_WITH\ |             |             |             |             |
| _AES\_128\_ |             |             |             |             |
| GCM\_SHA256 |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Enabled     | Enabled     | Enabled     | Enabled     |
| _RSA\_WITH\ |             |             |             |             |
| _AES\_256\_ |             |             |             |             |
| CBC\_SHA    |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| _RSA\_WITH\ |             | otref 12^]( |             |             |
| _AES\_256\_ |             | #fnsrc_d524 |             |             |
| CBC\_SHA384 |             | 41e3007){#f |             |             |
|             |             | nsrc_d52441 |             |             |
|             |             | e3007}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | N/A         | Enabled     | N/A         |
| _RSA\_WITH\ |             |             |             |             |
| _AES\_256\_ |             |             |             |             |
| GCM\_SHA384 |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Disabled    | Disabled    | Disabled    | Disabled    |
| _RSA\_WITH\ |             |             |             |             |
| _NULL\_SHA  |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | Enabled     | Enabled     | Enabled     | Enabled     |
| _RSA\_WITH\ |             |             |             |             |
| _RC4\_128\_ |             |             |             |             |
| SHA         |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_ECDHE\ | N/A         | N/A         | N/A         | Disabled    |
| _RSA\_WITH\ |             |             |             |             |
| _RC4\_128\_ |             |             |             |             |
| SHA         |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_EMPTY\ | u22+        | Enabled     | Enabled     | N/A         |
| _RENEGOTIAT |             |             |             |             |
| ION\_INFO\_ |             |             |             |             |
| SCSV[^Foot  |             |             |             |             |
| 13^](#GUID- |             |             |             |             |
| 7093246A-31 |             |             |             |             |
| A3-4304-AC5 |             |             |             |             |
| F-5FB640040 |             |             |             |             |
| 5E2__TLS_EM |             |             |             |             |
| PTY_RENEGOT |             |             |             |             |
| IATION_INFO |             |             |             |             |
| _SCSVIS-29D |             |             |             |             |
| D05D3){#GUI |             |             |             |             |
| D-7093246A- |             |             |             |             |
| 31A3-4304-A |             |             |             |             |
| C5F-5FB6400 |             |             |             |             |
| 405E2__TLS_ |             |             |             |             |
| EMPTY_RENEG |             |             |             |             |
| OTIATION_IN |             |             |             |             |
| FO_SCSVIS-2 |             |             |             |             |
| 9DD05D3}    |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled[^F | Disabled    | Disabled    |
| EXPORT\_WIT |             | ootref 10^] |             |             |
| H\_DES\_CBC |             | (#fnsrc_d52 |             |             |
| \_40\_MD5   |             | 441e3121){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e3121}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled[^F | Disabled    | Disabled    |
| EXPORT\_WIT |             | ootref 10^] |             |             |
| H\_DES\_CBC |             | (#fnsrc_d52 |             |             |
| \_40\_SHA   |             | 441e3139){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e3139}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled[^F | Disabled    | Disabled    |
| EXPORT\_WIT |             | ootref 10^] |             |             |
| H\_RC4\_40\ |             | (#fnsrc_d52 |             |             |
| _MD5        |             | 441e3157){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e3157}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled[^F | Disabled    | Disabled    |
| EXPORT\_WIT |             | ootref 10^] |             |             |
| H\_RC4\_40\ |             | (#fnsrc_d52 |             |             |
| _SHA        |             | 441e3176){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e3176}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| WITH\_3DES\ |             |             |             |             |
| _EDE\_CBC\_ |             |             |             |             |
| MD5         |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| WITH\_3DES\ |             |             |             |             |
| _EDE\_CBC\_ |             |             |             |             |
| SHA         |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled[^F | Disabled    | Disabled    |
| WITH\_DES\_ |             | ootref 11^] |             |             |
| CBC\_MD5    |             | (#fnsrc_d52 |             |             |
|             |             | 441e3226){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e3226}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled[^F | Disabled    | Disabled    |
| WITH\_DES\_ |             | ootref 11^] |             |             |
| CBC\_SHA    |             | (#fnsrc_d52 |             |             |
|             |             | 441e3245){# |             |             |
|             |             | fnsrc_d5244 |             |             |
|             |             | 1e3245}     |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| WITH\_RC4\_ |             |             |             |             |
| 128\_MD5    |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_KRB5\_ | Disabled    | Disabled    | Disabled    | Disabled    |
| WITH\_RC4\_ |             |             |             |             |
| 128\_SHA    |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_RSA\_W | Enabled     | Enabled     | Enabled     | Enabled     |
| ITH\_AES\_1 |             |             |             |             |
| 28\_CBC\_SH |             |             |             |             |
| A           |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_RSA\_W | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| ITH\_AES\_1 |             | otref 12^]( |             |             |
| 28\_CBC\_SH |             | #fnsrc_d524 |             |             |
| A256        |             | 41e3312){#f |             |             |
|             |             | nsrc_d52441 |             |             |
|             |             | e3312}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_RSA\_W | N/A         | N/A         | Enabled     | Enabled     |
| ITH\_AES\_1 |             |             |             |             |
| 28\_GCM\_SH |             |             |             |             |
| A256        |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_RSA\_W | Enabled     | Enabled     | Enabled     | Enabled     |
| ITH\_AES\_2 |             |             |             |             |
| 56\_CBC\_SH |             |             |             |             |
| A           |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_RSA\_W | N/A         | Enabled[^Fo | Enabled     | Enabled     |
| ITH\_AES\_2 |             | otref 12^]( |             |             |
| 56\_CBC\_SH |             | #fnsrc_d524 |             |             |
| A256        |             | 41e3363){#f |             |             |
|             |             | nsrc_d52441 |             |             |
|             |             | e3363}      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_RSA\_W | N/A         | N/A         | Enabled     | Enabled     |
| ITH\_AES\_2 |             |             |             |             |
| 56\_GCM\_SH |             |             |             |             |
| A384        |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| TLS\_RSA\_W | N/A         | Disabled    | Disabled    | Disabled    |
| ITH\_NULL\_ |             |             |             |             |
| SHA256      |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+

</div>
<!-- class="inftblhruleinformal" -->

^Footnote 10^ [RFC 4346 TLS 1.1](http://www.ietf.org/rfc/rfc4346.txt)
forbids the use of these suites. These can be used in the SSLv3/TLS1.0
protocols, but cannot be used in TLS 1.1 and later.

^Footnote 11^ [RFC 5246 TLS 1.2](http://www.ietf.org/rfc/rfc5246.txt)
forbids the use of these suites. These can be used in the
SSLv3/TLS1.0/TLS1.1 protocols, but cannot be used in TLS 1.2 and later.

^Footnote 12^ Cipher suites with SHA384 and SHA256 are available only
for TLS 1.2 or later.

^Footnote 13^ `TLS_EMPTY_RENEGOTIATION_INFO_SCSV`{.codeph} is a
pseudo-cipher suite that supports RFC 5746. See [Transport Layer
Security (TLS) Renegotiation
Issue](java-secure-socket-extension-jsse-reference-guide.html#GUID-9C767872-3A6C-4AD1-9805-49F112A0FA28 "In the fall of 2009, a flaw was discovered in the SSL/TLS protocols. A fix to the protocol was developed by the IETF TLS Working Group, and current versions of the JDK contain this fix. This section describes the situation in much more detail, along with interoperability issues when communicating with older implementations that do not contain this protocol fix.")
in [Java Secure Socket Extension (JSSE) Reference
Guide](java-secure-socket-extension-jsse-reference-guide.html#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345 "The Java Secure Socket Extension (JSSE) enables secure Internet communications. It provides a framework and an implementation for a Java version of the SSL, TLS, and DTLS protocols and includes functionality for data encryption, server authentication, message integrity, and optional client authentication.").

</div>
<!-- class="section" -->

<div class="section">
Tighter Checking of EncryptedPreMasterSecret Version Numbers

Prior to the JDK 7 release, the SSL/TLS implementation did not check the
version number in PreMasterSecret, and the SSL/TLS client did not send
the correct version number by default. Unless the system property
`com.sun.net.ssl.rsaPreMasterSecretFix`{.codeph} is set to
`true`{.codeph}, the TLS client sends the active negotiated version, but
not the expected maximum version supported by the client.

For compatibility, this behavior is preserved for SSL version 3.0 and
TLS version 1.0. However, for TLS version 1.1 or later, the
implementation tightens checking the PreMasterSecret version numbers as
required by [RFC 5246](http://www.ietf.org/rfc/rfc5246.txt). Clients
always send the correct version number, and servers check the version
number strictly. The system property,
`com.sun.net.ssl.rsaPreMasterSecretFix`{.codeph}, is not used in TLS 1.1
or later.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7}

The SunJCE Provider {#JSSEC-GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7 .sect2}
-------------------

<div>
As described briefly in The SUN Provider, US export regulations at the
time restricted the type of cryptographic functionality that could be
available in the JDK. A separate API and reference implementation was
developed that allowed applications to encrypt/decrypt date. The Java
Cryptographic Extension (JCE) was released as a separate "Optional
Package" (also briefly known as a "Standard Extension"), and was
available for JDK 1.2x and 1.3x. During the development of JDK 1.4,
regulations were relaxed enough that JCE (and SunJSSE) could be bundled
as part of the JDK.

<div class="section">
The following algorithms are available in the SunJCE provider:

<div class="tblformal" id="GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7__GUID-C2F51EF7-FFB7-4113-960C-DE484E8274C8">
Table 4-12 The SunJCE Provider Algorithm Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Names                   |
+:==================================+:==================================+
| `AlgorithmParameterGenerator`{.co | DiffieHellman                     |
| deph}                             |                                   |
+-----------------------------------+-----------------------------------+
| `AlgorithmParameters`{.codeph}    | AESBlowfish                       |
|                                   |                                   |
|                                   | DES                               |
|                                   |                                   |
|                                   | DESede                            |
|                                   |                                   |
|                                   | DiffieHellman                     |
|                                   |                                   |
|                                   | GCM                               |
|                                   |                                   |
|                                   | OAEP                              |
|                                   |                                   |
|                                   | PBE                               |
|                                   |                                   |
|                                   | PBES2                             |
|                                   |                                   |
|                                   | PBEWithHmacSHA1AndAES\_128        |
|                                   |                                   |
|                                   | PBEWithHmacSHA224AndAES\_128      |
|                                   |                                   |
|                                   | PBEWithHmacSHA256AndAES\_128      |
|                                   |                                   |
|                                   | PBEWithHmacSHA384AndAES\_128      |
|                                   |                                   |
|                                   | PBEWithHmacSHA512AndAES\_128      |
|                                   |                                   |
|                                   | PBEWithHmacSHA1AndAES\_256        |
|                                   |                                   |
|                                   | PBEWithHmacSHA224AndAES\_256      |
|                                   |                                   |
|                                   | PBEWithHmacSHA256AndAES\_256      |
|                                   |                                   |
|                                   | PBEWithHmacSHA384AndAES\_256      |
|                                   |                                   |
|                                   | PBEWithHmacSHA512AndAES\_256      |
|                                   |                                   |
|                                   | PBEWithMD5AndDES                  |
|                                   |                                   |
|                                   | PBEWithMD5AndTripleDES            |
|                                   |                                   |
|                                   | PBEWithSHA1AndDESede              |
|                                   |                                   |
|                                   | PBEWithSHA1AndRC2\_40             |
|                                   |                                   |
|                                   | PBEWithSHA1AndRC2\_128            |
|                                   |                                   |
|                                   | PBEWithSHA1AndRC4\_40             |
|                                   |                                   |
|                                   | PBEWithSHA1AndPC4\_128            |
|                                   |                                   |
|                                   | RC2                               |
+-----------------------------------+-----------------------------------+
| `Cipher`{.codeph}                 | See [Table                        |
|                                   | 4-13](oracle-providers.html#GUID-A |
|                                   | 47B1249-593C-4C38-A0D0-68FA7681E0 |
|                                   | A7__GUID-5AB84158-7D99-4604-98EC- |
|                                   | 1E2F755CCB1C "List of SunJCE Prov |
|                                   | ider Cipher Transformations; incl |
|                                   | udes algorithm names, modes, and  |
|                                   | paddings.")                       |
+-----------------------------------+-----------------------------------+
| `KeyAgreement`{.codeph}           | DiffieHellman                     |
+-----------------------------------+-----------------------------------+
| `KeyFactory`{.codeph}             | DiffieHellman                     |
+-----------------------------------+-----------------------------------+
| `KeyGenerator`{.codeph}           | AES                               |
|                                   |                                   |
|                                   | ARCFOUR                           |
|                                   |                                   |
|                                   | Blowfish                          |
|                                   |                                   |
|                                   | DES                               |
|                                   |                                   |
|                                   | DESede                            |
|                                   |                                   |
|                                   | HmacMD5                           |
|                                   |                                   |
|                                   | HmacSHA1                          |
|                                   |                                   |
|                                   | HmacSHA224                        |
|                                   |                                   |
|                                   | HmacSHA256                        |
|                                   |                                   |
|                                   | HmacSHA384                        |
|                                   |                                   |
|                                   | HmacSHA512                        |
|                                   |                                   |
|                                   | RC2                               |
+-----------------------------------+-----------------------------------+
| `KeyPairGenerator`{.codeph}       | DiffieHellman                     |
+-----------------------------------+-----------------------------------+
| `KeyStore`{.codeph}               | JCEKS                             |
+-----------------------------------+-----------------------------------+
| `Mac`{.codeph}                    | HmacMD5                           |
|                                   |                                   |
|                                   | HmacSHA1                          |
|                                   |                                   |
|                                   | HmacSHA224                        |
|                                   |                                   |
|                                   | HmacSHA384                        |
|                                   |                                   |
|                                   | HmacSHA512                        |
|                                   |                                   |
|                                   | HmacSHA256                        |
|                                   |                                   |
|                                   | HmacSHA512/224                    |
|                                   |                                   |
|                                   | HmacSHA512/256                    |
|                                   |                                   |
|                                   | HmacPBESHA1                       |
|                                   |                                   |
|                                   | PBEWithHmacSHA1                   |
|                                   |                                   |
|                                   | PBEWithHmacSHA224                 |
|                                   |                                   |
|                                   | PBEWithHmacSHA256                 |
|                                   |                                   |
|                                   | PBEWithHmacSHA384                 |
|                                   |                                   |
|                                   | PBEWithHmacSHA512                 |
+-----------------------------------+-----------------------------------+
| `SecretKeyFactory`{.codeph}       | DES                               |
|                                   |                                   |
|                                   | DESede                            |
|                                   |                                   |
|                                   | PBEWithMD5AndDES                  |
|                                   |                                   |
|                                   | PBEWithMD5AndTripleDES            |
|                                   |                                   |
|                                   | PBEWithSHA1AndDESede              |
|                                   |                                   |
|                                   | PBEWithSHA1AndRC2\_40             |
|                                   |                                   |
|                                   | PBEWithSHA1AndRC2\_128            |
|                                   |                                   |
|                                   | PBEWithSHA1AndRC4\_40             |
|                                   |                                   |
|                                   | PBEWithSHA1AndRC4\_128            |
|                                   |                                   |
|                                   | PBKDF2WithHmacSHA1                |
|                                   |                                   |
|                                   | PBKDF2WithHmacSHA224              |
|                                   |                                   |
|                                   | PBKDF2WithHmacSHA256              |
|                                   |                                   |
|                                   | PBKDF2WithHmacSHA384              |
|                                   |                                   |
|                                   | PBKDF2WithHmacSHA512              |
|                                   |                                   |
|                                   | PBEWithHmacSHA1AndAES\_128        |
|                                   |                                   |
|                                   | PBEWithHmacSHA224AndAES\_128      |
|                                   |                                   |
|                                   | PBEWithHmacSHA256AndAES\_128      |
|                                   |                                   |
|                                   | PBEWithHmacSHA384AndAES\_128      |
|                                   |                                   |
|                                   | PBEWithHmacSHA512AndAES\_128      |
|                                   |                                   |
|                                   | PBEWithHmacSHA1AndAES\_256        |
|                                   |                                   |
|                                   | PBEWithHmacSHA224AndAES\_256      |
|                                   |                                   |
|                                   | PBEWithHmacSHA256AndAES\_256      |
|                                   |                                   |
|                                   | PBEWithHmacSHA384AndAES\_256      |
|                                   |                                   |
|                                   | PBEWithHmacSHA512AndAES\_256      |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

The following table lists cipher transformations available in the SunJCE
provider.

<div class="tblformalwide" id="GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7__GUID-5AB84158-7D99-4604-98EC-1E2F755CCB1C">
Table 4-13 The SunJCE Provider Cipher Transformations

+-----------------------+-----------------------+-----------------------+
| Algorithm Names       | Modes                 | Paddings              |
+:======================+:======================+:======================+
| AES                   | ECB, CBC, PCBC, CTR,  | NoPadding,            |
|                       | CTS,                  | PKCS5Padding,         |
|                       | CFB[^Foot 14^](#GUID- | ISO10126Padding       |
|                       | A47B1249-593C-4C38-A0 |                       |
|                       | D0-68FA7681E0A7__CFBO |                       |
|                       | FBWITHNOSPECIFIEDVALU |                       |
|                       | E-00B67027){#GUID-A47 |                       |
|                       | B1249-593C-4C38-A0D0- |                       |
|                       | 68FA7681E0A7__CFBOFBW |                       |
|                       | ITHNOSPECIFIEDVALUE-0 |                       |
|                       | 0B67027},             |                       |
|                       | CFB8..CFB128,         |                       |
|                       | OFB[^Footref 14^](#fn |                       |
|                       | src_d52441e3699){#fns |                       |
|                       | rc_d52441e3699},      |                       |
|                       | OFB8..OFB128          |                       |
+-----------------------+-----------------------+-----------------------+
| AES                   | GCM                   | NoPadding             |
+-----------------------+-----------------------+-----------------------+
| AESWrap               | ECB                   | NoPadding             |
+-----------------------+-----------------------+-----------------------+
| AESWrap\_128          | ECB                   | NoPadding             |
+-----------------------+-----------------------+-----------------------+
| AESWrap\_192          | ECB                   | NoPadding             |
+-----------------------+-----------------------+-----------------------+
| AESWrap\_256          | ECB                   | NoPadding             |
+-----------------------+-----------------------+-----------------------+
| ARCFOUR               | ECB                   | NoPadding             |
+-----------------------+-----------------------+-----------------------+
| Blowfish, DES,        | ECB, CBC, PCBC, CTR,  | NoPadding,            |
| DESede, RC2           | CTS,                  | PKCS5Padding,         |
|                       | CFB[^Footref 14^](#fn | ISO10126Padding       |
|                       | src_d52441e3751){#fns |                       |
|                       | rc_d52441e3751},      |                       |
|                       | CFB8..CFB64,          |                       |
|                       | OFB[^Footref 14^](#fn |                       |
|                       | src_d52441e3754){#fns |                       |
|                       | rc_d52441e3754},      |                       |
|                       | OFB8..OFB64           |                       |
+-----------------------+-----------------------+-----------------------+
| DESedeWrap            | CBC                   | NoPadding             |
+-----------------------+-----------------------+-----------------------+
| PBEWithMD5AndDES,     | CBC                   | PKCS5Padding          |
| PBEWithMD5AndTripleDE |                       |                       |
| S[^Foot 15^](#GUID-A4 |                       |                       |
| 7B1249-593C-4C38-A0D0 |                       |                       |
| -68FA7681E0A7__PBEWIT |                       |                       |
| HMD5ANDTRIPLEDESISAPR |                       |                       |
| OPRIETAR-127140E8){#G |                       |                       |
| UID-A47B1249-593C-4C3 |                       |                       |
| 8-A0D0-68FA7681E0A7__ |                       |                       |
| PBEWITHMD5ANDTRIPLEDE |                       |                       |
| SISAPROPRIETAR-127140 |                       |                       |
| E8},                  |                       |                       |
| BEWithSHA1AndDESede,  |                       |                       |
| BEWithSHA1AndRC2\_40, |                       |                       |
| BEWithSHA1AndRC2\_128 |                       |                       |
| ,                     |                       |                       |
| BEWithSHA1AndRC4\_40, |                       |                       |
| BEWithSHA1AndRC4\_128 |                       |                       |
| ,                     |                       |                       |
| BEWithHmacSHA1AndAES\ |                       |                       |
| _128,                 |                       |                       |
| BEWithHmacSHA224AndAE |                       |                       |
| S\_128,               |                       |                       |
| BEWithHmacSHA256AndAE |                       |                       |
| S\_128,               |                       |                       |
| BEWithHmacSHA384AndAE |                       |                       |
| S\_128,               |                       |                       |
| BEWithHmacSHA512AndAE |                       |                       |
| S\_128,               |                       |                       |
| BEWithHmacSHA1AndAES\ |                       |                       |
| _256,                 |                       |                       |
| BEWithHmacSHA224AndAE |                       |                       |
| S\_256,               |                       |                       |
| BEWithHmacSHA256AndAE |                       |                       |
| S\_256,               |                       |                       |
| BEWithHmacSHA384AndAE |                       |                       |
| S\_256,               |                       |                       |
| BEWithHmacSHA512AndAE |                       |                       |
| S\_256                |                       |                       |
+-----------------------+-----------------------+-----------------------+
| RSA                   | ECB                   | NoPadding,PKCS1Paddin |
|                       |                       | g,                    |
|                       |                       | AEPPadding,           |
|                       |                       | AEPWithMD5AndMGF1Padd |
|                       |                       | ing,                  |
|                       |                       | AEPWithSHA1AndMGF1Pad |
|                       |                       | ding,                 |
|                       |                       | AEPWithSHA-1AndMGF1Pa |
|                       |                       | dding,                |
|                       |                       | AEPWithSHA-224AndMGF1 |
|                       |                       | Padding,              |
|                       |                       | AEPWithSHA-256AndMGF1 |
|                       |                       | Padding,              |
|                       |                       | AEPWithSHA-384AndMGF1 |
|                       |                       | Padding,              |
|                       |                       | AEPWithSHA-512AndMGF1 |
|                       |                       | Padding               |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

^Footnote 14^ CFB/OFB with no specified value defaults to the block size
of the algorithm. (i.e. AES is 128; Blowfish, DES, DESede, and RC2 are
64.)

^Footnote 15^ PBEWithMD5AndTripleDES is a proprietary algorithm that has
not been standardized.

</div>
<!-- class="section" -->

<div class="section">
Keysize Restrictions

The SunJCE provider uses the following default key sizes (in bits) and
enforces the following restrictions:

<span class="bold">KeyGenerator</span>

<div class="tblformal" id="GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7__GUID-0954AB50-8C28-4173-A9D7-1A76A41F1F02">
Table 4-14 The SunJCE Provider Key Size Restrictions

+-----------------------+-----------------------+-----------------------+
| Algorithm Name        | Default Key size      | Restrictions/Comments |
+:======================+:======================+:======================+
| AES                   | 128                   | Key size must be      |
|                       |                       | equal to 128, 192, or |
|                       |                       | 256.                  |
+-----------------------+-----------------------+-----------------------+
| ARCFOUR (RC4)         | 128                   | Key size must range   |
|                       |                       | between 40 and 1024   |
|                       |                       | (inclusive).          |
+-----------------------+-----------------------+-----------------------+
| Blowfish              | 128                   | Key size must be a    |
|                       |                       | multiple of 8,        |
|                       |                       | ranging from 32 to    |
|                       |                       | 448 (inclusive).      |
+-----------------------+-----------------------+-----------------------+
| DES                   | 56                    | Key size must be      |
|                       |                       | equal to 56.          |
+-----------------------+-----------------------+-----------------------+
| DESede (Triple DES)   | 168                   | Key size must be      |
|                       |                       | equal to 112 or 168.  |
|                       |                       |                       |
|                       |                       | A key size of 112     |
|                       |                       | will generate a       |
|                       |                       | Triple DES key with 2 |
|                       |                       | intermediate keys,    |
|                       |                       | and a key size of 168 |
|                       |                       | will generate a       |
|                       |                       | Triple DES key with 3 |
|                       |                       | intermediate keys.    |
|                       |                       |                       |
|                       |                       | Due to the            |
|                       |                       | \"Meet-In-The-Middle\ |
|                       |                       | "                     |
|                       |                       | problem, even though  |
|                       |                       | 112 or 168 bits of    |
|                       |                       | key material are      |
|                       |                       | used, the             |
|                       |                       | <span class="bold">ef |
|                       |                       | fective</span>        |
|                       |                       | key size is 80 or 112 |
|                       |                       | bits respectively.    |
+-----------------------+-----------------------+-----------------------+
| HmacMD5               | 512                   | No key size           |
|                       |                       | restriction.          |
+-----------------------+-----------------------+-----------------------+
| HmacSHA1              | 512                   | No key size           |
|                       |                       | restriction.          |
+-----------------------+-----------------------+-----------------------+
| HmacSHA224            | 224                   | No key size           |
|                       |                       | restriction.          |
+-----------------------+-----------------------+-----------------------+
| HmacSHA256            | 256                   | No key size           |
|                       |                       | restriction.          |
+-----------------------+-----------------------+-----------------------+
| HmacSHA384            | 384                   | No key size           |
|                       |                       | restriction.          |
+-----------------------+-----------------------+-----------------------+
| HmacSHA512            | 512                   | No key size           |
|                       |                       | restriction.          |
+-----------------------+-----------------------+-----------------------+
| RC2                   | 128                   | Key size must range   |
|                       |                       | between 40 and 1024   |
|                       |                       | (inclusive).          |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

<div class="infoboxnote" id="GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7__GUID-466583F9-CC6C-433B-A710-6D1B14894E47">
Note:

The various Password-Based Encryption (PBE) algorithms use various
algorithms to generate key data, and ultimately depends on the targeted
Cipher algorithm. For example,

"PBEWithMD5AndDES" will always generate 56--bit keys.

</div>
<div class="tblformal" id="GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7__GUID-FF45E2E3-47F7-4696-956C-31CD2902DA38">
Table 4-15 KeyPairGenerator

  Algorithm Name        Default Key size   Restrictions/Comments
  --------------------- ------------------ -------------------------------------------------------------------------------------------------------
  Diffie-Hellman (DH)   2048               Key size must be a multiple of 64, ranging from 512 to 1024, plus 1536, 2048, 3072, 4096, 6144, 8192.

</div>
<!-- class="inftblhruleinformal" -->

<div class="tblformal" id="GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7__GUID-5625E033-160D-4E27-9624-C2567D54032D">
Table 4-16 AlgorithmParameterGenerator

  Algorithm Name        Default Key size   Restrictions/Comments
  --------------------- ------------------ ----------------------------------------------------------------------------------
  Diffie-Hellman (DH)   2048               Key size must be a multiple of 64, ranging from 512 to 1024, plus 2048 and 3072.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-9CAAC18D-CFF0-4602-A1B7-53C9FAA98C9F}

The SunJGSS Provider {#JSSEC-GUID-9CAAC18D-CFF0-4602-A1B7-53C9FAA98C9F .sect2}
--------------------

<div>
The following algorithms are available in the SunJGSS provider:

<div class="section">
<div class="tblformal" id="GUID-9CAAC18D-CFF0-4602-A1B7-53C9FAA98C9F__GUID-E91D0A1B-CA28-45D5-A198-225215137A64">
Table 4-17 The SunJGSS Provider

  OID                               Name
  --------------------------------- -------------
  `1.2.840.113554.1.2.2`{.codeph}   Kerberos v5
  `1.3.6.1.5.5.2`{.codeph}          SPNEGO

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-EB759F08-B8D8-424A-9357-10F9002AE177}

The SunSASL Provider {#JSSEC-GUID-EB759F08-B8D8-424A-9357-10F9002AE177 .sect2}
--------------------

<div>
The following algorithms are available in the `SunSASL`{.codeph}
provider:

<div class="section">
<div class="tblformal" id="GUID-EB759F08-B8D8-424A-9357-10F9002AE177__GUID-A6BA0CF3-8021-49B4-A8DC-A15A2A242B10">
Table 4-18 The SunSASL Provider Algorithm Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Names                   |
+:==================================+:==================================+
| `SaslClient`{.codeph}             | CRAM-MD5                          |
|                                   |                                   |
|                                   | DIGEST-MD5                        |
|                                   |                                   |
|                                   | EXTERNAL                          |
|                                   |                                   |
|                                   | NTLM                              |
|                                   |                                   |
|                                   | PLAIN                             |
+-----------------------------------+-----------------------------------+
| `SaslServer`{.codeph}             | CRAM-MD5                          |
|                                   |                                   |
|                                   | DIGEST-MD5                        |
|                                   |                                   |
|                                   | NTLM                              |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-D09DE3FE-237F-4B7B-A323-0A370137E0F3}

The XMLDSig Provider {#JSSEC-GUID-D09DE3FE-237F-4B7B-A323-0A370137E0F3 .sect2}
--------------------

<div>
The following algorithms are available in the `XMLDSig`{.codeph}
provider:

<div class="section">
<div class="tblformalwide" id="GUID-D09DE3FE-237F-4B7B-A323-0A370137E0F3__GUID-6F042179-8A59-4B17-ABBA-F2D6CF20B6B1">
Table 4-19 The XMLDSig Provider Algorithm Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Names                   |
+:==================================+:==================================+
| `KeyInfoFactory`{.codeph}         | DOM                               |
+-----------------------------------+-----------------------------------+
| `TransformService`{.codeph}       | http://www.w3.org/TR/2001/REC-xml |
|                                   | -c14n-20010315                    |
|                                   | -                                 |
|                                   | <span class="italic">(Canonicaliz |
|                                   | ationMethod.INCLUSIVE)</span>     |
|                                   |                                   |
|                                   | http://www.w3.org/TR/2001/REC-xml |
|                                   | -c14n-20010315\#WithComments      |
|                                   | -                                 |
|                                   | <span class="italic">(Canonicaliz |
|                                   | ationMethod.INCLUSIVE\_WITH\_COMM |
|                                   | ENTS)</span>                      |
|                                   |                                   |
|                                   | http://www.w3.org/2001/10/xml-exc |
|                                   | -c14n\#                           |
|                                   | -                                 |
|                                   | <span class="italic">(Canonicaliz |
|                                   | ationMethod.EXCLUSIVE)</span>     |
|                                   |                                   |
|                                   | http://www.w3.org/2001/10/xml-exc |
|                                   | -c14n\#WithComments               |
|                                   | -                                 |
|                                   | <span class="italic">(Canonicaliz |
|                                   | ationMethod.EXCLUSIVE\_WITH\_COMM |
|                                   | ENTS)</span>                      |
|                                   |                                   |
|                                   | http://www.w3.org/2000/09/xmldsig |
|                                   | \#base64                          |
|                                   | -                                 |
|                                   | <span class="italic">(Transform.B |
|                                   | ASE64)</span>                     |
|                                   |                                   |
|                                   | http://www.w3.org/2000/09/xmldsig |
|                                   | \#enveloped-signature             |
|                                   | -                                 |
|                                   | <span class="italic">(Transform.E |
|                                   | NVELOPED)</span>                  |
|                                   |                                   |
|                                   | http://www.w3.org/TR/1999/REC-xpa |
|                                   | th-19991116                       |
|                                   | -                                 |
|                                   | <span class="italic">(Transform.X |
|                                   | PATH)</span>                      |
|                                   |                                   |
|                                   | http://www.w3.org/2002/06/xmldsig |
|                                   | -filter2                          |
|                                   | -                                 |
|                                   | <span class="italic">(Transform.X |
|                                   | PATH2)</span>                     |
|                                   |                                   |
|                                   | http://www.w3.org/TR/1999/REC-xsl |
|                                   | t-19991116                        |
|                                   | -                                 |
|                                   | <span class="italic">(Transform.X |
|                                   | SLT)</span>                       |
+-----------------------------------+-----------------------------------+
| `XMLSignatureFactory`{.codeph}    | DOM                               |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-DEAD6543-FB59-46F3-B4E7-EE1AFE246EA0}

The SunPCSC Provider {#JSSEC-GUID-DEAD6543-FB59-46F3-B4E7-EE1AFE246EA0 .sect2}
--------------------

<div>
<div class="section">
The SunPCSC provider enables applications to use the [Java Smart Card
I/O
API](https://docs.oracle.com/javase/8/docs/jre/api/security/smartcardio/spec/)
to interact with the PC/SC Smart Card stack of the underlying operating
system. Consult your operating system documentation for details.

On Solaris and Linux platforms, SunPCSC accesses the PC/SC stack via the
`libpcsclite.so`{.codeph} library. It looks for this library in the
directories `/usr/$LIBISA`{.codeph} and `/usr/local/$LIBISA`{.codeph},
where `$LIBISA`{.codeph} is expanded to `lib/64`{.codeph} on 64-bit
Solaris platforms and `lib64`{.codeph} on 64-bit Linux platforms. The
system property `sun.security.smartcardio.library`{.codeph} may also be
set to the full filename of an alternate `libpcsclite.so`{.codeph}
implementation. On Windows platforms, SunPCSC always calls into
`winscard.dll`{.codeph} and no Java-level configuration is necessary or
possible.

If PC/SC is available on the host platform, the SunPCSC implementation
can be obtained via `TerminalFactory.getDefault()`{.codeph} and
`TerminalFactory.getInstance("PC/SC")`{.codeph}. If PC/SC is not
available or not correctly configured, a `getInstance()`{.codeph} call
will fail with a `NoSuchAlgorithmException`{.codeph} and
`getDefault()`{.codeph} will return a JRE built-in implementation that
does not support any terminals.

The following algorithms are available in the `SunPCSC`{.codeph}
provider:

<div class="tblformal" id="GUID-DEAD6543-FB59-46F3-B4E7-EE1AFE246EA0__GUID-349B246C-F05B-4013-90C8-D231F7B817A8">
Table 4-20 The SunPCSC Provider Algorithm Names for Engine Classes

  Engine                       Algorithm Names
  ---------------------------- -----------------
  `TerminalFactory`{.codeph}   PC/SC

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-4F1737D6-1569-4340-B140-678C70E63CD5}

The SunMSCAPI Provider {#JSSEC-GUID-4F1737D6-1569-4340-B140-678C70E63CD5 .sect2}
----------------------

<div>
The SunMSCAPI provider enables applications to use the standard JCA/JCE
APIs to access the native cryptographic libraries, certificates stores
and key containers on the Microsoft Windows platform. The SunMSCAPI
provider itself does not contain cryptographic functionality, it is
simply a conduit between the Java environment and the native
cryptographic services on Windows.

<div class="section">
The following algorithms are available in the `SunMSCAPI`{.codeph}
provider:

<div class="tblformal" id="GUID-4F1737D6-1569-4340-B140-678C70E63CD5__GUID-BD31F123-97D0-4F61-84D4-645461A12C00">
Table 4-21 The SunMSCAPI Algorithm Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Names                   |
+:==================================+:==================================+
| `Cipher`{.codeph}                 | RSA                               |
|                                   | <span class="italic">RSA/ECB/PKCS |
|                                   | 1Padding                          |
|                                   | only</span>                       |
+-----------------------------------+-----------------------------------+
| `KeyPairGenerator`{.codeph}       | RSA                               |
+-----------------------------------+-----------------------------------+
| `KeyStore`{.codeph}               | <span class="bold">Windows-MY</sp |
|                                   | an>                               |
|                                   | : The keystore type that          |
|                                   | identifies the native Microsoft   |
|                                   | Windows MY keystore. It contains  |
|                                   | the user\'s personal certificates |
|                                   | and associated private keys.      |
|                                   |                                   |
|                                   | <span class="bold">Windows-ROOT</ |
|                                   | span>:                            |
|                                   | The keystore type that identifies |
|                                   | the native Microsoft Windows ROOT |
|                                   | keystore. It contains the         |
|                                   | certificates of Root certificate  |
|                                   | authorities and other self-signed |
|                                   | trusted certificates.             |
+-----------------------------------+-----------------------------------+
| `SecureRandom`{.codeph}           | <span class="bold">Windows-PRNG</ |
|                                   | span>                             |
|                                   | : The name of the native          |
|                                   | pseudo-random number generation   |
|                                   | (PRNG) algorithm.                 |
+-----------------------------------+-----------------------------------+
| `Signature`{.codeph}              | MD5withRSA                        |
|                                   |                                   |
|                                   | MD2withRSA                        |
|                                   |                                   |
|                                   | NONEwithRSA                       |
|                                   |                                   |
|                                   | SHA1withRSA                       |
|                                   |                                   |
|                                   | SHA256withRSA                     |
|                                   |                                   |
|                                   | SHA384withRSA                     |
|                                   |                                   |
|                                   | SHA512withRSA                     |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Keysize Restrictions

The SunMSCAPI provider uses the following default keysizes (in bits) and
enforce the following restrictions:

<span class="bold">KeyGenerator</span>

<div class="tblformal" id="GUID-4F1737D6-1569-4340-B140-678C70E63CD5__GUID-75AEA4F7-03AD-4067-A9F2-AF720D93D115">
Table 4-22 The SunMSCAPI Provider Keysize Restrictions

  Alg. Name   Default Keysize   Restrictions/Comments
  ----------- ----------------- -----------------------------------------------------------------------------------------------------------------------------
  RSA         2048              Keysize ranges from 512 bits to 16,384 bits (depending on the underlying Microsoft Windows cryptographic service provider).

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-091BF58C-82AB-4C9C-850F-1660824D5254}

The SunEC Provider {#JSSEC-GUID-091BF58C-82AB-4C9C-850F-1660824D5254 .sect2}
------------------

<div>
The SunEC provider implements Elliptical Curve Cryptography (ECC).
Compared to traditional cryptosystems such as RSA, ECC offers equivalent
security with smaller key sizes, which results in faster computations,
lower power consumption, and memory and bandwidth savings.

<div class="section">
Applications can now use the standard JCA/JCE APIs to access ECC
functionality without the dependency on external ECC libraries (via
SunPKCS11), as was the case in the JDK 6 release.

The following algorithms are available in the `SunEC`{.codeph} provider:

<div class="tblformal" id="GUID-091BF58C-82AB-4C9C-850F-1660824D5254__GUID-5DC56502-18CE-4855-920E-B70C12B74016">
Table 4-23 The SunEC Provider Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Name(s)                 |
+:==================================+:==================================+
| `AlgorithmParameters`{.codeph}    | EC                                |
+-----------------------------------+-----------------------------------+
| `KeyAgreement`{.codeph}           | ECDH                              |
+-----------------------------------+-----------------------------------+
| `KeyFactory`{.codeph}             | EC                                |
+-----------------------------------+-----------------------------------+
| `KeyPairGenerator`{.codeph}       | EC                                |
+-----------------------------------+-----------------------------------+
| `Signature`{.codeph}              | NONEwithECDSA                     |
|                                   |                                   |
|                                   | SHA1withECDSA                     |
|                                   |                                   |
|                                   | SHA224withECDSA                   |
|                                   |                                   |
|                                   | SHA256withECDSA                   |
|                                   |                                   |
|                                   | SHA384withECDSA                   |
|                                   |                                   |
|                                   | SHA512withECDSA                   |
|                                   |                                   |
|                                   | NONEwithECDSAinP1363Format        |
|                                   |                                   |
|                                   | SHA1withECDSAinP1363Format        |
|                                   |                                   |
|                                   | SHA224withECDSAinP1363Format      |
|                                   |                                   |
|                                   | SHA256withECDSAinP1363Format      |
|                                   |                                   |
|                                   | SHA384withECDSAinP1363Format      |
|                                   |                                   |
|                                   | SHA512withECDSAinP1363Format      |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Keysize Restrictions

The SunEC provider uses the following default keysizes (in bits) and
enforces the following restrictions:

<span class="bold">KeyPairGenerator</span>

<div class="tblformal" id="GUID-091BF58C-82AB-4C9C-850F-1660824D5254__GUID-F4C47EF1-0E9B-48CA-B060-91B085ADA199">
Table 4-24 The SunEC Provider Keysize Restrictions

  Alg. Name   Default Keysize   Restrictions/Comments
  ----------- ----------------- -------------------------------------------------
  EC          256               Keysize must range from 112 to 571 (inclusive).

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-B1F2B3F3-F2A4-4FF5-8887-3B3335343B2A}

The OracleUcrypto Provider {#JSSEC-GUID-B1F2B3F3-F2A4-4FF5-8887-3B3335343B2A .sect2}
--------------------------

<div>
The Solaris-only security provider `OracleUcrypto`{.codeph} leverages
the Solaris Ucrypto library to offload and delegate cryptographic
operations supported by the Oracle SPARC T4 based on-core cryptographic
instructions. The `OracleUcrypto`{.codeph} provider itself does not
contain cryptographic functionality; it is simply a conduit between the
Java environment and the Solaris Ucrypto library.

<div class="section">
If the underlying Solaris Ucrypto library does not support a particular
algorithm, then the `OracleUcrypto`{.codeph} provider will not support
it either. Consequently, at runtime, the supported algorithms consists
of the intersection of those that the Solaris Ucrypto library supports
and those that the `OracleUcrypto`{.codeph} provider recognizes.

The following algorithms are available in the `OracleUcrypto`{.codeph}
provider:

<div class="tblformal" id="GUID-B1F2B3F3-F2A4-4FF5-8887-3B3335343B2A__GUID-090F3F16-D42B-4185-9F51-6FC31B75752B">
Table 4-25 The OracleUcrypto Provider Algorithm Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Name(s)                 |
+:==================================+:==================================+
| `Cipher`{.codeph}                 | AES                               |
|                                   |                                   |
|                                   | RSA                               |
|                                   |                                   |
|                                   | AES/ECB/NoPadding                 |
|                                   |                                   |
|                                   | AES/ECB/PKCS5Padding              |
|                                   |                                   |
|                                   | AES/CBC/NoPadding                 |
|                                   |                                   |
|                                   | AES/CBC/PKCS5Padding              |
|                                   |                                   |
|                                   | AES/CTR/NoPadding                 |
|                                   |                                   |
|                                   | AES/GCM/NoPadding                 |
|                                   |                                   |
|                                   | AES/CFB128/NoPadding              |
|                                   |                                   |
|                                   | AES/CFB128/PKCS5Padding           |
|                                   |                                   |
|                                   | AES\_128/ECB/NoPadding            |
|                                   |                                   |
|                                   | AES\_192/ECB/NoPadding            |
|                                   |                                   |
|                                   | AES\_256/ECB/NoPadding            |
|                                   |                                   |
|                                   | AES\_128/CBC/NoPadding            |
|                                   |                                   |
|                                   | AES\_192/CBC/NoPadding            |
|                                   |                                   |
|                                   | AES\_256/CBC/NoPadding            |
|                                   |                                   |
|                                   | AES\_128/GCM/NoPadding            |
|                                   |                                   |
|                                   | AES\_192/GCM/NoPadding            |
|                                   |                                   |
|                                   | AES\_256/GCM/NoPadding            |
|                                   |                                   |
|                                   | RSA/ECB/PKCS1Padding              |
|                                   |                                   |
|                                   | RSA/ECB/NoPadding                 |
+-----------------------------------+-----------------------------------+
| `Signature`{.codeph}              | MD5withRSA                        |
|                                   |                                   |
|                                   | SHA1withRSA                       |
|                                   |                                   |
|                                   | SHA256withRSA                     |
|                                   |                                   |
|                                   | SHA384withRSA                     |
|                                   |                                   |
|                                   | SHA512withRSA                     |
+-----------------------------------+-----------------------------------+
| `MessageDigest`{.codeph}          | MD5                               |
|                                   |                                   |
|                                   | SHA                               |
|                                   |                                   |
|                                   | SHA-224                           |
|                                   |                                   |
|                                   | SHA-256                           |
|                                   |                                   |
|                                   | SHA-384                           |
|                                   |                                   |
|                                   | SHA-512                           |
|                                   |                                   |
|                                   | SHA3--224                         |
|                                   |                                   |
|                                   | SHA3--256                         |
|                                   |                                   |
|                                   | SHA3--384                         |
|                                   |                                   |
|                                   | SHA3--512                         |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Keysize Restrictions

The `OracleUcrypto`{.codeph} provider does not specify any default
keysizes or keysize restrictions; these are specified by the underlying
Solaris Ucrypto library.

</div>
<!-- class="section" -->

<div class="section">
OracleUcrypto Provider Configuration File

<div class="p">
The `OracleUcrypto`{.codeph} provider has a configuration file named
`ucrypto-solaris.cfg`{.codeph} that resides in the
`$JAVA_HOME/conf/security`{.codeph} directory. Modify this configuration
file to specify which algorithms to disable by default. For example, the
following configuration file disables AES with CFB128 mode by default:

``` {.codeblock dir="ltr"}
#
# Configuration file for the OracleUcrypto provider
#
disabledServices = {
  Cipher.AES/CFB128/PKCS5Padding
  Cipher.AES/CFB128/NoPadding
}
```

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-3185649A-C316-45F2-A70E-2B3FF6BDC34F}

The Apple Provider {#JSSEC-GUID-3185649A-C316-45F2-A70E-2B3FF6BDC34F .sect2}
------------------

<div>
The `Apple`{.codeph} provider implements a
`java.security.KeyStore`{.codeph} that provides access to the macOS
Keychain.

<div class="section">
The following algorithms are available in the `Apple`{.codeph} provider:

<div class="tblformal" id="GUID-3185649A-C316-45F2-A70E-2B3FF6BDC34F__GUID-E9F859FE-70A6-4665-A7C7-34ECDD0A193C">
Table 4-26 The Apple Provider Algorithm Name for Engine Classes

  Engine                Algorithm Name(s)
  --------------------- -------------------
  `KeyStore`{.codeph}   KeychainStore

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-67D4652C-2551-4BBE-9941-50A9348AEA84}

The JdkLDAP Provider {#JSSEC-GUID-67D4652C-2551-4BBE-9941-50A9348AEA84 .sect2}
--------------------

<div>
The JdkLDAP provider was introduced in JDK 9 as a replacement for the
LDAP CertStore implementation in the SUN provider.

<div class="section">
The following algorithms are available in the `JdkLDAP`{.codeph}
provider:

<div class="tblformal" id="GUID-67D4652C-2551-4BBE-9941-50A9348AEA84__GUID-44F15A48-44CB-4160-957D-5CAC7AA7CA74">
Table 4-27 The JdkLDAP Provider Algorithm Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Names                   |
+:==================================+:==================================+
| `CertStore`{.codeph}              | LDAP                              |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-D08B5350-6653-4FC6-B350-2B009A9E7FD6}

The JdkSASL Provider {#JSSEC-GUID-D08B5350-6653-4FC6-B350-2B009A9E7FD6 .sect2}
--------------------

<div>
The following algorithms are available in the `JdkSASL`{.codeph}
provider:

<div class="section">
<div class="tblformal" id="GUID-D08B5350-6653-4FC6-B350-2B009A9E7FD6__GUID-A6BA0CF3-8021-49B4-A8DC-A15A2A242B10">
Table 4-28 The JdkSASL Provider Algorithm Names for Engine Classes

+-----------------------------------+-----------------------------------+
| Engine                            | Algorithm Names                   |
+:==================================+:==================================+
| `SaslClient`{.codeph}             | GSSAPI                            |
+-----------------------------------+-----------------------------------+
| `SaslServer`{.codeph}             | GSSAPI                            |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

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
| --- ---------------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| ------ --            | l | dcommon/gifs/toc.gif |
|           [![Previou | e | )\                   |
| s](../../dcommon/gif | L |             <span cl |
| s/leftnav.gif)\      | o | ass="icon">Contents< |
|               [![Nex | g | /span>](toc.htm)     |
| t](../../dcommon/gif | o |   -- --------------- |
| s/rightnav.gif)\     | ] | -------------------- |
|                      | ( | -------------------- |
|    <span class="icon | . | ---                  |
| ">Previous</span>](h | . |                      |
| owtoimplaprovider.ht | / |                      |
| m)   <span class="ic | . |                      |
| on">Next</span>](pkc | . |                      |
| s11-reference-guide1 | / |                      |
| .htm)                | d |                      |
|   ------------------ | c |                      |
| -------------------- | o |                      |
| -------------------- | m |                      |
| --- ---------------- | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| ------ --            | / |                      |
|                      | g |                      |
|                      | i |                      |
|                      | f |                      |
|                      | s |                      |
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
