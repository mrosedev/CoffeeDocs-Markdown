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

  ----------------------------------------------------------- ------------------------------------------------------------------------------------------ --
         [![Previous](../../dcommon/gifs/leftnav.gif)\                                [![Next](../../dcommon/gifs/rightnav.gif)\                         
   <span class="icon">Previous</span>](oracle-providers.htm)   <span class="icon">Next</span>](java-authentication-and-authorization-service-jaas1.htm)  
  ----------------------------------------------------------- ------------------------------------------------------------------------------------------ --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-30E98B63-4910-40A1-A6DD-663EAF466991}<!-- End Header -->

<span class="enumeration_chapter">5 </span>PKCS\#11 Reference Guide {#JSSEC-GUID-30E98B63-4910-40A1-A6DD-663EAF466991 .sect1}
===================================================================

<div>
The Java platform defines a set of programming interfaces for performing
cryptographic operations. These interfaces are collectively known as the
Java Cryptography Architecture (JCA) and the Java Cryptography Extension
(JCE). See [Java Cryptography Architecture (JCA) Reference
Guide](java-cryptography-architecture-jca-reference-guide.htm#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.").

The cryptographic interfaces are provider-based. Specifically,
applications talk to Application Programming Interfaces (APIs), and the
actual cryptographic operations are performed in configured providers
which adhere to a set of Service Provider Interfaces (SPIs). This
architecture supports different provider implementations. Some providers
may perform cryptographic operations in software; others may perform the
operations on a hardware token (for example, on a smartcard device or on
a hardware cryptographic accelerator).

The Cryptographic Token Interface Standard, PKCS\#11, is produced by RSA
Security and defines native programming interfaces to cryptographic
tokens, such as hardware cryptographic accelerators and smartcards.
Existing applications that use the JCA and JCE APIs can access native
PKCS\#11 tokens with the PKCS\#11 provider. No modifications to the
application are required. The only requirement is to properly configure
the provider.

Although an application can make use of most PKCS\#11 features using
existing APIs, some applications might need more flexibility and
capabilities. For example, an application might want to deal with
smartcards being removed and inserted dynamically more easily. Or, a
PKCS\#11 token might require authentication for some non-key-related
operations and therefore, the application must be able to log into the
token without using keystore. The JCA gives applications greater
flexibility in dealing with different providers.

This document describes how native PKCS\#11 tokens can be configured
into the Java platform for use by Java applications. It also describes
how the JCA makes it easier for applications to deal with different
types of providers, including PKCS\#11 providers.

</div>
<div class="sect2">
[]{#GUID-6DA72F34-6C6A-4F7D-ADBA-5811576A9331}

SunPKCS11 Provider {#JSSEC-GUID-6DA72F34-6C6A-4F7D-ADBA-5811576A9331 .sect2}
------------------

<div>
The SunPKCS11 provider, in contrast to most other providers, does not
implement cryptographic algorithms itself. Instead, it acts as a bridge
between the Java JCA and JCE APIs and the native PKCS\#11 cryptographic
API, translating the calls and conventions between the two.

This means that Java applications calling standard JCA and JCE APIs can,
without modification, take advantage of algorithms offered by the
underlying PKCS\#11 implementations, such as, for example,

-   Cryptographic smartcards,
-   Hardware cryptographic accelerators, and
-   High performance software implementations.

<div class="infoboxnote" id="GUID-6DA72F34-6C6A-4F7D-ADBA-5811576A9331__GUID-1DBACA0C-33DE-436F-B9B1-18D9AD105863">
Note:

Java SE only facilitates accessing native PKCS\#11 implementations, it
does not itself include a native PKCS\#11 implementation. However,
cryptographic devices such as Smartcards and hardware accelerators often
come with software that includes a PKCS\#11 implementation, which you
need to install and configure according to manufacturer\'s instructions.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-97F1E537-CB59-4C7F-AB6B-05D4DBD69AC0}

SunPKCS11 Requirements {#JSSEC-GUID-97F1E537-CB59-4C7F-AB6B-05D4DBD69AC0 .sect2}
----------------------

<div>
The SunPKCS11 provider requires an implementation of PKCS\#11 v2.20 or
later to be installed on the system. This implementation must take the
form of a shared-object library (`.so` on Solaris and Linux) or
dynamic-link library (`.dll` on Windows). Please consult your vendor
documentation to find out if your cryptographic device includes such a
PKCS\#11 implementation, how to configure it, and what the name of the
library file is.

The SunPKCS11 provider supports a number of algorithms, provided that
the underlying PKCS\#11 implementation offers them. The algorithms and
their corresponding PKCS\#11 mechanisms are listed in the table in
[SunPKCS11 Provider Supported
Algorithms](pkcs11-reference-guide1.htm#GUID-D3EF9023-7DDC-435D-9186-D2FD05674777).

</div>
</div>
<div class="sect2">
[]{#GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9}

SunPKCS11 Configuration {#JSSEC-GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9 .sect2}
-----------------------

<div>
<div class="section">
The SunPKCS11 provider is in the module
<span class="apiname">jdk.crypto.cryptoki</span>. To use the provider,
you must first install it statically or programmatically.

To install the provider statically, add the provider to the Java
security properties file
(`java-home/conf/security/java.security`{.codeph}).

For example, here\'s a fragment of the `java.security`{.codeph} file
that installs the SunPKCS11 provider with the configuration file
`/opt/bar/cfg/pkcs11.cfg`{.codeph}.

``` {.oac_no_warn dir="ltr"}
# configuration for security providers 1-12 omitted
security.provider.13=SunPKCS11 /opt/bar/cfg/pkcs11.cfg
```

To install the provider dynamically, create an instance of the provider
with the appropriate configuration filename and then install it. Here is
an example.

``` {.oac_no_warn dir="ltr"}
    String configName = "/opt/bar/cfg/pkcs11.cfg";
    Provider p = Security.getProvider("SunPKCS11");
    p = p.configure(configName);
    Security.addProvider(p);
```

<div class="infoboxnote" id="GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9__GUID-160774D2-1740-4A7B-9C74-E82383614A0E">
Note:

Save the returned <span class="apiname">Provider</span> object from the
<span class="apiname">configure</span> method, then add that object, as
demonstrated in this example:

``` {.oac_no_warn dir="ltr"}
    p = p.configure(configName);
    Security.addProvider(p);
```

Don\'t add the provider from which you called the
<span class="apiname">configure</span> method:

``` {.oac_no_warn dir="ltr"}
    p.configure(configName);
    Security.addProvider(p);
```

If this provider cannot be configured in-place, then a new provider is
created and returned. Therefore, always use the provider returned from
the <span class="apiname">configure</span> method.

</div>
To use more than one slot per PKCS\#11 implementation, or to use more
than one PKCS\#11 implementation, simply repeat the installation for
each with the appropriate configuration file. This will result in a
SunPKCS11 provider instance for each slot of each PKCS\#11
implementation.

The configuration file is a text file that contains entries in the
following format:

`attribute=value`{.codeph}

The valid values for <span class="variable">attribute</span> and
<span class="variable">value</span> are described in the table in this
section:

The two mandatory attributes are `name`{.codeph} and `library`{.codeph}.

Here is a sample configuration file:

``` {.oac_no_warn dir="ltr"}
name = FooAccelerator
library = /opt/foo/lib/libpkcs11.so
```

Comments are denoted by lines starting with the `#`{.codeph} (number)
symbol.

<div class="tblformal" id="GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9__GUID-8ADD17FD-3320-4D8F-A1ED-319DFEABA338">
Table 5-1 Attributes in the PKCS\#11 Provider Configuration File

+-----------------------+-----------------------+-----------------------+
| Attribute             | Value                 | Description           |
+:======================+:======================+:======================+
| library               | Pathname of PKCS\#11  | This is the full      |
|                       | implementation        | pathname (including   |
|                       |                       | extension) of the     |
|                       |                       | PKCS\#11              |
|                       |                       | implementation; the   |
|                       |                       | format of the         |
|                       |                       | pathname is platform  |
|                       |                       | dependent. For        |
|                       |                       | example,              |
|                       |                       | `/opt/foo/lib/libpkcs |
|                       |                       | 11.so`{.codeph}       |
|                       |                       | might be the pathname |
|                       |                       | of a PKCS\#11         |
|                       |                       | implementation on     |
|                       |                       | Solaris and Linux     |
|                       |                       | while                 |
|                       |                       | `C:\foo\mypkcs11.dll` |
|                       |                       | {.codeph}             |
|                       |                       | might be the pathname |
|                       |                       | on Windows.           |
+-----------------------+-----------------------+-----------------------+
| name                  | Name suffix of this   | This string is        |
|                       | provider instance     | concatenated with the |
|                       |                       | prefix                |
|                       |                       | `SunPKCS11-`{.codeph} |
|                       |                       | to produce this       |
|                       |                       | provider instance\'s  |
|                       |                       | name (that is, the    |
|                       |                       | string returned by    |
|                       |                       | its                   |
|                       |                       | `Provider.getName()`{ |
|                       |                       | .codeph}              |
|                       |                       | method). For example, |
|                       |                       | if the                |
|                       |                       | `name`{.codeph}       |
|                       |                       | attribute is          |
|                       |                       | `"FooAccelerator"`{.c |
|                       |                       | odeph},               |
|                       |                       | then the provider     |
|                       |                       | instance\'s name will |
|                       |                       | be                    |
|                       |                       | `"SunPKCS11-FooAccele |
|                       |                       | rator"`{.codeph}.     |
+-----------------------+-----------------------+-----------------------+
| description           | Description of this   | This string will be   |
|                       | provider instance     | returned by the       |
|                       |                       | provider instance\'s  |
|                       |                       | `Provider.getInfo()`{ |
|                       |                       | .codeph}              |
|                       |                       | method. If none is    |
|                       |                       | specified, a default  |
|                       |                       | description will be   |
|                       |                       | returned.             |
+-----------------------+-----------------------+-----------------------+
| slot                  | Slot id               | This is the id of the |
|                       |                       | slot that this        |
|                       |                       | provider instance is  |
|                       |                       | to be associated      |
|                       |                       | with. For example,    |
|                       |                       | you would use         |
|                       |                       | `1`{.codeph} for the  |
|                       |                       | slot with the id      |
|                       |                       | `1`{.codeph} under    |
|                       |                       | PKCS\#11. At most one |
|                       |                       | of `slot`{.codeph} or |
|                       |                       | `slotListIndex`{.code |
|                       |                       | ph}                   |
|                       |                       | may be specified. If  |
|                       |                       | neither is specified, |
|                       |                       | the default is a      |
|                       |                       | `slotListIndex`{.code |
|                       |                       | ph}                   |
|                       |                       | of `0`{.codeph}.      |
+-----------------------+-----------------------+-----------------------+
| slotListIndex         | Slot index            | This is the slot      |
|                       |                       | index that this       |
|                       |                       | provider instance is  |
|                       |                       | to be associated      |
|                       |                       | with. It is the index |
|                       |                       | into the list of all  |
|                       |                       | slots returned by the |
|                       |                       | PKCS\#11 function     |
|                       |                       | `C_GetSlotList`{.code |
|                       |                       | ph}.                  |
|                       |                       | For example,          |
|                       |                       | `0`{.codeph}          |
|                       |                       | indicates the first   |
|                       |                       | slot in the list. At  |
|                       |                       | most one of           |
|                       |                       | `slot`{.codeph} or    |
|                       |                       | `slotListIndex`{.code |
|                       |                       | ph}                   |
|                       |                       | may be specified. If  |
|                       |                       | neither is specified, |
|                       |                       | the default is a      |
|                       |                       | `slotListIndex`{.code |
|                       |                       | ph}                   |
|                       |                       | of `0`{.codeph}.      |
+-----------------------+-----------------------+-----------------------+
| enabledMechanisms     | Brace enclosed,       | This is the list      |
|                       | whitespace-separated  | PKCS\#11 mechanisms   |
|                       | list of PKCS\#11      | that this provider    |
|                       | mechanisms to enable  | instance should use,  |
|                       |                       | provided that they    |
|                       |                       | are supported by both |
|                       |                       | the SunPKCS11         |
|                       |                       | provider and PKCS\#11 |
|                       |                       | token. All other      |
|                       |                       | mechanisms will be    |
|                       |                       | ignored. Each entry   |
|                       |                       | in the list is the    |
|                       |                       | name of a PKCS\#11    |
|                       |                       | mechanism. Here is an |
|                       |                       | example that lists    |
|                       |                       | two PKCS\#11          |
|                       |                       | mechanisms.           |
|                       |                       |                       |
|                       |                       | ``` {.oac_no_warn dir |
|                       |                       | ="ltr"}               |
|                       |                       | enabledMechanisms = { |
|                       |                       |   CKM_RSA_PKCS        |
|                       |                       |   CKM_RSA_PKCS_KEY_PA |
|                       |                       | IR_GEN                |
|                       |                       | }                     |
|                       |                       | ```                   |
|                       |                       |                       |
|                       |                       | At most one of        |
|                       |                       | `enabledMechanisms`{. |
|                       |                       | codeph}               |
|                       |                       | or                    |
|                       |                       | `disabledMechanisms`{ |
|                       |                       | .codeph}              |
|                       |                       | may be specified. If  |
|                       |                       | neither is specified, |
|                       |                       | the mechanisms        |
|                       |                       | enabled are those     |
|                       |                       | that are supported by |
|                       |                       | both the SunPKCS11    |
|                       |                       | provider (see         |
|                       |                       | [SunPKCS11 Provider   |
|                       |                       | Supported             |
|                       |                       | Algorithms](pkcs11-re |
|                       |                       | ference-guide1.htm#GU |
|                       |                       | ID-D3EF9023-7DDC-435D |
|                       |                       | -9186-D2FD05674777))  |
|                       |                       | and the PKCS\#11      |
|                       |                       | token.                |
+-----------------------+-----------------------+-----------------------+
| disabledMechanisms    | Brace enclosed,       | This is the list of   |
|                       | whitespace-separated  | PKCS\#11 mechanisms   |
|                       | list of PKCS\#11      | that this provider    |
|                       | mechanisms to disable | instance should       |
|                       |                       | ignore. Any mechanism |
|                       |                       | listed will be        |
|                       |                       | ignored by the        |
|                       |                       | provider, even if     |
|                       |                       | they are supported by |
|                       |                       | the token and the     |
|                       |                       | SunPKCS11 provider.   |
|                       |                       | The strings           |
|                       |                       | `SecureRandom`{.codep |
|                       |                       | h}                    |
|                       |                       | and                   |
|                       |                       | `KeyStore`{.codeph}   |
|                       |                       | may be specified to   |
|                       |                       | disable those         |
|                       |                       | services.             |
|                       |                       |                       |
|                       |                       | At most one of        |
|                       |                       | `enabledMechanisms`{. |
|                       |                       | codeph}               |
|                       |                       | or                    |
|                       |                       | `disabledMechanisms`{ |
|                       |                       | .codeph}              |
|                       |                       | may be specified. If  |
|                       |                       | neither is specified, |
|                       |                       | the mechanisms        |
|                       |                       | enabled are those     |
|                       |                       | that are supported by |
|                       |                       | both the SunPKCS11    |
|                       |                       | provider (see         |
|                       |                       | [SunPKCS11 Provider   |
|                       |                       | Supported             |
|                       |                       | Algorithms](pkcs11-re |
|                       |                       | ference-guide1.htm#GU |
|                       |                       | ID-D3EF9023-7DDC-435D |
|                       |                       | -9186-D2FD05674777))  |
|                       |                       | and the PKCS\#11      |
|                       |                       | token.                |
+-----------------------+-----------------------+-----------------------+
| attributes            | See below             | The                   |
|                       |                       | `attributes`{.codeph} |
|                       |                       | option can be used to |
|                       |                       | specify additional    |
|                       |                       | PKCS\#11 that should  |
|                       |                       | be set when creating  |
|                       |                       | PKCS\#11 key objects. |
|                       |                       | This makes it         |
|                       |                       | possible to           |
|                       |                       | accommodate tokens    |
|                       |                       | that require          |
|                       |                       | particular            |
|                       |                       | attributes. For       |
|                       |                       | details, see the      |
|                       |                       | section below.        |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Attributes Configuration

The attributes option allows you to specify additional PKCS\#11
attributes that should be set when creating PKCS\#11 key objects. By
default, the SunPKCS11 provider only specifies mandatory PKCS\#11
attributes when creating objects. For example, for RSA public keys it
specifies the key type and algorithm (CKA\_CLASS and CKA\_KEY\_TYPE) and
the key values for RSA public keys (CKA\_MODULUS and
CKA\_PUBLIC\_EXPONENT). The PKCS\#11 library you are using will assign
implementation specific default values to the other attributes of an RSA
public key, for example that the key can be used to encrypt and verify
messages (CKA\_ENCRYPT and CKA\_VERIFY = true).

The `attributes`{.codeph} option can be used if you do not like the
default values your PKCS\#11 implementation assigns or if your PKCS\#11
implementation does not support defaults and requires a value to be
specified explicitly. Note that specifying attributes that your PKCS\#11
implementation does not support or that are invalid for the type of key
in question may cause the operation to fail at runtime.

The option can be specified zero or more times, the options are
processed in the order specified in the configuration file as described
below. The `attributes`{.codeph} option has the format:

``` {.oac_no_warn dir="ltr"}
attributes(operation, keytype, keyalgorithm) = {
  name1 = value1
  [...]
}
```

Valid values for `operation`{.codeph} are:

-   `generate`{.codeph}, for keys generated via a
    <span class="apiname">KeyPairGenerator</span> or
    <span class="apiname">KeyGenerator</span>
-   `import`{.codeph}, for keys created via a
    <span class="apiname">KeyFactory</span> or
    <span class="apiname">SecretKeyFactory</span>. This also applies to
    Java software keys automatically converted to PKCS\#11 key objects
    when they are passed to the initialization method of a cryptographic
    operation, for example `Signature.initSign()`{.codeph}.
-   `*`{.codeph}, for keys created using either a generate or a create
    operation.

Valid values for `keytype`{.codeph} are `CKO_PUBLIC_KEY`{.codeph},
`CKO_PRIVATE_KEY`{.codeph}, and `CKO_SECRET_KEY`{.codeph}, for public,
private, and secret keys, respectively, and `*`{.codeph} to match any
type of key.

Valid values for `keyalgorithm`{.codeph} are one of the
`CKK_xxx`{.codeph} constants from the PKCS\#11 specification, or
`*`{.codeph} to match keys of any algorithm. The algorithms currently
supported by the SunPKCS11 provider include CKK\_RSA, CKK\_DSA, CKK\_DH,
CKK\_AES, CKK\_DES, CKK\_DES3, CKK\_RC4, CKK\_BLOWFISH,
CKK\_GENERIC\_SECRET, and CKK\_EC.

The attribute names and values are specified as a list of one or more
name-value pairs. `name`{.codeph} must be a `CKA_xxx`{.codeph} constant
from the PKCS\#11 specification, for example `CKA_SENSITIVE`{.codeph}.
`value`{.codeph} can be one of the following:

-   A boolean value, `true`{.codeph} or `false`{.codeph}
-   An integer, in decimal form (default) or in hexadecimal form if it
    begins with `0x`{.codeph}.
-   `null`{.codeph}, indicating that this attribute should
    <span class="italic">not</span> be specified when creating objects.

If the `attributes`{.codeph} option is specified multiple times, the
entries are processed in the order specified with the attributes
aggregated and later attributes overriding earlier ones. For example,
consider the following configuration file excerpt:

``` {.oac_no_warn dir="ltr"}
attributes(*,CKO_PRIVATE_KEY,*) = {
  CKA_SIGN = true
}

attributes(*,CKO_PRIVATE_KEY,CKK_DH) = {
  CKA_SIGN = null
}

attributes(*,CKO_PRIVATE_KEY,CKK_RSA) = {
  CKA_DECRYPT = true
}
```

The first entry says to specify `CKA_SIGN = true`{.codeph} for all
private keys. The second option overrides that with `null`{.codeph} for
Diffie-Hellman private keys, so the `CKA_SIGN`{.codeph} attribute will
not specified for them at all. Finally, the third option says to also
specify `CKA_DECRYPT = true`{.codeph} for RSA private keys. That means
RSA private keys will have both `CKA_SIGN = true`{.codeph} and
`CKA_DECRYPT = true`{.codeph} set.

There is also a special form of the `attributes`{.codeph} option. You
can write `attributes = compatibility`{.codeph} in the configuration
file. That is a shortcut for a whole set of attribute statements. They
are designed to provider maximum compatibility with existing Java
applications, which may expect, for example, all key components to be
accessible and secret keys to be usable for both encryption and
decryption. The `compatibility`{.codeph} attributes line can be used
together with other `attributes`{.codeph} lines, in which case the same
aggregation and overriding rules apply as described earlier.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-85EA1017-E59C-49B9-9207-65B7B2BF171E}

Accessing Network Security Services (NSS) {#JSSEC-GUID-85EA1017-E59C-49B9-9207-65B7B2BF171E .sect2}
-----------------------------------------

<div>
<div class="section">
[Network Security Services
(NSS)](http://www.mozilla.org/projects/security/pki/nss/) is a set of
open source security libraries whose crypto APIs are based on PKCS\#11
but it includes special features that are outside of the PKCS\#11
standard. The SunPKCS11 provider includes code to interact with these
NSS specific features, including several NSS specific configuration
directives, which are described below.

For best results, we recommend that you use the latest version of NSS
available. It should be at least version 3.12.

The SunPKCS11 provider uses NSS specific code when any of the
`nss`{.codeph} configuration directives described below are used. In
that case, the regular configuration commands `library`{.codeph},
`slot`{.codeph}, and `slotListIndex`{.codeph} cannot be used.

<div class="tblformal" id="GUID-85EA1017-E59C-49B9-9207-65B7B2BF171E__GUID-D7866EA0-8645-4F13-A702-7502BCDFC51F">
Table 5-2 NSS Attributes and Values

+-----------------------+-----------------------+-----------------------+
| Attribute             | Value                 | Description           |
+:======================+:======================+:======================+
| nssLibraryDirectory   | directory containing  | This is the full      |
|                       | the NSS and NSPR      | pathname of the       |
|                       | libraries             | directory containing  |
|                       |                       | the NSS and           |
|                       |                       | [NSPR](http://www.moz |
|                       |                       | illa.org/projects/nsp |
|                       |                       | r/)                   |
|                       |                       | libraries. It must be |
|                       |                       | specified unless NSS  |
|                       |                       | has already been      |
|                       |                       | loaded and            |
|                       |                       | initialized by        |
|                       |                       | another component     |
|                       |                       | running in the same   |
|                       |                       | process as the Java   |
|                       |                       | VM.                   |
|                       |                       |                       |
|                       |                       | Depending on your     |
|                       |                       | platform, you may     |
|                       |                       | have to set           |
|                       |                       | `LD_LIBRARY_PATH`{.co |
|                       |                       | deph}                 |
|                       |                       | or `PATH`{.codeph}    |
|                       |                       | (on Windows) to       |
|                       |                       | include this          |
|                       |                       | directory in order to |
|                       |                       | allow the operating   |
|                       |                       | system to locate the  |
|                       |                       | dependent libraries.  |
+-----------------------+-----------------------+-----------------------+
| nssSecmodDirectory    | directory containing  | The full pathname of  |
|                       | the NSS DB files      | the directory         |
|                       |                       | containing the NSS    |
|                       |                       | configuration and key |
|                       |                       | information           |
|                       |                       | (`secmod.db`{.codeph} |
|                       |                       | ,                     |
|                       |                       | `key3.db`{.codeph},   |
|                       |                       | and                   |
|                       |                       | `cert8.db`{.codeph}). |
|                       |                       | This directive must   |
|                       |                       | be specified unless   |
|                       |                       | NSS has already been  |
|                       |                       | initialized by        |
|                       |                       | another component     |
|                       |                       | (see above) or NSS is |
|                       |                       | used without database |
|                       |                       | files as described    |
|                       |                       | below.                |
+-----------------------+-----------------------+-----------------------+
| nssDbMode             | one of                | This directives       |
|                       | `readWrite`{.codeph}, | determines how the    |
|                       | `readOnly`{.codeph},  | NSS database is       |
|                       | and `noDb`{.codeph}   | accessed. In          |
|                       |                       | read-write mode, full |
|                       |                       | access is possible    |
|                       |                       | but only one process  |
|                       |                       | at a time should be   |
|                       |                       | accessing the         |
|                       |                       | databases. Read-only  |
|                       |                       | mode disallows        |
|                       |                       | modifications to the  |
|                       |                       | files.                |
|                       |                       |                       |
|                       |                       | The noDb mode allows  |
|                       |                       | NSS to be used        |
|                       |                       | without database      |
|                       |                       | files purely as a     |
|                       |                       | cryptographic         |
|                       |                       | provider. It is not   |
|                       |                       | possible to create    |
|                       |                       | persistent keys using |
|                       |                       | the PKCS11 KeyStore.  |
+-----------------------+-----------------------+-----------------------+
| nssModule             | one of                | NSS makes its         |
|                       | `keystore`{.codeph},  | functionality         |
|                       | `crypto`{.codeph},    | available using       |
|                       | `fips`{.codeph}, and  | several different     |
|                       | `trustanchors`{.codep | libraries and slots.  |
|                       | h}                    | This directive        |
|                       |                       | determines which of   |
|                       |                       | these modules is      |
|                       |                       | accessed by this      |
|                       |                       | instance of           |
|                       |                       | SunPKCS11.            |
|                       |                       |                       |
|                       |                       | The `crypto`{.codeph} |
|                       |                       | module is the default |
|                       |                       | in `noDb`{.codeph}    |
|                       |                       | mode. It supports     |
|                       |                       | crypto operations     |
|                       |                       | without login but no  |
|                       |                       | persistent keys.      |
|                       |                       |                       |
|                       |                       | The `fips`{.codeph}   |
|                       |                       | module is the default |
|                       |                       | if the NSS            |
|                       |                       | `secmod.db`{.codeph}  |
|                       |                       | has been set to       |
|                       |                       | FIPS-140 compliant    |
|                       |                       | mode. In this mode,   |
|                       |                       | NSS restricts the     |
|                       |                       | available algorithms  |
|                       |                       | and the PKCS\#11      |
|                       |                       | attributes with which |
|                       |                       | keys can be created.  |
|                       |                       |                       |
|                       |                       | The                   |
|                       |                       | `keystore`{.codeph}   |
|                       |                       | module is the default |
|                       |                       | in other              |
|                       |                       | configurations. It    |
|                       |                       | supports persistent   |
|                       |                       | keys using the PKCS11 |
|                       |                       | KeyStore, which are   |
|                       |                       | stored in the NSS DB  |
|                       |                       | files. This module    |
|                       |                       | requires login.       |
|                       |                       |                       |
|                       |                       | The                   |
|                       |                       | `trustanchors`{.codep |
|                       |                       | h}                    |
|                       |                       | module enables access |
|                       |                       | to NSS trust anchor   |
|                       |                       | certificates via the  |
|                       |                       | PKCS11 KeyStore, if   |
|                       |                       | `secmod.db`{.codeph}  |
|                       |                       | has been configured   |
|                       |                       | to include the trust  |
|                       |                       | anchor library.       |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="example" id="GUID-85EA1017-E59C-49B9-9207-65B7B2BF171E__GUID-98F50D8E-A21A-4749-A540-DEDA7DD5ED9E">
Example 5-1 SunPKCS11 Configuration Files for NSS

NSS as a pure cryptography provider

``` {.oac_no_warn dir="ltr"}
name = NSScrypto
nssLibraryDirectory = /opt/tests/nss/lib
nssDbMode = noDb
attributes = compatibility
```

NSS as a FIPS 140 compliant crypto token

``` {.oac_no_warn dir="ltr"}
name = NSSfips
nssLibraryDirectory = /opt/tests/nss/lib
nssSecmodDirectory = /opt/tests/nss/fipsdb
nssModule = fips
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect2">
[]{#GUID-7989F8B4-7260-4908-8203-99056B2D060E}

Troubleshooting PKCS\#11 {#JSSEC-GUID-7989F8B4-7260-4908-8203-99056B2D060E .sect2}
------------------------

<div>
<div class="section">
There could be issues with PKCS\#11 which requires debugging. To show
debug info about Library, Slots, Token, and Mechanism, add
`showInfo=true`{.codeph} in the SunPKCS11 provider configuration file,
which is `<java-home>/conf/security/sunpkcs11-solaris.cfg` or the
configuration file that you specified statically or dynamically as
described in [SunPKCS11
Configuration](pkcs11-reference-guide1.htm#GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9).

For additional debugging info, users can start or restart the Java
processes with one of the following options:

-   For general SunPKCS11 provider debugging info:

    `-Djava.security.debug=sunpkcs11`{.codeph}

-   For PKCS\#11 keystore specific debugging info:

    `-Djava.security.debug=pkcs11keystore`{.codeph}

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-F068B4E6-8FAD-4443-9269-7DF13573C8DF}

Disabling PKCS\#11 Providers and/or Individual PKCS\#11 Mechanisms {#JSSEC-GUID-F068B4E6-8FAD-4443-9269-7DF13573C8DF .sect2}
------------------------------------------------------------------

<div>
As part of the troubleshooting process, it could be helpful to
temporarily disable a PKCS\#11 provider or the specific mechanism of a
given provider.

<div class="section">
Please note that disabling a PKCS\#11 provider, is only a temporary
measure. By disabling the PKCS\#11 provider, the provider is no longer
available which can cause applications to break or have a performance
impact. Once the issue has been identified, only that specific mechanism
should remain disabled.

</div>
<!-- class="section" -->

<div class="section">
Disabling PKCS\#11 Providers

A PKCS\#11 provider can be disabled by using one of the following
methods:

1.  Disable PKCS\#11 for a single Java process. Start or restart the
    Java process with the following Java command line flag:

    `-Dsun.security.pkcs11.enable-solaris=false`{.codeph}

    <div class="infoboxnote" id="GUID-F068B4E6-8FAD-4443-9269-7DF13573C8DF__GUID-2A2DD2C2-41EC-44C6-A37F-9D52ED1BF951">
    Note:

    This step is only applicable to the SunPKCS11 provider when backed
    by the default Solaris PKCS\#11 provider file
    (`<java_home>/conf/security/sunpkcs11-solaris.cfg`).

    </div>
2.  Disable PKCS\#11 for all Java processes run with a particular Java
    installation: This can be done dynamically by using the API (not
    shown in this section) or statically by editing the
    `<java_home>/conf/security/java.security`{.codeph} file and
    commenting out the SunPKCS11 security provider (do not forget to
    re-number the order of providers, if necessary) as shown below.

    <div class="p">
    ``` {.oac_no_warn dir="ltr"}
    #
    # List of providers and their preference orders (see above):
    #
    security.provider.1=SUN
    security.provider.2=SunRsaSign
    security.provider.3=SunEC
    security.provider.4=SunJSSE
    security.provider.5=SunJCE
    security.provider.6=SunJGSS
    security.provider.7=SunSASL
    security.provider.8=XMLDSig
    security.provider.9=SunPCSC
    security.provider.10=JdkLDAP
    security.provider.11=JdkSASL
    security.provider.12=SunMSCAPI
    #security.provider.13=SunPKCS11
    ```

    </div>
    Start or restart the Java processes being run on this installation
    of Java.

</div>
<!-- class="section" -->

<div class="section" id="GUID-F068B4E6-8FAD-4443-9269-7DF13573C8DF__GUID-6D397DE0-3339-426C-ABA8-A0B079DB8A5A">
Disabling Specific Mechanisms

When an issue occurs in one of the mechanisms of PKCS\#11, it can be
resolved by disabling only that particular mechanism, rather than the
entire PKCS\#11 provider (do not forget to re-enable the PKCS\#11
provider if it was disabled earlier).

<div class="infoboxnote" id="GUID-F068B4E6-8FAD-4443-9269-7DF13573C8DF__GUID-2DFCFB11-76BD-46E8-9FE1-0033BBF66714">
Note:

To disable the PKCS\#11 SecureRandom implementation only, you can add
<span class="apiname">SecureRandom</span> to the list of disabled
mechanisms in the `<java-home>/conf/security/sunpkcs11-solaris.cfg`
file:

``` {.oac_no_warn dir="ltr"}
name = Solaris

description = SunPKCS11 accessing Solaris Cryptographic Framework

library = /usr/lib/$ISA/libpkcs11.so

handleStartupErrors = ignoreAll

# Use the X9.63 encoding for EC points (do not wrap in an ASN.1 OctetString).
useEcX963Encoding = true

attributes = compatibility

disabledMechanisms = {
  CKM_DSA_KEY_PAIR_GEN
  SecureRandom
}
```

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-4C366313-33B9-458C-A845-33D0C8A9C367}

Application Developers {#JSSEC-GUID-4C366313-33B9-458C-A845-33D0C8A9C367 .sect2}
----------------------

<div>
Java applications can use the existing JCA and JCE APIs to access
PKCS\#11 tokens through the SunPKCS11 provider.

</div>
<div class="sect3">
[]{#GUID-6E8B2F3C-792F-4512-9BB3-234C440ADC46}

### Token Login {#JSSEC-GUID-6E8B2F3C-792F-4512-9BB3-234C440ADC46 .sect3}

<div>
You can login to the keystore using a Personal Identification Number and
perform PKCS\#11 operations.

Certain PKCS\#11 operations, such as accessing private keys, require a
login using a Personal Identification Number, or PIN, before the
operations can proceed. The most common type of operations that require
login are those that deal with keys on the token. In a Java application,
such operations often involve first loading the keystore. When accessing
the PKCS\#11 token as a keystore via the
`java.security.KeyStore`{.codeph} class, you can supply the PIN in the
password input parameter to the
[`load`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/KeyStore.html#load-java.io.InputStream-char:A-)
method. The PIN will then be used by the SunPKCS11 provider for logging
into the token. Here is an example.

``` {.oac_no_warn dir="ltr"}
    char[] pin = ...; 
    KeyStore ks = KeyStore.getInstance("PKCS11");
    ks.load(null, pin); 
```

This is fine for an application that treats PKCS\#11 tokens as static
keystores. For an application that wants to accommodate PKCS\#11 tokens
more dynamically, such as smartcards being inserted and removed, you can
use the new `KeyStore.Builder`{.codeph} class. Here is an example of how
to initialize the builder for a PKCS\#11 keystore with a callback
handler.

``` {.oac_no_warn dir="ltr"}
    KeyStore.CallbackHandlerProtection chp =
        new KeyStore.CallbackHandlerProtection(new MyGuiCallbackHandler());
    KeyStore.Builder builder =
        KeyStore.Builder.newInstance("PKCS11", null, chp);
```

For the SunPKCS11 provider, the callback handler must be able to satisfy
a `PasswordCallback`{.codeph}, which is used to prompt the user for the
PIN. Whenever the application needs access to the keystore, it uses the
builder as follows.

``` {.oac_no_warn dir="ltr"}
    KeyStore ks = builder.getKeyStore();
    Key key = ks.getKey(alias, null);
```

The builder will prompt for a password as needed using the previously
configured callback handler. The builder will prompt for a password only
for the initial access. If the user of the application continues using
the same Smartcard, the user will not be prompted again. If the user
removes and inserts a different smartcard, the builder will prompt for a
password for the new card.

Depending on the PKCS\#11 token, there may be non-key-related operations
that also require token login. Applications that use such operations can
use the
[<span class="apiname">java.security.AuthProvider</span>](https://docs.oracle.com/javase/10/docs/api/java/security/AuthProvider.html)
class. The `AuthProvider`{.codeph} class extends from
`java.security.Provider`{.codeph} and defines methods to perform login
and logout operations on a provider, as well as to set a callback
handler for the provider to use.

For the SunPKCS11 provider, the callback handler must be able to satisfy
a `PasswordCallback`{.codeph}, which is used to prompt the user for the
PIN.

Here is an example of how an application might use an
`AuthProvider`{.codeph} to log into the token. (Note that you must
configure the SunPKCS11 provider before using it.)

``` {.oac_no_warn dir="ltr"}
    Provider p = Security.getProvider("SunPKCS11");
    AuthProvider aprov = (AuthProvider)p.configure(<provider configuration file>);
    aprov.login(subject, new MyGuiCallbackHandler());
```

</div>
</div>
<div class="sect3">
[]{#GUID-508B5E3B-BF39-4E02-A1BD-523352D3AA12}

### Token Keys {#JSSEC-GUID-508B5E3B-BF39-4E02-A1BD-523352D3AA12 .sect3}

<div>
Java `Key`{.codeph} objects may or may not contain actual key material.

-   A software <span class="apiname">Key</span> object does contain the
    actual key material and allows access to that material.
-   An unextractable key on a secure token (such as a smartcard) is
    represented by a Java <span class="apiname">Key</span> object that
    does not contain the actual key material. The
    <span class="apiname">Key</span> object only contains a reference to
    the actual key.

Applications and providers must use the correct interfaces to represent
these different types of <span class="apiname">Key</span> objects.
Software <span class="apiname">Key</span> objects (or any
<span class="apiname">Key</span> object that has access to the actual
key material) should implement the interfaces in the
[<span class="apiname">java.security.interfaces</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/package-summary.html)
and
[<span class="apiname">javax.crypto.interfaces</span>](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/package-summary.html)
packages (such as `DSAPrivateKey`{.codeph}). Key objects representing
unextractable token keys should only implement the relevant generic
interfaces in the
[<span class="apiname">java.security</span>](https://docs.oracle.com/javase/10/docs/api/java/security/package-summary.html)
and
[<span class="apiname">javax.crypto</span>](https://docs.oracle.com/javase/10/docs/api/javax/crypto/package-summary.html)
packages (`PrivateKey`{.codeph}, `PublicKey`{.codeph}, or
`SecretKey`{.codeph}). Identification of the algorithm of a key should
be performed using the `Key.getAlgorithm()`{.codeph} method.

Note that a <span class="apiname">Key</span> object for an unextractable
token key can only be used by the provider associated with that token.

</div>
</div>
<div class="sect3">
[]{#GUID-99785B51-50D8-458E-AA2C-755749F1E39E}

### Delayed Provider Selection {#JSSEC-GUID-99785B51-50D8-458E-AA2C-755749F1E39E .sect3}

<div>
Java cryptography `getInstance()`{.codeph} methods, such as
`Cipher.getInstance("AES")`{.codeph}, return the implementation from the
first provider that implemented the requested algorithm. However, the
JDK delays the selection of the provider until the relevant
initialization method is called. The initialization method accepts a
`Key`{.codeph} object and can determine at that point which provider can
accept the specified `Key`{.codeph} object. This ensures that the
selected provider can use the specified `Key`{.codeph} object. (If an
application attempts to use a `Key`{.codeph} object for an unextractable
token key with a provider that only accepts software key objects, then
the provider throws an `InvalidKeyException`{.codeph}. This is an issue
for the `Cipher`{.codeph}, `KeyAgreement`{.codeph}, `Mac`{.codeph}, and
`Signature`{.codeph} classes.) The following represents the affected
initialization methods.

-   `Cipher`{.codeph}</a>.init(\..., Key key, \...)</code>
-   `KeyAgreement`{.codeph}</a>.init(Key key, \...)</code>
-   `Mac`{.codeph}</a>.init(Key key, \...)</code>
-   `Signature`{.codeph}</a>.initSign(PrivateKey privateKey)</code>

Furthermore, if an application calls the initialization method multiple
times (each time with a different key, for example), the proper provider
for the given key is selected each time. In other words, a different
provider may be selected for each initialization call.

Although this delayed provider selection is hidden from the application,
it does affect the behavior of the `getProvider()`{.codeph} method for
`Cipher`{.codeph}, `KeyAgreement`{.codeph}, `Mac`{.codeph}, and
`Signature`{.codeph}. If `getProvider()`{.codeph} is called
<span class="variable">before</span> the initialization operation has
occurred (and therefore before provider selection has occurred), then
the first provider that supports the requested algorithm is returned.
This may not be the same provider as the one selected
<span class="italic">after</span> the initialization method is called.
If `getProvider()`{.codeph} is called
<span class="variable">after</span> the initialization operation has
occurred, then the actual selected provider is returned. It is
recommended that applications only call `getProvider()`{.codeph} after
they have called the relevant initialization method.

In addition to `getProvider()`{.codeph}, the following additional
methods are similarly affected.

-   `Cipher.getBlockSize`{.codeph}
-   `Cipher.getExcemptionMechanism`{.codeph}
-   `Cipher.getIV`{.codeph}
-   `Cipher.getOutputSize`{.codeph}
-   `Cipher.getParameters`{.codeph}
-   `Mac.getMacLength`{.codeph}
-   `Signature.getParameters`{.codeph}
-   `Signature.setParameter`{.codeph}

</div>
</div>
<div class="sect3">
[]{#GUID-60672551-8FF7-4BE1-AF28-CA0C81706B1C}

### JAAS KeyStoreLoginModule {#JSSEC-GUID-60672551-8FF7-4BE1-AF28-CA0C81706B1C .sect3}

<div>
The JDK comes with a JAAS keystore login module,
[<span class="apiname">KeyStoreLoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/KeyStoreLoginModule.html),
that allows an application to authenticate using its identity in a
specified keystore. After authentication, the application would acquire
its principal and credentials information (certificate and private key)
from the keystore. By using this login module and configuring it to use
a PKCS\#11 token as a keystore, the application can acquire this
information from a PKCS\#11 token.

Use the following options to configure the
`KeyStoreLoginModule`{.codeph} to use a PKCS\#11 token as the keystore.

-   `keyStoreURL="NONE"`{.codeph}
-   `keyStoreType="PKCS11"`{.codeph}
-   `keyStorePasswordURL=some_pin_url`{.codeph}

where

[<!-- -->]{#GUID-60672551-8FF7-4BE1-AF28-CA0C81706B1C__GUID-D778A65D-C000-44CD-B164-2B4745AA4289}<span class="variable">some\_pin\_url</span>

:   The location of the PIN. If the `keyStorePasswordURL`{.codeph}
    option is omitted, then the login module will get the PIN via the
    application\'s callback handler, supplying it with a
    `PasswordCallback`{.codeph} . Here is an example of a configuration
    file that uses a PKCS\#11 token as a keystore.

    ``` {.oac_no_warn dir="ltr"}
    other {
        com.sun.security.auth.module.KeyStoreLoginModule required
            keyStoreURL="NONE"
      keyStoreType="PKCS11"
      keyStorePasswordURL="file:/home/joe/scpin";
    };
    ```

If more than one SunPKCS11 provider has been configured dynamically or
in the `java.security`{.codeph} security properties file, you can use
the `keyStoreProvider`{.codeph} option to target a specific provider
instance. The argument to this option is the name of the provider. For
the SunPKCS11 provider, the provider name is of the form
`SunPKCS11-TokenName`{.codeph}, where `TokenName`{.codeph} is the name
suffix that the provider instance has been configured with, as detailed
in the [Table
5-1](pkcs11-reference-guide1.htm#GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9__GUID-8ADD17FD-3320-4D8F-A1ED-319DFEABA338 "PKCS#11 provider configuration file attributes.").
For example, the following configuration file names the PKCS\#11
provider instance with name suffix `SmartCard`{.codeph}.

``` {.oac_no_warn dir="ltr"}
other {
    com.sun.security.auth.module.KeyStoreLoginModule required
        keyStoreURL="NONE"
  keyStoreType="PKCS11"
  keyStorePasswordURL="file:/home/joe/scpin"
  keyStoreProvider="SunPKCS11-SmartCard";
};
```

Some PKCS\#11 tokens support login via a protected authentication path.
For example, a smartcard may have a dedicated PIN-pad to enter the pin.
Biometric devices will also have their own means to obtain
authentication information. If the PKCS\#11 token has a protected
authentication path, then use the `protected=true`{.codeph} option and
omit the `keyStorePasswordURL`{.codeph} option. Here is an example of a
configuration file for such a token.

``` {.oac_no_warn dir="ltr"}
other {
    com.sun.security.auth.module.KeyStoreLoginModule required
        keyStoreURL="NONE"
  keyStoreType="PKCS11"
  protected=true;
};
```

</div>
</div>
<div class="sect3">
[]{#GUID-CE29BCBA-4C87-4DA0-B170-328E579200BD}

### Tokens as JSSE Keystore and Trust Stores {#JSSEC-GUID-CE29BCBA-4C87-4DA0-B170-328E579200BD .sect3}

<div>
To use PKCS\#11 tokens as JSSE keystores or trust stores, the JSSE
application can use the APIs described in [Token
Login](pkcs11-reference-guide1.htm#GUID-6E8B2F3C-792F-4512-9BB3-234C440ADC46 "You can login to the keystore using a Personal Identification Number and perform PKCS#11 operations.")
to instantiate a <span class="apiname">KeyStore</span> that is backed by
a PKCS\#11 token and pass it to its key manager and trust manager. The
JSSE application will then have access to the keys on the token.

JSSE also supports configuring the use of keystores and trust stores via
system properties, as described in the [Java Secure Socket Extension
(JSSE) Reference
Guide](java-secure-socket-extension-jsse-reference-guide.htm#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345 "The Java Secure Socket Extension (JSSE) enables secure Internet communications. It provides a framework and an implementation for a Java version of the SSL, TLS, and DTLS protocols and includes functionality for data encryption, server authentication, message integrity, and optional client authentication.").
To use a PKCS\#11 token as a keystore or trust store, set the
`javax.net.ssl.keyStoreType`{.codeph} and
`javax.net.ssl.trustStoreType`{.codeph} system properties, respectively,
to \"PKCS11\", and set the `javax.net.ssl.keyStore`{.codeph} and
`javax.net.ssl.trustStore`{.codeph} system properties, respectively, to
`NONE`{.codeph}. To specify the use of a specific provider instance, use
the `javax.net.ssl.keyStoreProvider`{.codeph} and
`javax.net.ssl.trustStoreProvider`{.codeph} system properties (for
example, \"SunPKCS11-SmartCard\").

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-05DE5039-C62A-42B9-8F8E-DB6DB1B0CD44}

Using keytool and jarsigner with PKCS\#11 Tokens {#JSSEC-GUID-05DE5039-C62A-42B9-8F8E-DB6DB1B0CD44 .sect2}
------------------------------------------------

<div>
If the SunPKCS11 provider has been configured in the
`java.security`{.codeph} security properties file (located in the
`$JAVA_HOME/conf/security`{.codeph} directory of the Java runtime), then
keytool and jarsigner can be used to operate on the PKCS\#11 token by
specifying the following options.

<div class="p">
-   `-keystore NONE`{.codeph}
-   `-storetype PKCS11`{.codeph}

Here an example of a command to list the contents of the configured
PKCS\#11 token.

</div>
<div class="p">
``` {.oac_no_warn dir="ltr"}
keytool -keystore NONE -storetype PKCS11 -list
```

The PIN can be specified using the `-storepass`{.codeph} option. If none
has been specified, then `keytool`{.codeph} and `jarsigner`{.codeph}
will prompt for the token PIN. If the token has a protected
authentication path (such as a dedicated PIN-pad or a biometric reader),
then the `-protected`{.codeph} option must be specified, and no password
options can be specified.

</div>
If more than one SunPKCS11 provider has been configured in the
`java.security`{.codeph} security properties file, you can use the
`-providerName`{.codeph} option to target a specific provider instance.
The argument to this option is the name of the provider.

-   `-providerName providerName`{.codeph}

For the SunPKCS11 provider, `providerName`{.codeph} is of the form
`SunPKCS11-TokenName`{.codeph} where:

[<!-- -->]{#GUID-05DE5039-C62A-42B9-8F8E-DB6DB1B0CD44__GUID-486DE0FD-CA9D-401F-96D2-44FDB25B6FC3}<span class="variable">TokenName</span>

:   The name suffix that the provider instance has been configured with,
    as detailed in [Table
    5-1](pkcs11-reference-guide1.htm#GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9__GUID-8ADD17FD-3320-4D8F-A1ED-319DFEABA338 "PKCS#11 provider configuration file attributes.").
    For example, the following command lists the contents of the
    PKCS\#11 keystore provider instance with name suffix
    `SmartCard`{.codeph}.

    ``` {.oac_no_warn dir="ltr"}
    keytool -keystore NONE -storetype PKCS11 \
            -providerName SunPKCS11-SmartCard \
            -list
    ```

    If the SunPKCS11 provider has not been configured in the
    `java.security`{.codeph} security properties file, you can use the
    following options to instruct `keytool`{.codeph} and
    `jarsigner`{.codeph} to install the provider dynamically.

    -   `-providerClass sun.security.pkcs11.SunPKCS11`{.codeph}
    -   `-providerArg ConfigFilePath`{.codeph}

[<!-- -->]{#GUID-05DE5039-C62A-42B9-8F8E-DB6DB1B0CD44__GUID-BA567174-BE55-43B8-AE0B-F5564824E458}<span class="variable">ConfigFilePath</span>

:   <div class="p">
    The path to the token configuration file. Here is an example of a
    command to list a PKCS\#11 keystore when the SunPKCS11 provider has
    not been configured in the `java.security`{.codeph} file.

    ``` {.oac_no_warn dir="ltr"}
    keytool -keystore NONE -storetype PKCS11 \
            -providerClass sun.security.pkcs11.SunPKCS11 \
            -providerArg /foo/bar/token.config \
            -list
    ```

    </div>

</div>
</div>
<div class="sect2">
[]{#GUID-F8D31D74-8D4D-4981-BC63-05ABED100AB8}

Policy Tool {#JSSEC-GUID-F8D31D74-8D4D-4981-BC63-05ABED100AB8 .sect2}
-----------

<div>
<div class="infoboxnote" id="GUID-F8D31D74-8D4D-4981-BC63-05ABED100AB8__GUID-73BDA382-76B1-4F3C-8A13-CEB4B86B48F7">
Note:

The Policy Tool is deprecated in JDK 9.

</div>
The `keystore`{.codeph} entry in the default policy implementation has
the following syntax, which accommodates a PIN and multiple PKCS\#11
provider instances:

``` {.oac_no_warn dir="ltr"}
keystore "some_keystore_url", "keystore_type", "keystore_provider";
keystorePasswordURL "some_password_url";
```

Where

[<!-- -->]{#GUID-F8D31D74-8D4D-4981-BC63-05ABED100AB8__GUID-DCD1833C-101D-4568-A7DC-4E8F1F18ED67}<span class="variable">keystore\_provider</span>
:   The keystore provider name (for example,
    `"SunPKCS11-SmartCard"`{.codeph}).

[<!-- -->]{#GUID-F8D31D74-8D4D-4981-BC63-05ABED100AB8__GUID-8F5B3FF4-863B-4EA5-B16B-4454B035C54E}<span class="variable">some\_password\_url</span> 
:   A URL pointing to the location of the token PIN. Both
    <span class="variable">keystore\_provider</span> and the
    <span class="variable">keystorePasswordURL</span> line are optional.
    If <span class="variable">keystore\_provider</span> has not been
    specified, then the first configured provider that supports the
    specified keystore type is used. If the
    `keystorePasswordURL`{.codeph} line has not been specified, then no
    password is used.

<div class="example" id="GUID-F8D31D74-8D4D-4981-BC63-05ABED100AB8__GUID-466262E0-C186-4808-828D-FB8CEFDE1076">
Example 5-2 Keystore Policy Entry for a PKCS\#11 Token

The following is an example keystore policy entry for a PKCS\#11 token:

``` {.oac_no_warn dir="ltr"}
keystore "NONE", "PKCS11", "SunPKCS11-SmartCard";
keystorePasswordURL "file:/foo/bar/passwordFile";
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect2">
[]{#GUID-2216C9EC-5F64-424C-BA35-E7DDEDC61C53}

Provider Developers {#JSSEC-GUID-2216C9EC-5F64-424C-BA35-E7DDEDC61C53 .sect2}
-------------------

<div>
The `java.security.Provider`{.codeph} class enables provider developers
to more easily support PKCS\#11 tokens and cryptographic services
through provider services and parameter support.

See [Example
Provider](pkcs11-reference-guide1.htm#GUID-50C137F1-F23B-434D-AA90-5A744ABA2F5B "The following is an example of a simple provider that demonstrates features of the Provider class.")
for an example of a simple provider designed to demonstrate provider
services and parameter support.

</div>
<div class="sect3">
[]{#GUID-BDF21F95-43FA-462F-A89C-5DF20760440E}

### Provider Services {#JSSEC-GUID-BDF21F95-43FA-462F-A89C-5DF20760440E .sect3}

<div>
<div class="section">
For each service implemented by the provider, there must be a property
whose name is the type of service (`Cipher`{.codeph},
`Signature`{.codeph}, etc), followed by a period and the name of the
algorithm to which the service applies. The property value must specify
the fully qualified name of the class implementing the service. Here is
an example of a provider setting `KeyAgreement.DiffieHellman`{.codeph}
property to have the value
`com.sun.crypto.provider.DHKeyAgreement`{.codeph}.

``` {.oac_no_warn dir="ltr"}
put("KeyAgreement.DiffieHellman", "com.sun.crypto.provider.DHKeyAgreement")
```

The public static nested class
[<span class="apiname">Provider.Service</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Provider.Service.html)
encapsulates the properties of a provider service (including its type,
attributes, algorithm name, and algorithm aliases). Providers can
instantiate `Provider.Service`{.codeph} objects and register them by
calling the `Provider.putService()`{.codeph} method. This is equivalent
to creating a `Property`{.codeph} entry and calling the
`Provider.put()`{.codeph} method. Note that legacy `Property`{.codeph}
entries registered via `Provider.put`{.codeph} are still supported.

Here is an example of a provider creating a `Service`{.codeph} object
with the `KeyAgreement`{.codeph} type, for the `DiffieHellman`{.codeph}
algorithm, implemented by the class
`com.sun.crypto.provider.DHKeyAgreement`{.codeph}.

``` {.oac_no_warn dir="ltr"}
Service s = new Service(this, "KeyAgreement", "DiffieHellman",
    "com.sun.crypto.provider.DHKeyAgreement", null, null);
putService(s);
```

Using `Provider.Service`{.codeph} objects instead of legacy
`Property`{.codeph} entries has a couple of major benefits. One benefit
is that it allows the provider to have greater flexibility when
[Instantiating Engine
Classes](pkcs11-reference-guide1.htm#GUID-BDF21F95-43FA-462F-A89C-5DF20760440E__INSTANTIATINGENGINECLASSES-F41C69E1).
Another benefit is that it allows the provider to test [Parameter
Support](pkcs11-reference-guide1.htm#GUID-BDF21F95-43FA-462F-A89C-5DF20760440E__PARAMETERSUPPORT-57310DC1).
These features are discussed in detail next.

</div>
<!-- class="section" -->

<div class="section" id="GUID-BDF21F95-43FA-462F-A89C-5DF20760440E__INSTANTIATINGENGINECLASSES-F41C69E1">
Instantiating Engine Classes

By default, the Java Cryptography framework looks up the provider
property for a particular service and directly instantiates the engine
class registered for that property. A provider can to override this
behavior and instantiate the engine class for the requested service
itself.

To override the default behavior, the provider overrides the
`Provider.Service.newInstance()`{.codeph} method to add its custom
behavior. For example, the provider might call a custom constructor, or
might perform initialization using information not accessible outside
the provider (or that are only known by the provider).

</div>
<!-- class="section" -->

<div class="section" id="GUID-BDF21F95-43FA-462F-A89C-5DF20760440E__PARAMETERSUPPORT-57310DC1">
Parameter Support

The Java Cryptography framework may attempt a fast check to determine
whether a provider\'s service implementation can use an
application-specified parameter. To perform this fast check, the
framework calls `Provider.Service.supportsParameter()`{.codeph}.

The framework relies on this fast test during delayed provider selection
(see [Delayed Provider
Selection](pkcs11-reference-guide1.htm#GUID-99785B51-50D8-458E-AA2C-755749F1E39E)).
When an application invokes an initialization method and passes it a
`Key`{.codeph} object, the framework asks an underlying provider whether
it supports the object by calling its
`Service.supportsParameter()`{.codeph} method. If
`supportsParameter()`{.codeph} returns `false`{.codeph}, the framework
can immediately remove that provider from consideration. If
`supportsParameter()`{.codeph} returns `true`{.codeph}, the framework
passes the `Key`{.codeph} object to that provider\'s initialization
engine class implementation. A provider that requires software
`Key`{.codeph} objects should override this method to return
`false`{.codeph} when it is passed non-software keys. Likewise, a
provider for a PKCS\#11 token that contains unextractable keys should
only return `true`{.codeph} for `Key`{.codeph} objects that it created,
and which therefore correspond to the keys on its respective token.

<div class="infoboxnote" id="GUID-BDF21F95-43FA-462F-A89C-5DF20760440E__THEDEFAULTIMPLEMENTATIONOFSUPPORTSP-1E7A1649">
Note:

The default implementation of `supportsParameter()`{.codeph} returns
`true`{.codeph}. This allows existing providers to work without
modification. However, because of this lenient default implementation,
the framework must be prepared to catch exceptions thrown by providers
that reject the `Key`{.codeph} object inside their initialization engine
class implementations. The framework treats these cases the same as when
`supportsParameter()`{.codeph} returns `false`{.codeph}.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-AD009675-E028-4A86-BE87-8DBD03B538DC}

### Parameter Support {#JSSEC-GUID-AD009675-E028-4A86-BE87-8DBD03B538DC .sect3}

<div>
The Java Cryptography framework may attempt a fast check to determine
whether a provider\'s service implementation can use an
application-specified parameter. To perform this fast check, the
framework calls `Provider.Service.supportsParameter()`{.codeph}.

The framework relies on this fast test during delayed provider selection
(see [Delayed Provider
Selection](pkcs11-reference-guide1.htm#GUID-99785B51-50D8-458E-AA2C-755749F1E39E)).
When an application invokes an initialization method and passes it a
`Key`{.codeph} object, the framework asks an underlying provider whether
it supports the object by calling its
`Service.supportsParameter()`{.codeph} method. If
`supportsParameter()`{.codeph} returns `false`{.codeph}, the framework
can immediately remove that provider from consideration. If
`supportsParameter()`{.codeph} returns `true`{.codeph}, the framework
passes the `Key`{.codeph} object to that provider\'s initialization
engine class implementation. A provider that requires software
`Key`{.codeph} objects should override this method to return
`false`{.codeph} when it is passed non-software keys. Likewise, a
provider for a PKCS\#11 token that contains unextractable keys should
only return `true`{.codeph} for `Key`{.codeph} objects that it created,
and which therefore correspond to the keys on its respective token.

<div class="infoboxnote" id="GUID-AD009675-E028-4A86-BE87-8DBD03B538DC__GUID-019F1138-29BE-43FA-91DC-42CAED7D7ACF">
Note:

The default implementation of `supportsParameter()`{.codeph} returns
`true`{.codeph}. This allows existing providers to work without
modification. However, because of this lenient default implementation,
the framework must be prepared to catch exceptions thrown by providers
that reject the `Key`{.codeph} object inside their initialization engine
class implementations. The framework treats these cases the same as when
`supportsParameter()`{.codeph} returns `false`{.codeph}.

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-D3EF9023-7DDC-435D-9186-D2FD05674777}

SunPKCS11 Provider Supported Algorithms {#JSSEC-GUID-D3EF9023-7DDC-435D-9186-D2FD05674777 .sect2}
---------------------------------------

<div>
<div class="section">
[Table
5-3](pkcs11-reference-guide1.htm#GUID-D3EF9023-7DDC-435D-9186-D2FD05674777__GUID-21B92E76-EE33-47EA-BC0C-F428AF662C02 "List of Java Algorithms supported by the Sun PKCS#11 Provider.")
lists the Java algorithms supported by the SunPKCS11 provider and
corresponding PKCS\#11 mechanisms needed to support them. When multiple
mechanisms are listed, they are given in the order of preference and any
one of them is sufficient.

<div class="infoboxnote" id="GUID-D3EF9023-7DDC-435D-9186-D2FD05674777__GUID-E2C635BE-FFB1-4E12-90F3-5679264E9219">
Note:

SunPKCS11 can be instructed to ignore mechanisms by using the
`disabledMechanisms`{.codeph} and `enabledMechanisms`{.codeph}
configuration directives (see [SunPKCS11
Configuration](pkcs11-reference-guide1.htm#GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9)).

</div>
For Elliptic Curve mechanisms, the SunPKCS11 provider will only use keys
that use the `namedCurve`{.codeph} choice as encoding for the parameters
and only allow the uncompressed point format. The SunPKCS11 provider
assumes that a token supports all standard named domain parameters.

<div class="tblformal" id="GUID-D3EF9023-7DDC-435D-9186-D2FD05674777__GUID-21B92E76-EE33-47EA-BC0C-F428AF662C02">
Table 5-3 Java Algorithms Supported by the SunPKCS11 Provider

  Java Algorithm                     PKCS\#11 Mechanisms
  ---------------------------------- ----------------------------------------------------------
  Signature.MD2withRSA               CKM\_MD2\_RSA\_PKCS, CKM\_RSA\_PKCS, CKM\_RSA\_X\_509
  Signature.MD5withRSA               CKM\_MD5\_RSA\_PKCS, CKM\_RSA\_PKCS, CKM\_RSA\_X\_509
  Signature.SHA1withRSA              CKM\_SHA1\_RSA\_PKCS, CKM\_RSA\_PKCS, CKM\_RSA\_X\_509
  Signature.SHA224withRSA            CKM\_SHA224\_RSA\_PKCS, CKM\_RSA\_PKCS, CKM\_RSA\_X\_509
  Signature.SHA256withRSA            CKM\_SHA256\_RSA\_PKCS, CKM\_RSA\_PKCS, CKM\_RSA\_X\_509
  Signature.SHA384withRSA            CKM\_SHA384\_RSA\_PKCS, CKM\_RSA\_PKCS, CKM\_RSA\_X\_509
  Signature.SHA512withRSA            CKM\_SHA512\_RSA\_PKCS, CKM\_RSA\_PKCS, CKM\_RSA\_X\_509
  Signature.SHA1withDSA              CKM\_DSA\_SHA1, CKM\_DSA
  Signature.NONEwithDSA              CKM\_DSA
  Signature.SHA1withECDSA            CKM\_ECDSA\_SHA1, CKM\_ECDSA
  Signature.SHA224withECDSA          CKM\_ECDSA
  Signature.SHA256withECDSA          CKM\_ECDSA
  Signature.SHA384withECDSA          CKM\_ECDSA
  Signature.SHA512withECDSA          CKM\_ECDSA
  Signature.NONEwithECDSA            CKM\_ECDSA
  Cipher.RSA/ECB/NoPadding           CKM\_RSA\_X\_509
  Cipher.RSA/ECB/PKCS1Padding        CKM\_RSA\_PKCS
  Cipher.ARCFOUR                     CKM\_RC4
  Cipher.DES/CBC/NoPadding           CKM\_DES\_CBC
  Cipher.DES/CBC/PKCS5Padding        CKM\_DES\_CBC\_PAD, CKM\_DES\_CBC
  Cipher.DES/ECB/NoPadding           CKM\_DES\_ECB
  Cipher.DES/ECB/PKCS5Padding        CKM\_DES\_ECB
  Cipher.DESede/CBC/NoPadding        CKM\_DES3\_CBC
  Cipher.DESede/CBC/PKCS5Padding     CKM\_DES3\_CBC\_PAD, CKM\_DES3\_CBC
  Cipher.DESede/ECB/NoPadding        CKM\_DES3\_ECB
  Cipher.DESede/ECB/PKCS5Padding     CKM\_DES3\_ECB
  Cipher.AES/CBC/NoPadding           CKM\_AES\_CBC
  Cipher.AES/CBC/PKCS5Padding        CKM\_AES\_CBC\_PAD, CKM\_AES\_CBC
  Cipher.Blowfish/CBC/NoPadding      CKM\_BLOWFISH\_CBC
  Cipher.Blowfish/CBC/PKCS5Padding   CKM\_BLOWFISH\_CBC
  Cipher.AES/CTR/NoPadding           CKM\_AES\_CTR
  Cipher.AES/ECB/NoPadding           CKM\_AES\_ECB
  Cipher.AES/ECB/PKCS5Padding        CKM\_AES\_ECB
  Cipher.AES\_128/CBC/NoPadding      CKM\_AES\_CBC
  Cipher.AES\_128/ECB/NoPadding      CKM\_AES\_ECB
  Cipher.AES\_192/CBC/NoPadding      CKM\_AES\_CBC
  Cipher.AES\_192/ECB/NoPadding      CKM\_AES\_ECB
  Cipher.AES\_256/CBC/NoPadding      CKM\_AES\_CBC
  Cipher.AES\_256/ECB/NoPadding      CKM\_AES\_ECB
  KeyAgreement.ECDH                  CKM\_ECDH1\_DERIVE
  KeyAgreement.DiffieHellman         CKM\_DH\_PKCS\_DERIVE
  KeyPairGenerator.RSA               CKM\_RSA\_PKCS\_KEY\_PAIR\_GEN
  KeyPairGenerator.DSA               CKM\_DSA\_KEY\_PAIR\_GEN
  KeyPairGenerator.EC                CKM\_EC\_KEY\_PAIR\_GEN
  KeyPairGenerator.DiffieHellman     CKM\_DH\_PKCS\_KEY\_PAIR\_GEN
  KeyGenerator.ARCFOUR               CKM\_RC4\_KEY\_GEN
  KeyGenerator.DES                   CKM\_DES\_KEY\_GEN
  KeyGenerator.DESede                CKM\_DES3\_KEY\_GEN
  KeyGenerator.AES                   CKM\_AES\_KEY\_GEN
  KeyGenerator.Blowfish              CKM\_BLOWFISH\_KEY\_GEN
  Mac.HmacMD5                        CKM\_MD5\_HMAC
  Mac.HmacSHA1                       CKM\_SHA\_1\_HMAC
  Mac.HmacSHA224                     CKM\_SHA224\_HMAC
  Mac.HmacSHA256                     CKM\_SHA256\_HMAC
  Mac.HmacSHA384                     CKM\_SHA384\_HMAC
  Mac.HmacSHA512                     CKM\_SHA512\_HMAC
  MessageDigest.MD2                  CKM\_MD2
  MessageDigest.MD5                  CKM\_MD5
  MessageDigest.SHA1                 CKM\_SHA\_1
  MessageDigest.SHA-224              CKM\_SHA224
  MessageDigest.SHA-256              CKM\_SHA256
  MessageDigest.SHA-384              CKM\_SHA384
  MessageDigest.SHA-512              CKM\_SHA512
  KeyFactory.RSA                     Any supported RSA mechanism
  KeyFactory.DSA                     Any supported DSA mechanism
  KeyFactory.EC                      Any supported EC mechanism
  KeyFactory.DiffieHellman           Any supported Diffie-Hellman mechanism
  SecretKeyFactory.ARCFOUR           CKM\_RC4
  SecretKeyFactory.DES               CKM\_DES\_CBC
  SecretKeyFactory.DESede            CKM\_DES3\_CBC
  SecretKeyFactory.AES               CKM\_AES\_CBC
  SecretKeyFactory.Blowfish          CKM\_BLOWFISH\_CBC
  SecureRandom.PKCS11                CK\_TOKEN\_INFO has the CKF\_RNG bit set
  KeyStore.PKCS11                    Always available

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-F068390B-EB41-48A0-A713-B4CBCC72285D}

SunPKCS11 Provider KeyStore Requirements {#JSSEC-GUID-F068390B-EB41-48A0-A713-B4CBCC72285D .sect2}
----------------------------------------

<div>
The following describes the requirements placed by the SunPKCS11
provider\'s KeyStore implementation on the underlying native PKCS\#11
library.

<div class="section">
<div class="infoboxnote" id="GUID-F068390B-EB41-48A0-A713-B4CBCC72285D__GUID-D235AC91-F2D1-4F7A-83D5-5604508A9578">
Note:

Changes may be made in future releases to maximize interoperability with
as many existing PKCS\#11 libraries as possible.

</div>
</div>
<!-- class="section" -->

<div class="section">
Read-Only Access

To map existing objects stored on a PKCS\#11 token to KeyStore entries,
the SunPKCS11 provider\'s KeyStore implementation performs the following
operations.

1.  A search for all private key objects on the token is performed by
    calling `C_FindObjects[Init|Final]`{.codeph}. The search template
    includes the following attributes:
    -   CKA\_TOKEN = true
    -   CKA\_CLASS = CKO\_PRIVATE\_KEY
2.  A search for all certificate objects on the token is performed by
    calling `C_FindObjects[Init|Final]`{.codeph}. The search template
    includes the following attributes:
    -   CKA\_TOKEN = true
    -   CKA\_CLASS = CKO\_CERTIFICATE
3.  Each private key object is matched with its corresponding
    certificate by retrieving their respective CKA\_ID attributes. A
    matching pair must share the same unique CKA\_ID.

    For each matching pair, the certificate chain is built by following
    the issuer-\>subject path. From the end entity certificate, a call
    for `C_FindObjects[Init|Final]`{.codeph} is made with a search
    template that includes the following attributes:

    -   CKA\_TOKEN = true
    -   CKA\_CLASS = CKO\_CERTIFICATE
    -   CKA\_SUBJECT = \[DN of certificate issuer\]

    This search is continued until either no certificate for the issuer
    is found, or until a self-signed certificate is found. If more than
    one certificate is found the first one is used.

    Once a private key and certificate have been matched (and its
    certificate chain built), the information is stored in a private key
    entry with the CKA\_LABEL value from end entity certificate as the
    KeyStore alias.

    If the end entity certificate has no CKA\_LABEL, then the alias is
    derived from the CKA\_ID. If the CKA\_ID can be determined to
    consist exclusively of printable characters, then a String alias is
    created by decoding the CKA\_ID bytes using the UTF-8 charset.
    Otherwise, a hex String alias is created from the CKA\_ID bytes
    (\"0xFFFF\...\", for example).

    If multiple certificates share the same CKA\_LABEL, then the alias
    is derived from the CKA\_LABEL plus the end entity certificate
    issuer and serial number (`"MyCert/CN=foobar/1234"`, for example).

4.  Each certificate not part of a private key entry (as the end entity
    certificate) is checked whether it is trusted. If the CKA\_TRUSTED
    attribute is true, then a KeyStore trusted certificate entry is
    created with the CKA\_LABEL value as the KeyStore alias. If the
    certificate has no CKA\_LABEL, or if multiple certificates share the
    same CKA\_LABEL, then the alias is derived as described above.

    If the CKA\_TRUSTED attribute is not supported then no trusted
    certificate entries are created.

5.  Any private key or certificate object not part of a private key
    entry or trusted certificate entry is ignored.
6.  A search for all secret key objects on the token is performed by
    calling `C_FindObjects[Init|Final]`{.codeph}. The search template
    includes the following attributes:

    -   CKA\_TOKEN = true
    -   CKA\_CLASS = CKO\_SECRET\_KEY

    A KeyStore secret key entry is created for each secret key object,
    with the CKA\_LABEL value as the KeyStore alias. Each secret key
    object must have a unique CKA\_LABEL.

</div>
<!-- class="section" -->

<div class="section">
Write Access

To create new KeyStore entries on a PKCS\#11 token to KeyStore entries,
the SunPKCS11 provider\'s KeyStore implementation performs the following
operations.

1.  When creating a KeyStore entry (during KeyStore.setEntry, for
    example), C\_CreateObject is called with `CKA_TOKEN=true`{.codeph}
    to create token objects for the respective entry contents.

    Private key objects are stored with `CKA_PRIVATE=true`{.codeph}. The
    KeyStore alias (UTF8-encoded) is set as the CKA\_ID for both the
    private key and the corresponding end entity certificate. The
    KeyStore alias is also set as the CKA\_LABEL for the end entity
    certificate object.

    Each certificate in a private key entry\'s chain is also stored. The
    CKA\_LABEL is not set for CA certificates. If a CA certificate is
    already in the token, a duplicate is not stored.

    Secret key objects are stored with `CKA_PRIVATE=true`{.codeph}. The
    KeyStore alias is set as the CKA\_LABEL.

2.  If an attempt is made to convert a session object to a token object
    (for example, if KeyStore.setEntry is called and the private key
    object in the specified entry is a session object), then
    C\_CopyObject is called with `CKA_TOKEN=true`{.codeph}.
3.  If multiple certificates in the token are found to share the same
    CKA\_LABEL, then the write capabilities to the token are disabled.
4.  Since the PKCS\#11 specification does not allow regular applications
    to set `CKA_TRUSTED=true`{.codeph} (only token initialization
    applications may do so), trusted certificate entries can not be
    created.

</div>
<!-- class="section" -->

<div class="section">
Miscellaneous

In addition to the searches listed above, the following searches may be
used by the SunPKCS11 provider\'s KeyStore implementation to perform
internal functions. Specifically, `C_FindObjects[Init|Final]`{.codeph}
may be called with any of the following attribute templates:

-   ``` {.oac_no_warn dir="ltr"}
        CKA_TOKEN    true
        CKA_CLASS    CKO_CERTIFICATE
        CKA_SUBJECT  [subject DN]
    ```

-   ``` {.oac_no_warn dir="ltr"}
        CKA_TOKEN    true
        CKA_CLASS    CKO_SECRET_KEY
        CKA_LABEL    [label]
    ```

-   ``` {.oac_no_warn dir="ltr"}
        CKA_TOKEN    true
        CKA_CLASS    CKO_CERTIFICATE or CKO_PRIVATE_KEY
        CKA_ID       [cka_id]
    ```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-50C137F1-F23B-434D-AA90-5A744ABA2F5B}

Example Provider {#JSSEC-GUID-50C137F1-F23B-434D-AA90-5A744ABA2F5B .sect2}
----------------

<div>
The following is an example of a simple provider that demonstrates
features of the <span class="apiname">Provider</span> class.

<div class="section">
``` {.oac_no_warn dir="ltr"}
package com.foo;

import java.io.*;
import java.lang.reflect.*;
import java.security.*;
import javax.crypto.*;

/**
 * Example provider that demonstrates some Provider class features.
 *
 *  . implement multiple different algorithms in a single class.
 *    Previously each algorithm needed to be implemented in a separate class
 *    (e.g. one for SHA-256, one for SHA-384, etc.)
 *
 *  . multiple concurrent instances of the provider frontend class each
 *    associated with a different backend.
 *
 *  . it uses "unextractable" keys and lets the framework know which key
 *    objects it can and cannot support
 *
 * Note that this is only a simple example provider designed to demonstrate
 * several of the new features.  It is not explicitly designed for efficiency.
 */
public final class ExampleProvider extends Provider {

    // reference to the crypto backend that implements all the algorithms
    final CryptoBackend cryptoBackend;

    public ExampleProvider(String name, CryptoBackend cryptoBackend) {
        super(name, 1.0, "JCA/JCE provider for " + name);
        this.cryptoBackend = cryptoBackend;
        // register the algorithms we support (SHA-256, SHA-384, DESede, and AES)
        putService(new MyService
            (this, "MessageDigest", "SHA-256", "com.foo.ExampleProvider$MyMessageDigest"));
        putService(new MyService
            (this, "MessageDigest", "SHA-384", "com.foo.ExampleProvider$MyMessageDigest"));
        putService(new MyCipherService
            (this, "Cipher", "DES", "com.foo.ExampleProvider$MyCipher"));
        putService(new MyCipherService
            (this, "Cipher", "AES", "com.foo.ExampleProvider$MyCipher"));
    }

    // the API of our fictitious crypto backend
    static abstract class CryptoBackend {
        abstract byte[] digest(String algorithm, byte[] data);
        abstract byte[] encrypt(String algorithm, KeyHandle key, byte[] data);
        abstract byte[] decrypt(String algorithm, KeyHandle key, byte[] data);
        abstract KeyHandle createKey(String algorithm, byte[] keyData);
    }

    // the shell of the representation the crypto backend uses for keys
    private static final class KeyHandle {
        // fill in code
    }

    // we have our own ServiceDescription implementation that overrides newInstance()
    // that calls the (Provider, String) constructor instead of the no-args constructor
    private static class MyService extends Service {

        private static final Class[] paramTypes = {Provider.class, String.class};

        MyService(Provider provider, String type, String algorithm,
                String className) {
            super(provider, type, algorithm, className, null, null);
        }

        public Object newInstance(Object param) throws NoSuchAlgorithmException {
            try {
                // get the Class object for the implementation class
                Class clazz;
                Provider provider = getProvider();
                ClassLoader loader = provider.getClass().getClassLoader();
                if (loader == null) {
                    clazz = Class.forName(getClassName());
                } else {
                    clazz = loader.loadClass(getClassName());
                }
                // fetch the (Provider, String) constructor
                Constructor cons = clazz.getConstructor(paramTypes);
                // invoke constructor and return the SPI object
                Object obj = cons.newInstance(new Object[] {provider, getAlgorithm()});
                return obj;
            } catch (Exception e) {
                throw new NoSuchAlgorithmException("Could not instantiate service", e);
            }
        }
    }

    // custom ServiceDescription class for Cipher objects. See supportsParameter() below
    private static class MyCipherService extends MyService {
        MyCipherService(Provider provider, String type, String algorithm,
                String className) {
            super(provider, type, algorithm, className);
        }
        // we override supportsParameter() to let the framework know which
        // keys we can support. We support instances of MySecretKey, if they
        // are stored in our provider backend, plus SecretKeys with a RAW encoding.
        public boolean supportsParameter(Object obj) {
            if (obj instanceof SecretKey == false) {
                return false;
            }
            SecretKey key = (SecretKey)obj;
            if (key.getAlgorithm().equals(getAlgorithm()) == false) {
                return false;
            }
            if (key instanceof MySecretKey) {
                MySecretKey myKey = (MySecretKey)key;
                return myKey.provider == getProvider();
            } else {
                return "RAW".equals(key.getFormat());
            }
        }
    }

    // our generic MessageDigest implementation. It implements all digest
    // algorithms in a single class. We only implement the bare minimum
    // of MessageDigestSpi methods
    private static final class MyMessageDigest extends MessageDigestSpi {
        private final ExampleProvider provider;
        private final String algorithm;
        private ByteArrayOutputStream buffer;
        MyMessageDigest(Provider provider, String algorithm) {
            super();
            this.provider = (ExampleProvider)provider;
            this.algorithm = algorithm;
            engineReset();
        }
        protected void engineReset() {
            buffer = new ByteArrayOutputStream();
        }
        protected void engineUpdate(byte b) {
            buffer.write(b);
        }
        protected void engineUpdate(byte[] b, int ofs, int len) {
            buffer.write(b, ofs, len);
        }
        protected byte[] engineDigest() {
            byte[] data = buffer.toByteArray();
            byte[] digest = provider.cryptoBackend.digest(algorithm, data);
            engineReset();
            return digest;
        }
    }

    // our generic Cipher implementation, only partially complete. It implements
    // all cipher algorithms in a single class. We implement only as many of the
    // CipherSpi methods as required to show how it could work
    private static abstract class MyCipher extends CipherSpi {
        private final ExampleProvider provider;
        private final String algorithm;
        private int opmode;
        private MySecretKey myKey;
        private ByteArrayOutputStream buffer;
        MyCipher(Provider provider, String algorithm) {
            super();
            this.provider = (ExampleProvider)provider;
            this.algorithm = algorithm;
        }
        protected void engineInit(int opmode, Key key, SecureRandom random)
                throws InvalidKeyException {
            this.opmode = opmode;
            myKey = MySecretKey.getKey(provider, algorithm, key);
            if (myKey == null) {
                throw new InvalidKeyException();
            }
            buffer = new ByteArrayOutputStream();
        }
        protected byte[] engineUpdate(byte[] b, int ofs, int len) {
            buffer.write(b, ofs, len);
            return new byte[0];
        }
        protected int engineUpdate(byte[] b, int ofs, int len, byte[] out, int outOfs) {
            buffer.write(b, ofs, len);
            return 0;
        }
        protected byte[] engineDoFinal(byte[] b, int ofs, int len) {
            buffer.write(b, ofs, len);
            byte[] in = buffer.toByteArray();
            byte[] out;
            if (opmode == Cipher.ENCRYPT_MODE) {
                out = provider.cryptoBackend.encrypt(algorithm, myKey.handle, in);
            } else {
                out = provider.cryptoBackend.decrypt(algorithm, myKey.handle, in);
            }
            buffer = new ByteArrayOutputStream();
            return out;
        }
        // code for remaining CipherSpi methods goes here
    }

    // our SecretKey implementation. All our keys are stored in our crypto
    // backend, we only have an opaque handle available. There is no
    // encoded form of these keys.
    private static final class MySecretKey implements SecretKey {

        final String algorithm;
        final Provider provider;
        final KeyHandle handle;

        MySecretKey(Provider provider, String algorithm, KeyHandle handle) {
            super();
            this.provider = provider;
            this.algorithm = algorithm;
            this.handle = handle;
        }
        public String getAlgorithm() {
            return algorithm;
        }
        public String getFormat() {
            return null; // this key has no encoded form
        }
        public byte[] getEncoded() {
            return null; // this key has no encoded form
        }
        // Convert the given key to a key of the specified provider, if possible
        static MySecretKey getKey(ExampleProvider provider, String algorithm, Key key) {
            if (key instanceof SecretKey == false) {
                return null;
            }
            // algorithm name must match
            if (!key.getAlgorithm().equals(algorithm)) {
                return null;
            }
            // if key is already an instance of MySecretKey and is stored
            // on this provider, return it right away
            if (key instanceof MySecretKey) {
                MySecretKey myKey = (MySecretKey)key;
                if (myKey.provider == provider) {
                    return myKey;
                }
            }
            // otherwise, if the input key has a RAW encoding, convert it
            if (!"RAW".equals(key.getFormat())) {
                return null;
            }
            byte[] encoded = key.getEncoded();
            KeyHandle handle = provider.cryptoBackend.createKey(algorithm, encoded);
            return new MySecretKey(provider, algorithm, handle);
        }
    }
}
```

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
| - ------------------ | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ------------ --      | e | )\                   |
|          [![Previous | L |             <span cl |
| ](../../dcommon/gifs | o | ass="icon">Contents< |
| /leftnav.gif)\       | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|       [![Next](../.. | ] | -------------------- |
| /dcommon/gifs/rightn | ( | -------------------- |
| av.gif)\             | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](o | . |                      |
| racle-providers.htm) | . |                      |
|    <span class="icon | / |                      |
| ">Next</span>](java- | d |                      |
| authentication-and-a | c |                      |
| uthorization-service | o |                      |
| -jaas1.htm)          | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| - ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ------------ --      | s |                      |
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
