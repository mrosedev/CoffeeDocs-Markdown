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

  ------------------------------------------------------------------- --------------------------------------------------------- --
             [![Previous](../../dcommon/gifs/leftnav.gif)\                   [![Next](../../dcommon/gifs/rightnav.gif)\         
   <span class="icon">Previous</span>](troubleshooting-security.htm)   <span class="icon">Next</span>](howtoimplaprovider.htm)  
  ------------------------------------------------------------------- --------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190}<!-- End Header -->

<span class="enumeration_chapter">2 </span>Java Cryptography Architecture (JCA) Reference Guide {#JSSEC-GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 .sect1}
===============================================================================================

<div>
The Java Cryptography Architecture (JCA) is a major piece of the
platform, and contains a \"provider\" architecture and a set of APIs for
digital signatures, message digests (hashes), certificates and
certificate validation, encryption (symmetric/asymmetric block/stream
ciphers), key generation and management, and secure random number
generation, to name a few.

</div>
<div class="sect2">
[]{#GUID-815542FE-CF3D-407A-9673-CAE9840F6231}

Introduction to Java Cryptography Architecture {#JSSEC-GUID-815542FE-CF3D-407A-9673-CAE9840F6231 .sect2}
----------------------------------------------

<div>
The Java platform strongly emphasizes security, including language
safety, cryptography, public key infrastructure, authentication, secure
communication, and access control.

The JCA is a major piece of the platform, and contains a \"provider\"
architecture and a set of APIs for digital signatures, message digests
(hashes), certificates and certificate validation, encryption
(symmetric/asymmetric block/stream ciphers), key generation and
management, and secure random number generation, to name a few. These
APIs allow developers to easily integrate security into their
application code. The architecture was designed around the following
principles:

-   <span class="bold">Implementation independence</span>: Applications
    do not need to implement security algorithms. Rather, they can
    request security services from the Java platform. Security services
    are implemented in providers (see [Cryptographic Service
    Providers](java-cryptography-architecture-jca-reference-guide.html#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920)),
    which are plugged into the Java platform via a standard interface.
    An application may rely on multiple independent providers for
    security functionality.

-   <span class="bold">Implementation interoperability</span>: Providers
    are interoperable across applications. Specifically, an application
    is not bound to a specific provider, and a provider is not bound to
    a specific application.

-   <span class="bold">Algorithm extensibility</span>: The Java platform
    includes a number of built-in providers that implement a basic set
    of security services that are widely used today. However, some
    applications may rely on emerging standards not yet implemented, or
    on proprietary services. The Java platform supports the installation
    of custom providers that implement such services.

Other cryptographic communication libraries available in the JDK use the
JCA provider architecture, but are described elsewhere. The JSSE
components provides access to Secure Socket Layer (SSL), Transport Layer
Security (TLS), and Datagram Transport Layer Security (DTLS)
implementations; see [Java Secure Socket Extension (JSSE) Reference
Guide](java-secure-socket-extension-jsse-reference-guide.html#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345 "The Java Secure Socket Extension (JSSE) enables secure Internet communications. It provides a framework and an implementation for a Java version of the SSL, TLS, and DTLS protocols and includes functionality for data encryption, server authentication, message integrity, and optional client authentication.").
You can use Java Generic Security Services (JGSS) (via Kerberos) APIs,
and Simple Authentication and Security Layer (SASL) to securely exchange
messages between communicating applications; see [Introduction to JAAS
and Java GSS-API
Tutorials](introduction-jaas-and-java-gss-api-tutorials1.htm) and [Java
SASL API Programming and Deployment
Guide](java-sasl-api-programming-and-deployment-guide1.html#GUID-6D78EE33-62E6-4D85-9695-322EED493F72).

<div class="section">
Notes on Terminology

-   Prior to JDK 1.4, the JCE was an unbundled product, and as such, the
    JCA and JCE were regularly referred to as separate, distinct
    components. As JCE is now bundled in the JDK, the distinction is
    becoming less apparent. Since the JCE uses the same architecture as
    the JCA, the JCE should be more properly thought of as a part of the
    JCA.

-   The JCA within the JDK includes two software components:

    -   The framework that defines and supports cryptographic services
        for which providers supply implementations. This framework
        includes packages such as `java.security`{.codeph},
        `javax.crypto`{.codeph}, `javax.crypto.spec`{.codeph}, and
        `javax.crypto.interfaces`{.codeph}.
    -   The actual providers such as `Sun`{.codeph},
        `SunRsaSign`{.codeph}, `SunJCE`{.codeph}, which contain the
        actual cryptographic implementations.

    Whenever a specific JCA provider is mentioned, it will be referred
    to explicitly by the provider\'s name.

<div class="infoboxnotewarn" id="GUID-815542FE-CF3D-407A-9673-CAE9840F6231__GUID-4604E723-D0C5-432A-B831-F3D6B61C1614">
WARNING:

The JCA makes it easy to incorporate security features into your
application. However, this document does not cover the theory of
security/cryptography beyond an elementary introduction to concepts
necessary to discuss the APIs. This document also does not cover the
strengths/weaknesses of specific algorithms, not does it cover protocol
design. Cryptography is an advanced topic and one should consult a
solid, preferably recent, reference in order to make best use of these
tools.

You should always understand what you are doing and why: DO NOT simply
copy random code and expect it to fully solve your usage scenario. Many
applications have been deployed that contain significant security or
performance problems because the wrong tool or algorithm was selected.

</div>
</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-71693272-7F57-4155-99F9-A2139271FD6D}

### JCA Design Principles {#JSSEC-GUID-71693272-7F57-4155-99F9-A2139271FD6D .sect3}

<div>
The JCA was designed around these principles:

-   Implementation independence and interoperability
-   Algorithm independence and extensibility

Implementation independence and algorithm independence are
complementary; you can use cryptographic services, such as digital
signatures and message digests, without worrying about the
implementation details or even the algorithms that form the basis for
these concepts. While complete algorithm-independence is not possible,
the JCA provides standardized, algorithm-specific APIs. When
implementation-independence is not desirable, the JCA lets developers
indicate a specific implementation.

Algorithm independence is achieved by defining types of cryptographic
\"engines\" (services), and defining classes that provide the
functionality of these cryptographic engines. These classes are called
<span class="variable">engine classes</span>, and examples are the
[<span class="apiname">MessageDigest</span>](https://docs.oracle.com/javase/10/docs/api/java/security/MessageDigest.html),
[<span class="apiname">Signature</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Signature.html),
[<span class="apiname">KeyFactory</span>](https://docs.oracle.com/javase/10/docs/api/java/security/KeyFactory.html),
[<span class="apiname">KeyPairGenerator</span>](https://docs.oracle.com/javase/10/docs/api/java/security/KeyPairGenerator.html),
and
[<span class="apiname">Cipher</span>](https://docs.oracle.com/javase/10/docs/api/javax/crypto/Cipher.html)
classes.

Implementation independence is achieved using a \"provider\"-based
architecture. The term Cryptographic Service Provider (CSP), which is
used interchangeably with the term \"provider,\" (see [Cryptographic
Service
Providers](java-cryptography-architecture-jca-reference-guide.html#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920))
refers to a package or set of packages that implement one or more
cryptographic services, such as digital signature algorithms, message
digest algorithms, and key conversion services. A program may simply
request a particular type of object (such as a `Signature`{.codeph}
object) implementing a particular service (such as the DSA signature
algorithm) and get an implementation from one of the installed
providers. If desired, a program may instead request an implementation
from a specific provider. Providers may be updated transparently to the
application, for example when faster or more secure versions are
available.

Implementation interoperability means that various implementations can
work with each other, use each other\'s keys, or verify each other\'s
signatures. This would mean, for example, that for the same algorithms,
a key generated by one provider would be usable by another, and a
signature generated by one provider would be verifiable by another.

Algorithm extensibility means that new algorithms that fit in one of the
supported engine classes can be added easily.

</div>
</div>
<div class="sect3">
[]{#GUID-EAB9FF73-4C69-4FD5-8A0C-5CF48211A859}

### Provider Architecture {#JSSEC-GUID-EAB9FF73-4C69-4FD5-8A0C-5CF48211A859 .sect3}

<div>
Providers contain a package (or a set of packages) that supply concrete
implementations for the advertised cryptographic algorithms.

</div>
<div class="sect4">
[]{#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920}

#### Cryptographic Service Providers {#JSSEC-GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920 .sect4}

<div>
`java.security.Provider`{.codeph} is the base class for all security
providers. Each CSP contains an instance of this class which contains
the provider\'s name and lists all of the security services/algorithms
it implements. When an instance of a particular algorithm is needed, the
JCA framework consults the provider\'s database, and if a suitable match
is found, the instance is created.

Providers contain a package (or a set of packages) that supply concrete
implementations for the advertised cryptographic algorithms. Each JDK
installation has one or more providers installed and configured by
default. Additional providers may be added statically or dynamically.
Clients may configure their runtime environment to specify the provider
<span class="variable">preference order</span>. The preference order is
the order in which providers are searched for requested services when no
specific provider is requested.

To use the JCA, an application simply requests a particular type of
object (such as a `MessageDigest`{.codeph}) and a particular algorithm
or service (such as the \"SHA-256\" algorithm), and gets an
implementation from one of the installed providers. For example, the
following statement requests a SHA-256 message digest from an installed
provider:

``` {.codeblock dir="ltr"}
    md = MessageDigest.getInstance("SHA-256");
```

Alternatively, the program can request the objects from a specific
provider. Each provider has a name used to refer to it. For example, the
following statement requests a SHA-256 message digest from the provider
named ProviderC:

``` {.codeblock dir="ltr"}
    md = MessageDigest.getInstance("SHA-256", "ProviderC");
```

The following figures illustrates requesting an SHA-256 message digest
implementation. They show three different providers that implement
various message digest algorithms (SHA-256, SHA-384, and SHA-512). The
providers are ordered by preference from left to right (1-3). In [Figure
2-1](java-cryptography-architecture-jca-reference-guide.html#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920__REQUESTSHA-256MESSAGEDIGESTIMPLEMEN-0606134F),
an application requests a SHA-256 algorithm implementation
<span class="bold">without</span> specifying a provider name. The
providers are searched in preference order and the implementation from
the first provider supplying that particular algorithm, ProviderB, is
returned. In [Figure
2-2](java-cryptography-architecture-jca-reference-guide.html#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920__REQUESTSHA-256MESSAGEDIGESTWITHPROV-CB5635FE),
the application requests the SHA-256 algorithm implementation
<span class="bold">from a specific provider</span>, ProviderC. This
time, the implementation from ProviderC is returned, even though a
provider with a higher preference order, ProviderB, also supplies an MD5
implementation.

<div class="figure" id="GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920__REQUESTSHA-256MESSAGEDIGESTIMPLEMEN-0606134F">
Figure 2-1 Request SHA-256 Message Digest Implementation Without
Specifying Provider

\
![Description of Figure 2-1
follows](img/security-overview-message-digest-wo-provider.png "Description of Figure 2-1 follows")\
[Description of \"Figure 2-1 Request SHA-256 Message Digest
Implementation Without Specifying
Provider\"](img_text/security-overview-message-digest-wo-provider.htm)\

</div>
<!-- class="figure" -->

<div class="figure" id="GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920__REQUESTSHA-256MESSAGEDIGESTWITHPROV-CB5635FE">
Figure 2-2 Request SHA-256 Message Digest with ProviderC

\
![Description of Figure 2-2
follows](img/security-overview-message-digest-providerc.png "Description of Figure 2-2 follows")\
[Description of \"Figure 2-2 Request SHA-256 Message Digest with
ProviderC\"](img_text/security-overview-message-digest-providerc.htm)\

</div>
<!-- class="figure" -->

Cryptographic implementations in the JDK are distributed via several
different providers (`Sun`{.codeph}, `SunJSSE`{.codeph},
`SunJCE`{.codeph}, `SunRsaSign`{.codeph}) primarily for historical
reasons, but to a lesser extent by the type of functionality and
algorithms they provide. Other Java runtime environments may not
necessarily contain these providers, so applications should not request
a provider-specific implementation unless it is known that a particular
provider will be available.

The JCA offers a set of APIs that allow users to query which providers
are installed and what services they support.

This architecture also makes it easy for end-users to add additional
providers. Many third party provider implementations are already
available. See [The Provider
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-D8E30FE5-66B4-4F6A-88B7-280789E68307 "In order to be used, a cryptographic provider must first be installed, then registered either statically or dynamically. There are a variety of Sun providers shipped with this release (SUN, SunJCE, SunJSSE, SunRsaSign, etc.) that are already installed and registered. The following sections describe how to install and register additional providers.Each Provider class instance has a (currently case-sensitive) name, a version number, and a string description of the provider and its services.")
for more information on how providers are written, installed, and
registered.

</div>
</div>
<div class="sect4">
[]{#GUID-FD5163BD-E113-4B9D-A230-11184A668616}

#### How Providers Are Actually Implemented {#JSSEC-GUID-FD5163BD-E113-4B9D-A230-11184A668616 .sect4}

<div>
<span class="variable">Algorithm independence</span> is achieved by
defining a generic high-level Application Programming Interface (API)
that all applications use to access a service type.
<span class="variable">Implementation independence</span> is achieved by
having all provider implementations conform to well-defined interfaces.
Instances of engine classes are thus \"backed\" by implementation
classes which have the same method signatures. Application calls are
routed through the engine class and are delivered to the underlying
backing implementation. The implementation handles the request and
return the proper results.

<div class="section">
The application API methods in each engine class are routed to the
provider\'s implementations through classes that implement the
corresponding Service Provider Interface (SPI). That is, for each engine
class, there is a corresponding abstract SPI class which defines the
methods that each cryptographic service provider\'s algorithm must
implement. The name of each SPI class is the same as that of the
corresponding engine class, followed by `Spi`{.codeph}. For example, the
`Signature`{.codeph} engine class provides access to the functionality
of a digital signature algorithm. The actual provider implementation is
supplied in a subclass of `SignatureSpi`{.codeph}. Applications call the
engine class\' API methods, which in turn call the SPI methods in the
actual implementation.

Each SPI class is abstract. To supply the implementation of a particular
type of service for a specific algorithm, a provider must subclass the
corresponding SPI class and provide implementations for all the abstract
methods.

For each engine class in the API, implementation instances are requested
and instantiated by calling the
<span class="apiname">getInstance()</span>
<span class="variable">factory method</span> in the engine class. A
factory method is a static method that returns an instance of a class.
The engine classes use the framework provider selection mechanism
described above to obtain the actual backing implementation (SPI), and
then creates the actual engine object. Each instance of the engine class
encapsulates (as a private field) the instance of the corresponding SPI
class, known as the SPI object. All API methods of an API object are
declared final and their implementations invoke the corresponding SPI
methods of the encapsulated SPI object.

To make this clearer, review [Example
2-1](java-cryptography-architecture-jca-reference-guide.html#GUID-FD5163BD-E113-4B9D-A230-11184A668616__SAMPLECODEFORGETTINGANINSTANCEOFANE-724746B9)
and [Figure
2-3](java-cryptography-architecture-jca-reference-guide.html#GUID-FD5163BD-E113-4B9D-A230-11184A668616__GUID-F8F97C84-B042-4576-B56D-1FD217F20400):

</div>
<!-- class="section" -->

<div class="example" id="GUID-FD5163BD-E113-4B9D-A230-11184A668616__SAMPLECODEFORGETTINGANINSTANCEOFANE-724746B9">
Example 2-1 Sample Code for Getting an Instance of an Engine Class

``` {.codeblock dir="ltr"}
    import javax.crypto.*;

    Cipher c = Cipher.getInstance("AES");
    c.init(ENCRYPT_MODE, key);
```

</div>
<!-- class="example" -->

<div class="section">
<div class="figure" id="GUID-FD5163BD-E113-4B9D-A230-11184A668616__GUID-F8F97C84-B042-4576-B56D-1FD217F20400">
Figure 2-3 Application Retrieves "AES" Cipher Instance

![Description of Figure 2-3
follows](img/aes-cipher.gif "Description of Figure 2-3 follows")\
[Description of \"Figure 2-3 Application Retrieves "AES" Cipher
Instance\"](img_text/aes-cipher.htm)

</div>
<!-- class="figure" -->

Here an application wants an \"AES\" `javax.crypto.Cipher`{.codeph}
instance, and doesn\'t care which provider is used. The application
calls the `getInstance()`{.codeph} factory methods of the
`Cipher`{.codeph} engine class, which in turn asks the JCA framework to
find the first provider instance that supports \"AES\". The framework
consults each installed provider, and obtains the provider\'s instance
of the `Provider`{.codeph} class. (Recall that the `Provider`{.codeph}
class is a database of available algorithms.) The framework searches
each provider, finally finding a suitable entry in CSP3. This database
entry points to the implementation class `com.foo.AESCipher`{.codeph}
which extends `CipherSpi`{.codeph}, and is thus suitable for use by the
`Cipher`{.codeph} engine class. An instance of
`com.foo.AESCipher`{.codeph} is created, and is encapsulated in a
newly-created instance of `javax.crypto.Cipher`{.codeph}, which is
returned to the application. When the application now does the
<span class="apiname">init()</span> operation on the `Cipher`{.codeph}
instance, the `Cipher`{.codeph} engine class routes the request into the
corresponding <span class="apiname">engineInit()</span> backing method
in the `com.foo.AESCipher`{.codeph} class.

[Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
lists the Standard Names defined for the Java environment. Other
third-party providers may define their own implementations of these
services, or even additional services.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-C730728A-DB4B-488F-8171-34FC04BD0FF1}

#### Keystores {#JSSEC-GUID-C730728A-DB4B-488F-8171-34FC04BD0FF1 .sect4}

<div>
A database called a \"keystore\" can be used to manage a repository of
keys and certificates. Keystores are available to applications that need
data for authentication, encryption, or signing purposes.

Applications can access a keystore via an implementation of the
`KeyStore`{.codeph} class, which is in the `java.security`{.codeph}
package. As of JDK 9, the default and recommended keystore type (format)
is \"pkcs12\", which is based on the RSA PKCS12 Personal Information
Exchange Syntax Standard. Previously, the default keystore type was
\"jks\", which is a proprietary format. Other keystore formats are
available, such as \"jceks\", which is an alternate proprietary keystore
format, and \"pkcs11\", which is based on the RSA PKCS11 Standard and
supports access to cryptographic tokens such as hardware security
modules and smartcards.

Applications can choose different keystore implementations from
different providers, using the same provider mechanism described
previously. See [Key
Management](java-cryptography-architecture-jca-reference-guide.html#GUID-AB51DEFD-5238-4F96-967F-082F6D34FBEA "A database called a "keystore" can be used to manage a repository of keys and certificates. (A certificate is a digitally signed statement from one entity, saying that the public key of some other entity has a particular value.)").

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212}

### Engine Classes and Algorithms {#JSSEC-GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 .sect3}

<div>
An engine class provides the interface to a specific type of
cryptographic service, independent of a particular cryptographic
algorithm or provider.

The engines provides one of the following:

-   cryptographic operations (encryption, digital signatures, message
    digests, etc.),
-   generators or converters of cryptographic material (keys and
    algorithm parameters), or
-   objects (keystores or certificates) that encapsulate the
    cryptographic data and can be used at higher layers of abstraction.

The following engine classes are available:

-   [`SecureRandom`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-AEB77CD8-D28F-4BBE-B9E5-160B5DC35D36):
    used to generate random or pseudo-random numbers.
-   [`MessageDigest`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-FB0090CA-2BCC-4D2C-BD2F-6F0A97197BD7 "Procedure to create a MessageDigest object.Procedure to update the Message Digest object.Procedure to compute the digest using different types of digest() methods."):
    used to calculate the message digest (hash) of specified data.
-   [`Signature`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-9CF09CE2-9443-4F4E-8095-5CBFC7B697CF "Signature objects are modal objects. This means that a Signature object is always in a given state, where it may only do one type of operation. The first step for signing or verifying a signature is to create a Signature instance.A Signature object must be initialized before it is used. The initialization method depends on whether the object is going to be used for signing or for verification."):
    initialized with keys, these are used to sign data and verify
    digital signatures.
-   [`Cipher`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566):
    initialized with keys, these used for encrypting/decrypting data.
    There are various types of algorithms: symmetric bulk encryption
    (e.g. AES), asymmetric encryption (e.g. RSA), and password-based
    encryption (e.g. PBE).
-   [Message Authentication Codes
    (MAC)](java-cryptography-architecture-jca-reference-guide.html#GUID-8E014689-EBBB-4DE1-B6E0-24CE59AD8B9A "Similar to a MessageDigest, a Message Authentication Code (MAC) provides a way to check the integrity of information transmitted over or stored in an unreliable medium, but includes a secret key in the calculation."):
    like `MessageDigest`{.codeph}s, these also generate hash values, but
    are first initialized with keys to protect the integrity of
    messages.
-   [`KeyFactory`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-09C8DF67-7C78-453C-95B4-E7E7DEAD446A):
    used to convert existing opaque cryptographic keys of type
    [`Key`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC "The java.security.Key interface is the top-level interface for all opaque keys. It defines the functionality shared by all opaque key objects.")
    into key specifications (transparent representations of the
    underlying key material), and vice versa.
-   [`SecretKeyFactory`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-5E8F4099-779F-4484-9A95-F1CEA167601A):
    used to convert existing opaque cryptographic keys of type
    [`SecretKey`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC "The java.security.Key interface is the top-level interface for all opaque keys. It defines the functionality shared by all opaque key objects.")
    into key specifications (transparent representations of the
    underlying key material), and vice versa.
    `SecretKeyFactory`{.codeph}s are specialized `KeyFactory`{.codeph}s
    that create secret (symmetric) keys only.
-   [`KeyPairGenerator`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-7EA29AC2-28B5-405D-BD2F-7055EC9E1EDD):
    used to generate a new pair of public and private keys suitable for
    use with a specified algorithm.
-   [`KeyGenerator`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-F178CBC3-D25F-48B6-9F2F-ABB586E713A1 "A key generator is used to generate secret keys for symmetric algorithms."):
    used to generate new secret keys for use with a specified algorithm.
-   [`KeyAgreement`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-C4D8A5D0-ECA7-4686-A8F0-636115500C31 "Key agreement is a protocol by which 2 or more parties can establish the same cryptographic keys, without having to exchange any secret information."):
    used by two or more parties to agree upon and establish a specific
    key to use for a particular cryptographic operation.
-   [`AlgorithmParameters`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-33407B4E-D819-4294-94AB-C6FABF96A93D "Like Keys and Keyspecs, an algorithm's initialization parameters are represented by either AlgorithmParameters or AlgorithmParameterSpecs."):
    used to store the parameters for a particular algorithm, including
    parameter encoding and decoding.
-   [`AlgorithmParameterGenerator`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-921D1B8C-5A16-403E-B3A6-D9C6EC684D1C)
    : used to generate a set of AlgorithmParameters suitable for a
    specified algorithm.
-   [`KeyStore`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-09050137-31F1-468A-A552-B051A4E35876 "The KeyStore class supplies well-defined interfaces to access and modify the information in a keystore."):
    used to create and manage a <span class="variable">keystore</span>.
    A keystore is a database of keys. Private keys in a keystore have a
    certificate chain associated with them, which authenticates the
    corresponding public key. A keystore also contains certificates from
    trusted entities.
-   [`CertificateFactory`{.codeph}](java-cryptography-architecture-jca-reference-guide.html#GUID-9A581FBA-EDF7-4BCA-8244-4CE2C75E4CEA "The CertificateFactory class defines the functionality of a certificate factory, which is used to generate certificate and certificate revocation list (CRL) objects from their encoding."):
    used to create public key certificates and Certificate Revocation
    Lists (CRLs).
-   [`CertPathBuilder`{.codeph}](java-pki-programmers-guide.html#GUID-BEFCC824-21C1-4AD3-B670-D0CA01F08D95 "The CertPathBuilder class is an engine class used to build a certification path."):
    used to build certificate chains (also known as certification
    paths).
-   [`CertPathValidator`{.codeph}](java-pki-programmers-guide.html#GUID-808C1A6D-6A67-4026-A9DE-223A428EC80A "The CertPathValidator class is an engine class used to validate a certification path."):
    used to validate certificate chains.
-   [`CertStore`{.codeph}](java-pki-programmers-guide.html#GUID-5404B79C-3D49-4668-974C-1BACD1A98B73 "The CertStore class is an engine class used to provide the functionality of a certificate and certificate revocation list (CRL) repository."):
    used to retrieve `Certificate`{.codeph}s and `CRL`{.codeph}s from a
    repository.

<div class="infoboxnote" id="GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212__GUID-4ADAF14D-B1E3-451D-9708-F21608DCC42A">
Note:

A <span class="variable">generator</span> creates objects with brand-new
contents, whereas a <span class="variable">factory</span> creates
objects from existing material (for example, an encoding).

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-5C9A28FC-8B6B-45BA-8A71-6BEEA34EC27F}

Core Classes and Interfaces {#JSSEC-GUID-5C9A28FC-8B6B-45BA-8A71-6BEEA34EC27F .sect2}
---------------------------

<div>
The following are the core classes and interfaces provided in the JCA.

-   `Provider`{.codeph} and `Security`{.codeph}
-   `SecureRandom`{.codeph}, `MessageDigest`{.codeph},
    `Signature`{.codeph}, `Cipher`{.codeph}, `Mac`{.codeph},
    `KeyFactory`{.codeph}, `SecretKeyFactory`{.codeph},
    `KeyPairGenerator`{.codeph}, `KeyGenerator`{.codeph},
    `KeyAgreement`{.codeph}, `AlgorithmParameter`{.codeph},
    `AlgorithmParameterGenerator`{.codeph}, `KeyStore`{.codeph},
    `CertificateFactory`{.codeph}, and engine
-   `Key Interface`{.codeph}, `KeyPair`{.codeph}
-   `AlgorithmParameterSpec Interface`{.codeph},
    `AlgorithmParameters`{.codeph},
    `AlgorithmParameterGenerator`{.codeph}, and algorithm parameter
    specification interfaces and classes in the
    `java.security.spec`{.codeph} and `javax.crypto.spec`{.codeph}
    packages.
-   `KeySpec Interface`{.codeph}, `EncodedKeySpec`{.codeph},
    `PKCS8EncodedKeySpec`{.codeph}, and `X509EncodedKeySpec`{.codeph}.
-   `SecretKeyFactory`{.codeph}, `KeyFactory`{.codeph},
    `KeyPairGenerator`{.codeph}, `KeyGenerator`{.codeph},
    `KeyAgreement`{.codeph}, and `KeyStore`{.codeph}.

<div class="infoboxnote" id="GUID-5C9A28FC-8B6B-45BA-8A71-6BEEA34EC27F__GUID-81034E79-9AB1-4E97-8EEA-5129FDBB3183">
Note:

See `CertPathBuilder`{.codeph}, `CertPathValidator`{.codeph}, and
`CertStore`{.codeph}engine classes in the [Java PKI Programmers
Guide](java-pki-programmers-guide.html#GUID-650D0D53-B617-4055-AFD3-AF5C2629CBBF "The Java Certification Path API consists of classes and interfaces for handling certification paths, which are also called certification chains. If a certification path meets certain validation rules, it may be used to securely establish the mapping of a public key to a subject.").

</div>
The guide will cover the most useful high-level classes first (Provider,
Security, SecureRandom, MessageDigest, Signature, Cipher, and Mac), then
delve into the various support classes. For now, it is sufficient to
simply say that Keys (public, private, and secret) are generated and
represented by the various JCA classes, and are used by the high-level
classes as part of their operation.

This section shows the signatures of the main methods in each class and
interface. Examples for some of these classes (MessageDigest, Signature,
KeyPairGenerator, SecureRandom, KeyFactory, and key specification
classes) are supplied in the corresponding [Code
Examples](java-cryptography-architecture-jca-reference-guide.html#GUID-871FA938-5110-409E-A4EC-16F2A898093A)
sections.

The complete reference documentation for the relevant Security API
packages can be found in the package summaries:

-   [`java.security`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/package-summary.html)
-   [`javax.crypto`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/package-summary.html)
-   [`java.security.cert`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/cert/package-summary.html)
-   [`java.security.spec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/package-summary.html)
-   [`javax.crypto.spec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/package-summary.html)
-   [`java.security.interfaces`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/package-summary.html)
-   [`javax.crypto.interfaces`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/package-summary.html)

</div>
<div class="sect3">
[]{#GUID-D8E30FE5-66B4-4F6A-88B7-280789E68307}

### The Provider Class {#JSSEC-GUID-D8E30FE5-66B4-4F6A-88B7-280789E68307 .sect3}

<div>
The term \"Cryptographic Service Provider\" (used interchangeably with
\"provider\" in this document) refers to a package or set of packages
that supply a concrete implementation of a subset of the JDK Security
API cryptography features. The `Provider`{.codeph}
<span class="italic">class</span> is the interface to such a package or
set of packages. It has methods for accessing the provider name, version
number, and other information. Please note that in addition to
registering implementations of cryptographic services, the
`Provider`{.codeph} class can also be used to register implementations
of other security services that might get defined as part of the JDK
Security API or one of its extensions.

To supply implementations of cryptographic services, an entity (e.g., a
development group) writes the implementation code and creates a subclass
of the `Provider`{.codeph} class. The constructor of the
`Provider`{.codeph} subclass sets the values of various properties; the
JDK Security API uses these values to look up the services that the
provider implements. In other words, the subclass specifies the names of
the classes implementing the services.

<div class="figure" id="GUID-D8E30FE5-66B4-4F6A-88B7-280789E68307__GUID-DA3FDF88-BB48-44FA-A992-70FB7CA08DBF">
Figure 2-4 Provider Class

![Description of Figure 2-4
follows](img/provider.png "Description of Figure 2-4 follows")\
[Description of \"Figure 2-4 Provider Class\"](img_text/provider.htm)

</div>
<!-- class="figure" -->

There are several types of services that can be implemented by provider
packages; See [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.").

The different implementations may have different characteristics. Some
may be software-based, while others may be hardware-based. Some may be
platform-independent, while others may be platform-specific. Some
provider source code may be available for review and evaluation, while
some may not. The JCA lets both end-users and developers decide what
their needs are.

You can find information about how end-users install the cryptography
implementations that fit their needs, and how developers request the
implementations that fit theirs.

<div class="p">
<div class="infoboxnote" id="GUID-D8E30FE5-66B4-4F6A-88B7-280789E68307__GUID-8FA29B58-275F-40EE-B871-31BAF7A54250">
Note:

To implement a provider, see [Steps to Implement and Integrate a
Provider](howtoimplaprovider.html#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:").

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741}

#### How Provider Implementations Are Requested and Supplied {#JSSEC-GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741 .sect4}

<div>
<div class="section">
For each engine class (see [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider."))
in the API, a implementation instance is requested and instantiated by
calling one of the <span class="apiname">getInstance</span> methods on
the engine class, specifying the name of the desired algorithm and,
optionally, the name of the provider (or the `Provider`{.codeph} class)
whose implementation is desired.

``` {.codeblock dir="ltr"}
static EngineClassName getInstance(String algorithm)
    throws NoSuchAlgorithmException

static EngineClassName getInstance(String algorithm, String provider)
    throws NoSuchAlgorithmException, NoSuchProviderException

static EngineClassName getInstance(String algorithm, Provider provider)
    throws NoSuchAlgorithmException
```

where

<span class="italic">EngineClassName</span>

is the desired engine type (MessageDigest/Cipher/etc). For example:

``` {.codeblock dir="ltr"}
    MessageDigest md = MessageDigest.getInstance("SHA-256");
    KeyAgreement ka = KeyAgreement.getInstance("DH", "SunJCE");
```

return an instance of the \"SHA-256\" MessageDigest and \"DH\"
KeyAgreement objects, respectively.

[Java Security Standard Algorithm
Names](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
contains the list of names that have been standardized for use with the
Java environment. Some providers may choose to also include alias names
that also refer to the same algorithm. For example, the \"SHA256\"
algorithm might be referred to as \"SHA-256\". Applications should use
standard names instead of an alias, as not all providers may alias
algorithm names in the same way.

<div class="p">
<div class="infoboxnote" id="GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741__GUID-123854F3-B43E-4650-8BB4-BF14004B3468">
Note:

The algorithm name is not case-sensitive. For example, all the following
calls are equivalent:

``` {.codeblock dir="ltr"}
MessageDigest.getInstance("SHA256")
MessageDigest.getInstance("sha256")
MessageDigest.getInstance("sHa256")
```

</div>
</div>
If no provider is specified, `getInstance`{.codeph} searches the
registered providers for an implementation of the requested
cryptographic service associated with the named algorithm. In any given
Java Virtual Machine (JVM), providers are installed in a given
<span class="variable">preference order</span>, the order in which the
provider list is searched if a specific provider is not requested. (See
[Installing
Providers](java-cryptography-architecture-jca-reference-guide.html#GUID-E28AC9F2-CBD7-49FC-85B8-5011A94D9007 "In order to be used, a cryptographic provider must first be installed, then registered either statically or dynamically. There are a variety of Sun providers shipped with this release (SUN, SunJCE, SunJSSE, SunRsaSign, etc.) that are already installed and registered. The following sections describe how to install and register additional providers.").)
For example, suppose there are two providers installed in a JVM,
`PROVIDER_1`{.codeph} and `PROVIDER_2`{.codeph}. Assume that:

-   `PROVIDER_1`{.codeph} implements SHA-256 and DESede.
    `PROVIDER_1`{.codeph} has preference order 1 (the highest priority).
-   `PROVIDER_2`{.codeph} implements SHA256withDSA, SHA-256, RC5, and
    RSA. `PROVIDER_2`{.codeph} has preference order 2.

Now let\'s look at three scenarios:

1.  If we are looking for an SHA-256 implementation. Both providers
    supply such an implementation. The `PROVIDER_1`{.codeph}
    implementation is returned since `PROVIDER_1`{.codeph} has the
    highest priority and is searched first.
2.  If we are looking for an SHA256withDSA signature algorithm,
    `PROVIDER_1`{.codeph} is first searched for it. No implementation is
    found, so `PROVIDER_2`{.codeph} is searched. Since an implementation
    is found, it is returned.
3.  Suppose we are looking for a SHA256withRSA signature algorithm.
    Since no installed provider implements it, a
    `NoSuchAlgorithmException`{.codeph} is thrown.

The <span class="apiname">getInstance</span> methods that include a
provider argument are for developers who want to specify which provider
they want an algorithm from. A federal agency, for example, will want to
use a provider implementation that has received federal certification.
Let\'s assume that the SHA256withDSA implementation from
`PROVIDER_1`{.codeph} has not received such certification, while the DSA
implementation of `PROVIDER_2`{.codeph} has received it.

A federal agency program would then have the following call, specifying
`PROVIDER_2`{.codeph} since it has the certified implementation:

``` {.codeblock dir="ltr"}
Signature dsa = Signature.getInstance("SHA256withDSA", "PROVIDER_2");
```

In this case, if `PROVIDER_2`{.codeph} was not installed, a
`NoSuchProviderException`{.codeph} would be thrown, even if another
installed provider implements the algorithm requested.

A program also has the option of getting a list of all the installed
providers (using the <span class="apiname">getProviders</span> method in
[The Security
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-DE597505-1B42-4AE3-AE2D-45F9123138FA)
class) and choosing one from the list.

<div class="p">
<div class="infoboxnote" id="GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741__GUID-8A66CE47-C14C-4CBC-BA2E-E5BAAFBF9477">
Note:

General purpose applications <span class="bold">SHOULD NOT</span>
request cryptographic services from specific providers. Otherwise,
applications are tied to specific providers which may not be available
on other Java implementations. They also might not be able to take
advantage of available optimized providers (for example hardware
accelerators via PKCS11 or native OS implementations such as
Microsoft\'s MSCAPI) that have a higher preference order than the
specific requested provider.

</div>
</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-E28AC9F2-CBD7-49FC-85B8-5011A94D9007}

#### Installing Providers {#JSSEC-GUID-E28AC9F2-CBD7-49FC-85B8-5011A94D9007 .sect4}

<div>
In order to be used, a cryptographic provider must first be installed,
then registered either statically or dynamically. There are a variety of
Sun providers shipped with this release (`SUN`{.codeph},
`SunJCE`{.codeph}, `SunJSSE`{.codeph}, `SunRsaSign`{.codeph}, etc.) that
are already installed and registered. The following sections describe
how to install and register additional providers.

All JDK providers are already installed and registered. However, if you
require any third-party providers, see [Step 8: Prepare for
Testing](howtoimplaprovider.html#GUID-FB9C6DB2-DE9A-4EFE-89B4-C2C168C5982D "The next steps describe how to install and configure your new provider so that it is available via the JCA.")
from [Steps to Implement and Integrate a
Provider](howtoimplaprovider.html#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:")
for information about how to add providers to the class or module path,
register providers (statically or dynamically), and add any required
permissions.

</div>
</div>
<div class="sect4">
[]{#GUID-F8089178-4CDC-4947-A118-7D02ED3EDFD8}

#### Provider Class Methods {#JSSEC-GUID-F8089178-4CDC-4947-A118-7D02ED3EDFD8 .sect4}

<div>
Each `Provider`{.codeph} class instance has a (currently case-sensitive)
name, a version number, and a string description of the provider and its
services.

<div class="section">
You can query the `Provider`{.codeph} instance for this information by
calling the following methods:

``` {.codeblock dir="ltr"}
public String getName()
public double getVersion()
public String getInfo()
```

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-DE597505-1B42-4AE3-AE2D-45F9123138FA}

### The Security Class {#JSSEC-GUID-DE597505-1B42-4AE3-AE2D-45F9123138FA .sect3}

<div>
The <span class="apiname">Security</span> class manages installed
providers and security-wide properties. It only contains static methods
and is never instantiated. The methods for adding or removing providers,
and for setting `Security`{.codeph} properties, can only be executed by
a trusted program. Currently, a \"trusted program\" is either

-   A local application not running under a security manager, or
-   An applet or application with permission to execute the specified
    method (see below).

The determination that code is considered trusted to perform an
attempted action (such as adding a provider) requires that the applet is
granted the proper permission(s) for that particular action. The policy
configuration file(s) for a JDK installation specify what permissions
(which types of system resource accesses) are allowed by code from
specified code sources. (See below and the [Default Policy
Implementation and Policy File
Syntax](permissions-jdk1.html#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D)
and [Java Security Architecture
Specification](https://docs.oracle.com/javase/8/docs/technotes/guides/security/spec/security-spec.doc.html)
files.)

Code being executed is always considered to come from a particular
\"code source\". The code source includes not only the location (URL)
where the code originated from, but also a reference to any public
key(s) corresponding to the private key(s) that may have been used to
sign the code. Public keys in a code source are referenced by (symbolic)
alias names from the user\'s .

In a policy configuration file, a code source is represented by two
components: a code base (URL), and an alias name (preceded by
`signedBy`{.codeph}), where the alias name identifies the keystore entry
containing the public key that must be used to verify the code\'s
signature.

Each \"grant\" statement in such a file grants a specified code source a
set of permissions, specifying which actions are allowed.

Here is a sample policy configuration file:

``` {.codeblock dir="ltr"}
grant codeBase "file:/home/sysadmin/", signedBy "sysadmin" {
    permission java.security.SecurityPermission "insertProvider";
    permission java.security.SecurityPermission "removeProvider";
    permission java.security.SecurityPermission "putProviderProperty.*";
};
```

This configuration file specifies that code loaded from a signed JAR
file in the `/home/sysadmin/`{.codeph} directory on the local file
system can add or remove providers or set provider properties. (Note
that the signature of the JAR file can be verified using the public key
referenced by the alias name `sysadmin`{.codeph} in the user\'s
keystore.).

Either component of the code source (or both) may be missing. Here\'s an
example of a configuration file where the `codeBase`{.codeph} is
omitted:

``` {.codeblock dir="ltr"}
grant signedBy "sysadmin" {
    permission java.security.SecurityPermission "insertProvider.*";
    permission java.security.SecurityPermission "removeProvider.*";
};
```

If this policy is in effect, code that comes in a JAR File signed by
`/home/sysadmin/`{.codeph} directory on the local filesystem can add or
remove providers. The code does not need to be signed.

An example where neither `codeBase`{.codeph} nor `signedBy`{.codeph} is
included is:

``` {.codeblock dir="ltr"}
grant {
    permission java.security.SecurityPermission "insertProvider.*";
    permission java.security.SecurityPermission "removeProvider.*";
};
```

Here, with both code source components missing, any code (regardless of
where it originates, or whether or not it is signed, or who signed it)
can add/remove providers. Obviously, this is definitely not recommended,
as this grant could open a security hole. Untrusted code could install a
Provider, thus affecting later code that is depending on a properly
functioning implementation. (For example, a rogue `Cipher`{.codeph}
object might capture and store the sensitive information it receives.)

</div>
<div class="sect4">
[]{#GUID-F6337AB7-D5A0-4AEC-B026-20E885D41E90}

#### Managing Providers {#JSSEC-GUID-F6337AB7-D5A0-4AEC-B026-20E885D41E90 .sect4}

<div>
The following tables summarize the methods in the `Security`{.codeph}
class you can use to query which `Provider`{.codeph}s are installed, as
well as to install or remove providers at runtime.

<div class="section">
Querying Providers

<div class="tblformal" id="GUID-F6337AB7-D5A0-4AEC-B026-20E885D41E90__GUID-2846E40D-F447-42D0-99BE-7A7C18C69B62">
  Method                                                         Description
  -------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `static Provider[] getProviders()`{.codeph}                    Returns an array containing all the installed providers (technically, the `Provider`{.codeph} subclass for each package provider). The order of the `Provider`{.codeph}s in the array is their preference order.
  `static Provider getProvider (String providerName)`{.codeph}   Returns the `Provider`{.codeph} named `providerName`{.codeph}. It returns `null`{.codeph} if the `Provider`{.codeph} is not found.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Adding Providers

<div class="tblformal" id="GUID-F6337AB7-D5A0-4AEC-B026-20E885D41E90__GUID-A7326F94-A51D-47F9-A638-D44E80710671">
  Method                                                                     Description
  -------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `static int addProvider(Provider provider)`{.codeph}                       Adds a `Provider`{.codeph} to the end of the list of installed `Provider`{.codeph}s. It returns the preference position in which the `Provider`{.codeph} was added, or `-1`{.codeph} if the `Provider`{.codeph} was not added because it was already installed.
  `static int insertProviderAt (Provider provider, int position)`{.codeph}   Adds a new `Provider`{.codeph} at a specified position. If the given provider is installed at the requested position, the provider formerly at that position and all providers with a position greater than `position`{.codeph} are shifted up one position (towards the end of the list). This method returns the preference position in which the `Provider`{.codeph} was added, or `-1`{.codeph} if the `Provider`{.codeph} was not added because it was already installed.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Removing Providers

<div class="tblformal" id="GUID-F6337AB7-D5A0-4AEC-B026-20E885D41E90__GUID-B2A12498-B82E-48A3-8E2C-D2DE65AA3B61">
  Method                                               Description
  ---------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `static void removeProvider(String name)`{.codeph}   Removes the `Provider`{.codeph} with the specified name. It returns silently if the provider is not installed. When the specified provider is removed, all providers located at a position greater than where the specified provider was are shifted down one position (towards the head of the list of installed providers).

</div>
<!-- class="inftblhruleinformal" -->

<div class="infoboxnote" id="GUID-F6337AB7-D5A0-4AEC-B026-20E885D41E90__GUID-D4EE4FE3-379E-451D-BDAE-FAC97B332CC4">
Note:

If you want to change the preference position of a provider, you must
first remove it, and then insert it back in at the new preference
position.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-BC5C75FC-DCF7-4E57-874C-42F7EDA8FF1E}

#### Security Properties {#JSSEC-GUID-BC5C75FC-DCF7-4E57-874C-42F7EDA8FF1E .sect4}

<div>
The `Security`{.codeph} class maintains a list of system-wide Security
Properties. These properties are similar to the `System`{.codeph}
properties, but are security-related. These properties can be set
statically (through the `<java-home>/conf/security/java.security` file)
or dynamically (using an API). See [Step 8.1: Configure the
Provider](howtoimplaprovider.html#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 "Register your provider so that the JCE framework can find your provider, either with the ServiceLoader class or in the class path or module path.")
from [Steps to Implement and Integrate a
Provider](howtoimplaprovider.html#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:").
for an example of registering a provider statically with the
`security.provider.n`{.codeph} Security Property. If you want to set
properties dynamically, trusted programs can use the following methods:

``` {.codeblock dir="ltr"}
static String getProperty(String key)
static void setProperty(String key, String datum)
```

<div class="infoboxnote" id="GUID-BC5C75FC-DCF7-4E57-874C-42F7EDA8FF1E__GUID-35369CF0-AB08-463E-ACFC-DB1568B85F22">
Note:

The list of security providers is established during VM startup;
therefore, the methods described above must be used to alter the
provider list.

</div>
</div>
</div>
</div>
<div class="sect3">
[]{#GUID-AEB77CD8-D28F-4BBE-B9E5-160B5DC35D36}

### The SecureRandom Class {#JSSEC-GUID-AEB77CD8-D28F-4BBE-B9E5-160B5DC35D36 .sect3}

<div>
The SecureRandom class is an engine class (see [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider."))
that provides cryptographically strong random numbers, either by
accessing a pseudo-random number generator (PRNG), a deterministic
algorithm that produces a pseudo-random sequence from an initial seed
value, or by reading a native source of randomness (for example,
`/dev/random` or a true random number generator). One example of a PRNG
is the Deterministic Random Bits Generator (DRBG) as specified in [NIST
SP
800-90Ar1](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-90Ar1.pdf).
Other implementations may produce true random numbers, and yet others
may use a combination of both techniques. A cryptographically strong
random number minimally complies with the statistical random number
generator tests specified in [FIPS 140-2, Security Requirements for
Cryptographic
Modules](http://csrc.nist.gov/publications/fips/fips140-2/fips1402.pdf),
section 4.9.1.

All Java SE implementations must indicate the strongest (most random)
implementation of SecureRandom that they provide in the
`securerandom.strongAlgorithms`{.codeph} property of the
`java.security.Security`{.codeph} class. This implementation can be used
when a particularly strong random value is required.

The `securerandom.drbg.config`{.codeph} property is used to specify the
DRBG `SecureRandom`{.codeph} configuration and implementations in the
SUN provider. The `securerandom.drbg.config`{.codeph} is a property of
the `java.security.Security`{.codeph} class. Other DRBG implementations
can also use the `securerandom.drbg.config`{.codeph} property.

<div class="figure" id="GUID-AEB77CD8-D28F-4BBE-B9E5-160B5DC35D36__GUID-BC14EED8-64AD-4750-9417-6E35322A2C07">
Figure 2-5 SecureRandom class

![Description of Figure 2-5
follows](img/secure-random.png "Description of Figure 2-5 follows")\
[Description of \"Figure 2-5 SecureRandom
class\"](img_text/secure-random.htm)

</div>
<!-- class="figure" -->

</div>
<div class="sect4">
[]{#GUID-5E53C490-C1B5-4862-A32F-EAD6ADC0AE35}

#### Creating a SecureRandom Object {#JSSEC-GUID-5E53C490-C1B5-4862-A32F-EAD6ADC0AE35 .sect4}

<div>
There are several ways to obtain an instance of `SecureRandom`{.codeph}:

-   All Java SE implementations provide a default
    `SecureRandom`{.codeph} using the no-argument constructor:
    `new SecureRandom()`{.codeph}. This constructor traverses the list
    of registered security providers, starting with the most preferred
    provider, then returns a new
    <span class="apiname">SecureRandom</span> object from the first
    provider that supports a `SecureRandom`{.codeph} random number
    generator (RNG) algorithm. If none of the providers support a RNG
    algorithm, then it returns a
    <span class="apiname">SecureRandom</span> object that uses SHA1PRNG
    from the SUN provider.

-   To get a specific implementation of `SecureRandom`{.codeph}, use one
    of the [How Provider Implementations Are Requested and
    Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

-   Use the `getInstanceStrong()`{.codeph} method to obtain a strong
    `SecureRandom`{.codeph} implementation as defined by the
    `securerandom.strongAlgorithms`{.codeph} property of the
    `java.security.Security`{.codeph} class. This property lists
    platform implementations that are suitable for generating important
    values.

</div>
</div>
<div class="sect4">
[]{#GUID-4E42B9E7-FF0B-4FD6-B67A-44F28F943BA8}

#### Seeding or Re-Seeding the SecureRandom Object {#JSSEC-GUID-4E42B9E7-FF0B-4FD6-B67A-44F28F943BA8 .sect4}

<div>
The <span class="apiname">SecureRandom</span> object is initialized with
a random seed unless the call to
<span class="apiname">getInstance()</span> is followed by a call to one
of the following <span class="apiname">setSeed</span> methods.

``` {.codeblock dir="ltr"}
    void setSeed(byte[] seed)
    void setSeed(long seed)
```

You must call <span class="apiname">setSeed</span> before the first
<span class="apiname">nextBytes</span> call to prevent any environmental
randomness.

The randomness of the bits produced by the
<span class="apiname">SecureRandom</span> object depends on the
randomness of the seed bits

At any time a `SecureRandom`{.codeph} object may be re-seeded using one
of the `setSeed`{.codeph} or `reseed`{.codeph} methods. The given seed
for `setSeed`{.codeph} supplements, rather than replaces, the existing
seed; therefore, repeated calls are guaranteed never to reduce
randomness.

</div>
</div>
<div class="sect4">
[]{#GUID-2FCAEC55-8FB5-4FCD-9826-38ABA0AF26DD}

#### Using a SecureRandom Object {#JSSEC-GUID-2FCAEC55-8FB5-4FCD-9826-38ABA0AF26DD .sect4}

<div>
To get random bytes, a caller simply passes an array of any length,
which is then filled with random bytes:

``` {.codeblock dir="ltr"}
    void nextBytes(byte[] bytes)
```

</div>
</div>
<div class="sect4">
[]{#GUID-B85818A1-2AAD-449C-BFB9-EC9146C1B340}

#### Generating Seed Bytes {#JSSEC-GUID-B85818A1-2AAD-449C-BFB9-EC9146C1B340 .sect4}

<div>
If desired, it is possible to invoke the
<span class="apiname">generateSeed</span> method to generate a given
number of seed bytes (to seed other random number generators, for
example):

``` {.codeblock dir="ltr"}
byte[] generateSeed(int numBytes)
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-FB0090CA-2BCC-4D2C-BD2F-6F0A97197BD7}

### The MessageDigest Class {#JSSEC-GUID-FB0090CA-2BCC-4D2C-BD2F-6F0A97197BD7 .sect3}

<div>
The `MessageDigest`{.codeph} class is an engine class (see [Engine
Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider."))
designed to provide the functionality of cryptographically secure
message digests such as SHA-256 or SHA-512. A cryptographically secure
message digest takes arbitrary-sized input (a byte array), and generates
a fixed-size output, called a <span class="variable">digest</span> or
hash.

<div class="figure" id="GUID-FB0090CA-2BCC-4D2C-BD2F-6F0A97197BD7__GUID-55B0CED3-CB64-479F-9599-A95FD2B243FC">
Figure 2-6 MessageDigest Class

![Description of Figure 2-6
follows](img/message-digest.png "Description of Figure 2-6 follows")\
[Description of \"Figure 2-6 MessageDigest
Class\"](img_text/message-digest.htm)

</div>
<!-- class="figure" -->

For example, the SHA-256 algorithm produces a 32-byte digest, and
SHA-512\'s is 64 bytes.

A digest has two properties:

-   It should be computationally infeasible to find two messages that
    hash to the same value.
-   The digest should not reveal anything about the input that was used
    to generate it.

Message digests are used to produce unique and reliable identifiers of
data. They are sometimes called \"checksums\" or the \"digital
fingerprints\" of the data. Changes to just one bit of the message
should produce a different digest value.

Message digests have many uses and can determine when data has been
modified, intentionally or not. Recently, there has been considerable
effort to determine if there are any weaknesses in popular algorithms,
with mixed results. When selecting a digest algorithm, one should always
consult a recent reference to determine its status and appropriateness
for the task at hand.

</div>
<div class="sect4">
[]{#GUID-2F162F9E-8A5F-4586-8E3A-CEF37ECD5E2A}

#### Creating a MessageDigest Object {#JSSEC-GUID-2F162F9E-8A5F-4586-8E3A-CEF37ECD5E2A .sect4}

<div>
Procedure to create a `MessageDigest`{.codeph} object.

-   <span>To compute a digest, create a message digest instance. The
    `MessageDigest`{.codeph} objects are obtained by using one of the
    <span class="apiname">getInstance()</span> methods in the
    `MessageDigest`{.codeph} class. See [How Provider Implementations
    Are Requested and
    Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).</span>
    <div>
    The factory method returns an initialized message digest object. It
    thus does not need further initialization.
    </div>

</div>
</div>
<div class="sect4">
[]{#GUID-72106C04-D90A-4CB8-B320-1F4F864221DC}

#### Updating a Message Digest Object {#JSSEC-GUID-72106C04-D90A-4CB8-B320-1F4F864221DC .sect4}

<div>
Procedure to update the Message Digest object.

-   <span>To calculate the digest of some data, you have to supply the
    data to the initialized message digest object. It can be provided
    all at once, or in chunks. Pieces can be fed to the message digest
    by calling one of the `update`{.codeph} methods:</span>

    <div>
    ``` {.codeblock dir="ltr"}
    void update(byte input)
    void update(byte[] input)
    void update(byte[] input, int offset, int len)
    ```

    </div>

</div>
</div>
<div class="sect4">
[]{#GUID-616B5D4B-F334-46B4-9969-6CB4ADF29789}

#### Computing the Digest {#JSSEC-GUID-616B5D4B-F334-46B4-9969-6CB4ADF29789 .sect4}

<div>
Procedure to compute the digest using different types of
<span class="apiname">digest()</span> methods.

<div class="p">
The data chunks have to be supplied by calls to `update`{.codeph}
method. See [Updating a Message Digest
Object](java-cryptography-architecture-jca-reference-guide.html#GUID-72106C04-D90A-4CB8-B320-1F4F864221DC "Procedure to update the Message Digest object.").

</div>
<!-- class="section" -->

-   <span>The digest is computed using a call to one of the
    `digest`{.codeph} methods:</span>

    <div>
    ``` {.codeblock dir="ltr"}
    byte[] digest()
    byte[] digest(byte[] input)
    int digest(byte[] buf, int offset, int len)
    ```

    </div>
    1.  <span>The `byte[] digest()`{.codeph} method return the computed
        digest.</span>
    2.  <span>The `byte[] digest(byte[] input)`{.codeph} method does a
        final `update(input)`{.codeph} with the input byte array before
        calling `digest()`{.codeph}, which returns the digest byte
        array.</span>
    3.  <span>The `int digest(byte[] buf, int offset, int len)`{.codeph}
        method stores the computed digest in the provided buffer
        `buf`{.codeph}, starting at `offset`{.codeph}. `len`{.codeph} is
        the number of bytes in `buf`{.codeph} allotted for the digest,
        the method returns the number of bytes actually stored in
        `buf`{.codeph}. If there is not enough room in the buffer, the
        method will throw an exception.</span>

    <div>
    See [Computing a MessageDigest
    Object](java-cryptography-architecture-jca-reference-guide.html#GUID-6E9FB890-F011-450E-9EC5-EBB358E1D8A1 "An example describing the procedure to compute a MessageDigest object.").

    </div>

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-9CF09CE2-9443-4F4E-8095-5CBFC7B697CF}

### The Signature Class {#JSSEC-GUID-9CF09CE2-9443-4F4E-8095-5CBFC7B697CF .sect3}

<div>
The `Signature`{.codeph} class is an engine class (see [Engine Classes
and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.")(
designed to provide the functionality of a cryptographic digital
signature algorithm such as SHA256withDSA or SHA512withRSA. A
cryptographically secure signature algorithm takes arbitrary-sized input
and a private key and generates a relatively short (often fixed-size)
string of bytes, called the <span class="variable">signature</span>,
with the following properties:

-   Only the owner of a private/public key pair is able to create a
    signature. It should be computationally infeasible for anyone having
    only the public key and a number of signatures to recover the
    private key.
-   Given the public key corresponding to the private key used to
    generate the signature, it should be possible to verify the
    authenticity and integrity of the input.

<div class="figure" id="GUID-9CF09CE2-9443-4F4E-8095-5CBFC7B697CF__GUID-9CD447B5-97F4-4E45-B883-77C9EAFCB7B6">
Figure 2-7 Signature Class

![Description of Figure 2-7
follows](img/signature.png "Description of Figure 2-7 follows")\
[Description of \"Figure 2-7 Signature Class\"](img_text/signature.htm)

</div>
<!-- class="figure" -->

A <span class="apiname">Signature</span> object is initialized for
signing with a Private Key and is given the data to be signed. The
resulting signature bytes are typically kept with the signed data. When
verification is needed, another <span class="apiname">Signature</span>
object is created and initialized for verification and given the
corresponding Public Key. The data and the signature bytes are fed to
the signature object, and if the data and signature match, the
<span class="apiname">Signature</span> object reports success.

Even though a signature seems similar to a message digest, they have
very different purposes in the type of protection they provide. In fact,
algorithms such as \"SHA256WithRSA\" use the message digest \"SHA256\"
to initially \"compress\" the large data sets into a more manageable
form, then sign the resulting 32 byte message digest with the \"RSA\"
algorithm.

For an example for signing and verifying data, see [Generating and
Verifying a Signature Using Generated
Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-7389E94B-A595-4020-A4D2-73FB0DD5A05A "Examples of generating and verifying a signature using generated keys.").

</div>
<div class="sect4">
[]{#GUID-3586E054-8F23-4D2B-BEA4-47635DAB4EEE}

#### Signature Object States {#JSSEC-GUID-3586E054-8F23-4D2B-BEA4-47635DAB4EEE .sect4}

<div>
`Signature`{.codeph} objects are modal objects. This means that a
`Signature`{.codeph} object is always in a given state, where it may
only do one type of operation.

States are represented as final integer constants defined in their
respective classes.

The three states a `Signature`{.codeph} object may have are:

-   `UNINITIALIZED`{.codeph}
-   `SIGN`{.codeph}
-   `VERIFY`{.codeph}

When it is first created, a `Signature`{.codeph} object is in the
`UNINITIALIZED`{.codeph} state. The `Signature`{.codeph} class defines
two initialization methods, `initSign`{.codeph} and
`initVerify`{.codeph}, which change the state to `SIGN`{.codeph} and
`VERIFY`{.codeph} , respectively.

</div>
</div>
<div class="sect4">
[]{#GUID-1240FDC5-818E-4067-9C3C-D9635DF7D8A6}

#### Creating a Signature Object {#JSSEC-GUID-1240FDC5-818E-4067-9C3C-D9635DF7D8A6 .sect4}

<div>
The first step for signing or verifying a signature is to create a
`Signature`{.codeph} instance.

`Signature`{.codeph} objects are obtained by using one of the
`Signature`{.codeph} <span class="apiname">getInstance()</span> static
factory methods. See [How Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
</div>
<div class="sect4">
[]{#GUID-B3C371AB-A447-4F28-9C6E-1349FAC889E6}

#### Initializing a Signature Object {#JSSEC-GUID-B3C371AB-A447-4F28-9C6E-1349FAC889E6 .sect4}

<div>
A `Signature`{.codeph} object must be initialized before it is used. The
initialization method depends on whether the object is going to be used
for signing or for verification.

If it is going to be used for signing, the object must first be
initialized with the private key of the entity whose signature is going
to be generated. This initialization is done by calling the method:

``` {.codeblock dir="ltr"}
final void initSign(PrivateKey privateKey)
```

This method puts the `Signature`{.codeph} object in the `SIGN`{.codeph}
state. If instead the `Signature`{.codeph} object is going to be used
for verification, it must first be initialized with the public key of
the entity whose signature is going to be verified. This initialization
is done by calling either of these methods:

``` {.codeblock dir="ltr"}
    final void initVerify(PublicKey publicKey)

    final void initVerify(Certificate certificate)
```

This method puts the `Signature`{.codeph} object in the
`VERIFY`{.codeph} state.

</div>
</div>
<div class="sect4">
[]{#GUID-93D13151-06F6-4BEA-8F83-074CDB5809DA}

#### Signing with a Signature Object {#JSSEC-GUID-93D13151-06F6-4BEA-8F83-074CDB5809DA .sect4}

<div>
If the `Signature`{.codeph} object has been initialized for signing (if
it is in the `SIGN`{.codeph} state), the data to be signed can then be
supplied to the object. This is done by making one or more calls to one
of the `update`{.codeph} methods:

``` {.codeblock dir="ltr"}
final void update(byte b)
final void update(byte[] data)
final void update(byte[] data, int off, int len)
```

Calls to the `update`{.codeph} method(s) should be made until all the
data to be signed has been supplied to the `Signature`{.codeph} object.

To generate the signature, simply call one of the `sign`{.codeph}
methods:

``` {.codeblock dir="ltr"}
final byte[] sign()
final int sign(byte[] outbuf, int offset, int len)
```

The first method returns the signature result in a byte array. The
second stores the signature result in the provided buffer
<span class="variable">outbuf</span>, starting at
<span class="variable">offset</span>. <span class="variable">len</span>
is the number of bytes in <span class="variable">outbuf</span> allotted
for the signature. The method returns the number of bytes actually
stored.

Signature encoding is algorithm specific. See [Java Security Standard
Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
to know more about the use of ASN.1 encoding in the Java Cryptography
Architecture.

A call to a `sign`{.codeph} method resets the signature object to the
state it was in when previously initialized for signing via a call to
`initSign`{.codeph}. That is, the object is reset and available to
generate another signature with the same private key, if desired, via
new calls to `update`{.codeph} and `sign`{.codeph}.

Alternatively, a new call can be made to `initSign`{.codeph} specifying
a different private key, or to `initVerify`{.codeph} (to initialize the
`Signature`{.codeph} object to verify a signature).

</div>
</div>
<div class="sect4">
[]{#GUID-1B8AD667-3717-4D9E-B92E-322CFF8C832A}

#### Verifying with a Signature Object {#JSSEC-GUID-1B8AD667-3717-4D9E-B92E-322CFF8C832A .sect4}

<div>
If the `Signature`{.codeph} object has been initialized for verification
(if it is in the `VERIFY`{.codeph} state), it can then verify if an
alleged signature is in fact the authentic signature of the data
associated with it. To start the process, the data to be verified (as
opposed to the signature itself) is supplied to the object. The data is
passed to the object by calling one of the `update`{.codeph} methods:

``` {.codeblock dir="ltr"}
final void update(byte b)
final void update(byte[] data)
final void update(byte[] data, int off, int len)
```

Calls to the `update`{.codeph} method(s) should be made until all the
data to be verified has been supplied to the `Signature`{.codeph}
object. The signature can now be verified by calling one of the
`verify`{.codeph} methods:

``` {.codeblock dir="ltr"}
final boolean verify(byte[] signature)

final boolean verify(byte[] signature, int offset, int length)
```

The argument must be a byte array containing the signature. This byte
array would hold the signature bytes which were returned by a previous
call to one of the `sign`{.codeph} methods.

The `verify`{.codeph} method returns a `boolean`{.codeph} indicating
whether or not the encoded signature is the authentic signature of the
data supplied to the `update`{.codeph} method(s).

A call to the `verify`{.codeph} method resets the signature object to
its state when it was initialized for verification via a call to
`initVerify`{.codeph}. That is, the object is reset and available to
verify another signature from the identity whose public key was
specified in the call to `initVerify`{.codeph}.

Alternatively, a new call can be made to `initVerify`{.codeph}
specifying a different public key (to initialize the
`Signature`{.codeph} object for verifying a signature from a different
entity), or to `initSign`{.codeph} (to initialize the
`Signature`{.codeph} object for generating a signature).

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566}

### The Cipher Class {#JSSEC-GUID-94225C88-F2F1-44D1-A781-1DD9D5094566 .sect3}

<div>
The `Cipher`{.codeph} class provides the functionality of a
cryptographic cipher used for encryption and decryption. Encryption is
the process of taking data (called
<span class="variable">cleartext</span>) and a
<span class="variable">key</span>, and producing data
(<span class="variable">ciphertext</span>) meaningless to a third-party
who does not know the key. Decryption is the inverse process: that of
taking ciphertext and a key and producing cleartext.

<div class="figure" id="GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__GUID-25964623-7C57-4290-9086-29968AA379B1">
Figure 2-8 The Cipher Class

![Description of Figure 2-8
follows](img/cipher.gif "Description of Figure 2-8 follows")\
[Description of \"Figure 2-8 The Cipher Class\"](img_text/cipher.htm)

</div>
<!-- class="figure" -->

<div class="section">
Symmetric vs. Asymmetric Cryptography

There are two major types of encryption:
<span class="variable">symmetric</span> (also known as
<span class="variable">secret key</span>), and
<span class="variable">asymmetric</span> (or
<span class="variable">public key cryptography</span>). In symmetric
cryptography, the same secret key to both encrypt and decrypt the data.
Keeping the key private is critical to keeping the data confidential. On
the other hand, asymmetric cryptography uses a public/private key pair
to encrypt data. Data encrypted with one key is decrypted with the
other. A user first generates a public/private key pair, and then
publishes the public key in a trusted database that anyone can access. A
user who wishes to communicate securely with that user encrypts the data
using the retrieved public key. Only the holder of the private key will
be able to decrypt. Keeping the private key confidential is critical to
this scheme.

Asymmetric algorithms (such as RSA) are generally much slower than
symmetric ones. These algorithms are not designed for efficiently
protecting large amounts of data. In practice, asymmetric algorithms are
used to exchange smaller secret keys which are used to initialize
symmetric algorithms.

</div>
<!-- class="section" -->

<div class="section">
Stream vs. Block Ciphers

There are two major types of ciphers:
<span class="variable">block</span> and
<span class="variable">stream</span>. Block ciphers process entire
blocks at a time, usually many bytes in length. If there is not enough
data to make a complete input block, the data must be
<span class="variable">padded</span>: that is, before encryption, dummy
bytes must be added to make a multiple of the cipher\'s block size.
These bytes are then stripped off during the decryption phase. The
padding can either be done by the application, or by initializing a
cipher to use a padding type such as \"PKCS5PADDING\". In contrast,
stream ciphers process incoming data one small unit (typically a byte or
even a bit) at a time. This allows for ciphers to process an arbitrary
amount of data without padding.

</div>
<!-- class="section" -->

<div class="section" id="GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__MODESOFOPERATION-A64768C7">
Modes Of Operation

When encrypting using a simple block cipher, two identical blocks of
plaintext will always produce an identical block of cipher text.
Cryptanalysts trying to break the ciphertext will have an easier job if
they note blocks of repeating text. A cipher mode of operation makes the
ciphertext less predictable with output block alterations based on block
position or the values of other ciphertext blocks. The first block will
need an initial value, and this value is called the
<span class="variable">initialization vector (IV)</span>. Since the IV
simply alters the data before any encryption, the IV should be random
but does not necessarily need to be kept secret. There are a variety of
modes, such as CBC (Cipher Block Chaining), CFB (Cipher Feedback Mode),
and OFB (Output Feedback Mode). ECB (Electronic Codebook Mode) is a mode
in which there is no influence from block position or other ciphertext
blocks. Because ECB ciphertexts are the same if they use the same
plaintext/key, this mode is not typically suitable for cryptographic
applications and should not be used.

Some algorithms such as AES and RSA allow for keys of different lengths,
but others are fixed, such as 3DES. Encryption using a longer key
generally implies a stronger resistance to message recovery. As usual,
there is a trade off between security and time, so choose the key length
appropriately.

Most algorithms use binary keys. Most humans do not have the ability to
remember long sequences of binary numbers, even when represented in
hexadecimal. Character passwords are much easier to recall. Because
character passwords are generally chosen from a small number of
characters (for example, \[a-zA-Z0-9\]), protocols such as
\"Password-Based Encryption\" (PBE) have been defined which take
character passwords and generate strong binary keys. In order to make
the task of getting from password to key very time-consuming for an
attacker (via so-called \"rainbow table attacks\" or \"precomputed
dictionary attacks\" where common dictionary word-\>value mappings are
precomputed), most PBE implementations will mix in a random number,
known as a <span class="variable">salt</span>, to reduce the usefulness
of precomputed tables.

Newer cipher modes such as Authenticated Encryption with Associated Data
(AEAD) (for example, [Galois/Counter Mode
(GCM)](http://csrc.nist.gov/publications/nistpubs/800-38D/SP-800-38D.pdf))
encrypt data and authenticate the resulting message simultaneously.
Additional Associated Data (AAD) can be used during the calculation of
the resulting AEAD tag (MAC), but this AAD data is not output as
ciphertext. (For example, some data might not need to be kept
confidential, but should figure into the tag calculation to detect
modifications.) The <span class="apiname">Cipher.updateAAD()</span>
methods can be used to include AAD in the tag calculations.

</div>
<!-- class="section" -->

<div class="section">
Using an AES Cipher with GCM Mode

AES Cipher with GCM is an AEAD Cipher which has different usage patterns
than the non-AEAD ciphers. Apart from the regular data, it also takes
AAD which is optional for encryption/decryption but AAD must be supplied
before data for encryption/decryption. In addition, in order to use GCM
securely, callers should not re-use key and IV combinations for
encryption. This means that the cipher object should be explicitly
re-initialized with a different set of parameters every time for each
encryption operation.

</div>
<!-- class="section" -->

<div class="example" id="GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__SECRETKEYMYKEY...BYTEMYAAD...BYTEPL-7249BF00">
Example 2-2 Sample Code for Using an AES Cipher with GCM Mode

``` {.codeblock dir="ltr"}
    SecretKey myKey = ...
    byte[] myAAD = ...
    byte[] plainText = ...
        int myTLen = ... 
        byte[] myIv = ...

    GCMParameterSpec myParams = new GCMParameterSpec(myTLen, myIv);
    Cipher c = Cipher.getInstance("AES/GCM/NoPadding");
    c.init(Cipher.ENCRYPT_MODE, myKey, myParams);

    // AAD is optional, if present, it must be supplied before any update/doFinal calls.
    c.updateAAD(myAAD);  // if AAD is non-null
    byte[] cipherText = new byte[c.getOutputSize(plainText.length)];
    // conclusion of encryption operation
    int actualOutputLen = c.doFinal(plainText, 0, plainText.length, cipherText);
 
    // To decrypt, same AAD and GCM parameters must be supplied
    c.init(Cipher.DECRYPT_MODE, myKey, myParams);
    c.updateAAD(myAAD);
    byte[] recoveredText = c.doFinal(cipherText, 0, actualOutputLen);

    // MUST CHANGE IV VALUE if the same key were to be used again for encryption
        byte[] newIv = ...;
    myParams = new GCMParameterSpec(myTLen, newIv);
```

</div>
<!-- class="example" -->

<div class="section">
Creating a Cipher Object

`Cipher`{.codeph} objects are obtained by using one of the
`Cipher`{.codeph} <span class="apiname">getInstance()</span> static
factory methods. See [How Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).
Here, the algorithm name is slightly different than with other engine
classes, in that it specifies not just an algorithm name, but a
\"transformation\". A transformation is a string that describes the
operation (or set of operations) to be performed on the given input to
produce some output. A transformation always includes the name of a
cryptographic algorithm (e.g., `AES`{.codeph}), and may be followed by a
mode and padding scheme.

A transformation is of the form:

-   \"<span class="variable">algorithm/mode/padding</span>\" or
-   \"<span class="variable">algorithm</span>\"

For example, the following are valid transformations:

``` {.codeblock dir="ltr"}
    "AES/CBC/PKCS5Padding"

    "AES"
```

If just a transformation name is specified, the system will determine if
there is an implementation of the requested transformation available in
the environment, and if there is more than one, returns there is a
preferred one.

If both a transformation name and a package provider are specified, the
system will determine if there is an implementation of the requested
transformation in the package requested, and throw an exception if there
is not.

It is recommended to use a transformation that fully specifies the
algorithm, mode, and padding. By not doing so, the provider will use a
default. For example, the SunJCE and SunPKCS11 providers use ECB as the
default mode, and PKCS5Padding as the default padding for many symmetric
ciphers.

This means that in the case of the `SunJCE`{.codeph} provider:

``` {.codeblock dir="ltr"}
    Cipher c1 = Cipher.getInstance("AES/ECB/PKCS5Padding");
```

and

``` {.codeblock dir="ltr"}
    Cipher c1 = Cipher.getInstance("AES");
```

are equivalent statements.

<div class="p">
<div class="infoboxnote" id="GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__GUID-CAFC698A-6EE6-4448-98F8-9FE612C86FDA">
Note:

ECB mode is the easiest block cipher mode to use and is the default in
the JDK and JRE. ECB works for single blocks of data when using
different keys, but it absolutely should not be used for multiple data
blocks. Other cipher modes such as Cipher Block Chaining (CBC) or
Galois/Counter Mode (GCM) are more appropriate.

</div>
</div>
Using modes such as CFB and OFB, block ciphers can encrypt data in units
smaller than the cipher\'s actual block size. When requesting such a
mode, you may optionally specify the number of bits to be processed at a
time by appending this number to the mode name as shown in the
\"<span class="variable">AES/CFB8/NoPadding</span>\" and
\"<span class="variable">AES/OFB32/PKCS5Padding</span>\"
transformations. If no such number is specified, a provider-specific
default is used. (For example, the `SunJCE`{.codeph} provider uses a
default of 128 bits for AES.) Thus, block ciphers can be turned into
byte-oriented stream ciphers by using an 8 bit mode such as CFB8 or
OFB8.

[Java Security Standard Algorithm
Names](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
contains a list of standard names that can be used to specify the
algorithm name, mode, and padding scheme components of a transformation.

The objects returned by factory methods are uninitialized, and must be
initialized before they become usable.

</div>
<!-- class="section" -->

<div class="section">
Initializing a Cipher Object

A Cipher object obtained via `getInstance`{.codeph} must be initialized
for one of four modes, which are defined as final integer constants in
the `Cipher`{.codeph} class. The modes can be referenced by their
symbolic names, which are shown below along with a description of the
purpose of each mode:

[<!-- -->]{#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__GUID-7CD0B30D-A692-401F-8B7F-1D8CAF2558AA}ENCRYPT\_MODE
:   Encryption of data.

[<!-- -->]{#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__GUID-5E5D22CB-35E7-4472-BB46-C85985D27707}DECRYPT\_MODE
:   Decryption of data.

[<!-- -->]{#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__GUID-53BB5B82-CDCF-4FA4-83F9-5F0B82EC715C}WRAP\_MODE
:   Wrapping a `java.security.Key`{.codeph} into bytes so that the key
    can be securely transported.

[<!-- -->]{#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__GUID-17922D9E-7BE5-4179-B8E0-0C06E4BAFD60}UNWRAP\_MODE
:   Unwrapping of a previously wrapped key into a
    `java.security.Key`{.codeph} object.

Each of the Cipher initialization methods takes an operational mode
parameter (`opmode`{.codeph}), and initializes the Cipher object for
that mode. Other parameters include the key (`key`{.codeph}) or
certificate containing the key (`certificate`{.codeph}), algorithm
parameters (`params`{.codeph}), and a source of randomness
(`random`{.codeph}).

To initialize a Cipher object, call one of the following `init`{.codeph}
methods:

``` {.codeblock dir="ltr"}
    public void init(int opmode, Key key);

    public void init(int opmode, Certificate certificate);

    public void init(int opmode, Key key, SecureRandom random);

    public void init(int opmode, Certificate certificate,
                     SecureRandom random);

    public void init(int opmode, Key key,
                     AlgorithmParameterSpec params);

    public void init(int opmode, Key key,
                     AlgorithmParameterSpec params, SecureRandom random);

    public void init(int opmode, Key key,
                     AlgorithmParameters params);

    public void init(int opmode, Key key,
                     AlgorithmParameters params, SecureRandom random);
```

If a Cipher object that requires parameters (e.g., an initialization
vector) is initialized for encryption, and no parameters are supplied to
the `init`{.codeph} method, the underlying cipher implementation is
supposed to supply the required parameters itself, either by generating
random parameters or by using a default, provider-specific set of
parameters.

However, if a Cipher object that requires parameters is initialized for
decryption, and no parameters are supplied to the `init`{.codeph}
method, an `InvalidKeyException`{.codeph} or
`InvalidAlgorithmParameterException`{.codeph} exception will be raised,
depending on the `init`{.codeph} method that has been used.

See [Managing Algorithm
Parameters](java-cryptography-architecture-jca-reference-guide.html#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__MANAGINGALGORITHMPARAMETERS-63E08852).

The same parameters that were used for encryption must be used for
decryption.

Note that when a Cipher object is initialized, it loses all
previously-acquired state. In other words, initializing a Cipher is
equivalent to creating a new instance of that Cipher, and initializing
it. For example, if a Cipher is first initialized for decryption with a
given key, and then initialized for encryption, it will lose any state
acquired while in decryption mode.

</div>
<!-- class="section" -->

<div class="section">
Encrypting and Decrypting Data

Data can be encrypted or decrypted in one step
(<span class="variable">single-part operation</span>) or in multiple
steps (<span class="variable">multiple-part operation</span>). A
multiple-part operation is useful if you do not know in advance how long
the data is going to be, or if the data is too long to be stored in
memory all at once.

To encrypt or decrypt data in a single step, call one of the
`doFinal`{.codeph} methods:

``` {.codeblock dir="ltr"}
    public byte[] doFinal(byte[] input);

    public byte[] doFinal(byte[] input, int inputOffset, int inputLen);

    public int doFinal(byte[] input, int inputOffset,
                       int inputLen, byte[] output);

    public int doFinal(byte[] input, int inputOffset,
                       int inputLen, byte[] output, int outputOffset)
```

To encrypt or decrypt data in multiple steps, call one of the
`update`{.codeph} methods:

``` {.codeblock dir="ltr"}
    public byte[] update(byte[] input);

    public byte[] update(byte[] input, int inputOffset, int inputLen);

    public int update(byte[] input, int inputOffset, int inputLen,
                      byte[] output);

    public int update(byte[] input, int inputOffset, int inputLen,
                      byte[] output, int outputOffset)
```

A multiple-part operation must be terminated by one of the above
`doFinal`{.codeph} methods (if there is still some input data left for
the last step), or by one of the following `doFinal`{.codeph} methods
(if there is no input data left for the last step):

``` {.codeblock dir="ltr"}
    public byte[] doFinal();

    public int doFinal(byte[] output, int outputOffset);
```

All the `doFinal`{.codeph} methods take care of any necessary padding
(or unpadding), if padding (or unpadding) has been requested as part of
the specified transformation.

A call to `doFinal`{.codeph} resets the Cipher object to the state it
was in when initialized via a call to `init`{.codeph}. That is, the
Cipher object is reset and available to encrypt or decrypt (depending on
the operation mode that was specified in the call to `init`{.codeph})
more data.

</div>
<!-- class="section" -->

<div class="section" id="GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__WRAPPINGANDUNWRAPPINGKEYS-74578038">
Wrapping and Unwrapping Keys

Wrapping a key enables secure transfer of the key from one place to
another.

The `wrap/unwrap`{.codeph} API makes it more convenient to write code
since it works with key objects directly. These methods also enable the
possibility of secure transfer of hardware-based keys.

To <span class="bold">wrap</span> a Key, first initialize the Cipher
object for WRAP\_MODE, and then call the following:

``` {.codeblock dir="ltr"}
    public final byte[] wrap(Key key);
```

If you are supplying the wrapped key bytes (the result of calling
`wrap`{.codeph}) to someone else who will unwrap them, be sure to also
send additional information the recipient will need in order to do the
`unwrap`{.codeph}:

-   The name of the key algorithm.
-   The type of the wrapped key (one of `Cipher.SECRET_KEY`{.codeph},
    `Cipher.PRIVATE_KEY`{.codeph}, or `Cipher.PUBLIC_KEY`{.codeph}).

The key algorithm name can be determined by calling the
`getAlgorithm`{.codeph} method from the Key interface:

``` {.codeblock dir="ltr"}
    public String getAlgorithm();
```

To <span class="bold">unwrap</span> the bytes returned by a previous
call to `wrap`{.codeph}, first initialize a Cipher object for
UNWRAP\_MODE, then call the following:

``` {.codeblock dir="ltr"}
    public final Key unwrap(byte[] wrappedKey,
                            String wrappedKeyAlgorithm,
                            int wrappedKeyType));
```

Here, `wrappedKey`{.codeph} is the bytes returned from the previous call
to wrap, `wrappedKeyAlgorithm`{.codeph} is the algorithm associated with
the wrapped key, and `wrappedKeyType`{.codeph} is the type of the
wrapped key. This must be one of `Cipher.SECRET_KEY`{.codeph},
`Cipher.PRIVATE_KEY`{.codeph}, or `Cipher.PUBLIC_KEY`{.codeph}.

</div>
<!-- class="section" -->

<div class="section" id="GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__MANAGINGALGORITHMPARAMETERS-63E08852">
Managing Algorithm Parameters

The parameters being used by the underlying
<span class="apiname">Cipher</span> implementation, which were either
explicitly passed to the `init`{.codeph} method by the application or
generated by the underlying implementation itself, can be retrieved from
the <span class="apiname">Cipher</span> object by calling its
`getParameters`{.codeph} method, which returns the parameters as a
`java.security.AlgorithmParameters`{.codeph} object (or `null`{.codeph}
if no parameters are being used). If the parameter is an initialization
vector (IV), it can also be retrieved by calling the `getIV`{.codeph}
method.

In the following example, a <span class="apiname">Cipher</span> object
implementing password-based encryption (PBE) is initialized with just a
key and no parameters. However, the selected algorithm for
password-based encryption requires two parameters - a
<span class="variable">salt</span> and an
<span class="variable">iteration count</span>. Those will be generated
by the underlying algorithm implementation itself. The application can
retrieve the generated parameters from the
<span class="apiname">Cipher</span> object, see [Example
2-3](java-cryptography-architecture-jca-reference-guide.html#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__EXAMPLE-1314-724A0BB7).

The same parameters that were used for encryption must be used for
decryption. They can be instantiated from their encoding and used to
initialize the corresponding Cipher object for decryption, see [Example
2-4](java-cryptography-architecture-jca-reference-guide.html#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__EXAMPLE-1315-724A0E25).

If you did not specify any parameters when you initialized a Cipher
object, and you are not sure whether or not the underlying
implementation uses any parameters, you can find out by simply calling
the `getParameters`{.codeph} method of your Cipher object and checking
the value returned. A return value of `null`{.codeph} indicates that no
parameters were used.

The following cipher algorithms implemented by the `SunJCE`{.codeph}
provider use parameters:

-   AES, DES-EDE, and Blowfish, when used in feedback (i.e., CBC, CFB,
    OFB, or PCBC) mode, use an initialization vector (IV). The
    `javax.crypto.spec.IvParameterSpec`{.codeph} class can be used to
    initialize a <span class="apiname">Cipher</span> object with a
    given IV. In addition, CTR and GCM modes require an IV.
-   PBE <span class="apiname">Cipher</span> algorithms use a set of
    parameters, comprising a salt and an iteration count. The
    `javax.crypto.spec.PBEParameterSpec`{.codeph} class can be used to
    initialize a <span class="apiname">Cipher</span> object implementing
    a PBE algorithm (for example: PBEWithHmacSHA256AndAES\_256) with a
    given salt and iteration count.

Note that you do not have to worry about storing or transferring any
algorithm parameters for use by the decryption operation if you use the
[The SealedObject
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-33BA4D9F-5253-4A53-81C1-38569E8FFCA8 "This class enables a programmer to create an object and protect its confidentiality with a cryptographic algorithm.")
class. This class attaches the parameters used for sealing (encryption)
to the encrypted object contents, and uses the same parameters for
unsealing (decryption).

</div>
<!-- class="section" -->

<div class="example" id="GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__EXAMPLE-1314-724A0BB7">
Example 2-3 Sample Code for Retrieving Parameters from the Cipher Object

The application can retrieve the generated parameters for encryption
from the Cipher object as follows:

``` {.codeblock dir="ltr"}
    import javax.crypto.*;
    import java.security.AlgorithmParameters;

    // get cipher object for password-based encryption
    Cipher c = Cipher.getInstance("PBEWithHmacSHA256AndAES_256");

    // initialize cipher for encryption, without supplying
    // any parameters. Here, "myKey" is assumed to refer
    // to an already-generated key.
    c.init(Cipher.ENCRYPT_MODE, myKey);

    // encrypt some data and store away ciphertext
    // for later decryption
    byte[] cipherText = c.doFinal("This is just an example".getBytes());

    // retrieve parameters generated by underlying cipher
    // implementation
    AlgorithmParameters algParams = c.getParameters();

    // get parameter encoding and store it away
    byte[] encodedAlgParams = algParams.getEncoded();
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-94225C88-F2F1-44D1-A781-1DD9D5094566__EXAMPLE-1315-724A0E25">
Example 2-4 Sample Code for Initializing the Cipher Object for
Decryption

The same parameters that were used for encryption must be used for
decryption. They can be instantiated from their encoding and used to
initialize the corresponding Cipher object for decryption as follows:

``` {.codeblock dir="ltr"}
    import javax.crypto.*;
    import java.security.AlgorithmParameters;

    // get parameter object for password-based encryption
    AlgorithmParameters algParams;
    algParams = AlgorithmParameters.getInstance("PBEWithHmacSHA256AndAES_256");

    // initialize with parameter encoding from above
    algParams.init(encodedAlgParams);

    // get cipher object for password-based encryption
    Cipher c = Cipher.getInstance("PBEWithHmacSHA256AndAES_256");

    // initialize cipher for decryption, using one of the
    // init() methods that takes an AlgorithmParameters
    // object, and pass it the algParams object from above
    c.init(Cipher.DECRYPT_MODE, myKey, algParams);
```

</div>
<!-- class="example" -->

<div class="section">
Cipher Output Considerations

Some of the `update`{.codeph} and `doFinal`{.codeph} methods of Cipher
allow the caller to specify the output buffer into which to encrypt or
decrypt the data. In these cases, it is important to pass a buffer that
is large enough to hold the result of the encryption or decryption
operation.

The following method in Cipher can be used to determine how big the
output buffer should be:

``` {.codeblock dir="ltr"}
    public int getOutputSize(int inputLen)
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-F64C7E9B-12B4-4BFA-A4E7-B2877400C836}

### Other Cipher-based Classes {#JSSEC-GUID-F64C7E9B-12B4-4BFA-A4E7-B2877400C836 .sect3}

<div>
There are some helper classes which internally use `Cipher`{.codeph}s to
provide easy access to common cipher uses.

<div class="section">
Topics

[The Cipher Stream
Classes](java-cryptography-architecture-jca-reference-guide.html#GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF "The CipherInputStream and CipherOutputStream classes are Cipher stream classes.")

[The SealedObject
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-33BA4D9F-5253-4A53-81C1-38569E8FFCA8 "This class enables a programmer to create an object and protect its confidentiality with a cryptographic algorithm.")

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF}

#### The Cipher Stream Classes {#JSSEC-GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF .sect4}

<div>
The `CipherInputStream`{.codeph} and `CipherOutputStream`{.codeph}
classes are Cipher stream classes.

<div class="section">
The CipherInputStream Class

This class is a `FilterInputStream`{.codeph} that encrypts or decrypts
the data passing through it. It is composed of an
`InputStream`{.codeph}. <span class="apiname">CipherInputStream</span>
represents a secure input stream into which a
<span class="apiname">Cipher</span> object has been interposed. The
`read`{.codeph} methods of
<span class="apiname">CipherInputStream</span> return data that are read
from the underlying <span class="apiname">InputStream</span> but have
additionally been processed by the embedded
<span class="apiname">Cipher</span> object. The
<span class="apiname">Cipher</span> object must be fully initialized
before being used by a CipherInputStream.

For example, if the embedded <span class="apiname">Cipher</span> has
been initialized for decryption, the
<span class="apiname">CipherInputStream</span> will attempt to decrypt
the data it reads from the underlying
<span class="apiname">InputStream</span> before returning them to the
application.

This class adheres strictly to the semantics, especially the failure
semantics, of its ancestor classes `java.io.FilterInputStream`{.codeph}
and `java.io.InputStream`{.codeph}. This class has exactly those methods
specified in its ancestor classes, and overrides them all, so that the
data are additionally processed by the embedded cipher. Moreover, this
class catches all exceptions that are not thrown by its ancestor
classes. In particular, the `skip(long)`{.codeph} method skips only data
that has been processed by the <span class="apiname">Cipher</span>.

It is crucial for a programmer using this class not to use methods that
are not defined or overridden in this class (such as a new method or
constructor that is later added to one of the super classes), because
the design and implementation of those methods are unlikely to have
considered security impact with regard to
<span class="apiname">CipherInputStream</span>. See [Example
2-5](java-cryptography-architecture-jca-reference-guide.html#GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF__SAMPLECODEFORENCRYPTINGINPUTSTREAMD-74CAEA35)
for its usage, suppose `cipher1`{.codeph} has been initialized for
encryption. The program reads and encrypts the content from the file
`/tmp/a.txt`{.codeph} and then stores the result (the encrypted bytes)
in `/tmp/b.txt`{.codeph}.

[Example
2-6](java-cryptography-architecture-jca-reference-guide.html#GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF__THEFOLLOWINGEXAMPLEDEMONSTRATESHOWT-74CAEEB6)
demonstrates how to easily connect several instances of
`CipherInputStream`{.codeph} and `FileInputStream`{.codeph}. In this
example, assume that `cipher1`{.codeph} and `cipher2`{.codeph} have been
initialized for encryption and decryption (with corresponding keys),
respectively. The program copies the content from file
`/tmp/a.txt`{.codeph} to `/tmp/b.txt`{.codeph}, except that the content
is first encrypted and then decrypted back when it is read from
`/tmp/a.txt`{.codeph}. Of course since this program simply encrypts text
and decrypts it back right away, it\'s actually not very useful except
as a simple way of illustrating chaining of
`CipherInputStreams`{.codeph}.

Note that the read methods of the `CipherInputStream`{.codeph} will
block until data is returned from the underlying cipher. If a block
cipher is used, a full block of cipher text will have to be obtained
from the underlying `InputStream`{.codeph}.

</div>
<!-- class="section" -->

<div class="example" id="GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF__SAMPLECODEFORENCRYPTINGINPUTSTREAMD-74CAEA35">
Example 2-5 Sample Code for Using CipherInputStream and FileInputStream

The code below demonstrates how to use a `CipherInputStream`{.codeph}
containing that cipher and a `FileInputStream`{.codeph} in order to
encrypt input stream data:

``` {.codeblock dir="ltr"}
try (FileInputStream fis = new FileInputStream("/tmp/a.txt");
CipherInputStream cis = new CipherInputStream(fis, cipher1);
FileOutputStream fos = new FileOutputStream("/tmp/b.txt")) {
    byte[] b = new byte[8];
    int i = cis.read(b);
    while (i != -1) {
        fos.write(b, 0, i);
        i = cis.read(b);
    }
}
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF__THEFOLLOWINGEXAMPLEDEMONSTRATESHOWT-74CAEEB6">
Example 2-6 Sample Code for Connecting CipherInputStream and
FileInputStream

The following example demonstrates how to easily connect several
instances of <span class="apiname">CipherInputStream</span> and
<span class="apiname">FileInputStream</span>. In this example, assume
that `cipher1`{.codeph} and `cipher2`{.codeph} have been initialized for
encryption and decryption (with corresponding keys), respectively:

``` {.codeblock dir="ltr"}
try (FileInputStream fis = new FileInputStream("/tmp/a.txt");
        CipherInputStream cis1 = new CipherInputStream(fis, cipher1);
        CipherInputStream cis2 = new CipherInputStream(cis1, cipher2);
        FileOutputStream fos = new FileOutputStream("/tmp/b.txt")) {
    byte[] b = new byte[8];
    int i = cis2.read(b);
    while (i != -1) {
        fos.write(b, 0, i);
        i = cis2.read(b);
    }
}  
```

</div>
<!-- class="example" -->

<div class="section">
The CipherOutputStream Class

This class is a `FilterOutputStream`{.codeph} that encrypts or decrypts
the data passing through it. It is composed of an
`OutputStream`{.codeph}, or one of its subclasses, and a
`Cipher`{.codeph}. <span class="apiname">CipherOutputStream</span>
represents a secure output stream into which a
<span class="apiname">Cipher</span> object has been interposed. The
`write`{.codeph} methods of
<span class="apiname">CipherOutputStream</span> first process the data
with the embedded <span class="apiname">Cipher</span> object before
writing them out to the underlying
<span class="apiname">OutputStream</span>. The
<span class="apiname">Cipher</span> object must be fully initialized
before being used by a <span class="apiname">CipherOutputStream</span>.

For example, if the embedded <span class="apiname">Cipher</span> has
been initialized for encryption, the `CipherOutputStream`{.codeph} will
encrypt its data, before writing them out to the underlying output
stream.

This class adheres strictly to the semantics, especially the failure
semantics, of its ancestor classes `java.io.OutputStream`{.codeph} and
`java.io.FilterOutputStream`{.codeph}. This class has exactly those
methods specified in its ancestor classes, and overrides them all, so
that all data are additionally processed by the embedded cipher.
Moreover, this class catches all exceptions that are not thrown by its
ancestor classes.

It is crucial for a programmer using this class not to use methods that
are not defined or overridden in this class (such as a new method or
constructor that is later added to one of the super classes), because
the design and implementation of those methods are unlikely to have
considered security impact with regard to `CipherOutputStream`{.codeph}.

See [Example
2-7](java-cryptography-architecture-jca-reference-guide.html#GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF__SAMPLECODEFORUSINGCIPHEROUTPUTSTREA-74D596DC)
, for its usage, suppose `cipher1`{.codeph} has been initialized for
encryption. The program reads the content from the file
`/tmp/a.txt`{.codeph}, then encrypts and stores the result (the
encrypted bytes) in `/tmp/b.txt`{.codeph}.

[Example
2-7](java-cryptography-architecture-jca-reference-guide.html#GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF__SAMPLECODEFORUSINGCIPHEROUTPUTSTREA-74D596DC)
demonstrates how to easily connect several instances of
`CipherOutputStream`{.codeph} and `FileOutputStream`{.codeph}. In this
example, assume that `cipher1`{.codeph} and `cipher2`{.codeph} have been
initialized for decryption and encryption (with corresponding keys),
respectively. The program copies the content from file
`/tmp/a.txt`{.codeph} to `/tmp/b.txt`{.codeph}, except that the content
is first encrypted and then decrypted back before it is written to
`/tmp/b.txt`{.codeph}.

One thing to keep in mind when using <span class="variable">block</span>
cipher algorithms is that a full block of plaintext data must be given
to the `CipherOutputStream`{.codeph} before the data will be encrypted
and sent to the underlying output stream.

There is one other important difference between the `flush`{.codeph} and
`close`{.codeph} methods of this class, which becomes even more relevant
if the encapsulated <span class="apiname">Cipher</span> object
implements a block cipher algorithm with padding turned on:

-   `flush`{.codeph} flushes the underlying
    <span class="apiname">OutputStream</span> by forcing any buffered
    output bytes that have already been processed by the encapsulated
    Cipher object to be written out. Any bytes buffered by the
    encapsulated <span class="apiname">Cipher</span> object and waiting
    to be processed by it will <span class="bold">not</span> be written
    out.
-   `close`{.codeph} closes the underlying
    <span class="apiname">OutputStream</span> and releases any system
    resources associated with it. It invokes the `doFinal`{.codeph}
    method of the encapsulated <span class="apiname">Cipher</span>
    object, causing any bytes buffered by it to be processed and written
    out to the underlying stream by calling its `flush`{.codeph} method.

</div>
<!-- class="section" -->

<div class="example" id="GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF__SAMPLECODEFORUSINGCIPHEROUTPUTSTREA-74D596DC">
Example 2-7 Sample Code for Using CipherOutputStream and
FileOutputStream

The code demonstrates how to use a `CipherOutputStream`{.codeph}
containing that cipher and a `FileOutputStream`{.codeph} in order to
encrypt data to be written to an output stream:

``` {.codeblock dir="ltr"}
try (FileInputStream fis = new FileInputStream("/tmp/a.txt");
        FileOutputStream fos = new FileOutputStream("/tmp/b.txt");
        CipherOutputStream cos = new CipherOutputStream(fos, cipher1)) {
    byte[] b = new byte[8];
    int i = fis.read(b);
    while (i != -1) {
        cos.write(b, 0, i);
        i = fis.read(b);
    }
    cos.flush();
}
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF__SAMPLECODEFORCONNECTINGCIPHEROUTPUT-74D599F3">
Example 2-8 Sample Code for Connecting CipherOutputStream and
FileOutputStream

The code demonstrates how to easily connect several instances of
<span class="apiname">CipherOutputStream</span> and
<span class="apiname">FileOutputStream</span>. In this example, assume
that `cipher1`{.codeph} and `cipher2`{.codeph} have been initialized for
decryption and encryption (with corresponding keys), respectively:

``` {.codeblock dir="ltr"}
try (FileInputStream fis = new FileInputStream("/tmp/a.txt");
        FileOutputStream fos = new FileOutputStream("/tmp/b.txt");
        CipherOutputStream cos1 = new CipherOutputStream(fos, cipher1);
        CipherOutputStream cos2 = new CipherOutputStream(cos1, cipher2)) {
    byte[] b = new byte[8];
    int i = fis.read(b);
    while (i != -1) {
        cos2.write(b, 0, i);
        i = fis.read(b);
    }
    cos2.flush();
}
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-33BA4D9F-5253-4A53-81C1-38569E8FFCA8}

#### The SealedObject Class {#JSSEC-GUID-33BA4D9F-5253-4A53-81C1-38569E8FFCA8 .sect4}

<div>
This class enables a programmer to create an object and protect its
confidentiality with a cryptographic algorithm.

<div class="section">
Given any object that implements the `java.io.Serializable`{.codeph}
interface, one can create a `SealedObject`{.codeph} that encapsulates
the original object, in serialized format (i.e., a \"deep copy\"), and
seals (encrypts) its serialized contents, using a cryptographic
algorithm such as AES, to protect its confidentiality. The encrypted
content can later be decrypted (with the corresponding algorithm using
the correct decryption key) and de-serialized, yielding the original
object.

A typical usage is illustrated in the following code segment: In order
to seal an object, you create a `SealedObject`{.codeph} from the object
to be sealed and a fully initialized `Cipher`{.codeph} object that will
encrypt the serialized object contents. In this example, the String
\"This is a secret\" is sealed using the AES algorithm. Note that any
algorithm parameters that may be used in the sealing operation are
stored inside of `SealedObject`{.codeph}:

``` {.codeblock dir="ltr"}
    // create Cipher object
    // NOTE: sKey is assumed to refer to an already-generated
    // secret AES key.
    Cipher c = Cipher.getInstance("AES");
    c.init(Cipher.ENCRYPT_MODE, sKey);

    // do the sealing
    SealedObject so = new SealedObject("This is a secret", c);
```

The original object that was sealed can be recovered in two different
ways:

-   by using a `Cipher`{.codeph} object that has been initialized with
    the exact same algorithm, key, padding scheme, etc., that were used
    to seal the object:

    ``` {.codeblock dir="ltr"}
        c.init(Cipher.DECRYPT_MODE, sKey);
        try {
            String s = (String)so.getObject(c);
        } catch (Exception e) {
            // do something
        };
    ```

    This approach has the advantage that the party who unseals the
    sealed object does not require knowledge of the decryption key. For
    example, after one party has initialized the cipher object with the
    required decryption key, it could hand over the cipher object to
    another party who then unseals the sealed object.

-   by using the appropriate decryption key (since AES is a symmetric
    encryption algorithm, we use the same key for sealing and
    unsealing):

    ``` {.codeblock dir="ltr"}
        try {
            String s = (String)so.getObject(sKey);
        } catch (Exception e) {
            // do something
        };
    ```

    In this approach, the `getObject`{.codeph} method creates a cipher
    object for the appropriate decryption algorithm and initializes it
    with the given decryption key and the algorithm parameters (if any)
    that were stored in the sealed object. This approach has the
    advantage that the party who unseals the object does not need to
    keep track of the parameters (e.g., the IV) that were used to seal
    the object.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-8E014689-EBBB-4DE1-B6E0-24CE59AD8B9A}

### The Mac Class {#JSSEC-GUID-8E014689-EBBB-4DE1-B6E0-24CE59AD8B9A .sect3}

<div>
Similar to a `MessageDigest`{.codeph}, a Message Authentication Code
(MAC) provides a way to check the integrity of information transmitted
over or stored in an unreliable medium, but includes a secret key in the
calculation.

<div class="section">
Only someone with the proper key will be able to verify the received
message. Typically, message authentication codes are used between two
parties that share a secret key in order to validate information
transmitted between these parties.

<div class="figure" id="GUID-8E014689-EBBB-4DE1-B6E0-24CE59AD8B9A__GUID-53D5C5FD-6E47-42AC-AEA2-C8BDCFB8B566">
Figure 2-9 The Mac Class

![Description of Figure 2-9
follows](img/mac-class.png "Description of Figure 2-9 follows")\
[Description of \"Figure 2-9 The Mac Class\"](img_text/mac-class.htm)

</div>
<!-- class="figure" -->

A MAC mechanism that is based on cryptographic hash functions is
referred to as HMAC. HMAC can be used with any cryptographic hash
function, e.g., SHA-256, in combination with a secret shared key.

The `Mac`{.codeph} class provides the functionality of a Message
Authentication Code (MAC). See [HMAC-SHA256
Example](java-cryptography-architecture-jca-reference-guide.html#GUID-1B141C6A-7BB3-4DA2-A112-ADEBCE7F4B4A "The following is a sample program that demonstrates how to generate a secret-key object for HMAC-SHA256, and initialize a HMAC-SHA256 object with it.").

</div>
<!-- class="section" -->

<div class="section">
Creating a Mac Object

`Mac`{.codeph} objects are obtained by using one of the `Mac`{.codeph}
<span class="apiname"> getInstance() </span>static factory methods. See
[How Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Initializing a Mac Object

A Mac object is always initialized with a (secret) key and may
optionally be initialized with a set of parameters, depending on the
underlying MAC algorithm.

To initialize a Mac object, call one of its
<span class="apiname">init</span> methods:

``` {.codeblock dir="ltr"}
    public void init(Key key);

    public void init(Key key, AlgorithmParameterSpec params);
```

You can initialize your Mac object with any (secret-)key object that
implements the `javax.crypto.SecretKey`{.codeph} interface. This could
be an object returned by
<span class="apiname">javax.crypto.KeyGenerator.generateKey()</span>, or
one that is the result of a key agreement protocol, as returned by
<span class="apiname">javax.crypto.KeyAgreement.generateSecret()</span>,
or an instance of `javax.crypto.spec.SecretKeySpec`{.codeph}.

With some MAC algorithms, the (secret-)key algorithm associated with the
(secret-)key object used to initialize the Mac object does not matter
(this is the case with the HMAC-MD5 and HMAC-SHA1 implementations of the
`SunJCE`{.codeph} provider). With others, however, the (secret-)key
algorithm does matter, and an `InvalidKeyException`{.codeph} is thrown
if a (secret-)key object with an inappropriate (secret-)key algorithm is
used.

</div>
<!-- class="section" -->

<div class="section">
Computing a MAC

A MAC can be computed in one step (<span class="variable">single-part
operation</span>) or in multiple steps
(<span class="variable">multiple-part operation</span>). A multiple-part
operation is useful if you do not know in advance how long the data is
going to be, or if the data is too long to be stored in memory all at
once.

To compute the MAC of some data in a single step, call the following
<span class="apiname">doFinal</span> method:

``` {.codeblock dir="ltr"}
    public byte[] doFinal(byte[] input);
```

To compute the MAC of some data in multiple steps, call one of the
`update`{.codeph} methods:

``` {.codeblock dir="ltr"}
    public void update(byte input);

    public void update(byte[] input);

    public void update(byte[] input, int inputOffset, int inputLen);
```

A multiple-part operation must be terminated by the above
`doFinal`{.codeph} method (if there is still some input data left for
the last step), or by one of the following `doFinal`{.codeph} methods
(if there is no input data left for the last step):

``` {.codeblock dir="ltr"}
    public byte[] doFinal();

    public void doFinal(byte[] output, int outOffset);
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC}

### Key Interfaces {#JSSEC-GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC .sect3}

<div>
The `java.security.Key`{.codeph} interface is the top-level interface
for all opaque keys. It defines the functionality shared by all opaque
key objects.

To this point, we have focused the high-level uses of the JCA without
getting lost in the details of what keys are and how they are
generated/represented. It is now time to turn our attention to keys.

An <span class="variable">opaque</span> key representation is one in
which you have no direct access to the key material that constitutes a
key. In other words: \"opaque\" gives you limited access to the
key\--just the three methods defined by the `Key`{.codeph} interface
(see below): `getAlgorithm`{.codeph}, `getFormat`{.codeph}, and
`getEncoded`{.codeph}.

This is in contrast to a <span class="variable">transparent</span>
representation, in which you can access each key material value
individually, through one of the `get`{.codeph} methods defined in the
corresponding <span class="apiname">KeySpec</span> interface (see [The
KeySpec
Interface](java-cryptography-architecture-jca-reference-guide.html#GUID-CFF50556-89F9-4AB0-9EDE-D5763B900BFF "This interface contains no methods or constants. Its only purpose is to group and provide type safety for all key specifications. All key specifications must implement this interface.")).

All opaque keys have three characteristics:

[<!-- -->]{#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC__GUID-5B43C71A-CA72-4787-B3AE-F8FA11DF7866}<span class="bold">An Algorithm</span>

:   The key algorithm for that key. The key algorithm is usually an
    encryption or asymmetric operation algorithm (such as
    `AES`{.codeph}, `DSA`{.codeph} or `RSA`{.codeph}), which will work
    with those algorithms and with related algorithms (such as
    `SHA256withRSA`{.codeph}). The name of the algorithm of a key is
    obtained using this method:

    ``` {.codeblock dir="ltr"}
    String getAlgorithm()
    ```

[<!-- -->]{#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC__GUID-5D585F10-ECBA-4A07-AC3D-5C3ABA919A6A}<span class="bold">An Encoded Form</span>

:   The external encoded form for the key used when a standard
    representation of the key is needed outside the Java Virtual
    Machine, as when transmitting the key to some other party. The key
    is encoded according to a standard format (such as X.509 or PKCS8),
    and is returned using the method:

    ``` {.codeblock dir="ltr"}
    byte[] getEncoded()
    ```

[<!-- -->]{#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC__GUID-EC833FCD-5697-4E38-9933-6E336A126496}<span class="bold">A Format</span>

:   The name of the format of the encoded key. It is returned by the
    method:

    ``` {.codeblock dir="ltr"}
    String getFormat()
    ```

Keys are generally obtained through key generators such as the
<span class="apiname">KeyGenerator</span> class and the
<span class="apiname">KeyPairGenerator</span> class, certificates, key
specifications (see the [The KeySpec
Interface](java-cryptography-architecture-jca-reference-guide.html#GUID-CFF50556-89F9-4AB0-9EDE-D5763B900BFF "This interface contains no methods or constants. Its only purpose is to group and provide type safety for all key specifications. All key specifications must implement this interface."))
using a <span class="apiname">KeyFactory</span>, or a
<span class="apiname">Keystore</span> implementation accessing a
keystore database used to manage keys. It is possible to parse encoded
keys, in an algorithm-dependent manner, using a
<span class="apiname">KeyFactory</span>.

It is also possible to parse certificates, using a
<span class="apiname">CertificateFactory</span>.

Here is a list of interfaces which extend the `Key`{.codeph} interface
in the `java.security.interfaces`{.codeph} and
`javax.crypto.interfaces`{.codeph} packages:

-   [<span class="apiname">SecretKey</span>](https://docs.oracle.com/javase/10/docs/api/javax/crypto/SecretKey.html)
    -   [<span class="apiname">PBEKey</span>](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/PBEKey.html)
-   [<span class="apiname">PrivateKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/PrivateKey.html)
    -   [<span class="apiname">DHPrivateKey</span>](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHPrivateKey.html)
    -   [<span class="apiname">DSAPrivateKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAPrivateKey.html)
    -   [<span class="apiname">ECPrivateKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/ECPrivateKey.html)
    -   [<span class="apiname">RSAMultiPrimePrivateCrtKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAMultiPrimePrivateCrtKey.html)
    -   [<span class="apiname">RSAPrivateCrtKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPrivateCrtKey.html)
    -   [<span class="apiname">RSAPrivateKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPrivateKey.html)
-   [<span class="apiname">PublicKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/PublicKey.html)
    -   [<span class="apiname">DHPublicKey</span>](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHPublicKey.html)
    -   [<span class="apiname">DSAPublicKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAPublicKey.html)
    -   [<span class="apiname">ECPublicKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/ECPublicKey.html)
    -   [<span class="apiname">RSAPublicKey</span>](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPublicKey.html)

<div class="section">
The PublicKey and PrivateKey Interfaces

The `PublicKey`{.codeph} and `PrivateKey`{.codeph} interfaces (which
both extend the `Key`{.codeph} interface) are methodless interfaces,
used for type-safety and type-identification.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-9A793484-AE6A-4513-A603-BFEAE887DD8B}

### The KeyPair Class {#JSSEC-GUID-9A793484-AE6A-4513-A603-BFEAE887DD8B .sect3}

<div>
The `KeyPair`{.codeph} class is a simple holder for a key pair (a public
key and a private key).

<div class="section">
It has two public methods, one for returning the private key, and the
other for returning the public key:

``` {.codeblock dir="ltr"}
PrivateKey getPrivate()
PublicKey getPublic()
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-D1EA35A1-710A-4EBC-8ABB-10875411EBB0}

### Key Specification Interfaces and Classes {#JSSEC-GUID-D1EA35A1-710A-4EBC-8ABB-10875411EBB0 .sect3}

<div>
`Key`{.codeph} objects and key specifications (`KeySpec`{.codeph}s) are
two different representations of key data. `Cipher`{.codeph}s use
`Key`{.codeph} objects to initialize their encryption algorithms, but
keys may need to be converted into a more portable format for
transmission or storage.

<div class="section">
A <span class="variable">transparent</span> representation of keys means
that you can access each key material value individually, through one of
the `get`{.codeph} methods defined in the corresponding specification
class. For example, `DSAPrivateKeySpec`{.codeph} defines
`getX`{.codeph}, `getP`{.codeph}, `getQ`{.codeph}, and `getG`{.codeph}
methods, to access the private key `x`{.codeph}, and the DSA algorithm
parameters used to calculate the key: the prime `p`{.codeph}, the
sub-prime `q`{.codeph}, and the base `g`{.codeph}. If the key is stored
on a hardware device, its specification may contain information that
helps identify the key on the device.

This representation is contrasted with an
<span class="variable">opaque</span> representation, as defined by the
[Key
Interfaces](java-cryptography-architecture-jca-reference-guide.html#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC "The java.security.Key interface is the top-level interface for all opaque keys. It defines the functionality shared by all opaque key objects.")
interface, in which you have no direct access to the key material
fields. In other words, an \"opaque\" representation gives you limited
access to the key\--just the three methods defined by the `Key`{.codeph}
interface: `getAlgorithm`{.codeph}, `getFormat`{.codeph}, and
`getEncoded`{.codeph}.

A key may be specified in an algorithm-specific way, or in an
algorithm-independent encoding format (such as ASN.1). For example, a
DSA private key may be specified by its components `x`{.codeph},
`p`{.codeph}, `q`{.codeph}, and `g`{.codeph} (see
[`DSAPrivateKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/DSAPrivateKeySpec.html)),
or it may be specified using its DER encoding (see
[`PKCS8EncodedKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/PKCS8EncodedKeySpec.html)).

The [The KeyFactory
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-09C8DF67-7C78-453C-95B4-E7E7DEAD446A)
and [The SecretKeyFactory
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-5E8F4099-779F-4484-9A95-F1CEA167601A)
classes can be used to convert between opaque and transparent key
representations (that is, between `Key`{.codeph}s and
`KeySpec`{.codeph}s, assuming that the operation is possible. (For
example, private keys on smart cards might not be able leave the card.
Such `Key`{.codeph}s are not convertible.)

In the following sections, we discuss the key specification interfaces
and classes in the `java.security.spec`{.codeph} package.

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-CFF50556-89F9-4AB0-9EDE-D5763B900BFF}

#### The KeySpec Interface {#JSSEC-GUID-CFF50556-89F9-4AB0-9EDE-D5763B900BFF .sect4}

<div>
This interface contains no methods or constants. Its only purpose is to
group and provide type safety for all key specifications. All key
specifications must implement this interface.

</div>
</div>
<div class="sect4">
[]{#GUID-5DE3B786-8E76-4679-B66B-6B3EC098075E}

#### The KeySpec Subinterfaces {#JSSEC-GUID-5DE3B786-8E76-4679-B66B-6B3EC098075E .sect4}

<div>
Like the `Key`{.codeph} interface, there are a similar set of
`KeySpec`{.codeph} interfaces.

<div class="section">
-   [`SecretKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/SecretKeySpec.html)
-   [`EncodedKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/EncodedKeySpec.html)
    -   [`PKCS8EncodedKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/PKCS8EncodedKeySpec.html)
    -   [`X509EncodedKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/X509EncodedKeySpec.html)
-   [`DESKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/DESKeySpec.html)
-   [`DESedeKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/DESedeKeySpec.html)
-   [`PBEKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/PBEKeySpec.html)
-   [`DHPrivateKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/DHPrivateKeySpec.html)
-   [`DSAPrivateKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/DSAPrivateKeySpec.html)
-   [`ECPrivateKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/ECPrivateKeySpec.html)
-   [`RSAPrivateKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/RSAPrivateKeySpec.html)
    -   [`RSAMultiPrimePrivateCrtKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/RSAMultiPrimePrivateCrtKeySpec.html)
    -   [`RSAPrivateCrtKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/RSAPrivateCrtKeySpec.html)
-   [`DHPublicKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/DHPublicKeySpec.html)
-   [`DSAPublicKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/DSAPublicKeySpec.html)
-   [`ECPublicKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/ECPublicKeySpec.html)
-   [`RSAPublicKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/RSAPublicKeySpec.html)

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-8EAA36B1-5CD8-40FC-944E-099C71E716B4}

#### The EncodedKeySpec Class {#JSSEC-GUID-8EAA36B1-5CD8-40FC-944E-099C71E716B4 .sect4}

<div>
<div class="section">
This abstract class (which implements the [The KeySpec
Interface](java-cryptography-architecture-jca-reference-guide.html#GUID-CFF50556-89F9-4AB0-9EDE-D5763B900BFF "This interface contains no methods or constants. Its only purpose is to group and provide type safety for all key specifications. All key specifications must implement this interface.")
interface) represents a public or private key in encoded format. Its
<span class="apiname">getEncoded</span> method returns the encoded key:

``` {.codeblock dir="ltr"}
abstract byte[] getEncoded();
```

and its <span class="apiname">getFormat</span> method returns the name
of the encoding format:

``` {.codeblock dir="ltr"}
abstract String getFormat();
```

See the next sections for the concrete implementations
`PKCS8EncodedKeySpec`{.codeph} and `X509EncodedKeySpec`{.codeph}.

</div>
<!-- class="section" -->

</div>
<div class="sect5">
[]{#GUID-7E6373D0-273A-4C5C-B3EB-14ABBE6B759E}

##### The PKCS8EncodedKeySpec Class {#JSSEC-GUID-7E6373D0-273A-4C5C-B3EB-14ABBE6B759E .sect5}

<div>
This class, which is a subclass of `EncodedKeySpec`{.codeph}, represents
the DER encoding of a private key, according to the format specified in
the PKCS8 standard.

<div class="section">
Its <span class="apiname">getEncoded</span> method returns the key
bytes, encoded according to the PKCS8 standard. Its
<span class="apiname">getFormat</span> method returns the string
\"PKCS\#8\".

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect5">
[]{#GUID-F41053CD-D1F3-4BAE-B97D-72C53A9892DC}

##### The X509EncodedKeySpec Class {#JSSEC-GUID-F41053CD-D1F3-4BAE-B97D-72C53A9892DC .sect5}

<div>
This class, which is a subclass of `EncodedKeySpec`{.codeph}, represents
the DER encoding of a public key, according to the format specified in
the X.509 standard.

<div class="section">
Its `getEncoded`{.codeph} method returns the key bytes, encoded
according to the X.509 standard. Its `getFormat`{.codeph} method returns
the string \"X.509\".

</div>
<!-- class="section" -->

</div>
</div>
</div>
</div>
<div class="sect3">
[]{#GUID-D4A4B706-6C4F-436D-B5ED-A29C98260578}

### Generators and Factories {#JSSEC-GUID-D4A4B706-6C4F-436D-B5ED-A29C98260578 .sect3}

<div>
Newcomers to Java and the JCA APIs in particular sometimes do not grasp
the distinction between generators and factories.

<div class="figure" id="GUID-D4A4B706-6C4F-436D-B5ED-A29C98260578__GUID-39757065-9091-43DE-8CEC-C1E00A75DF36">
Figure 2-10 Generators and Factories

![Description of Figure 2-10
follows](img/genrator-factory.gif "Description of Figure 2-10 follows")\
[Description of \"Figure 2-10 Generators and
Factories\"](img_text/genrator-factory.htm)

</div>
<!-- class="figure" -->

Generators are used to <span class="bold">generate brand new
objects</span>. Generators can be initialized in either an
algorithm-dependent or algorithm-independent way. For example, to create
a Diffie-Hellman (DH) keypair, an application could specify the
necessary P and G values, or the generator could simply be initialized
with the appropriate key length, and the generator will select
appropriate P and G values. In both cases, the generator will produce
brand new keys based on the parameters.

On the other hand, factories are used to <span class="bold">convert data
from one existing object type to another</span>. For example, an
application might have available the components of a DH private key and
can package them as a [The KeySpec
Interface](java-cryptography-architecture-jca-reference-guide.html#GUID-CFF50556-89F9-4AB0-9EDE-D5763B900BFF "This interface contains no methods or constants. Its only purpose is to group and provide type safety for all key specifications. All key specifications must implement this interface."),
but needs to convert them into a
[PrivateKey](java-cryptography-architecture-jca-reference-guide.html#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC "The java.security.Key interface is the top-level interface for all opaque keys. It defines the functionality shared by all opaque key objects.")
object that can be used by a `KeyAgreement`{.codeph} object, or
vice-versa. Or they might have the byte array of a certificate, but need
to use a `CertificateFactory`{.codeph} to convert it into a
`X509Certificate`{.codeph} object. Applications use factory objects to
do the conversion.

</div>
<div class="sect4">
[]{#GUID-09C8DF67-7C78-453C-95B4-E7E7DEAD446A}

#### The KeyFactory Class {#JSSEC-GUID-09C8DF67-7C78-453C-95B4-E7E7DEAD446A .sect4}

<div>
<div class="section">
The `KeyFactory`{.codeph} class is an [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.")
designed to perform conversions between opaque cryptographic [Key
Interfaces](java-cryptography-architecture-jca-reference-guide.html#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC "The java.security.Key interface is the top-level interface for all opaque keys. It defines the functionality shared by all opaque key objects.")
and [Key Specification Interfaces and
Classes](java-cryptography-architecture-jca-reference-guide.html#GUID-D1EA35A1-710A-4EBC-8ABB-10875411EBB0 "Key objects and key specifications (KeySpecs) are two different representations of key data. Ciphers use Key objects to initialize their encryption algorithms, but keys may need to be converted into a more portable format for transmission or storage.")
(transparent representations of the underlying key material).

<div class="figure" id="GUID-09C8DF67-7C78-453C-95B4-E7E7DEAD446A__GUID-A3F628B1-EA36-4F80-9FB3-18565C99D33D">
Figure 2-11 KeyFactory Class

![Description of Figure 2-11
follows](img/keyfactory.gif "Description of Figure 2-11 follows")\
[Description of \"Figure 2-11 KeyFactory
Class\"](img_text/keyfactory.htm)

</div>
<!-- class="figure" -->

Key factories are bi-directional. They allow you to build an opaque key
object from a given key specification (key material), or to retrieve the
underlying key material of a key object in a suitable format.

Multiple compatible key specifications can exist for the same key. For
example, a DSA public key may be specified by its components
`y`{.codeph}, `p`{.codeph}, `q`{.codeph}, and `g`{.codeph} (see
`java.security.spec.DSAPublicKeySpec`{.codeph}), or it may be specified
using its DER encoding according to the X.509 standard (see [The
X509EncodedKeySpec
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-F41053CD-D1F3-4BAE-B97D-72C53A9892DC "This class, which is a subclass of EncodedKeySpec, represents the DER encoding of a public key, according to the format specified in the X.509 standard.")).

A key factory can be used to translate between compatible key
specifications. Key parsing can be achieved through translation between
compatible key specifications, e.g., when you translate from
`X509EncodedKeySpec`{.codeph} to `DSAPublicKeySpec`{.codeph}, you
basically parse the encoded key into its components. For an example, see
the end of the [Generating/Verifying Signatures Using Key Specifications
and
KeyFactory](java-cryptography-architecture-jca-reference-guide.html#GUID-5514BAFF-5F0F-403C-9943-56A632D6E406 "Sample code that is used to generate and verify signatures using key specifications and KeyFactory.")
section.

</div>
<!-- class="section" -->

<div class="section">
Creating a KeyFactory Object

`KeyFactory`{.codeph} objects are obtained by using one of the
`KeyFactory`{.codeph}getInstance() static factory methods. See [How
Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Converting Between a Key Specification and a Key Object

If you have a key specification for a public key, you can obtain an
opaque `PublicKey`{.codeph} object from the specification by using the
`generatePublic`{.codeph} method:

``` {.codeblock dir="ltr"}
PublicKey generatePublic(KeySpec keySpec)
```

Similarly, if you have a key specification for a private key, you can
obtain an opaque `PrivateKey`{.codeph} object from the specification by
using the `generatePrivate`{.codeph} method:

``` {.codeblock dir="ltr"}
PrivateKey generatePrivate(KeySpec keySpec)
```

</div>
<!-- class="section" -->

<div class="section">
Converting Between a Key Object and a Key Specification

If you have a `Key`{.codeph} object, you can get a corresponding key
specification object by calling the `getKeySpec`{.codeph} method:

``` {.codeblock dir="ltr"}
KeySpec getKeySpec(Key key, Class keySpec)
```

`keySpec`{.codeph} identifies the specification class in which the key
material should be returned. It could, for example, be
`DSAPublicKeySpec.class`{.codeph} , to indicate that the key material
should be returned in an instance of the `DSAPublicKeySpec`{.codeph}
class. See [Generating/Verifying Signatures Using Key Specifications and
KeyFactory](java-cryptography-architecture-jca-reference-guide.html#GUID-5514BAFF-5F0F-403C-9943-56A632D6E406 "Sample code that is used to generate and verify signatures using key specifications and KeyFactory.").

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-5E8F4099-779F-4484-9A95-F1CEA167601A}

#### The SecretKeyFactory Class {#JSSEC-GUID-5E8F4099-779F-4484-9A95-F1CEA167601A .sect4}

<div>
<div class="section">
The `SecretKeyFactory`{.codeph} class represents a factory for secret
keys. Unlike the <span class="apiname">KeyFactory</span> class (see [The
KeyFactory
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-09C8DF67-7C78-453C-95B4-E7E7DEAD446A)),
a `javax.crypto.SecretKeyFactory`{.codeph} object operates only on
secret (symmetric) keys, whereas a `java.security.KeyFactory`{.codeph}
object processes the public and private key components of a key pair.

<div class="figure" id="GUID-5E8F4099-779F-4484-9A95-F1CEA167601A__GUID-B147D33F-7429-4584-82BD-71838EA98DE1">
Figure 2-12 SecretKeyFactory Class

![Description of Figure 2-12
follows](img/secretkeyfactory.png "Description of Figure 2-12 follows")\
[Description of \"Figure 2-12 SecretKeyFactory
Class\"](img_text/secretkeyfactory.htm)

</div>
<!-- class="figure" -->

Key factories are used to convert [Key
Interfaces](java-cryptography-architecture-jca-reference-guide.html#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC "The java.security.Key interface is the top-level interface for all opaque keys. It defines the functionality shared by all opaque key objects.")
(opaque cryptographic keys of type `java.security.Key`{.codeph}) into
[Key Specification Interfaces and
Classes](java-cryptography-architecture-jca-reference-guide.html#GUID-D1EA35A1-710A-4EBC-8ABB-10875411EBB0 "Key objects and key specifications (KeySpecs) are two different representations of key data. Ciphers use Key objects to initialize their encryption algorithms, but keys may need to be converted into a more portable format for transmission or storage.")
(transparent representations of the underlying key material in a
suitable format), and vice versa.

Objects of type `java.security.Key`{.codeph}, of which
`java.security.PublicKey`{.codeph}, `java.security.PrivateKey`{.codeph},
and `javax.crypto.SecretKey`{.codeph} are subclasses, are opaque key
objects, because you cannot tell how they are implemented. The
underlying implementation is provider-dependent, and may be software or
hardware based. Key factories allow providers to supply their own
implementations of cryptographic keys.

For example, if you have a key specification for a Diffie-Hellman public
key, consisting of the public value `y`{.codeph}, the prime modulus
`p`{.codeph}, and the base `g`{.codeph}, and you feed the same
specification to Diffie-Hellman key factories from different providers,
the resulting `PublicKey`{.codeph} objects will most likely have
different underlying implementations.

A provider should document the key specifications supported by its
secret key factory. For example, the `SecretKeyFactory`{.codeph} for DES
keys supplied by the `SunJCE`{.codeph} provider supports
`DESKeySpec`{.codeph} as a transparent representation of DES keys, the
`SecretKeyFactory`{.codeph} for DES-EDE keys supports
`DESedeKeySpec`{.codeph} as a transparent representation of DES-EDE
keys, and the `SecretKeyFactory`{.codeph} for PBE supports
`PBEKeySpec`{.codeph} as a transparent representation of the underlying
password.

The following is an example of how to use a `SecretKeyFactory`{.codeph}
to convert secret key data into a `SecretKey`{.codeph} object, which can
be used for a subsequent `Cipher`{.codeph} operation:

``` {.codeblock dir="ltr"}
    // Note the following bytes are not realistic secret key data
    // bytes but are simply supplied as an illustration of using data
    // bytes (key material) you already have to build a DESedeKeySpec.

    byte[] desEdeKeyData = getKeyData();
    DESedeKeySpec desEdeKeySpec = new DESedeKeySpec(desEdeKeyData);
    SecretKeyFactory keyFactory = SecretKeyFactory.getInstance("DESede");
    SecretKey secretKey = keyFactory.generateSecret(desEdeKeySpec);
```

In this case, the underlying implementation of `SecretKey`{.codeph} is
based on the provider of `KeyFactory`{.codeph}.

An alternative, provider-independent way of creating a functionally
equivalent `SecretKey`{.codeph} object from the same key material is to
use the `javax.crypto.spec.SecretKeySpec`{.codeph} class, which
implements the `javax.crypto.SecretKey`{.codeph} interface:

``` {.codeblock dir="ltr"}
    byte[] aesKeyData = getKeyData();
    SecretKeySpec secretKey = new SecretKeySpec(aesKeyData, "AES");
```

</div>
<!-- class="section" -->

<div class="section">
Creating a SecretKeyFactory Object

<span class="apiname">SecretKeyFactory</span> objects are obtained by
using one of the <span class="apiname">SecretKeyFactory</span>
<span class="apiname">getInstance()</span> static factory methods. See
[How Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Converting Between a Key Specification and a Secret Key Object

If you have a key specification for a secret key, you can obtain an
opaque <span class="apiname">SecretKey</span> object from the
specification by using the <span class="apiname">generateSecret</span>
method:

``` {.oac_no_warn dir="ltr"}
SecretKey generateSecret(KeySpec keySpec)
```

</div>
<!-- class="section" -->

<div class="section">
Converting Between a Secret Key Object and a Key Specification

If you have a <span class="apiname">SecretKey</span> object, you can get
a corresponding key specification object by calling the
<span class="apiname">getKeySpec</span> method:

``` {.oac_no_warn dir="ltr"}
KeySpec getKeySpec(Key key, Class keySpec)
```

<span class="apiname">keySpec</span> identifies the specification class
in which the key material should be returned. It could, for example,
be` DESKeySpec.class`{.codeph}, to indicate that the key material should
be returned in an instance of the
<span class="apiname">DESKeySpec</span> class.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-7EA29AC2-28B5-405D-BD2F-7055EC9E1EDD}

#### The KeyPairGenerator Class {#JSSEC-GUID-7EA29AC2-28B5-405D-BD2F-7055EC9E1EDD .sect4}

<div>
<div class="section">
The `KeyPairGenerator`{.codeph} class is an engine class (see [Engine
Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider."))
used to generate pairs of public and private keys.

<div class="figure" id="GUID-7EA29AC2-28B5-405D-BD2F-7055EC9E1EDD__GUID-3DB89ACB-BF5C-4155-B2BF-E3ED4BEACE8D">
Figure 2-13 KeyPairGenerator Class

![Description of Figure 2-13
follows](img/keypairgenerator.gif "Description of Figure 2-13 follows")\
[Description of \"Figure 2-13 KeyPairGenerator
Class\"](img_text/keypairgenerator.htm)

</div>
<!-- class="figure" -->

There are two ways to generate a key pair: in an algorithm-independent
manner, and in an algorithm-specific manner. The only difference between
the two is the initialization of the object.

See [Generating a Pair of
Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-ED6EDA78-8D20-4059-92E1-FBDDE4D3DFE6 "In this example we will generate a public-private key pair for the algorithm named ")
for examples of calls to the methods documented below.

</div>
<!-- class="section" -->

<div class="section">
Creating a KeyPairGenerator

All key pair generation starts with a `KeyPairGenerator`{.codeph}.
`KeyPairGenerator`{.codeph} objects are obtained by using one of the
`KeyPairGenerator`{.codeph} <span class="apiname">getInstance()</span>
static factory methods. See [How Provider Implementations Are Requested
and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Initializing a KeyPairGenerator

A key pair generator for a particular algorithm creates a public/private
key pair that can be used with this algorithm. It also associates
algorithm-specific parameters with each of the generated keys.

A key pair generator needs to be initialized before it can generate
keys. In most cases, algorithm-independent initialization is sufficient.
But in other cases, algorithm-specific initialization can be used.

</div>
<!-- class="section" -->

<div class="section">
Algorithm-Independent Initialization

All key pair generators share the concepts of a keysize and a source of
randomness. The keysize is interpreted differently for different
algorithms. For example, in the case of the DSA algorithm, the keysize
corresponds to the length of the modulus. (See [Java Security Standard
Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
for information about the keysizes for specific algorithms.)

An `initialize`{.codeph} method takes two universally shared types of
arguments:

``` {.codeblock dir="ltr"}
void initialize(int keysize, SecureRandom random)
```

Another `initialize`{.codeph} method takes only a `keysize`{.codeph}
argument; it uses a system-provided source of randomness:

``` {.codeblock dir="ltr"}
void initialize(int keysize)
```

Since no other parameters are specified when you call the above
algorithm-independent `initialize`{.codeph} methods, it is up to the
provider what to do about the algorithm-specific parameters (if any) to
be associated with each of the keys.

If the algorithm is a \"DSA\" algorithm, and the modulus size (keysize)
is 512, 768, 1024, 2048, or 3072, then the `SUN`{.codeph} provider uses
a set of precomputed values for the `p`{.codeph}, `q`{.codeph}, and
`g`{.codeph} parameters. If the modulus size is not one of the above
values, the `SUN`{.codeph} provider creates a new set of parameters.
Other providers might have precomputed parameter sets for more than just
the three modulus sizes mentioned above. Still others might not have a
list of precomputed parameters at all and instead always create new
parameter sets.

</div>
<!-- class="section" -->

<div class="section">
Algorithm-Specific Initialization

For situations where a set of algorithm-specific parameters already
exists (such as \"community parameters\" in DSA), there are two
`initialize`{.codeph} methods that have an [The AlgorithmParameterSpec
Interface](java-cryptography-architecture-jca-reference-guide.html#GUID-190C91B4-991D-416E-A932-C0E37B33A86D "AlgorithmParameterSpec is an interface to a transparent specification of cryptographic parameters. This interface contains no methods or constants. Its only purpose is to group (and provide type safety for) all parameter specifications. All parameter specifications must implement this interface.")
argument. One also has a `SecureRandom`{.codeph} argument, while the
source of randomness is system-provided for the other:

``` {.codeblock dir="ltr"}
void initialize(AlgorithmParameterSpec params,
                SecureRandom random)

void initialize(AlgorithmParameterSpec params)
```

See [Generating a Pair of
Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-ED6EDA78-8D20-4059-92E1-FBDDE4D3DFE6 "In this example we will generate a public-private key pair for the algorithm named ").

</div>
<!-- class="section" -->

<div class="section">
Generating a Key Pair

The procedure for generating a key pair is always the same, regardless
of initialization (and of the algorithm). You always call the following
method from `KeyPairGenerator`{.codeph}:

``` {.codeblock dir="ltr"}
KeyPair generateKeyPair()
```

Multiple calls to `generateKeyPair`{.codeph} will yield different key
pairs.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-F178CBC3-D25F-48B6-9F2F-ABB586E713A1}

#### The KeyGenerator Class {#JSSEC-GUID-F178CBC3-D25F-48B6-9F2F-ABB586E713A1 .sect4}

<div>
A key generator is used to generate secret keys for symmetric
algorithms.

<div class="section">
<div class="figure" id="GUID-F178CBC3-D25F-48B6-9F2F-ABB586E713A1__GUID-E128C2F7-1771-4798-AD6F-023E341AE627">
Figure 2-14 The KeyGenerator Class

![Description of Figure 2-14
follows](img/keygenerator.gif "Description of Figure 2-14 follows")\
[Description of \"Figure 2-14 The KeyGenerator
Class\"](img_text/keygenerator.htm)

</div>
<!-- class="figure" -->

</div>
<!-- class="section" -->

<div class="section">
Creating a `KeyGenerator`{.codeph}

`KeyGenerator`{.codeph} objects are obtained by using one of the
`KeyGenerator`{.codeph} <span class="apiname">getInstance()</span>
static factory methods. See [How Provider Implementations Are Requested
and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Initializing a KeyGenerator Object

A key generator for a particular symmetric-key algorithm creates a
symmetric key that can be used with that algorithm. It also associates
algorithm-specific parameters (if any) with the generated key.

There are two ways to generate a key: in an algorithm-independent
manner, and in an algorithm-specific manner. The only difference between
the two is the initialization of the object:

-   <span class="bold">Algorithm-Independent Initialization</span>

    All key generators share the concepts of a
    <span class="variable">keysize</span> and a
    <span class="variable">source of randomness</span>. There is an
    `init`{.codeph} method that takes these two universally shared types
    of arguments. There is also one that takes just a `keysize`{.codeph}
    argument, and uses a system-provided source of randomness, and one
    that takes just a source of randomness:

    ``` {.codeblock dir="ltr"}

        public void init(SecureRandom random);

        public void init(int keysize);

        public void init(int keysize, SecureRandom random);
    ```

    Since no other parameters are specified when you call the above
    algorithm-independent `init`{.codeph} methods, it is up to the
    provider what to do about the algorithm-specific parameters (if any)
    to be associated with the generated key.

-   <span class="bold">Algorithm-Specific Initialization</span>

    For situations where a set of algorithm-specific parameters already
    exists, there are two `init`{.codeph} methods that have an
    `AlgorithmParameterSpec`{.codeph} argument. One also has a
    `SecureRandom`{.codeph} argument, while the source of randomness is
    system-provided for the other:

    ``` {.codeblock dir="ltr"}
        public void init(AlgorithmParameterSpec params);

        public void init(AlgorithmParameterSpec params, SecureRandom random);
    ```

In case the client does not explicitly initialize the KeyGenerator (via
a call to an `init`{.codeph} method), each provider must supply (and
document) a default initialization.

</div>
<!-- class="section" -->

<div class="section">
Creating a Key

The following method generates a secret key:

``` {.codeblock dir="ltr"}
    public SecretKey generateKey();
```

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-C4D8A5D0-ECA7-4686-A8F0-636115500C31}

### The KeyAgreement Class {#JSSEC-GUID-C4D8A5D0-ECA7-4686-A8F0-636115500C31 .sect3}

<div>
Key agreement is a protocol by which 2 or more parties can establish the
same cryptographic keys, without having to exchange any secret
information.

<div class="section">
<div class="figure" id="GUID-C4D8A5D0-ECA7-4686-A8F0-636115500C31__GUID-98958A82-0755-47FC-9ABD-EF5482B7C7E7">
Figure 2-15 The KeyAgreement Class

![Description of Figure 2-15
follows](img/keyagreement.gif "Description of Figure 2-15 follows")\
[Description of \"Figure 2-15 The KeyAgreement
Class\"](img_text/keyagreement.htm)

</div>
<!-- class="figure" -->

Each party initializes their key agreement object with their private
key, and then enters the public keys for each party that will
participate in the communication. In most cases, there are just two
parties, but algorithms such as Diffie-Hellman allow for multiple
parties (3 or more) to participate. When all the public keys have been
entered, each `KeyAgreement`{.codeph} object will generate (agree upon)
the same key.

The KeyAgreement class provides the functionality of a key agreement
protocol. The keys involved in establishing a shared secret are created
by one of the key generators (`KeyPairGenerator`{.codeph} or
`KeyGenerator`{.codeph}), a `KeyFactory`{.codeph}, or as a result from
an intermediate phase of the key agreement protocol.

</div>
<!-- class="section" -->

<div class="section">
Creating a KeyAgreement Object

Each party involved in the key agreement has to create a KeyAgreement
object. `KeyAgreement`{.codeph} objects are obtained by using one of the
`KeyAgreement`{.codeph} <span class="apiname">getInstance()</span>
static factory methods. See [How Provider Implementations Are Requested
and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Initializing a KeyAgreement Object

You initialize a KeyAgreement object with your private information. In
the case of Diffie-Hellman, you initialize it with your Diffie-Hellman
private key. Additional initialization information may contain a source
of randomness and/or a set of algorithm parameters. Note that if the
requested key agreement algorithm requires the specification of
algorithm parameters, and only a key, but no parameters are provided to
initialize the KeyAgreement object, the key must contain the required
algorithm parameters. (For example, the Diffie-Hellman algorithm uses a
prime modulus `p`{.codeph} and a base generator `g`{.codeph} as its
parameters.)

To initialize a KeyAgreement object, call one of its `init`{.codeph}
methods:

``` {.codeblock dir="ltr"}
    public void init(Key key);

    public void init(Key key, SecureRandom random);

    public void init(Key key, AlgorithmParameterSpec params);

    public void init(Key key, AlgorithmParameterSpec params,
                     SecureRandom random);
```

</div>
<!-- class="section" -->

<div class="section">
Executing a KeyAgreement Phase

Every key agreement protocol consists of a number of phases that need to
be executed by each party involved in the key agreement.

To execute the next phase in the key agreement, call the
<span class="apiname">doPhase</span> method:

``` {.codeblock dir="ltr"}
    public Key doPhase(Key key, boolean lastPhase);
```

The `key`{.codeph} parameter contains the key to be processed by that
phase. In most cases, this is the public key of one of the other parties
involved in the key agreement, or an intermediate key that was generated
by a previous phase. `doPhase`{.codeph} may return an intermediate key
that you may have to send to the other parties of this key agreement, so
they can process it in a subsequent phase.

The `lastPhase`{.codeph} parameter specifies whether or not the phase to
be executed is the last one in the key agreement: A value of
`FALSE`{.codeph} indicates that this is not the last phase of the key
agreement (there are more phases to follow), and a value of
`TRUE`{.codeph} indicates that this is the last phase of the key
agreement and the key agreement is completed, i.e.,
`generateSecret`{.codeph} can be called next.

In the example of [Diffie-Hellman Key Exchange between 2
Parties](java-cryptography-architecture-jca-reference-guide.html#GUID-98B5A57E-E5BA-46F2-BE35-2056F43C58A4 "The program runs the Diffie-Hellman key agreement protocol between 2 parties.")
, you call `doPhase`{.codeph} once, with `lastPhase`{.codeph} set to
`TRUE`{.codeph}. In the example of Diffie-Hellman between three parties,
you call `doPhase`{.codeph} twice: the first time with
`lastPhase`{.codeph} set to `FALSE`{.codeph}, the 2nd time with
`lastPhase`{.codeph} set to `TRUE`{.codeph}.

</div>
<!-- class="section" -->

<div class="section">
Generating the Shared Secret

After each party has executed all the required key agreement phases, it
can compute the shared secret by calling one of the
<span class="apiname">generateSecret</span> methods:

``` {.codeblock dir="ltr"}
    public byte[] generateSecret();

    public int generateSecret(byte[] sharedSecret, int offset);

    public SecretKey generateSecret(String algorithm);
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-AB51DEFD-5238-4F96-967F-082F6D34FBEA}

### Key Management {#JSSEC-GUID-AB51DEFD-5238-4F96-967F-082F6D34FBEA .sect3}

<div>
A database called a \"keystore\" can be used to manage a repository of
keys and certificates. (A <span class="variable">certificate</span> is a
digitally signed statement from one entity, saying that the public key
of some other entity has a particular value.)

<div class="section" id="GUID-AB51DEFD-5238-4F96-967F-082F6D34FBEA__KEYSTORELOCATION-86EBB624">
Keystore Location

The user keystore is by default stored in a file named
`.keystore`{.codeph} in the user\'s home directory, as determined by the
`user.home`{.codeph} system property whose default value depends on the
operating system:

-   Solaris, Linux, and MacOS: `/home/username/`{.codeph}
-   Windows: `C:\Users\username\`{.codeph}

Of course, keystore files can be located as desired. In some
environments, it may make sense for multiple keystores to exist. For
example, one keystore might hold a user\'s private keys, and another
might hold certificates used to establish trust relationships.

In addition to the user\'s keystore, the JDK also maintains a
system-wide keystore which is used to store trusted certificates from a
variety of Certificate Authorities (CA\'s). These CA certificates can be
used to help make trust decisions. For example, in SSL/TLS/DTLS when the
`SunJSSE`{.codeph} provider is presented with certificates from a remote
peer, the default trustmanager will consult one of the following files
to determine if the connection is to be trusted:

-   Solaris, Linux, and MacOS:
    `<java-home>/lib/security/cacerts`{.codeph}
-   Windows: `<java-home>\lib\security\cacerts`{.codeph}

Instead of using the system-wide `cacerts`{.codeph} keystore,
applications can set up and use their own keystores, or even use the
user keystore described above.

</div>
<!-- class="section" -->

<div class="section" id="GUID-AB51DEFD-5238-4F96-967F-082F6D34FBEA__KEYSTOREIMPLEMENTATION-86EBBA97">
Keystore Implementation

The `KeyStore`{.codeph} class supplies well-defined interfaces to access
and modify the information in a keystore. It is possible for there to be
multiple different concrete implementations, where each implementation
is that for a particular <span class="variable">type</span> of keystore.

Currently, there are two command-line tools that make use of
`KeyStore`{.codeph}: <span class="bold">`keytool`{.codeph}</span> and
<span class="bold">`jarsigner`{.codeph}</span>, and also a GUI-based
tool named <span class="bold">`policytool`{.codeph}</span>. It is also
used by the `Policy`{.codeph} reference implementation when it processes
policy files specifying the permissions (allowed accesses to system
resources) to be granted to code from various sources. Since
`KeyStore`{.codeph} is publicly available, JDK users can write
additional security applications that use it.

Applications can choose different <span class="variable">types</span> of
keystore implementations from different providers, using the
`getInstance`{.codeph} factory method in the `KeyStore`{.codeph} class.
A keystore type defines the storage and data format of the keystore
information, and the algorithms used to protect private keys in the
keystore and the integrity of the keystore itself. Keystore
implementations of different types are not compatible.

The default keystore implementation is \"pkcs12\". This is a
cross-platform keystore based on the RSA PKCS12 Personal Information
Exchange Syntax Standard. This standard is primarily meant for storing
or transporting a user\'s private keys, certificates, and miscellaneous
secrets. Arbitrary attributes can be associated with individual entries
in a PKCS12 keystore.

``` {.codeblock dir="ltr"}
    keystore.type=pkcs12
```

To have tools and other applications use a different default keystore
implementation, you can change that line to specify a different type.

Some applications, such as `keytool`{.codeph}, also let you override the
default keystore type (via the `-storetype`{.codeph} command-line
parameter).

<div class="infoboxnote" id="GUID-AB51DEFD-5238-4F96-967F-082F6D34FBEA__GUID-AFAA8199-86D1-45F8-B282-F34CAEFAA44A">
Note:

Keystore type designations are case-insensitive. For example, \"jks\"
would be considered the same as \"JKS\".

</div>
PKCS12 is the default and recommened keystore type. However, there are
three other types of keystores that come with the JDK implementation.

1.  <span class="bold">\"jceks\"</span> is an alternate proprietary
    keystore format to \"jks\" that uses Password-Based Encryption with
    Triple-DES.

    The \"jceks\" implementation can parse and convert a \"jks\"
    keystore file to the \"jceks\" format. You may upgrade your keystore
    of type \"jks\" to a keystore of type \"jceks\" by changing the
    password of a private-key entry in your keystore and specifying
    `"-storetype jceks"`{.codeph} as the keystore type. To apply the
    cryptographically strong(er) key protection supplied to a private
    key named \"signkey\" in your default keystore, use the following
    command, which will prompt you for the old and new key passwords:

    ``` {.codeblock dir="ltr"}
        keytool -keypass -alias signkey -storetype jceks
    ```

    See [keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549)
    in <span><cite>Java Platform, Standard Edition Tools
    Reference</cite></span> .

2.  <span class="bold">\"jks\"</span> is another option. It implements
    the keystore as a file, utilizing a proprietary keystore type
    (format). It protects each private key with its own individual
    password, and also protects the integrity of the entire keystore
    with a (possibly different) password.
3.  <span class="bold">\"dks\"</span> is a domain keystore. It is a
    collection of keystores presented as a single logical keystore. The
    keystores that comprise a given domain are specified by
    configuration data whose syntax is described in
    [`DomainLoadStoreParameter`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/DomainLoadStoreParameter.html).

Keystore implementations are provider-based. If you want to write your
own KeyStore implementations, see [How to Implement a Provider in the
Java Cryptography
Architecture](howtoimplaprovider.html#GUID-C485394F-08C9-4D35-A245-1B82CDDBC031 "This document describes what you need to do in order to integrate your provider into Java SE so that algorithms and other services can be found when Java Security API clients request them.").

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-09050137-31F1-468A-A552-B051A4E35876}

#### The KeyStore Class {#JSSEC-GUID-09050137-31F1-468A-A552-B051A4E35876 .sect4}

<div>
The `KeyStore`{.codeph} class supplies well-defined interfaces to access
and modify the information in a keystore.

<div class="section">
The `KeyStore`{.codeph} class is an [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.").

<div class="figure" id="GUID-09050137-31F1-468A-A552-B051A4E35876__GUID-E500AFDF-303F-4F6A-8F30-B78446C385BC">
Figure 2-16 KeyStore Class

![Description of Figure 2-16
follows](img/keystore.png "Description of Figure 2-16 follows")\
[Description of \"Figure 2-16 KeyStore Class\"](img_text/keystore.htm)

</div>
<!-- class="figure" -->

This class represents an in-memory collection of keys and certificates.
`KeyStore`{.codeph} manages two types of entries:

-   <span class="bold">Key Entry</span>: This type of keystore entry
    holds very sensitive cryptographic key information, which must be
    protected from unauthorized access. Typically, a key stored in this
    type of entry is a secret key, or a private key accompanied by the
    certificate chain authenticating the corresponding public key.

    Private keys and certificate chains are used by a given entity for
    self-authentication using digital signatures. For example, software
    distribution organizations digitally sign JAR files as part of
    releasing and/or licensing software.

-   <span class="bold">Trusted Certificate Entry</span>: This type of
    entry contains a single public key certificate belonging to another
    party. It is called a <span class="variable">trusted
    certificate</span> because the keystore owner trusts that the public
    key in the certificate indeed belongs to the identity identified by
    the <span class="variable">subject</span> (owner) of the
    certificate.

    This type of entry can be used to authenticate other parties.

Each entry in a keystore is identified by an \"alias\" string. In the
case of private keys and their associated certificate chains, these
strings distinguish among the different ways in which the entity may
authenticate itself. For example, the entity may authenticate itself
using different certificate authorities, or using different public key
algorithms.

Whether keystores are persistent, and the mechanisms used by the
keystore if it is persistent, are not specified here. This convention
allows use of a variety of techniques for protecting sensitive (e.g.,
private or secret) keys. Smart cards or other integrated cryptographic
engines (SafeKeyper) are one option, and simpler mechanisms such as
files may also be used (in a variety of formats).

The main `KeyStore`{.codeph} methods are described below.

</div>
<!-- class="section" -->

<div class="section">
Creating a KeyStore Object

KeyStore objects are obtained by using one of the KeyStore getInstance()
method. See [How Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Loading a Particular Keystore into Memory

Before a `KeyStore`{.codeph} object can be used, the actual keystore
data must be loaded into memory via the
<span class="apiname">load</span> method:

``` {.codeblock dir="ltr"}
final void load(InputStream stream, char[] password)
```

The optional password is used to check the integrity of the keystore
data. If no password is supplied, no integrity check is performed.

To create an empty keystore, you pass `null`{.codeph} as the
`InputStream`{.codeph} argument to the <span class="apiname">load</span>
method.

A DKS keystore is loaded by passing a
[`DomainLoadStoreParameter`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/DomainLoadStoreParameter.html)
to the alternative load method:

``` {.codeblock dir="ltr"}
final void load(KeyStore.LoadStoreParameter param)
```

</div>
<!-- class="section" -->

<div class="section">
Getting a List of the Keystore Aliases

All keystore entries are accessed via unique
<span class="variable">aliases</span>. The `aliases`{.codeph} method
returns an enumeration of the alias names in the keystore:

``` {.codeblock dir="ltr"}
final Enumeration aliases()
```

</div>
<!-- class="section" -->

<div class="section">
Determining Keystore Entry Types

As stated in the KeyStore class, there are two different types of
entries in a keystore. The following methods determine whether the entry
specified by the given alias is a key/certificate or a trusted
certificate entry, respectively:

``` {.codeblock dir="ltr"}
final boolean isKeyEntry(String alias)
final boolean isCertificateEntry(String alias)
```

</div>
<!-- class="section" -->

<div class="section">
Adding/Setting/Deleting Keystore Entries

The <span class="apiname">setCertificateEntry</span> method assigns a
certificate to a specified alias:

``` {.codeblock dir="ltr"}
final void setCertificateEntry(String alias, Certificate cert)
```

If `alias`{.codeph} doesn\'t exist, a trusted certificate entry with
that alias is created. If `alias`{.codeph} exists and identifies a
trusted certificate entry, the certificate associated with it is
replaced by `cert`{.codeph}.

The <span class="apiname">setKeyEntry</span> methods add (if
`alias`{.codeph} doesn\'t yet exist) or set key entries:

``` {.codeblock dir="ltr"}
final void setKeyEntry(String alias,
                       Key key,
                       char[] password,
                       Certificate[] chain)

final void setKeyEntry(String alias,
                       byte[] key,
                       Certificate[] chain)
```

In the method with `key`{.codeph} as a byte array, it is the bytes for a
key in protected format. For example, in the keystore implementation
supplied by the `SUN`{.codeph} provider, the `key`{.codeph} byte array
is expected to contain a protected private key, encoded as an
`EncryptedPrivateKeyInfo`{.codeph} as defined in the PKCS8 standard. In
the other method, the `password`{.codeph} is the password used to
protect the key.

The <span class="apiname">deleteEntry</span> method deletes an entry:

``` {.codeblock dir="ltr"}
final void deleteEntry(String alias)
```

PKCS \#12 keystores support entries containing arbitrary attributes. Use
the
[`PKCS12Attribute`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/PKCS12Attribute.html)
class to create the attributes. When creating the new keystore entry use
a constructor method that accepts attributes. Finally, use the following
method to add the entry to the keystore:

``` {.codeblock dir="ltr"}
final void setEntry(String alias, Entry entry, 
                    ProtectionParameter protParam)
```

</div>
<!-- class="section" -->

<div class="section">
Getting Information from the Keystore

The `getKey`{.codeph} method returns the key associated with the given
alias. The key is recovered using the given password:

``` {.codeblock dir="ltr"}
final Key getKey(String alias, char[] password)
```

The following methods return the certificate, or certificate chain,
respectively, associated with the given alias:

``` {.codeblock dir="ltr"}
final Certificate getCertificate(String alias)
final Certificate[] getCertificateChain(String alias)
```

You can determine the name (`alias`{.codeph}) of the first entry whose
certificate matches a given certificate via the following:

``` {.codeblock dir="ltr"}
final String getCertificateAlias(Certificate cert)
```

PKCS \#12 keystores support entries containing arbitrary attributes. Use
the following method to retrieve an entry that may contain attributes:

``` {.codeblock dir="ltr"}
final Entry getEntry(String alias, ProtectionParameter protParam)
```

and then use the
[`KeyStore.Entry.getAttributes`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/KeyStore.Entry.html#getAttributes--)
method to extract such attributes and use the methods of the
[`KeyStore.Entry.Attribute`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/KeyStore.Entry.Attribute.html)
interface to examine them.

</div>
<!-- class="section" -->

<div class="section">
Saving the KeyStore

The in-memory keystore can be saved via the `store`{.codeph} method:

``` {.codeblock dir="ltr"}
final void store(OutputStream stream, char[] password)
```

The password is used to calculate an integrity checksum of the keystore
data, which is appended to the keystore data.

A DKS keystore is stored by passing a
[`DomainLoadStoreParameter`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/DomainLoadStoreParameter.html)
to the alternative store method:

``` {.codeblock dir="ltr"}
final void store(KeyStore.LoadStoreParameter param)
```

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-33407B4E-D819-4294-94AB-C6FABF96A93D}

### Algorithm Parameters Classes {#JSSEC-GUID-33407B4E-D819-4294-94AB-C6FABF96A93D .sect3}

<div>
Like `Key`{.codeph}s and `Keyspec`{.codeph}s, an algorithm\'s
initialization parameters are represented by either
`AlgorithmParameter`{.codeph}s or `AlgorithmParameterSpec`{.codeph}s.

Depending on the use situation, algorithms can use the parameters
directly, or the parameters might need to be converted into a more
portable format for transmission or storage.

A <span class="variable">transparent</span> representation of a set of
parameters (via `AlgorithmParameterSpec`{.codeph}) means that you can
access each parameter value in the set individually. You can access
these values through one of the `get`{.codeph} methods defined in the
corresponding specification class (e.g., `DSAParameterSpec`{.codeph}
defines `getP`{.codeph}, `getQ`{.codeph}, and `getG`{.codeph} methods,
to access `p`{.codeph}, `q`{.codeph}, and `g`{.codeph}, respectively).

In contrast, the [The AlgorithmParameters
Class](java-cryptography-architecture-jca-reference-guide.html#GUID-EF3A257D-5489-472A-8297-7E9952A5AAB0 "The AlgorithmParameters class provides an opaque representation of cryptographic parameters.")
class supplies an <span class="variable">opaque</span> representation,
in which you have no direct access to the parameter fields. You can only
get the name of the algorithm associated with the parameter set (via
`getAlgorithm`{.codeph}) and some kind of encoding for the parameter set
(via `getEncoded`{.codeph}).

</div>
<div class="sect4">
[]{#GUID-190C91B4-991D-416E-A932-C0E37B33A86D}

#### The AlgorithmParameterSpec Interface {#JSSEC-GUID-190C91B4-991D-416E-A932-C0E37B33A86D .sect4}

<div>
`AlgorithmParameterSpec`{.codeph} is an interface to a transparent
specification of cryptographic parameters. This interface contains no
methods or constants. Its only purpose is to group (and provide type
safety for) all parameter specifications. All parameter specifications
must implement this interface.

<div class="section">
The following are the algorithm parameter specification interfaces and
classes in the `java.security.spec`{.codeph} and
`javax.crypto.spec`{.codeph} packages:

-   [`DHParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/DHParameterSpec.html)
-   [`DHGenParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/DHGenParameterSpec.html)
-   [`DSAParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/DSAParameterSpec.html)
-   [`ECGenParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/ECGenParameterSpec.html)
-   [`ECParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/ECParameterSpec.html)
-   [`GCMParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/GCMParameterSpec.html)
-   [`IvParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/IvParameterSpec.html)
-   [`MGF1ParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/MGF1ParameterSpec.html)
-   [`OAEPParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/OAEPParameterSpec.html)
-   [`PBEParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/PBEParameterSpec.html)
-   [`PSSParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/PSSParameterSpec.html)
-   [`RC2ParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/RC2ParameterSpec.html)
-   [`RC5ParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/RC5ParameterSpec.html)
-   [`RSAKeyGenParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/RSAKeyGenParameterSpec.html)

The following algorithm parameter specs are used specifically for XML
digital signatures.

-   [`Interface C14NMethodParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/C14NMethodParameterSpec.html)
-   [`Interface DigestMethodParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/DigestMethodParameterSpec.html)
-   [`Interface SignatureMethodParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/SignatureMethodParameterSpec.html)
-   [`Interface TransformParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/TransformParameterSpec.html)
-   [`Interface ExcC14NParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/ExcC14NParameterSpec.html)
-   [`Interface HMACParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/HMACParameterSpec.html)
-   [`Interface XPathFilter2ParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/XPathFilter2ParameterSpec.html)
-   [`Interface XPathFilterParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/XPathFilterParameterSpec.html)
-   [`XSLTTransformParameterSpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/XSLTTransformParameterSpec.html)

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-EF3A257D-5489-472A-8297-7E9952A5AAB0}

#### The AlgorithmParameters Class {#JSSEC-GUID-EF3A257D-5489-472A-8297-7E9952A5AAB0 .sect4}

<div>
The `AlgorithmParameters`{.codeph} class provides an opaque
representation of cryptographic parameters.

<div class="section">
The AlgorithmParameters Class

The `AlgorithmParameters`{.codeph} class is an [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.")
.You can initialize the `AlgorithmParameters`{.codeph} class using a
specific `AlgorithmParameterSpec`{.codeph} object, or by encoding the
parameters in a recognized format. You can retrieve the resulting
specification with the <span class="apiname">getParameterSpec</span>
method (see the following section).

</div>
<!-- class="section" -->

<div class="section">
Creating an AlgorithmParameters Object

`AlgorithmParameters`{.codeph} objects are obtained by using one of the
`AlgorithmParameters`{.codeph} getInstance() static factory methods. For
more information, see [How Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Initializing an AlgorithmParameters Object

Once an `AlgorithmParameters`{.codeph} object is instantiated, it must
be initialized via a call to `init`{.codeph}, using an appropriate
parameter specification or parameter encoding:

``` {.codeblock dir="ltr"}
void init(AlgorithmParameterSpec paramSpec)
void init(byte[] params)
void init(byte[] params, String format)
```

In these `init`{.codeph} methods, `params`{.codeph} is an array
containing the encoded parameters, and `format`{.codeph} is the name of
the decoding format. In the `init`{.codeph} method with a
`params`{.codeph} argument but no `format`{.codeph} argument, the
primary decoding format for parameters is used. The primary decoding
format is ASN.1, if an ASN.1 specification for the parameters exists.

</div>
<!-- class="section" -->

<div class="section">
Obtaining the Encoded Parameters

A byte encoding of the parameters represented in an
`AlgorithmParameters`{.codeph} object may be obtained via a call to
`getEncoded`{.codeph}:

``` {.codeblock dir="ltr"}
byte[] getEncoded()
```

This method returns the parameters in their primary encoding format. The
primary encoding format for parameters is ASN.1, if an ASN.1
specification for this type of parameters exists.

If you want the parameters returned in a specified encoding format, use

``` {.codeblock dir="ltr"}
byte[] getEncoded(String format)
```

If `format`{.codeph} is null, the primary encoding format for parameters
is used, as in the other <span class="apiname">getEncoded</span> method.

</div>
<!-- class="section" -->

<div class="section">
Converting an AlgorithmParameters Object to a Transparent Specification

A transparent parameter specification for the algorithm parameters may
be obtained from an `AlgorithmParameters`{.codeph} object via a call to
`getParameterSpec`{.codeph}:

``` {.codeblock dir="ltr"}
AlgorithmParameterSpec getParameterSpec(Class paramSpec)
```

`paramSpec`{.codeph} identifies the specification class in which the
parameters should be returned. The specification class could be, for
example, `DSAParameterSpec.class`{.codeph} to indicate that the
parameters should be returned in an instance of the
`DSAParameterSpec`{.codeph} class. (This class is in the
`java.security.spec`{.codeph} package.)

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-921D1B8C-5A16-403E-B3A6-D9C6EC684D1C}

#### The AlgorithmParameterGenerator Class {#JSSEC-GUID-921D1B8C-5A16-403E-B3A6-D9C6EC684D1C .sect4}

<div>
<div class="section">
The `AlgorithmParameterGenerator`{.codeph} class is an [Engine Classes
and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.")
used to generate a set of <span class="bold">brand-new</span> parameters
suitable for a certain algorithm (the algorithm is specified when an
`AlgorithmParameterGenerator`{.codeph} instance is created). This object
is used when you do not have an existing set of algorithm parameters,
and want to generate one from scratch.

</div>
<!-- class="section" -->

<div class="section">
Creating an AlgorithmParameterGenerator Object

`AlgorithmParameterGenerator`{.codeph} objects are obtained by using one
of the `AlgorithmParameterGenerator`{.codeph} getInstance() static
factory methods. See [How Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Initializing an AlgorithmParameterGenerator Object

The `AlgorithmParameterGenerator`{.codeph} object can be initialized in
two different ways: an algorithm-independent manner or an
algorithm-specific manner.

The algorithm-independent approach uses the fact that all parameter
generators share the concept of a \"size\" and a source of randomness.
The measure of size is universally shared by all algorithm parameters,
though it is interpreted differently for different algorithms. For
example, in the case of parameters for the DSA algorithm, \"size\"
corresponds to the size of the prime modulus, in bits. (See [Java
Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
to know more about the sizes for specific algorithms.) When using this
approach, algorithm-specific parameter generation values\--if
any\--default to some standard values. One `init`{.codeph} method that
takes these two universally shared types of arguments:

``` {.codeblock dir="ltr"}
void init(int size, SecureRandom random);
```

Another `init`{.codeph} method takes only a `size`{.codeph} argument and
uses a system-provided source of randomness:

``` {.codeblock dir="ltr"}
void init(int size)
```

A third approach initializes a parameter generator object using
algorithm-specific semantics, which are represented by a set of
algorithm-specific parameter generation values supplied in an
`AlgorithmParameterSpec`{.codeph} object:

``` {.codeblock dir="ltr"}
void init(AlgorithmParameterSpec genParamSpec,
                          SecureRandom random)

void init(AlgorithmParameterSpec genParamSpec)
```

To generate Diffie-Hellman system parameters, for example, the parameter
generation values usually consist of the size of the prime modulus and
the size of the random exponent, both specified in number of bits.

</div>
<!-- class="section" -->

<div class="section">
Generating Algorithm Parameters

Once you have created and initialized an AlgorithmParameterGenerator
object, you can use the generateParameters method to generate the
algorithm parameters:

`AlgorithmParameters generateParameters()`{.codeph}

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-9A581FBA-EDF7-4BCA-8244-4CE2C75E4CEA}

### The CertificateFactory Class {#JSSEC-GUID-9A581FBA-EDF7-4BCA-8244-4CE2C75E4CEA .sect3}

<div>
The `CertificateFactory`{.codeph} class defines the functionality of a
certificate factory, which is used to generate certificate and
certificate revocation list (CRL) objects from their encoding.

<div class="section">
The `CertificateFactory`{.codeph} class is an [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.").

A certificate factory for X.509 must return certificates that are an
instance of `java.security.cert.X509Certificate`{.codeph}, and CRLs that
are an instance of `java.security.cert.X509CRL`{.codeph}.

</div>
<!-- class="section" -->

<div class="section">
Creating a CertificateFactory Object

`CertificateFactory`{.codeph} objects are obtained by using one of the
`getInstance()`{.codeph} static factory methods. For more information,
see [How Provider Implementations Are Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741).

</div>
<!-- class="section" -->

<div class="section">
Generating Certificate Objects

To generate a certificate object and initialize it with the data read
from an input stream, use the `generateCertificate`{.codeph} method:

``` {.codeblock dir="ltr"}
final Certificate generateCertificate(InputStream inStream)
```

To return a (possibly empty) collection view of the certificates read
from a given input stream, use the `generateCertificates`{.codeph}
method:

``` {.codeblock dir="ltr"}
final Collection generateCertificates(InputStream inStream)
```

</div>
<!-- class="section" -->

<div class="section">
Generating CRL Objects

To generate a certificate revocation list (CRL) object and initialize it
with the data read from an input stream, use the `generateCRL`{.codeph}
method:

``` {.codeblock dir="ltr"}
final CRL generateCRL(InputStream inStream)
```

To return a (possibly empty) collection view of the CRLs read from a
given input stream, use the `generateCRLs`{.codeph} method:

``` {.codeblock dir="ltr"}
final Collection generateCRLs(InputStream inStream)
```

</div>
<!-- class="section" -->

<div class="section">
Generating CertPath Objects

The certificate path builder and validator for PKIX is defined by the
Internet X.509 Public Key Infrastructure Certificate and CRL Profile,
[RFC 5280](http://www.ietf.org/rfc/rfc5280.txt).

A certificate store implementation for retrieving certificates and CRLs
from Collection and LDAP directories, using the PKIX LDAP V2 Schema is
also available from the IETF as [RFC
2587](http://www.ietf.org/rfc/rfc2587.txt).

To generate a `CertPath`{.codeph} object and initialize it with data
read from an input stream, use one of the following
`generateCertPath`{.codeph} methods (with or without specifying the
encoding to be used for the data):

``` {.codeblock dir="ltr"}
final CertPath generateCertPath(InputStream inStream)

final CertPath generateCertPath(InputStream inStream,
                                String encoding)
```

To generate a `CertPath`{.codeph} object and initialize it with a list
of certificates, use the following method:

``` {.codeblock dir="ltr"}
final CertPath generateCertPath(List certificates)
```

To retrieve a list of the `CertPath`{.codeph} encoding supported by this
certificate factory, you can call the `getCertPathEncodings`{.codeph}
method:

``` {.codeblock dir="ltr"}
final Iterator getCertPathEncodings()
```

The default encoding will be listed first.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-C9C9DD6C-3A6B-4759-B41E-AAAC502C0229}

How the JCA Might Be Used in a SSL/TLS Implementation {#JSSEC-GUID-C9C9DD6C-3A6B-4759-B41E-AAAC502C0229 .sect2}
-----------------------------------------------------

<div>
With an understanding of the JCA classes, consider how these classes
might be combined to implement an advanced network protocol like
SSL/TLS.

<div class="section">
The SSL/TLS Overview section in the [SSL, TLS, and DTLS
Protocols](java-security-overview1.html#GUID-FCF419A7-B856-46DD-A36F-C6F88F9AF37F "The JDK provides APIs and an implementation of the SSL, TLS, and DTLS protocols that includes functionality for data encryption, message integrity, and server and client authentication. Applications can use SSL/TLS/DTLS to provide for the secure passage of data between two peers over any application protocol, such as HTTP on top of TCP/IP.")
describes at a high level how the protocols work. As asymmetric (public
key) cipher operations are much slower than symmetric operations (secret
key), public key cryptography is used to establish secret keys which are
then used to protect the actual application data. Vastly simplified, the
SSL/TLS handshake involves exchanging initialization data, performing
some public key operations to arrive at a secret key, and then using
that key to encrypt further traffic.

<div class="infoboxnote" id="GUID-C9C9DD6C-3A6B-4759-B41E-AAAC502C0229__GUID-33252E3C-D0BD-4073-9D36-C31CBC961EF5">
Note:

The details presented here simply show how some of the above classes
might be employed. This section will not present sufficient information
for building a SSL/TLS implementation. For more information, see [Java
Secure Socket Extension (JSSE) Reference
Guide](java-secure-socket-extension-jsse-reference-guide.html#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345 "The Java Secure Socket Extension (JSSE) enables secure Internet communications. It provides a framework and an implementation for a Java version of the SSL, TLS, and DTLS protocols and includes functionality for data encryption, server authentication, message integrity, and optional client authentication.")
and [RFC 5246: The Transport Layer Security (TLS) Protocol, Version
1.2](https://tools.ietf.org/html/rfc5246).

</div>
Assume that this SSL/TLS implementation will be made available as a JSSE
provider. A concrete implementation of the `Provider`{.codeph} class is
first written that will eventually be registered in the
`Security`{.codeph} class\' list of providers. This provider mainly
provides a mapping from algorithm names to actual implementation
classes. (that is: \"SSLContext.TLS\"-\>\"com.foo.TLSImpl\") When an
application requests an \"TLS\" instance (via
`SSLContext.getInstance("TLS")`{.codeph}), the provider\'s list is
consulted for the requested algorithm, and an appropriate instance is
created.

Before discussing details of the actual handshake, a quick review of
some of the JSSE\'s architecture is needed. The heart of the JSSE
architecture is the `SSLContext`{.codeph}. The context eventually
creates end objects (`SSLSocket`{.codeph} and `SSLEngine`{.codeph})
which actually implement the SSL/TLS protocol. `SSLContext`{.codeph}s
are initialized with two callback classes, `KeyManager`{.codeph} and
`TrustManager`{.codeph}, which allow applications to first select
authentication material to send and second to verify credentials sent by
a peer.

A JSSE `KeyManager`{.codeph} is responsible for choosing which
credentials to present to a peer. Many algorithms are possible, but a
common strategy is to maintain a RSA or DSA public/private key pair
along with a `X509Certificate`{.codeph} in a `KeyStore`{.codeph} backed
by a disk file. When a `KeyStore`{.codeph} object is initialized and
loaded from the file, the file\'s raw bytes are converted into
`PublicKey`{.codeph} and `PrivateKey`{.codeph} objects using a
`KeyFactory`{.codeph}, and a certificate chain\'s bytes are converted
using a `CertificateFactory`{.codeph}. When a credential is needed, the
`KeyManager`{.codeph} simply consults this `KeyStore`{.codeph} object
and determines which credentials to present.

A `KeyStore`{.codeph}\'s contents might have originally been created
using a utility such as `keytool`{.codeph}. `keytool`{.codeph} creates a
RSA or DSA `KeyPairGenerator`{.codeph} and initializes it with an
appropriate keysize. This generator is then used to create a
`KeyPair`{.codeph} which `keytool`{.codeph} would store along with the
newly-created certificate in the `KeyStore`{.codeph}, which is
eventually written to disk.

A JSSE `TrustManager`{.codeph} is responsible for verifying the
credentials received from a peer. There are many ways to verify
credentials: one of them is to create a `CertPath`{.codeph} object, and
let the JDK\'s built-in Public Key Infrastructure (PKI) framework handle
the validation. Internally, the CertPath implementation might create a
`Signature`{.codeph} object, and use that to verify that the each of the
signatures in the certificate chain.

With this basic understanding of the architecture, we can look at some
of the steps in the SSL/TLS handshake. The client begins by sending a
ClientHello message to the server. The server selects a ciphersuite to
use, and sends that back in a ServerHello message, and begins creating
JCA objects based on the suite selection. We\'ll use server-only
authentication in the following examples.

<div class="figure" id="GUID-C9C9DD6C-3A6B-4759-B41E-AAAC502C0229__GUID-882646E9-0A5E-4ED7-B681-DFFB0FD15668">
Figure 2-17 SSL/TLS Messages

![Description of Figure 2-17
follows](img/ssl-client.png "Description of Figure 2-17 follows")\
[Description of \"Figure 2-17 SSL/TLS
Messages\"](img_text/ssl-client.htm)

</div>
<!-- class="figure" -->

Server-only authentication is described in the following examples. The
examples are vastly simplified, but gives an idea of how the JSSE
classes might be combined to create a higher level protocol:

</div>
<!-- class="section" -->

<div class="example" id="GUID-C9C9DD6C-3A6B-4759-B41E-AAAC502C0229__GUID-3C2B038D-8282-4518-9923-9E4598F7200A">
Example 2-9 SSL/TLS Server Uses a RSA-based ciphersuite Such as
TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA

The server\'s `KeyManager`{.codeph} is queried, and returns an
appropriate RSA entry. The server\'s credentials (that is:
certificate/public key) are sent in the server\'s Certificate message.
The client\'s `TrustManager`{.codeph} verifies the server\'s
certificate, and if accepted, the client generates some random bytes
using a `SecureRandom`{.codeph} object. This is then encrypted using an
encrypting asymmetric RSA `Cipher`{.codeph} object that has been
initialized with the `PublicKey`{.codeph} found in the server\'s
certificate. This encrypted data is sent in a Client Key Exchange
message. The server would use its corresponding `PrivateKey`{.codeph} to
recover the bytes using a similar `Cipher`{.codeph} in decrypt mode.
These bytes are then used to establish the actual encryption keys.

</div>
<!-- class="example" -->

<div class="example" id="GUID-C9C9DD6C-3A6B-4759-B41E-AAAC502C0229__GUID-44DAB934-48B2-4359-8E56-57B01B5D5FA0">
Example 2-10 Choose an Ephemeral Diffie-Hellman Key Agreement Algorithm
Along with the DSA Signature Algorithm such as
TLS\_DHE\_DSS\_WITH\_AES\_128\_CBC\_SHA

The two sides must each establish a new temporary DH public/private
keypair using a `KeyPairGenerator`{.codeph}. Each generator creates DH
keys which can then be further converted into pieces using the
`KeyFactory`{.codeph} and `DHPublicKeySpec`{.codeph} classes. Each side
then creates a `KeyAgreement`{.codeph} object and initializes it with
their respective DH `PrivateKey`{.codeph}s. The server sends its public
key pieces in a `ServerKeyExchange`{.codeph} message (protected by the
DSA signature algorithm, and the client sends its public key in a
ClientKeyExchange message. When the public keys are reassembled using
another `KeyFactory`{.codeph}, they are fed into the agreement objects.
The `KeyAgreement`{.codeph} objects then generate agreed-upon bytes that
are then used to establish the actual encryption keys.

Once the actual encryption keys have been established, the secret key is
used to initialize a symmetric `Cipher`{.codeph} object, and this cipher
is used to protect all data in transit. To help determine if the data
has been modified, a `MessageDigest`{.codeph} is created and receives a
copy of the data destined for the network. When the packet is complete,
the digest (hash) is appended to data, and the entire packet is
encrypted by the `Cipher`{.codeph}. If a block cipher such as AES is
used, the data must be padded to make a complete block. On the remote
side, the steps are simply reversed.

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect2">
[]{#GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1}

Cryptographic Strength Configuration {#JSSEC-GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1 .sect2}
------------------------------------

<div>
You can configure the cryptographic strength of the Java Cryptography
Extension (JCE) architecture using jurisdiction policy files (see
[Jurisdiction Policy File
Format](java-cryptography-architecture-jca-reference-guide.html#GUID-F2CF205E-744E-4C16-B504-B6F79781E762))
and the security properties file.

Prior to Oracle Java JDK 9, the default cryptographic strength allowed
by Oracle implementations was "strong but limited" (for example AES keys
limited to 128 bits). To remove this restriction, administrators could
download and install a separate "unlimited strength" Jurisdiction Policy
Files bundle. The Jurisdiction Policy File mechanism was reworked for
JDK 9. It now allows for much more flexible configuration. The Oracle
JDK now ships with a default value of "unlimited" rather than "limited".
As always, administrators and users must still continue to follow all
import/export guidelines for their geographical locations. The active
cryptographic strength is now determined using a Security Property
(typically set in the `java.security`{.codeph} properties file), in
combination with the jurisdiction policy files found in the
configuration directory.

All the necessary JCE policy files to provide either unlimited
cryptographic strength or strong but limited cryptographic strength are
bundled with the JDK.

<div class="section">
Cryptographic Strength Settings

Each directory under `<java_home>/conf/security/policy`{.codeph}
represents a set of policy configurations defined by the jurisdiction
policy files that they contain. You activate a particular cryptographic
strength setting represented by the policy files in a directory by
setting the `crypto.policy`{.codeph} Security Property (configured in
the file `<java_home>/conf/security/java.security`{.codeph}) to point to
that directory.

<div class="p">
The JDK comes bundled with two such directories, `limited`{.codeph} and
`unlimited`{.codeph}, each containing a number of policy files. By
default, the `crypto.policy`{.codeph} Security Property is set to:

``` {.oac_no_warn dir="ltr"}
crypto.policy = unlimited
```

</div>
The overall value is the intersection of the files contained within the
directory. These policy files settings are VM-wide, and affect all
applications running on this VM. If you want to override cryptographic
strength at the application level, see [How to Make Applications Exempt
from Cryptographic
Restrictions](java-cryptography-architecture-jca-reference-guide.html#GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D).

</div>
<!-- class="section" -->

<div class="section">
Unlimited Directory Contents

The `unlimited`{.codeph} directory contains the following policy files:

<div class="p">
-   `<java_home>/conf/security/unlimited/default_US_export.policy`{.codeph}

    <div class="p">
    ``` {.oac_no_warn dir="ltr"}
    // Default US Export policy file.  
    grant {     
    // There is no restriction to any algorithms.
         permission javax.crypto.CryptoAllPermission;
    };
    ```

    <div class="infoboxnote" id="GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1__GUID-5E09236A-26C9-4879-95CB-6E5F2EC1B6C3">
    Note:

    As there are no current restrictions on export of cryptography from
    the United States, the `default_US_export.policy` file is set with
    no restrictions.

    </div>
    </div>
-   <div class="p">
    `<java_home>/conf/security/unlimited/default_local.policy`{.codeph}

    ``` {.oac_no_warn dir="ltr"}
    // Country specific policy file for countries with no limits on crypto strength.  
    grant {     
    // There is no restriction to any algorithms.
         permission javax.crypto.CryptoAllPermission;
    };
    ```

    <div class="infoboxnote" id="GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1__GUID-44F8E9BD-3982-4E54-8907-05AC7B28453A">
    Note:

    Depending on the country, there may be local restrictions, but as
    this policy file is located in the `unlimited`{.codeph} directory,
    there are no restrictions listed here.

    </div>
    </div>

</div>
To select unlimited cryptographic strength as defined in these two files
set `crypto.policy = unlimited`{.codeph} in the file
`<java_home>/conf/security/java.security`{.codeph}.

</div>
<!-- class="section" -->

<div class="section">
Limited Directory Contents

The `limited`{.codeph} directory currently contains the following policy
files:

-   <div class="p">
    `<java_home>/conf/security/limited/default_US_export.policy`{.codeph}

    ``` {.oac_no_warn dir="ltr"}
    // Default US Export policy file.  
    grant {     
    // There is no restriction to any algorithms.
         permission javax.crypto.CryptoAllPermission;
    };
    ```

    <div class="infoboxnote" id="GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1__GUID-297C34B0-18F6-4D2B-802F-B11D6B0FC233">
    Note:

    Even though this is in the `limited`{.codeph} directory, as there
    are no current restrictions on export of cryptography from the
    United States, the `default_US_export.policy` file is set with no
    restrictions.

    </div>
    </div>
-   `<java_home>/conf/security/limited/default_local.policy`{.codeph}

    ``` {.oac_no_warn dir="ltr"}
    // Some countries have import limits on crypto strength. This policy file
    // is worldwide importable.

    grant {
        permission javax.crypto.CryptoPermission "DES", 64;
        permission javax.crypto.CryptoPermission "DESede", *;
        permission javax.crypto.CryptoPermission "RC2", 128, 
                                         "javax.crypto.spec.RC2ParameterSpec", 128;
        permission javax.crypto.CryptoPermission "RC4", 128;
        permission javax.crypto.CryptoPermission "RC5", 128, 
              "javax.crypto.spec.RC5ParameterSpec", *, 12, *;
        permission javax.crypto.CryptoPermission "RSA", *;
        permission javax.crypto.CryptoPermission *, 128;
    };
    ```

    <div class="infoboxnote" id="GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1__GUID-53F6BA3F-7413-4B06-AA40-24359147478D">
    Note:

    This local policy file shows the default restrictions. It should be
    allowed by any country, including those that have import
    restrictions, but please obtain legal guidance.

    </div>
-   `<java_home>/conf/security/limited/exempt_local.policy`{.codeph}

    ``` {.oac_no_warn dir="ltr"}
    // Some countries have import limits on crypto strength, but may allow for
    // these exemptions if the exemption mechanism is used.

    grant {
        // There is no restriction to any algorithms if KeyRecovery is enforced.
        permission javax.crypto.CryptoPermission *, "KeyRecovery"; 

        // There is no restriction to any algorithms if KeyEscrow is enforced.
        permission javax.crypto.CryptoPermission *, "KeyEscrow"; 

        // There is no restriction to any algorithms if KeyWeakening is enforced. 
        permission javax.crypto.CryptoPermission *, "KeyWeakening";
    };
    ```

    <div class="infoboxnote" id="GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1__GUID-9AA5D629-D309-4DF2-9BCE-66BD1DDC8E76">
    Note:

    Countries that have import restrictions should use "limited", but
    these restrictions could be relaxed if the exemption mechanism can
    be employed. See [How to Make Applications Exempt from Cryptographic
    Restrictions](java-cryptography-architecture-jca-reference-guide.html#GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D).
    Please obtain legal guidance for your situation.

    </div>

</div>
<!-- class="section" -->

<div class="section">
Custom Cryptographic Strength Settings

To set up restrictions to cryptographic strength that are different than
the settings in the policy files in the `limited`{.codeph} or
`unlimited`{.codeph} directory, you can create a new directory, parallel
with `limited`{.codeph} and `unlimited`{.codeph}, and place your policy
files there. For example, you may create a directory called
`custom`{.codeph}. In this `custom`{.codeph} directory you include the
files `default_*export.policy`{.codeph} and/or
`exempt_*local.policy`{.codeph}.

To select cryptographic strength as defined in the files in the
`custom`{.codeph} directory, set `crypto.policy = custom`{.codeph} in
the file `<java_home>/conf/security/java.security`{.codeph}.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-F2CF205E-744E-4C16-B504-B6F79781E762}

Jurisdiction Policy File Format {#JSSEC-GUID-F2CF205E-744E-4C16-B504-B6F79781E762 .sect2}
-------------------------------

<div>
<div class="section">
JCA represents its jurisdiction policy files as Java-style policy files
with corresponding permission statements. As described in [Cryptographic
Strength
Configuration](java-cryptography-architecture-jca-reference-guide.html#GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1),
a Java policy file specifies what permissions are allowed for code from
specified code sources. A permission represents access to a system
resource. In the case of JCA, the \"resources\" are cryptography
algorithms, and code sources do not need to be specified, because the
cryptographic restrictions apply to all code.

A jurisdiction policy file consists of a very basic \"grant entry\"
containing one or more \"permission entries.\"

``` {.codeblock dir="ltr"}
grant {
    <permission entries>;
};
```

The format of a permission entry in a jurisdiction policy file is:

``` {.codeblock dir="ltr"}
permission <crypto permission class name>
    [<alg_name>
        [
            [, <exemption mechanism name>]
            [, <maxKeySize>
                [, <AlgorithmParameterSpec class name>,
                       <parameters for constructing an AlgorithmParameterSpec object>
                ]
            ]
        ]
    ];
```

A sample jurisdiction policy file that includes restricting the AES
algorithm to maximum key sizes of 128 bits is:

``` {.codeblock dir="ltr"}
    grant {
        permission javax.crypto.CryptoPermission "AES", 128;
        // ...
    };
```

A permission entry must begin with the word `permission`{.codeph}. Items
that appear in a permission entry must appear in the specified order. An
entry is terminated with a semicolon. Case is unimportant for the
identifiers (`grant`{.codeph}, `permission`{.codeph}) but is significant
for the `<crypto permission class name>`{.codeph} or for any string that
is passed in as a value. An asterisk (`*`{.codeph}) can be used as a
wildcard for any permission entry option. For example, an asterisk for
an `<alg_name>`{.codeph} option means \"all algorithms.\"

The following table describes a permission entry\'s options:

<div class="tblformal" id="GUID-F2CF205E-744E-4C16-B504-B6F79781E762__GUID-4B590C91-3FAE-4242-AE13-89EE1D99FE3B">
Table 2-1 Permission Entry Options

+-----------------------------------+-----------------------------------+
| Option                            | Description                       |
+:==================================+:==================================+
| `<crypto permission class name>`{ | Specific permission class name,   |
| .codeph}                          | such as                           |
|                                   | `javax.crypto.CryptoPermission`{. |
|                                   | codeph}.                          |
|                                   | Required.                         |
|                                   |                                   |
|                                   | A crypto permission class         |
|                                   | reflects the ability of an        |
|                                   | application to use certain        |
|                                   | algorithms with certain key sizes |
|                                   | in certain environments. There    |
|                                   | are two crypto permission         |
|                                   | classes:                          |
|                                   | `CryptoPermission`{.codeph} and   |
|                                   | `CryptoAllPermission`{.codeph}.   |
|                                   | The special                       |
|                                   | `CryptoAllPermission`{.codeph}    |
|                                   | class implies all                 |
|                                   | cryptography-related permissions, |
|                                   | that is, it specifies that there  |
|                                   | are no cryptography-related       |
|                                   | restrictions.                     |
+-----------------------------------+-----------------------------------+
| `<alg_name> `{.codeph}            | Quoted string specifying the      |
|                                   | standard name of a cryptography   |
|                                   | algorithm, such as \"AES\" or     |
|                                   | \"RSA\". Optional.                |
+-----------------------------------+-----------------------------------+
| `<exemption mechanism name>`{.cod | Quoted string indicating an       |
| eph}                              | exemption mechanism which, if     |
|                                   | enforced, enables a reduction in  |
|                                   | cryptographic restrictions.       |
|                                   | Optional.                         |
|                                   |                                   |
|                                   | Exemption mechanism names that    |
|                                   | can be used include               |
|                                   | \"KeyRecovery\" \"KeyEscrow\",    |
|                                   | and \"KeyWeakening\".             |
+-----------------------------------+-----------------------------------+
| `<maxKeySize>`{.codeph}           | Integer specifying the maximum    |
|                                   | key size (in bits) allowed for    |
|                                   | the specified algorithm.          |
|                                   | Optional.                         |
+-----------------------------------+-----------------------------------+
| `<AlgorithmParameterSpec class na | Class name that specifies the     |
| me>`{.codeph}                     | strength of the algorithm.        |
|                                   | Optional.                         |
|                                   |                                   |
|                                   | For some algorithms, it may not   |
|                                   | be sufficient to specify the      |
|                                   | algorithm strength in terms of    |
|                                   | just a key size. For example, in  |
|                                   | the case of the \"RC5\"           |
|                                   | algorithm, the number of rounds   |
|                                   | must also be considered. For      |
|                                   | algorithms whose strength needs   |
|                                   | to be expressed as more than a    |
|                                   | key size, use this option to      |
|                                   | specify the                       |
|                                   | `AlgorithmParameterSpec`{.codeph} |
|                                   | class name that does this (such   |
|                                   | as                                |
|                                   | `javax.crypto.spec.RC5ParameterSp |
|                                   | ec`{.codeph}                      |
|                                   | for the \"RC5\" algorithm).       |
+-----------------------------------+-----------------------------------+
| `<parameters for constructing an  | List of parameters for            |
| AlgorithmParameterSpec object>`{. | constructing the specified        |
| codeph}                           | `AlgorithmParameterSpec`{.codeph} |
|                                   | object. Required if               |
|                                   | ` <AlgorithmParameterSpec class n |
|                                   | ame>`{.codeph}                    |
|                                   | has been specified and requires   |
|                                   | parameters.                       |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D}

How to Make Applications Exempt from Cryptographic Restrictions {#JSSEC-GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D .sect2}
---------------------------------------------------------------

<div>
<div class="section">
<div class="infoboxnote" id="GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D__GUID-CD61A0CD-BB98-4CF9-B958-D75C1DF166A1">
Attention:

This section should be ignored by most application developers. It is
only for people whose applications may be exported to those few
countries whose governments mandate cryptographic restrictions, if it is
desired that such applications have fewer cryptographic restrictions
than those mandated.

</div>
By default, an application can use cryptographic algorithms of any
strength. However, due to import control restrictions by the governments
of a few countries, you may have to limit those algorithms\' strength.
The JCA framework includes an ability to enforce restrictions regarding
the maximum strengths of cryptographic algorithms available to
applications in different jurisdiction contexts (locations). You specify
these restrictions in jurisdiction policy files. For more information
about jurisdiction policy files and how to create and configure them,
see [Cryptographic Strength
Configuration](java-cryptography-architecture-jca-reference-guide.html#GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1).

It is possible that the governments of some or all such countries may
allow certain applications to become exempt from some or all
cryptographic restrictions. For example, they may consider certain types
of applications as \"special\" and thus exempt. Or they may exempt any
application that utilizes an \"exemption mechanism,\" such as key
recovery. Applications deemed to be exempt could get access to stronger
cryptography than that allowed for non-exempt applications in such
countries.

In order for an application to be recognized as \"exempt\" at runtime,
it must meet the following conditions:

-   It must have a permission policy file bundled with it in a JAR file.
    The permission policy file specifies what cryptography-related
    permissions the application has, and under what conditions (if any).
-   The JAR file containing the application and the permission policy
    file must have been signed using a code-signing certificate issued
    after the application was accepted as exempt.

Below are sample steps required in order to make an application exempt
from some cryptographic restrictions. This is a basic outline that
includes information about what is required by JCA in order to recognize
and treat applications as being exempt. You will need to know the
exemption requirements of the particular country or countries in which
you would like your application to be able to be run but whose
governments require cryptographic restrictions. You will also need to
know the requirements of a JCA framework vendor that has a process in
place for handling exempt applications. Consult such a vendor for
further information.

<div class="infoboxnote" id="GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D__GUID-870A208D-FE85-4D1E-A1C1-BA8B9616650D">
Note:

The `SunJCE`{.codeph} provider does not supply an implementation of the
`ExemptionMechanismSpi`{.codeph} class

</div>
1.  Write and Compile Your Application Code
2.  Create a Permission Policy File Granting Appropriate Cryptographic
    Permissions
3.  Prepare for Testing
    a.  Apply for Government Approval From the Government Mandating
        Restrictions.
    b.  Get a Code-Signing Certificate
    c.  Bundle the Application and Permission Policy File into a JAR
        file
    d.  [Step 7.1: Get a Code-Signing
        Certificate](howtoimplaprovider.html#GUID-434AACF7-0D2C-494A-B32A-508A6B605F62 "The next step is to request a code-signing certificate so that you can use it to sign your provider prior to testing. The certificate will be good for both testing and production. It will be valid for 5 years.")
    e.  Set Up Your Environment Like That of a User in a Restricted
        Country
    f.  (only for applications using exemption mechanisms) Install a
        Provider Implementing the Exemption Mechanism Specified by the
        entry in the Permission Policy File
4.  Test Your Application
5.  Apply for U.S. Government Export Approval If Required
6.  Deploy Your Application

</div>
<!-- class="section" -->

<div class="section">
Special Code Requirements for Applications that Use Exemption Mechanisms

When an application has a permission policy file associated with it (in
the same JAR file) and that permission policy file specifies an
exemption mechanism, then when the <span class="apiname">Cipher</span>
`getInstance`{.codeph} method is called to instantiate a
<span class="apiname">Cipher</span>, the JCA code searches the installed
providers for one that implements the specified exemption mechanism. If
it finds such a provider, JCA instantiates an
`ExemptionMechanism`{.codeph} API object associated with the provider\'s
implementation, and then associates the `ExemptionMechanism`{.codeph}
object with the <span class="apiname">Cipher</span> returned by
`getInstance`{.codeph}.

After instantiating a Cipher, and prior to initializing it (via a call
to the Cipher `init`{.codeph} method), your code must call the following
<span class="apiname">Cipher</span> method:

``` {.codeblock dir="ltr"}
    public ExemptionMechanism getExemptionMechanism()
```

This call returns the `ExemptionMechanism`{.codeph} object associated
with the Cipher. You must then initialize the exemption mechanism
implementation by calling the following method on the returned
`ExemptionMechanism`{.codeph}:

``` {.codeblock dir="ltr"}
    public final void init(Key key)
```

The argument you supply should be the same as the argument of the same
types that you will subsequently supply to a Cipher `init`{.codeph}
method.

Once you have initialized the `ExemptionMechanism`{.codeph}, you can
proceed as usual to initialize and use the Cipher.

</div>
<!-- class="section" -->

<div class="section">
Permission Policy Files

In order for an application to be recognized at runtime as being
\"exempt\" from some or all cryptographic restrictions, it must have a
permission policy file bundled with it in a JAR file. The permission
policy file specifies what cryptography-related permissions the
application has, and under what conditions (if any).

The format of a permission entry in a permission policy file that
accompanies an exempt application is the same as the format for a
jurisdiction policy file downloaded with the JDK, which is:

``` {.codeblock dir="ltr"}
permission <crypto permission class name>
    [<alg_name>
        [
            [, <exemption mechanism name>]
            [, <maxKeySize>
                [, <AlgorithmParameterSpec class name>,
                       <parameters for constructing an AlgorithmParameterSpec object>
                ]
            ]
        ]
    ];
```

See [Jurisdiction Policy File
Format](java-cryptography-architecture-jca-reference-guide.html#GUID-F2CF205E-744E-4C16-B504-B6F79781E762).

</div>
<!-- class="section" -->

<div class="section">
Permission Policy Files for Exempt Applications

Some applications may be allowed to be completely unrestricted. Thus,
the permission policy file that accompanies such an application usually
just needs to contain the following:

``` {.codeblock dir="ltr"}
grant {
    // There are no restrictions to any algorithms.
    permission javax.crypto.CryptoAllPermission;
};
```

If an application just uses a single algorithm (or several specific
algorithms), then the permission policy file could simply mention that
algorithm (or algorithms) explicitly, rather than granting
<span class="apiname">CryptoAllPermission</span>.

For example, if an application just uses the Blowfish algorithm, the
permission policy file doesn\'t have to grant
<span class="apiname">CryptoAllPermission</span> to all algorithms. It
could just specify that there is no cryptographic restriction if the
Blowfish algorithm is used. In order to do this, the permission policy
file would look like the following:

``` {.codeblock dir="ltr"}
grant {
    permission javax.crypto.CryptoPermission "Blowfish";
};
```

</div>
<!-- class="section" -->

<div class="section">
Permission Policy Files for Applications Exempt Due to Exemption
Mechanisms

If an application is considered \"exempt\" if an exemption mechanism is
enforced, then the permission policy file that accompanies the
application must specify one or more exemption mechanisms. At run time,
the application will be considered exempt if any of those exemption
mechanisms is enforced. Each exemption mechanism must be specified in a
permission entry that looks like the following:

``` {.codeblock dir="ltr"}
    // No algorithm restrictions if specified
    // exemption mechanism is enforced.
    permission javax.crypto.CryptoPermission *,
        "<ExemptionMechanismName>";
```

where `<ExemptionMechanismName>`{.codeph} specifies the name of an
exemption mechanism. The list of possible exemption mechanism names
includes:

-   `KeyRecovery`{.codeph}
-   `KeyEscrow`{.codeph}
-   `KeyWeakening`{.codeph}

As an example, suppose your application is exempt if either key recovery
or key escrow is enforced. Then your permission policy file should
contain the following:

``` {.codeblock dir="ltr"}
grant {
    // No algorithm restrictions if KeyRecovery is enforced.
    permission javax.crypto.CryptoPermission *, "KeyRecovery";

    // No algorithm restrictions if KeyEscrow is enforced.
    permission javax.crypto.CryptoPermission *, "KeyEscrow";
};
```

<div class="p">
<div class="infoboxnote" id="GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D__GUID-04F2AC6B-93B0-4124-9B04-99B8D7672EFE">
Note:

Permission entries that specify exemption mechanisms should
<span class="variable">not</span> also specify maximum key sizes. The
allowed key sizes are actually determined from the installed exempt
jurisdiction policy files, as described in the next section.

</div>
</div>
</div>
<!-- class="section" -->

<div class="section">
How Bundled Permission Policy Files Affect Cryptographic Permissions

At runtime, when an application instantiates a
<span class="apiname">Cipher</span> (via a call to its
`getInstance`{.codeph} method) and that application has an associated
permission policy file, JCA checks to see whether the permission policy
file has an entry that applies to the algorithm specified in the
`getInstance`{.codeph} call. If it does, and the entry grants
<span class="apiname">CryptoAllPermission</span> or does not specify
that an exemption mechanism must be enforced, it means there is no
cryptographic restriction for this particular algorithm.

If the permission policy file has an entry that applies to the algorithm
specified in the `getInstance`{.codeph} call and the entry
<span class="variable">does</span> specify that an exemption mechanism
must be enforced, then the exempt jurisdiction policy file(s) are
examined. If the exempt permissions include an entry for the relevant
algorithm and exemption mechanism, and that entry is implied by the
permissions in the permission policy file bundled with the application,
and if there is an implementation of the specified exemption mechanism
available from one of the registered providers, then the maximum key
size and algorithm parameter values for the
<span class="apiname">Cipher</span> are determined from the exempt
permission entry.

If there is no exempt permission entry implied by the relevant entry in
the permission policy file bundled with the application, or if there is
no implementation of the specified exemption mechanism available from
any of the registered providers, then the application is only allowed
the standard default cryptographic permissions.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-6EA080B2-D6B3-4FAD-8369-2170756E0469}

Standard Names {#JSSEC-GUID-6EA080B2-D6B3-4FAD-8369-2170756E0469 .sect2}
--------------

<div>
The Standard Names document contains information about the algorithm
specifications.

<div class="section">
[Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
describes the standard names for algorithms, certificate and keystore
types that the JDK Security API requires and uses. It also contains more
information about the algorithm specifications. Specific provider
information can be found in [JDK Providers
Documentation](oracle-providers.html#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313 "This document contains the technical details of the providers that are included in the JDK. It is assumed that readers have a strong understanding of the Java Cryptography Architecture and Provider Architecture.").

Cryptographic implementations in the JDK are distributed through several
different providers primarily for historical reasons (`Sun`{.codeph},
`SunJSSE`{.codeph}, `SunJCE`{.codeph}, `SunRsaSign`{.codeph}). Note
these providers may not be available on all JDK implementations, and
therefore, truly portable applications should call
<span class="apiname">getInstance()</span> without specifying specific
providers. Applications specifying a particular provider may not be able
to take advantage of native providers tuned for an underlying operating
environment (such as PKCS or Microsoft\'s CAPI).

The `SunPKCS11`{.codeph} provider itself does not contain any
cryptographic algorithms, but instead, directs requests into an
underlying PKCS11 implementation. Consult [PKCS\#11 Reference
Guide](pkcs11-reference-guide1.html#GUID-30E98B63-4910-40A1-A6DD-663EAF466991)
and the underlying PKCS11 implementation to determine if a desired
algorithm will be available through the PKCS11 provider. Likewise, on
Windows systems, the `SunMSCAPI`{.codeph} provider does not provide any
cryptographic functionality, but instead routes requests to the
underlying Operating System for handling.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-4FE9F3DF-5D49-44F6-8F28-7541114D520C}

Packaging Your Application {#JSSEC-GUID-4FE9F3DF-5D49-44F6-8F28-7541114D520C .sect2}
--------------------------

<div>
You can package an application in three different kinds of modules:

-   Named or explicit module: A module that appears on the module path
    and contains module configuration information in the
    `module-info.class` file.

-   Automatic module:  A module that appears on the module path, but
    does not contain module configuration information in a
    `module-info.class` file (essentially a \"regular\" JAR file).

-   Unnamed module: A module that appears on the class path. It may or
    may not have a `module-info.class` file; this file is ignored.

It is recommended that you package your applications in named modules as
they provide better performance, stronger encapsulation, and simpler
configuration. They also offer greater flexibility; you can use them
with non-modular JDKs or even as unnamed modules by specifying them in a
modular JDK\'s class path.

For more information about modules, see [The State of the Module
System](http://openjdk.java.net/projects/jigsaw/spec/sotms/) and [JEP
261: Module System](http://openjdk.java.net/jeps/261)

</div>
</div>
<div class="sect2">
[]{#GUID-871FA938-5110-409E-A4EC-16F2A898093A}

Additional JCA Code Samples {#JSSEC-GUID-871FA938-5110-409E-A4EC-16F2A898093A .sect2}
---------------------------

<div>
These examples illustrate use of several JCA mechanisms. See also
[Sample Programs for Diffie-Hellman Key Exchange, AES/GCM, and
HMAC-SHA256](java-cryptography-architecture-jca-reference-guide.html#GUID-725B837C-9DB3-4B9F-A8D8-1E1C72B558E0 "The following are sample programs for Diffie-Hellman key exchange, AES/GCM, and HMAC-SHA256.")

<div class="section">
Topics

[Computing a MessageDigest
Object](java-cryptography-architecture-jca-reference-guide.html#GUID-6E9FB890-F011-450E-9EC5-EBB358E1D8A1 "An example describing the procedure to compute a MessageDigest object.")

[Generating a Pair of
Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-ED6EDA78-8D20-4059-92E1-FBDDE4D3DFE6 "In this example we will generate a public-private key pair for the algorithm named ")

[Generating and Verifying a Signature Using Generated
Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-7389E94B-A595-4020-A4D2-73FB0DD5A05A "Examples of generating and verifying a signature using generated keys.")

[Generating/Verifying Signatures Using Key Specifications and
KeyFactory](java-cryptography-architecture-jca-reference-guide.html#GUID-5514BAFF-5F0F-403C-9943-56A632D6E406 "Sample code that is used to generate and verify signatures using key specifications and KeyFactory.")

[Determining If Two Keys Are
Equal](java-cryptography-architecture-jca-reference-guide.html#GUID-F7F401C9-63E6-4BE4-9F32-A28B3568EBCC "Example code for determining if two keys are equal.")

[Reading Base64-Encoded
Certificates](java-cryptography-architecture-jca-reference-guide.html#GUID-CD24C31B-45FA-480C-AFCA-C108C01689D8)

[Parsing a Certificate
Reply](java-cryptography-architecture-jca-reference-guide.html#GUID-8001F1B9-7DBF-4135-A5F3-0042F803E58A)

[Using
Encryption](java-cryptography-architecture-jca-reference-guide.html#GUID-AA678E6B-7EAB-44F3-A8CD-F59BEA201BBF "This section takes the user through the process of generating a key, creating and initializing a cipher object, encrypting a file, and then decrypting it. Throughout this example, we use the Advanced Encryption Standard (AES).")

[Using Password-Based
Encryption](java-cryptography-architecture-jca-reference-guide.html#GUID-C9F76AFB-6B20-45A7-B84F-96756C8A94B4)

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-6E9FB890-F011-450E-9EC5-EBB358E1D8A1}

### Computing a MessageDigest Object {#JSSEC-GUID-6E9FB890-F011-450E-9EC5-EBB358E1D8A1 .sect3}

<div>
An example describing the procedure to compute a MessageDigest object.

1.  <span>Create the `MessageDigest`{.codeph} object, as in the
    following example:</span>

    <div>
    ``` {.codeblock dir="ltr"}
       MessageDigest sha = MessageDigest.getInstance("SHA-256");
    ```

    This call assigns a properly initialized message digest object to
    the `sha`{.codeph} variable. The implementation implements the
    Secure Hash Algorithm (SHA-256), as defined in the National
    Institute for Standards and Technology\'s (NIST) [FIPS 180-2
    document](http://csrc.nist.gov/publications/fips/index.html).

    </div>
2.  <span>Suppose we have three byte arrays, `i1`{.codeph},
    `i2`{.codeph} and `i3`{.codeph}, which form the total input whose
    message digest we want to compute. This digest (or \"hash\") could
    be calculated via the following calls:</span>

    <div>
    ``` {.codeblock dir="ltr"}
       sha.update(i1);
       sha.update(i2);
       sha.update(i3);
       byte[] hash = sha.digest();
    ```

    </div>
3.  **Optional:** <span>An equivalent alternative series of calls would
    be:</span>

    <div>
    ``` {.codeblock dir="ltr"}
       sha.update(i1);
       sha.update(i2);
       byte[] hash = sha.digest(i3);
    ```

    </div>
    <div>
    After the message digest has been calculated, the message digest
    object is automatically reset and ready to receive new data and
    calculate its digest. All former state (i.e., the data supplied to
    `update`{.codeph} calls) is lost.

    </div>

<div class="example" id="GUID-6E9FB890-F011-450E-9EC5-EBB358E1D8A1__GUID-330AF0AF-315C-4418-8882-6CF8F4C9E551">
Example 2-11 Hash Implementations Through Cloning

Some hash implementations may support intermediate hashes through
cloning. Suppose we want to calculate separate hashes for:

-   `i1`{.codeph}
-   `i1 and i2`{.codeph}
-   `i1, i2, and i3`{.codeph}

The following is one way to calculate these hashes; however, this code
works only if the SHA-256 implementation is cloneable:

``` {.codeblock dir="ltr"}
/* compute the hash for i1 */
sha.update(i1);
byte[] i1Hash = sha.clone().digest();

/* compute the hash for i1 and i2 */
sha.update(i2);
byte[] i12Hash = sha.clone().digest();

/* compute the hash for i1, i2 and i3 */
sha.update(i3);
byte[] i123hash = sha.digest();
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-6E9FB890-F011-450E-9EC5-EBB358E1D8A1__GUID-B26EFA90-D3F5-4D84-BC21-4463D144473D">
Example 2-12 Determine if the Hash Implementation is Cloneable or not
Cloneable

Some implementations of message digests are cloneable, others are not.
To determine whether or not cloning is possible, attempt to clone the
`MessageDigest`{.codeph} object and catch the potential exception as
follows:

``` {.codeblock dir="ltr"}
try {
    // try and clone it
    /* compute the hash for i1 */
    sha.update(i1);
    byte[] i1Hash = sha.clone().digest();
    // ...
    byte[] i123hash = sha.digest();
} catch (CloneNotSupportedException cnse) {
    // do something else, such as the code shown below
}
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-6E9FB890-F011-450E-9EC5-EBB358E1D8A1__GUID-27A86AA9-D666-434E-9132-6714C46CF320">
Example 2-13 Compute Intermediate Digests if the Hash Implementation is
not Cloneable

If a message digest is not cloneable, the other, less elegant way to
compute intermediate digests is to create several digests. In this case,
the number of intermediate digests to be computed must be known in
advance:

``` {.codeblock dir="ltr"}
   MessageDigest md1 = MessageDigest.getInstance("SHA-256");
   MessageDigest md2 = MessageDigest.getInstance("SHA-256");
   MessageDigest md3 = MessageDigest.getInstance("SHA-256");

   byte[] i1Hash = md1.digest(i1);

   md2.update(i1);
   byte[] i12Hash = md2.digest(i2);

   md3.update(i1);
   md3.update(i2);
   byte[] i123Hash = md3.digest(i3);
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-ED6EDA78-8D20-4059-92E1-FBDDE4D3DFE6}

### Generating a Pair of Keys {#JSSEC-GUID-ED6EDA78-8D20-4059-92E1-FBDDE4D3DFE6 .sect3}

<div>
In this example we will generate a public-private key pair for the
algorithm named \"DSA\" (Digital Signature Algorithm), and use this
keypair in future examples. We will generate keys with a 2048-bit
modulus. We don\'t care which provider supplies the algorithm
implementation.

<div class="section">
Creating the Key Pair Generator

The first step is to get a key pair generator object for generating keys
for the DSA algorithm:

``` {.codeblock dir="ltr"}
    KeyPairGenerator keyGen = KeyPairGenerator.getInstance("DSA");
```

</div>
<!-- class="section" -->

<div class="section">
Initializing the Key Pair Generator

The next step is to initialize the key pair generator. In most cases,
algorithm-independent initialization is sufficient, but in some cases,
algorithm-specific initialization is used.

</div>
<!-- class="section" -->

<div class="section">
Algorithm-Independent Initialization

All key pair generators share the concepts of a keysize and a source of
randomness. The `KeyPairGenerator`{.codeph} class initialization methods
at a minimum needs a keysize. If the source of randomness is not
explicitly provided, a `SecureRandom`{.codeph} implementation of the
highest-priority installed provider will be used. Thus to generate keys
with a keysize of 2048, simply call:

``` {.codeblock dir="ltr"}
    keyGen.initialize(2048);
```

The following code illustrates how to use a specific, additionally
seeded `SecureRandom `{.codeph}object:

``` {.codeblock dir="ltr"}
    SecureRandom random = SecureRandom.getInstance("DRBG", "SUN");
    random.setSeed(userSeed);
    keyGen.initialize(2048, random);
```

Since no other parameters are specified when you call the above
algorithm-independent <span class="apiname">initialize</span> method, it
is up to the provider what to do about the algorithm-specific parameters
(if any) to be associated with each of the keys. The provider may use
precomputed parameter values or may generate new values.

</div>
<!-- class="section" -->

<div class="section">
Algorithm-Specific Initialization

For situations where a set of algorithm-specific parameters already
exists (such as \"community parameters\" in DSA), there are two
`initialize`{.codeph} methods that have an
`AlgorithmParameterSpec`{.codeph} argument. Suppose your key pair
generator is for the \"DSA\" algorithm, and you have a set of
DSA-specific parameters, `p`{.codeph}, `q`{.codeph}, and `g`{.codeph},
that you would like to use to generate your key pair. You could execute
the following code to initialize your key pair generator (recall that
`DSAParameterSpec`{.codeph} is an `AlgorithmParameterSpec`{.codeph}):

``` {.codeblock dir="ltr"}
    DSAParameterSpec dsaSpec = new DSAParameterSpec(p, q, g);
    keyGen.initialize(dsaSpec);
```

</div>
<!-- class="section" -->

<div class="section">
Generating the Pair of Keys

The final step is actually generating the key pair. No matter which type
of initialization was used (algorithm-independent or
algorithm-specific), the same code is used to generate the
` KeyPair`{.codeph}:

``` {.codeblock dir="ltr"}
    KeyPair pair = keyGen.generateKeyPair();
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-7389E94B-A595-4020-A4D2-73FB0DD5A05A}

### Generating and Verifying a Signature Using Generated Keys {#JSSEC-GUID-7389E94B-A595-4020-A4D2-73FB0DD5A05A .sect3}

<div>
Examples of generating and verifying a signature using generated keys.

<div class="section">
The following signature generation and verification examples use the
`KeyPair`{.codeph} generated in the [Generating a Pair of
Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-ED6EDA78-8D20-4059-92E1-FBDDE4D3DFE6 "In this example we will generate a public-private key pair for the algorithm named ")
.

</div>
<!-- class="section" -->

<div class="section">
Generating a Signature

We first create a Signature Class object:

``` {.codeblock dir="ltr"}
    Signature dsa = Signature.getInstance("SHA256withDSA");
```

Next, using the key pair generated in the key pair example, we
initialize the object with the private key, then sign a byte array
called `data`{.codeph}.

``` {.codeblock dir="ltr"}
   /* Initializing the object with a private key */
    PrivateKey priv = pair.getPrivate();
    dsa.initSign(priv);

   /* Update and sign the data */
    dsa.update(data);
    byte[] sig = dsa.sign();
```

</div>
<!-- class="section" -->

<div class="section">
Verifying a Signature

Verifying the signature is straightforward. (Note that here we also use
the key pair generated in the key pair example.)

``` {.codeblock dir="ltr"}
   /* Initializing the object with the public key */
   PublicKey pub = pair.getPublic();
   dsa.initVerify(pub);

   /* Update and verify the data */
   dsa.update(data);
   boolean verifies = dsa.verify(sig);
   System.out.println("signature verifies: " + verifies);
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-5514BAFF-5F0F-403C-9943-56A632D6E406}

### Generating/Verifying Signatures Using Key Specifications and KeyFactory {#JSSEC-GUID-5514BAFF-5F0F-403C-9943-56A632D6E406 .sect3}

<div>
Sample code that is used to generate and verify signatures using key
specifications and `KeyFactory`{.codeph}.

<div class="section">
Suppose that, rather than having a public/private key pair (as, for
example, was generated in the [Generating a Pair of
Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-ED6EDA78-8D20-4059-92E1-FBDDE4D3DFE6 "In this example we will generate a public-private key pair for the algorithm named ")
above), you simply have the components of your DSA private key:
`x`{.codeph} (the private key), `p`{.codeph} (the prime), `q`{.codeph}
(the sub-prime), and `g`{.codeph} (the base).

Further suppose you want to use your private key to digitally sign some
data, which is in a byte array named `someData`{.codeph}. You would do
the following steps, which also illustrate creating a key specification
and using a key factory to obtain a `PrivateKey`{.codeph} from the key
specification (`initSign`{.codeph} requires a `PrivateKey`{.codeph}):

``` {.codeblock dir="ltr"}
    DSAPrivateKeySpec dsaPrivKeySpec = new DSAPrivateKeySpec(x, p, q, g);

    KeyFactory keyFactory = KeyFactory.getInstance("DSA");
    PrivateKey privKey = keyFactory.generatePrivate(dsaPrivKeySpec);

    Signature sig = Signature.getInstance("SHA256withDSA");
    sig.initSign(privKey);
    sig.update(someData);
    byte[] signature = sig.sign();
```

Suppose Alice wants to use the data you signed. In order for her to do
so, and to verify your signature, you need to send her three things:

1.  The data
2.  The signature
3.  The public key corresponding to the private key you used to sign the
    data

You can store the `someData`{.codeph} bytes in one file, and the
`signature`{.codeph} bytes in another, and send those to Alice.

For the public key, assume, as in the signing example above, you have
the components of the DSA public key corresponding to the DSA private
key used to sign the data. Then you can create a
`DSAPublicKeySpec`{.codeph} from those components:

``` {.codeblock dir="ltr"}
    DSAPublicKeySpec dsaPubKeySpec = new DSAPublicKeySpec(y, p, q, g);
```

You still need to extract the key bytes so that you can put them in a
file. To do so, you can first call the `generatePublic`{.codeph} method
on the DSA key factory already created in the example above:

``` {.codeblock dir="ltr"}
  
    PublicKey pubKey = keyFactory.generatePublic(dsaPubKeySpec);
```

Then you can extract the (encoded) key bytes via the following:

``` {.codeblock dir="ltr"}
    byte[] encKey = pubKey.getEncoded();
```

You can now store these bytes in a file, and send it to Alice along with
the files containing the data and the signature.

Now, assume Alice has received these files, and she copied the data
bytes from the data file to a byte array named `data`{.codeph}, the
signature bytes from the signature file to a byte array named
`signature`{.codeph}, and the encoded public key bytes from the public
key file to a byte array named `encodedPubKey`{.codeph}.

Alice can now execute the following code to verify the signature. The
code also illustrates how to use a key factory in order to instantiate a
DSA public key from its encoding (`initVerify`{.codeph} requires a
`PublicKey`{.codeph}).

``` {.codeblock dir="ltr"}
    X509EncodedKeySpec pubKeySpec = new X509EncodedKeySpec(encodedPubKey);

    KeyFactory keyFactory = KeyFactory.getInstance("DSA");
    PublicKey pubKey = keyFactory.generatePublic(pubKeySpec);

    Signature sig = Signature.getInstance("SHA256withDSA");
    sig.initVerify(pubKey);
    sig.update(data);
    sig.verify(signature);
```

<div class="p">
<div class="infoboxnote" id="GUID-5514BAFF-5F0F-403C-9943-56A632D6E406__GUID-6139C985-28C3-43D0-8F90-5B1DF9F45ABE">
Note:

In the above, Alice needed to generate a `PublicKey`{.codeph} from the
encoded key bits, since `initVerify`{.codeph} requires a
`PublicKey`{.codeph} . Once she has a `PublicKey`{.codeph}, she could
also use the `KeyFactory`{.codeph}`getKeySpec`{.codeph} method to
convert it to a `DSAPublicKeySpec`{.codeph} so that she can access the
components, if desired, as in:

</div>
</div>
``` {.codeblock dir="ltr"}
    DSAPublicKeySpec dsaPubKeySpec =
        (DSAPublicKeySpec)keyFactory.getKeySpec(pubKey, DSAPublicKeySpec.class);
```

Now she can access the DSA public key components `y`{.codeph},
`p`{.codeph}, `q`{.codeph}, and `g`{.codeph} through the corresponding
\"get\" methods on the `DSAPublicKeySpec`{.codeph} class
(`getY`{.codeph}, `getP`{.codeph}, `getQ`{.codeph}, and
`getG`{.codeph}).

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-36893ED5-E3CA-496B-BC78-B13EE971C736}

### Generating Random Numbers {#JSSEC-GUID-36893ED5-E3CA-496B-BC78-B13EE971C736 .sect3}

<div>
The following code sample illustrates generating random numbers
configured with different security strengths using a DRBG implementation
of the <span class="apiname">SecureRandom</span> class:

<div class="section">
``` {.oac_no_warn dir="ltr"}
    SecureRandom drbg;
    byte[] buffer = new byte[32];

    // Any DRBG can be provided 
    drbg = SecureRandom.getInstance("DRBG");
    drbg.nextBytes(buffer);

    SecureRandomParameters params = drbg.getParameters();
    if (params instanceof DrbgParameters.Instantiation) {
        DrbgParameters.Instantiation ins = (DrbgParameters.Instantiation) params;
        if (ins.getCapability().supportsReseeding()) {
            drbg.reseed();
        }
    } 

    // The following call requests a weak DRBG instance. It is only
    // guaranteed to support 112 bits of security strength.
    drbg = SecureRandom.getInstance("DRBG",
        DrbgParameters.instantiation(112, NONE, null));

    // Both the next two calls will likely fail, because drbg could be
    // instantiated with a smaller strength with no prediction resistance
    // support.
    drbg.nextBytes(buffer,
        DrbgParameters.nextBytes(256, false, "more".getBytes()));
    drbg.nextBytes(buffer,
        DrbgParameters.nextBytes(112, true, "more".getBytes()));

    // The following call requests a strong DRBG instance, with a
    // personalization string. If it successfully returns an instance,
    // that instance is guaranteed to support 256 bits of security strength
    // with prediction resistance available.
    drbg = SecureRandom.getInstance("DRBG", DrbgParameters.instantiation(
        256, PR_AND_RESEED, "hello".getBytes()));

    // Prediction resistance is not requested in this single call,
    // but an additional input is used.
    drbg.nextBytes(buffer,
        DrbgParameters.nextBytes(-1, false, "more".getBytes()));

    // Same for this call.
    drbg.reseed(DrbgParameters.reseed(false, "extra".getBytes()));
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-F7F401C9-63E6-4BE4-9F32-A28B3568EBCC}

### Determining If Two Keys Are Equal {#JSSEC-GUID-F7F401C9-63E6-4BE4-9F32-A28B3568EBCC .sect3}

<div>
Example code for determining if two keys are equal.

<div class="section">
In many cases you would like to know if two keys are equal; however, the
default method `java.lang.Object.equals`{.codeph} may not give the
desired result. The most provider-independent approach is to compare the
encoded keys. If this comparison isn\'t appropriate (for example, when
comparing an `RSAPrivateKey`{.codeph} and an
`RSAPrivateCrtKey`{.codeph}), you should compare each component.

The following code demonstrates this idea:

``` {.codeblock dir="ltr"}
   static boolean keysEqual(Key key1, Key key2) {
       if (key1.equals(key2)) {
          return true;
       }

       if (Arrays.equals(key1.getEncoded(), key2.getEncoded())) {
          return true;
       }

    // More code for different types of keys here.
    // For example, the following code can check if
    // an RSAPrivateKey and an RSAPrivateCrtKey are equal:
    // if ((key1 instanceof RSAPrivateKey) &&
    //     (key2 instanceof RSAPrivateKey)) {
    //     if ((key1.getModulus().equals(key2.getModulus())) &&
    //         (key1.getPrivateExponent().equals(
    //                                      key2.getPrivateExponent()))) {
    //         return true;
    //     }
    // }

        return false;
    }
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-CD24C31B-45FA-480C-AFCA-C108C01689D8}

### Reading Base64-Encoded Certificates {#JSSEC-GUID-CD24C31B-45FA-480C-AFCA-C108C01689D8 .sect3}

<div>
<div class="section">
The following example reads a file with Base64-encoded certificates,
which are each bounded at the beginning by

``` {.codeblock dir="ltr"}
-----BEGIN CERTIFICATE-----
```

and at the end by

``` {.codeblock dir="ltr"}
-----END CERTIFICATE-----
```

We convert the `FileInputStream`{.codeph} (which does not support
`mark`{.codeph} and `reset`{.codeph} ) to a
`ByteArrayInputStream`{.codeph} (which supports those methods), so that
each call to `generateCertificate`{.codeph} consumes only one
certificate, and the read position of the input stream is positioned to
the next certificate in the file:

``` {.codeblock dir="ltr"}
    try (FileInputStream fis = new FileInputStream(filename);
        BufferedInputStream bis = new BufferedInputStream(fis)) {
        CertificateFactory cf = CertificateFactory.getInstance("X.509");
        while (bis.available() > 0) {
            Certificate cert = cf.generateCertificate(bis); 
            System.out.println(cert.toString());
        }
   }
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-8001F1B9-7DBF-4135-A5F3-0042F803E58A}

### Parsing a Certificate Reply {#JSSEC-GUID-8001F1B9-7DBF-4135-A5F3-0042F803E58A .sect3}

<div>
<div class="section">
The following example parses a PKCS7-formatted certificate reply stored
in a file and extracts all the certificates from it:

``` {.codeblock dir="ltr"}
   try (FileInputStream fis = new FileInputStream(filename)) {
      CertificateFactory cf = CertificateFactory.getInstance("X.509");

      Collection<? extends Certificate> c = cf.generateCertificates(fis);
      for (Certificate cert : c) {
          System.out.println(cert);
      }

      // Or use the aggregate operations below for the above for-loop
      // c.stream().forEach(e -> System.out.println(e));
   }
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-AA678E6B-7EAB-44F3-A8CD-F59BEA201BBF}

### Using Encryption {#JSSEC-GUID-AA678E6B-7EAB-44F3-A8CD-F59BEA201BBF .sect3}

<div>
This section takes the user through the process of generating a key,
creating and initializing a cipher object, encrypting a file, and then
decrypting it. Throughout this example, we use the Advanced Encryption
Standard (AES).

<div class="section">
Generating a Key

To create an AES key, we have to instantiate a
<span class="apiname">KeyGenerator</span> for AES. We do not specify a
provider, because we do not care about a particular AES key generation
implementation. Since we do not initialize the
<span class="apiname">KeyGenerator</span>, a system-provided source of
randomness and a default keysize will be used to create the AES key:

``` {.codeblock dir="ltr"}
    KeyGenerator keygen = KeyGenerator.getInstance("AES");
    keygen.init(128);
    SecretKey aesKey = keygen.generateKey();
```

After the key has been generated, the same KeyGenerator object can be
re-used to create further keys.

</div>
<!-- class="section" -->

<div class="section">
Creating a Cipher

The next step is to create a <span class="apiname">Cipher</span>
instance. To do this, we use one of the `getInstance`{.codeph} factory
methods of the <span class="apiname">Cipher</span> class. We must
specify the name of the requested transformation, which includes the
following components, separated by slashes (/):

-   the algorithm name
-   the mode (optional)
-   the padding scheme (optional)

In this example, we create an AES cipher in Cipher Block Chaining mode,
with PKCS5-style padding. We do not specify a provider, because we do
not care about a particular implementation of the requested
transformation.

The standard algorithm name for AES is \"AES\", the standard name for
the Cipher Block Chaining mode is \"CBC\", and the standard name for
PKCS5-style padding is \"PKCS5Padding\":

``` {.codeblock dir="ltr"}
    Cipher aesCipher;

    // Create the cipher
    aesCipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
```

We use the generated `aesKey`{.codeph} from above to initialize the
<span class="apiname">Cipher</span> object for encryption:

``` {.codeblock dir="ltr"}
    // Initialize the cipher for encryption
    aesCipher.init(Cipher.ENCRYPT_MODE, aesKey);

    // Our cleartext
    byte[] cleartext = "This is just an example".getBytes();

    // Encrypt the cleartext
    byte[] ciphertext = aesCipher.doFinal(cleartext);

    // Retrieve the parameters used during encryption to properly  
    // initialize the cipher for decryption
    AlgorithmParameters params = aesCipher.getParameters();

    // Initialize the same cipher for decryption
    aesCipher.init(Cipher.DECRYPT_MODE, aesKey, params);

    // Decrypt the ciphertext
    byte[] cleartext1 = aesCipher.doFinal(ciphertext);
```

`cleartext`{.codeph} and `cleartext1`{.codeph} are identical.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-C9F76AFB-6B20-45A7-B84F-96756C8A94B4}

### Using Password-Based Encryption {#JSSEC-GUID-C9F76AFB-6B20-45A7-B84F-96756C8A94B4 .sect3}

<div>
<div class="section">
In this example, we prompt the user for a password from which we derive
an encryption key.

It would seem logical to collect and store the password in an object of
type `java.lang.String`{.codeph}. However, here\'s the caveat: Objects
of type `String`{.codeph} are immutable, i.e., there are no methods
defined that allow you to change (overwrite) or zero out the contents of
a `String`{.codeph} after usage. This feature makes `String`{.codeph}
objects unsuitable for storing security sensitive information such as
user passwords. You should always collect and store security sensitive
information in a char array instead. For that reason, the
`javax.crypto.spec.PBEKeySpec`{.codeph} class takes (and returns) a
password as a char array.

In order to use Password-Based Encryption (PBE) as defined in PKCS5, we
have to specify a <span class="variable">salt</span> and an
<span class="variable">iteration count</span>. The same salt and
iteration count that are used for encryption must be used for
decryption. Newer PBE algorithms use an iteration count of at least
1000.

``` {.codeblock dir="ltr"}
    PBEKeySpec pbeKeySpec;
    PBEParameterSpec pbeParamSpec;
    SecretKeyFactory keyFac;

    // Salt
    byte[] salt = new SecureRandom().nextBytes(salt);

    // Iteration count
    int count = 1000;

    // Create PBE parameter set
    pbeParamSpec = new PBEParameterSpec(salt, count);

    // Prompt user for encryption password.
    // Collect user password as char array, and convert
    // it into a SecretKey object, using a PBE key
    // factory.
    char[] password = System.console.readPassword("Enter encryption password: ");
    pbeKeySpec = new PBEKeySpec(password);
    keyFac = SecretKeyFactory.getInstance("PBEWithHmacSHA256AndAES_256");
    SecretKey pbeKey = keyFac.generateSecret(pbeKeySpec);

    // Create PBE Cipher
    Cipher pbeCipher = Cipher.getInstance("PBEWithHmacSHA256AndAES_256");

    // Initialize PBE Cipher with key and parameters
    pbeCipher.init(Cipher.ENCRYPT_MODE, pbeKey, pbeParamSpec);

    // Our cleartext
    byte[] cleartext = "This is another example".getBytes();

    // Encrypt the cleartext
    byte[] ciphertext = pbeCipher.doFinal(cleartext);
```

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-725B837C-9DB3-4B9F-A8D8-1E1C72B558E0}

Sample Programs for Diffie-Hellman Key Exchange, AES/GCM, and HMAC-SHA256 {#JSSEC-GUID-725B837C-9DB3-4B9F-A8D8-1E1C72B558E0 .sect2}
-------------------------------------------------------------------------

<div>
The following are sample programs for Diffie-Hellman key exchange,
AES/GCM, and HMAC-SHA256.

<div class="section">
Topics

[Diffie-Hellman Key Exchange between 2
Parties](java-cryptography-architecture-jca-reference-guide.html#GUID-98B5A57E-E5BA-46F2-BE35-2056F43C58A4 "The program runs the Diffie-Hellman key agreement protocol between 2 parties.")

[Diffie-Hellman Key Exchange between 3
Parties](java-cryptography-architecture-jca-reference-guide.html#GUID-3DADAE4E-EBC1-46CE-A47B-A09AD9E2A01E "The program runs the Diffie-Hellman key agreement protocol between 3 parties.")

[AES/GCM
Example](java-cryptography-architecture-jca-reference-guide.html#GUID-BCF9A664-EA76-49C9-AB0C-662FD7542B85 "The following is a sample program to demonstrate AES/GCM usage to encrypt/decrypt data.")

[HMAC-SHA256
Example](java-cryptography-architecture-jca-reference-guide.html#GUID-1B141C6A-7BB3-4DA2-A112-ADEBCE7F4B4A "The following is a sample program that demonstrates how to generate a secret-key object for HMAC-SHA256, and initialize a HMAC-SHA256 object with it.")

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-98B5A57E-E5BA-46F2-BE35-2056F43C58A4}

### Diffie-Hellman Key Exchange between 2 Parties {#JSSEC-GUID-98B5A57E-E5BA-46F2-BE35-2056F43C58A4 .sect3}

<div>
The program runs the Diffie-Hellman key agreement protocol between 2
parties.

<div class="section">
``` {.oac_no_warn dir="ltr"}
/*
 * Copyright (c) 1997, 2017, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle nor the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
import java.io.*;
import java.math.BigInteger;
import java.security.*;
import java.security.spec.*;
import java.security.interfaces.*;
import javax.crypto.*;
import javax.crypto.spec.*;
import javax.crypto.interfaces.*;
import com.sun.crypto.provider.SunJCE;

public class DHKeyAgreement2 {
    private DHKeyAgreement2() {}
    public static void main(String argv[]) throws Exception {
        
        /*
         * Alice creates her own DH key pair with 2048-bit key size
         */
        System.out.println("ALICE: Generate DH keypair ...");
        KeyPairGenerator aliceKpairGen = KeyPairGenerator.getInstance("DH");
        aliceKpairGen.initialize(2048);
        KeyPair aliceKpair = aliceKpairGen.generateKeyPair();
        
        // Alice creates and initializes her DH KeyAgreement object
        System.out.println("ALICE: Initialization ...");
        KeyAgreement aliceKeyAgree = KeyAgreement.getInstance("DH");
        aliceKeyAgree.init(aliceKpair.getPrivate());
        
        // Alice encodes her public key, and sends it over to Bob.
        byte[] alicePubKeyEnc = aliceKpair.getPublic().getEncoded();
        
        /*
         * Let's turn over to Bob. Bob has received Alice's public key
         * in encoded format.
         * He instantiates a DH public key from the encoded key material.
         */
        KeyFactory bobKeyFac = KeyFactory.getInstance("DH");
        X509EncodedKeySpec x509KeySpec = new X509EncodedKeySpec(alicePubKeyEnc);

        PublicKey alicePubKey = bobKeyFac.generatePublic(x509KeySpec);

        /*
         * Bob gets the DH parameters associated with Alice's public key.
         * He must use the same parameters when he generates his own key
         * pair.
         */
        DHParameterSpec dhParamFromAlicePubKey = ((DHPublicKey)alicePubKey).getParams();

        // Bob creates his own DH key pair
        System.out.println("BOB: Generate DH keypair ...");
        KeyPairGenerator bobKpairGen = KeyPairGenerator.getInstance("DH");
        bobKpairGen.initialize(dhParamFromAlicePubKey);
        KeyPair bobKpair = bobKpairGen.generateKeyPair();

        // Bob creates and initializes his DH KeyAgreement object
        System.out.println("BOB: Initialization ...");
        KeyAgreement bobKeyAgree = KeyAgreement.getInstance("DH");
        bobKeyAgree.init(bobKpair.getPrivate());

        // Bob encodes his public key, and sends it over to Alice.
        byte[] bobPubKeyEnc = bobKpair.getPublic().getEncoded();

        /*
         * Alice uses Bob's public key for the first (and only) phase
         * of her version of the DH
         * protocol.
         * Before she can do so, she has to instantiate a DH public key
         * from Bob's encoded key material.
         */
        KeyFactory aliceKeyFac = KeyFactory.getInstance("DH");
        x509KeySpec = new X509EncodedKeySpec(bobPubKeyEnc);
        PublicKey bobPubKey = aliceKeyFac.generatePublic(x509KeySpec);
        System.out.println("ALICE: Execute PHASE1 ...");
        aliceKeyAgree.doPhase(bobPubKey, true);

        /*
         * Bob uses Alice's public key for the first (and only) phase
         * of his version of the DH
         * protocol.
         */
        System.out.println("BOB: Execute PHASE1 ...");
        bobKeyAgree.doPhase(alicePubKey, true);

        /*
         * At this stage, both Alice and Bob have completed the DH key
         * agreement protocol.
         * Both generate the (same) shared secret.
         */
        try {
            byte[] aliceSharedSecret = aliceKeyAgree.generateSecret();
            int aliceLen = aliceSharedSecret.length;
            byte[] bobSharedSecret = new byte[aliceLen];
            int bobLen;
        } catch (ShortBufferException e) {
            System.out.println(e.getMessage());
        }        // provide output buffer of required size
        bobLen = bobKeyAgree.generateSecret(bobSharedSecret, 0);
        System.out.println("Alice secret: " +
                toHexString(aliceSharedSecret));
        System.out.println("Bob secret: " +
                toHexString(bobSharedSecret));
        if (!java.util.Arrays.equals(aliceSharedSecret, bobSharedSecret))
            throw new Exception("Shared secrets differ");
        System.out.println("Shared secrets are the same");

        /*
         * Now let's create a SecretKey object using the shared secret
         * and use it for encryption. First, we generate SecretKeys for the
         * "AES" algorithm (based on the raw shared secret data) and
         * Then we use AES in CBC mode, which requires an initialization
         * vector (IV) parameter. Note that you have to use the same IV
         * for encryption and decryption: If you use a different IV for
         * decryption than you used for encryption, decryption will fail.
         *
         * If you do not specify an IV when you initialize the Cipher
         * object for encryption, the underlying implementation will generate
         * a random one, which you have to retrieve using the
         * javax.crypto.Cipher.getParameters() method, which returns an
         * instance of java.security.AlgorithmParameters. You need to transfer
         * the contents of that object (e.g., in encoded format, obtained via
         * the AlgorithmParameters.getEncoded() method) to the party who will
         * do the decryption. When initializing the Cipher for decryption,
         * the (reinstantiated) AlgorithmParameters object must be explicitly
         * passed to the Cipher.init() method.
         */
        System.out.println("Use shared secret as SecretKey object ...");
        SecretKeySpec bobAesKey = new SecretKeySpec(bobSharedSecret, 0, 16, "AES");
        SecretKeySpec aliceAesKey = new SecretKeySpec(aliceSharedSecret, 0, 16, "AES");

        /*
         * Bob encrypts, using AES in CBC mode
         */
        Cipher bobCipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        bobCipher.init(Cipher.ENCRYPT_MODE, bobAesKey);
        byte[] cleartext = "This is just an example".getBytes();
        byte[] ciphertext = bobCipher.doFinal(cleartext);

        // Retrieve the parameter that was used, and transfer it to Alice in
        // encoded format
        byte[] encodedParams = bobCipher.getParameters().getEncoded();

        /*
         * Alice decrypts, using AES in CBC mode
         */

        // Instantiate AlgorithmParameters object from parameter encoding
        // obtained from Bob
        AlgorithmParameters aesParams = AlgorithmParameters.getInstance("AES");
        aesParams.init(encodedParams);
        Cipher aliceCipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        aliceCipher.init(Cipher.DECRYPT_MODE, aliceAesKey, aesParams);
        byte[] recovered = aliceCipher.doFinal(ciphertext);
        if (!java.util.Arrays.equals(cleartext, recovered))
            throw new Exception("AES in CBC mode recovered text is " +
                    "different from cleartext");
        System.out.println("AES in CBC mode recovered text is "
                "same as cleartext");
    }

    /*
     * Converts a byte to hex digit and writes to the supplied buffer
     */
    private static void byte2hex(byte b, StringBuffer buf) {
        char[] hexChars = { '0', '1', '2', '3', '4', '5', '6', '7', '8',
                '9', 'A', 'B', 'C', 'D', 'E', 'F' };
        int high = ((b & 0xf0) >> 4);
        int low = (b & 0x0f);
        buf.append(hexChars[high]);
        buf.append(hexChars[low]);
    }

    /*
     * Converts a byte array to hex string
     */
    private static String toHexString(byte[] block) {
        StringBuffer buf = new StringBuffer();
        int len = block.length;
        for (int i = 0; i < len; i++) {
            byte2hex(block[i], buf);
            if (i < len-1) {
                buf.append(":");
            }
        }
        return buf.toString();
    }
}
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-3DADAE4E-EBC1-46CE-A47B-A09AD9E2A01E}

### Diffie-Hellman Key Exchange between 3 Parties {#JSSEC-GUID-3DADAE4E-EBC1-46CE-A47B-A09AD9E2A01E .sect3}

<div>
The program runs the Diffie-Hellman key agreement protocol between 3
parties.

<div class="section">
``` {.codeblock dir="ltr"}
/*
 * Copyright (c) 1997, 2017, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle nor the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */
import java.security.*;
import java.security.spec.*;
import javax.crypto.*;
import javax.crypto.spec.*;
import javax.crypto.interfaces.*;
   /*
    * This program executes the Diffie-Hellman key agreement protocol between
    * 3 parties: Alice, Bob, and Carol using a shared 2048-bit DH parameter.
    */
    public class DHKeyAgreement3 {
        private DHKeyAgreement3() {}
        public static void main(String argv[]) throws Exception {
        // Alice creates her own DH key pair with 2048-bit key size
            System.out.println("ALICE: Generate DH keypair ...");
            KeyPairGenerator aliceKpairGen = KeyPairGenerator.getInstance("DH");
            aliceKpairGen.initialize(2048);
            KeyPair aliceKpair = aliceKpairGen.generateKeyPair();
        // This DH parameters can also be constructed by creating a
        // DHParameterSpec object using agreed-upon values
            DHParameterSpec dhParamShared = ((DHPublicKey)aliceKpair.getPublic()).getParams();
        // Bob creates his own DH key pair using the same params
            System.out.println("BOB: Generate DH keypair ...");
            KeyPairGenerator bobKpairGen = KeyPairGenerator.getInstance("DH");
            bobKpairGen.initialize(dhParamShared);
            KeyPair bobKpair = bobKpairGen.generateKeyPair();
        // Carol creates her own DH key pair using the same params
            System.out.println("CAROL: Generate DH keypair ...");
            KeyPairGenerator carolKpairGen = KeyPairGenerator.getInstance("DH");
            carolKpairGen.initialize(dhParamShared);
            KeyPair carolKpair = carolKpairGen.generateKeyPair();
        // Alice initialize
            System.out.println("ALICE: Initialize ...");
            KeyAgreement aliceKeyAgree = KeyAgreement.getInstance("DH");
            aliceKeyAgree.init(aliceKpair.getPrivate());
        // Bob initialize
            System.out.println("BOB: Initialize ...");
            KeyAgreement bobKeyAgree = KeyAgreement.getInstance("DH");
            bobKeyAgree.init(bobKpair.getPrivate());
        // Carol initialize
            System.out.println("CAROL: Initialize ...");
            KeyAgreement carolKeyAgree = KeyAgreement.getInstance("DH");
            carolKeyAgree.init(carolKpair.getPrivate());
        // Alice uses Carol's public key
            Key ac = aliceKeyAgree.doPhase(carolKpair.getPublic(), false);
        // Bob uses Alice's public key
            Key ba = bobKeyAgree.doPhase(aliceKpair.getPublic(), false);
        // Carol uses Bob's public key
            Key cb = carolKeyAgree.doPhase(bobKpair.getPublic(), false);
        // Alice uses Carol's result from above
            aliceKeyAgree.doPhase(cb, true);
        // Bob uses Alice's result from above
            bobKeyAgree.doPhase(ac, true);
        // Carol uses Bob's result from above
            carolKeyAgree.doPhase(ba, true);
        // Alice, Bob and Carol compute their secrets
            byte[] aliceSharedSecret = aliceKeyAgree.generateSecret();
            System.out.println("Alice secret: " + toHexString(aliceSharedSecret));
            byte[] bobSharedSecret = bobKeyAgree.generateSecret();
            System.out.println("Bob secret: " + toHexString(bobSharedSecret));
            byte[] carolSharedSecret = carolKeyAgree.generateSecret();
            System.out.println("Carol secret: " + toHexString(carolSharedSecret));
        // Compare Alice and Bob
            if (!java.util.Arrays.equals(aliceSharedSecret, bobSharedSecret))
                throw new Exception("Alice and Bob differ");
            System.out.println("Alice and Bob are the same");
        // Compare Bob and Carol
            if (!java.util.Arrays.equals(bobSharedSecret, carolSharedSecret))
                throw new Exception("Bob and Carol differ");
            System.out.println("Bob and Carol are the same");
        }
    /*
     * Converts a byte to hex digit and writes to the supplied buffer
     */
        private static void byte2hex(byte b, StringBuffer buf) {
            char[] hexChars = { '0', '1', '2', '3', '4', '5', '6', '7', '8',
                                '9', 'A', 'B', 'C', 'D', 'E', 'F' };
            int high = ((b & 0xf0) >> 4);
            int low = (b & 0x0f);
            buf.append(hexChars[high]);
            buf.append(hexChars[low]);
        }
    /*
     * Converts a byte array to hex string
     */
        private static String toHexString(byte[] block) {
            StringBuffer buf = new StringBuffer();
            int len = block.length;
            for (int i = 0; i < len; i++) {
                byte2hex(block[i], buf);
                if (i < len-1) {
                    buf.append(":");
                }
            }
            return buf.toString();
        }
    }
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-BCF9A664-EA76-49C9-AB0C-662FD7542B85}

### AES/GCM Example {#JSSEC-GUID-BCF9A664-EA76-49C9-AB0C-662FD7542B85 .sect3}

<div>
The following is a sample program to demonstrate AES/GCM usage to
encrypt/decrypt data.

``` {.oac_no_warn dir="ltr"}
/*
 * Copyright (c) 2017, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle nor the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */

import java.security.AlgorithmParameters;
import java.util.Arrays;
import javax.crypto.*;

public class AESGCMTest {

    public static void main(String[] args) throws Exception {
        // Slightly longer than 1 AES block (128 bits) to show PADDING
        // is "handled" by GCM.
        byte[] data = {
            0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07,
            0x08, 0x09, 0x0a, 0x0b, 0x0c, 0x0d, 0x0e, 0x0f,
            0x10};

        // Create a 128-bit AES key.
        KeyGenerator kg = KeyGenerator.getInstance("AES");
        kg.init(128);
        SecretKey key = kg.generateKey();

        // Obtain a AES/GCM cipher to do the enciphering. Must obtain
        // and use the Parameters for successful decryption.
        Cipher encCipher = Cipher.getInstance("AES/GCM/NOPADDING");
        encCipher.init(Cipher.ENCRYPT_MODE, key);
        byte[] enc = encCipher.doFinal(data);
        AlgorithmParameters ap = encCipher.getParameters();

        // Obtain a similar cipher, and use the parameters.
        Cipher decCipher = Cipher.getInstance("AES/GCM/NOPADDING");
        decCipher.init(Cipher.DECRYPT_MODE, key, ap);
        byte[] dec = decCipher.doFinal(enc);

        if (Arrays.compare(data, dec) != 0) {
            throw new Exception("Original data != decrypted data");
        }
    }
}
```

</div>
</div>
<div class="sect3">
[]{#GUID-1B141C6A-7BB3-4DA2-A112-ADEBCE7F4B4A}

### HMAC-SHA256 Example {#JSSEC-GUID-1B141C6A-7BB3-4DA2-A112-ADEBCE7F4B4A .sect3}

<div>
The following is a sample program that demonstrates how to generate a
secret-key object for HMAC-SHA256, and initialize a HMAC-SHA256 object
with it.

<div class="example" id="GUID-1B141C6A-7BB3-4DA2-A112-ADEBCE7F4B4A__GUID-4C1C7226-F8A7-4780-8B85-40DFD7702C31">
Example 2-14 Generate a Secret-key Object for HMAC-SHA256

``` {.codeblock dir="ltr"}
/*
 * Copyright (c) 1997, 2017, Oracle and/or its affiliates. All rights reserved.
 *
 * Redistribution and use in source and binary forms, with or without
 * modification, are permitted provided that the following conditions
 * are met:
 *
 *   - Redistributions of source code must retain the above copyright
 *     notice, this list of conditions and the following disclaimer.
 *
 *   - Redistributions in binary form must reproduce the above copyright
 *     notice, this list of conditions and the following disclaimer in the
 *     documentation and/or other materials provided with the distribution.
 *
 *   - Neither the name of Oracle nor the names of its
 *     contributors may be used to endorse or promote products derived
 *     from this software without specific prior written permission.
 *
 * THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS
 * IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
 * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
 * PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
 * CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
 * EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
 * PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
 * PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF
 * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING
 * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 * SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */

import java.security.*;
import javax.crypto.*;

    /**
     * This program demonstrates how to generate a secret-key object for
     * HMACSHA256, and initialize an HMACSHA256 object with it.
     */

    public class initMac {

        public static void main(String[] args) throws Exception {

            // Generate secret key for HmacSHA256
            KeyGenerator kg = KeyGenerator.getInstance("HmacSHA256");
            SecretKey sk = kg.generateKey();

            // Get instance of Mac object implementing HmacSHA256, and
            // initialize it with the above secret key
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(sk);
            byte[] result = mac.doFinal("Hi There".getBytes());
        }
    }
```

</div>
<!-- class="example" -->

</div>
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
| --------- ---------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| ------- --           | l | dcommon/gifs/toc.gif |
|              [![Prev | e | )\                   |
| ious](../../dcommon/ | L |             <span cl |
| gifs/leftnav.gif)\   | o | ass="icon">Contents< |
|                  [![ | g | /span>](toc.htm)     |
| Next](../../dcommon/ | o |   -- --------------- |
| gifs/rightnav.gif)\  | ] | -------------------- |
|                      | ( | -------------------- |
|    <span class="icon | . | ---                  |
| ">Previous</span>](t | . |                      |
| roubleshooting-secur | / |                      |
| ity.htm)   <span cla | . |                      |
| ss="icon">Next</span | . |                      |
| >](howtoimplaprovide | / |                      |
| r.htm)               | d |                      |
|   ------------------ | c |                      |
| -------------------- | o |                      |
| -------------------- | m |                      |
| --------- ---------- | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| ------- --           | / |                      |
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
