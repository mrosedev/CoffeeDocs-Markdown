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

  ------------------------------------------------------------ ----------------------------------------------------------------------------- --
         [![Previous](../../dcommon/gifs/leftnav.gif)\                          [![Next](../../dcommon/gifs/rightnav.gif)\                   
   <span class="icon">Previous</span>](general-security1.htm)   <span class="icon">Next</span>](java-se-platform-security-architecture.htm)  
  ------------------------------------------------------------ ----------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-2EF91196-D468-4D0F-8FDC-DA2BEA165D10}<!-- End Header -->

Java Security Overview {#JSSEC-GUID-2EF91196-D468-4D0F-8FDC-DA2BEA165D10 .sect1}
======================

<div>
Java security includes a large set of APIs, tools, and implementations
of commonly-used security algorithms, mechanisms, and protocols. The
Java security APIs span a wide range of areas, including cryptography,
public key infrastructure, secure communication, authentication, and
access control. Java security technology provides the developer with a
comprehensive security framework for writing applications, and also
provides the user or administrator with a set of tools to securely
manage applications.

</div>
<div class="sect2">
[]{#GUID-69EE84E6-E0BD-48B2-B3F2-200D9A5FCF93}

Introduction to Java Security {#JSSEC-GUID-69EE84E6-E0BD-48B2-B3F2-200D9A5FCF93 .sect2}
-----------------------------

<div>
The JDK is designed with a strong emphasis on security. At its core, the
Java language itself is type-safe and provides automatic garbage
collection, enhancing the robustness of application code. A secure class
loading and verification mechanism ensures that only legitimate Java
code is executed. The Java security architecture includes a large set of
application programming interfaces (APIs), tools, and implementations of
commonly-used security algorithms, mechanisms, and protocols.

The Java security APIs span a wide range of areas. Cryptographic and
public key infrastructure (PKI) interfaces provide the underlying basis
for developing secure applications. Interfaces for performing
authentication and access control enable applications to guard against
unauthorized access to protected resources.

The APIs allow for multiple interoperable implementations of algorithms
and other security services. Services are implemented in
<span class="variable">providers</span>, which are plugged into the JDK
through a standard interface that makes it easy for applications to
obtain security services without having to know anything about their
implementations. This allows developers to focus on how to integrate
security into their applications, rather than on how to actually
implement complex security mechanisms.

The JDK includes a number of providers that implement a core set of
security services. It also allows for additional custom providers to be
installed. This enables developers to extend the platform with new
security mechanisms.

The JDK is divided into modules. Modules that contain security APIs
include the following:

<div class="tblformal" id="GUID-69EE84E6-E0BD-48B2-B3F2-200D9A5FCF93__GUID-F0CDE653-E96D-4643-A7D5-4858F75CA2E5">
Table 1-1 Modules That Contain Security APIs

  Module                                                                                                                          Description
  ------------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  [<span class="apiname">java.base</span>](https://docs.oracle.com/javase/10/docs/api/java.base-summary.html)                     Defines the foundational APIs of <span>Java SE</span>. Contained packages include [<span class="apiname">java.security</span>](https://docs.oracle.com/javase/10/docs/api/java/security/package-summary.html), [<span class="apiname">javax.crypto</span>](https://docs.oracle.com/javase/10/docs/api/javax/crypto/package-summary.html), [<span class="apiname">javax.net.ssl</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/package-summary.html), and [<span class="apiname">javax.security.auth</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/package-summary.html).
  [<span class="apiname">java.security.jgss</span>](https://docs.oracle.com/javase/10/docs/api/java.security.jgss-summary.html)   Defines the Java binding of the IETF Generic Security Services API (GSS-API). This module also contains GSS-API mechanisms including Kerberos v5 and SPNEGO.
  [<span class="apiname">java.security.sasl</span>](https://docs.oracle.com/javase/10/docs/api/java.security.sasl-summary.html)   Defines Java support for the IETF Simple Authentication and Security Layer (SASL). This module also contains SASL mechanisms including DIGEST-MD5, CRAM-MD5, and NTLM.
  [<span class="apiname">java.smartcardio</span>](https://docs.oracle.com/javase/10/docs/api/java.smartcardio-summary.html)       Defines the Java Smart Card I/O API.
  [<span class="apiname">java.xml.crypto</span>](https://docs.oracle.com/javase/10/docs/api/java.xml.crypto-summary.html)         Defines the API for XML cryptography.
  [<span class="apiname">jdk.security.auth</span>](https://docs.oracle.com/javase/10/docs/api/jdk.security.auth-summary.html)     Provides implementations of the <span class="apiname">javax.security.auth.\*</span> interfaces and various authentication modules.
  [<span class="apiname">jdk.security.jgss</span>](https://docs.oracle.com/javase/10/docs/api/jdk.security.jgss-summary.html)     Defines Java extensions to the GSS-API and an implementation of the SASL GSS-API mechanism.

</div>
<!-- class="inftblhruleinformal" -->

</div>
</div>
<div class="sect2">
[]{#GUID-65C96219-B2AB-4205-808E-5B41CB2AD694}

Java Language Security and Bytecode Verification {#JSSEC-GUID-65C96219-B2AB-4205-808E-5B41CB2AD694 .sect2}
------------------------------------------------

<div>
The Java language is designed to be type-safe and easy to use. It
provides automatic memory management, garbage collection, and
range-checking on arrays. This reduces the overall programming burden
placed on developers, leading to fewer subtle programming errors and to
safer, more robust code.

A compiler translates Java programs into a machine-independent bytecode
representation. A bytecode verifier is invoked to ensure that only
legitimate bytecodes are executed in the Java runtime. It checks that
the bytecodes conform to the Java Language Specification and do not
violate Java language rules or namespace restrictions. The verifier also
checks for memory management violations, stack underflows or overflows,
and illegal data typecasts. Once bytecodes have been verified, the Java
runtime prepares them for execution.

<div class="p">
In addition, the Java language defines different access modifiers that
can be assigned to Java classes, methods, and fields, enabling
developers to restrict access to their class implementations as
appropriate. The language defines four distinct access levels:

-   `private`{.codeph}: Most restrictive modifier; access is not allowed
    outside the particular class in which the private member (a method,
    for example) is defined.

-   `protected`{.codeph}: Allows access to any subclass or to other
    classes within the same package.

-   Package-private: If not specified, then this is the default access
    level; allows access to classes within the same package.

-   `public`{.codeph}: No longer guarantees that the element is
    accessible everywhere; accessibility depends upon whether the
    package containing that element is exported by its defining module
    and whether that module is readable by the module containing the
    code that is attempting to access it.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-0C458D46-BA4F-4091-817B-9902B6E18240}

Basic Security Architecture {#JSSEC-GUID-0C458D46-BA4F-4091-817B-9902B6E18240 .sect2}
---------------------------

<div>
The JDK defines a set of APIs spanning major security areas, including
cryptography, public key infrastructure, authentication, secure
communication, and access control. The APIs allow developers to easily
integrate security into their application code.

The APIs are designed around the following principles:

[<!-- -->]{#GUID-0C458D46-BA4F-4091-817B-9902B6E18240__GUID-E3E05B58-32DE-4017-A5C8-4A97E0D050F5}<span class="variable">Implementation independence</span>
:   Applications do not need to implement security themselves. Rather,
    they can request security services from the JDK. Security services
    are implemented in providers (see the section [Security
    Providers](java-security-overview1.htm#GUID-74E1EFEA-F1DD-466C-B61A-CB5E89FA50DE "The java.security.Provider class encapsulates the notion of a security provider in the Java platform. It specifies the provider's name and lists the security services it implements. Multiple providers may be configured at the same time and are listed in order of preference. When a security service is requested, the highest priority provider that implements that service is selected.")),
    which are plugged into the JDK via a standard interface. An
    application may rely on multiple independent providers for security
    functionality.

[<!-- -->]{#GUID-0C458D46-BA4F-4091-817B-9902B6E18240__GUID-755A8E77-2D9C-4C46-B0AE-562957014B3D}<span class="variable">Implementation interoperability</span>

:   Providers are interoperable across applications. Specifically, an
    application is not bound to a specific provider if it does not rely
    on default values from the provider.

[<!-- -->]{#GUID-0C458D46-BA4F-4091-817B-9902B6E18240__GUID-194E3FEB-06EE-4E3D-9473-206E99B76414}<span class="variable">Algorithm extensibility</span>
:   The JDK includes a number of built-in providers that implement a
    basic set of security services that are widely used today. However,
    some applications may rely on emerging standards not yet
    implemented, or on proprietary services. The JDK supports the
    installation of custom providers that implement such services.

</div>
<div class="sect3">
[]{#GUID-74E1EFEA-F1DD-466C-B61A-CB5E89FA50DE}

### Security Providers {#JSSEC-GUID-74E1EFEA-F1DD-466C-B61A-CB5E89FA50DE .sect3}

<div>
The `java.security.Provider`{.codeph} class encapsulates the notion of a
security provider in the Java platform. It specifies the provider\'s
name and lists the security services it implements. Multiple providers
may be configured at the same time and are listed in order of
preference. When a security service is requested, the highest priority
provider that implements that service is selected.

Applications rely on the relevant `getInstance`{.codeph} method to
request a security service from an underlying provider.

For example, message digest creation represents one type of service
available from providers. To request an implementation of a specific
message digest algorithm, call the method
<span class="apiname">java.security.MessageDigest.getInstance</span>.
The following statement requests a SHA-256 message digest implementation
without specifying a provider name:

``` {.codeblock dir="ltr"}
    MessageDigest md = MessageDigest.getInstance("SHA-256");
```

The following figure illustrates how this statement obtains a SHA-256
message digest implementation. The providers are searched in preference
order, and the implementation from the first provider supplying that
particular algorithm, `ProviderB`{.codeph}, is returned.

<div class="figure" id="GUID-74E1EFEA-F1DD-466C-B61A-CB5E89FA50DE__SHA-256MESSAGEDIGESTWITHOUTPROVIDER-1D43C810">
Figure 1-1 Request SHA-256 Message Digest Implementation Without
Specifying Provider

\
![Description of Figure 1-1
follows](img/security-overview-message-digest-wo-provider.png "Description of Figure 1-1 follows")\
[Description of \"Figure 1-1 Request SHA-256 Message Digest
Implementation Without Specifying
Provider\"](img_text/security-overview-message-digest-wo-provider.htm)\

</div>
<!-- class="figure" -->

You can optionally request an implementation from a specific provider by
specifying the provider\'s name. The following statement requests a
SHA-256 message digest implementation from a specific provider,
`ProviderC`{.codeph}:

``` {.codeblock dir="ltr"}
    MessageDigest md = MessageDigest.getInstance("SHA-256", "ProviderC");
```

The following figure illustrates how this statement requests a SHA-256
message digest implementation from a specific provider,
`ProviderC`{.codeph}. In this case, the implementation from that
provider is returned, even though a provider with a higher preference
order, `ProviderB`{.codeph}, also supplies a SHA-256 implementation.

<div class="figure" id="GUID-74E1EFEA-F1DD-466C-B61A-CB5E89FA50DE__REQUESTSHA-256MESSAGEDIGESTIMPLEMEN-1D37A87C">
Figure 1-2 Request SHA-256 Message Digest Implementation from Specific
Provider

\
![Description of Figure 1-2
follows](img/security-overview-message-digest-providerc.png "Description of Figure 1-2 follows")\
[Description of \"Figure 1-2 Request SHA-256 Message Digest
Implementation from Specific
Provider\"](img_text/security-overview-message-digest-providerc.htm)\

</div>
<!-- class="figure" -->

For more information about cryptographic services, such as message
digest algorithms, see the section [Java
Cryptography](java-security-overview1.htm#GUID-C6D250FC-F147-4284-A6BF-8384DFD39DA6 "The Java cryptography architecture is a framework for accessing and developing cryptographic functionality for the Java platform.").

Oracle\'s implementation of the Java platform includes a number of
built-in default providers that implement a basic set of security
services that can be used by applications. Note that other vendor
implementations of the Java platform may include different sets of
providers that encapsulate vendor-specific sets of security services.
The term built-in default providers refers to the providers available in
Oracle\'s implementation.

</div>
</div>
<div class="sect3">
[]{#GUID-25BF3893-E577-4C96-9A4A-BEA39555CA72}

### File Locations {#JSSEC-GUID-25BF3893-E577-4C96-9A4A-BEA39555CA72 .sect3}

<div>
The following table lists locations of some security-related files and
tools.

<div class="section">
<div class="tblformal" id="GUID-25BF3893-E577-4C96-9A4A-BEA39555CA72__GUID-5DE08858-9C50-4879-8050-9C419F7A92DA">
Table 1-2 Java security files and tools

+-----------------------+-----------------------+-----------------------+
| File Name or Tool     | Location              | Description           |
| Name                  |                       |                       |
+:======================+:======================+:======================+
| `java.security`       | `<java-home>/conf/sec | Certain aspects of    |
|                       | urity`{.codeph}       | Java security, such   |
|                       |                       | as configuring the    |
|                       |                       | providers, may be     |
|                       |                       | customized by setting |
|                       |                       | Security Properties.  |
|                       |                       | You may set Security  |
|                       |                       | Properties statically |
|                       |                       | in the                |
|                       |                       | `java.security`{.code |
|                       |                       | ph}                   |
|                       |                       | file. Security        |
|                       |                       | Properties may also   |
|                       |                       | be set dynamically by |
|                       |                       | calling appropriate   |
|                       |                       | methods of the        |
|                       |                       | `Security`{.codeph}   |
|                       |                       | class (in the         |
|                       |                       | `java.security`{.code |
|                       |                       | ph}                   |
|                       |                       | package).             |
+-----------------------+-----------------------+-----------------------+
| `java.policy`         | `<java-home>/conf/sec | This is the default   |
|                       | urity`{.codeph}       | system policy file;   |
|                       |                       | see [Security         |
|                       |                       | Policy](java-security |
|                       |                       | -overview1.htm#GUID-5 |
|                       |                       | FB6B917-DDFE-42F5-923 |
|                       |                       | 3-8E6250C1EA93 "A lim |
|                       |                       | ited set of default p |
|                       |                       | ermissions are grante |
|                       |                       | d to code by class lo |
|                       |                       | aders. Administrators |
|                       |                       |  have the ability to  |
|                       |                       | flexibly manage addit |
|                       |                       | ional code permission |
|                       |                       | s via a security poli |
|                       |                       | cy.").                |
+-----------------------+-----------------------+-----------------------+
| Cryptographic policy  | `<java-home>/conf/sec | This directory        |
| directory             | urity/policy`{.codeph | contains sets of      |
|                       | }                     | jurisdiction policy   |
|                       |                       | files; see            |
|                       |                       | [Cryptographic        |
|                       |                       | Strength              |
|                       |                       | Configuration](java-c |
|                       |                       | ryptography-architect |
|                       |                       | ure-jca-reference-gui |
|                       |                       | de.htm#GUID-EFA5AC2D- |
|                       |                       | 644E-4CD9-8523-C6D393 |
|                       |                       | 6D5FB1).              |
+-----------------------+-----------------------+-----------------------+
| `cacerts`             | `<java-home>/lib/secu | The `cacerts` file    |
|                       | rity`{.codeph}        | represents a          |
|                       |                       | system-wide keystore  |
|                       |                       | with Certificate      |
|                       |                       | Authority (CA) and    |
|                       |                       | other trusted         |
|                       |                       | certificates. For     |
|                       |                       | information about     |
|                       |                       | configuring and       |
|                       |                       | managing this file,   |
|                       |                       | see                   |
|                       |                       | [keytool](olink:JSWOR |
|                       |                       | -GUID-5990A2E4-78E3-4 |
|                       |                       | 7B7-AE75-6D1826259549 |
|                       |                       | )                     |
|                       |                       | in <span><cite>Java   |
|                       |                       | Platform, Standard    |
|                       |                       | Edition Tools         |
|                       |                       | Reference</cite></spa |
|                       |                       | n>.                   |
+-----------------------+-----------------------+-----------------------+
| `keytool`{.codeph},   | `<java-home>/bin`{.co | For more information  |
| `jarsigner`{.codeph}, | deph}                 | about                 |
| `policytool`{.codeph} |                       | security-related      |
|                       |                       | tools, see [Security  |
| Windows only:         |                       | Tools and             |
| `kinit`{.codeph},     |                       | Commands](olink:JSWOR |
| `klist`{.codeph},     |                       | -GUID-F73EC9CE-C422-4 |
| `ktab`{.codeph}       |                       | EDB-B3E6-AA3A3A1DDB8E |
|                       |                       | )                     |
|                       |                       | in <span><cite>Java   |
|                       |                       | Platform, Standard    |
|                       |                       | Edition Tools         |
|                       |                       | Reference</cite></spa |
|                       |                       | n>.                   |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-C6D250FC-F147-4284-A6BF-8384DFD39DA6}

Java Cryptography {#JSSEC-GUID-C6D250FC-F147-4284-A6BF-8384DFD39DA6 .sect2}
-----------------

<div>
The Java cryptography architecture is a framework for accessing and
developing cryptographic functionality for the Java platform.

It includes APIs for a large variety of cryptographic services,
including the following:

-   Message digest algorithms
-   Digital signature algorithms
-   Symmetric bulk and stream encryption
-   Asymmetric encryption
-   Password-based encryption (PBE)
-   Elliptic Curve Cryptography (ECC)
-   Key agreement algorithms
-   Key generators
-   Message Authentication Codes (MACs)
-   Secure Random Number Generators

<div class="p">
For historical (export control) reasons, the cryptography APIs are
organized into two distinct packages:

-   The `java.security`{.codeph} and `java.security.*`{.codeph} packages
    contains classes that are <span class="variable">not</span> subject
    to export controls (like `Signature`{.codeph} and
    `MessageDigest`{.codeph})

-   The `javax.crypto`{.codeph} package contains classes that are
    subject to export controls (like `Cipher`{.codeph} and
    `KeyAgreement`{.codeph})

</div>
The cryptographic interfaces are provider-based, allowing for multiple
and interoperable cryptography implementations. Some providers may
perform cryptographic operations in software; others may perform the
operations on a hardware token (for example, on a smart card device or
on a hardware cryptographic accelerator). Providers that implement
export-controlled services must be digitally signed by a certificate
issued by the Oracle JCE Certificate Authority.

The Java platform includes built-in providers for many of the most
commonly used cryptographic algorithms, including the RSA, DSA, and
ECDSA signature algorithms, the AES encryption algorithm, the SHA-2
message digest algorithms, and the Diffie-Hellman (DH) and Elliptic
Curve Diffie-Hellman (ECDH) key agreement algorithms. Most of the
built-in providers implement cryptographic algorithms in Java code.

The Java platform also includes a built-in provider that acts as a
bridge to a native PKCS\#11 (v2.x) token. This provider, named
`SunPKCS11`{.codeph}, allows Java applications to seamlessly access
cryptographic services located on PKCS\#11-compliant tokens.

On Windows, the Java platform includes a built-in provider that acts as
a bridge to the native Microsoft CryptoAPI. This provider, named
`SunMSCAPI`{.codeph}, allows Java applications to seamlessly access
cryptographic services on Windows through the CryptoAPI.

</div>
</div>
<div class="sect2">
[]{#GUID-054AD71D-D449-47FF-B6F7-F416DA821D46}

Public Key Infrastructure {#JSSEC-GUID-054AD71D-D449-47FF-B6F7-F416DA821D46 .sect2}
-------------------------

<div>
Public Key Infrastructure (PKI) is a term used for a framework that
enables secure exchange of information based on public key cryptography.
It allows identities (of people, organizations, etc.) to be bound to
digital certificates and provides a means of verifying the authenticity
of certificates. PKI encompasses keys, certificates, public key
encryption, and trusted Certification Authorities (CAs) who generate and
digitally sign certificates.

The Java platform includes APIs and provider support for X.509 digital
certificates and Certificate Revocation Lists (CRLs), as well as
PKIX-compliant certification path building and validation. The classes
related to PKI are located in the `java.security`{.codeph} and
`java.security.cert`{.codeph} packages.

</div>
<div class="sect3">
[]{#GUID-EB29B931-D1DE-420B-849C-D731A8DF9CDC}

### Key and Certificate Storage {#JSSEC-GUID-EB29B931-D1DE-420B-849C-D731A8DF9CDC .sect3}

<div>
The Java platform provides for long-term persistent storage of
cryptographic keys and certificates via key and certificate stores.
Specifically, the `java.security.KeyStore`{.codeph} class represents a
<span class="italic">key store</span>, a secure repository of
cryptographic keys and/or trusted certificates (to be used, for example,
during certification path validation), and the
`java.security.cert.CertStore`{.codeph} class represents a
<span class="italic">certificate store</span>, a public and potentially
vast repository of unrelated and typically untrusted certificates. A
`CertStore`{.codeph} may also store CRLs.

`KeyStore`{.codeph} and `CertStore`{.codeph} implementations are
distinguished by types. The Java platform includes the standard PKCS11
and PKCS12 key store types (whose implementations are compliant with the
corresponding PKCS specifications from RSA Security). It also contains a
proprietary file-based key store type called JKS (which stands for Java
Key Store), and a type called DKS (Domain Key Store) which is a
collection of keystores that are presented as a single logical keystore.

The Java platform includes a special built-in key store, `cacerts`, that
contains a number of certificates for well-known, trusted CAs. The
keytool utility is able to list the certificates included in `cacerts`.
See [keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) in
<span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

The SunPKCS11 provider mentioned in the section [Java
Cryptography](java-security-overview1.htm#GUID-C6D250FC-F147-4284-A6BF-8384DFD39DA6 "The Java cryptography architecture is a framework for accessing and developing cryptographic functionality for the Java platform.")
includes a PKCS11 `KeyStore`{.codeph} implementation. This means that
keys and certificates residing in secure hardware (such as a smart card)
can be accessed and used by Java applications via the
`KeyStore`{.codeph} API. Note that smart card keys may not be permitted
to leave the device. In such cases, the `java.security.Key`{.codeph}
object returned by the `KeyStore`{.codeph} API may simply be a reference
to the key (that is, it would not contain the actual key material). Such
a `Key`{.codeph} object can only be used to perform cryptographic
operations on the device where the actual key resides.

The Java platform also includes an LDAP certificate store type (for
accessing certificates stored in an LDAP directory), as well as an
in-memory Collection certificate store type (for accessing certificates
managed in a `java.util.Collection`{.codeph} object).

</div>
</div>
<div class="sect3">
[]{#GUID-BC9A5E59-953A-4EBC-9F03-BEF099B64F5B}

### Public Key Infrastructure Tools {#JSSEC-GUID-BC9A5E59-953A-4EBC-9F03-BEF099B64F5B .sect3}

<div>
There are two built-in tools for working with keys, certificates, and
key stores:

-   `keytool`{.codeph} creates and manages key stores. Use it to perform
    the following tasks:

    -   Create public/private key pairs
    -   Display, import, and export X.509 v1, v2, and v3 certificates
        stored as files
    -   Create X.509 certificates
    -   Issue certificate (PKCS\#10) requests to be sent to CAs
    -   Create certificates based on certificate requests
    -   Import certificate replies (obtained from the CAs sent
        certificate requests)
    -   Designate public key certificates as trusted
    -   Accept a password and store it securely as a secret key

-   `jarsigner`{.codeph} signs JAR files and verifies signatures on
    signed JAR files. The Java ARchive (JAR) file format enables the
    bundling of multiple files into a single file. Typically, a JAR file
    contains the class files and auxiliary resources associated with
    applets and applications.

<div class="p">
To digitally sign code, perform the following:

1.  Use `keytool`{.codeph} to generate or import appropriate keys and
    certificates into your key store (if they are not there already).

2.  Use the `jar`{.codeph} tool to package the code in a JAR file.

3.  <div class="p">
    Use the `jarsigner`{.codeph} tool to sign the JAR file. The
    `jarsigner`{.codeph} tool accesses a key store to find any keys and
    certificates needed to sign a JAR file or to verify the signature of
    a signed JAR file.

    <div class="infoboxnote" id="GUID-BC9A5E59-953A-4EBC-9F03-BEF099B64F5B__GUID-5B222233-498E-4C87-94A9-D8FC5BAFD8E3">
    Note:

    `jarsigner`{.codeph} can optionally generate signatures that include
    a timestamp. Systems (such as Java Plug-in) that verify JAR file
    signatures can check the timestamp and accept a JAR file that was
    signed while the signing certificate was valid rather than requiring
    the certificate to be current. (Certificates typically expire
    annually, and it is not reasonable to expect JAR file creators to
    re-sign deployed JAR files annually.)

    </div>
    </div>

</div>
See [keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) and
[jarsigner](olink:JSWOR-GUID-925E7A1B-B3F3-44D2-8B49-0B3FA2C54864) in
<span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-F8BE6C49-3506-4D1A-8E4E-053CA439D1E2}

Authentication {#JSSEC-GUID-F8BE6C49-3506-4D1A-8E4E-053CA439D1E2 .sect2}
--------------

<div>
Authentication is the process of determining the identity of a user. In
the context of the Java runtime environment, it is the process of
identifying the user of an executing Java program. In certain cases,
this process may rely on the services described in the section [Java
Cryptography](java-security-overview1.htm#GUID-C6D250FC-F147-4284-A6BF-8384DFD39DA6 "The Java cryptography architecture is a framework for accessing and developing cryptographic functionality for the Java platform.").

The Java platform provides APIs that enable an application to perform
user authentication via pluggable login modules. Applications call into
the `LoginContext`{.codeph} class (in the
`javax.security.auth.login`{.codeph} package), which in turn references
a configuration. The configuration specifies which login module (an
implementation of the `javax.security.auth.spi.LoginModule`{.codeph}
interface) is to be used to perform the actual authentication.

Since applications solely talk to the standard `LoginContext`{.codeph}
API, they can remain independent from the underlying plug-in modules.
New or updated modules can be plugged in for an application without
having to modify the application itself. The following figure
illustrates the independence between applications and underlying login
modules:

<div class="figure" id="GUID-F8BE6C49-3506-4D1A-8E4E-053CA439D1E2__GUID-99060EF8-D731-4093-BFAB-B715A085DA49">
Figure 1-3 Authentication Login Modules Plugging into the Authentication
Framework

![Description of Figure 1-3
follows](img/security-overview-authentication-login-modules.png "Description of Figure 1-3 follows")\
[Description of \"Figure 1-3 Authentication Login Modules Plugging into
the Authentication
Framework\"](img_text/security-overview-authentication-login-modules.htm)

</div>
<!-- class="figure" -->

It is important to note that although login modules are pluggable
components that can be configured into the Java platform, they are not
plugged in via security providers. Therefore, they do not follow the
provider searching model as described in the section [Security
Providers](java-security-overview1.htm#GUID-74E1EFEA-F1DD-466C-B61A-CB5E89FA50DE "The java.security.Provider class encapsulates the notion of a security provider in the Java platform. It specifies the provider's name and lists the security services it implements. Multiple providers may be configured at the same time and are listed in order of preference. When a security service is requested, the highest priority provider that implements that service is selected.").
Instead, as is shown in [Figure
1-3](java-security-overview1.htm#GUID-F8BE6C49-3506-4D1A-8E4E-053CA439D1E2__GUID-99060EF8-D731-4093-BFAB-B715A085DA49),
login modules are administered by their own unique configuration.

The Java platform provides the following built-in login modules, all in
the `com.sun.security.auth.module`{.codeph} package:

-   `Krb5LoginModule`{.codeph} for authentication using Kerberos
    protocols
-   `JndiLoginModule`{.codeph} for username/password authentication
    using LDAP or NIS databases
-   `KeyStoreLoginModule`{.codeph} for logging into any type of key
    store, including a PKCS\#11 token key store

Authentication can also be achieved during the process of establishing a
secure communication channel between two peers. The Java platform
provides implementations of a number of standard communication
protocols, which are discussed in the section [Secure
Communication](java-security-overview1.htm#GUID-4E5FEEF5-A541-4222-AD18-31AE184F38E4 "The data that travels across a network can be accessed by someone who is not the intended recipient. When the data includes private information, such as passwords and credit card numbers, steps must be taken to make the data unintelligible to unauthorized parties. It is also important to ensure that you are sending the data to the appropriate party, and that the data has not been modified, either intentionally or unintentionally, during transport.").

</div>
</div>
<div class="sect2">
[]{#GUID-4E5FEEF5-A541-4222-AD18-31AE184F38E4}

Secure Communication {#JSSEC-GUID-4E5FEEF5-A541-4222-AD18-31AE184F38E4 .sect2}
--------------------

<div>
The data that travels across a network can be accessed by someone who is
not the intended recipient. When the data includes private information,
such as passwords and credit card numbers, steps must be taken to make
the data unintelligible to unauthorized parties. It is also important to
ensure that you are sending the data to the appropriate party, and that
the data has not been modified, either intentionally or unintentionally,
during transport.

Cryptography forms the basis required for secure communication; see the
section [Java
Cryptography](java-security-overview1.htm#GUID-C6D250FC-F147-4284-A6BF-8384DFD39DA6 "The Java cryptography architecture is a framework for accessing and developing cryptographic functionality for the Java platform.").
The Java platform also provides API support and provider implementations
for a number of standard secure communication protocols.

</div>
<div class="sect3">
[]{#GUID-FCF419A7-B856-46DD-A36F-C6F88F9AF37F}

### SSL, TLS, and DTLS Protocols {#JSSEC-GUID-FCF419A7-B856-46DD-A36F-C6F88F9AF37F .sect3}

<div>
The JDK provides APIs and an implementation of the SSL, TLS, and DTLS
protocols that includes functionality for data encryption, message
integrity, and server and client authentication. Applications can use
SSL/TLS/DTLS to provide for the secure passage of data between two peers
over any application protocol, such as HTTP on top of TCP/IP.

The `javax.net.ssl.SSLSocket`{.codeph} class represents a network socket
that encapsulates SSL/TLS support on top of a normal stream socket
(`java.net.Socket`{.codeph}). Some applications might want to use
alternate data transport abstractions (for example, New-I/O); the
`javax.net.ssl.SSLEngine`{.codeph} class is available to produce and
consume SSL/TLS/DTLS packets.

The JDK also includes APIs that support the notion of pluggable
(provider-based) key managers and trust managers.
<span class="variable">A key manager</span> is encapsulated by the
`javax.net.ssl.KeyManager`{.codeph} class, and manages the keys used to
perform authentication. A <span class="variable">trust manager</span> is
encapsulated by the `TrustManager`{.codeph} class (in the same package),
and makes decisions about who to trust based on certificates in the key
store it manages.

The JDK includes a built-in provider that implements the SSL/TLS/DTLS
protocols:

-   SSLv3
-   TLSv1
-   TLSv1.1
-   TLSv1.2
-   DTLSv1.0
-   DTLSv1.2

</div>
</div>
<div class="sect3">
[]{#GUID-7C74ECA4-3645-4756-B8FB-63D84480F4AD}

### Simple Authentication and Security Layer (SASL) {#JSSEC-GUID-7C74ECA4-3645-4756-B8FB-63D84480F4AD .sect3}

<div>
Simple Authentication and Security Layer (SASL) is an Internet standard
that specifies a protocol for authentication and optional establishment
of a security layer between client and server applications. SASL defines
how authentication data is to be exchanged, but does not itself specify
the contents of that data. It is a framework into which specific
authentication mechanisms that specify the contents and semantics of the
authentication data can fit. There are a number of standard SASL
mechanisms defined by the Internet community for various security levels
and deployment scenarios.

The Java SASL API, which is in the
[<span class="apiname">java.security.sasl</span>](https://docs.oracle.com/javase/10/docs/api/java.security.sasl-summary.html)
module, defines classes and interfaces for applications that use SASL
mechanisms. It is defined to be mechanism-neutral; an application that
uses the API need not be hardwired into using any particular SASL
mechanism. Applications can select the mechanism to use based on desired
security features. The API supports both client and server applications.
The `javax.security.sasl.Sasl`{.codeph} class is used to create
`SaslClient`{.codeph} and `SaslServer`{.codeph} objects.

SASL mechanism implementations are supplied in provider packages. Each
provider may support one or more SASL mechanisms and is registered and
invoked via the standard provider architecture.

The Java platform includes a built-in provider that implements the
following SASL mechanisms:

-   CRAM-MD5, DIGEST-MD5, EXTERNAL, GSSAPI, NTLM, and PLAIN client
    mechanisms
-   CRAM-MD5, DIGEST-MD5, GSSAPI, and NTLM server mechanisms

</div>
</div>
<div class="sect3">
[]{#GUID-40739A87-4E28-4195-A156-AFA008CF3B2A}

### Generic Security Service API and Kerberos {#JSSEC-GUID-40739A87-4E28-4195-A156-AFA008CF3B2A .sect3}

<div>
The Java platform contains an API with the Java language bindings for
the Generic Security Service Application Programming Interface
(GSS-API), which is in the `java.security.jgss`{.codeph} module. GSS-API
offers application programmers uniform access to security services atop
a variety of underlying security mechanisms. The Java GSS-API currently
requires use of a Kerberos v5 mechanism, and the Java platform includes
a built-in implementation of this mechanism. At this time, it is not
possible to plug in additional mechanisms.

<div class="p">
<div class="infoboxnote" id="GUID-40739A87-4E28-4195-A156-AFA008CF3B2A__GUID-45ABD440-FDD0-47DB-AD11-CB3BDB67A92C">
Note:

The `Krb5LoginModule`{.codeph} mentioned in the section
[Authentication](java-security-overview1.htm#GUID-F8BE6C49-3506-4D1A-8E4E-053CA439D1E2)
can be used in conjunction with the GSS Kerberos mechanism.

</div>
</div>
The Java platform also includes a built-in implementation of the Simple
and Protected GSS-API Negotiation Mechanism (SPNEGO) GSS-API mechanism.

Before two applications can use GSS-API to securely exchange messages
between them, they must establish a joint security context. The context
encapsulates shared state information that might include, for example,
cryptographic keys. Both applications create and use an
`org.ietf.jgss.GSSContext`{.codeph} object to establish and maintain the
shared information that makes up the security context. Once a security
context has been established, it can be used to prepare secure messages
for exchange.

The Java GSS APIs are in the `org.ietf.jgss`{.codeph} package. The Java
platform also defines basic Kerberos classes, like
`KerberosPrincipal`{.codeph}, `KerberosTicket`{.codeph},
`KerberosKey`{.codeph}, and `KeyTab`{.codeph}, which are located in the
`javax.security.auth.kerberos`{.codeph} package.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-BBEC2DC8-BA00-42B1-B52A-A49488FCF8FE}

Access Control {#JSSEC-GUID-BBEC2DC8-BA00-42B1-B52A-A49488FCF8FE .sect2}
--------------

<div>
The access control architecture in the Java platform protects access to
sensitive resources (for example, local files) or sensitive application
code (for example, methods in a class). All access control decisions are
mediated by a security manager, represented by the
`java.lang.SecurityManager`{.codeph} class. A `SecurityManager`{.codeph}
must be installed into the Java runtime in order to activate the access
control checks.

Java applets and Java Web Start applications are automatically run with
a `SecurityManager`{.codeph} installed. However, local applications
executed via the `java`{.codeph} command are by default not run with a
`SecurityManager`{.codeph} installed. In order to run local applications
with a `SecurityManager`{.codeph}, either the application itself must
programmatically set one via the `setSecurityManager`{.codeph} method
(in the `java.lang.System`{.codeph} class), or `java`{.codeph} must be
invoked with a `-Djava.security.manager`{.codeph} argument on the
command line.

</div>
<div class="sect3">
[]{#GUID-7A49C00B-BEA6-4050-9E32-6168211585F7}

### Permissions {#JSSEC-GUID-7A49C00B-BEA6-4050-9E32-6168211585F7 .sect3}

<div>
A permission represents access to a system resource. In order for a
resource access to be allowed for an applet (or an application running
with a security manager), the corresponding permission must be
explicitly granted to the code attempting the access.

When Java code is loaded by a class loader into the Java runtime, the
class loader automatically associates the following information with
that code:

-   Where the code was loaded from
-   Who signed the code (if anyone)
-   Default permissions granted to the code

This information is associated with the code regardless of whether the
code is downloaded over an untrusted network (e.g., an applet) or loaded
from the filesystem (e.g., a local application). The location from which
the code was loaded is represented by a URL, the code signer is
represented by the signer\'s certificate chain, and default permissions
are represented by `java.security.Permission`{.codeph} objects.

The default permissions automatically granted to downloaded code include
the ability to make network connections back to the host from which it
originated. The default permissions automatically granted to code loaded
from the local filesystem include the ability to read files from the
directory it came from, and also from subdirectories of that directory.

Note that the identity of the user executing the code is not available
at class loading time. It is the responsibility of application code to
authenticate the end user if necessary (see the section
[Authentication](java-security-overview1.htm#GUID-F8BE6C49-3506-4D1A-8E4E-053CA439D1E2)).
Once the user has been authenticated, the application can dynamically
associate that user with executing code by invoking the `doAs`{.codeph}
method in the `javax.security.auth.Subject`{.codeph} class.

</div>
</div>
<div class="sect3">
[]{#GUID-5FB6B917-DDFE-42F5-9233-8E6250C1EA93}

### Security Policy {#JSSEC-GUID-5FB6B917-DDFE-42F5-9233-8E6250C1EA93 .sect3}

<div>
A limited set of default permissions are granted to code by class
loaders. Administrators have the ability to flexibly manage additional
code permissions via a security policy.

<span>Java SE</span> encapsulates the notion of a security policy in the
`java.security.Policy`{.codeph} class. There is only one
`Policy`{.codeph} object installed into the Java runtime at any given
time. The basic responsibility of the `Policy`{.codeph} object is to
determine whether access to a protected resource is permitted to code
(characterized by where it was loaded from, who signed it, and who is
executing it). How a `Policy`{.codeph} object makes this determination
is implementation-dependent. For example, it may consult a database
containing authorization data, or it may contact another service.

<span>Java SE</span> includes a default `Policy`{.codeph} implementation
that reads its authorization data from one or more ASCII (UTF-8) files
configured in the security properties file. These policy files contain
the exact sets of permissions granted to code: specifically, the exact
sets of permissions granted to code loaded from particular locations,
signed by particular entities, and executing as particular users. The
policy entries in each file must conform to a documented proprietary
syntax, and may be composed via a simple text editor or the graphical
`policytool`{.codeph} utility.

<div class="infoboxnote" id="GUID-5FB6B917-DDFE-42F5-9233-8E6250C1EA93__GUID-D3875F06-72F8-4E32-976D-4F0CA67889C2">
Note:

The `policytool`{.codeph} is deprecated and marked for removal in the
next major JDK release.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-2779612B-8DE1-49D3-8EC3-C678C3A9FC35}

### Access Control Enforcement {#JSSEC-GUID-2779612B-8DE1-49D3-8EC3-C678C3A9FC35 .sect3}

<div>
The Java runtime keeps track of the sequence of Java calls that are made
as a program executes. When access to a protected resource is requested,
the entire call stack, by default, is evaluated to determine whether the
requested access is permitted.

As mentioned previously, resources are protected by the
`SecurityManager`{.codeph}. Security-sensitive code in the JDK and in
applications protects access to resources via code like the following:

``` {.codeblock dir="ltr"}
SecurityManager sm = System.getSecurityManager();
if (sm != null) {
   sm.checkPermission(perm);
}
```

The <span class="apiname">Permission</span> object `perm`{.codeph}
corresponds to the requested access. For example, if an attempt is made
to read the file `/tmp/abc`, the permission may be constructed as
follows:

``` {.codeblock dir="ltr"}
Permission perm = new java.io.FilePermission("/tmp/abc", "read");
```

The default implementation of `SecurityManager`{.codeph} delegates its
decision to the `java.security.AccessController`{.codeph}
implementation. The `AccessController`{.codeph} traverses the call
stack, passing to the installed security `Policy`{.codeph} each code
element in the stack, along with the requested permission (for example,
the `FilePermission`{.codeph} in the previous example). The
`Policy`{.codeph} determines whether the requested access is granted,
based on the permissions configured by the administrator. If access is
not granted, the `AccessController`{.codeph} throws a
`java.lang.SecurityException.`{.codeph}

[Figure
1-4](java-security-overview1.htm#GUID-2779612B-8DE1-49D3-8EC3-C678C3A9FC35__GUID-33C5A83F-81FF-42DA-8A2C-D726305C9F98)
illustrates access control enforcement. In this particular example,
there are initially two elements on the call stack, `ClassA`{.codeph}
and `ClassB`{.codeph}. `ClassA`{.codeph} invokes a method in
`ClassB`{.codeph}, which then attempts to access the file `/tmp/abc` by
creating an instance of `java.io.FileInputStream`{.codeph}. The
`FileInputStream`{.codeph} constructor creates a
`FilePermission`{.codeph}, `perm`{.codeph}, as shown above, and then
passes `perm`{.codeph} to the `SecurityManager`{.codeph} class\'s
`checkPermission`{.codeph} method. In this particular case, only the
permissions for `ClassA`{.codeph} and `ClassB`{.codeph} need to be
checked, because all classes in the `java.base`{.codeph} module,
including `FileInputStream`{.codeph}, `SecurityManager`{.codeph}, and
`AccessController`{.codeph}, automatically receives all permissions.

In this example, `ClassA`{.codeph} and `ClassB`{.codeph} have different
code characteristics -- they come from different locations and have
different signers. Each may have been granted a different set of
permissions. The `AccessController`{.codeph} only grants access to the
requested file if the `Policy`{.codeph} indicates that both classes have
been granted the required `FilePermission`{.codeph}.

<div class="figure" id="GUID-2779612B-8DE1-49D3-8EC3-C678C3A9FC35__GUID-33C5A83F-81FF-42DA-8A2C-D726305C9F98">
Figure 1-4 Controlling Access to Resources

\
![Description of Figure 1-4
follows](img/controlling-access-resources.jpg "Description of Figure 1-4 follows")\
[Description of \"Figure 1-4 Controlling Access to
Resources\"](img_text/controlling-access-resources.htm)\

</div>
<!-- class="figure" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-BFC0C7D7-72B5-4DEC-ACF4-5DF4F7925303}

XML Signature {#JSSEC-GUID-BFC0C7D7-72B5-4DEC-ACF4-5DF4F7925303 .sect2}
-------------

<div>
The Java XML Digital Signature API is a standard Java API for generating
and validating XML Signatures.

XML Signatures can be applied to data of any type, XML or binary (see
[XML Signature Syntax and
Processing](http://www.w3.org/TR/xmldsig-core/)). The resulting
signature is represented in XML. An XML Signature can be used to secure
your data and provide data integrity, message authentication, and signer
authentication.

The API is designed to support all of the required or recommended
features of the W3C Recommendation for XML-Signature Syntax and
Processing. The API is extensible and pluggable and is based on the Java
Cryptography Service Provider Architecture.

The Java XML Digital Signature API, which is in the
[<span class="apiname">java.xml.crypto</span>](https://docs.oracle.com/javase/10/docs/api/java.xml.crypto-summary.html)
module, consists of six packages:

-   `javax.xml.crypto`{.codeph}
-   `javax.xml.crypto.dsig`{.codeph}
-   `javax.xml.crypto.dsig.keyinfo`{.codeph}
-   `javax.xml.crypto.dsig.spec`{.codeph}
-   `javax.xml.crypto.dom`{.codeph}
-   `javax.xml.crypto.dsig.dom`{.codeph}

</div>
</div>
<div class="sect2">
[]{#GUID-49933D9B-83AF-4A3D-94A3-00061A9A212F}

Additional Information about Java Security {#JSSEC-GUID-49933D9B-83AF-4A3D-94A3-00061A9A212F .sect2}
------------------------------------------

<div>
Find additional Java security documentation at [Java SE
Security](http://www.oracle.com/technetwork/java/javase/tech/index-jsp-136007.html).

<div class="infoboxnote" id="GUID-49933D9B-83AF-4A3D-94A3-00061A9A212F__GUID-D3F86052-D6D7-4F6A-9485-44EBB0B27F14">
Note:

Historically, as new types of security services were added to <span>Java
SE</span> (sometimes initially as extensions), various acronyms were
used to refer to them. Since these acronyms are still in use in the Java
security documentation, here is an explanation of what they represent:

-   JSSE (Java Secure Socket Extension) refers to the SSL-related
    services as described in the section [SSL, TLS, and DTLS
    Protocols](java-security-overview1.htm#GUID-FCF419A7-B856-46DD-A36F-C6F88F9AF37F "The JDK provides APIs and an implementation of the SSL, TLS, and DTLS protocols that includes functionality for data encryption, message integrity, and server and client authentication. Applications can use SSL/TLS/DTLS to provide for the secure passage of data between two peers over any application protocol, such as HTTP on top of TCP/IP.")

-   JCE (Java Cryptography Extension) refers to cryptographic services
    as described in the section [Java
    Cryptography](java-security-overview1.htm#GUID-C6D250FC-F147-4284-A6BF-8384DFD39DA6 "The Java cryptography architecture is a framework for accessing and developing cryptographic functionality for the Java platform.")

-   JAAS (Java Authentication and Authorization Service) refers to the
    authentication and user-based access control services as described
    in the sections
    [Authentication](java-security-overview1.htm#GUID-F8BE6C49-3506-4D1A-8E4E-053CA439D1E2)
    and [Access
    Control](java-security-overview1.htm#GUID-BBEC2DC8-BA00-42B1-B52A-A49488FCF8FE "The access control architecture in the Java platform protects access to sensitive resources (for example, local files) or sensitive application code (for example, methods in a class). All access control decisions are mediated by a security manager, represented by the java.lang.SecurityManager class. A SecurityManager must be installed into the Java runtime in order to activate the access control checks."),
    respectively

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-CF323502-F719-4618-91FE-4D37CB57FF24}

Java Security Classes Summary {#JSSEC-GUID-CF323502-F719-4618-91FE-4D37CB57FF24 .sect2}
-----------------------------

<div>
The following table describes some of the names, packages, and usage of
the Java security classes and interfaces..

<div class="section">
<div class="tblformalwide" id="GUID-CF323502-F719-4618-91FE-4D37CB57FF24__GUID-88D2FAB1-3189-4F9E-AB5A-481276277F62">
Table 1-3 Java security packages and classes

  Package                                   Class/Interface Name                  Usage                                                                                                                   Module
  ----------------------------------------- ------------------------------------- ----------------------------------------------------------------------------------------------------------------------- -------------------------------
  `java.lang`{.codeph}                      `SecurityException`{.codeph}          Indicates a security violation                                                                                          `java.base`{.codeph}
  `java.lang`{.codeph}                      `SecurityManager`{.codeph}            Mediates all access control decisions                                                                                   `java.base`{.codeph}
  `java.lang`{.codeph}                      `System`{.codeph}                     Installs the SecurityManager                                                                                            `java.base`{.codeph}
  `java.security`{.codeph}                  `AccessController`{.codeph}           Called by default implementation of SecurityManager to make access control decisions                                    `java.base`{.codeph}
  `java.security`{.codeph}                  `DomainLoadStoreParameter`{.codeph}   Stores parameters for the Domain keystore (DKS)                                                                         `java.base`{.codeph}
  `java.security`{.codeph}                  `Key`{.codeph}                        Represents a cryptographic key                                                                                          `java.base`{.codeph}
  `java.security`{.codeph}                  `KeyStore`{.codeph}                   Represents a repository of keys and trusted certificates                                                                `java.base`{.codeph}
  `java.security`{.codeph}                  `MessageDigest`{.codeph}              Represents a message digest                                                                                             `java.base`{.codeph}
  `java.security`{.codeph}                  `Permission`{.codeph}                 Represents access to a particular resource                                                                              `java.base`{.codeph}
  `java.security`{.codeph}                  `PKCS12Attribute`{.codeph}            Supports attributes in PKCS12 keystores                                                                                 `java.base`{.codeph}
  `java.security`{.codeph}                  `Policy`{.codeph}                     Encapsulates the security policy                                                                                        `java.base`{.codeph}
  `java.security`{.codeph}                  `Provider`{.codeph}                   Encapsulates security service implementations                                                                           `java.base`{.codeph}
  `java.security`{.codeph}                  `Security`{.codeph}                   Manages security providers and Security Properties                                                                      `java.base`{.codeph}
  `java.security`{.codeph}                  `Signature`{.codeph}                  Creates and verifies digital signatures                                                                                 `java.base`{.codeph}
  `java.security.cert`{.codeph}             `Certificate`{.codeph}                Represents a public key certificate                                                                                     `java.base`{.codeph}
  `java.security.cert`{.codeph}             `CertStore`{.codeph}                  Represents a repository of unrelated and typically untrusted certificates                                               `java.base`{.codeph}
  `java.security.cert`{.codeph}             `CRL`{.codeph}                        Represents a CRL                                                                                                        `java.base`{.codeph}
  `javax.crypto`{.codeph}                   `Cipher`{.codeph}                     Performs encryption and decryption                                                                                      `java.base`{.codeph}
  `javax.crypto`{.codeph}                   `KeyAgreement`{.codeph}               Performs a key exchange                                                                                                 `java.base`{.codeph}
  `javax.net.ssl`{.codeph}                  `KeyManager`{.codeph}                 Manages keys used to perform SSL/TLS authentication                                                                     `java.base`{.codeph}
  `javax.net.ssl`{.codeph}                  `SSLEngine`{.codeph}                  Produces/consumes SSL/TLS packets, allowing the application freedom to choose a transport mechanism                     `java.base`{.codeph}
  `javax.net.ssl`{.codeph}                  `SSLSocket`{.codeph}                  Represents a network socket that encapsulates SSL/TLS support on top of a normal stream socket                          `java.base`{.codeph}
  `javax.net.ssl`{.codeph}                  `TrustManager`{.codeph}               Makes decisions about who to trust in SSL/TLS interactions (for example, based on trusted certificates in key stores)   `java.base`{.codeph}
  `javax.security.auth`{.codeph}            `Subject`{.codeph}                    Represents a user                                                                                                       `java.base`{.codeph}
  `javax.security.auth.kerberos`{.codeph}   `KerberosPrincipal`{.codeph}          Represents a Kerberos principal                                                                                         `java.base`{.codeph}
  `javax.security.auth.kerberos`{.codeph}   `KerberosTicket`{.codeph}             Represents a Kerberos ticket                                                                                            `java.base`{.codeph}
  `javax.security.auth.kerberos`{.codeph}   `KerberosKey`{.codeph}                Represents a Kerberos key                                                                                               `java.base`{.codeph}
  `javax.security.auth.kerberos`{.codeph}   `KerberosTab`{.codeph}                Represents a Kerberos keytab file                                                                                       `java.base`{.codeph}
  `javax.security.auth.login`{.codeph}      `LoginContext`{.codeph}               Supports pluggable authentication                                                                                       `java.base`{.codeph}
  `javax.security.auth.spi`{.codeph}        `LoginModule`{.codeph}                Implements a specific authentication mechanism                                                                          `java.base`{.codeph}
  `javax.security.sasl`{.codeph}            `Sasl`{.codeph}                       Creates SaslClient and SaslServer objects                                                                               `java.security.sasl`{.codeph}
  `javax.security.sasl`{.codeph}            `SaslClient`{.codeph}                 Performs SASL authentication as a client                                                                                `java.security.sasl`{.codeph}
  `javax.security.sasl`{.codeph}            `SaslServer`{.codeph}                 Performs SASL authentication as a server                                                                                `java.security.sasl`{.codeph}
  `org.ietf.jgss`{.codeph}                  `GSSContext`{.codeph}                 Encapsulates a GSS-API security context and provides the security services available via the context                    `java.security.jgss`{.codeph}
  `com.sun.security.auth.module`{.codeph}   `JndiLoginModule`{.codeph}            Performs username/password authentication using LDAP or NIS                                                             `jdk.security.auth`{.codeph}
  `com.sun.security.auth.module`{.codeph}   `KeyStoreLoginModule`{.codeph}        Performs authentication based on key store login                                                                        `jdk.security.auth`{.codeph}
  `com.sun.security.auth.module`{.codeph}   `Krb5LoginModule`{.codeph}            Performs authentication using Kerberos protocols                                                                        `jdk.security.auth`{.codeph}

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-E1A1E8ED-B39F-404B-8036-637F697B45A2}

Deprecated Security APIs Marked for Removal {#JSSEC-GUID-E1A1E8ED-B39F-404B-8036-637F697B45A2 .sect2}
-------------------------------------------

<div>
The following APIs are deprecated and eligible to be removed in a future
release.

<div class="section">
You can check the API dependencies using the `jdeprscan`{.codeph} tool.
See [jdeprscan](olink:JSWOR-GUID-2B7588B0-92DB-4A88-88D4-24D183660A62)
in <span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

The following classes are deprecated and marked for removal:

-   <span class="apiname">com.sun.security.auth.PolicyFile</span>
-   <span class="apiname">com.sun.security.auth.SolarisNumericGroupPrincipal</span>
-   <span class="apiname">com.sun.security.auth.SolarisNumericUserPrincipal</span>
-   <span class="apiname">com.sun.security.auth.SolarisPrincipal</span>
-   <span class="apiname">com.sun.security.auth.X500Principal</span>
-   <span class="apiname">com.sun.security.auth.module.SolarisLoginModule</span>
-   <span class="apiname">com.sun.security.auth.module.SolarisSystem</span>

The following methods are deprecated and marked for removal:

-   <span class="apiname">java.lang.SecurityManager.getInCheck</span>
-   <span class="apiname">java.lang.SecurityManager.checkMemberAccess</span>
-   <span class="apiname">java.lang.SecurityManager.classDepth</span>
-   <span class="apiname">java.lang.SecurityManager.currentClassLoader</span>
-   <span class="apiname">java.lang.SecurityManager.currentLoadedClass</span>
-   <span class="apiname">java.lang.SecurityManager.inClass</span>
-   <span class="apiname">java.lang.SecurityManager.inClassLoader</span>
-   <span class="apiname">java.lang.SecurityManager.checkAwtEventQueueAccess</span>
-   <span class="apiname">java.lang.SecurityManager.checkTopLevelWindow</span>
-   <span class="apiname">java.lang.SecurityManager.checkSystemClipboardAccess</span>

The following field is deprecated and marked for removal:

-   <span class="apiname">java.lang.SecurityManager.incheck</span>

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-86FA42B9-E18B-4E2B-9F2D-7567320B53AA}

Security Tools Summary {#JSSEC-GUID-86FA42B9-E18B-4E2B-9F2D-7567320B53AA .sect2}
----------------------

<div>
The following tables describe Java security and Kerberos-related tools.

<div class="section">
See [Security Tools and
Commands](olink:JSWOR-GUID-F73EC9CE-C422-4EDB-B3E6-AA3A3A1DDB8E) in
<span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

<div class="tblformal" id="GUID-86FA42B9-E18B-4E2B-9F2D-7567320B53AA__GUID-AE24FA75-05AF-41A1-83E7-C39207835A71">
Table 1-4 Java Security Tools

+-----------------------------------+-----------------------------------+
| Tool                              | Usage                             |
+:==================================+:==================================+
| `jar`{.codeph}                    | Creates Java Archive (JAR) files  |
+-----------------------------------+-----------------------------------+
| `jarsigner`{.codeph}              | Signs and verifies signatures on  |
|                                   | JAR files                         |
+-----------------------------------+-----------------------------------+
| `keytool`{.codeph}                | Creates and manages key stores    |
+-----------------------------------+-----------------------------------+
| `policytool`{.codeph}             | Creates and edits policy files    |
|                                   | for use with default Policy       |
|                                   | implementation                    |
|                                   | <div class="infoboxnote" id="GUID |
|                                   | -86FA42B9-E18B-4E2B-9F2D-7567320B |
|                                   | 53AA__GUID-D3875F06-72F8-4E32-976 |
|                                   | D-4F0CA67889C2">                  |
|                                   | Note:                             |
|                                   |                                   |
|                                   | `policytool`{.codeph} is          |
|                                   | deprecated and marked for         |
|                                   | removal.                          |
|                                   | </div>                            |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

There are also three Kerberos-related tools that are shipped with the
JDK for Windows. Equivalent functionality is provided in tools of the
same name that are automatically part of the Solaris and Linux operating
environments.

<div class="tblformal" id="GUID-86FA42B9-E18B-4E2B-9F2D-7567320B53AA__GUID-2761073A-DA7E-4885-8B08-E15CAE52E897">
Table 1-5 Kerberos-related Tools

  Tool               Usage
  ------------------ ---------------------------------------------------------------------------
  `kinit`{.codeph}   Obtains and caches Kerberos ticket-granting tickets
  `klist`{.codeph}   Lists entries in the local Kerberos credentials cache and key table
  `ktab`{.codeph}    Manages the names and service keys stored in the local Kerberos key table

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-2EF0B3B8-9F3A-41CF-A7DA-63DB52180084}

Built-In Providers {#JSSEC-GUID-2EF0B3B8-9F3A-41CF-A7DA-63DB52180084 .sect2}
------------------

<div>
<div class="section">
The <span>Java SE</span> implementation from Oracle includes a number of
built-in provider packages. See [JDK Providers
Documentation](oracle-providers.htm#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313 "This document contains the technical details of the providers that are included in the JDK. It is assumed that readers have a strong understanding of the Java Cryptography Architecture and Provider Architecture.").

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
| -- ----------------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
|  --                  | e | )\                   |
|          [![Previous | L |             <span cl |
| ](../../dcommon/gifs | o | ass="icon">Contents< |
| /leftnav.gif)\       | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
| [![Next](../../dcomm | ] | -------------------- |
| on/gifs/rightnav.gif | ( | -------------------- |
| )\                   | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](g | . |                      |
| eneral-security1.htm | . |                      |
| )   <span class="ico | / |                      |
| n">Next</span>](java | d |                      |
| -se-platform-securit | c |                      |
| y-architecture.htm)  | o |                      |
|                      | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| -- ----------------- | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
|  --                  | s |                      |
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
