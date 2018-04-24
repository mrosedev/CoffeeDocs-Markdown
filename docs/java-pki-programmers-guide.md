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

  --------------------------------------------------------------------------- -------------------------------------------------------------------------------------- --
                 [![Previous](../../dcommon/gifs/leftnav.gif)\                                      [![Next](../../dcommon/gifs/rightnav.gif)\                       
   <span class="icon">Previous</span>](troubleshooting-jsse-sample-code.htm)   <span class="icon">Next</span>](java-sasl-api-programming-and-deployment-guide1.htm)  
  --------------------------------------------------------------------------- -------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-650D0D53-B617-4055-AFD3-AF5C2629CBBF}<!-- End Header -->

<span class="enumeration_chapter">10 </span>Java PKI Programmers Guide {#JSSEC-GUID-650D0D53-B617-4055-AFD3-AF5C2629CBBF .sect1}
======================================================================

<div>
The Java Certification Path API consists of classes and interfaces for
handling certification paths, which are also called certification
chains. If a certification path meets certain validation rules, it may
be used to securely establish the mapping of a public key to a subject.

<div class="section">
Topics

[PKI Programmers Guide
Overview](java-pki-programmers-guide.htm#GUID-D6A18B1E-A2A8-4CA2-BD18-514CD807810E "The Java Certification Path API defines interfaces and abstract classes for creating, building, and validating certification paths.  Implementations may be plugged in using a provider-based interface.")

[Core Classes and
Interfaces](java-pki-programmers-guide.htm#GUID-271526C4-6095-4233-9F7F-0CD0C62BDA93 "The core classes of the Java Certification Path API consist of interfaces and classes that support certification path functionality in an algorithm and implementation-independent manner.")

[Implementing a Service
Provider](java-pki-programmers-guide.htm#GUID-266DD62E-39A7-435B-90DF-7EB1425D56E1 "Experienced programmers can create their own provider packages supplying certification path service implementations.")

[Appendix A: Standard
Names](java-pki-programmers-guide.htm#GUID-EF1585DC-20BF-4140-B71E-0A8528D4A57D "The Java Certification Path API requires and utilizes a set of standard names for certification path validation algorithms, encodings and certificate storage types.")

[Appendix B: CertPath Implementation in SUN
Provider](java-pki-programmers-guide.htm#GUID-EB250086-0AC1-4D60-AE2A-FC7461374746)

[Appendix C: OCSP
Support](java-pki-programmers-guide.htm#GUID-E6E737DB-4000-4005-969E-BCD0238B1566 "Client-side support for the On-Line Certificate Status Protocol (OCSP) as defined in RFC 2560 is supported.")

[Appendix D: CertPath Implementation in JdkLDAP
Provider](java-pki-programmers-guide.htm#GUID-FF62B0E3-E57A-4F40-970A-0481AF750CCD "The JdkLDAP provider supports the LDAP implementation of the CertStore engine class.")

[Appendix E: Disabling Cryptographic
Algorithms](java-pki-programmers-guide.htm#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3 "The jdk.certpath.disabledAlgorithms Security Property contains a list of cryptographic algorithms and key size constraints that are considered weak or broken. Certificates and other data (CRLs, OCSPResponses) containing any of these algorithms or key sizes will be blocked during certification path building and validation. This property is used by Oracle's PKIX implementation, other implementations might not examine and use it.")

</div>
<!-- class="section" -->

</div>
<div class="sect2">
[]{#GUID-D6A18B1E-A2A8-4CA2-BD18-514CD807810E}

PKI Programmers Guide Overview {#JSSEC-GUID-D6A18B1E-A2A8-4CA2-BD18-514CD807810E .sect2}
------------------------------

<div>
The Java Certification Path API defines interfaces and abstract classes
for creating, building, and validating certification paths. 
Implementations may be plugged in using a provider-based interface.

<div class="section">
This API is based on the [Cryptographic Service
Providers](java-cryptography-architecture-jca-reference-guide.htm#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920)
architecture, described in the<cite> Java Cryptography Architecture
Reference Guide</cite>, and includes algorithm-specific classes for
building and validating X.509 certification paths according to the PKIX
standards. The PKIX standards were developed by the [IETF PKIX working
group](http://datatracker.ietf.org/wg/pkix/charter/).

This API was originally specified using the [Java Community
Process](http://jcp.org/en/home/index) program as Java Specification
Request (JSR) 000055. The API was included in the Java SDK, starting
with Java SE Development Kit (JDK) 1.4. See [JSR 55: Certification Path
API](http://jcp.org/en/jsr/detail?id=55).

</div>
<!-- class="section" -->

<div class="section">
Who Should Read This Document

This document is intended for two types of experienced developers:

1.  Those who want to design secure applications that build or validate
    certification paths.

2.  Those who want to write a service provider implementation for
    building or validating certification paths.

</div>
<!-- class="section" -->

<div class="section" id="GUID-D6A18B1E-A2A8-4CA2-BD18-514CD807810E__GUID-4BEA98CF-CE46-4BB2-B7D0-E7170C4B955C">
This document assumes that you have already read [Cryptographic Service
Providers](java-cryptography-architecture-jca-reference-guide.htm#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920).

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-2EFB901C-9ED1-4823-9311-B05B49E34AEA}

### Introduction to Public Key Certificates {#JSSEC-GUID-2EFB901C-9ED1-4823-9311-B05B49E34AEA .sect3}

<div>
Users of public key applications and systems must be confident that a
subject\'s public key is genuine, i.e., that the associated private key
is owned by the subject. Public key certificates are used to establish
this trust.

A <span class="bold">public key (or identity) certificate</span> is a
binding of a public key to an identity, which is digitally signed by the
private key of another entity, often called a
<span class="bold">Certification Authority</span> (CA). For the
remainder of this section, the term CA is used to refer to an entity
that signs a certificate.

If the user does not have a trusted copy of the public key of the CA
that signed the subject\'s public key certificate, then another public
key certificate vouching for the signing CA is required. This logic can
be applied recursively, until a chain of certificates (or
<span class="bold">a certification path</span>) is discovered from a
<span class="bold">trust anchor</span> or a
<span class="bold">most-trusted CA</span> to the target subject
(commonly referred to as the <span class="bold">end-entity</span>). The
<span class="bold">most-trusted CA</span> is usually specified by a
certificate issued to a CA that the user directly trusts. In general, a
certification path is an ordered list of certificates, usually comprised
of the end-entity\'s public key certificate and zero or more additional
certificates. A certification path typically has one or more encodings,
allowing it to be safely transmitted across networks and to different
operating system architectures.

The following figure illustrates a certification path from a
most-trusted CA\'s public key (CA 1) to the target subject (Alice). The
certification path establishes trust in Alice\'s public key through an
intermediate CA named CA2.

<div class="figure" id="GUID-2EFB901C-9ED1-4823-9311-B05B49E34AEA__GUID-9B683BE7-5148-49FD-A561-A5E6C220F7F7">
Figure 10-1 Certification Path from CA\'s Public Key (CA 1) to the
Target Subject

![Description of Figure 10-1
follows](img/publickey_pki.png "Description of Figure 10-1 follows")\
[Description of \"Figure 10-1 Certification Path from CA\'s Public Key
(CA 1) to the Target Subject\"](img_text/publickey_pki.htm)

</div>
<!-- class="figure" -->

A certification path must be validated before it can be relied on to
establish trust in a subject\'s public key. Validation can consist of
various checks on the certificates contained in the certification path,
such as verifying the signatures and checking that each certificate has
not been revoked. The PKIX standards define an algorithm for validating
certification paths consisting of X.509 certificates.

Often a user may not have a certification path from a most-trusted CA to
the subject. Providing services to build or discover certification paths
is an important feature of public key enabled systems. [RFC
2587](http://www.ietf.org/rfc/rfc2587.txt) defines an LDAP (Lightweight
Directory Access Protocol) schema definition that facilitates the
discovery of X.509 certification paths using the LDAP directory service
protocol.

Building and validating certification paths is an important part of many
standard security protocols such as SSL/TLS/DTLS, S/MIME, and IPsec. The
Java Certification Path API provides a set of classes and interfaces for
developers who need to integrate this functionality into their
applications. This API benefits two types of developers: those who need
to write service provider implementations for a specific certification
path building or validation algorithm; and those who need to access
standard algorithms for creating, building, and validating certification
paths in an implementation-independent manner.

</div>
</div>
<div class="sect3">
[]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23}

### X.509 Certificates and Certificate Revocation Lists (CRLs) {#JSSEC-GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23 .sect3}

<div>
A public-key certificate is a digitally signed statement from one entity
saying that the public key and some other information of another entity
has some specific value.

<div class="section">
The following table defines some of the key terms:

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-AE06C840-0CDB-4B6E-8704-6D4748E6E0F0}<span class="variable">Public Keys</span>
:   These are numbers associated with a particular entity, and are
    intended to be known to everyone who needs to have trusted
    interactions with that entity. Public keys are used to verify
    signatures.

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-BD9AF829-3573-4518-B55C-7176F73B1766}<span class="variable">Digitally Signed</span>
:   If some data is <span class="variable">digitally signed</span> it
    has been stored with the \"identity\" of an entity, and a signature
    that proves that entity knows about the data. The data is rendered
    unforgeable by signing with the entitys\' private key.

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-D9C21B0B-3E70-4DC5-AE83-BB794E175306}<span class="variable">Identity</span>
:   A known way of addressing an entity. In some systems the identity is
    the public key, in others it can be anything from a UNIX UID to an
    Email address to an X.509 Distinguished Name.

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-02ECE861-7359-4FF7-8A78-EE7F9B412062}<span class="variable">Signature</span>
:   A signature is computed over some data using the private key of an
    entity (the signer).

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-27909E67-E056-4AC0-8BBB-26C32D3D2ACF}<span class="variable">Private Keys</span>
:   These are numbers, each of which is supposed to be known only to the
    particular entity whose private key it is (that is, it\'s supposed
    to be kept secret). Private and public keys exist in pairs in all
    public key cryptography systems (also referred to as \"public key
    crypto systems\"). In a typical public key crypto system, such as
    DSA, a private key corresponds to exactly one public key. Private
    keys are used to compute signatures.

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-A64089C4-83C1-4550-9D16-28732ADA7947}<span class="variable">Entity</span>
:   An entity is a person, organization, program, computer, business,
    bank, or something else you are trusting to some degree.

Basically, public key cryptography requires access to users\' public
keys. In a large-scale networked environment it is impossible to
guarantee that prior relationships between communicating entities have
been established or that a trusted repository exists with all used
public keys. Certificates were invented as a solution to this public key
distribution problem. Now a <span class="variable">Certification
Authority</span> (CA) can act as a <span class="variable">Trusted Third
Party</span>. CAs are entities (e.g., businesses) that are trusted to
sign (issue) certificates for other entities. It is assumed that CAs
will only create valid and reliable certificates as they are bound by
legal agreements. There are many public Certification Authorities, such
as [VeriSign](http://www.verisign.com), [Thawte](http://www.thawte.com),
[Entrust](http://www.entrust.com), and so on. You can also run your own
Certification Authority using products such as the Netscape/Microsoft
Certificate Servers or the Entrust CA product for your organization.

</div>
<!-- class="section" -->

<div class="section">
What Applications use Certificates?

Probably the most widely visible application of X.509 certificates today
is in web browsers (such as Mozilla Firefox and Microsoft Internet
Explorer) that support the TLS protocol. TLS (Transport Layer Security)
is a security protocol that provides privacy and authentication for your
network traffic. These browsers can only use this protocol with web
servers that support TLS.

Other technologies that rely on X.509 certificates include:

-   Various code-signing schemes, such as signed Java ARchives, and
    Microsoft Authenticode.
-   Various secure E-Mail standards, such as PEM and S/MIME.

</div>
<!-- class="section" -->

<div class="section">
How do I Get a Certificate?

There are two basic techniques used to get certificates:

-   You can create one yourself (using the right tools, such as
    keytool).
-   You can ask a Certification Authority to issue you one (either
    directly or using a tool such as <span class="bold">keytool</span>
    to generate the request).

The main inputs to the certificate creation process are:

-   Matched <span class="variable">public and private keys</span>,
    generated using some special tools (such as keytool), or a browser.
    <span class="bold">Only the public key is ever shown to anyone
    else.</span> The private key is used to sign data; if someone knows
    your private key, they can masquerade as you \... perhaps forging
    legal documents attributed to you!
-   You need to provide <span class="variable">information about the
    entity being certified</span> (e.g., you). This normally includes
    information such as your name and organizational address. If you ask
    a CA to issue a certificate for you, you will normally need to
    provide proof to show correctness of the information.

If you are asking a CA to issue you a certificate, you provide your
public key and some information about you. You\'ll use a tool (such as
keytool or a browser that supports Certificate Signing Request
generation). to digitally sign this information, and send it to the CA.
The CA will then generate the certificate and return it.

If you\'re generating the certificate yourself, you\'ll take that same
information, add a little more (dates during which the certificate is
valid, a serial number), and just create the certificate using some tool
(such as keytool). Not everyone will accept self-signed certificates;
one part of the value provided by a CA is to serve as a neutral and
trusted introduction service, based in part on their verification
requirements, which are openly published in their Certification Service
Practices (CSP).

</div>
<!-- class="section" -->

<div class="section">
What\'s Inside an X.509 Certificate?

The X.509 standard defines what information can go into a certificate,
and describes how to write it down (the data format). All X.509
certificates have the following data, in addition to the signature:

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-1B3500E7-D036-45DA-BDD4-B6698F4CF5CF}<span class="bold">Version</span>
:   This identifies which version of the X.509 standard applies to this
    certificate, which affects what information can be specified in it.
    Thus far, three versions are defined.

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-1A458D8C-2304-4E0F-BEE6-C7BFD204A10B}<span class="bold">Serial Number</span>
:   The entity that created the certificate is responsible for assigning
    it a serial number to distinguish it from other certificates it
    issues. This information is used in numerous ways, for example when
    a certificate is revoked its serial number is placed in a
    Certificate Revocation List (CRL).

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-0B248269-402E-42E7-A0B3-597ADDE96611}<span class="bold">Signature Algorithm Identifier</span>
:   This identifies the algorithm used by the CA to sign the
    certificate.

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-1BD8A301-9D9B-411D-A04C-51FE3686E206}<span class="bold">Issuer Name</span>
:   The X.500 name of the entity that signed the certificate. This is
    normally a CA. Using this certificate implies trusting the entity
    that signed this certificate. (Note that in some cases, such as
    <span class="variable">root or top-level</span> CA certificates, the
    issuer signs its own certificate.)

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-D359D40A-D9C6-4212-B15D-CEC95618C378}<span class="bold">Validity Period</span>
:   Each certificate is valid only for a limited amount of time. This
    period is described by a start date and time and an end date and
    time, and can be as short as a few seconds or almost as long as a
    century. The validity period chosen depends on a number of factors,
    such as the strength of the private key used to sign the certificate
    or the amount one is willing to pay for a certificate. This is the
    expected period that entities can rely on the public value, if the
    associated private key has not been compromised.

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-01030D38-927F-4C7E-859A-AF25A09F8992}<span class="bold">Subject Name</span>

:   The name of the entity whose public key the certificate identifies.
    This name uses the X.500 standard, so it is intended to be unique
    across the Internet. This is the Distinguished Name (DN) of the
    entity, for example,

    ``` {.oac_no_warn dir="ltr"}
        CN=Java Duke, OU=Java Software Division, O=Sun Microsystems Inc, C=US
    ```

    (These refer to the subject\'s Common Name, Organizational Unit,
    Organization, and Country.)

[<!-- -->]{#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23__GUID-36D2585D-476B-44DC-BDB6-6E2AB2FB112A}<span class="bold">Subject Public Key Information</span>
:   This is the public key of the entity being named, together with an
    algorithm identifier which specifies which public key crypto system
    this key belongs to and any associated key parameters.

<span class="variable">X.509 Version 1</span> has been available since
1988, is widely deployed, and is the most generic.

<span class="variable">X.509 Version 2</span> introduced the concept of
subject and issuer unique identifiers to handle the possibility of reuse
of subject and/or issuer names over time. Most certificate profile
documents strongly recommend that names not be reused, and that
certificates should not make use of unique identifiers. Version 2
certificates are not widely used.

<span class="variable">X.509 Version 3</span> is the most recent (1996)
and supports the notion of extensions, whereby anyone can define an
extension and include it in the certificate. Some common extensions in
use today are: <span class="variable">KeyUsage</span> (limits the use of
the keys to particular purposes such as \"signing-only\") and
<span class="variable">AlternativeNames</span> (allows other identities
to also be associated with this public key, e.g. DNS names, Email
addresses, IP addresses). Extensions can be marked
<span class="variable">critical</span> to indicate that the extension
should be checked and enforced/used. For example, if a certificate has
the KeyUsage extension marked critical and set to \"keyCertSign\" then
if this certificate is presented during SSL communication, it should be
rejected, as the certificate extension indicates that the associated
private key should only be used for signing certificates and not for SSL
use.

All the data in a certificate is encoded using two related standards
called ASN.1/DER. <span class="variable">Abstract Syntax Notation
1</span> describes data. The <cite>Distinguished Encoding Rules</cite>
describe a single way to store and transfer that data.

</div>
<!-- class="section" -->

<div class="section">
What Java API Can Be Used to Access and Manage Certificates?

The Certificate API, found in the
[`java.security.cert`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/cert/package-summary.html)
package, includes the following:

-   <span class="bold">CertificateFactory</span> class defines the
    functionality of a certificate factory, which is used to generate
    certificate, certificate revocation list (CRL), and certification
    path objects from their encoding.
-   <span class="bold">Certificate</span> class is an abstract class for
    managing a variety of certificates. It is an abstraction for
    certificates that have different formats but important common uses.
    For example, different types of certificates, such as X.509 and PGP,
    share general certificate functionality (like encoding and
    verifying) and some types of information like public key.
-   <span class="bold">CRL</span> class is an abstract class for
    managing a variety of Certificate Revocation Lists (CRLs).
-   <span class="bold">X509Certificate</span> class is an abstract class
    for X.509 Certificates. It provides a standard way to access all the
    attributes of an X.509 certificate.
-   <span class="bold">X509Extension</span> interface is an interface
    for an X.509 extension. The extensions defined for X.509 v3
    certificates and v2 CRLs (Certificate Revocation Lists) provide
    mechanisms for associating additional attributes with users or
    public keys, such as for managing the certification hierarchy, and
    for managing CRL distribution.
-   <span class="bold">X509CRL</span> class is an abstract class for an
    X.509 Certificate Revocation List (CRL). A CRL is a time-stamped
    list identifying revoked certificates. It is signed by a
    Certification Authority (CA) and made freely available in a public
    repository.
-   <span class="bold">X509CRLEntry</span> class is an abstract class
    for a CRL entry.

</div>
<!-- class="section" -->

<div class="section">
What Java Tool Can Generate, Display, Import, and Export X.509
Certificates?

There is a tool named
[keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) that
can be used to create public/private key pairs and X.509 v3
certificates, and to manage keystores. Keys and certificates are used to
digitally sign your Java applications and applets (see
[jarsigner](olink:JSWOR-GUID-925E7A1B-B3F3-44D2-8B49-0B3FA2C54864)).

A <span class="variable">keystore</span> is a protected database that
holds keys and certificates. Access to a keystore is guarded by a
password (defined at the time the keystore is created, by the person who
creates the keystore, and changeable only when providing the current
password). In addition, each private key in a keystore can be guarded by
its own password.

Using <span class="bold">keytool</span>, it is possible to display,
import, and export X.509 v1, v2, and v3 certificates stored as files,
and to generate new v3 certificates. For examples, see the \"EXAMPLES\"
section for
[keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) in the
<span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-271526C4-6095-4233-9F7F-0CD0C62BDA93}

Core Classes and Interfaces {#JSSEC-GUID-271526C4-6095-4233-9F7F-0CD0C62BDA93 .sect2}
---------------------------

<div>
The core classes of the Java Certification Path API consist of
interfaces and classes that support certification path functionality in
an algorithm and implementation-independent manner.

<div class="section">
The API builds on and extends the existing `java.security.cert`{.codeph}
package for handling certificates. The core classes can be broken up
into 4 class categories: Basic, Validation, Building, and Storage:

-   [Basic Certification Path
    Classes](java-pki-programmers-guide.htm#GUID-2D30176C-EE5A-41F8-896B-1A16E7F786B8 "The basic certification path classes provide fundamental functionality for encoding and representing certification paths. The key basic class in the Java Certification Path API is CertPath, which encapsulates the universal aspects shared by all types of certification paths. An application uses an instance of the CertificateFactory class to create a CertPath object.")

    -   `CertPath`{.codeph}, `CertificateFactory`{.codeph}, and
        `CertPathParameters`{.codeph}

-   [Certification Path Validation
    Classes](java-pki-programmers-guide.htm#GUID-C825028D-5F30-4041-ACC4-466657F59F02 "The Java Certification Path API includes classes and interfaces for validating certification paths. An application uses an instance of the CertPathValidator class to validate a CertPath object. If successful, the result of the validation algorithm is returned in an object implementing the CertPathValidatorResult interface.")

    -   `CertPathValidator`{.codeph},
        `CertPathValidatorResult`{.codeph}, and
        `CertPathChecker`{.codeph}

-   [Certification Path Building
    Classes](java-pki-programmers-guide.htm#GUID-CBABC770-E714-4E6C-AD40-EA680BE91C20 "The Java Certification Path API includes classes for building (or discovering) certification paths. An application uses an instance of the CertPathBuilder class to build a CertPath object. If successful, the result of the build is returned in an object implementing the CertPathBuilderResult interface.")

    -   `CertPathBuilder`{.codeph}, and `CertPathBuilderResult`{.codeph}

-   [Certificate/CRL Storage
    Classes](java-pki-programmers-guide.htm#GUID-AB96FD45-6F8A-4785-B6C5-082BEB6CDA5E "The Java Certification Path API includes the CertStore class for retrieving certificates and CRLs from a repository.")

    -   `CertStore`{.codeph}, `CertStoreParameters`{.codeph},
        `CertSelector`{.codeph}, and `CRLSelector`{.codeph}

The Java Certification Path API also includes a set of
algorithm-specific classes modeled for use with the PKIX certification
path validation algorithm defined in [RFC
5280](http://www.ietf.org/rfc/rfc5280.txt): <cite>Public Key
Infrastructure Certificate and Certificate Revocation List (CRL)
Profile</cite>. The [PKIX
Classes](java-pki-programmers-guide.htm#GUID-5BBEF087-CA8A-4287-97FB-BD88DCD12FE5 "The Java Certification Path API includes a set of algorithm-specific classes modeled for use with the PKIX certification path validation algorithm.")
are:

-   `TrustAnchor`{.codeph}

-   `PKIXParameters`{.codeph}

-   `PKIXCertPathValidatorResult`{.codeph}

-   `PKIXBuilderParameters`{.codeph}

-   `PKIXCertPathBuilderResult`{.codeph}

-   `PKIXCertPathChecker`{.codeph}

-   `PKIXRevocationChecker`{.codeph}

The complete reference documentation for the relevant Certification Path
API classes can be found in
[`java.security.cert`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/cert/package-summary.html).

Most of the classes and interfaces in the
<span class="apiname">CertPath</span> API are not thread-safe. However,
there are some exceptions, which will be noted in this guide and in the
API specification. Multiple threads that need to access a single
non-thread-safe object concurrently should synchronize amongst
themselves and provide the necessary locking. Multiple threads each
manipulating separate objects need not synchronize.

</div>
<!-- class="section" -->

<div class="section">
Topics

[Basic Certification Path
Classes](java-pki-programmers-guide.htm#GUID-2D30176C-EE5A-41F8-896B-1A16E7F786B8 "The basic certification path classes provide fundamental functionality for encoding and representing certification paths. The key basic class in the Java Certification Path API is CertPath, which encapsulates the universal aspects shared by all types of certification paths. An application uses an instance of the CertificateFactory class to create a CertPath object.")

[Certification Path Validation
Classes](java-pki-programmers-guide.htm#GUID-C825028D-5F30-4041-ACC4-466657F59F02 "The Java Certification Path API includes classes and interfaces for validating certification paths. An application uses an instance of the CertPathValidator class to validate a CertPath object. If successful, the result of the validation algorithm is returned in an object implementing the CertPathValidatorResult interface.")

[Certification Path Building
Classes](java-pki-programmers-guide.htm#GUID-CBABC770-E714-4E6C-AD40-EA680BE91C20 "The Java Certification Path API includes classes for building (or discovering) certification paths. An application uses an instance of the CertPathBuilder class to build a CertPath object. If successful, the result of the build is returned in an object implementing the CertPathBuilderResult interface.")

[Certificate/CRL Storage
Classes](java-pki-programmers-guide.htm#GUID-AB96FD45-6F8A-4785-B6C5-082BEB6CDA5E "The Java Certification Path API includes the CertStore class for retrieving certificates and CRLs from a repository.")

[PKIX
Classes](java-pki-programmers-guide.htm#GUID-5BBEF087-CA8A-4287-97FB-BD88DCD12FE5 "The Java Certification Path API includes a set of algorithm-specific classes modeled for use with the PKIX certification path validation algorithm.")

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-2D30176C-EE5A-41F8-896B-1A16E7F786B8}

### Basic Certification Path Classes {#JSSEC-GUID-2D30176C-EE5A-41F8-896B-1A16E7F786B8 .sect3}

<div>
The basic certification path classes provide fundamental functionality
for encoding and representing certification paths. The key basic class
in the Java Certification Path API is `CertPath`{.codeph}, which
encapsulates the universal aspects shared by all types of certification
paths. An application uses an instance of the
`CertificateFactory`{.codeph} class to create a `CertPath`{.codeph}
object.

<div class="section">
Topics

[The CertPath
Class](java-pki-programmers-guide.htm#GUID-E47B8A0E-6B3A-4B49-994D-CF185BF441EC "The CertPath class is an abstract class for certification paths. It defines the functionality shared by all certification path objects. Various certification path types can be implemented by subclassing the CertPath class, even though they may have different contents and ordering schemes.")

[The CertificateFactory
Class](java-pki-programmers-guide.htm#GUID-BCABADD4-C0DC-4987-B187-F086B4BCE195 "The CertificateFactory class is an engine class that defines the functionality of a certificate factory. It is used to generate Certificate, CRL, and CertPath objects.")

[The CertPathParameters
Interface](java-pki-programmers-guide.htm#GUID-2AF52C1B-8EE2-4D65-9273-F7AC523AB42F "The CertPathParameters interface is a transparent representation of the set of parameters used with a particular certification path builder or validation algorithm.")

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-E47B8A0E-6B3A-4B49-994D-CF185BF441EC}

#### The CertPath Class {#JSSEC-GUID-E47B8A0E-6B3A-4B49-994D-CF185BF441EC .sect4}

<div>
The `CertPath`{.codeph} class is an abstract class for certification
paths. It defines the functionality shared by all certification path
objects. Various certification path types can be implemented by
subclassing the `CertPath`{.codeph} class, even though they may have
different contents and ordering schemes.

All `CertPath`{.codeph} objects are serializable, immutable and
thread-safe and share the following characteristics:

-   A type

    This corresponds to the type of the certificates in the
    certification path, for example: X.509. The type of a
    `CertPath`{.codeph} is obtained using the method:

    ``` {.codeblock dir="ltr"}
        public String getType()
    ```

    For standard certificate types, see [CertificateFactory
    Types](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html#certificatefactory-types).

-   A list of certificates

    The `getCertificates`{.codeph} method returns the list of
    certificates in the certification path:

    ``` {.codeblock dir="ltr"}
        public abstract List<? extends Certificate> getCertificates()
    ```

    This method returns a `List`{.codeph} of zero or more
    `java.security.cert.Certificate`{.codeph} objects. The returned
    `List`{.codeph} and the `Certificates`{.codeph} contained within it
    are immutable, in order to protect the contents of the
    `CertPath`{.codeph} object. The ordering of the certificates
    returned depends on the type. By convention, the certificates in a
    `CertPath`{.codeph} object of type X.509 are ordered starting with
    the target certificate and ending with a certificate issued by the
    trust anchor. That is, the issuer of one certificate is the subject
    of the following one. The certificate representing the
    `TrustAnchor`{.codeph} should not be included in the certification
    path. Unvalidated X.509 `CertPath`{.codeph}s may not follow this
    convention. PKIX `CertPathValidator`{.codeph}s will detect any
    departure from these conventions that cause the certification path
    to be invalid and throw a `CertPathValidatorException`{.codeph}.

-   One or more encodings

    Each `CertPath`{.codeph} object supports one or more encodings.
    These are external encoded forms for the certification path, used
    when a standard representation of the path is needed outside the
    Java Virtual Machine (as when transmitting the path over a network
    to some other party). Each path can be encoded in a default format,
    the bytes of which are returned using the method:

    ``` {.codeblock dir="ltr"}
        public abstract byte[] getEncoded()
    ```

    Alternatively, the `getEncoded(String)`{.codeph} method returns a
    specific supported encoding by specifying the encoding format as a
    `String`{.codeph} (ex: \"PKCS7\"). For standard encoding formats,
    see [CertPath
    Encodings](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html#certpath-encodings).

    ``` {.codeblock dir="ltr"}
        public abstract byte[] getEncoded(String encoding)
    ```

    Also, the `getEncodings`{.codeph} method returns an iterator over
    the supported encoding format `String`{.codeph}s (the default
    encoding format is returned first):

    ``` {.codeblock dir="ltr"}
        public abstract Iterator<String> getEncodings()
    ```

All `CertPath`{.codeph} objects are also `Serializable`{.codeph}.
`CertPath`{.codeph} objects are resolved into an alternate
`CertPath.CertPathRep`{.codeph} object during serialization. This allows
a `CertPath`{.codeph} object to be serialized into an equivalent
representation regardless of its underlying implementation.

`CertPath`{.codeph} objects are generated from an encoded byte array or
list of `Certificate`{.codeph}s using a `CertificateFactory`{.codeph}.
Alternatively, a `CertPathBuilder`{.codeph} may be used to try to find a
`CertPath`{.codeph} from a most-trusted CA to a particular subject. Once
a `CertPath`{.codeph} object has been created, it may be validated by
passing it to the `validate`{.codeph} method of
`CertPathValidator`{.codeph}. Each of these concepts are explained in
more detail in subsequent sections.

</div>
</div>
<div class="sect4">
[]{#GUID-BCABADD4-C0DC-4987-B187-F086B4BCE195}

#### The CertificateFactory Class {#JSSEC-GUID-BCABADD4-C0DC-4987-B187-F086B4BCE195 .sect4}

<div>
The `CertificateFactory`{.codeph} class is an engine class that defines
the functionality of a certificate factory. It is used to generate
`Certificate`{.codeph}, `CRL`{.codeph}, and `CertPath`{.codeph} objects.

A `CertificateFactory`{.codeph} should not be confused with a
`CertPathBuilder`{.codeph}. A `CertPathBuilder`{.codeph} (discussed
later) is used to discover or find a certification path when one does
not exist. In contrast, a `CertificateFactory`{.codeph} is used when a
certification path has already been discovered and the caller needs to
instantiate a `CertPath`{.codeph} object from its contents, which exist
in a different form such as an encoded byte array or an array of
`Certificate`{.codeph}s.

<div class="section">
Creating a CertificateFactory Object

See the
[CertificateFactory](java-cryptography-architecture-jca-reference-guide.htm#GUID-9A581FBA-EDF7-4BCA-8244-4CE2C75E4CEA "The CertificateFactory class defines the functionality of a certificate factory, which is used to generate certificate and certificate revocation list (CRL) objects from their encoding.")
section in the <cite> Java Cryptography Architecture Reference
Guide</cite> for the details of creating a `CertificateFactory`{.codeph}
object.

</div>
<!-- class="section" -->

<div class="section">
Generating CertPath Objects

A `CertificateFactory`{.codeph} instance generates `CertPath`{.codeph}
objects from a `List`{.codeph} of `Certificate`{.codeph} objects or from
an `InputStream`{.codeph} that contains the encoded form of a
`CertPath`{.codeph}. Just like a `CertPath`{.codeph}, each
`CertificateFactory`{.codeph} supports a default encoding format for
certification paths (ex: PKCS\#7). To generate a `CertPath`{.codeph}
object and initialize it with the data read from an input stream (in the
default encoding format), use the `generateCertPath`{.codeph} method:

``` {.oac_no_warn dir="ltr"}
public final CertPath generateCertPath(InputStream inStream)
```

or from a particular encoding format:

``` {.oac_no_warn dir="ltr"}
    public final CertPath generateCertPath(InputStream inStream, 
                                           String encoding)
```

To find out what encoding formats are supported, use the
`getCertPathEncodings`{.codeph} method (the default encoding is returned
first):

``` {.oac_no_warn dir="ltr"}
public final Iterator<String> getCertPathEncodings()
```

To generate a certification path object from a `List`{.codeph} of
`Certificate`{.codeph} objects, use the following method:

``` {.oac_no_warn dir="ltr"}
public final CertPath generateCertPath(List<? extends Certificate> certificates)
```

A `CertificateFactory`{.codeph} always returns `CertPath`{.codeph}
objects that consist of `Certificates`{.codeph} that are of the same
type as the factory. For example, a `CertificateFactory`{.codeph} of
type X.509 returns `CertPath`{.codeph} objects consisting of
certificates that are an instance of
`java.security.cert.X509Certificate`{.codeph}.

The following code sample illustrates generating a certification path
from a PKCS\#7 encoded certificate reply stored in a file:

``` {.oac_no_warn dir="ltr"}
    // open an input stream to the file
    FileInputStream fis = new FileInputStream(filename);
    // instantiate a CertificateFactory for X.509
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    // extract the certification path from
    // the PKCS7 SignedData structure
    CertPath cp = cf.generateCertPath(fis, "PKCS7");
    // print each certificate in the path
    List<Certificate> certs = cp.getCertificates();
    for (Certificate cert : certs) {
        System.out.println(cert);
    }
```

Here\'s another code sample that fetches a certificate chain from a
`KeyStore`{.codeph} and converts it to a `CertPath`{.codeph} using a
`CertificateFactory`{.codeph}:

``` {.oac_no_warn dir="ltr"}
    // instantiate a KeyStore with type JKS
    KeyStore ks = KeyStore.getInstance("JKS");
    // load the contents of the KeyStore
    ks.load(new FileInputStream("./keystore"),
        "password".toCharArray());
    // fetch certificate chain stored with alias "sean"
    Certificate[] certArray = ks.getCertificateChain("sean");
    // convert chain to a List
    List certList = Arrays.asList(certArray);
    // instantiate a CertificateFactory for X.509
    CertificateFactory cf = CertificateFactory.getInstance("X.509");
    // extract the certification path from
    // the List of Certificates
    CertPath cp = cf.generateCertPath(certList);
```

Note that there is an existing method in `CertificateFactory`{.codeph}
named `generateCertificates`{.codeph} that parses a sequence of
`Certificates`{.codeph}. For encodings consisting of multiple
certificates, use `generateCertificates`{.codeph} when you want to parse
a collection of possibly unrelated certificates. Otherwise, use
`generateCertPath`{.codeph} when you want to generate a
`CertPath`{.codeph} and subsequently validate it with a
`CertPathValidator`{.codeph} (discussed later).

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-2AF52C1B-8EE2-4D65-9273-F7AC523AB42F}

#### The CertPathParameters Interface {#JSSEC-GUID-2AF52C1B-8EE2-4D65-9273-F7AC523AB42F .sect4}

<div>
The `CertPathParameters`{.codeph} interface is a transparent
representation of the set of parameters used with a particular
certification path builder or validation algorithm.

Its main purpose is to group (and provide type safety for) all
certification path parameter specifications. The
`CertPathParameters`{.codeph} interface extends the `Cloneable`{.codeph}
interface and defines a `clone()`{.codeph} method that does not throw an
exception. All concrete implementations of this interface should
implement and override the `Object.clone()`{.codeph} method, if
necessary. This allows applications to clone any
`CertPathParameters`{.codeph} object.

Objects implementing the `CertPathParameters`{.codeph} interface are
passed as arguments to methods of the `CertPathValidator`{.codeph} and
`CertPathBuilder`{.codeph} classes. Typically, a concrete implementation
of the `CertPathParameters`{.codeph} interface will hold a set of input
parameters specific to a particular certification path build or
validation algorithm. For example, the `PKIXParameters`{.codeph} class
is an implementation of the `CertPathParameters`{.codeph} interface that
holds a set of input parameters for the PKIX certification path
validation algorithm. One such parameter is the set of most-trusted CAs
that the caller trusts for anchoring the validation process. This
parameter among others is discussed in more detail in the section
discussing the `PKIXParameters`{.codeph} class.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-C825028D-5F30-4041-ACC4-466657F59F02}

### Certification Path Validation Classes {#JSSEC-GUID-C825028D-5F30-4041-ACC4-466657F59F02 .sect3}

<div>
The Java Certification Path API includes classes and interfaces for
validating certification paths. An application uses an instance of the
`CertPathValidator`{.codeph} class to validate a `CertPath`{.codeph}
object. If successful, the result of the validation algorithm is
returned in an object implementing the
`CertPathValidatorResult`{.codeph} interface.

<div class="section">
Topics

[The CertPathValidator
Class](java-pki-programmers-guide.htm#GUID-808C1A6D-6A67-4026-A9DE-223A428EC80A "The CertPathValidator class is an engine class used to validate a certification path.")

[The CertPathValidatorResult
Interface](java-pki-programmers-guide.htm#GUID-29AC2D33-7518-4DEA-A4CC-544CB174B915 "The CertPathValidatorResult interface is a transparent representation of the successful result or output of a certification path validation algorithm.")

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-808C1A6D-6A67-4026-A9DE-223A428EC80A}

#### The CertPathValidator Class {#JSSEC-GUID-808C1A6D-6A67-4026-A9DE-223A428EC80A .sect4}

<div>
The `CertPathValidator`{.codeph} class is an engine class used to
validate a certification path.

<div class="section">
Creating a CertPathValidator Object

As with all engine classes, the way to get a
`CertPathValidator`{.codeph} object for a particular validation
algorithm is to call one of the `getInstance`{.codeph} static factory
methods on the `CertPathValidator`{.codeph} class:

``` {.codeblock dir="ltr"}
        public static CertPathValidator getInstance(String algorithm)
        public static CertPathValidator getInstance(String algorithm, 
                                                    String provider)
        public static CertPathValidator getInstance(String algorithm, 
                                                    Provider provider)
```

The `algorithm`{.codeph} parameter is the name of a certification path
validation algorithm (for example, \"PKIX\"). Standard
`CertPathValidator`{.codeph} algorithm names are listed in the [Java
Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).

</div>
<!-- class="section" -->

<div class="section">
Validating a Certification Path

Once a `CertPathValidator`{.codeph} object is created, paths can be
validated by calling the `validate`{.codeph} method, passing it the
certification path to be validated and a set of algorithm-specific
parameters:

``` {.codeblock dir="ltr"}
        public final CertPathValidatorResult 
                validate(CertPath certPath, CertPathParameters params)
                throws CertPathValidatorException, 
                       InvalidAlgorithmParameterException
```

If the validation algorithm is successful, the result is returned in an
object implementing the `CertPathValidatorResult`{.codeph} interface.
Otherwise, a `CertPathValidatorException`{.codeph} is thrown. The
`CertPathValidatorException`{.codeph} contains methods that return the
`CertPath`{.codeph}, and if relevant, the index of the certificate that
caused the algorithm to fail and the root exception or cause of the
failure.

Note that the `CertPath`{.codeph} and `CertPathParameters`{.codeph}
passed to the `validate`{.codeph} method must be of a type that is
supported by the validation algorithm. Otherwise, an
`InvalidAlgorithmParameterException`{.codeph} is thrown. For example, a
`CertPathValidator`{.codeph} instance that implements the PKIX algorithm
validates `CertPath`{.codeph} objects of type X.509 and
`CertPathParameters`{.codeph} that are an instance of
`PKIXParameters`{.codeph}.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-29AC2D33-7518-4DEA-A4CC-544CB174B915}

#### The CertPathValidatorResult Interface {#JSSEC-GUID-29AC2D33-7518-4DEA-A4CC-544CB174B915 .sect4}

<div>
The `CertPathValidatorResult`{.codeph} interface is a transparent
representation of the successful result or output of a certification
path validation algorithm.

The main purpose of this interface is to group and provide type safety
for all validation results. Similar to the `CertPathParameters`{.codeph}
interface, `CertPathValidatorResult`{.codeph} extends
`Cloneable`{.codeph} and defines a `clone()`{.codeph} method that does
not throw an exception. This allows applications to clone any
`CertPathValidatorResult`{.codeph} object.

Objects implementing the `CertPathValidatorResult`{.codeph} interface
are returned by the `validate`{.codeph} method of
`CertPathValidatorResult`{.codeph} interface when successful. If not
successful, a `CertPathValidatorException`{.codeph} is thrown with a
description of the failure. Typically, a concrete implementation of the
`CertPathValidatorResult`{.codeph} interface will hold a set of output
parameters specific to a particular certification path validation
algorithm. For example, the `PKIXCertPathValidatorResult`{.codeph} class
is an implementation of the `CertPathValidatorResult`{.codeph}
interface, which contains methods to get the output parameters of the
PKIX certification path validation algorithm. One such parameter is the
valid policy tree. This parameter among others is discussed in more
detail in the section discussing the
`PKIXCertPathValidatorResult`{.codeph} class.

The following code sample shows how to create a
`CertPathValidator`{.codeph} and use it to validate a certification
path. The sample assumes that the `CertPath`{.codeph} and
`CertPathParameters`{.codeph} objects which are passed to the
`validate`{.codeph} method have been previously created; a more complete
example will be illustrated in the section describing the PKIX classes.

``` {.codeblock dir="ltr"}
    // create CertPathValidator that implements the "PKIX" algorithm
    CertPathValidator cpv = null;
    try {
        cpv = CertPathValidator.getInstance("PKIX");
    } catch (NoSuchAlgorithmException nsae) {
        System.err.println(nsae);
        System.exit(1);
    }
    // validate certification path ("cp") with specified parameters ("params")
    try {
        CertPathValidatorResult cpvResult = cpv.validate(cp, params);
    } catch (InvalidAlgorithmParameterException iape) {
        System.err.println("validation failed: " + iape);
        System.exit(1);
    } catch (CertPathValidatorException cpve) {
        System.err.println("validation failed: " + cpve);
        System.err.println("index of certificate that caused exception: "
                + cpve.getIndex());
        System.exit(1);
    }
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-CBABC770-E714-4E6C-AD40-EA680BE91C20}

### Certification Path Building Classes {#JSSEC-GUID-CBABC770-E714-4E6C-AD40-EA680BE91C20 .sect3}

<div>
The Java Certification Path API includes classes for building (or
discovering) certification paths. An application uses an instance of the
`CertPathBuilder`{.codeph} class to build a `CertPath`{.codeph} object.
If successful, the result of the build is returned in an object
implementing the `CertPathBuilderResult`{.codeph} interface.

<div class="section">
Topics

[The CertPathBuilder
Class](java-pki-programmers-guide.htm#GUID-BEFCC824-21C1-4AD3-B670-D0CA01F08D95 "The CertPathBuilder class is an engine class used to build a certification path.")

[The CertPathBuilderResult
Interface](java-pki-programmers-guide.htm#GUID-47B1564D-DFC3-4F0F-A006-CB7303EDD919 "The CertPathBuilderResult interface is a transparent representation of the result or output of a certification path builder algorithm.")

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-BEFCC824-21C1-4AD3-B670-D0CA01F08D95}

#### The CertPathBuilder Class {#JSSEC-GUID-BEFCC824-21C1-4AD3-B670-D0CA01F08D95 .sect4}

<div>
The `CertPathBuilder`{.codeph} class is an engine class used to build a
certification path.

<div class="section">
Creating a CertPathBuilder Object

As with all engine classes, the way to get a `CertPathBuilder`{.codeph}
object for a particular build algorithm is to call one of the
`getInstance`{.codeph} static factory method on the
`CertPathBuilder`{.codeph} class:

``` {.codeblock dir="ltr"}
        public static CertPathBuilder getInstance(String algorithm)
        public static CertPathBuilder getInstance(String algorithm, 
                                                  String provider)
        public static CertPathBuilder getInstance(String algorithm, 
                                                  Provider provider)
```

The `algorithm`{.codeph} parameter is the name of a certification path
builder algorithm (for example, \"PKIX\"). Standard
`CertPathBuilder`{.codeph} algorithm names are listed in [Java Security
Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).

</div>
<!-- class="section" -->

<div class="section">
Building a Certification Path

Once a `CertPathBuilder`{.codeph} object is created, paths can be
constructed by calling the `build`{.codeph} method, passing it an
algorithm-specific parameter specification:

``` {.codeblock dir="ltr"}
        public final CertPathBuilderResult build(CertPathParameters params)
                throws CertPathBuilderException, 
                       InvalidAlgorithmParameterException
```

If the build algorithm is successful, the result is returned in an
object implementing the `CertPathBuilderResult`{.codeph} interface.
Otherwise, a `CertPathBuilderException`{.codeph} is thrown containing
information about the failure; for example, the underlying exception (if
any) and an error message.

Note that the `CertPathParameters`{.codeph} passed to the
`build`{.codeph} method must be of a type that is supported by the build
algorithm. Otherwise, an `InvalidAlgorithmParameterException`{.codeph}
is thrown.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-47B1564D-DFC3-4F0F-A006-CB7303EDD919}

#### The CertPathBuilderResult Interface {#JSSEC-GUID-47B1564D-DFC3-4F0F-A006-CB7303EDD919 .sect4}

<div>
The `CertPathBuilderResult`{.codeph} interface is a transparent
representation of the result or output of a certification path builder
algorithm.

This interface contains a method to return the certification path that
has been successfully built:

``` {.codeblock dir="ltr"}
        public CertPath getCertPath()
```

The purpose of the `CertPathBuilderResult`{.codeph} interface is to
group (and provide type safety for) all build results. Like the
`CertPathValidatorResult`{.codeph} interface,
`CertPathBuilderResult`{.codeph} extends `Cloneable`{.codeph} and
defines a `clone()`{.codeph} method that does not throw an exception.
This allows applications to clone any `CertPathBuilderResult`{.codeph}
object.

Objects implementing the `CertPathBuilderResult`{.codeph} interface are
returned by the `build`{.codeph} method of `CertPathBuilder`{.codeph}.

The following code sample shows how to create a
`CertPathBuilder`{.codeph} and use it to build a certification path. The
sample assumes that the `CertPathParameters`{.codeph} object which is
passed to the `build`{.codeph} method has been previously created; a
more complete example will be illustrated in the section describing the
PKIX classes.

``` {.codeblock dir="ltr"}
    // create CertPathBuilder that implements the "PKIX" algorithm
    CertPathBuilder cpb = null;
    try {
        cpb = CertPathBuilder.getInstance("PKIX");
    } catch (NoSuchAlgorithmException nsae) {
        System.err.println(nsae);
        System.exit(1);
    }
    // build certification path using specified parameters ("params")
    try {
        CertPathBuilderResult cpbResult = cpb.build(params);
        CertPath cp = cpbResult.getCertPath();
        System.out.println("build passed, path contents: " + cp);
    } catch (InvalidAlgorithmParameterException iape) {
        System.err.println("build failed: " + iape);
        System.exit(1);
    } catch (CertPathBuilderException cpbe) {
        System.err.println("build failed: " + cpbe);
        System.exit(1);
    }
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-AB96FD45-6F8A-4785-B6C5-082BEB6CDA5E}

### Certificate/CRL Storage Classes {#JSSEC-GUID-AB96FD45-6F8A-4785-B6C5-082BEB6CDA5E .sect3}

<div>
The Java Certification Path API includes the `CertStore`{.codeph} class
for retrieving certificates and CRLs from a repository.

This class enables a caller to specify the repository a
`CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph}
implementation should use to find certificates and CRLs. See the
`addCertStores`{.codeph} method of the `PKIXParameters`{.codeph} class.

A `CertPathValidator`{.codeph} implementation may use the
`CertStore`{.codeph} object that the caller specifies as a callback
mechanism to fetch CRLs for performing revocation checks. Similarly, a
`CertPathBuilder`{.codeph} may use the `CertStore`{.codeph} as a
callback mechanism to fetch certificates and, if performing revocation
checks, CRLs.

<div class="section">
Topics

[The CertStore
Class](java-pki-programmers-guide.htm#GUID-5404B79C-3D49-4668-974C-1BACD1A98B73 "The CertStore class is an engine class used to provide the functionality of a certificate and certificate revocation list (CRL) repository.")

[The CertStoreParameters
Interface](java-pki-programmers-guide.htm#GUID-BC87018F-F888-4905-8ED4-AE574C646AF2 "The CertStoreParameters interface is a transparent representation of the set of parameters used with a particular CertStore.")

[The CertSelector and CRLSelector
Interfaces](java-pki-programmers-guide.htm#GUID-263AAFB6-DC37-4B64-95E7-60D59D7728B5 "The CertSelector and CRLSelector interfaces are a specification of the set of criteria for selecting certificates and CRLs from a collection or large group of certificates and CRLs.")

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-5404B79C-3D49-4668-974C-1BACD1A98B73}

#### The CertStore Class {#JSSEC-GUID-5404B79C-3D49-4668-974C-1BACD1A98B73 .sect4}

<div>
The `CertStore`{.codeph} class is an engine class used to provide the
functionality of a certificate and certificate revocation list (CRL)
repository.

This class can be used by `CertPathBuilder`{.codeph} and
`CertPathValidator`{.codeph} implementations to find certificates and
CRLs, or as a general purpose certificate and CRL retrieval mechanism.

Unlike the `java.security.KeyStore`{.codeph} class, which provides
access to a cache of private keys and trusted certificates, a
`CertStore`{.codeph} is designed to provide access to a potentially vast
repository of untrusted certificates and CRLs. For example, an LDAP
implementation of `CertStore`{.codeph} provides access to certificates
and CRLs stored in one or more directories using the LDAP protocol.

All public methods of `CertStore`{.codeph} objects are thread-safe. That
is, multiple threads may concurrently invoke these methods on a single
`CertStore`{.codeph} object (or more than one) with no ill effects. This
allows a `CertPathBuilder`{.codeph} to search for a CRL while
simultaneously searching for further certificates, for instance.

<div class="section">
Creating a CertStore Object

As with all engine classes, the way to get a `CertStore`{.codeph} object
for a particular repository type is to call one of the
`getInstance`{.codeph} static factory methods on the
`CertStore`{.codeph} class:

``` {.codeblock dir="ltr"}
        public static CertStore getInstance(String type, 
                CertStoreParameters params)
        public static CertStore getInstance(String type,
                CertStoreParameters params, String provider)
        public static CertStore getInstance(String type,
                CertStoreParameters params, Provider provider)
```

The `type`{.codeph} parameter is the name of a certificate repository
type (for example, \"LDAP\"). Standard `CertStore`{.codeph} types are
listed in [Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).

The initialization parameters (`params`{.codeph}) are specific to the
repository type. For example, the initialization parameters for a
server-based repository may include the hostname and the port of the
server. An `InvalidAlgorithmParameterException`{.codeph} is thrown if
the parameters are invalid for this `CertStore`{.codeph} type. The
`getCertStoreParameters`{.codeph} method returns the
`CertStoreParameters`{.codeph} that were used to initialize a
`CertStore`{.codeph}:

``` {.codeblock dir="ltr"}
        public final CertStoreParameters getCertStoreParameters()
```

</div>
<!-- class="section" -->

<div class="section">
Retrieving Certificates

After you have created a `CertStore`{.codeph} object, you can retrieve
certificates from the repository using the `getCertificates`{.codeph}
method. This method takes a `CertSelector`{.codeph} (discussed in more
detail later) object as an argument, which specifies a set of selection
criteria for determining which certificates should be returned:

``` {.codeblock dir="ltr"}
        public final Collection<? extends Certificate> getCertificates(CertSelector selector) 
                throws CertStoreException
```

This method returns a `Collection`{.codeph} of
`java.security.cert.Certificate`{.codeph} objects that satisfy the
selection criteria. An empty `Collection`{.codeph} is returned if there
are no matches. A `CertStoreException`{.codeph} is usually thrown if an
unexpected error condition is encountered, such as a communications
failure with a remote repository.

For some `CertStore`{.codeph} implementations, it may not be feasible to
search the entire repository for certificates or CRLs that match the
specified selection criteria. In these instances, the
`CertStore`{.codeph} implementation may use information that is
specified in the selectors to locate certificates and CRLs. For
instance, an LDAP `CertStore`{.codeph} may not search all entries in the
directory. Instead, it may just search entries that are likely to
contain the certificates it is looking for. If the
`CertSelector`{.codeph} provided does not provide enough information for
the LDAP `CertStore`{.codeph} to determine which entries it should look
in, the LDAP `CertStore`{.codeph} may throw a
`CertStoreException`{.codeph}.

</div>
<!-- class="section" -->

<div class="section">
Retrieving CRLs

You can also retrieve CRLs from the repository using the
`getCRLs`{.codeph} method. This method takes a `CRLSelector`{.codeph}
(discussed in more detail later) object as an argument, which specifies
a set of selection criteria for determining which CRLs should be
returned:

``` {.codeblock dir="ltr"}
        public final Collection<? extends CRL> getCRLs(CRLSelector selector) 
                throws CertStoreException
```

This method returns a `Collection`{.codeph} of
`java.security.cert.CRL`{.codeph} objects that satisfy the selection
criteria. An empty `Collection`{.codeph} is returned if there are no
matches.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-BC87018F-F888-4905-8ED4-AE574C646AF2}

#### The CertStoreParameters Interface {#JSSEC-GUID-BC87018F-F888-4905-8ED4-AE574C646AF2 .sect4}

<div>
The `CertStoreParameters`{.codeph} interface is a transparent
representation of the set of parameters used with a particular
`CertStore`{.codeph}.

The main purpose of this interface is to group and provide type safety
for all certificate storage parameter specifications. The
`CertStoreParameters`{.codeph} interface extends the
`Cloneable`{.codeph} interface and defines a `clone`{.codeph} method
that does not throw an exception. Implementations of this interface
should implement and override the `Object.clone()`{.codeph} method, if
necessary. This allows applications to clone any
`CertStoreParameters`{.codeph} object.

Objects implementing the `CertStoreParameters`{.codeph} interface are
passed as arguments to the `getInstance`{.codeph} method of the
`CertStore`{.codeph} class. Two classes implementing the
`CertStoreParameters`{.codeph} interface are defined in this API: the
`LDAPCertStoreParameters`{.codeph} class and the
`CollectionCertStoreParameters`{.codeph} class.

<div class="section" id="GUID-BC87018F-F888-4905-8ED4-AE574C646AF2__THELDAPCERTSTOREPARAMETERSCLASS-C0996E42">
The LDAPCertStoreParameters Class

The `LDAPCertStoreParameters`{.codeph} class is an implementation of the
`CertStoreParameters`{.codeph} interface and holds a set of minimal
initialization parameters (host and port number of the directory server)
for retrieving certificates and CRLs from a `CertStore`{.codeph} of type
<span class="bold">LDAP</span>.

See `LDAPCertStoreParameters`{.codeph}</a></code>.

</div>
<!-- class="section" -->

<div class="section" id="GUID-BC87018F-F888-4905-8ED4-AE574C646AF2__THECOLLECTIONCERTSTOREPARAMETERSCLA-C09970DC">
The CollectionCertStoreParameters Class

The `CollectionCertStoreParameters`{.codeph} class is an implementation
of the `CertStoreParameters`{.codeph} interface and holds a set of
initialization parameters for retrieving certificates and CRLs from a
`CertStore`{.codeph} of type <span class="bold">Collection</span>.

See `CollectionCertStoreParameters`{.codeph}</a></code>.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-263AAFB6-DC37-4B64-95E7-60D59D7728B5}

#### The CertSelector and CRLSelector Interfaces {#JSSEC-GUID-263AAFB6-DC37-4B64-95E7-60D59D7728B5 .sect4}

<div>
The `CertSelector`{.codeph} and `CRLSelector`{.codeph} interfaces are a
specification of the set of criteria for selecting certificates and CRLs
from a collection or large group of certificates and CRLs.

The interfaces group and provide type safety for all selector
specifications. Each selector interface extends `Cloneable`{.codeph} and
defines a `clone()`{.codeph} method that does not throw an exception.
This allows applications to clone any `CertSelector`{.codeph} or
`CRLSelector`{.codeph} object.

The `CertSelector`{.codeph} and `CRLSelector`{.codeph} interfaces each
define a method named `match`{.codeph}. The `match`{.codeph} method
takes a `Certificate`{.codeph} or `CRL`{.codeph} object as an argument
and returns `true`{.codeph} if the object satisfies the selection
criteria. Otherwise, it returns `false`{.codeph}. The `match`{.codeph}
method for the `CertSelector`{.codeph} interface is defined as follows:

``` {.codeblock dir="ltr"}
        public boolean match(Certificate cert)
```

and for the `CRLSelector`{.codeph} interface:

``` {.codeblock dir="ltr"}
        public boolean match(CRL crl)
```

Typically, objects implementing these interfaces are passed as
parameters to the `getCertificates`{.codeph} and `getCRLs`{.codeph}
methods of the `CertStore`{.codeph} class. These methods return a
`Collection`{.codeph} of `Certificate`{.codeph}s or `CRL`{.codeph}s from
the `CertStore`{.codeph} repository that match the specified selection
criteria. `CertSelector`{.codeph}s may also be used to specify the
validation constraints on a target or end-entity certificate in a
certification path (see for example, the
` PKIXParameters.setTargetCertConstraints`{.codeph} method.)

</div>
<div class="sect5">
[]{#GUID-2229C26E-1196-4E4F-8F23-731CE5CA254E}

##### The X509CertSelector Class {#JSSEC-GUID-2229C26E-1196-4E4F-8F23-731CE5CA254E .sect5}

<div>
The `X509CertSelector`{.codeph} class is an implementation of the
`CertSelector`{.codeph} interface that defines a set of criteria for
selecting X.509 certificates.

An `X509Certificate`{.codeph} object must match
<span class="variable">all</span> of the specified criteria to be
selected by the `match`{.codeph} method. The selection criteria are
designed to be used by a `CertPathBuilder`{.codeph} implementation to
discover potential certificates as it builds an X.509 certification
path.

For example, the `setSubject`{.codeph} method of
`X509CertSelector`{.codeph} allows a PKIX `CertPathBuilder`{.codeph} to
filter out `X509Certificate`{.codeph}s that do not match the issuer name
of the preceding `X509Certificate`{.codeph} in a partially completed
chain. By setting this and other criteria in an
`X509CertSelector`{.codeph} object, a `CertPathBuilder`{.codeph} is able
to discard irrelevant certificates and more easily find an X.509
certification path that meets the requirements specified in the
`CertPathParameters`{.codeph} object.

See [RFC 5280](http://www.ietf.org/rfc/rfc5280.txt) for definitions of
the X.509 certificate extensions mentioned in this section.

<div class="section">
Creating an X509CertSelector Object

An `X509CertSelector`{.codeph} object is created by calling the default
constructor:

``` {.codeblock dir="ltr"}
        public X509CertSelector()
```

No criteria are initially set (any `X509Certificate`{.codeph} will
match).

</div>
<!-- class="section" -->

<div class="section">
Setting Selection Criteria

The selection criteria allow a caller to match on different components
of an X.509 certificate. A few of the methods for setting selection
criteria are described here. See `X509CertSelector`{.codeph}</a></code>.

The `setIssuer`{.codeph} methods set the issuer criterion:

``` {.codeblock dir="ltr"}
        public void setIssuer(X500Principal issuer)
        public void setIssuer(String issuerDN)
        public void setIssuer(byte[] issuerDN)
```

The specified distinguished name (in `X500Principal`{.codeph}, [RFC
2253](http://www.ietf.org/rfc/rfc2253.txt) String or ASN.1 DER encoded
form) must match the issuer distinguished name in the certificate. If
null, any issuer distinguished name will do. Note that use of an
`X500Principal`{.codeph} to represent a distinguished name is preferred
because it is more efficient and suitably typed.

Similarly, the `setSubject`{.codeph} methods set the subject criterion:

``` {.codeblock dir="ltr"}
        public void setSubject(X500Principal subject)
        public void setSubject(String subjectDN)
        public void setSubject(byte[] subjectDN)
```

The specified distinguished name (in `X500Principal`{.codeph}, RFC 2253
String or ASN.1 DER encoded form) must match the subject distinguished
name in the certificate. If null, any subject distinguished name will
do.

The `setSerialNumber`{.codeph} method sets the serialNumber criterion:

``` {.codeblock dir="ltr"}
        public void setSerialNumber(BigInteger serial)
```

The specified serial number must match the certificate serial number in
the certificate. If null, any certificate serial number will do.

The `setAuthorityKeyIdentifier`{.codeph} method sets the
authorityKeyIdentifier criterion:

``` {.codeblock dir="ltr"}
        public void setAuthorityKeyIdentifier(byte[] authorityKeyID)
```

The certificate must contain an Authority Key Identifier extension
matching the specified value. If null, no check will be done on the
authorityKeyIdentifier criterion.

The `setCertificateValid`{.codeph} method sets the certificateValid
criterion:

``` {.codeblock dir="ltr"}
        public void setCertificateValid(Date certValid)
```

The specified date must fall within the certificate validity period for
the certificate. If null, any date is valid.

The `setKeyUsage`{.codeph} method sets the keyUsage criterion:

``` {.codeblock dir="ltr"}
        public void setKeyUsage(boolean[] keyUsage)
```

The certificate\'s Key Usage Extension must allow the specified key
usage values (those which are set to true). If null, no keyUsage check
will be done.

</div>
<!-- class="section" -->

<div class="section">
Getting Selection Criteria

The current values for each of the selection criteria can be retrieved
using an appropriate `get`{.codeph} method. See
`X509CertSelector`{.codeph}</a></code> .

</div>
<!-- class="section" -->

<div class="example" id="GUID-2229C26E-1196-4E4F-8F23-731CE5CA254E__GUID-222FD599-5D26-4181-B9F5-C319EDD5BBC7">
Here is an example of retrieving X.509 certificates from an LDAP
`CertStore`{.codeph} with the `X509CertSelector`{.codeph} class.

First, we create the `LDAPCertStoreParameters`{.codeph} object that we
will use to initialize the `CertStore`{.codeph} object with the hostname
and port of the LDAP server:

``` {.codeblock dir="ltr"}
        LDAPCertStoreParameters lcsp = new 
                LDAPCertStoreParameters("ldap.sun.com", 389);
```

Next, create the `CertStore`{.codeph} object, and pass it the
`LDAPCertStoreParameters`{.codeph} object, as in the following
statement:

``` {.codeblock dir="ltr"}
        CertStore cs = CertStore.getInstance("LDAP", lcsp);
```

This call creates a `CertStore`{.codeph} object that retrieves
certificates and CRLs from an LDAP repository using the schema defined
in RFC 2587.

The following block of code establishes an `X509CertSelector`{.codeph}
to retrieve all unexpired (as of the current date and time) end-entity
certificates issued to a particular subject with 1) a key usage that
allows digital signatures, and 2) a subject alternative name with a
specific email address:

``` {.codeblock dir="ltr"}
        X509CertSelector xcs = new X509CertSelector();

        // select only unexpired certificates
        xcs.setCertificateValid(new Date());

        // select only certificates issued to
        // 'CN=alice, O=xyz, C=us'
        xcs.setSubject(new X500Principal("CN=alice, O=xyz, C=us"));

        // select only end-entity certificates
        xcs.setBasicConstraints(-2);

        // select only certificates with a digitalSignature
        // keyUsage bit set (set the first entry in the
        // boolean array to true)
        boolean[] keyUsage = {true};
        xcs.setKeyUsage(keyUsage);

        // select only certificates with a subjectAltName of
        // 'alice@xyz.example.com' (1 is the integer value of 
        // an RFC822Name)
        xcs.addSubjectAlternativeName(1, "alice@xyz.example.com");
```

Then we pass the selector to the `getCertificates`{.codeph} method of
our `CertStore`{.codeph} object that we previously created:

``` {.codeblock dir="ltr"}
        Collection<Certificate> certs = cs.getCertificates(xcs);
```

A PKIX `CertPathBuilder`{.codeph} may use similar code to help discover
and sort through potential certificates by discarding those that do not
meet validation constraints or other criteria.

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect5">
[]{#GUID-08C0B832-6934-4A28-8932-8CEB87259BA8}

##### The X509CRLSelector Class {#JSSEC-GUID-08C0B832-6934-4A28-8932-8CEB87259BA8 .sect5}

<div>
The `X509CRLSelector`{.codeph} class is an implementation of the
`CRLSelector`{.codeph} interface that defines a set of criteria for
selecting X.509 CRLs.

An `X509CRL`{.codeph} object must match
<span class="variable">all</span> of the specified criteria to be
selected by the `match`{.codeph} method. The selection criteria are
designed to be useful to a `CertPathValidator`{.codeph} or
`CertPathBuilder`{.codeph} implementation that must retrieve CRLs from a
repository to check the revocation status of certificates in an X.509
certification path.

For example, the `setDateAndTime`{.codeph} method of
`X509CRLSelector`{.codeph} allows a PKIX `CertPathValidator`{.codeph} to
filter out `X509CRL`{.codeph}s that have been issued after or expire
before the time indicated. By setting this and other criteria in an
`X509CRLSelector`{.codeph} object, it allows the
`CertPathValidator`{.codeph} to discard irrelevant CRLs and more easily
check if a certificate has been revoked.

Please refer to [RFC 5280](http://www.ietf.org/rfc/rfc5280.txt) for
definitions of the X.509 CRL fields and extensions mentioned in this
section.

<div class="section">
Creating an X509CRLSelector Object

An `X509CRLSelector`{.codeph} object is created by calling the default
constructor:

``` {.codeblock dir="ltr"}
        public X509CRLSelector()
```

No criteria are initially set (any `X509CRL`{.codeph} will match).

</div>
<!-- class="section" -->

<div class="section">
Setting Selection Criteria

The selection criteria allow a caller to match on different components
of an X.509 CRL. Most of the methods for setting selection criteria are
described here. Please refer to the
`X509CRLSelector Class`{.codeph}</a></code> API documentation for
details on the remaining methods.

The `setIssuers`{.codeph} and `setIssuerNames`{.codeph} methods set the
issuerNames criterion:

``` {.codeblock dir="ltr"}
        public void setIssuers(Collection<X500Principal> issuers)
        public void setIssuerNames(Collection<?> names)
```

The issuer distinguished name in the CRL must match at least one of the
specified distinguished names. The `setIssuers`{.codeph} method is
preferred as the use of `X500Principal`{.codeph}s to represent
distinguished names is more efficient and suitably typed. For the
`setIssuerNames`{.codeph} method, each entry of the `names`{.codeph}
argument is either a `String`{.codeph} or a byte array (representing the
name, in RFC 2253 or ASN.1 DER encoded form, respectively). If null, any
issuer distinguished name will do.

The `setMinCRLNumber`{.codeph} and `setMaxCRLNumber`{.codeph} methods
set the minCRLNumber and maxCRLNumber criterion:

``` {.codeblock dir="ltr"}
        public void setMinCRLNumber(BigInteger minCRL)
        public void setMaxCRLNumber(BigInteger maxCRL)
```

The CRL must have a CRL Number extension whose value is greater than or
equal to the specified value if the `setMinCRLNumber`{.codeph} method is
called, and less than or equal to the specified value if the
`setMaxCRLNumber`{.codeph} method is called. If the value passed to one
of these methods is null, the corresponding check is not done.

The `setDateAndTime`{.codeph} method sets the dateAndTime criterion:

``` {.codeblock dir="ltr"}
        public void setDateAndTime(Date dateAndTime)
```

The specified date must be equal to or later than the value of the
thisUpdate component of the CRL and earlier than the value of the
nextUpdate component. If null, no dateAndTime check will be done.

The `setCertificateChecking`{.codeph} method sets the certificate whose
revocation status is being checked:

``` {.codeblock dir="ltr"}
        public void setCertificateChecking(X509Certificate cert)
```

This is not a criterion. Rather, it is optional information that may
help a `CertStore`{.codeph} find CRLs that would be relevant when
checking revocation for the specified certificate. If null is specified,
then no such optional information is provided. An application should
always call this method when checking revocation for a particular
certificate, as it may provide the `CertStore`{.codeph} with more
information for finding the correct CRLs and filtering out irrelevant
ones.

</div>
<!-- class="section" -->

<div class="section">
Getting Selection Criteria

The current values for each of the selection criteria can be retrieved
using an appropriate `get`{.codeph} method. Please refer to the
`X509CRLSelector Class`{.codeph}</a></code> API documentation for
further details on these methods.

</div>
<!-- class="section" -->

<div class="example" id="GUID-08C0B832-6934-4A28-8932-8CEB87259BA8__GUID-D4DD15D1-6345-446B-8B02-0F2C7C1FCBC4">
Creating an `X509CRLSelector`{.codeph} to retrieve CRLs from an LDAP
repository is similar to the `X509CertSelector`{.codeph} example.
Suppose we want to retrieve all current (as of the current date and
time) CRLs issued by a specific CA and with a minimum CRL number. First,
we create an `X509CRLSelector`{.codeph} object and call the appropriate
methods to set the selection criteria:

``` {.codeblock dir="ltr"}
        X509CRLSelector xcrls = new X509CRLSelector();
        // select CRLs satisfying current date and time
        xcrls.setDateAndTime(new Date());
        // select CRLs issued by 'O=xyz, C=us'
        xcrls.addIssuerName("O=xyz, C=us");
        // select only CRLs with a CRL number at least '2'
        xcrls.setMinCRLNumber(new BigInteger("2"));
```

Then we pass the selector to the `getCRLs`{.codeph} method of our
`CertStore`{.codeph} object (created in the `X509CertSelector`{.codeph}
example):

``` {.codeblock dir="ltr"}
        Collection<CRL> crls = cs.getCRLs(xcrls);
```

</div>
<!-- class="example" -->

</div>
</div>
</div>
</div>
<div class="sect3">
[]{#GUID-5BBEF087-CA8A-4287-97FB-BD88DCD12FE5}

### PKIX Classes {#JSSEC-GUID-5BBEF087-CA8A-4287-97FB-BD88DCD12FE5 .sect3}

<div>
The Java Certification Path API includes a set of algorithm-specific
classes modeled for use with the PKIX certification path validation
algorithm.

The PKIX certification path validation algorithm is defined in [RFC
5280](http://www.ietf.org/rfc/rfc5280.txt): <cite>Internet X.509 Public
Key Infrastructure Certificate and Certificate Revocation List (CRL)
Profile</cite>.

<div class="section">
Topics

[The TrustAnchor
Class](java-pki-programmers-guide.htm#GUID-772D31A0-FF9B-4A1E-985B-2100177C74F9 "The TrustAnchor class represents a "most-trusted CA", which is used as a trust anchor for validating X.509 certification paths.")

[The PKIXParameters
Class](java-pki-programmers-guide.htm#GUID-3D95A3BE-74CB-4357-BB85-9A8DEA36A457 "The PKIXParametersClass class specifies the set of input parameters defined by the PKIX certification path validation algorithm. It also includes a few additional useful parameters.")

[The CertPathValidatorResult
Interface](java-pki-programmers-guide.htm#GUID-29AC2D33-7518-4DEA-A4CC-544CB174B915 "The CertPathValidatorResult interface is a transparent representation of the successful result or output of a certification path validation algorithm.")

[The PolicyNode Interface and PolicyQualifierInfo
Class](java-pki-programmers-guide.htm#GUID-3AD41382-E729-469B-83EE-CB2FE66D71D8 "The PKIX validation algorithm defines several outputs related to certificate policy processing. Most applications will not need to use these outputs, but all providers that implement the PKIX validation or building algorithm must support them.")

[The PKIXBuilderParameters
Class](java-pki-programmers-guide.htm#GUID-BB092D65-80CA-457E-A7B4-F1B41A1A674A "The PKIXBuilderParameters class specifies the set of parameters to be used with CertPathBuilder class.")

[The PKIXCertPathBuilderResult
Class](java-pki-programmers-guide.htm#GUID-BF0E3B2B-1DA5-4A95-A8DD-C03C04EA70E7 "The PKIXCertPathBuilderResult class represents the successful result of the PKIX certification path construction algorithm.")

[The PKIXCertPathChecker
Class](java-pki-programmers-guide.htm#GUID-D46630F6-939D-4054-A451-3D8206ED4E62 "The PKIXCertPathChecker class allows a user to extend a PKIX CertPathValidator or CertPathBuilder implementation. This is an advanced feature that most users will not need to understand. However, anyone implementing a PKIX service provider should read this section")

[Using PKIXCertPathChecker in Certificate Path
Validation](java-pki-programmers-guide.htm#GUID-F727578E-71D0-4BC5-9B06-47EE13F9CBCF "Using a PKIXCertPathChecker to customize certificate path validation is relatively straightforward.")

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-772D31A0-FF9B-4A1E-985B-2100177C74F9}

#### The TrustAnchor Class {#JSSEC-GUID-772D31A0-FF9B-4A1E-985B-2100177C74F9 .sect4}

<div>
The `TrustAnchor`{.codeph} class represents a \"most-trusted CA\", which
is used as a trust anchor for validating X.509 certification paths.

A `TrustAnchor`{.codeph} includes the public key of the CA, the CA\'s
name, and any constraints on the set of paths that can be validated
using this key. These parameters can be specified in the form of a
trusted `X509Certificate`{.codeph} or as individual parameters.

All `TrustAnchor`{.codeph} objects are immutable and thread-safe. That
is, multiple threads may concurrently invoke the methods defined in this
class on a single `TrustAnchor`{.codeph} object (or more than one) with
no ill effects. Requiring `TrustAnchor`{.codeph} objects to be immutable
and thread-safe allows them to be passed around to various pieces of
code without worrying about coordinating access.

<div class="p">
<div class="infoboxnote" id="GUID-772D31A0-FF9B-4A1E-985B-2100177C74F9__GUID-A6811FA1-310C-4285-8B60-CFFE15ADB5EF">
Note:

Although this class is described as a PKIX class it may be used with
other X.509 certification path validation algorithms.

</div>
</div>
<div class="section">
Creating a TrustAnchor Object

To instantiate a `TrustAnchor`{.codeph} object, a caller must specify
\"the most-trusted CA\" as a trusted `X509Certificate`{.codeph} or
public key and distinguished name pair. The caller may also optionally
specify name constraints that are applied to the trust anchor by the
validation algorithm during initialization. Note that support for name
constraints on trust anchors is not required by the PKIX algorithm,
therefore a PKIX `CertPathValidator`{.codeph} or
`CertPathBuilder`{.codeph} may choose not to support this parameter and
instead throw an exception. Use one of the following constructors to
create a `TrustAnchor`{.codeph} object:

``` {.codeblock dir="ltr"}
        public TrustAnchor(X509Certificate trustedCert, 
                byte[] nameConstraints)
        public TrustAnchor(X500Principal caPrincipal, PublicKey pubKey, 
                byte[] nameConstraints)
        public TrustAnchor(String caName, PublicKey pubKey, 
                byte[] nameConstraints)
```

The `nameConstraints`{.codeph} parameter is specified as a byte array
containing the ASN.1 DER encoding of a NameConstraints extension. An
`IllegalArgumentException`{.codeph} is thrown if the name constraints
cannot be decoded (are not formatted correctly).

</div>
<!-- class="section" -->

<div class="section">
Getting Parameter Values

Each of the parameters can be retrieved using a corresponding get
method:

``` {.codeblock dir="ltr"}
        public final X509Certificate getTrustedCert()
        public final X500Principal getCA()
        public final String getCAName()
        public final PublicKey getCAPublicKey()
        public final byte[] getNameConstraints()
```

<div class="infoboxnote" id="GUID-772D31A0-FF9B-4A1E-985B-2100177C74F9__GUID-096C0339-B93D-4C97-8EF4-83EAB4B4F0F0">
Note:

The `getTrustedCert`{.codeph} method returns `null`{.codeph} if the
trust anchor was specified as a public key and name pair. Likewise, the
`getCA`{.codeph}, `getCAName`{.codeph} and `getCAPublicKey`{.codeph}
methods return `null`{.codeph} if the trust anchor was specified as an
`X509Certificate`{.codeph}.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-3D95A3BE-74CB-4357-BB85-9A8DEA36A457}

#### The PKIXParameters Class {#JSSEC-GUID-3D95A3BE-74CB-4357-BB85-9A8DEA36A457 .sect4}

<div>
The `PKIXParametersClass`{.codeph} class specifies the set of input
parameters defined by the PKIX certification path validation algorithm.
It also includes a few additional useful parameters.

This class implements the `CertPathParameters`{.codeph} interface.

An X.509 `CertPath`{.codeph} object and a `PKIXParameters`{.codeph}
object are passed as arguments to the `validate`{.codeph} method of a
`CertPathValidator`{.codeph} instance implementing the PKIX algorithm.
The `CertPathValidator`{.codeph} uses the parameters to initialize the
PKIX certification path validation algorithm.

<div class="section">
Creating a PKIXParameters Object

To instantiate a `PKIXParameters`{.codeph} object, a caller must specify
\"the most-trusted CA(s)\" as defined by the PKIX validation algorithm.
The most-trusted CAs can be specified using one of two constructors:

``` {.codeblock dir="ltr"}
        public PKIXParameters(Set<TrustAnchor> trustAnchors) 
            throws InvalidAlgorithmParameterException
        public PKIXParameters(KeyStore keystore)
            throws KeyStoreException, InvalidAlgorithmParameterException
```

The first constructor allows the caller to specify the most-trusted CAs
as a `Set`{.codeph} of `TrustAnchor`{.codeph} objects. Alternatively, a
caller can use the second constructor and specify a `KeyStore`{.codeph}
instance containing trusted certificate entries, each of which will be
considered as a most-trusted CA.

</div>
<!-- class="section" -->

<div class="section">
Setting Parameter Values

After a `PKIXParameters`{.codeph} object has been created, a caller can
set (or replace the current value of) various parameters. A few of the
methods for setting parameters are described here. Please refer to the
`  PKIXParameters `{.codeph} API documentation for details on the other
methods.

The `setInitialPolicies`{.codeph} method sets the initial policy
identifiers, as specified by the PKIX validation algorithm. The elements
of the `Set`{.codeph} are object identifiers (OIDs) represented as a
`String`{.codeph}. If the `initialPolicies`{.codeph} parameter is null
or not set, any policy is acceptable:

``` {.codeblock dir="ltr"}
        public void setInitialPolicies(Set<String> initialPolicies)
```

The `setDate`{.codeph} method sets the time for which the validity of
the path should be determined. If the `date`{.codeph} parameter is not
set or is null, the current date is used:

``` {.codeblock dir="ltr"}
        public void setDate(Date date)
```

The `setPolicyMappingInhibited`{.codeph} method sets the value of the
policy mapping inhibited flag. The default value for the flag, if not
specified, is false:

``` {.codeblock dir="ltr"}
        public void setPolicyMappingInhibited(boolean val)
```

The `setExplicitPolicyRequired`{.codeph} method sets the value of the
explicit policy required flag. The default value for the flag, if not
specified, is false:

``` {.codeblock dir="ltr"}
        public void setExplicitPolicyRequired(boolean val)
```

The `setAnyPolicyInhibited`{.codeph} method sets the value of the any
policy inhibited flag. The default value for the flag, if not specified,
is false:

``` {.codeblock dir="ltr"}
        public void setAnyPolicyInhibited(boolean val)
```

The `setTargetCertConstraints`{.codeph} method allows the caller to set
constraints on the target or end-entity certificate. For example, the
caller can specify that the target certificate must contain a specific
subject name. The constraints are specified as a `CertSelector`{.codeph}
object. If the `selector`{.codeph} parameter is null or not set, no
constraints are defined on the target certificate:

``` {.codeblock dir="ltr"}
        public void setTargetCertConstraints(CertSelector selector)
```

The `setCertStores`{.codeph} method allows a caller to specify a
`List`{.codeph} of `CertStore`{.codeph} objects that will be used by a
PKIX implementation of `CertPathValidator`{.codeph} to find CRLs for
path validation. This provides an extensible mechanism for specifying
where to locate CRLs. The `setCertStores`{.codeph} method takes a
`List`{.codeph} of `CertStore`{.codeph} objects as a parameter. The
first `CertStore`{.codeph}s in the list may be preferred to those that
appear later.

``` {.codeblock dir="ltr"}
        public void setCertStores(List<CertStore> stores)
```

The `setCertPathCheckers`{.codeph} method allows a caller to extend the
PKIX validation algorithm by creating implementation-specific
certification path checkers. For example, this mechanism can be used to
process private certificate extensions. The
`setCertPathCheckers`{.codeph} method takes a list of
`PKIXCertPathChecker`{.codeph} (discussed later) objects as a parameter:

``` {.codeblock dir="ltr"}
        public void setCertPathCheckers(List<PKIXCertPathChecker> checkers)
```

The `setRevocationEnabled`{.codeph} method allows a caller to disable
revocation checking. Revocation checking is enabled by default, since it
is a required check of the PKIX validation algorithm. However, PKIX does
not define how revocation should be checked. An implementation may use
CRLs or OCSP, for example. This method allows the caller to disable the
implementation\'s default revocation checking mechanism if it is not
appropriate. A different revocation checking mechanism can then be
specified by calling the `setCertPathCheckers`{.codeph} method, and
passing it a `PKIXCertPathChecker`{.codeph} that implements the
alternate mechanism.

``` {.codeblock dir="ltr"}
        public void setRevocationEnabled(boolean val)
```

The `setPolicyQualifiersRejected`{.codeph} method allows a caller to
enable or disable policy qualifier processing. When a
`PKIXParameters`{.codeph} object is created, this flag is set to
`true`{.codeph}. This setting reflects the most common (and simplest)
strategy for processing policy qualifiers. Applications that want to use
a more sophisticated policy must set this flag to `false`{.codeph}.

``` {.codeblock dir="ltr"}
        public void setPolicyQualifiersRejected(boolean qualifiersRejected)
```

</div>
<!-- class="section" -->

<div class="section">
Getting Parameter Values

The current values for each of the parameters can be retrieved using an
appropriate `get`{.codeph} method. Please refer to the
`Class PKIXParameters`{.codeph}</a></code> API documentation for further
details on these methods.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-DF6CA960-B37A-4EE1-9E43-76561F711A7D}

#### The PKIXCertPathValidatorResult Class {#JSSEC-GUID-DF6CA960-B37A-4EE1-9E43-76561F711A7D .sect4}

<div>
The `PKIXCertPathValidatorResult`{.codeph} class represents the result
of the PKIX certification path validation algorithm.

This class implements the `CertPathValidatorResult`{.codeph} interface. 
It holds the valid policy tree and subject public key resulting from the
validation algorithm, and includes methods (`getPolicyTree()`{.codeph}
and `getPublicKey()`{.codeph}) for returning them. Instances of
`PKIXCertPathValidatorResult`{.codeph} are returned by the
`validate`{.codeph} method of `CertPathValidator`{.codeph} objects
implementing the PKIX algorithm.

Please refer to the `PKIXCertPathValidatorResult`{.codeph}</a></code>
API documentation for more detailed information on this class.

</div>
</div>
<div class="sect4">
[]{#GUID-3AD41382-E729-469B-83EE-CB2FE66D71D8}

#### The PolicyNode Interface and PolicyQualifierInfo Class {#JSSEC-GUID-3AD41382-E729-469B-83EE-CB2FE66D71D8 .sect4}

<div>
The PKIX validation algorithm defines several outputs related to
certificate policy processing. Most applications will not need to use
these outputs, but all providers that implement the PKIX validation or
building algorithm must support them.

<div class="section">
The `PolicyNode`{.codeph} interface represents a node of a valid policy
tree resulting from a successful execution of the PKIX certification
path validation. An application can obtain the root of a valid policy
tree using the `getPolicyTree`{.codeph} method of
`PKIXCertPathValidatorResult`{.codeph}. Policy Trees are discussed in
more detail in the [RFC 5280](http://www.ietf.org/rfc/rfc5280.txt).

The `getPolicyQualifiers`{.codeph} method of `PolicyNode`{.codeph}
returns a `Set`{.codeph} of `PolicyQualifierInfo`{.codeph} objects, each
of which represents a policy qualifier contained in the Certificate
Policies extension of the relevant certificate that this policy applies
to.

Most applications will not need to examine the valid policy tree and
policy qualifiers. They can achieve their policy processing goals by
setting the policy-related parameters in `PKIXParameters`{.codeph}.
However, the valid policy tree is available for more sophisticated
applications, especially those that process policy qualifiers.

Please refer to the `Interface PolicyNode`{.codeph}</a></code> and
`PolicyQualifierInfo`{.codeph}</a></code> API documentation for more
detailed information on these classes.

</div>
<!-- class="section" -->

<div class="example" id="GUID-3AD41382-E729-469B-83EE-CB2FE66D71D8__GUID-C0D7260A-3ACE-449E-A3EE-6C6E42E82B68">
Example 10-1 Example of Validating a Certification Path using the PKIX
algorithm

This is an example of validating a certification path with the PKIX
validation algorithm. The example ignores most of the exception handling
and assumes that the certification path and public key of the trust
anchor have already been created.

First, create the `CertPathValidator`{.codeph}, as in the following
line:

``` {.codeblock dir="ltr"}
    CertPathValidator cpv = CertPathValidator.getInstance("PKIX");
```

The next step is to create a `TrustAnchor`{.codeph} object. This will be
used as an anchor for validating the certification path. In this
example, the most-trusted CA is specified as a public key and name (name
constraints are not applied and are specified as `null`{.codeph}):

``` {.codeblock dir="ltr"}
    TrustAnchor anchor = new TrustAnchor("O=xyz,C=us", pubkey, null);
```

The next step is to create a `PKIXParameters`{.codeph} object. This will
be used to populate the parameters used by the PKIX algorithm. In this
example, we pass to the constructor a `Set`{.codeph} containing a single
element - the `TrustAnchor`{.codeph} we created in the previous step:

``` {.codeblock dir="ltr"}
    PKIXParameters params = new PKIXParameters(Collections.singleton(anchor));
```

Next, we populate the parameters object with constraints or other
parameters used by the validation algorithm. In this example, we enable
the explicitPolicyRequired flag and specify a set of initial policy OIDs
(the contents of the set are not shown):

``` {.codeblock dir="ltr"}
    // set other PKIX parameters here
    params.setExplicitPolicyRequired(true);
    params.setInitialPolicies(policyIds);
```

The final step is to validate the certification path using the input
parameter set we have created:

``` {.codeblock dir="ltr"}
    try {
        PKIXCertPathValidatorResult result =
            (PKIXCertPathValidatorResult) cpv.validate(certPath, params);
        PolicyNode policyTree = result.getPolicyTree();
        PublicKey subjectPublicKey = result.getPublicKey();
    } catch (CertPathValidatorException cpve) {
        System.out.println("Validation failure, cert[" 
            + cpve.getIndex() + "] :" + cpve.getMessage());
    }
```

If the validation algorithm is successful, the policy tree and subject
public key resulting from the validation algorithm are obtained using
the `getPolicyTree`{.codeph} and `getPublicKey`{.codeph} methods of
`PKIXCertPathValidatorResult`{.codeph}.

Otherwise, a `CertPathValidatorException`{.codeph} is thrown and the
caller can catch the exception and print some details about the failure,
such as the error message and the index of the certificate that caused
the failure.

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-BB092D65-80CA-457E-A7B4-F1B41A1A674A}

#### The PKIXBuilderParameters Class {#JSSEC-GUID-BB092D65-80CA-457E-A7B4-F1B41A1A674A .sect4}

<div>
The `PKIXBuilderParameters`{.codeph} class specifies the set of
parameters to be used with` CertPathBuilder`{.codeph} class.

This class (which extends the `PKIXParameters`{.codeph} class) specifies
the set of parameters to be used with
[CertPathBuilder](java-pki-programmers-guide.htm#GUID-BEFCC824-21C1-4AD3-B670-D0CA01F08D95 "The CertPathBuilder class is an engine class used to build a certification path.")
class that build certification paths validated against the PKIX
certification path validation algorithm.

A `PKIXBuilderParameters`{.codeph} object is passed as an argument to
the `build`{.codeph} method of a `CertPathBuilder`{.codeph} instance
implementing the PKIX algorithm. All PKIX `CertPathBuilder`{.codeph}s
<span class="variable">must</span> return certification paths which have
been validated according to the PKIX certification path validation
algorithm.

Please note that the mechanism that a PKIX `CertPathBuilder`{.codeph}
uses to validate a constructed path is an implementation detail. For
example, an implementation might attempt to first build a path with
minimal validation and then fully validate it using an instance of a
PKIX `CertPathValidator`{.codeph}, whereas a more efficient
implementation may validate more of the path as it is building it, and
backtrack to previous stages if it encounters validation failures or
dead-ends.

<div class="section">
Creating a PKIXBuilderParameters Object

Creating a `PKIXBuilderParameters`{.codeph} object is similar to
creating a `PKIXParameters`{.codeph} object. However, a caller
<span class="variable">must</span> specify constraints on the target or
end-entity certificate when creating a `PKIXBuilderParameters`{.codeph}
object. These constraints should provide the `CertPathBuilder`{.codeph}
with enough information to find the target certificate. The constraints
are specified as a `CertSelector`{.codeph} object. Use one of the
following constructors to create a `PKIXBuilderParameters`{.codeph}
object:

``` {.codeblock dir="ltr"}
        public PKIXBuilderParameters(Set<TrustAnchor> trustAnchors, 
                CertSelector targetConstraints)
                throws InvalidAlgorithmParameterException
        public PKIXBuilderParameters(KeyStore keystore, 
                CertSelector targetConstraints) 
                throws KeyStoreException, InvalidAlgorithmParameterException
                                                
```

</div>
<!-- class="section" -->

<div class="section">
Getting/Setting Parameter Values

The `PKIXBuilderParameters`{.codeph} class inherits all of the
parameters that can be set in the `PKIXParameters`{.codeph} class. In
addition, the `setMaxPathLength`{.codeph} method can be called to place
a limit on the maximum number of certificates in a certification path:

``` {.codeblock dir="ltr"}
        public void setMaxPathLength(int maxPathLength)
```

The `maxPathLength`{.codeph} parameter specifies the maximum number of
non-self-issued intermediate certificates that may exist in a
certification path. A `CertPathBuilder`{.codeph} instance implementing
the PKIX algorithm must not build paths longer than the length
specified. If the value is 0, the path can only contain a single
certificate. If the value is -1, the path length is unconstrained (i.e.,
there is no maximum). The default maximum path length, if not specified,
is 5. This method is useful to prevent the `CertPathBuilder`{.codeph}
from spending resources and time constructing long paths that may or may
not meet the caller\'s requirements.

If any of the CA certificates in the path contain a Basic Constraints
extension, the value of the pathLenConstraint component of the extension
overrides the value of the `maxPathLength`{.codeph} parameter whenever
the result is a certification path of smaller length. There is also a
corresponding `getMaxPathLength`{.codeph} method for retrieving this
parameter:

``` {.codeblock dir="ltr"}
        public int getMaxPathLength()
```

Also, the `setCertStores`{.codeph} method (inherited from the
`PKIXParameters`{.codeph} class) is typically used by a PKIX
implementation of `CertPathBuilder`{.codeph} to find Certificates for
path construction as well as finding CRLs for path validation. This
provides an extensible mechanism for specifying where to locate
Certificates and CRLs.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-BF0E3B2B-1DA5-4A95-A8DD-C03C04EA70E7}

#### The PKIXCertPathBuilderResult Class {#JSSEC-GUID-BF0E3B2B-1DA5-4A95-A8DD-C03C04EA70E7 .sect4}

<div>
The `PKIXCertPathBuilderResult`{.codeph} class represents the successful
result of the PKIX certification path construction algorithm.

This class extends the `PKIXCertPathValidatorResult`{.codeph} class and
implements the `CertPathBuilder`{.codeph} interface.  Instances of
`PKIXCertPathBuilderResult`{.codeph} are returned by the
`build`{.codeph} method of `CertPathBuilder`{.codeph} objects
implementing the PKIX algorithm.

The `getCertPath`{.codeph} method of a
`PKIXCertPathBuilderResult`{.codeph} instance always returns a
`CertPath`{.codeph} object validated using the PKIX certification path
validation algorithm. The returned `CertPath`{.codeph} object does not
include the most-trusted CA certificate that may have been used to
anchor the path. Instead, use the `getTrustAnchor`{.codeph} method to
get the `Certificate`{.codeph} of the most-trusted CA.

See the `PKIXCertPathBuilderResult`{.codeph}</a></code> API
documentation for more detailed information on this class.

<div class="example" id="GUID-BF0E3B2B-1DA5-4A95-A8DD-C03C04EA70E7__GUID-A7BCEA02-89BD-4A73-90B3-B3FA597AB3B3">
Example 10-2 Example of Building a Certification Path using the PKIX
algorithm

This is an example of building a certification path validated against
the PKIX algorithm. Some details have been left out, such as exception
handling, and the creation of the trust anchors and certificates for
populating the `CertStore`{.codeph}.

First, create the `CertPathBuilder`{.codeph}, as in the following
example:

``` {.codeblock dir="ltr"}
    CertPathBuilder cpb = CertPathBuilder.getInstance("PKIX");
```

This call creates a `CertPathBuilder`{.codeph} object that returns paths
validated against the PKIX algorithm.

The next step is to create a `PKIXBuilderParameters`{.codeph} object.
This will be used to populate the PKIX parameters used by the
`CertPathBuilder`{.codeph}:

``` {.codeblock dir="ltr"}
    // Create parameters object, passing it a Set of
    // trust anchors for anchoring the path
    // and a target subject DN.
    X509CertSelector targetConstraints = new X509CertSelector();
    targetConstraints.setSubject("CN=alice,O=xyz,C=us");
    PKIXBuilderParameters params = 
        new PKIXBuilderParameters(trustAnchors, targetConstraints);
```

The next step is to specify the `CertStore`{.codeph} that the
`CertPathBuilder`{.codeph} will use to look for certificates and CRLs.
For this example, we will populate a Collection `CertStore`{.codeph}
with the certificates and CRLs:

``` {.codeblock dir="ltr"}
    CollectionCertStoreParameters ccsp = 
        new CollectionCertStoreParameters(certsAndCrls);
    CertStore store = CertStore.getInstance("Collection", ccsp);
    params.addCertStore(store);
```

The next step is to build the certification path using the input
parameter set we have created:

``` {.codeblock dir="ltr"}
    try {
        PKIXCertPathBuilderResult result = 
            (PKIXCertPathBuilderResult) cpb.build(params);
        CertPath cp = result.getCertPath();
    } catch (CertPathBuilderException cpbe) {
        System.out.println("build failed: " + cpbe.getMessage());
    }
```

If the `CertPathBuilder`{.codeph} cannot build a path that meets the
supplied parameters it will throw a `CertPathBuilderException`{.codeph}.
Otherwise, the validated certification path can be obtained from the
`PKIXCertPathBuilderResult`{.codeph} using the `getCertPath`{.codeph}
method.

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-D46630F6-939D-4054-A451-3D8206ED4E62}

#### The PKIXCertPathChecker Class {#JSSEC-GUID-D46630F6-939D-4054-A451-3D8206ED4E62 .sect4}

<div>
The PKIXCertPathChecker class allows a user to extend a PKIX
`CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph}
implementation. This is an advanced feature that most users will not
need to understand. However, anyone implementing a PKIX service provider
should read this section

The `PKIXCertPathChecker`{.codeph} class is an abstract class that
executes one or more checks on an X.509 certificate. Developers should
create concrete implementations of the `PKIXCertPathChecker`{.codeph}
class when it is necessary to dynamically extend a PKIX
`CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph}
implementation at runtime. The following are a few examples of when a
`PKIXCertPathChecker`{.codeph} implementation is useful:

-   If the revocation mechanism supplied by a PKIX
    `CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph}
    implementation is not adequate: For example, you can use the
    `PKIXRevocationChecker`{.codeph}</a></code> (introduced in JDK 8;
    see [Check Revocation Status of Certificates with
    PKIXRevocationChecker
    Class](java-pki-programmers-guide.htm#GUID-43A3A247-E165-408C-AD74-88A75BFB4750 "An instance of PKIXRevocationChecker checks the revocation status of certificates with the Online Certificate Status Protocol (OCSP) or Certificate Revocation Lists (CRLs)."))
    to have more control over the revocation mechanism, or you can
    implement your own `PKIXCertPathChecker`{.codeph} to check that
    certificates have not been revoked.

-   If the user wants to recognize certificates containing a critical
    private extension. Since the extension is private, it will not be
    recognized by the PKIX `CertPathValidator`{.codeph} or
    `CertPathBuilder`{.codeph} implementation and a
    `CertPathValidatorException`{.codeph} will be thrown. In this case,
    a developer can implement a `PKIXCertPathChecker`{.codeph} that
    recognizes and processes the critical private extension.

-   If the developer wants to record information about each certificate
    processed for debugging or display purposes.

-   If the user wants to reject certificates with certain policy
    qualifiers.

The `setCertPathCheckers`{.codeph} method of the
`PKIXParameters`{.codeph} class allows a user to pass a `List`{.codeph}
of `PKIXCertPathChecker`{.codeph} objects to a PKIX
`CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph}
implementation. Each of the `PKIXCertPathChecker`{.codeph} objects will
be called in turn, for each certificate processed by the PKIX
`CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph}
implementation.

<div class="section">
Creating and using a PKIXCertPathChecker Object

The `PKIXCertPathChecker`{.codeph} class does not have a public
constructor. This is intentional, since creating an instance of
`PKIXCertPathChecker`{.codeph} is an implementation-specific issue. For
example, the constructor for a `PKIXCertPathChecker`{.codeph}
implementation that uses OCSP to check a certificate\'s revocation
status may require the hostname and port of the OCSP server:

``` {.codeblock dir="ltr"}
        PKIXCertPathChecker checker = new OCSPChecker("ocsp.sun.com", 1321);
```

Once the checker has been instantiated, it can be added as a parameter
using the `addCertPathChecker`{.codeph} method of the
`PKIXParameters`{.codeph} class:

``` {.codeblock dir="ltr"}
        params.addCertPathChecker(checker);
```

Alternatively, a `List`{.codeph} of checkers can be added using the
`setCertPathCheckers`{.codeph} method of the `PKIXParameters`{.codeph}
class.

</div>
<!-- class="section" -->

<div class="section">
Implementing a PKIXCertPathChecker Object

The `PKIXCertPathChecker`{.codeph} class is abstract. It has four
methods (`check`{.codeph}, `getSupportedExtensions`{.codeph},
`init`{.codeph}, and `isForwardCheckingSupported`{.codeph}) that all
concrete subclasses must implement.

Implementing a `PKIXCertPathChecker`{.codeph} may be trivial or complex.
A `PKIXCertPathChecker`{.codeph} implementation can be stateless or
stateful. A stateless implementation does not maintain state between
successive calls of the `check`{.codeph} method. For example, a
`PKIXCertPathChecker`{.codeph} that checks that each certificate
contains a particular policy qualifier is stateless. In contrast, a
stateful implementation does maintain state between successive calls of
the `check`{.codeph} method. The `check`{.codeph} method of a stateful
implementation usually depends on the contents of prior certificates in
the certification path. For example, a `PKIXCertPathChecker`{.codeph}
that processes the NameConstraints extension is stateful.

Also, the order in which the certificates processed by a service
provider implementation are presented (passed) to a
`PKIXCertPathChecker`{.codeph} is very important, especially if the
implementation is stateful. Depending on the algorithm used by the
service provider, the certificates may be presented in
<span class="variable">reverse</span> or
<span class="variable">forward</span> order. A reverse ordering means
that the certificates are ordered from the most trusted CA (if present)
to the target subject, whereas a forward ordering means that the
certificates are ordered from the target subject to the most trusted CA.
The order must be made known to the `PKIXCertPathChecker`{.codeph}
implementation, so that it knows how to process consecutive
certificates.

</div>
<!-- class="section" -->

<div class="section">
Initializing a PKIXCertPathChecker Object

The `init`{.codeph} method initializes the internal state of the
checker:

``` {.codeblock dir="ltr"}
        public abstract void init(boolean forward)
```

All stateful implementations should clear or initialize any internal
state in the checker. This prevents a service provider implementation
from calling a checker that is in an uninitialized state. It also allows
stateful checkers to be reused in subsequent operations without
reinstantiating them. The `forward`{.codeph} parameter indicates the
order of the certificates presented to the
`PKIXCertPathChecker`{.codeph}. If `forward`{.codeph} is
`true`{.codeph}, the certificates are presented from target to trust
anchor; if `false`{.codeph}, from trust anchor to target.

</div>
<!-- class="section" -->

<div class="section">
Forward Checking

The `isForwardCheckingSupported`{.codeph} method returns a
`boolean`{.codeph} that indicates if the `PKIXCertPathChecker`{.codeph}
supports forward checking:

``` {.codeblock dir="ltr"}
        public abstract boolean isForwardCheckingSupported()
```

All `PKIXCertPathChecker`{.codeph} implementations
<span class="variable">must</span>support reverse checking. A
`PKIXCertPathChecker`{.codeph} implementation
<span class="variable">may</span>support forward checking.

Supporting forward checking improves the efficiency of
`CertPathBuilder`{.codeph}s that build forward, since it allows paths to
be checked as they are built. However, some stateful
`PKIXCertPathChecker`{.codeph}s may find it difficult or impossible to
support forward checking.

</div>
<!-- class="section" -->

<div class="section">
Supported Extensions

The `getSupportedExtensions`{.codeph} method returns an immutable
`Set`{.codeph} of OID `String`{.codeph}s for the X.509 extensions that
the `PKIXCertPathChecker`{.codeph} implementation supports (i.e.,
recognizes, is able to process):

``` {.codeblock dir="ltr"}
        public abstract Set<String> getSupportedExtensions()
```

The method should return `null`{.codeph} if no extensions are processed.
All implementations should return the `Set`{.codeph} of OID
`String`{.codeph}s that the `check`{.codeph} method may process.

A `CertPathBuilder`{.codeph} can use this information to identify
certificates with unrecognized critical extensions, even when performing
a forward build with a `PKIXCertPathChecker`{.codeph} that does not
support forward checking.

</div>
<!-- class="section" -->

<div class="section">
Executing the Check

The following method executes a check on the certificate:

``` {.codeblock dir="ltr"}
        public abstract void 
                check(Certificate cert, Collection<String> unresolvedCritExts)
                throws CertPathValidatorException
```

The `unresolvedCritExts`{.codeph} parameter contains a collection of
OIDs as `String`{.codeph}s. These OIDs represent the set of critical
extensions in the certificate that have not yet been resolved by the
certification path validation algorithm. Concrete implementations of the
`check`{.codeph} method should remove any critical extensions that it
processes from the `unresolvedCritExts`{.codeph} parameter.

If the certificate does not pass the check(s), a
`CertPathValidatorException`{.codeph} should be thrown.

</div>
<!-- class="section" -->

<div class="section">
Cloning a PKIXCertPathChecker

The `PKIXCertPathChecker`{.codeph} class implements the
`Cloneable`{.codeph} interface. All stateful
`PKIXCertPathChecker`{.codeph} implementations must override the
`clone`{.codeph} method if necessary. The default implementation of the
`clone`{.codeph} method calls the `Object.clone`{.codeph} method, which
performs a simple clone by copying all fields of the original object to
the new object. A stateless implementation should not override the
`clone`{.codeph} method. However, all stateful implementations must
ensure that the default `clone`{.codeph} method is correct, and override
it if necessary. For example, a `PKIXCertPathChecker`{.codeph} that
stores state in an array must override the `clone`{.codeph} method to
make a copy of the array, rather than just a reference to the array.

The reason that `PKIXCertPathChecker`{.codeph} objects are
`Cloneable`{.codeph} is to allow a PKIX `CertPathBuilder`{.codeph}
implementation to efficiently backtrack and try another path when a
potential certification path reaches a dead end or point of failure. In
this case, the implementation is able to restore prior path validation
states by restoring the cloned objects.

</div>
<!-- class="section" -->

<div class="example" id="GUID-D46630F6-939D-4054-A451-3D8206ED4E62__GUID-44A52013-BF80-49DC-BE95-A0AC981333E7">
Example 10-3 Sample Code to Check for a Private Extension

This is an example of a stateless `PKIXCertPathChecker`{.codeph}
implementation. It checks if a private extension exists in a certificate
and processes it according to some rules.

``` {.codeblock dir="ltr"}
        import java.security.cert.Certificate;
        import java.security.cert.X509Certificate;
        import java.util.Collection;
        import java.util.Collections;
        import java.util.Set;
        import java.security.cert.PKIXCertPathChecker;
        import java.security.cert.CertPathValidatorException;

        public class MyChecker extends PKIXCertPathChecker {
            private static Set supportedExtensions =
                Collections.singleton("2.16.840.1.113730.1.1");

            /*
             * Initialize checker
             */
            public void init(boolean forward) 
                throws CertPathValidatorException {
                // nothing to initialize
            }

            public Set getSupportedExtensions() {        
                return supportedExtensions;
            }

            public boolean isForwardCheckingSupported() {
                return true;
            }

            /*
             * Check certificate for presence of Netscape's
             * private extension
             * with OID "2.16.840.1.113730.1.1"
             */
            public void check(Certificate cert, 
                              Collection unresolvedCritExts)
                throws CertPathValidatorException 
            {
                X509Certificate xcert = (X509Certificate) cert;
                byte[] ext = 
                    xcert.getExtensionValue("2.16.840.1.113730.1.1");
                if (ext == null)
                    return;

                //
                // process private extension according to some 
                // rules - if check fails, throw a 
                // CertPathValidatorException ...
                // {insert code here}

                // remove extension from collection of unresolved 
                // extensions (if it exists)
                if (unresolvedCritExts != null)
                    unresolvedCritExts.remove("2.16.840.1.113730.1.1");
            }
        }
```

</div>
<!-- class="example" -->

<div class="section">
How a PKIX Service Provider implementation should use a
PKIXCertPathChecker

Each `PKIXCertPathChecker`{.codeph} object must be initialized by a
service provider implementation before commencing the build or
validation algorithm, for example:

``` {.codeblock dir="ltr"}
        List<PKIXCertPathChecker> checkers = params.getCertPathCheckers();
        for (PKIXCertPathChecker checker : checkers) {
            checker.init(false);
        }
```

For each certificate that it validates, the service provider
implementation must call the `check`{.codeph} method of each
`PKIXCertPathChecker`{.codeph} object in turn, passing it the
certificate and any remaining unresolved critical extensions:

``` {.codeblock dir="ltr"}
        for (PKIXCertPathChecker checker : checkers) {
            checker.check(cert, unresolvedCritExts);
        }
```

If any of the `check`{.codeph}s throw a
`CertPathValidatorException`{.codeph}, a `CertPathValidator`{.codeph}
implementation should terminate the validation procedure. However, a
`CertPathBuilder`{.codeph} implementation may simply log the failure and
continue to search for other potential paths. If all of the
`check`{.codeph}s are successful, the service provider implementation
should check that all critical extensions have been resolved and if not,
consider the validation to have failed. For example:

``` {.codeblock dir="ltr"}
        if (unresolvedCritExts != null &&
            !unresolvedCritExts.isEmpty())
        {
            // note that a CertPathBuilder may have an enclosing
            // try block to catch the exception below and continue on error
            throw new CertPathValidatorException
                ("Unrecognized Critical Extension");
        }
```

As discussed in the previous section, a `CertPathBuilder`{.codeph}
implementation may need to backtrack when a potential certification path
reaches a dead end or point of failure. Backtracking in this context
implies returning to the previous certificate in the path and checking
for other potential paths. If the `CertPathBuilder`{.codeph}
implementation is validating the path as it is building it, it will need
to restore the previous state of each `PKIXCertPathChecker`{.codeph}. It
can do this by making clones of the `PKIXCertPathChecker`{.codeph}
objects <span class="variable">before</span> each certificate is
processed, for example:

``` {.codeblock dir="ltr"}
        /* clone checkers */
        List newList = new ArrayList(checkers);
        ListIterator li = newList.listIterator();
        while (li.hasNext()) {   
            PKIXCertPathChecker checker = (PKIXCertPathChecker) li.next();
            li.set(checker.clone());
        }
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-F727578E-71D0-4BC5-9B06-47EE13F9CBCF}

#### Using PKIXCertPathChecker in Certificate Path Validation {#JSSEC-GUID-F727578E-71D0-4BC5-9B06-47EE13F9CBCF .sect4}

<div>
Using a `PKIXCertPathChecker`{.codeph} to customize certificate path
validation is relatively straightforward.

<div class="section">
Basic Certification Path Validation

First, consider code that validates a certificate path:

``` {.codeblock dir="ltr"}
Set<TrustAnchor> trustAnchors = getTrustAnchors();
CertPath cp = getCertPath();

PKIXParameters pkixp = new PKIXParameters(trustAnchors);
pkixp.setRevocationEnabled(false);

CertPathValidator cpv = CertPathValidator.getInstance("PKIX");
PKIXCertPathValidatorResult pcpvr =
    (PKIXCertPathValidatorResult)cpv.validate(cp, pkixp);
```

If the validation fails, the `validate()`{.codeph} method throws an
exception.

The fundamental steps are as follows:

1.  Obtain the CA root certificates and the certification path to be
    validated.
2.  Create a `PKIXParameters`{.codeph} with the trust anchors.
3.  Use a `CertPathValidator`{.codeph} to validate the certificate path.

In this example, `getTrustAnchors()`{.codeph} and
`getCertPath()`{.codeph} are the methods that obtain CA root
certificates and the certification path.

The `getTrustAnchors()`{.codeph} method in the example must return a
`Set`{.codeph} of `TrustAnchor`{.codeph}s that represent the CA root
certificates you wish to use for validation. Here is one simple
implementation that loads a single CA root certificate from a file:

``` {.codeblock dir="ltr"}
public Set<TrustAnchor> getTrustAnchors()
    throws IOException, CertificateException {

  CertificateFactory cf = CertificateFactory.getInstance("X.509");

  X509Certificate c;
  try (InputStream in = new FileInputStream("x509_ca-certificate.cer")) {
    c = (X509Certificate)cf.generateCertificate(in);
  }

  TrustAnchor anchor = new TrustAnchor(c, null);
  return Collections.singleton(anchor);
}
```

Similarly, here is a simple implementation of `getCertPath()`{.codeph}
that loads a certificate path from a file:

``` {.codeblock dir="ltr"}
public CertPath getCertPath() throws IOException, CertificateException {
  CertificateFactory cf = CertificateFactory.getInstance("X.509");

  CertPath cp;
  try (InputStream in = new FileInputStream("certpath.pkcs7")) {     
    cp = cf.generateCertPath(in, "PKCS7");
  }   
  return cp;
}
```

Note that PKCS\#7 does not require a specific order for the certificates
in the file, so this code only works for certification path validation
when the certificates are ordered starting from the entity to be
validated and progressing back toward the CA root. If the certificates
are not in the right order, you need to do some additional processing.
`CertificateFactory`{.codeph} has a `generateCertPath()`{.codeph} method
that accepts a `Collection`{.codeph}, which is useful for this type of
processing.

</div>
<!-- class="section" -->

<div class="section">
Adding in a `PKIXCertPathChecker`{.codeph}

To customize certification path validation, add a
`PKIXCertPathChecker`{.codeph} as follows. In this example,
`SimpleChecker`{.codeph} is a `PKIXCertPathChecker`{.codeph} subclass.
The new lines are shown in <span class="bold">bold</span>.

``` {.codeblock dir="ltr"}
Set<TrustAnchor> trustAnchors = getTrustAnchors();
CertPath cp = getCertPath();

PKIXParameters pkixp = new PKIXParameters(trustAnchors);
pkixp.setRevocationEnabled(false);

SimpleChecker sc = new SimpleChecker();
pkixp.addCertPathChecker(sc);

CertPathValidator cpv = CertPathValidator.getInstance("PKIX");
PKIXCertPathValidatorResult pcpvr =
    (PKIXCertPathValidatorResult)cpv.validate(cp, pkixp);
```

`SimpleChecker`{.codeph} is a rudimentary subclass of
`PKIXCertPathChecker`{.codeph}. Its `check()`{.codeph} method is called
for every certificate in the certification path that is being validated.
`SimpleChecker`{.codeph} uses an `AlgorithmConstraints`{.codeph}
implementation to examine the signature algorithm and public key of each
certificate.

``` {.codeblock dir="ltr"}
import java.security.AlgorithmConstraints;
import java.security.CryptoPrimitive;
import java.security.Key;
import java.security.cert.*;
import java.util.*;

public class SimpleChecker extends PKIXCertPathChecker {
  private final static Set<CryptoPrimitive> SIGNATURE_PRIMITIVE_SET =
      EnumSet.of(CryptoPrimitive.SIGNATURE);
  
  public void init(boolean forward) throws CertPathValidatorException {}
  
  public boolean isForwardCheckingSupported() { return true; }
  
  public Set<String> getSupportedExtensions() { return null; }
  
  public void check(Certificate cert,
      Collection<String> unresolvedCritExts)
      throws CertPathValidatorException {
    X509Certificate c = (X509Certificate)cert;
    String sa = c.getSigAlgName();
    Key key = c.getPublicKey();
    
    AlgorithmConstraints constraints = new SimpleConstraints();
    
    if (constraints.permits(SIGNATURE_PRIMITIVE_SET, sa, null) == false)
      throw new CertPathValidatorException("Forbidden algorithm: " + sa);

    if (constraints.permits(SIGNATURE_PRIMITIVE_SET, key) == false)
      throw new CertPathValidatorException("Forbidden key: " + key);
  }
}
```

Finally, `SimpleConstraints`{.codeph} is an
`AlgorithmConstraints`{.codeph} implementation that requires RSA 2048.

``` {.codeblock dir="ltr"}
import java.security.AlgorithmConstraints;
import java.security.AlgorithmParameters;
import java.security.CryptoPrimitive;
import java.security.Key;
import java.security.interfaces.RSAKey;
import java.util.Set;

public class SimpleConstraints implements AlgorithmConstraints {
  public boolean permits(Set<CryptoPrimitive> primitives,
      String algorithm, AlgorithmParameters parameters) {
    return permits(primitives, algorithm, null, parameters);
  }

  public boolean permits(Set<CryptoPrimitive> primitives, Key key) {
    return permits(primitives, null, key, null);
  }
  
  public boolean permits(Set<CryptoPrimitive> primitives,
      String algorithm, Key key, AlgorithmParameters parameters) {
    if (algorithm == null) algorithm = key.getAlgorithm();
    
    if (algorithm.indexOf("RSA") == -1) return false;
    
    if (key != null) {
      RSAKey rsaKey = (RSAKey)key;
      int size = rsaKey.getModulus().bitLength();
      if (size < 2048) return false;
    }

    return true;
  }
}
```

</div>
<!-- class="section" -->

</div>
<div class="sect5">
[]{#GUID-43A3A247-E165-408C-AD74-88A75BFB4750}

##### Check Revocation Status of Certificates with PKIXRevocationChecker Class {#JSSEC-GUID-43A3A247-E165-408C-AD74-88A75BFB4750 .sect5}

<div>
An instance of `PKIXRevocationChecker`{.codeph} checks the revocation
status of certificates with the Online Certificate Status Protocol
(OCSP) or Certificate Revocation Lists (CRLs).

The `PKIXRevocationChecker`{.codeph}</a></code> (introduced in JDK 8),
which is a subclass of `PKIXCertPathChecker`{.codeph}, checks the
revocation status of certificates with the PKIX algorithm.

An instance of `PKIXRevocationChecker`{.codeph} checks the revocation
status of certificates with the Online Certificate Status Protocol
(OCSP) or Certificate Revocation Lists (CRLs). OCSP is described in [RFC
2560](http://www.ietf.org/rfc/rfc2560.txt) and is a network protocol for
determining the status of a certificate. A CRL is a time-stamped list
identifying revoked certificates, and RFC 5280 describes an algorithm
for determining the revocation status of certificates using CRLs.

Each PKIX `CertPathValidator`{.codeph} and `CertPathBuilder`{.codeph}
instance provides a default revocation implementation that is enabled by
default. If you want more control over the revocation settings used by
that implementation, use the `PKIXRevocationChecker`{.codeph} class.

Follow these general steps to check the revocation status of a
certificate path with the `PKIXRevocationChecker`{.codeph} class:

1.  Obtain a `PKIXRevocationChecker`{.codeph} instance by calling the
    `getRevocationChecker`{.codeph} method of a PKIX
    `CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph} instance.

2.  Set additional parameters and options specific to certificate
    revocation with methods contained in the
    `PKIXRevocationChecker`{.codeph} class. These methods include
    `setOCSPResponder(URI)`{.codeph}</a></code>, which sets the URI that
    identifies the location of the OCSP responder (although normally the
    URI is included in the certificate and does not have to be set) and
    `setOptions(Set<PKIXRevocationChecker.Option>)`{.codeph}</a></code>,
    which sets revocation options.
    `PKIXRevocationChecker.Option`{.codeph}</a></code> is an enumerated
    type used to specify the following options:

    -   `ONLY_END_ENTITY`{.codeph}: Only check the revocation status of
        end-entity certificates.
    -   `PREFER_CRLS`{.codeph}: By default, OCSP is the preferred
        mechanism for checking revocation status, with CRLs as the
        fallback mechanism. Switch this preference to CRLs with this
        option.
    -   `SOFT_FAIL`{.codeph}: Ignore network failures.

3.  After obtaining an instance of `PKIXRevocationChecker`{.codeph}, add
    it to a `PKIXParameters`{.codeph} or
    `PKIXBuilderParameters`{.codeph} object with the
    `addCertPathChecker`{.codeph}</a></code> or
    `setCertPathCheckers`{.codeph}</a></code> method.

4.  Follow one of these steps depending on whether you are using a PKIX
    `CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph} instance:

    -   If you are using a PKIX `CertPathValidator`{.codeph} instance,
        call the `validate`{.codeph}</a></code> method using as
        arguments the certificate path you want to validate and the
        `PKIXParameters`{.codeph} object that contains a revocation
        checker.

    -   If you are using a PKIX `CertPathBuilder`{.codeph} instance,
        call the `build`{.codeph}</a></code> method using as arguments
        the `PKIXBuilderParameters`{.codeph} object that contains a
        revocation checker.

5.  Call the `validate`{.codeph} method of the PKIX
    `CertPathValidator`{.codeph} or `CertPathBuilder`{.codeph} instance
    using as arguments the certificate path you want to validate and the
    `PKIXParameters`{.codeph} or `PKIXBuilderParameters`{.codeph} object
    that contains a revocation checker.

The following excerpt checks the revocation status of certificates
contained in a certificate path. The `CertPath`{.codeph} object
`path`{.codeph} is the certificate path, and `params`{.codeph} is an
object of type `PKIXParameters`{.codeph}:

``` {.codeblock dir="ltr"}
    CertPathValidator cpv = CertPathValidator.getInstance("PKIX");
    PKIXRevocationChecker rc = (PKIXRevocationChecker)cpv.getRevocationChecker();
    rc.setOptions(EnumSet.of(Option.SOFT_FAIL));
    params.addCertPathChecker(rc);
    params.setRevocationEnabled(false);
    CertPathValidatorResult res = cpv.validate(path, params);
```

In this excerpt, the `SOFT_FAIL`{.codeph} option causes the revocation
checker to ignore any network failures (such as failing to establish a
connection to the OCSP server) when it checks the revocation status.

</div>
</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-266DD62E-39A7-435B-90DF-7EB1425D56E1}

Implementing a Service Provider {#JSSEC-GUID-266DD62E-39A7-435B-90DF-7EB1425D56E1 .sect2}
-------------------------------

<div>
Experienced programmers can create their own provider packages supplying
certification path service implementations.

<div class="section">
This section assumes that you have read [Java Cryptography Architecture
(JCA) Reference
Guide](java-cryptography-architecture-jca-reference-guide.htm#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.").

The following engine classes are defined in the Java Certification Path
API:

-   <span class="bold">`CertPathValidator`{.codeph}</span> - used to
    validate certification paths

-   <span class="bold">`CertPathBuilder`{.codeph}</span> - used to build
    certification paths

-   <span class="bold">`CertStore`{.codeph}</span> - used to retrieve
    certificates and CRLs from a repository

In addition, the pre-existing `CertificateFactory`{.codeph} engine class
also supports the generation of certification paths.

The application interfaces supplied by an engine class are implemented
in terms of a \"Service Provider Interface\" (SPI). The name of each SPI
class is the same as that of the corresponding engine class, followed by
\"Spi\". For example, the SPI class corresponding to the
`CertPathValidator`{.codeph} engine class is the
`CertPathValidatorSpi`{.codeph} class. Each SPI class is abstract. To
supply the implementation of a particular type of service, for a
specific algorithm or type, a provider must subclass the corresponding
SPI class and provide implementations for all the abstract methods. For
example, the `CertStore`{.codeph} class provides access to the
functionality of retrieving certificates and CRLs from a repository. The
actual implementation supplied in a `CertStoreSpi`{.codeph} subclass
would be that for a specific type of certificate repository, such as
LDAP.

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-BFF21E4E-30F9-4D92-BD1E-C530DD33609F}

### Steps to Implement and Integrate a Provider {#JSSEC-GUID-BFF21E4E-30F9-4D92-BD1E-C530DD33609F .sect3}

<div>
When implementing and integrating a provider for the certification path
services, you must ensure that certain information is provided.

<div class="section">
Developers should follow the [Steps to Implement and Integrate a
Provider](howtoimplaprovider.htm#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:").
Here are some additional rules to follow for certain steps:

</div>
<!-- class="section" -->

<div class="section">
Step 3: Write your \"Master Class\", a subclass of Provider

In [Step 3: Write Your Master Class, a Subclass of
Provider](howtoimplaprovider.htm#GUID-1C82EDB9-96CA-44AB-8590-E299814D6A46 "Create a subclass of the java.security.Provider class. This is essentially a lookup table that advertises the algorithms that your provider implements.")
these are the properties that must be defined for the certification path
services, where the algorithm name is substituted for
<span class="variable">algName</span>, and certstore type for
<span class="variable">storeType</span>:

-   `CertPathValidator`{.codeph}.<span class="variable">algName</span>

-   `CertPathBuilder`{.codeph}.<span class="variable">algName</span>

-   `CertStore`{.codeph}.<span class="variable">storeType</span>

See [Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
for the standard names that are defined for
<span class="variable">algName</span> and
<span class="variable">storeType</span>. The value of each property must
be the fully qualified name of the class implementing the specified
algorithm, or certstore type. That is, it must be the package name
followed by the class name, where the two are separated by a period. For
example, a provider sets the `CertPathValidator.PKIX`{.codeph} property
to have the value
`"sun.security.provider.certpath.PKIXCertPathValidator" ` as follows:

``` {.codeblock dir="ltr"}
put("CertPathValidator.PKIX", "sun.security.provider.certpath.PKIXCertPathValidator")
```

In addition, service attributes can be defined for the certification
path services. These attributes can be used as filters for selecting
service providers. See Appendix A for the definition of some standard
service attributes. For example, a provider may set the
`ValidationAlgorithm`{.codeph} service attribute to the name of an RFC
or specification that defines the PKIX validation algorithm:

``` {.codeblock dir="ltr"}
put("CertPathValidator.PKIX ValidationAlgorithm", "RFC5280");
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-BFF21E4E-30F9-4D92-BD1E-C530DD33609F__GUID-37433574-5578-471C-8D0A-9293E3E576DD">
Step 11: Document your Provider and its Supported Services

In [Step 12: Document Your Provider and Its Supported
Services](howtoimplaprovider.htm#GUID-912FAB1D-628A-47EA-A1DD-A216F2DD4245),
certification path service providers should document the following
information for each SPI:

<span class="bold">Certificate Factories</span>

A provider should document what types of certification paths (and the
version numbers of the certificates in the path, if relevant) can be
created by the factory. A provider should describe the ordering of the
certificates in the certification path, as well as the contents.

A provider should document the list of encoding formats supported. This
is not technically necessary, since the client can request them by
calling the <span class="apiname">getCertPathEncodings</span> method.
However, the documentation should describe each encoding format in more
detail and reference any standards when applicable.

<span class="bold">Certification Path Validators</span>

A provider should document any relevant information regarding the
`CertPathValidator`{.codeph} implementation, including the types of
certification paths that it validates. In particular, a PKIX
`CertPathValidator`{.codeph} implementation should document the
following information:

-   The RFC or specification it is compliant with.
-   The mechanism it uses to check that certificates have not been
    revoked.
-   Any optional certificate or CRL extensions that it recognizes and
    how it processes them.

<span class="bold">Certification Path Builders</span>

A provider should document any relevant information regarding the
`CertPathBuilder`{.codeph} implementation, including the types of
certification paths that it creates and whether or not they are
validated. In particular a PKIX `CertPathBuilder`{.codeph}
implementation should document the following information:

-   The RFC or specification it is compliant with.
-   The mechanism it uses to check that certificates have not been
    revoked.
-   Any optional certificate or CRL extensions that it recognizes and
    how it processes them.
-   Details on the algorithm it uses for finding certification paths.
    Ex: depth-first, breadth-first, forward (i.e., from target to trust
    anchor(s)), reverse (i.e., from trust anchor(s) to target).
-   The algorithm it uses to select and sort potential certificates. For
    example, given two certificates that are potential candidates for
    the next certificate in the path, what criteria are used to select
    one before the other? What criteria are used to reject a
    certificate?
-   If applicable, the algorithm it uses for backtracking or
    constructing another path (i.e., when potential paths do not meet
    constraints).
-   The types of `CertStore`{.codeph} implementations that have been
    tested. The implementation should be designed to work with any
    `CertStore`{.codeph} type, but this information may still be useful.

All `CertPathBuilder`{.codeph} implementations should provide additional
debugging support, in order to analyze and correct potential path
building problems. Details on how to access this debugging information
should be documented.

<span class="bold">Certificate/CRL Stores</span>

A provider should document what types of certificates and CRLs (and the
version numbers, if relevant) are retrieved by the `CertStore`{.codeph}.

A provider should also document any relevant information regarding the
`CertStore`{.codeph} implementation (such as protocols used or formats
supported). For example, an LDAP `CertStore`{.codeph} implementation
should describe which versions of LDAP are supported and which standard
attributes are used for finding certificates and CRLs. It should also
document if the implementation caches results, and for how long (i.e.,
under what conditions are they refreshed).

If the implementation returns the certificates and CRLs in a particular
order, it should describe the sorting algorithm. An implementation
should also document any additional or default initialization
parameters. Finally, an implementation should document if and how it
uses information in the `CertSelector`{.codeph} or
`CRLSelector`{.codeph} objects to find certificates and CRLs.

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-255CC70E-E05E-4109-AA6E-51B83C5A3618}

#### Service Interdependencies {#JSSEC-GUID-255CC70E-E05E-4109-AA6E-51B83C5A3618 .sect4}

<div>
Common types of algorithm interdependencies in certification path
service implementations.

The following are some common types of algorithm interdependencies in
certification path service implementations:

-   Certification Path Validation and Signature Algorithms

    A `CertPathValidator`{.codeph} implementation often requires use of
    a signature algorithm to verify each certificate\'s digital
    signature. The <span class="apiname">setSigProvider</span> method of
    the `PKIXParameters`{.codeph} class allows a user to specify a
    specific `Signature`{.codeph} provider.

-   Certification Path Builders and Certificate Factories

    A `CertPathBuilder`{.codeph} implementation will often utilize a
    `CertificateFactory`{.codeph} to generate a certification path from
    a list of certificates.

-   CertStores and Certificate Factories

    A `CertStore`{.codeph} implementation will often utilize a
    `CertificateFactory`{.codeph} to generate certificates and CRLs from
    their encodings. For example, an LDAP `CertStore`{.codeph}
    implementation may use an X.509 `CertificateFactory`{.codeph} to
    generate X.509 certificates and CRLs from their ASN.1 encoded form.

</div>
</div>
<div class="sect4">
[]{#GUID-5C8A1966-6636-475F-B533-3D080DB0653A}

#### Certification Path Parameter Specification Interfaces {#JSSEC-GUID-5C8A1966-6636-475F-B533-3D080DB0653A .sect4}

<div>
The Certification Path API contains two interfaces representing
<span class="variable">transparent</span> specifications of parameters,
the `CertPathParameters`{.codeph} and `CertStoreParameters`{.codeph}
interfaces.

Two implementations of the `CertPathParameters`{.codeph} interface are
included, the `PKIXParameters`{.codeph} and
`PKIXBuilderParameters`{.codeph} classes. If you are working with PKIX
certification path validation and algorithm parameters, you can utilize
these classes. If you need parameters for a different algorithm, you
will need to supply your own `CertPathParameters`{.codeph}
implementation for that algorithm.

Two implementations of the `CertStoreParameters`{.codeph} interface are
included, the `LDAPCertStoreParameters`{.codeph} and the
`CollectionCertStoreParameters`{.codeph} classes. These classes are to
be used with LDAP and Collection `CertStore`{.codeph} implementations,
respectively. If you need parameters for a different repository type,
you will need to supply your own `CertStoreParameters`{.codeph}
implementation for that type.

The `CertPathParameters`{.codeph} and `CertStoreParameters`{.codeph}
interfaces each define a `clone`{.codeph} method that implementations
should override. A typical implementation will perform a \"deep\" copy
of the object, such that subsequent changes to the copy will not affect
the original (and vice versa). However, this is not an absolute
requirement for implementations of `CertStoreParameters`{.codeph}. A
shallow copy implementation of `clone`{.codeph} is more appropriate for
applications that need to hold a reference to a parameter contained in
the `CertStoreParameters`{.codeph}. For example, since
<span class="apiname">CertStore.getInstance</span> makes a clone of the
specified `CertStoreParameters`{.codeph}, a shallow copy
`clone`{.codeph} allows an application to hold a reference to and later
release the resources of a particular `CertStore`{.codeph}
initialization parameter, rather than waiting for the garbage collection
mechanism. This should be done with the utmost care, since the
`CertStore`{.codeph} may still be in use by other threads.

</div>
</div>
<div class="sect4">
[]{#GUID-67EDE244-431F-4382-9384-B5CBD8163C05}

#### Certification Path Result Specification Interfaces {#JSSEC-GUID-67EDE244-431F-4382-9384-B5CBD8163C05 .sect4}

<div>
The Certification Path API contains two interfaces representing
<span class="variable">transparent</span> specifications of results, the
`CertPathValidatorResult`{.codeph} and `CertPathBuilderResult`{.codeph}
interfaces.

One implementation for each of the interfaces is included: the
`PKIXCertPathValidatorResult`{.codeph} and
`PKIXCertPathBuilderResult`{.codeph} classes. If you are implementing
PKIX certification path service providers, you can utilize these
classes. If you need certification path results for a different
algorithm, you will need to supply your own
`CertPathValidatorResult`{.codeph} or `CertPathBuilderResult`{.codeph}
implementation for that algorithm.

A PKIX implementation of a `CertPathValidator`{.codeph} or a
`CertPathBuilder`{.codeph} may find it useful to store additional
information in the `PKIXCertPathValidatorResult`{.codeph} or
`PKIXCertPathBuilderResult`{.codeph}, such as debugging traces. In these
cases, the implementation should implement a subclass of the appropriate
result class with methods to retrieve the relevant information. These
classes must be shipped with the provider classes, for example, as part
of the provider JAR file.

</div>
</div>
<div class="sect4">
[]{#GUID-C6FC73C4-E9CA-45A2-A135-5E81FA345F5F}

#### Certification Path Exception Classes {#JSSEC-GUID-C6FC73C4-E9CA-45A2-A135-5E81FA345F5F .sect4}

<div>
The Certification Path API contains a set of exception classes for
handling errors.
`CertPathValidatorException, CertPathBuilderException`{.codeph}, and
`CertStoreException`{.codeph} are subclasses of
`GeneralSecurityException`{.codeph}.

You may need to extend these classes in your service provider
implementation.

For example, a `CertPathBuilder`{.codeph} implementation may provide
additional information such as debugging traces when a
`CertPathBuilderException`{.codeph} is thrown. The implementation may
throw a subclass of `CertPathBuilderException`{.codeph} that holds this
information. Likewise, a `CertStore`{.codeph} implementation can provide
additional information when a failure occurs by throwing a subclass of
`CertStoreException`{.codeph} . Also, you may want to implement a
subclass of `CertPathValidatorException`{.codeph} to describe a
particular failure mode of your `CertPathValidator`{.codeph}
implementation.

In each case, the new exception classes must be shipped with the
provider classes, for example, as part of the provider JAR file. Each
provider should document the exception subclasses.

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-EF1585DC-20BF-4140-B71E-0A8528D4A57D}

Appendix A: Standard Names {#JSSEC-GUID-EF1585DC-20BF-4140-B71E-0A8528D4A57D .sect2}
--------------------------

<div>
The Java Certification Path API requires and utilizes a set of standard
names for certification path validation algorithms, encodings and
certificate storage types.

<div class="section">
The standard names previously found here in Appendix A and in the other
security specifications (JCA/JSSE/etc.) have been combined in the [Java
Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).
Specific provider information can be found in the [JDK
Providers](oracle-providers.htm#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313 "This document contains the technical details of the providers that are included in the JDK. It is assumed that readers have a strong understanding of the Java Cryptography Architecture and Provider Architecture.").

Please note that a service provider may choose to define a new name for
a proprietary or non-standard algorithm that is not mentioned in the
Standard Names document. However, to prevent name collisions, it is
recommended that the name be prefixed with the reverse Internet domain
name of the provider\'s organization (for example:
`com.sun.MyCertPathValidator`{.codeph}).

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-EB250086-0AC1-4D60-AE2A-FC7461374746}

Appendix B: CertPath Implementation in SUN Provider {#JSSEC-GUID-EB250086-0AC1-4D60-AE2A-FC7461374746 .sect2}
---------------------------------------------------

<div>
<div class="section">
The \"SUN\" provider supports the following standard algorithms, types
and encodings:

-   `CertificateFactory`{.codeph}: <span class="bold">X.509</span>
    `CertPath`{.codeph} type with <span class="bold">PKCS7</span> and
    <span class="bold">PkiPath</span> encodings
-   `CertPathValidator`{.codeph}: <span class="bold">PKIX</span>
    algorithm
-   `CertPathBuilder`{.codeph}: <span class="bold">PKIX</span> algorithm
-   `CertStore`{.codeph}: <span class="bold">Collection </span>
    `CertStore`{.codeph} type

Each of these service provider interface implementations is discussed in
more detail below.

</div>
<!-- class="section" -->

<div class="section">
CertificateFactory

The \"SUN\" provider for the `CertificateFactory`{.codeph} engine class
supports generation of X.509 `CertPath`{.codeph} objects. The PKCS7 and
PkiPath encodings are supported. The PKCS\#7 implementation supports a
subset of [RFC 2315](http://www.ietf.org/rfc/rfc2315.txt) (only the
SignedData ContentInfo type is supported). The certificates in the
`CertPath`{.codeph} are ordered in the forward direction (from target to
trust anchor). Each certificate in the `CertPath`{.codeph} is of type
`java.security.cert.X509Certificate`{.codeph} , and versions 1, 2 and 3
are supported.

</div>
<!-- class="section" -->

<div class="section">
CertPathValidator

The \"SUN\" provider supplies a PKIX implementation of the
`CertPathValidator`{.codeph} engine class. The implementation validates
`CertPath`{.codeph}s of type X.509 and implements the certification path
validation algorithm defined in [RFC
5280:](http://www.ietf.org/rfc/rfc5280.txt) <cite>PKIX Certificate and
CRL Profile</cite>. This implementation sets the
`ValidationAlgorithm`{.codeph} service attribute to \"RFC5280\".

Weak cryptographic algorithms can be disabled in the \"SUN\" provider
using the `jdk.certpath.disabledAlgorithms`{.codeph} Security Property.
See [Appendix E: Disabling Cryptographic
Algorithms](java-pki-programmers-guide.htm#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3 "The jdk.certpath.disabledAlgorithms Security Property contains a list of cryptographic algorithms and key size constraints that are considered weak or broken. Certificates and other data (CRLs, OCSPResponses) containing any of these algorithms or key sizes will be blocked during certification path building and validation. This property is used by Oracle's PKIX implementation, other implementations might not examine and use it.")
for a description and examples of this property.

The PKIX Certificate and CRL Profile has many optional features. The
\"SUN\" provider implements support for the policy mapping, [authority
information
access](java-pki-programmers-guide.htm#GUID-EB250086-0AC1-4D60-AE2A-FC7461374746__SECTION-1310-623E8D62)
and [CRL distribution point
certificate](java-pki-programmers-guide.htm#GUID-EB250086-0AC1-4D60-AE2A-FC7461374746__SECTION-139-623E860E)
extensions, the issuing distribution point CRL extension, and the reason
code and certificate issuer CRL entry extensions. It does not implement
support for the freshest CRL or subject information access certificate
extensions. It also does not include support for the freshest CRL and
delta CRL Indicator CRL extensions and the invalidity date and hold
instruction code CRL entry extensions.

The implementation supports a CRL revocation checking mechanism that
conforms to section 6.3 of the PKIX Certificate and CRL Profile. OCSP
([RFC 2560](http://www.ietf.org/rfc/rfc2560.txt)) is also currently
supported as a built in revocation checking mechanism. See [Appendix C:
OCSP
Support](java-pki-programmers-guide.htm#GUID-E6E737DB-4000-4005-969E-BCD0238B1566 "Client-side support for the On-Line Certificate Status Protocol (OCSP) as defined in RFC 2560 is supported.")
for more details on the implementation and configuration and how it
works in conjunction with CRLs.

The implementation does not support the `nameConstraints`{.codeph}
parameter of the `TrustAnchor`{.codeph} class and the
`validate`{.codeph} method throws an
`InvalidAlgorithmParameterException`{.codeph} if it is specified.

</div>
<!-- class="section" -->

<div class="section">
CertPathBuilder

The \"SUN\" provider supplies a PKIX implementation of the
`CertPathBuilder`{.codeph} engine class. The implementation builds
`CertPath`{.codeph}s of type X.509. Each `CertPath`{.codeph} is
validated according to the PKIX algorithm defined in [RFC 5280:
<span class="variable">PKIX Certificate and CRL
Profile</span>](http://www.ietf.org/rfc/rfc5280.txt). This
implementation sets the `ValidationAlgorithm`{.codeph} service attribute
to \"RFC5280\".

The implementation requires that the `targetConstraints`{.codeph}
parameter of a `PKIXBuilderParameters`{.codeph} object is an instance of
`X509CertSelector`{.codeph} and the subject criterion is set to a
non-null value. Otherwise the `build`{.codeph} method throws an
`InvalidAlgorithmParameterException`{.codeph}.

The implementation builds `CertPath`{.codeph} objects in a forward
direction using a depth-first algorithm. It backtracks to previous
states and tries alternate paths when a potential path is determined to
be invalid or exceeds the `PKIXBuilderParameters`{.codeph}
`maxPathLength`{.codeph} parameter.

Validation of the path is performed in the same manner as the
`CertPathValidator`{.codeph} implementation. The implementation
validates most of the path as it is being built, in order to eliminate
invalid paths earlier in the process. Validation checks that cannot be
executed on certificates ordered in a forward direction are delayed and
executed on the path after it has been constructed (but before it is
returned to the application).

As with `CertPathValidator`{.codeph}, the
`jdk.certpath.disabledAlgorithms`{.codeph} Security Property can be used
to exclude cryptographic algorithms that are not considered safe.

When two or more potential certificates are discovered that may lead to
finding a path that meets the specified constraints, the implementation
uses the following criteria to prioritize the certificates (in the
examples below, assume a `TrustAnchor`{.codeph} distinguished name of
\"ou=D,ou=C,o=B,c=A\" is specified):

1.  The issuer DN of the certificate matches the DN of one of the
    specified `TrustAnchor`{.codeph}s (ex: issuerDN =
    \"ou=D,ou=C,o=B,c=A\").
2.  The issuer DN of the certificate is a descendant of the DN of one of
    the `TrustAnchor`{.codeph}s, ordered by proximity to the anchor (ex:
    issuerDN = \"ou=E,ou=D,ou=C,o=B,c=A\").
3.  The issuer DN of the certificate is an ancestor of the DN of one of
    the `TrustAnchor`{.codeph}s, ordered by proximity to the anchor (ex:
    issuerDN = \"ou=C,o=B,c=A\".
4.  The issuer DN of the certificate is in the same namespace of one of
    the `TrustAnchor`{.codeph}s, ordered by proximity to the anchor (ex:
    issuerDN = \"ou=G,ou=C,o=B,c=A\").
5.  The issuer DN of the certificate is an ancestor of the subject DN of
    the certificate, ordered by proximity to the subject.

These are followed by certificates which don\'t meet any of the above
criteria.

This implementation has been tested with the LDAP and Collection
`CertStore`{.codeph} implementations included in this release of the
\"SUN\" provider.

Debugging support can be enabled by setting the
`java.security.debug`{.codeph} property to `certpath`{.codeph}. For
example:

``` {.codeblock dir="ltr"}
       java -Djava.security.debug=certpath BuildCertPath
```

This will print additional debugging information to standard error.

</div>
<!-- class="section" -->

<div class="section">
Collection CertStore

The SUN provider supports the Collection implementation of the
`CertStore`{.codeph} engine class.

The Collection `CertStore`{.codeph} implementation can hold any objects
that are an instance of `java.security.cert.Certificate`{.codeph} or
`java.security.cert.CRL`{.codeph}.

The certificates and CRLs are not returned in any particular order and
will not contain duplicates.

</div>
<!-- class="section" -->

<div class="section" id="GUID-EB250086-0AC1-4D60-AE2A-FC7461374746__SECTION-139-623E860E">
Support for the CRL Distribution Points Extension

Support for the CRL Distribution Points extension is available. It is
disabled by default for compatibility and can be enabled by setting the
system property `com.sun.security.enableCRLDP`{.codeph} to the value
true.

If set to true, Sun\'s PKIX implementation uses the information in a
certificate\'s CRL Distribution Points extension (in addition to
`CertStores`{.codeph} that are specified) to find the CRL, provided the
distribution point is an X.500 distinguished name or a URI of type ldap,
http, or ftp.

<div class="infoboxnote" id="GUID-EB250086-0AC1-4D60-AE2A-FC7461374746__GUID-04FA26C1-BD2F-49EA-AB41-4CDACEB64B54">
Note:

Depending on your network and firewall setup, it may be necessary to
also configure your networking proxy servers.

</div>
</div>
<!-- class="section" -->

<div class="section" id="GUID-EB250086-0AC1-4D60-AE2A-FC7461374746__SECTION-1310-623E8D62">
Support for the Authority Information Access (AIA) Extension

Support for the `caIssuers`{.codeph} access method of the Authority
Information Access extension is available. It is disabled by default for
compatibility and can be enabled by setting the system property
`com.sun.security.enableAIAcaIssuers`{.codeph} to the value true.

If set to true, Sun\'s PKIX implementation of `CertPathBuilder`{.codeph}
uses the information in a certificate\'s AIA extension (in addition to
CertStores that are specified) to find the issuing CA certificate,
provided it is a URI of type ldap, http, or ftp.

<div class="infoboxnote" id="GUID-EB250086-0AC1-4D60-AE2A-FC7461374746__GUID-0073BEE2-F442-4AB2-96B8-353D0D92AE36">
Note:

Depending on your network and firewall setup, it may be necessary to
also configure your networking proxy servers.

</div>
</div>
<!-- class="section" -->

<div class="section">
Maximum Network Connection Timeout for CRL Retrievals

Set the maximum connection timeout for CRL retrievals, in seconds, with
the system property `com.sun.security.crl.timeout`{.codeph}. If the
property has not been set, or if its value is negative, it\'s set to the
default value of 15 seconds. A value of 0 means an infinite timeout.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-E6E737DB-4000-4005-969E-BCD0238B1566}

Appendix C: OCSP Support {#JSSEC-GUID-E6E737DB-4000-4005-969E-BCD0238B1566 .sect2}
------------------------

<div>
Client-side support for the On-Line Certificate Status Protocol (OCSP)
as defined in RFC 2560 is supported.

<div class="section">
OCSP checking is controlled by the following five Security Properties:

<div class="tblformal" id="GUID-E6E737DB-4000-4005-969E-BCD0238B1566__GUID-E342DEB0-ACE2-44DB-8E21-61EFDDA25D57">
+-----------------------------------+-----------------------------------+
| Property Name                     | Description                       |
+:==================================+:==================================+
| `ocsp.enable`{.codeph}            | This property\'s value is either  |
|                                   | true or false. If true, OCSP      |
|                                   | checking is enabled when doing    |
|                                   | certificate revocation checking;  |
|                                   | if false or not set, OCSP         |
|                                   | checking is disabled.             |
+-----------------------------------+-----------------------------------+
| `ocsp.responderURL`{.codeph}      | This property\'s value is a URL   |
|                                   | that identifies the location of   |
|                                   | the OCSP responder. Here is an    |
|                                   | example                           |
|                                   |                                   |
|                                   | ``` {.codeblock dir="ltr"}        |
|                                   | ocsp.responderURL=http://ocsp.exa |
|                                   | mple.net:80                       |
|                                   | ```                               |
|                                   |                                   |
|                                   | By default, the location of the   |
|                                   | OCSP responder is determined      |
|                                   | implicitly from the certificate   |
|                                   | being validated. The property is  |
|                                   | used when the Authority           |
|                                   | Information Access extension      |
|                                   | (defined in RFC 5280) is absent   |
|                                   | from the certificate or when it   |
|                                   | requires overriding.              |
+-----------------------------------+-----------------------------------+
| `ocsp.responderCertSubjectName`{. | This property\'s value is the     |
| codeph}                           | subject name of the OCSP          |
|                                   | responder\'s certificate. Here is |
|                                   | an example                        |
|                                   |                                   |
|                                   | ``` {.codeblock dir="ltr"}        |
|                                   | ocsp.responderCertSubjectName="CN |
|                                   | =OCSP Responder, O=XYZ Corp"      |
|                                   | ```                               |
|                                   |                                   |
|                                   | By default, the certificate of    |
|                                   | the OCSP responder is that of the |
|                                   | issuer of the certificate being   |
|                                   | validated. This property          |
|                                   | identifies the certificate of the |
|                                   | OCSP responder when the default   |
|                                   | does not apply. Its value is a    |
|                                   | string distinguished name         |
|                                   | (defined in RFC 2253) which       |
|                                   | identifies a certificate in the   |
|                                   | set of certificates supplied      |
|                                   | during cert path validation. In   |
|                                   | cases where the subject name      |
|                                   | alone is not sufficient to        |
|                                   | uniquely identify the             |
|                                   | certificate, then both the        |
|                                   | `ocsp.responderCertIssuerName`{.c |
|                                   | odeph}                            |
|                                   | and                               |
|                                   | `ocsp.responderCertSerialNumber`{ |
|                                   | .codeph}                          |
|                                   | properties must be used instead.  |
|                                   | When this property is set, then   |
|                                   | those two properties are ignored. |
+-----------------------------------+-----------------------------------+
| `ocsp.responderCertIssuerName`{.c | This property\'s value is the     |
| odeph}                            | issuer name of the OCSP           |
|                                   | responder\'s certificate . Here   |
|                                   | is an example                     |
|                                   |                                   |
|                                   | ``` {.codeblock dir="ltr"}        |
|                                   | ocsp.responderCertIssuerName="CN= |
|                                   | Enterprise CA, O=XYZ Corp"        |
|                                   | ```                               |
|                                   |                                   |
|                                   | By default, the certificate of    |
|                                   | the OCSP responder is that of the |
|                                   | issuer of the certificate being   |
|                                   | validated. This property          |
|                                   | identifies the certificate of the |
|                                   | OCSP responder when the default   |
|                                   | does not apply. Its value is a    |
|                                   | string distinguished name         |
|                                   | (defined in RFC 2253) which       |
|                                   | identifies a certificate in the   |
|                                   | set of certificates supplied      |
|                                   | during cert path validation. When |
|                                   | this property is set then the     |
|                                   | `ocsp.responderCertSerialNumber`{ |
|                                   | .codeph}                          |
|                                   | property must also be set. Note   |
|                                   | that this property is ignored     |
|                                   | when the                          |
|                                   | `ocsp.responderCertSubjectName`{. |
|                                   | codeph}                           |
|                                   | property has been set.            |
+-----------------------------------+-----------------------------------+
| `ocsp.responderCertSerialNumber`{ | This property\'s value is the     |
| .codeph}                          | serial number of the OCSP         |
|                                   | responder\'s certificate Here is  |
|                                   | an example                        |
|                                   |                                   |
|                                   | ``` {.codeblock dir="ltr"}        |
|                                   | ocsp.responderCertSerialNumber=2A |
|                                   | :FF:00                            |
|                                   | ```                               |
|                                   |                                   |
|                                   | By default, the certificate of    |
|                                   | the OCSP responder is that of the |
|                                   | issuer of the certificate being   |
|                                   | validated. This property          |
|                                   | identifies the certificate of the |
|                                   | OCSP responder when the default   |
|                                   | does not apply. Its value is a    |
|                                   | string of hexadecimal digits      |
|                                   | (colon or space separators may be |
|                                   | present) which identifies a       |
|                                   | certificate in the set of         |
|                                   | certificates supplied during cert |
|                                   | path validation. When this        |
|                                   | property is set then the          |
|                                   | `ocsp.responderCertIssuerName`{.c |
|                                   | odeph}                            |
|                                   | property must also be set. Note   |
|                                   | that this property is ignored     |
|                                   | when the                          |
|                                   | `ocsp.responderCertSubjectName`{. |
|                                   | codeph}                           |
|                                   | property has been set.            |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

These properties may be set either statically in the Java runtime\'s
`<java_home>/conf/security/java.security` file, or dynamically using the
<span class="apiname">java.security.Security.setProperty()</span>
method.

By default, OCSP checking is not enabled. It is enabled by setting the
`ocsp.enable`{.codeph} property to `"true"`{.codeph}. Use of the
remaining properties is optional. Note that enabling OCSP checking only
has an effect if revocation checking has also been enabled. Revocation
checking is enabled via the
<span class="apiname">PKIXParameters.setRevocationEnabled()</span>
method.

OCSP checking works in conjunction with Certificate Revocation Lists
(CRLs) during revocation checking. Below is a summary of the interaction
of OCSP and CRLs. Failover to CRLs occurs only if an OCSP problem is
encountered. Failover does not occur if the OCSP responder confirms
either that the certificate has been revoked or that it has not been
revoked.

<div class="tblformal" id="GUID-E6E737DB-4000-4005-969E-BCD0238B1566__GUID-923086ED-0588-4942-882E-B5A4E1809341">
  PKIXParameters RevocationEnabled (default=true)   `ocsp.enable`{.codeph} (default=false)   Behavior
  ------------------------------------------------- ---------------------------------------- --------------------------------------------------------
  true                                              true                                     Revocation checking using OCSP, failover to using CRLs
  true                                              false                                    Revocation checking using CRLs only
  false                                             true                                     No revocation checking
  false                                             false                                    No revocation checking

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Maximum Allowable Clock Skew

You might encounter connection failures during revocation checking
because the network is slow or the system clock is off by some amount.
Set the maximum allowable clock skew (the time difference between
response time and local time), in seconds, used for revocation checks
with the system property `com.sun.security.ocsp.clockskew`{.codeph}. If
the property has not been set, or if its value is negative, it\'s set to
the default value of 900 seconds (15 minutes).

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-FF62B0E3-E57A-4F40-970A-0481AF750CCD}

Appendix D: CertPath Implementation in JdkLDAP Provider {#JSSEC-GUID-FF62B0E3-E57A-4F40-970A-0481AF750CCD .sect2}
-------------------------------------------------------

<div>
The JdkLDAP provider supports the LDAP implementation of the
`CertStore`{.codeph} engine class.

<div class="section">
LDAP CertStore

The LDAP `CertStore`{.codeph} implementation retrieves certificates and
CRLs from an LDAP directory using the LDAP schema defined in [RFC
2587](http://www.ietf.org/rfc/rfc2587.txt).

The LDAPSchema service attribute is set to \"RFC2587\".

The implementation fetches certificates from different locations,
depending on the values of the subject, issuer, and basicConstraints
selection criteria specified in the `X509CertSelector`{.codeph}. It
performs as many of the following operations as possible:

1.  Subject non-null, basicConstraints \<= -1

    Looks for certificates in the subject DN\'s \"userCertificate\"
    attribute.

2.  Subject non-null, basicConstraints \>= -1

    Looks for certificates in the forward element of the subject DN\'s
    \"crossCertificatePair\" attribute AND in the subject\'s
    \"caCertificate\" attribute.

3.  Issuer non-null, basicConstraints \>= -1

    Looks for certificates in the reverse element of the issuer DN\'s
    \"crossCertificatePair\" attribute AND in the issuer DN\'s
    \"caCertificate\" attribute.

In each case, certificates are checked using
<span class="apiname">X509CertSelector.match()</span> before adding them
to the resulting collection.

If none of the conditions specified above applies, then an exception is
thrown to indicate that it was impossible to fetch certificates using
the criteria supplied. Note that even if one or more of the conditions
apply, the Collection returned may still be empty if there are no
certificates in the directory.

The implementation fetches CRLs from the issuer DNs specified in the
<span class="apiname">setCertificateChecking</span>,
<span class="apiname">addIssuerName</span> or
<span class="apiname">setIssuerNames</span> methods of the
`X509CRLSelector`{.codeph} class. If no issuer DNs have been specified
using one of these methods, the implementation throws an exception
indicating it was impossible to fetch CRLs using the criteria supplied.
Otherwise, the CRLs are searched as follows:

1.  The implementation first creates a list of issuer names. If a
    certificate was specified in the
    <span class="apiname">setCertificateChecking</span> method, it uses
    the issuer of that certificate. Otherwise, it uses the issuer names
    specified using the <span class="apiname">addIssuerName</span> or
    <span class="apiname">setIssuerNames</span> methods.

2.  Next, the implementation iterates through the list of issuer names.
    For each issuer name, it searches first in the issuer\'s
    `"authorityRevocationList"`{.codeph} attribute and then, if no
    matching CRL was found there, in the issuer\'s
    `"certificateRevocationList"`{.codeph} attribute. One exception to
    the above is that if the issuer name was obtained from the
    certificate specified in the
    <span class="apiname">setCertificateChecking</span> method, it only
    checks the issuer\'s `"authorityRevocationList"`{.codeph} attribute
    if the specified certificate is a CA certificate.

3.  All CRLs are checked using
    <span class="apiname">X509CRLSelector.match()</span> before adding
    them to the resulting collection.

4.  If no CRLs satisfying the selection criteria can be found, an empty
    Collection is returned.

</div>
<!-- class="section" -->

<div class="section">
Caching

By default each LDAP CertStore instance caches lookups for a maximum of
30 seconds. The cache lifetime can be changed by setting the system
property `sun.security.certpath.ldap.cache.lifetime`{.codeph} to a value
in seconds. A value of `0`{.codeph} disables the cache completely. A
value of `-1`{.codeph} means unlimited lifetime.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3}

Appendix E: Disabling Cryptographic Algorithms {#JSSEC-GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3 .sect2}
----------------------------------------------

<div>
The `jdk.certpath.disabledAlgorithms`{.codeph} Security Property
contains a list of cryptographic algorithms and key size constraints
that are considered weak or broken. Certificates and other data (CRLs,
OCSPResponses) containing any of these algorithms or key sizes will be
blocked during certification path building and validation. This property
is used by Oracle\'s PKIX implementation, other implementations might
not examine and use it.

<div class="section" id="GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3__THEEXACTSYNTAXOFTHEJDK.CERTPATH.DIS-E836920C">
<div class="p">
The exact syntax of the `jdk.certpath.disabledAlgorithms`{.codeph}
property is described in the `java.security` file. In Java SE 9, the
default value of the property is:

``` {.oac_no_warn dir="ltr"}
jdk.certpath.disabledAlgorithms=MD2, MD5, SHA1 jdkCA & usage TLSServer, \
    RSA keySize < 1024, DSA keySize < 1024, EC keySize < 224
```

</div>
<div class="p">
In this syntax:

[<!-- -->]{#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3__GUID-B0501142-4173-4B89-BCAB-258A16642B90}MD2

:   Any MD2-based algorithm will be blocked.

    For example, a certificate, CRL, or OCSPResponse signed with an
    MD2withRSA signature algorithm.

[<!-- -->]{#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3__GUID-B88364D6-A8F1-4647-89E9-254574E7A6CF}MD5

:   Any MD5-based algorithm will be blocked.

    For example, a certificate, CRL, or OCSPResponse signed with an
    MD5withRSA signature algorithm.

[<!-- -->]{#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3__GUID-BBF5D821-1F96-4B27-8790-1C16DE97E2A0}SHA1 jdkCA & usage TLSServer
:   All SHA1 certificates that chain to trust anchors pre-installed in
    the cacerts keystore and that are used for authentication of TLS
    Servers. See [JEP 288](http://openjdk.java.net/jeps/288).

[<!-- -->]{#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3__GUID-0277D5D2-7B44-497A-8326-E03E7308FEF8}RSA keySize \< 1024

:   Any RSA key less than 1024 bits will be blocked.

    For example, a certificate with a 768-bit RSA public key.

[<!-- -->]{#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3__GUID-D46E89B2-3499-4AA3-9722-B052D8DCA85E}DSA keySize \< 1024

:   Any DSA key less than 1024 bits will be blocked.

    For example, a certificate with a 512-bit DSA public key.

[<!-- -->]{#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3__GUID-D354B4DE-FA31-45F3-97D4-0B50CE4E7122}EC keySize \< 224

:   Any EC key less than 224 bits will be blocked.

    For example, a certificate with a 160-bit EC public key.

</div>
Administrators or users can modify the value of the
`jdk.certpath.disabledAlgorithms`{.codeph} property to address
additional security requirements. However, removing any of the current
algorithms or key sizes is not recommended.

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
| ----------------- -- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| ---- --              | L |             <span cl |
|                  [![ | o | ass="icon">Contents< |
| Previous](../../dcom | g | /span>](toc.htm)     |
| mon/gifs/leftnav.gif | o |   -- --------------- |
| )\                   | ] | -------------------- |
|                      | ( | -------------------- |
| [![Next](../../dcomm | . | ---                  |
| on/gifs/rightnav.gif | . |                      |
| )\                   | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](t | / |                      |
| roubleshooting-jsse- | d |                      |
| sample-code.htm)   < | c |                      |
| span class="icon">Ne | o |                      |
| xt</span>](java-sasl | m |                      |
| -api-programming-and | m |                      |
| -deployment-guide1.h | o |                      |
| tm)                  | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| ----------------- -- | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| ---- --              | a |                      |
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
