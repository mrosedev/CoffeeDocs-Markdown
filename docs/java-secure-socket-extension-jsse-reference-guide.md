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

  ----------------------------------------------------------------------- ---------------------------------------------------------------- --
               [![Previous](../../dcommon/gifs/leftnav.gif)\                         [![Next](../../dcommon/gifs/rightnav.gif)\            
   <span class="icon">Previous</span>](kerberos-5-gss-api-mechanism.htm)   <span class="icon">Next</span>](running-jsse-sample-code1.htm)  
  ----------------------------------------------------------------------- ---------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345}<!-- End Header -->

<script type="text/javascript">
window.name='java-secure-socket-extension-jsse-reference-guide'
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
<span class="enumeration_chapter">8 </span>Java Secure Socket Extension (JSSE) Reference Guide {#JSSEC-GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345 .sect1}
==============================================================================================

<div>
The Java Secure Socket Extension (JSSE) enables secure Internet
communications. It provides a framework and an implementation for a Java
version of the SSL, TLS, and DTLS protocols and includes functionality
for data encryption, server authentication, message integrity, and
optional client authentication.

</div>
<div class="sect2">
[]{#GUID-0EF5DA4E-856C-4AD2-A9FD-0837C5881DDA}

Introduction to JSSE {#JSSEC-GUID-0EF5DA4E-856C-4AD2-A9FD-0837C5881DDA .sect2}
--------------------

<div>
Data that travels across a network can easily be accessed by someone who
is not the intended recipient. When the data includes private
information, such as passwords and credit card numbers, steps must be
taken to make the data unintelligible to unauthorized parties. It is
also important to ensure that the data has not been modified, either
intentionally or unintentionally, during transport. The Secure Sockets
Layer (SSL) and Transport Layer Security (TLS) protocols were designed
to help protect the privacy and integrity of data while it is being
transferred across a network.

<div class="section">
The Java Secure Socket Extension (JSSE) enables secure Internet
communications. It provides a framework and an implementation for a Java
version of the SSL and TLS protocols and includes functionality for data
encryption, server authentication, message integrity, and optional
client authentication. Using JSSE, developers can provide for the secure
passage of data between a client and a server running any application
protocol (such as HTTP, Telnet, or FTP) over TCP/IP. For an introduction
to SSL, see [Secure Sockets Layer (SSL) Protocol
Overview](java-secure-socket-extension-jsse-reference-guide.htm#GUID-69ECD56C-3B20-47F4-AEF0-A06EFA13A61D "Secure Sockets Layer (SSL) is the most widely used protocol for implementing cryptography on the web. SSL uses a combination of cryptographic processes to provide secure communication over a network. This section provides an introduction to SSL and the cryptographic processes it uses.").

By abstracting the complex underlying security algorithms and
handshaking mechanisms, JSSE minimizes the risk of creating subtle but
dangerous security vulnerabilities. Furthermore, it simplifies
application development by serving as a building block that developers
can integrate directly into their applications.

JSSE provides both an application programming interface (API) framework
and an implementation of that API. The JSSE API supplements the core
network and cryptographic services defined by the
`java.security`{.codeph} and `java.net`{.codeph} packages by providing
extended networking socket classes, trust managers, key managers, SSL
contexts, and a socket factory framework for encapsulating socket
creation behavior. Because the `SSLSocket`{.codeph} class is based on a
blocking I/O model, the Java Development Kit (JDK) includes a
nonblocking `SSLEngine`{.codeph} class to enable implementations to
choose their own I/O methods.

The JSSE API supports the following security protocols:

-   SSL: version 3.0

-   TLS: version 1.0, 1.1, and 1.2

-   DTLS: versions 1.0 and 1.2

These security protocols encapsulate a normal bidirectional stream
socket, and the JSSE API adds transparent support for authentication,
encryption, and integrity protection.sions. Note that the JSSE
implementation that is shipped with the JDK does not implement SSL 2.0.

JSSE is a security component of the Java SE platform, and is based on
the same design principles found elsewhere in the [Java Cryptography
Architecture (JCA) Reference
Guide](java-cryptography-architecture-jca-reference-guide.htm#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.")
framework. This framework for cryptography-related security components
allows them to have implementation independence and, whenever possible,
algorithm independence. JSSE uses the [Cryptographic Service
Providers](java-cryptography-architecture-jca-reference-guide.htm#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920)
defined by the JCA framework.

Other security components in the Java SE platform include the [Java
Authentication and Authorization Service (JAAS) Reference
Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html)
and the [Java Security Tools](olink:JSWOR691). JSSE encompasses many of
the same concepts and algorithms as those in JCA but automatically
applies them underneath a simple stream socket API.

The JSSE API was designed to allow other SSL/TLS/DTLS protocol and
Public Key Infrastructure (PKI) implementations to be plugged in
seamlessly. Developers can also provide alternative logic to determine
if remote hosts should be trusted or what authentication key material
should be sent to a remote host.

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-F069F4ED-DF2C-4B3B-90FB-F89E700CF21A}

### JSSE Features and Benefits {#JSSEC-GUID-F069F4ED-DF2C-4B3B-90FB-F89E700CF21A .sect3}

<div>
JSSE includes the following important benefits and features:

-   Included as a standard component of the JDK
-   Extensible, provider-based architecture
-   Implemented in 100% pure Java
-   Provides API support for SSL/TLS/DTLS
-   Provides implementations of SSL 3.0, TLS (versions 1.0, 1.1, and
    1.2), and DTLS (versions 1.0 and 1.2)
-   Includes classes that can be instantiated to create secure channels
    (`SSLSocket`{.codeph}, `SSLServerSocket`{.codeph}, and
    `SSLEngine`{.codeph})
-   Provides support for cipher suite negotiation, which is part of the
    SSL/TLS/DTLS handshaking used to initiate or verify secure
    communications
-   Provides support for client and server authentication, which is part
    of the normal SSL/TLS/DTLS handshaking
-   Provides support for HTTP encapsulated in the SSL/TLS protocol,
    which allows access to data such as web pages using HTTPS
-   Provides server session management APIs to manage memory-resident
    SSL sessions
-   Provides support for server name indication extension, which
    facilitates secure connections to virtual servers.
-   Provides support for certificate status request extension (OCSP
    stapling), which saves client certificate validation round-trips and
    resources.
-   Provides support for Server Name Indication (SNI) Extension, which
    extends the SSL/TLS/DTLS protocols to indicate what server name the
    client is attempting to connect to during handshaking.
-   Provides support for endpoint identification during handshaking,
    which prevents man-in-the-middle attacks.
-   Provides support for cryptographic algorithm constraints, which
    provides fine-grained control over algorithms negotiated by JSSE.

JSSE uses the following cryptographic algorithms:

<div class="tblformal" id="GUID-F069F4ED-DF2C-4B3B-90FB-F89E700CF21A__GUID-7DC2C301-C20F-4381-9B3F-9376E97783B2">
Table 8-1 Cryptographic Algorithms Used by JSSE

+-----------------------+-----------------------+-----------------------+
| Cryptographic         | Cryptographic         | Key Lengths           |
| Functionality         | Algorithm[^Foot 1^](# | (Bits)[^Foot 2^](#fn_ |
|                       | fn_1){#fn_1}          | 2){#fn_2}             |
+:======================+:======================+:======================+
| Bulk encryption       | Advanced Encryption   | 256[^Foot 3^](#fn_3){ |
|                       | Standard (AES)        | #fn_3}                |
|                       |                       |                       |
|                       |                       | 128                   |
+-----------------------+-----------------------+-----------------------+
| Bulk encryption       | Data Encryption       | 64 (56 effective)     |
|                       | Standard (DES)        |                       |
|                       |                       | 64 (40 effective)     |
+-----------------------+-----------------------+-----------------------+
| Bulk encryption       | Rivest Cipher 4 (RC4) | 128                   |
|                       |                       |                       |
|                       |                       | 128 (40 effective)    |
+-----------------------+-----------------------+-----------------------+
| Bulk encryption       | Triple DES (3DES)     | 192 (112 effective)   |
+-----------------------+-----------------------+-----------------------+
| Hash algorithm        | Message Digest        | 128                   |
|                       | Algorithm (MD5)       |                       |
+-----------------------+-----------------------+-----------------------+
| Hash algorithm        | Secure Hash Algorithm | 160                   |
|                       | 1 (SHA1)              |                       |
+-----------------------+-----------------------+-----------------------+
| Hash algorithm        | Secure Hash Algorithm | 224                   |
|                       | 224 (SHA224)          |                       |
+-----------------------+-----------------------+-----------------------+
| Hash algorithm        | Secure Hash Algorithm | 256                   |
|                       | 256 (SHA256)          |                       |
+-----------------------+-----------------------+-----------------------+
| Hash algorithm        | Secure Hash Algorithm | 384                   |
|                       | 384 (SHA384)          |                       |
+-----------------------+-----------------------+-----------------------+
| Hash algorithm        | Secure Hash Algorithm | 512                   |
|                       | 512 (SHA512)          |                       |
+-----------------------+-----------------------+-----------------------+
| Authentication        | Digital Signature     | 1024, 2048, 3072      |
|                       | Algorithm (DSA)       |                       |
+-----------------------+-----------------------+-----------------------+
| Authentication        | Elliptic Curve        | 160 through 512       |
|                       | Digital Signature     |                       |
|                       | Algorithm (ECDSA)     |                       |
+-----------------------+-----------------------+-----------------------+
| Authentication and    | Rivest-Shamir-Adleman | 512 and larger        |
| key exchange          | (RSA)                 |                       |
+-----------------------+-----------------------+-----------------------+
| Key exchange          | Static Elliptic Curve | 160 through 512       |
|                       | Diffie-Hellman (ECDH) |                       |
+-----------------------+-----------------------+-----------------------+
| Key exchange          | Ephemeral Elliptic    | 160 through 512       |
|                       | Curve Diffie-Hellman  |                       |
|                       | (ECDHE)               |                       |
+-----------------------+-----------------------+-----------------------+
| Key agreement         | Diffie-Hellman (DH)   | 512, 768, 1024, 2048, |
|                       |                       | 3072, 4096, 6144,     |
|                       |                       | 8192                  |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

^Footnote 1^ The SunJSSE implementation uses the [Java Cryptography
Architecture
(JCA)](java-cryptography-architecture-jca-reference-guide.htm#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.")
for all its cryptographic algorithms.

^Footnote 2^ A JSSE provider may disable or deactivate weak algorithms
and weak keys.

^Footnote 3^ Cipher suites that use AES\_256 require the appropriate
Java Cryptography Extension (JCE) unlimited strength jurisdiction policy
file set, which is included in the JDK. By default, the active
cryptography policy is unlimited. See [Cryptographic Strength
Configuration](java-cryptography-architecture-jca-reference-guide.htm#GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1).

</div>
</div>
<div class="sect3">
[]{#GUID-2DF22C2B-C32E-4665-BB4B-E9510865FDC0}

### JSSE Standard API {#JSSEC-GUID-2DF22C2B-C32E-4665-BB4B-E9510865FDC0 .sect3}

<div>
The JSSE standard API, available in the `javax.net`{.codeph} and
`javax.net.ssl`{.codeph} packages, provides:

-   Secure sockets tailored to client and server-side applications.
-   A non-blocking engine for producing and consuming streams of
    SSL/TLS/DTLS data (`SSLEngine`{.codeph}).
-   Factories for creating sockets, server sockets, SSL sockets, and SSL
    server sockets. By using socket factories, you can encapsulate
    socket creation and configuration behavior.
-   A class representing a secure socket context that acts as a factory
    for secure socket factories and engines.
-   Key and trust manager interfaces (including X.509-specific key and
    trust managers), and factories that can be used for creating them.
-   A class for secure HTTP URL connections (HTTPS).

</div>
</div>
<div class="sect3">
[]{#GUID-59EC25A8-4CE4-4D94-896B-8E6FB23C2838}

### SunJSSE Provider {#JSSEC-GUID-59EC25A8-4CE4-4D94-896B-8E6FB23C2838 .sect3}

<div>
Oracle\'s implementation of Java SE includes a JSSE provider named
<span class="variable">SunJSSE</span>, which comes preinstalled and
preregistered with the JCA. This provider supplies the following
cryptographic services:

-   An implementation of the SSL 3.0, TLS (versions 1.0, 1.1, and 1.2),
    and DTLS (versions 1.0 and 1.2) security protocols.
-   An implementation of the most common SSL, TLS, and DTLS cipher
    suites. This implementation encompasses a combination of
    authentication, key agreement, encryption, and integrity protection.
-   An implementation of an X.509-based key manager that chooses
    appropriate authentication keys from a standard JCA keystore.
-   An implementation of an X.509-based trust manager that implements
    rules for certificate chain path validation.

See [The SunJSSE
Provider](oracle-providers.htm#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2).

</div>
</div>
<div class="sect3">
[]{#GUID-DF5DA7C2-7B13-4341-B8F2-E4A64F8C0FFA}

### JSSE Related Documentation {#JSSEC-GUID-DF5DA7C2-7B13-4341-B8F2-E4A64F8C0FFA .sect3}

<div>
The following list contains links to online documentation and names of
books about related subjects:

<div class="section">
JSSE API Documentation

-   [<span class="apiname">javax.net</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/package-summary.html)
    package

-   [<span class="apiname">javax.net.ssl</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/package-summary.html)
    package

</div>
<!-- class="section" -->

<div class="section">
Java SE Security

-   The [Java SE
    Security](http://www.oracle.com/technetwork/java/javase/tech/index-jsp-136007.html)
    home page

-   The [Security Features in Java
    SE](https://docs.oracle.com/javase/tutorial/security/) trail of the
    Java Tutorial

-   [Java PKI Programmers
    Guide](java-pki-programmers-guide.htm#GUID-650D0D53-B617-4055-AFD3-AF5C2629CBBF "The Java Certification Path API consists of classes and interfaces for handling certification paths, which are also called certification chains. If a certification path meets certain validation rules, it may be used to securely establish the mapping of a public key to a subject.")

-   [Inside Java 2 Platform Security, Second Edition: Architecture, API
    Design and
    Implementation](http://www.oracle.com/technetwork/java/javaee/gong-135902.html)

</div>
<!-- class="section" -->

<div class="section">
Cryptography

-   The [Cryptography and
    Security](http://people.csail.mit.edu/rivest/crypto-security.html)
    page by Dr. Ronald L. Rivest (no longer maintained)

-   <cite>Applied Cryptography</cite>, Second Edition by Bruce Schneier.
    John Wiley and Sons, Inc., 1996.

-   <cite>Cryptography Theory and Practice</cite> by Doug Stinson. CRC
    Press, Inc., 1995. Third edition published in 2005.

-   <cite>Cryptography & Network Security: Principles & Practice</cite>
    by William Stallings. Prentice Hall, 1998. Fifth edition published
    in 2010.

</div>
<!-- class="section" -->

<div class="section">
Secure Sockets Layer (SSL)

-   [The Secure Sockets Layer (SSL) Protocol Version 3.0
    RFC](https://www.rfc-editor.org/rfc/rfc6101.txt)

-   [The TLS Protocol Version 1.0
    RFC](http://www.ietf.org/rfc/rfc2246.txt)

-   [HTTP Over TLS RFC](http://www.ietf.org/rfc/rfc2818.txt)

-   <cite>SSL and TLS: Designing and Building Secure Systems</cite> by
    Eric Rescorla. Addison Wesley Professional, 2000.

-   <cite>SSL and TLS Essentials: Securing the Web</cite> by Stephen
    Thomas. John Wiley and Sons, Inc., 2000.

-   <cite>Java 2 Network Security</cite>, Second Edition, by Marco
    Pistoia, Duane F Reller, Deepak Gupta, Milind Nagnur, and Ashok K
    Ramani. Prentice Hall, 1999.

</div>
<!-- class="section" -->

<div class="section">
Transport Layer Security (TLS)

-   [The TLS Protocol Version 1.0
    RFC](http://www.ietf.org/rfc/rfc2246.txt)

-   [The TLS Protocol Version 1.1
    RFC](https://www.ietf.org/rfc/rfc4346.txt)

-   [The TLS Protocol Version 1.2
    RFC](https://www.ietf.org/rfc/rfc5246.txt)

-   [Transport Layer Security (TLS)
    Extensions](https://tools.ietf.org/html/rfc6066.txt)

-   [HTTP Over TLS RFC](http://www.ietf.org/rfc/rfc2818.txt)

</div>
<!-- class="section" -->

<div class="section">
Datagram Transport Layer Security (DTLS)

-   [The DTLS Protocol Version 1.0
    RFC](https://tools.ietf.org/html/rfc4347.txt)

-   [The DTLS Protocol Version 1.2
    RFC](https://tools.ietf.org/html/rfc6347.txt)

</div>
<!-- class="section" -->

<div class="section">
U.S. Encryption Policies

-   [U.S. Department of Commerce](http://www.commerce.gov/)

-   [Technology CEO Council](http://www.techceocouncil.org)

-   Current export policies: [Encryption and Export Administration
    Regulations
    (EAR)](https://www.bis.doc.gov/index.php/policy-guidance/encryption)

-   [NIST Computer Security
    Publications](http://csrc.nist.gov/publications/index.html)

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329}

Terms and Definitions {#JSSEC-GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329 .sect2}
---------------------

<div>
The following are commonly used cryptography terms and their
definitions.

<div class="section">

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-075E9DFF-524E-4884-876F-34F1AA3882AA}authentication

:   The process of confirming the identity of a party with whom one is
    communicating.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-7FF9BA53-CF01-4D61-A040-D569A1A49EDE}certificate

:   A digitally signed statement vouching for the identity and public
    key of an entity (person, company, and so on). Certificates can
    either be self-signed or issued by a Certificate Authority (CA) an
    entity that is trusted to issue valid certificates for other
    entities. Well-known CAs include Comodo, Entrust, and GoDaddy. X509
    is a common certificate format that can be managed by the JDK\'s
    `keytool`{.codeph}.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-AA9858E7-5643-40A3-B495-83C296EBC4BB}cipher suite

:   A combination of cryptographic parameters that define the security
    algorithms and key sizes used for authentication, key agreement,
    encryption, and integrity protection.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-909E701D-8DA3-4DA2-8270-EEF43AE39BEB}cryptographic hash function

:   An algorithm that is used to produce a relatively small fixed-size
    string of bits (called a hash) from an arbitrary block of data. A
    cryptographic hash function is similar to a checksum and has three
    primary characteristics: it's a one-way function, meaning that it is
    not possible to produce the original data from the hash; a small
    change in the original data produces a large change in the resulting
    hash; and it doesn't require a cryptographic key.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-60304F31-E57E-4DF6-8A0F-ED84B5EDEFBF}Cryptographic Service Provider (CSP)

:   Sometimes referred to simply as
    [providers](java-cryptography-architecture-jca-reference-guide.htm#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920)
    for short, the Java Cryptography Architecture (JCA) defines it as a
    package (or set of packages) that implements one or more engine
    classes for specific cryptographic algorithms. An engine class
    defines a cryptographic service in an abstract fashion without a
    concrete implementation.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-6649F852-7B07-422E-B564-31C78CE6F722}Datagram Transport Layer Security (DTLS) Protocol

:   A protocol that manages client and server authentication, data
    integrity, and encrypted communication between the client and server
    based on an unreliable transport channel such as UDP.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-AA38F0B8-97E2-410E-BAA4-4BECE30D36A5}decryption

:   See
    [encryption/decryption](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__ENCRYPTION_DECRYPTION_TERM_JSSEREFGUIDE).

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-2BBD1416-FE35-4349-B19E-00DBAE4A2157}digital signature

:   A digital equivalent of a handwritten signature. It is used to
    ensure that data transmitted over a network was sent by whoever
    claims to have sent it and that the data has not been modified in
    transit. For example, an RSA-based digital signature is calculated
    by first computing a cryptographic hash of the data and then
    encrypting the hash with the sender\'s private key.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-0DEFA86F-0CD5-47F0-B646-A839235155D2}encryption/decryption

:   Encryption is the process of using a complex algorithm to convert an
    original message (<span>cleartext</span>) to an encoded message
    (<span>ciphertext</span>) that is unintelligible unless it is
    decrypted. Decryption is the inverse process of producing cleartext
    from ciphertext.

    The algorithms used to encrypt and decrypt data typically come in
    two categories: secret key (<span>symmetric</span>) cryptography and
    public key (<span>asymmetric</span>) cryptography.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-25F35B62-4DF2-41E8-AB27-4CAEE441D1BC}endpoint identification

:   An IPv4 or IPv6 address used to identify an endpoint on the network.

    Endpoint identification procedures are handled during SSL/TLS
    handshake.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-1B478F10-1ADC-4F49-9A48-EAE466C590CE}handshake protocol

:   The negotiation phase during which the two socket peers agree to use
    a new or existing session. The handshake protocol is a series of
    messages exchanged over the record protocol. At the end of the
    handshake, new connection-specific encryption and integrity
    protection keys are generated based on the key agreement secrets in
    the session.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-56B237A2-73C5-4403-9B88-A875D527F7E8}<span class="italic">java-home</span>

:   Variable placeholder used throughout this document to refer to the
    directory where the Java Development Kit (JDK) is installed.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-D64212F7-DDE3-44E4-8CE1-9321BA096EC6}key agreement

:   A method by which two parties cooperate to establish a common key.
    Each side generates some data, which is exchanged. These two pieces
    of data are then combined to generate a key. Only those holding the
    proper private initialization data can obtain the final key.
    Diffie-Hellman (DH) is the most common example of a key agreement
    algorithm.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-C11E0DE5-5263-42BE-8E22-45A6B8497484}key exchange

:   A method by which keys are exchanged. One side generates a private
    key and encrypts it using the peer\'s public key (typically RSA).
    The data is transmitted to the peer, who decrypts the key using the
    corresponding private key.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-D7CAC72A-2714-4C9B-88E2-7F317DE94CEE}key manager/trust manager

:   Key managers and trust managers use keystores for their key
    material. A key manager manages a keystore and supplies public keys
    to others as needed (for example, for use in authenticating the user
    to others). A trust manager decides who to trust based on
    information in the truststore it manages.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-E3D57C3C-21D3-47E2-95BC-1B2825E8AFCB}keystore/truststore

:   A keystore is a database of key material. Key material is used for a
    variety of purposes, including authentication and data integrity.
    Various types of keystores are available, including PKCS12 and
    Oracle\'s JKS.

    Generally speaking, keystore information can be grouped into two
    categories: key entries and trusted certificate entries. A key entry
    consists of an entity\'s identity and its private key, and can be
    used for a variety of cryptographic purposes. In contrast, a trusted
    certificate entry contains only a public key in addition to the
    entity\'s identity. Thus, a trusted certificate entry can't be used
    where a private key is required, such as in a
    `javax.net.ssl.KeyManager`{.codeph}. In the JDK implementation of
    JKS, a keystore may contain both key entries and trusted certificate
    entries.

    A truststore is a keystore that is used when making decisions about
    what to trust. If you receive data from an entity that you already
    trust, and if you can verify that the entity is the one that it
    claims to be, then you can assume that the data really came from
    that entity.

    An entry should only be added to a truststore if the user trusts
    that entity. By either generating a key pair or by importing a
    certificate, the user gives trust to that entry. Any entry in the
    truststore is considered a trusted entry.

    It may be useful to have two different keystore files: one
    containing just your key entries, and the other containing your
    trusted certificate entries, including CA certificates. The former
    contains private information, whereas the latter does not. Using two
    files instead of a single keystore file provides a cleaner
    separation of the logical distinction between your own certificates
    (and corresponding private keys) and others\' certificates. To
    provide more protection for your private keys, store them in a
    keystore with restricted access, and provide the trusted
    certificates in a more publicly accessible keystore if needed.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-4B34D2B2-316D-486B-9472-56AAA9C25C6A}message authentication code (MAC)

:   Provides a way to check the integrity of information transmitted
    over or stored in an unreliable medium, based on a secret key.
    Typically, MACs are used between two parties that share a secret key
    in order to validate information transmitted between these parties.

    A MAC mechanism that is based on cryptographic hash functions is
    referred to as HMAC. HMAC can be used with any cryptographic hash
    function, such as Message Digest 5 (MD5) and the Secure Hash
    Algorithm (SHA-256), in combination with a secret shared key. HMAC
    is specified in RFC 2104.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-7DFACB29-B03D-4FCF-B0F6-3A03D703AE37}public-key cryptography

:   A cryptographic system that uses an encryption algorithm in which
    two keys are produced. One key is made public, whereas the other is
    kept private. The public key and the private key are cryptographic
    inverses; what one key encrypts only the other key can decrypt.
    Public-key cryptography is also called <span>asymmetric
    cryptography</span>.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-1270AA98-9C99-475F-B98E-5A4B36F2D772}Record Protocol

:   A protocol that packages all data (whether application-level or as
    part of the handshake process) into discrete records of data much
    like a TCP stream socket converts an application byte stream into
    network packets. The individual records are then protected by the
    current encryption and integrity protection keys.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-92FD0D23-A4E1-4472-87D3-E569B0BD206F}secret-key cryptography

:   A cryptographic system that uses an encryption algorithm in which
    the same key is used both to encrypt and decrypt the data.
    Secret-key cryptography is also called <span>symmetric
    cryptography</span>.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-1EAB6FA7-7147-45D0-AAA1-9B3C82616A38}Secure Sockets Layer (SSL) Protocol

:   A protocol that manages client and server authentication, data
    integrity, and encrypted communication between the client and
    server.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-9CDD96C7-62D6-436A-ACF0-900C955673EC}session

:   A named collection of state information including authenticated peer
    identity, cipher suite, and key agreement secrets that are
    negotiated through a secure socket handshake and that can be shared
    among multiple secure socket instances.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-F6D857BB-D1B9-4E43-AEB4-FB6840216E6D}Transport Layer Security (TLS) Protocol

:   A protocol that manages client and server authentication, data
    integrity, and encrypted communication between the client and server
    based on a reliable transport channel such as TCP.

    TLS 1 is the successor of the SSL 3.0 protocol.

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-8E9201DB-D0D5-4DFB-AB72-CDBF7C797D92}trust manager

:   See [\"key manager/trust
    manager\"](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-D7CAC72A-2714-4C9B-88E2-7F317DE94CEE).

[<!-- -->]{#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-4B18A49C-1C39-49B9-B650-AA22C80AF68D}truststore

:   See
    [\"keystore/truststore\"](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329__GUID-E3D57C3C-21D3-47E2-95BC-1B2825E8AFCB).

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-69ECD56C-3B20-47F4-AEF0-A06EFA13A61D}

Secure Sockets Layer (SSL) Protocol Overview {#JSSEC-GUID-69ECD56C-3B20-47F4-AEF0-A06EFA13A61D .sect2}
--------------------------------------------

<div>
Secure Sockets Layer (SSL) is the most widely used protocol for
implementing cryptography on the web. SSL uses a combination of
cryptographic processes to provide secure communication over a network.
This section provides an introduction to SSL and the cryptographic
processes it uses.

<div class="section">
SSL provides a secure enhancement to the standard TCP/IP sockets
protocol used for Internet communications. As shown in [Table
8-2](java-secure-socket-extension-jsse-reference-guide.htm#GUID-69ECD56C-3B20-47F4-AEF0-A06EFA13A61D__GUID-44FB6EEC-B8FB-410E-8FB8-8E74A2F6CC06 "List of protocols supported in each layer of the TCP/IP protocol stack."),
the secure sockets layer is added between the transport layer and the
application layer in the standard TCP/IP protocol stack. The application
most commonly used with SSL is Hypertext Transfer Protocol (HTTP), the
protocol for Internet web pages. Other applications, such as Net News
Transfer Protocol (NNTP), Telnet, Lightweight Directory Access Protocol
(LDAP), Interactive Message Access Protocol (IMAP), and File Transfer
Protocol (FTP), can be used with SSL as well.

<div class="tblformal" id="GUID-69ECD56C-3B20-47F4-AEF0-A06EFA13A61D__GUID-44FB6EEC-B8FB-410E-8FB8-8E74A2F6CC06">
Table 8-2 TCP/IP Protocol Stack with SSL

  TCP/IP Layer           Protocol
  ---------------------- ------------------------------------
  Application Layer      HTTP, NNTP, Telnet, FTP, and so on
  Secure Sockets Layer   SSL
  Transport Layer        TCP
  Internet Layer         IP

</div>
<!-- class="inftblhruleinformal" -->

SSL was developed by Netscape in 1994, and with input from the Internet
community, has evolved to become a standard. It is now under the control
of the international standards organization, the Internet Engineering
Task Force (IETF). The IETF renamed SSL to Transport Layer Security
(TLS), and released the first specification, version 1.0, in January
1999. TLS 1.0 is a modest upgrade to the most recent version of SSL,
version 3.0. This upgrade corrected defects in previous versions and
prohibited the use of known weak algorithms. TLS 1.1 was released in
April 2006, and TLS 1.2 in August 2008.

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-4F882170-B4A9-4E61-8411-6D7194B32FED}

### Why Use SSL? {#JSSEC-GUID-4F882170-B4A9-4E61-8411-6D7194B32FED .sect3}

<div>
Transferring sensitive information over a network can be risky due to
the following issues:

-   You can't always be sure that the entity with whom you are
    communicating is really who you think it is.
-   Network data can be intercepted, so it's possible that it can be
    read by an unauthorized third party, sometimes known as an attacker.
-   An attacker who intercepts data may be able to modify it before
    sending it on to the receiver.

SSL addresses each of these issues. It addresses the first issue by
optionally allowing each of two communicating parties to ensure the
identity of the other party in a process called authentication. After
the parties are authenticated, SSL provides an encrypted connection
between the two parties for secure message transmission. Encrypting the
communication between the two parties provides privacy and therefore
addresses the second issue. The encryption algorithms used with SSL
include a secure hash function, which is similar to a checksum. This
ensures that data isn't modified in transit. The secure hash function
addresses the third issue of data integrity.

<div class="infoboxnote" id="GUID-4F882170-B4A9-4E61-8411-6D7194B32FED__GUID-54858195-D682-43E1-BC8F-07ED16B4211C">
Note:

Both authentication and encryption are optional and depend on the
negotiated cipher suites between the two entities.

</div>
An e-commerce transaction is an obvious example of when to use SSL. In
an e-commerce transaction, it would be foolish to assume that you can
guarantee the identity of the server with whom you are communicating. It
would be easy enough for someone to create a phony website promising
great services if only you enter your credit card number. SSL allows
you, the client, to authenticate the identity of the server. It also
allows the server to authenticate the identity of the client, although
in Internet transactions, this is seldom done.

After the client and the server are comfortable with each other\'s
identity, SSL provides privacy and data integrity through the encryption
algorithms that it uses. This allows sensitive information, such as
credit card numbers, to be transmitted securely over the Internet.

Although SSL provides authentication, privacy, and data integrity, it
doesn't provide nonrepudiation services. <span>Nonrepudiation</span>
means that an entity that sends a message can't later deny sending it.
When the digital equivalent of a signature is associated with a message,
the communication can later be proved. SSL alone does not provide
nonrepudiation.

</div>
</div>
<div class="sect3">
[]{#GUID-83C9697A-35B7-4962-972F-06795E705BE9}

### How SSL Works {#JSSEC-GUID-83C9697A-35B7-4962-972F-06795E705BE9 .sect3}

<div>
One of the reasons that SSL is effective is that it uses several
different cryptographic processes. SSL uses public-key cryptography to
provide authentication, and secret-key cryptography with hash functions
to provide for privacy and data integrity. Before you can understand
SSL, it's helpful to understand these cryptographic processes.

</div>
</div>
<div class="sect3">
[]{#GUID-AE5F865E-126F-4EF2-8333-DBEB879E06EC}

### Cryptographic Processes {#JSSEC-GUID-AE5F865E-126F-4EF2-8333-DBEB879E06EC .sect3}

<div>
The primary purpose of cryptography is to make it difficult for an
unauthorized third party to access and understand private communication
between two parties. It is not always possible to restrict all
unauthorized access to data, but private data can be made unintelligible
to unauthorized parties through the process of encryption. Encryption
uses complex algorithms to convert the original message (cleartext) to
an encoded message (ciphertext). The algorithms used to encrypt and
decrypt data that is transferred over a network typically come in two
categories: secret-key cryptography and public-key cryptography.

<div class="section">
Both secret-key cryptography and public-key cryptography depend on the
use of an agreed-upon cryptographic key or pair of keys. A key is a
string of bits that is used by the cryptographic algorithm or algorithms
during the process of encrypting and decrypting the data. A
cryptographic key is like a key for a lock; only with the right key can
you open the lock.

Safely transmitting a key between two communicating parties is not a
trivial matter. A public key certificate enables a party to safely
transmit its public key, while providing assurance to the receiver of
the authenticity of the public key. See [Public Key
Certificates](java-secure-socket-extension-jsse-reference-guide.htm#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1).

The descriptions of the cryptographic processes in secret-key
cryptography and public-key cryptography follow conventions widely used
by the security community: the two communicating parties are labeled
with the names Alice and Bob. The unauthorized third party, also known
as the attacker, is named Charlie.

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-D2F6DDC1-9689-4BC2-B6D5-4EA13596AEB0}

#### Secret-Key Cryptography {#JSSEC-GUID-D2F6DDC1-9689-4BC2-B6D5-4EA13596AEB0 .sect4}

<div>
With secret-key cryptography, both communicating parties, Alice and Bob,
use the same key to encrypt and decrypt the messages. Before any
encrypted data can be sent over the network, both Alice and Bob must
have the key and must agree on the cryptographic algorithm that they
will use for encryption and decryption

One of the major problems with secret-key cryptography is the logistical
issue of how to get the key from one party to the other without allowing
access to an attacker. If Alice and Bob are securing their data with
secret-key cryptography, and if Charlie gains access to their key, then
Charlie can understand any secret messages he intercepts between Alice
and Bob. Not only can Charlie decrypt Alice\'s and Bob\'s messages, but
he can also pretend that he is Alice and send encrypted data to Bob. Bob
won't know that the message came from Charlie, not Alice.

After the problem of secret key distribution is solved, secret-key
cryptography can be a valuable tool. The algorithms provide excellent
security and encrypt data relatively quickly. The majority of the
sensitive data sent in an SSL session is sent using secret-key
cryptography.

Secret-key cryptography is also called <span>symmetric
cryptography</span> because the same key is used to both encrypt and
decrypt the data. Well-known secret-key cryptographic algorithms include
Advanced Encryption Standard (AES), Triple Data Encryption Standard
(3DES), and Rivest Cipher 4 (RC4).

</div>
</div>
<div class="sect4">
[]{#GUID-0B0D23FF-1AE8-42FC-95F2-3767833D5E86}

#### Public-Key Cryptography {#JSSEC-GUID-0B0D23FF-1AE8-42FC-95F2-3767833D5E86 .sect4}

<div>
Public-key cryptography solves the logistical problem of key
distribution by using both a public key and a private key. The public
key can be sent openly through the network while the private key is kept
private by one of the communicating parties. The public and the private
keys are cryptographic inverses of each other; what one key encrypts,
the other key will decrypt.

Assume that Bob wants to send a secret message to Alice using public-key
cryptography. Alice has both a public key and a private key, so she
keeps her private key in a safe place and sends her public key to Bob.
Bob encrypts the secret message to Alice using Alice\'s public key.
Alice can later decrypt the message with her private key.

If Alice encrypts a message using her private key and sends the
encrypted message to Bob, then Bob can be sure that the data he receives
comes from Alice; if Bob can decrypt the data with Alice\'s public key,
the message must have been encrypted by Alice with her private key, and
only Alice has Alice\'s private key. The problem is that anybody else
can read the message as well because Alice\'s public key is public.
Although this scenario does not allow for secure data communication, it
does provide the basis for digital signatures. A digital signature is
one of the components of a public key certificate, and is used in SSL to
authenticate a client or a server. See [Public Key
Certificates](java-secure-socket-extension-jsse-reference-guide.htm#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1)
and [Digital
Signatures](java-secure-socket-extension-jsse-reference-guide.htm#GUID-ECC35863-046D-40D4-8B74-5F0150D4342A "Once a cryptographic hash is created for a message, the hash is encrypted with the sender's private key. This encrypted hash is called a digital signature.").

Public-key cryptography is also called <span class="italic">asymmetric
cryptography</span> because different keys are used to encrypt and
decrypt the data. A well-known public key cryptographic algorithm often
used with SSL is the Rivest Shamir Adleman (RSA) algorithm. Another
public key algorithm used with SSL that is designed specifically for
secret key exchange is the Diffie-Hellman (DH) algorithm. Public-key
cryptography requires extensive computations, making it very slow. It is
therefore typically used only for encrypting small pieces of data, such
as secret keys, rather than for the bulk of encrypted data
communications.

</div>
</div>
<div class="sect4">
[]{#GUID-694CE95C-6E3C-4F0E-9ABB-E8DCA655EAA7}

#### Comparison Between Secret-Key and Public-Key Cryptography {#JSSEC-GUID-694CE95C-6E3C-4F0E-9ABB-E8DCA655EAA7 .sect4}

<div>
Both secret-key cryptography and public-key cryptography have strengths
and weaknesses. With secret-key cryptography, data can be encrypted and
decrypted quickly, but because both communicating parties must share the
same secret key information, the logistics of exchanging the key can be
a problem. With public-key cryptography, key exchange is not a problem
because the public key does not need to be kept secret, but the
algorithms used to encrypt and decrypt data require extensive
computations, and are therefore very slow

</div>
</div>
<div class="sect4">
[]{#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1}

#### Public Key Certificates {#JSSEC-GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1 .sect4}

<div>
<div class="section">
A public key certificate provides a safe way for an entity to pass on
its public key to be used in asymmetric cryptography. The public key
certificate avoids the following situation: if Charlie creates his own
public key and private key, he can claim that he is Alice and send his
public key to Bob. Bob will be able to communicate with Charlie, but Bob
will think that he is sending his data to Alice.

A public key certificate can be thought of as the digital equivalent of
a passport. It is issued by a trusted organization and provides
identification for the bearer. A trusted organization that issues public
key certificates is known as a Certificate Authority (CA). The CA can be
likened to a notary public. To obtain a certificate from a CA, one must
provide proof of identity. Once the CA is confident that the applicant
represents the organization it says it represents, the CA signs the
certificate attesting to the validity of the information contained
within the certificate.

A public key certificate contains the following fields:

[<!-- -->]{#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1__GUID-DF67D8BF-E90F-4CE0-966A-285C7EE4D31E}Issuer
:   The CA that issued the certificate. If a user trusts the CA that
    issued the certificate, and if the certificate is valid, then the
    user can trust the certificate.

[<!-- -->]{#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1__GUID-3C068594-4632-4DDA-9727-1F3A6091C943}Period of validity
:   A certificate has an expiration date. This date should be checked
    when verifying the validity of a certificate.

[<!-- -->]{#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1__GUID-56FADB73-2F48-4C4A-9530-DF911AEA23E3}Subject
:   Includes information about the entity that the certificate
    represents.

[<!-- -->]{#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1__GUID-5DFE9BC0-59C1-4755-A986-6864F3DC58A1}Subject\'s public key
:   The primary piece of information that the certificate provides is
    the subject\'s public key. All the other fields are provided to
    ensure the validity of this key.

[<!-- -->]{#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1__GUID-8AEA3D0D-F256-46CE-ABD1-2D381BBE91B6}Signature
:   The certificate is digitally signed by the CA that issued the
    certificate. The signature is created using the CA\'s private key
    and ensures the validity of the certificate. Because only the
    certificate is signed, not the data sent in the SSL transaction, SSL
    does not provide for nonrepudiation.

If Bob only accepts Alice\'s public key as valid when she sends it in a
public key certificate, then Bob won't be fooled into sending secret
information to Charlie when Charlie masquerades as Alice.

Multiple certificates may be linked in a certificate chain. When a
certificate chain is used, the first certificate is always that of the
sender. The next is the certificate of the entity that issued the
sender\'s certificate. If more certificates are in the chain, then each
is that of the authority that issued the previous certificate. The final
certificate in the chain is the certificate for a root CA. A root CA is
a public Certificate Authority that is widely trusted. Information for
several root CAs is typically stored in the client\'s Internet browser.
This information includes the CA\'s public key. Well-known CAs include
VeriSign, Entrust, and GTE CyberTrust.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-86CD4C06-0B0F-4B0F-9C41-3EDC5658F491}

#### Cryptographic Hash Functions {#JSSEC-GUID-86CD4C06-0B0F-4B0F-9C41-3EDC5658F491 .sect4}

<div>
When sending encrypted data, SSL typically uses a cryptographic hash
function to ensure data integrity. The hash function prevents Charlie
from tampering with data that Alice sends to Bob.

A cryptographic hash function is similar to a checksum. The main
difference is that whereas a checksum is designed to detect accidental
alterations in data, a cryptographic hash function is designed to detect
deliberate alterations. When data is processed by a cryptographic hash
function, a small string of bits, known as a <span>hash</span>, is
generated. The slightest change to the message typically makes a large
change in the resulting hash. A cryptographic hash function does not
require a cryptographic key. A hash function often used with SSL is
Secure Hash Algorithm (SHA). SHA was proposed by the [U.S. National
Institute of Standards and Technology
(NIST)](http://www.nist.gov/index.html).

</div>
</div>
<div class="sect4">
[]{#GUID-0EB1B09A-0B04-43EA-873D-1E7EE325010D}

#### Message Authentication Code {#JSSEC-GUID-0EB1B09A-0B04-43EA-873D-1E7EE325010D .sect4}

<div>
A message authentication code (MAC) is similar to a cryptographic hash,
except that it is based on a secret key. When secret key information is
included with the data that is processed by a cryptographic hash
function, then the resulting hash is known as an HMAC.

If Alice wants to be sure that Charlie does not tamper with her message
to Bob, then she can calculate an HMAC for her message and append the
HMAC to her original message. She can then encrypt the message plus the
HMAC using a secret key that she shares with Bob. When Bob decrypts the
message and calculates the HMAC, he will be able to tell if the message
was modified in transit. With SSL, an HMAC is used with the transmission
of secure data.

</div>
</div>
<div class="sect4">
[]{#GUID-ECC35863-046D-40D4-8B74-5F0150D4342A}

#### Digital Signatures {#JSSEC-GUID-ECC35863-046D-40D4-8B74-5F0150D4342A .sect4}

<div>
Once a cryptographic hash is created for a message, the hash is
encrypted with the sender\'s private key. This encrypted hash is called
a digital signature.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B}

### The SSL Handshake {#JSSEC-GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B .sect3}

<div>
Communication using SSL begins with an exchange of information between
the client and the server. This exchange of information is called the
SSL handshake. The SSL handshake includes the following stages:

1.  <span class="bold">Negotiating the cipher suite</span>

    The SSL session begins with a negotiation between the client and the
    server as to which cipher suite they will use. A <span>cipher
    suite</span> is a set of cryptographic algorithms and key sizes that
    a computer can use to encrypt data. The cipher suite includes
    information about the public key exchange algorithms or key
    agreement algorithms, and cryptographic hash functions. The client
    tells the server which cipher suites it has available, and the
    server chooses the best mutually acceptable cipher suite.

2.  <span class="bold">Authenticating the server\'s identity
    (optional)</span>

    In SSL, the authentication step is optional, but in the example of
    an e-commerce transaction over the web, the client will generally
    want to authenticate the server. Authenticating the server allows
    the client to be sure that the server represents the entity that the
    client believes the server represents.

    To prove that a server belongs to the organization that it claims to
    represent, the server presents its public key certificate to the
    client. If this certificate is valid, then the client can be sure of
    the identity of the server.

    The client and server exchange information that allows them to agree
    on the same secret key. For example, with RSA, the client uses the
    server\'s public key, obtained from the public key certificate, to
    encrypt the secret key information. The client sends the encrypted
    secret key information to the server. Only the server can decrypt
    this message because the server\'s private key is required for this
    decryption.

3.  <span class="bold">Agreeing on encryption mechanisms</span>

    Both the client and the server now have access to the same secret
    key. With each message, they use the cryptographic hash function,
    chosen in the first step of the handshake, and shared secret
    information, to compute an HMAC that they append to the message.
    They then use the secret key and the secret key algorithm negotiated
    in the first step of the handshake to encrypt the secure data and
    the HMAC. The client and server can now communicate securely using
    their encrypted and hashed data.

</div>
</div>
<div class="sect3">
[]{#GUID-D04EF7C1-B1D4-4611-9896-A7B5573CBEED}

### The SSL Protocol {#JSSEC-GUID-D04EF7C1-B1D4-4611-9896-A7B5573CBEED .sect3}

<div>
[The SSL
Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B)
provides a high-level description of the SSL handshake, which is the
exchange of information between the client and the server prior to
sending the encrypted message. [Figure
8-1](java-secure-socket-extension-jsse-reference-guide.htm#GUID-D04EF7C1-B1D4-4611-9896-A7B5573CBEED__GUID-14810B76-CBF2-4F3C-9493-DDDB93358230)
provides more detail. It shows the sequence of messages that are
exchanged in the SSL handshake. Messages that are sent only in certain
situations are noted as optional. Each of the SSL messages is described
in detail afterward.

<div class="figure" id="GUID-D04EF7C1-B1D4-4611-9896-A7B5573CBEED__GUID-14810B76-CBF2-4F3C-9493-DDDB93358230">
Figure 8-1 The SSL/TLS Handshake

![This figure shows the sequence of messages that are exchanged in the
SSL handshake. These messages are described in detail in the following
text.](img/ssl-client.png "This figure shows the sequence of messages that are exchanged in the SSL handshake. These messages are described in detail in the following text.")

</div>
<!-- class="figure" -->

The SSL messages are sent in the following order:

1.  <span class="bold">Client hello:</span> The client sends the server
    information including the highest version of SSL that it supports
    and a list of the cipher suites that it supports (TLS 1.0 is
    indicated as SSL 3.1). The cipher suite information includes
    cryptographic algorithms and key sizes.
2.  <span class="bold">Server hello:</span> The server chooses the
    highest version of SSL and the best cipher suite that both the
    client and server support and sends this information to the client.
3.  (Optional) <span class="bold">Certificate:</span> The server sends
    the client a certificate or a certificate chain. A certificate chain
    typically begins with the server\'s public key certificate and ends
    with the certificate authority\'s root certificate. This message is
    optional, but is used whenever server authentication is required.
4.  (Optional) <span class="bold">Certificate request:</span> If the
    server must authenticate the client, then it sends the client a
    certificate request. In Internet applications, this message is
    rarely sent.
5.  (Optional) <span class="bold">Server key exchange:</span> The server
    sends the client a server key exchange message if the public key
    information from the Certificate is not sufficient for key exchange.
    For example, in cipher suites based on Diffie-Hellman (DH), this
    message contains the server\'s DH public key.
6.  <span class="bold">Server hello done:</span> The server tells the
    client that it is finished with its initial negotiation messages.
7.  (Optional) <span class="bold">Certificate:</span> If the server
    Certificate request from the client, the client sends its
    certificate chain, just as the server did previously.

    <div class="p">
    <div class="infoboxnote" id="GUID-D04EF7C1-B1D4-4611-9896-A7B5573CBEED__GUID-296D3B3F-97C6-466C-BDB7-716D4EDEA51C">
    Note:

    Only a few Internet server applications ask for a certificate from
    the client.

    </div>
    </div>
8.  <span class="bold">Client key exchange:</span> The client generates
    information used to create a key to use for symmetric encryption.
    For RSA, the client then encrypts this key information with the
    server\'s public key and sends it to the server. For cipher suites
    based on DH, this message contains the client\'s DH public key.
9.  (Optional) <span class="bold">Certificate verify:</span> This
    message is sent by the client when the client presents a certificate
    as previously explained. Its purpose is to allow the server to
    complete the process of authenticating the client. When this message
    is used, the client sends information that it digitally signs using
    a cryptographic hash function. When the server decrypts this
    information with the client\'s public key, the server is able to
    authenticate the client.
10. <span class="bold">Change cipher spec:</span> The client sends a
    message telling the server to change to encrypted mode.
11. <span class="bold">Finished</span> The client tells the server that
    it is ready for secure data communication to begin.
12. <span class="bold">Change cipher spec:</span> The server sends a
    message telling the client to change to encrypted mode.
13. <span class="bold">Finished:</span> The server tells the client that
    it is ready for secure data communication to begin. This is the end
    of the SSL handshake.
14. <span class="bold">Encrypted data:</span> The client and the server
    communicate using the symmetric encryption algorithm and the
    cryptographic hash function negotiated during the client hello and
    server hello, and using the secret key that the client sent to the
    server during the client key exchange. The handshake can be
    renegotiated at this time. See [Handshaking Again
    (Renegotiation)](java-secure-socket-extension-jsse-reference-guide.htm#GUID-FCA1CA1F-9FF1-4C9F-8FE8-EBFDE84F735F "Once the initial handshake is finished and application data is flowing, either side is free to initiate a new handshake at any time. An application might like to use a stronger cipher suite for especially critical operations, or a server application might want to require client authentication.").
15. <span class="bold">Close Messages:</span>At the end of the
    connection, each side sends a `close_notify`{.codeph} alert to
    inform the peer that the connection is closed.

If the parameters generated during an SSL session are saved, then these
parameters can sometimes be reused for future SSL sessions. Saving SSL
session parameters allows encrypted communication to begin much more
quickly.

</div>
<div class="sect4">
[]{#GUID-FCA1CA1F-9FF1-4C9F-8FE8-EBFDE84F735F}

#### Handshaking Again (Renegotiation) {#JSSEC-GUID-FCA1CA1F-9FF1-4C9F-8FE8-EBFDE84F735F .sect4}

<div>
Once the initial handshake is finished and application data is flowing,
either side is free to initiate a new handshake at any time. An
application might like to use a stronger cipher suite for especially
critical operations, or a server application might want to require
client authentication.

Regardless of the reason, the new handshake takes place over the
existing encrypted session, and application data and handshake messages
are interleaved until a new session is established.

Your application can initiate a new handshake by using one of the
following methods:

-   `SSLSocket.startHandshake()`{.codeph}
-   `SSLEngine.beginHandshake()`{.codeph}

<div class="infoboxnote" id="GUID-FCA1CA1F-9FF1-4C9F-8FE8-EBFDE84F735F__GUID-B4E262C5-520F-4941-B49D-791402E56838">
Note:

a protocol flaw related to renegotiation was found in 2009. The protocol
and the Java SE implementation have both been fixed. See [Transport
Layer Security (TLS) Renegotiation
Issue](java-secure-socket-extension-jsse-reference-guide.htm#GUID-9C767872-3A6C-4AD1-9805-49F112A0FA28 "In the fall of 2009, a flaw was discovered in the SSL/TLS protocols. A fix to the protocol was developed by the IETF TLS Working Group, and current versions of the JDK contain this fix. This section describes the situation in much more detail, along with interoperability issues when communicating with older implementations that do not contain this protocol fix.").

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-D6A538A2-8CEF-4C6D-9C44-295758E64E38}

#### Cipher Suite Choice and Remote Entity Verification {#JSSEC-GUID-D6A538A2-8CEF-4C6D-9C44-295758E64E38 .sect4}

<div>
The SSL/TLS protocols define a specific series of steps to ensure a
<span class="italic">protected</span> connection. However, the choice of
cipher suite directly affects the type of security that the connection
enjoys. For example, if an anonymous cipher suite is selected, then the
application has no way to verify the remote peer\'s identity. If a suite
with no encryption is selected, then the privacy of the data cannot be
protected. Additionally, the SSL/TLS protocols do not specify that the
credentials received must match those that peer might be expected to
send. If the connection were somehow redirected to a rogue peer, but the
rogue\'s credentials were acceptable based on the current trust
material, then the connection would be considered valid.

When using raw `SSLSocket`{.codeph} and `SSLEngine`{.codeph} classes,
you should always check the peer\'s credentials before sending any data.
The `SSLSocket`{.codeph} and `SSLEngine`{.codeph} classes do not
automatically verify that the host name in a URL matches the host name
in the peer\'s credentials. An application could be exploited with URL
spoofing if the host name is not verified. Since JDK 7, endpoint
identification/verification procedures can be handled during SSL/TLS
handshaking. See the
[<span class="apiname">SSLParameters.getEndpointIdentificationAlgorithm</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#getEndpointIdentificationAlgorithm--)
method.

Protocols such as HTTPS ([HTTP Over
TLS](http://www.ietf.org/rfc/rfc2818.txt)) do require host name
verification. Since JDK 7, the HTTPS endpoint identification is enforced
during handshaking for <span class="apiname">HttpsURLConnection</span>
by default. See the
[<span class="apiname">SSLParameters.getEndpointIdentificationAlgorithm</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#getEndpointIdentificationAlgorithm--)
method. Alternatively, applications can use the
<span class="apiname">HostnameVerifier</span> interface to override the
default HTTPS host name rules. See [The HostnameVerifier
Interface](java-secure-socket-extension-jsse-reference-guide.htm#GUID-9E46E5AA-FE3E-48D7-B616-98A143F74587)
and [HttpsURLConnection
Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A14E129D-4D9D-4F38-A9F0-ED6F97B18863 "The javax.net.ssl.HttpsURLConnection class extends the java.net.HttpURLConnection class and adds support for HTTPS-specific features.").

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-E1A3A7C3-309A-4415-903B-B31C96F68C86}

Client-Driven OCSP and OCSP Stapling {#JSSEC-GUID-E1A3A7C3-309A-4415-903B-B31C96F68C86 .sect2}
------------------------------------

<div>
Use the Online Certificate Status Protocol (OCSP) to determine the X.509
certificate revocation status during the Transport Layer Security (TLS)
handshake.

<div class="p">
X.509 certificates used in TLS can be revoked by the issuing Certificate
Authority (CA) if there is reason to believe that a certificate is
compromised. You can check the revocation status of certificates during
the TLS handshake by using one of the following approaches.

-   <span class="bold">Certificate Revocation List (CRL)</span>

    A CRL is a simple list of revoked certificates. The application
    receiving a certificate gets the CRL from a CRL server and checks if
    the certificate received is on the list. There are two disadvantages
    to using CRLs that mean a certificate could be revoked, but the
    revoked certificate is not listed in the CRL:

    -   CRLs can become very large so there can be a substantial
        increase in network traffic.

    -   Many CRLs are created with longer validity periods, which
        increases the possibility of a certificate being revoked within
        that validity period and not showing up until the next CRL
        refresh.

    See [Certificate/CRL Storage
    Classes](java-pki-programmers-guide.htm#GUID-AB96FD45-6F8A-4785-B6C5-082BEB6CDA5E "The Java Certification Path API includes the CertStore class for retrieving certificates and CRLs from a repository.")
    topic of the <cite>Java PKI Programmer\'s Guide</cite>.

-   <span class="bold">Client-driven OCSP </span>

    In client-driven OCSP, the client uses OCSP to contact an OCSP
    responder to check the certificate's revocation status. The amount
    of data required is small, and the OCSP responder is likely to be
    more up-to-date with the revocation status than a CRL. Each client
    connecting to a server requires an OCSP response for each
    certificate being checked. If the server is a popular one,
    and many of the clients are using client­-driven OCSP, these OCSP
    requests can have a negative effect on the performance of the OCSP
    responder.

-   <span class="bold">OCSP stapling</span>

    OCSP stapling enables the server, rather than the client, to make
    the request to the OCSP responder. The server staples the OCSP
    response to the certificate and returns it to the client during the
    TLS handshake. This approach enables the presenter of the
    certificate, rather than the issuing CA, to bear the resource cost
    of providing OCSP responses. It also enables the server to cache the
    OCSP responses and supply them to all clients. This significantly
    reduces the load on the OCSP responder because the response can be
    cached and periodically refreshed by the server rather than by each
    client.

</div>
</div>
<div class="sect3">
[]{#GUID-5B5A093F-FE4E-4D57-B66C-93CD6F78B1D1}

### Client-Driven OCSP and Certificate Revocation {#JSSEC-GUID-5B5A093F-FE4E-4D57-B66C-93CD6F78B1D1 .sect3}

<div>
Client-driven Online Certificate Status Protocol (OCSP) enables the
client to check the certificate revocation status by connecting to an
OCSP responder during the Transport Layer Security (TLS) handshake.

The client-driven OCSP request occurs during the TLS handshake just
after the client receives the certificate from the server and validates
it. See [SSL
Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B).

<div class="section">
TLS Handshake with Client-Driven OCSP

Client-driven OCSP is used during the TLS handshake between the client
and the server to check the server certificate revocation status. After
the client receives the certificate it performs certificate validation.
If the validation is successful, then the client verifies that the
certificate was not revoked by the issuer. This is done by sending an
OCSP request to an OCSP responder. After receiving the OCSP response,
the client checks this response before to completing the TLS handshake.

<div class="figure" id="GUID-5B5A093F-FE4E-4D57-B66C-93CD6F78B1D1__GUID-68392211-A1E0-4D96-97AD-3E6FFEA4AE40">
Figure 8-2 TLS Handshake with Client-Driven OCSP

![Description of Figure 8-2
follows](img/client-driven-ocsp.png "Description of Figure 8-2 follows")\
[Description of \"Figure 8-2 TLS Handshake with Client-Driven
OCSP\"](img_text/client-driven-ocsp.htm)

</div>
<!-- class="figure" -->

Usually the client finds the OCSP responder\'s URL by looking in the
Authority Information Access (AIA) extension of the certificate, but it
can be set to a static URL through the use of a system property.

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-4E3834C7-E741-499E-9646-3557670FD88A}

#### Setting up a Java Client to use Client-Driven OCSP {#JSSEC-GUID-4E3834C7-E741-499E-9646-3557670FD88A .sect4}

<div>
Client-driven OCSP is enabled by enabling revocation checking and
enabling OCSP.

<div class="p">
To configure a Java client to use client-driven OCSP, the Java client
must already be set up to connect to a server using TLS.

</div>
<!-- class="section" -->

1.  <span>Enable revocation checking. You can do this in two different
    ways.</span>
    -   Set the system property
        `com.sun.net.ssl.checkRevocation`{.codeph} to `true`{.codeph}.
    -   Use the `setRevocationEnabled`{.codeph} method on
        `PKIXParameters`{.codeph}. See [The PKIXParameters
        Class](java-pki-programmers-guide.htm#GUID-3D95A3BE-74CB-4357-BB85-9A8DEA36A457 "The PKIXParametersClass class specifies the set of input parameters defined by the PKIX certification path validation algorithm. It also includes a few additional useful parameters.").
2.  <span>Enable client-driven OCSP:</span>

    <div>
    Set the Security Property `ocsp.enable`{.codeph} to `true`{.codeph}.

    </div>

<div class="section">
Both steps are necessary. The `ocsp.enable`{.codeph} setting has no
effect unless revocation checking is enabled.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-489366D5-635A-4204-8980-3FB126047C45}

### OCSP Stapling and Certificate Revocation {#JSSEC-GUID-489366D5-635A-4204-8980-3FB126047C45 .sect3}

<div>
Online Certificate Status Protocol (OCSP) stapling enables the presenter
of a certificate, rather than the issuing Certificate Authority (CA), to
bear the resource cost of providing the OCSP responses that contain the
certificate's revocation status.

<div class="section">
TLS Handshake with OCSP Stapling

OCSP stapling is used during the Transport Layer Security (TLS)
handshake between the client and the server to check the server
certificate revocation status. The server makes the OCSP request to the
OCSP responder and staples the OCSP responses to the certificates
returned to the client. By having the server make the request to the
OCSP responder, the responses can be cached, and then used multiple
times for many clients.

The TLS handshake begins with the TLS `ClientHello`{.codeph} message.
When OCSP stapling is used, this message is sent to the server with the
`status_request`{.codeph} extension that indicates that the server
should perform an OCSP request. After processing the
`ClientHello`{.codeph} message, the server sends an OCSP request to the
appropriate OCSP responder for each certificate. When the server
receives the OCSP responses from the OCSP responders, it sends a
`ServerHello`{.codeph} message with its `status_request`{.codeph}
extension, indicating that OCSP responses will be provided in the TLS
handshake. The server will then present the server certificate chain,
followed by a message that consists of one or more OCSP responses for
those certificates. The client receiving the certificates with stapled
OCSP responses validates each certificate, and then checks the OCSP
responses before continuing with the handshake.

If, from the client's perspective, the stapled OCSP response from the
server for a certificate is missing, the client will attempt to use
client-driven OCSP or CRLs to get revocation information, if either of
these are enabled and revocation checking is set to `true`{.codeph}.

<div class="figure" id="GUID-489366D5-635A-4204-8980-3FB126047C45__GUID-E53642EE-979E-49F0-A632-BD6A560AEC64">
Figure 8-3 TLS Handshake with OCSP Stapling

![Description of Figure 8-3
follows](img/ocsp-stapling.png "Description of Figure 8-3 follows")\
[Description of \"Figure 8-3 TLS Handshake with OCSP
Stapling\"](img_text/ocsp-stapling.htm)

</div>
<!-- class="figure" -->

For more information about TLS handshake messages, see [The SSL
Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B).

</div>
<!-- class="section" -->

<div class="section">
Status Request Versus Multiple Status Request

The OCSP stapling feature implements the TLS Certificate Status Request
extension (section 8 of [RFC 6066](http://tools.ietf.org/html/rfc6066))
and the Multiple Certificate Status Request Extension ([RFC
6961](http://tools.ietf.org/html/rfc6961)).

The TLS Certificate Status Request extension requests revocation
information for only the server certificate in the certificate chain
while the Multiple Certificate Status Request Extension requests
revocation information for all certificates in the certificate chain. In
the case where only the server certificate\'s revocation information is
sent to the client, other certificates in the chain may be verified
using using the Certificate Revocation Lists (CRLs) or client-driven
OCSP (but the client will need to be set up to do this).

Although TLS allows the server to also request the client's certificate,
there is no provision in OCSP stapling that enables the client to
contact the appropriate OCSP responder and staple the response to the
certificate sent to the server.

</div>
<!-- class="section" -->

<div class="section">
The OCSP Request and Response

OCSP request and response messages are usually sent over unencrypted
HTTP. The response is signed by the CA.

If necessary, the stapled responses can be obtained in the client code
by calling the `getStatusResponses`{.codeph} method on the
`ExtendedSSLSession`{.codeph} object. The method signature is:

``` {.oac_no_warn dir="ltr"}
public List<byte[]> getStatusResponses();
```

The OCSP response is encoded using the Distinguished Encoding Rules
(DER) in a format described by the ASN.1 found in [RFC
6960](http://tools.ietf.org/html/rfc6960).

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-F15D190D-85A1-4012-8FE3-060DBD90E579}

#### Setting Up a Java Client to Use OCSP Stapling {#JSSEC-GUID-F15D190D-85A1-4012-8FE3-060DBD90E579 .sect4}

<div>
Online Certificate Status Protocol (OCSP) stapling is enabled on the
client side by setting the system property
`jdk.tls.client.enableStatusRequestExtension`{.codeph} to
`true`{.codeph} (its default value).

<div class="p">
To configure a Java client to make use of the OCSP response stapled to
the certificate returned by a server, the Java client must already be
set up to connect to a server using TLS, and the server must be set up
to staple an OCSP response to the certificate it returns part of the TLS
handshake.

</div>
<!-- class="section" -->

1.  <span>Enable OCSP stapling on the client:</span>

    <div>
    If necessary, set the system property
    `jdk.tls.client.enableStatusRequestExtension`{.codeph} to
    `true`{.codeph}.

    </div>
2.  <span>Enable revocation checking. You can do this in two different
    ways.</span>

    -   Set the system property
        `com.sun.net.ssl.checkRevocation`{.codeph} to `true`{.codeph}.
        You can do this from the command line or in the code.
    -   Use the `setRevocationEnabled`{.codeph} method on the
        `PKIXParameters`{.codeph} class. See [The PKIXParameters
        Class](java-pki-programmers-guide.htm#GUID-3D95A3BE-74CB-4357-BB85-9A8DEA36A457 "The PKIXParametersClass class specifies the set of input parameters defined by the PKIX certification path validation algorithm. It also includes a few additional useful parameters.").

    <div>
    For the client to include the stapled responses received from the
    server in the certificate validation, revocation checking must be
    set to `true`{.codeph}. If revocation checking is not set to
    `true`{.codeph}, then the connection will be allowed to proceed
    regardless of the presence or status of the revocation information

    </div>

</div>
</div>
<div class="sect4">
[]{#GUID-423716FB-DA34-4C73-B3A1-EB4CE120BB62}

#### Setting Up a Java Server to Use OCSP Stapling {#JSSEC-GUID-423716FB-DA34-4C73-B3A1-EB4CE120BB62 .sect4}

<div>
Online Certificate Status Protocol (OCSP) stapling is enabled on the
server by setting the system property
`jdk.tls.server.enableStatusRequestExtension`{.codeph} to
`true`{.codeph}. (It is set to `false`{.codeph} by default.)

<div class="p">
The following steps can be used to configure a Java server to connect to
an OCSP responder and staple the OCSP response to the certificate to be
returned to the client. The Java server must already be set up to
respond to clients using TLS.

</div>
<!-- class="section" -->

1.  <span>Enable OCSP stapling on the server:</span>

    <div>
    Set the system property
    `jdk.tls.server.enableStatusRequestExtension`{.codeph} to
    `true`{.codeph}.

    </div>
2.  **Optional:** <span>Set other properties as required. See [OCSP
    Stapling Configuration
    Properties](java-secure-socket-extension-jsse-reference-guide.htm#GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37 "This topic lists the effects of setting various properties when using the Online Certificate Status Protocol (OCSP). It shows the properties used in both client-driven OCSP and OCSP stapling.")
    for a list of the valid properties.</span>

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37}

### OCSP Stapling Configuration Properties {#JSSEC-GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37 .sect3}

<div>
This topic lists the effects of setting various properties when using
the Online Certificate Status Protocol (OCSP). It shows the properties
used in both client-driven OCSP and OCSP stapling.

<div class="section">
Server-side Properties

Most of the properties are read at `SSLContext`{.codeph} instantiation
time. This means that if you set a property, you must obtain a new
`SSLContext`{.codeph} object so that an `SSLSocket`{.codeph} or
`SSLEngine`{.codeph} object you obtain from that `SSLContext`{.codeph}
object will reflect the property setting. The one exception is
the` jdk.tls.stapling.responseTimeout`{.codeph} property. That property
is evaluated when the `ServerHandshaker`{.codeph} object is created
(essentially at the same time that an `SSLSocket`{.codeph} or
`SSLEngine`{.codeph} object gets created).

</div>
<!-- class="section" -->

<div class="section">
<div class="tblformalwide" id="GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37__GUID-B67B52FB-CD64-48FC-9552-23E929727680">
Table 8-3 Server-Side OCSP stapling Properties

+-----------------------+-----------------------+-----------------------+
| Property              | Description           | Default Value         |
+:======================+:======================+:======================+
| `jdk.tls.server.enabl | Enables the           | False                 |
| eStatusRequestExtensi | server-side support   |                       |
| on`{.codeph}          | for OCSP stapling.    |                       |
+-----------------------+-----------------------+-----------------------+
| `jdk.tls.stapling.res | Controls the maximum  | 5000 (integer value   |
| ponseTimeout`{.codeph | amount of time the    | in milliseconds)      |
| }                     | server will use to    |                       |
|                       | obtain OCSP           |                       |
|                       | responses, whether    |                       |
|                       | from the cache or by  |                       |
|                       | contacting an OCSP    |                       |
|                       | responder.            |                       |
|                       |                       |                       |
|                       | The responses that    |                       |
|                       | are already received  |                       |
|                       | will be sent in a     |                       |
|                       | `CertificateStatus`{. |                       |
|                       | codeph}               |                       |
|                       | message, if           |                       |
|                       | applicable based on   |                       |
|                       | the type of stapling  |                       |
|                       | being done.           |                       |
+-----------------------+-----------------------+-----------------------+
| `jdk.tls.stapling.cac | Controls the maximum  | 256 objects           |
| heSize`{.codeph}      | cache size in         |                       |
|                       | entries.              |                       |
|                       |                       |                       |
|                       | If the cache is full  |                       |
|                       | and a new response    |                       |
|                       | needs to be cached,   |                       |
|                       | then the least        |                       |
|                       | recently used cache   |                       |
|                       | entry will be         |                       |
|                       | replaced with the new |                       |
|                       | one. A value of zero  |                       |
|                       | or less for this      |                       |
|                       | property means that   |                       |
|                       | the cache will have   |                       |
|                       | no upper bound on the |                       |
|                       | number of responses   |                       |
|                       | it can contain.       |                       |
+-----------------------+-----------------------+-----------------------+
| `jdk.tls.stapling.cac | Controls the maximum  | 3600 seconds (1 hour) |
| heLifetime`{.codeph}  | life of a cached      |                       |
|                       | response.             |                       |
|                       |                       |                       |
|                       | It is possible for    |                       |
|                       | responses to have     |                       |
|                       | shorter lifetimes     |                       |
|                       | than the value set    |                       |
|                       | with this property if |                       |
|                       | the response has a    |                       |
|                       | <span class="bold">ne |                       |
|                       | xtUpdate</span>       |                       |
|                       | field that expires    |                       |
|                       | sooner than the cache |                       |
|                       | lifetime. A value of  |                       |
|                       | zero or less for this |                       |
|                       | property disables the |                       |
|                       | cache lifetime. If an |                       |
|                       | object has no         |                       |
|                       | <span class="bold">ne |                       |
|                       | xtUpdate</span>       |                       |
|                       | value and cache       |                       |
|                       | lifetimes are         |                       |
|                       | disabled, then the    |                       |
|                       | response will not be  |                       |
|                       | cached.               |                       |
+-----------------------+-----------------------+-----------------------+
| `jdk.tls.stapling.res | Enables the           | Not set               |
| ponderURI`{.codeph}   | administrator to set  |                       |
|                       | a default URI in the  |                       |
|                       | event that            |                       |
|                       | certificates used for |                       |
|                       | TLS do not have the   |                       |
|                       | Authority Info Access |                       |
|                       | (AIA) extension.      |                       |
|                       |                       |                       |
|                       | It will not override  |                       |
|                       | the Authority Info    |                       |
|                       | Access extension      |                       |
|                       | value unless the      |                       |
|                       | `jdk.tls.stapling.res |                       |
|                       | ponderOverride`{.code |                       |
|                       | ph}                   |                       |
|                       | property is set.      |                       |
+-----------------------+-----------------------+-----------------------+
| `jdk.tls.stapling.res | Enables a URI         | False                 |
| ponderOverride`{.code | provided through the  |                       |
| ph}                   | `jdk.tls.stapling.res |                       |
|                       | ponderURI`{.codeph}   |                       |
|                       | property to override  |                       |
|                       | any AIA extension     |                       |
|                       | value.                |                       |
+-----------------------+-----------------------+-----------------------+
| `jdk.tls.stapling.ign | Disables the          | False                 |
| oreExtensions`{.codep | forwarding of OCSP    |                       |
| h}                    | extensions specified  |                       |
|                       | in                    |                       |
|                       | the `status_request`{ |                       |
|                       | .codeph} or `status_r |                       |
|                       | equest_v2`{.codeph} T |                       |
|                       | LS                    |                       |
|                       | extensions.           |                       |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
Client-Side Settings

</div>
<!-- class="section" -->

<div class="section">
<div class="tblformal" id="GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37__GUID-F7BC7AEB-8918-40C7-AA80-E0CF554FD1F3">
Table 8-4 Client-Side Settings Used in OCSP Stapling

  PKIXBuilderParameters   checkRevocation Property   PKIXRevocationChecker                                             Result
  ----------------------- -------------------------- ----------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Default                 Default                    Default                                                           Revocation checking is disabled.
  Default                 True                       Default                                                           Revocation checking is enabled.[\[1\]](java-secure-socket-extension-jsse-reference-guide.htm#GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37__NOTETHATCLIENT-SIDEOCSPFALLBACKWILL-1B855C3C)
  Instantiated            Default                    Default                                                           Revocation checking is enabled.[\[1\]](java-secure-socket-extension-jsse-reference-guide.htm#GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37__NOTETHATCLIENT-SIDEOCSPFALLBACKWILL-1B855C3C)
  Instantiated            Default                    Instantiated, added to `PKIXBuilderParameters`{.codeph} object.   Revocation checking is enabled and[\[1\]](java-secure-socket-extension-jsse-reference-guide.htm#GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37__NOTETHATCLIENT-SIDEOCSPFALLBACKWILL-1B855C3C)will behave according to the `PKIXRevocationChecker`{.codeph} settings.

</div>
<!-- class="inftblhruleinformal" -->

Footnote 1 Note that client-side OCSP fallback will occur only if the
`ocsp.enable`{.codeph} Security Property is set to `true`{.codeph}.

Developers have some flexibility in how to handle the responses provided
through OCSP stapling. OCSP stapling makes no changes to the current
methodologies involved in certificate path checking and revocation
checking. This means that it is possible to have both client and server
assert the `status_request`{.codeph} extensions, obtain OCSP responses
through the `CertificateStatus`{.codeph} message, and provide user
flexibility in how to react to revocation information, or the lack
thereof.

If no `PKIXBuilderParameters`{.codeph} is provided by the caller, then
revocation checking is disabled. If the caller creates
a `PKIXBuilderParameters`{.codeph} object and uses
the `setRevocationEnabled`{.codeph} method to enable revocation
checking, then stapled OCSP responses will be evaluated. This is also
the case if the `com.sun.net.ssl.checkRevocation`{.codeph} property is
set to `true`{.codeph}.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-B7AB25FA-7F0C-4EFA-A827-813B2CE7FBDC}

JSSE Classes and Interfaces {#JSSEC-GUID-B7AB25FA-7F0C-4EFA-A827-813B2CE7FBDC .sect2}
---------------------------

<div>
<div class="section">
To communicate securely, both sides of the connection must be
SSL-enabled. In the JSSE API, the endpoint classes of the connection are
`SSLSocket`{.codeph} and `SSLEngine`{.codeph}. In [Figure
8-4](java-secure-socket-extension-jsse-reference-guide.htm#GUID-B7AB25FA-7F0C-4EFA-A827-813B2CE7FBDC__GUID-A0AB7CF4-2CB8-4F12-8EF8-68EA03C6217D),
the major classes used to create `SSLSocket`{.codeph} and
`SSLEngine`{.codeph} are laid out in a logical ordering.

<div class="figure" id="GUID-B7AB25FA-7F0C-4EFA-A827-813B2CE7FBDC__GUID-A0AB7CF4-2CB8-4F12-8EF8-68EA03C6217D">
Figure 8-4 JSSE Classes Used to Create SSLSocket and SSLEngine

![Description of Figure 8-4
follows](img/jsse-classes-and-interfaces.png "Description of Figure 8-4 follows")\
[Description of \"Figure 8-4 JSSE Classes Used to Create SSLSocket and
SSLEngine\"](img_text/jsse-classes-and-interfaces.htm)

</div>
<!-- class="figure" -->

An `SSLSocket`{.codeph} is created either by an
`SSLSocketFactory`{.codeph} or by an `SSLServerSocket`{.codeph}
accepting an inbound connection. In turn, an `SSLServerSocket`{.codeph}
is created by an `SSLServerSocketFactory`{.codeph}. Both
`SSLSocketFactory`{.codeph} and `SSLServerSocketFactory`{.codeph}
objects are created by an `SSLContext`{.codeph}. An `SSLEngine`{.codeph}
is created directly by an `SSLContext`{.codeph}, and relies on the
application to handle all I/O.

<div class="infoboxnote" id="GUID-B7AB25FA-7F0C-4EFA-A827-813B2CE7FBDC__GUID-1C41051F-5CE0-44B3-A0E9-D7FC41D3C6EE">
Note:

When using raw `SSLSocket`{.codeph} or `SSLEngine`{.codeph} classes, you
should always check the peer\'s credentials before sending any data.
Since JDK 7, endpoint identification/verification procedures can be
handled during SSL/TLS handshaking. See the method
[<span class="apiname">SSLParameters.setEndpointIdentificationAlgorithm</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#getEndpointIdentificationAlgorithm--).

For example, the host name in a URL matches the host name in the peer\'s
credentials. An application could be exploited with URL spoofing if the
host name is not verified.

</div>
</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-4A6ABFE4-6B0E-4DF2-A9E8-EEEB71935293}

### JSSE Core Classes and Interfaces {#JSSEC-GUID-4A6ABFE4-6B0E-4DF2-A9E8-EEEB71935293 .sect3}

<div>
The core JSSE classes are part of the
[<span class="apiname">javax.net</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/package-summary.html)
and
[<span class="apiname">javax.net.ssl</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/package-summary.html)
packages.

</div>
</div>
<div class="sect3">
[]{#GUID-6AF71CD9-4E87-49E1-B175-89810D54139E}

### SocketFactory and ServerSocketFactory Classes {#JSSEC-GUID-6AF71CD9-4E87-49E1-B175-89810D54139E .sect3}

<div>
The abstract `javax.net.SocketFactory`{.codeph} class is used to create
sockets. Subclasses of this class are factories that create particular
subclasses of sockets and thus provide a general framework for the
addition of public socket-level functionality. For example, see
[SSLSocketFactory and SSLServerSocketFactory
Classes](java-secure-socket-extension-jsse-reference-guide.htm#GUID-F0917FCC-FBB0-4E36-8D79-37F14F8A274B).

The abstract `javax.net.ServerSocketFactory`{.codeph} class is analogous
to the `SocketFactory`{.codeph} class, but is used specifically for
creating server sockets.

Socket factories are a simple way to capture a variety of policies
related to the sockets being constructed, producing such sockets in a
way that does not require special configuration of the code that asks
for the sockets:

-   Due to polymorphism of both factories and sockets, different kinds
    of sockets can be used by the same application code just by passing
    different kinds of factories.
-   Factories can themselves be customized with parameters used in
    socket construction. For example, factories could be customized to
    return sockets with different networking timeouts or security
    parameters already configured.
-   The sockets returned to the application can be subclasses of
    `java.net.Socket`{.codeph} (or `javax.net.ssl.SSLSocket`{.codeph}),
    so that they can directly expose new APIs for features such as
    compression, security, record marking, statistics collection, or
    firewall tunneling.

</div>
</div>
<div class="sect3">
[]{#GUID-F0917FCC-FBB0-4E36-8D79-37F14F8A274B}

### SSLSocketFactory and SSLServerSocketFactory Classes {#JSSEC-GUID-F0917FCC-FBB0-4E36-8D79-37F14F8A274B .sect3}

<div>
The `javax.net.ssl.SSLSocketFactory`{.codeph} class acts as a factory
for creating secure sockets. This class is an abstract subclass of
[`javax.net.SocketFactory`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/SocketFactory.html).

Secure socket factories encapsulate the details of creating and
initially configuring secure sockets. This includes authentication keys,
peer certificate validation, enabled cipher suites, and the like.

The `javax.net.ssl.SSLServerSocketFactory`{.codeph} class is analogous
to the `SSLSocketFactory`{.codeph} class, but is used specifically for
creating server sockets.

</div>
<div class="sect4">
[]{#GUID-86684173-0E06-4EA9-AF89-B80E0D7B602E}

#### Obtaining an SSLSocketFactory {#JSSEC-GUID-86684173-0E06-4EA9-AF89-B80E0D7B602E .sect4}

<div>
The following ways can be used to obtain an `SSLSocketFactory`{.codeph}:

<div class="section">
-   Get the default factory by calling the
    `SSLSocketFactory.getDefault()`{.codeph} static method.
-   Receive a factory as an API parameter. That is, code that must
    create sockets but does not care about the details of how the
    sockets are configured can include a method with an
    `SSLSocketFactory`{.codeph} parameter that can be called by clients
    to specify which `SSLSocketFactory`{.codeph} to use when creating
    sockets (for example, `javax.net.ssl.HttpsURLConnection`{.codeph}).
-   Construct a new factory with specifically configured behavior.

The default factory is typically configured to support server
authentication only so that sockets created by the default factory do
not leak any more information about the client than a normal TCP socket
would.

Many classes that create and use sockets do not need to know the details
of socket creation behavior. Creating sockets through a socket factory
passed in as a parameter is a good way of isolating the details of
socket configuration, and increases the reusability of classes that
create and use sockets.

You can create new socket factory instances either by implementing your
own socket factory subclass or by using another class which acts as a
factory for socket factories. One example of such a class is
`SSLContext`{.codeph}, which is provided with the JSSE implementation as
a provider-based configuration class.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-8EF3AA86-6559-482D-82C7-4F6F6951A1AB}

### SSLSocket and SSLServerSocket Classes {#JSSEC-GUID-8EF3AA86-6559-482D-82C7-4F6F6951A1AB .sect3}

<div>
The `javax.net.ssl.SSLSocket`{.codeph} class is a subclass of the
standard Java `java.net.Socket`{.codeph} class. It supports all of the
standard socket methods and adds methods specific to secure sockets. It
supports all of the standard socket methods and adds methods specific to
secure sockets. Instances of this class encapsulate the
<span class="apiname">SSLContext</span> under which they were created.
See [The SSLContext
Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C281CAF3-275F-4DE4-8B47-4A84363CF39F "The javax.net.ssl.SSLContext class is an engine class for an implementation of a secure socket protocol. An instance of this class acts as a factory for SSLSocket, SSLServerSocket, and SSLEngine. An SSLContext object holds all of the state information shared across all objects created under that context. For example, session state is associated with the SSLContext when it is negotiated through the handshake protocol by sockets created by socket factories provided by the context. These cached sessions can be reused and shared by other sockets created under the same context.").
There are APIs to control the creation of secure socket sessions for a
socket instance, but trust and key management are not directly exposed.

The `javax.net.ssl.SSLServerSocket`{.codeph} class is analogous to the
`SSLSocket`{.codeph} class, but is used specifically for creating server
sockets.

To prevent peer spoofing, you should always verify the credentials
presented to an `SSLSocket`{.codeph}. See [Cipher Suite Choice and
Remote Entity
Verification](java-secure-socket-extension-jsse-reference-guide.htm#GUID-D6A538A2-8CEF-4C6D-9C44-295758E64E38).

<div class="p">
<div class="infoboxnote" id="GUID-8EF3AA86-6559-482D-82C7-4F6F6951A1AB__GUID-1242F7C2-58EE-4389-BD47-8316EBD20B28">
Note:

Due to the complexity of the SSL and TLS protocols, it is difficult to
predict whether incoming bytes on a connection are handshake or
application data, and how that data might affect the current connection
state (even causing the process to block). In the Oracle JSSE
implementation, the `available()`{.codeph} method on the object obtained
by `SSLSocket.getInputStream()`{.codeph} returns a count of the number
of application data bytes successfully decrypted from the SSL connection
but not yet read by the application.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-BA88D2CC-EC63-4A74-A696-E1A56BD68BF0}

#### Obtaining an SSLSocket {#JSSEC-GUID-BA88D2CC-EC63-4A74-A696-E1A56BD68BF0 .sect4}

<div>
Instances of <span class="apiname">SSLSocket</span> can be obtained in
one of the following ways:

-   <span>An <span class="apiname">SSLSocket</span> can be created by an
    instance of
    [<span class="apiname">SSLSocketFactory</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLSocketFactory.html)
    via one of the several <span class="apiname">createSocket</span>
    methods of that class.</span>
-   <span>An <span class="apiname">SSLSocket</span> can be created
    through the <span class="apiname">accept</span> method of the
    <span class="apiname">SSLServerSocket</span> class.</span>

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-8796681D-06C8-4884-ADE4-782394F6F6FB}

### SSLEngine Class {#JSSEC-GUID-8796681D-06C8-4884-ADE4-782394F6F6FB .sect3}

<div>
SSL/TLS/DTLS is becoming increasingly popular. It is being used in a
wide variety of applications across a wide range of computing platforms
and devices. Along with this popularity come demands to use SSL/TLS/DTLS
with different I/O and threading models to satisfy the applications\'
performance, scalability, footprint, and other requirements. There are
demands to use SSL/TLS/DTLS with blocking and nonblocking I/O channels,
asynchronous I/O, arbitrary input and output streams, and byte buffers.
There are demands to use it in highly scalable, performance-critical
environments, requiring management of thousands of network connections.

Abstraction of the I/O transport mechanism using the
`SSLEngine`{.codeph} class in Java SE allows applications to use the
SSL/TLS/DTLS protocols in a transport-independent way, and thus frees
application developers to choose transport and computing models that
best meet their needs. Not only does this abstraction allow applications
to use nonblocking I/O channels and other I/O models, it also
accommodates different threading models. This effectively leaves the I/O
and threading decisions up to the application developer. Because of this
flexibility, the application developer must manage I/O and threading
(complex topics in and of themselves), as well as have some
understanding of the SSL/TLS/DTLS protocols. The abstraction is
therefore an advanced API: beginners should use `SSLSocket`{.codeph}.

Users of other Java programming language APIs such as the Java Generic
Security Services (Java GSS-API) and the Java Simple Authentication
Security Layer (Java SASL) will notice similarities in that the
application is also responsible for transporting data.

The core class is
[`javax.net.ssl.SSLEngine`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngine.html).
It encapsulates an SSL/TLS/DTLS state machine and operates on inbound
and outbound byte buffers supplied by the user of the
`SSLEngine`{.codeph} class. [Figure
8-5](java-secure-socket-extension-jsse-reference-guide.htm#GUID-8796681D-06C8-4884-ADE4-782394F6F6FB__GUID-A02F05DD-41AA-47E3-A1BE-9AB4AC6E4BC2)
illustrates the flow of data from the application, through
`SSLEngine`{.codeph}, to the transport mechanism, and back.

<div class="figure" id="GUID-8796681D-06C8-4884-ADE4-782394F6F6FB__GUID-A02F05DD-41AA-47E3-A1BE-9AB4AC6E4BC2">
Figure 8-5 Flow of Data Through SSLEngine

![The following text describes this
figure.](img/sslengine_jsse.png "The following text describes this figure.")

</div>
<!-- class="figure" -->

The application, shown on the left, supplies application (plaintext)
data in an application buffer and passes it to
<span class="apiname">SSLEngine</span>. The
<span class="apiname">SSLEngine</span> object processes the data
contained in the buffer, or any handshaking data, to produce
SSL/TLS/DTLS encoded data and places it to the network buffer supplied
by the application. The application is then responsible for using an
appropriate transport (shown on the right) to send the contents of the
network buffer to its peer. Upon receiving SSL/TLS/DTLS encoded data
from its peer (via the transport), the application places the data into
a network buffer and passes it to
<span class="apiname">SSLEngine</span>. The
<span class="apiname">SSLEngine</span> object processes the network
buffer\'s contents to produce handshaking data or application data.

An instance of the `SSLEngine`{.codeph} class can be in one of the
following states:

[<!-- -->]{#GUID-8796681D-06C8-4884-ADE4-782394F6F6FB__GUID-B02D18CC-ADD5-44A5-805E-25CD2998855B}Creation
:   The `SSLEngine`{.codeph} has been created and initialized, but has
    not yet been used. During this phase, an application may set any
    `SSLEngine`{.codeph}-specific settings (enabled cipher suites,
    whether the `SSLEngine`{.codeph} should handshake in client or
    server mode, and so on). Once handshaking has begun, though, any new
    settings (except client/server mode) will be used for the next
    handshake.

[<!-- -->]{#GUID-8796681D-06C8-4884-ADE4-782394F6F6FB__GUID-0F78430D-0144-4BFE-8E16-6DE2FAD40A64}Initial handshaking
:   The initial handshake is a procedure by which the two peers exchange
    communication parameters until an `SSLSession`{.codeph} is
    established. Application data can't be sent during this phase.

[<!-- -->]{#GUID-8796681D-06C8-4884-ADE4-782394F6F6FB__GUID-4FFB7915-D7CE-49E5-9E71-0C542A09854A}Application data
:   After the communication parameters have been established and the
    handshake is complete, application data can flow through the
    `SSLEngine`{.codeph}. Outbound application messages are encrypted
    and integrity protected, and inbound messages reverse the process.

[<!-- -->]{#GUID-8796681D-06C8-4884-ADE4-782394F6F6FB__GUID-21E779D2-2FBB-46D2-9275-E742012D20DB}Rehandshaking
:   Either side can request a renegotiation of the session at any time
    during the Application Data phase. New handshaking data can be
    intermixed among the application data. Before starting the
    rehandshake phase, the application may reset the SSL/TLS/DTLS
    communication parameters such as the list of enabled ciphersuites
    and whether to use client authentication, but can not change between
    client/server modes. As before, after handshaking has begun, any new
    `SSLEngine `{.codeph}configuration settings won't be used until the
    next handshake.

[<!-- -->]{#GUID-8796681D-06C8-4884-ADE4-782394F6F6FB__GUID-5FBA1A16-3A76-416F-A4F9-3271D9F2E45D}Closure
:   When the connection is no longer needed, the application should
    close the `SSLEngine`{.codeph} and should send/receive any remaining
    messages to the peer before closing the underlying transport
    mechanism. Once an engine is closed, it is not reusable: a new
    `SSLEngine`{.codeph} must be created.

</div>
<div class="sect4">
[]{#GUID-16B697CD-77EB-468F-94A1-04254BA75FD7}

#### Creating an SSLEngine Object {#JSSEC-GUID-16B697CD-77EB-468F-94A1-04254BA75FD7 .sect4}

<div>
Use the `SSLContext.createSSLEngine()`{.codeph} method to create an
`SSLEngine`{.codeph} object.

<div class="section">
Before you create an `SSLEngine`{.codeph} object, you must configure the
engine to act as a client or a server, and set other configuration
parameters, such as which cipher suites to use and whether client
authentication is required. The
[`SSLContext.createSSLEngine`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLContext.html#createSSLEngine--)
method creates an
[`javax.net.ssl.SSLEngine`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngine.html)
object.

<div class="infoboxnote" id="GUID-16B697CD-77EB-468F-94A1-04254BA75FD7__GUID-E7142213-957C-4DEB-8C5D-CD8BE3E5A286">
Note:

The server name and port number are not used for communicating with the
server (all transport is the responsibility of the application). They
are hints to the JSSE provider to use for SSL session caching, and for
Kerberos-based cipher suite implementations to determine which server
credentials should be obtained.

</div>
</div>
<!-- class="section" -->

<div class="example" id="GUID-16B697CD-77EB-468F-94A1-04254BA75FD7__THEFOLLOWINGSAMPLECODECREATESASSLEN-225FBEA9">
Example 8-1 Sample Code for Creating an SSLEngine Client for TLS with
JKS as Keystore

The following sample code creates an
<span class="apiname">SSLEngine</span> client for TLS that uses JKS as
keystore:

``` {.codeblock dir="ltr"}
    import javax.net.ssl.*;
    import java.security.*;

    // Create and initialize the SSLContext with key material
    char[] passphrase = "passphrase".toCharArray();

    // First initialize the key and trust material
    KeyStore ksKeys = KeyStore.getInstance("JKS");
    ksKeys.load(new FileInputStream("testKeys"), passphrase);
    KeyStore ksTrust = KeyStore.getInstance("JKS");
    ksTrust.load(new FileInputStream("testTrust"), passphrase);

    // KeyManagers decide which key material to use
    KeyManagerFactory kmf = KeyManagerFactory.getInstance("PKIX");
    kmf.init(ksKeys, passphrase);

    // TrustManagers decide whether to allow connections
    TrustManagerFactory tmf = TrustManagerFactory.getInstance("PKIX");
    tmf.init(ksTrust);

    // Get an instance of SSLContext for SSL/TLS protocols
    sslContext = SSLContext.getInstance("TLS");
    sslContext.init(kmf.getKeyManagers(), tmf.getTrustManagers(), null);

    // Create the engine
    SSLEngine engine = sslContext.createSSLengine(hostname, port);

    // Use as client
    engine.setUseClientMode(true);
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4}

#### Generating and Processing SSL/TLS Data {#JSSEC-GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4 .sect4}

<div>
The two main `SSLEngine`{.codeph} methods are `wrap()`{.codeph} and
`unwrap()`{.codeph}. They are responsible for generating and consuming
network data respectively. Depending on the state of the
`SSLEngine`{.codeph} object, this data might be handshake or application
data.

<div class="section">
Each `SSLEngine`{.codeph} object has several phases during its lifetime.
Before application data can be sent or received, the SSL/TLS protocol
requires a handshake to establish cryptographic parameters. This
handshake requires a series of back-and-forth steps by the
`SSLEngine`{.codeph} object. For more details about the handshake
itself, see [The SSL
Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B).

During the initial handshaking, the `wrap()`{.codeph} and
`unwrap()`{.codeph} methods generate and consume handshake data, and the
application is responsible for transporting the data. The
`wrap()`{.codeph} and `unwrap()`{.codeph} method sequence is repeated
until the handshake is finished. Each `SSLEngine`{.codeph} operation
generates an instance of the `SSLEngineResult`{.codeph} class, in which
the `SSLEngineResult.HandshakeStatus`{.codeph} field is used to
determine what operation must occur next to move the handshake along.

[Table
8-5](java-secure-socket-extension-jsse-reference-guide.htm#GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4__GUID-498B945A-6C5B-4291-8278-B34D79CCF010 "Sequence of methods called during a typical handshake, with corresponding messages and statuses")
shows the sequence of methods called during a typical handshake, with
corresponding messages and statuses.

<div class="tblformal" id="GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4__GUID-498B945A-6C5B-4291-8278-B34D79CCF010">
Table 8-5 Typical Handshake

  Client                                  SSL/TLS Message                                                                                                           <span class="apiname">HandshakeStatus</span>
  --------------------------------------- ------------------------------------------------------------------------------------------------------------------------- ----------------------------------------------
  <span class="apiname">wrap()</span>     <span class="apiname">ClientHello</span>                                                                                  <span class="apiname">NEED\_UNWRAP</span>
  <span class="apiname">unwrap()</span>   <span class="apiname">ServerHello</span>/<span class="apiname">Cert</span>/<span class="apiname">ServerHelloDone</span>   <span class="apiname">NEED\_WRAP</span>
  <span class="apiname">wrap()</span>     <span class="apiname">ClientKeyExchange</span>                                                                            <span class="apiname">NEED\_WRAP</span>
  <span class="apiname">wrap()</span>     <span class="apiname">ChangeCipherSpec</span>                                                                             <span class="apiname">NEED\_WRAP</span>
  <span class="apiname">wrap()</span>     <span class="apiname">Finished</span>                                                                                     <span class="apiname">NEED\_UNWRAP</span>
  <span class="apiname">unwrap()</span>   <span class="apiname">ChangeCipherSpec</span>                                                                             <span class="apiname">NEED\_UNWRAP</span>
  <span class="apiname">unwrap()</span>   <span class="apiname">Finished</span>                                                                                     <span class="apiname">FINISHED</span>

</div>
<!-- class="inftblhruleinformal" -->

[Figure
8-6](java-secure-socket-extension-jsse-reference-guide.htm#GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4__STATEMACHINEDURINGDTLSHANDSHAKE-D6B2B3FD)
shows the state machine during a typical SSL/TLS handshake, with
corresponding messages and statuses:

<div class="figure" id="GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4__STATEMACHINEDURINGDTLSHANDSHAKE-D6B2B3FD">
Figure 8-6 State Machine during SSL/TLS Handshake

![Description of Figure 8-6
follows](img/ssl-tls-handshake.png "Description of Figure 8-6 follows")\
[Description of \"Figure 8-6 State Machine during SSL/TLS
Handshake\"](img_text/ssl-tls-handshake.htm)

</div>
<!-- class="figure" -->

When handshaking is complete, further calls to `wrap()`{.codeph} will
attempt to consume application data and package it for transport. The
`unwrap()`{.codeph} method will attempt the opposite.

To send data to the peer, the application first supplies the data that
it wants to send via `SSLEngine.wrap()`{.codeph} to obtain the
corresponding SSL/TLS encoded data. The application then sends the
encoded data to the peer using its chosen transport mechanism. When the
application receives the SSL/TLS encoded data from the peer via the
transport mechanism, it supplies this data to the `SSLEngine`{.codeph}
via `SSLEngine.unwrap()`{.codeph} to obtain the plaintext data sent by
the peer.

</div>
<!-- class="section" -->

<div class="example" id="GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4__GUID-223D79BF-70AD-4F6C-B472-81C28C010BD9">
Example 8-2 Sample Code for Creating a Nonblocking SocketChannel

The following example is an SSL application that uses a non-blocking
`SocketChannel`{.codeph} to communicate with its peer. It sends the
string \"hello\" to the peer by encoding it using the
`SSLEngine`{.codeph} created in [Example
8-1](java-secure-socket-extension-jsse-reference-guide.htm#GUID-16B697CD-77EB-468F-94A1-04254BA75FD7__THEFOLLOWINGSAMPLECODECREATESASSLEN-225FBEA9)
. It uses information from the `SSLSession`{.codeph} to determine how
large to make the byte buffers.

<div class="infoboxnote" id="GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4__GUID-6DE5C28C-B4CD-438F-9A68-33BB5C3E2E94">
Note:

The example can be made more robust and scalable by using a
`Selector`{.codeph} with the nonblocking `SocketChannel`{.codeph}.

</div>
``` {.codeblock dir="ltr"}
    // Create a nonblocking socket channel
    SocketChannel socketChannel = SocketChannel.open();
    socketChannel.configureBlocking(false);
    socketChannel.connect(new InetSocketAddress(hostname, port));

    // Complete connection
    while (!socketChannel.finishedConnect()) {
    // do something until connect completed
    }

    //Create byte buffers for holding application and encoded data

    SSLSession session = engine.getSession();
    ByteBuffer myAppData = ByteBuffer.allocate(session.getApplicationBufferSize());
    ByteBuffer myNetData = ByteBuffer.allocate(session.getPacketBufferSize());
    ByteBuffer peerAppData = ByteBuffer.allocate(session.getApplicationBufferSize());
    ByteBuffer peerNetData = ByteBuffer.allocate(session.getPacketBufferSize());

    // Do initial handshake
    doHandshake(socketChannel, engine, myNetData, peerNetData);

    myAppData.put("hello".getBytes());
    myAppData.flip();

    while (myAppData.hasRemaining()) {
    // Generate SSL/TLS/DTLS encoded data (handshake or application data)
    SSLEngineResult res = engine.wrap(myAppData, myNetData);

    // Process status of call
    if (res.getStatus() == SSLEngineResult.Status.OK) {
        myAppData.compact();

        // Send SSL/TLS/DTLS encoded data to peer
        while(myNetData.hasRemaining()) {
            int num = socketChannel.write(myNetData);
            if (num == 0) {
                // no bytes written; try again later
            }
        }
    }

    // Handle other status:  BUFFER_OVERFLOW, CLOSED
    ...
    }
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4__GUID-FDF2BEE0-D9F4-4653-BD90-4167FEB96C45">
Example 8-3 Sample Code for Reading Data From Nonblocking SocketChannel

The following sample code illustrates how to read data from the same
nonblocking `SocketChannel`{.codeph} and extract the plaintext data from
it by using `SSLEngine`{.codeph} created in [Example
8-1](java-secure-socket-extension-jsse-reference-guide.htm#GUID-16B697CD-77EB-468F-94A1-04254BA75FD7__THEFOLLOWINGSAMPLECODECREATESASSLEN-225FBEA9).
Each iteration of this code may or may not produce plaintext data,
depending on whether handshaking is in progress.

``` {.codeblock dir="ltr"}
    // Read SSL/TLS/DTLS encoded data from peer
    int num = socketChannel.read(peerNetData);
    if (num == -1) {
        // The channel has reached end-of-stream
    } else if (num == 0) {
        // No bytes read; try again ...
    } else {
        // Process incoming data
        peerNetData.flip();
        res = engine.unwrap(peerNetData, peerAppData);

        if (res.getStatus() == SSLEngineResult.Status.OK) {
            peerNetData.compact();

        if (peerAppData.hasRemaining()) {
            // Use peerAppData
        }
    }
    // Handle other status:  BUFFER_OVERFLOW, BUFFER_UNDERFLOW, CLOSED
    ...
    }
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-D0F8B9C3-721B-43A4-B2CE-7512B175F76D}

#### Datagram Transport Layer Security (DTLS) Protocol {#JSSEC-GUID-D0F8B9C3-721B-43A4-B2CE-7512B175F76D .sect4}

<div>
Datagram Transport Layer Security (DTLS) protocol is designed to
construct "TLS over datagram" traffic that doesn\'t require or provide
reliable or in-order delivery of data. Java Secure Socket Extension
(JSSE) API and the SunJSSE security provider support the DTLS protocol.

Because the TLS requires a transparent reliable transport channel such
as TCP it can't be used to secure unreliable datagram traffic. DTLS is a
datagram-compatible variant of TLS.

The JSSE API now supports [DTLS Version
1.0](http://tools.ietf.org/html/rfc4347) and [DTLS Version
1.2](http://tools.ietf.org/html/rfc6347) along with Secure Socket Layer
(SSL) and Transport Layer Security (TLS) protocols.

The
[`javax.net.ssl.SSLEngine`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngine.html)
programming model is used by the JSSE API for DTLS.

</div>
<div class="sect5">
[]{#GUID-B62245D1-5337-4B51-B1F3-CA89099157C1}

##### The DTLS Handshake {#JSSEC-GUID-B62245D1-5337-4B51-B1F3-CA89099157C1 .sect5}

<div>
Before application data can be sent or received, the DTLS protocol
requires a handshake to establish cryptographic parameters. This
handshake requires a series of back-and-forth messages between the
client and server by the `SSLEngine`{.codeph} object.

<div class="section" id="GUID-B62245D1-5337-4B51-B1F3-CA89099157C1__THESSLHANDSHAKE-7D20D1E0">
DTLS handshake requires all messages be received properly. Thus, in
unreliable datagram traffic, missing or delayed packets must be
retransmitted. Since
[`javax.net.ssl.SSLEngine`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngine.html)
is not responsible for I/O operations, it is up to the application to
provide timers and signal the SSLEngine when a retransmission is needed.
It is important that you implement a timer and retransmission strategy
for your application. See [Handling Retransmissions in DTLS
Connections](java-secure-socket-extension-jsse-reference-guide.htm#GUID-6C8AA45B-EB45-4767-BBB4-B7C5A64A60B7 "In SSL/TLS over a reliable connection, data is guaranteed to arrive in the proper order, and retransmission is unnecessary. However, for DTLS, which often works over unreliable media, missing or delayed handshake messages must be retransmitted.").

The DTLS handshake includes the following stages:

1.  <span class="bold">Negotiating the cipher suite</span>

    The DTLS session begins with a negotiation between the client and
    the server as to which cipher suite they will use. A <span>cipher
    suite</span> is a set of cryptographic algorithms and key sizes that
    a computer can use to encrypt data. The cipher suite includes
    information about the public key exchange algorithms or key
    agreement algorithms, and cryptographic hash functions. The client
    tells the server which cipher suites it has available, and the
    server chooses the best mutually acceptable cipher suite.

    A cookie is exchanged between the client and server along with the
    cipher suite in order to prevent denial of service attacks (DoS).

2.  <span class="bold">Authenticating the server\'s identity
    (optional)</span>

    The authentication step is optional, but in the example of an
    e-commerce transaction over the web, the client chooses to
    authenticate the server. Authenticating the server allows the client
    to be sure that the server represents the entity that the client
    believes the server represents.

    To prove that a server belongs to the organization that it claims to
    represent, the server presents its public key certificate to the
    client. If this certificate is valid, then the client can be sure of
    the identity of the server.

    The client and server exchange information that allows them to agree
    on the same secret key. For example, with RSA, the client uses the
    server\'s public key, obtained from the public key certificate, to
    encrypt the secret key information. The client sends the encrypted
    secret key information to the server. Only the server can decrypt
    this message because the server\'s private key is required for this
    decryption.

3.  <span class="bold">Agreeing on encryption mechanisms</span>

    Both the client and the server now have access to the same secret
    key. With each message, they use the cryptographic hash function,
    chosen in the first step of the handshake, and shared secret
    information, to compute an HMAC that they append to the message.
    They then use the secret key and the secret key algorithm negotiated
    in the first step of the handshake to encrypt the secure data and
    the HMAC. The client and server can now communicate securely using
    their encrypted and hashed data.

</div>
<!-- class="section" -->

</div>
<div class="sect6">
[]{#GUID-F1BFB231-BE35-4B14-BB8D-7F33D31A117D}

###### The DTLS Handshake Message Exchange {#JSSEC-GUID-F1BFB231-BE35-4B14-BB8D-7F33D31A117D .sect6}

<div>
In a DTLS handshake, series of back-and-forth messages are exchanged
between the client and server by the `SSLEngine`{.codeph} object.

[Figure
8-7](java-secure-socket-extension-jsse-reference-guide.htm#GUID-F1BFB231-BE35-4B14-BB8D-7F33D31A117D__GUID-72C1D49C-0A80-4548-BF96-2D72E1C65912)
shows the sequence of messages that are exchanged in the DTLS handshake.
Messages that are sent only in certain situations are noted as optional.
Each message is described following the figure.

To know more about DTLS handshake messages, see [DTLS Version
1.0](http://tools.ietf.org/html/rfc4347) and [DTLS Version
1.2](http://tools.ietf.org/html/rfc6347).

<div class="figure" id="GUID-F1BFB231-BE35-4B14-BB8D-7F33D31A117D__GUID-72C1D49C-0A80-4548-BF96-2D72E1C65912">
Figure 8-7 DTLS Handshake

![Description of Figure 8-7
follows](img/dtls-handshake.png "Description of Figure 8-7 follows")\
[Description of \"Figure 8-7 DTLS
Handshake\"](img_text/dtls-handshake.htm)

</div>
<!-- class="figure" -->

The following handshake messages are exchanged between the client and
server during DTLS handshake:

1.  <span class="bold">ClientHello:</span>

    The client sends the server information including the highest
    version of DTLS that it supports and a list of the cipher suites
    that it supports. The cipher suite information includes
    cryptographic algorithms and key sizes.

2.  <span class="bold">HelloVerifyRequest:</span>

    The server responds to the ClientHello message from the client with
    a cookie.

3.  <span class="bold">ClientHello:</span>

    The client sends a second ClientHello message to the server with
    highest version of DTLS that it supports and a list of the cipher
    suites that it supports. The cookie received in the
    HelloVerifyRequest is sent back to the server.

4.  <span class="bold">ServerHello:</span>

    The server chooses the highest version of DTLS and the best cipher
    suite that both the client and server support and sends this
    information to the client.

5.  (Optional) <span class="bold">Certificate:</span>

    The server sends the client a certificate or a certificate chain. A
    certificate chain typically begins with the server\'s public key
    certificate and ends with the certificate authority\'s root
    certificate. This message is optional, but is used whenever server
    authentication is required

6.  (Optional) <span class="bold">CertificateRequest:</span>

    If the server must authenticate the client, then it sends the client
    a certificate request. In Internet applications, this message is
    rarely sent.

7.  (Optional) <span class="bold">ServerKeyExchange:</span>

    The server sends the client a server key exchange message if the
    public key information from the Certificate is not sufficient for
    key exchange. For example, in cipher suites based on Diffie-Hellman
    (DH), this message contains the server\'s DH public key.

8.  <span class="bold">ServerHelloDone:</span>

    The server tells the client that it is finished with its initial
    negotiation messages.

9.  (Optional) <span class="bold">Certificate:</span>

    If the server Certificate request from the client, the client sends
    its certificate chain, just as the server did previously.

    <div class="p">
    <div class="infoboxnote" id="GUID-F1BFB231-BE35-4B14-BB8D-7F33D31A117D__GUID-296D3B3F-97C6-466C-BDB7-716D4EDEA51C">
    Note:

    Only a few Internet server applications ask for a certificate from
    the client.

    </div>
    </div>
10. <span class="bold">ClientKeyExchange:</span>

    The client generates information used to create a key to use for
    symmetric encryption. For RSA, the client then encrypts this key
    information with the server\'s public key and sends it to the
    server. For cipher suites based on DH, this message contains the
    client\'s DH public key.

11. (Optional) <span class="bold">CertificateVerify:</span>

    This message is sent by the client when the client presents a
    certificate as previously explained. Its purpose is to allow the
    server to complete the process of authenticating the client. When
    this message is used, the client sends information that it digitally
    signs using a cryptographic hash function. When the server decrypts
    this information with the client\'s public key, the server is able
    to authenticate the client.

12. <span class="bold">ChangeCipherSpec:</span>

    The client sends a message telling the server that subsequent data
    will be protected under the newly negotiated CipherSpec and keys and
    the data is encrypted

13. <span class="bold">Finished:</span>

    The client tells the server that it is ready for secure data
    communication to begin.

14. <span class="bold">ChangeCipherSpec:</span>

    The server sends a message telling the client that subsequent data
    will be protected under the newly negotiated CipherSpec and keys and
    the data is encrypted.

15. <span class="bold">Finished:</span>

    The server tells the client that it is ready for secure data
    communication to begin. This is the end of the DTLS handshake.

</div>
</div>
<div class="sect6">
[]{#GUID-E1E48823-8B76-456A-88FA-B4D531183520}

###### Handshaking Again (Renegotiation) {#JSSEC-GUID-E1E48823-8B76-456A-88FA-B4D531183520 .sect6}

<div>
Once the initial handshake is finished and application data is flowing,
either side is free to initiate a new handshake at any time. An
application might like to use a stronger cipher suite for especially
critical operations, or a server application might want to require
client authentication.

Regardless of the reason, the new handshake takes place over the
existing encrypted session, and application data and handshake messages
are interleaved until a new session is established.

Your application can initiate a new handshake by using the
`SSLEngine.beginHandshake()`{.codeph} method.

<div class="infoboxnote" id="GUID-E1E48823-8B76-456A-88FA-B4D531183520__GUID-B4E262C5-520F-4941-B49D-791402E56838">
Note:

A protocol flaw related to renegotiation was found in 2009. The protocol
and the Java SE implementation have both been fixed. See [Transport
Layer Security (TLS) Renegotiation
Issue](java-secure-socket-extension-jsse-reference-guide.htm#GUID-9C767872-3A6C-4AD1-9805-49F112A0FA28 "In the fall of 2009, a flaw was discovered in the SSL/TLS protocols. A fix to the protocol was developed by the IETF TLS Working Group, and current versions of the JDK contain this fix. This section describes the situation in much more detail, along with interoperability issues when communicating with older implementations that do not contain this protocol fix.").

</div>
<div class="example" id="GUID-E1E48823-8B76-456A-88FA-B4D531183520__GUID-E31F4DB7-7133-414A-A7A8-4AECA3A8A5CA">
Example 8-4 Sample Code for Handling DTLS handshake Status and Overall
Status

``` {.oac_no_warn dir="ltr"}
void handshake(SSLEngine engine, DatagramSocket socket, SocketAddress peerAddr) throws Exception {
    boolean endLoops = false;
    // private static int MAX_HANDSHAKE_LOOPS = 60;
    int loops = MAX_HANDSHAKE_LOOPS;
    engine.beginHandshake();
    while (!endLoops && (serverException == null) && (clientException == null)) {
        if (--loops < 0) {
            throw new RuntimeException("Too many loops to produce handshake packets");
        }
        SSLEngineResult.HandshakeStatus hs = engine.getHandshakeStatus();
        if (hs == SSLEngineResult.HandshakeStatus.NEED_UNWRAP ||
                hs == SSLEngineResult.HandshakeStatus.NEED_UNWRAP_AGAIN) {
            ByteBuffer iNet;
            ByteBuffer iApp;
            if (hs == SSLEngineResult.HandshakeStatus.NEED_UNWRAP) {
                // Receive ClientHello request and other SSL/TLS/DTLS records
                byte[] buf = new byte[1024];
                DatagramPacket packet = new DatagramPacket(buf, buf.length);
                try {
                    socket.receive(packet);
                } catch (SocketTimeoutException ste) {
                    // Retransmit the packet if timeout
                    List <Datagrampacket> packets = onReceiveTimeout(engine, peerAddr);
                    for (DatagramPacket p : packets) {
                        socket.send(p);
                    }
                    continue;
                }
                iNet = ByteBuffer.wrap(buf, 0, packet.getLength());
                iApp = ByteBuffer.allocate(1024);
            } else {
                iNet = ByteBuffer.allocate(0);
                iApp = ByteBuffer.allocate(1024);
            }
            SSLEngineResult r = engine.unwrap(iNet, iApp);
            SSLEngineResult.Status rs = r.getStatus();
            hs = r.getHandshakeStatus();
            if (rs == SSLEngineResult.Status.BUFFER_OVERFLOW) {
                // The client maximum fragment size config does not work?
                throw new Exception("Buffer overflow: " +
                                    "incorrect client maximum fragment size");
            } else if (rs == SSLEngineResult.Status.BUFFER_UNDERFLOW) {
                // Bad packet, or the client maximum fragment size
                // config does not work?
                if (hs != SSLEngineResult.HandshakeStatus.NOT_HANDSHAKING) {
                    throw new Exception("Buffer underflow: " +
                                        "incorrect client maximum fragment size");
                } // Otherwise, ignore this packet
            } else if (rs == SSLEngineResult.Status.CLOSED) {
                endLoops = true;
            } // Otherwise, SSLEngineResult.Status.OK
            if (rs != SSLEngineResult.Status.OK) {
                continue;
            }
        } else if (hs == SSLEngineResult.HandshakeStatus.NEED_WRAP) {
            // Call a function to produce handshake packets
            List <DatagramPacket> packets = produceHandshakePackets(engine, peerAddr);
            for (DatagramPacket p : packets) {
                socket.send(p);
            }
        } else if (hs == SSLEngineResult.HandshakeStatus.NEED_TASK) {
            runDelegatedTasks(engine);
        } else if (hs == SSLEngineResult.HandshakeStatus.NOT_HANDSHAKING) {
            // OK, time to do application data exchange
            endLoops = true;
        } else if (hs == SSLEngineResult.HandshakeStatus.FINISHED) {
            endLoops = true;
        }
    }
    SSLEngineResult.HandshakeStatus hs = engine.getHandshakeStatus();
    if (hs != SSLEngineResult.HandshakeStatus.NOT_HANDSHAKING) {
        throw new Exception("Not ready for application data yet");
    }
}
```

</div>
<!-- class="example" -->

</div>
</div>
</div>
<div class="sect5">
[]{#GUID-6C8AA45B-EB45-4767-BBB4-B7C5A64A60B7}

##### Handling Retransmissions in DTLS Connections {#JSSEC-GUID-6C8AA45B-EB45-4767-BBB4-B7C5A64A60B7 .sect5}

<div>
In SSL/TLS over a reliable connection, data is guaranteed to arrive in
the proper order, and retransmission is unnecessary. However, for DTLS,
which often works over unreliable media, missing or delayed handshake
messages must be retransmitted.

<div class="section">
The `SSLEngine`{.codeph} class operates in a completely
transport-neutral manner, and the application layer performs all I/O.
Because the `SSLEngine`{.codeph} class isn't responsible for I/O, the
application instead is responsible for providing timers and signalling
the `SSLEngine`{.codeph} class when a retransmission is needed. The
application layer must determine the right timeout value and when to
trigger the timeout event. During handshaking, if an
`SSLEngine`{.codeph} object is in `HandshakeStatus.NEED_UNWRAP`{.codeph}
state, a call to <span class="apiname">SSLEngine.wrap()</span> means
that the previous packets were lost, and must be retransmitted. For such
cases, the DTLS implementation of the `SSLEngine`{.codeph} class takes
the responsibility to wrap the previous necessary handshaking messages
again if necessary.

<div class="infoboxnote" id="GUID-6C8AA45B-EB45-4767-BBB4-B7C5A64A60B7__GUID-3AC8121B-28CE-4611-8E66-06E9CEC39B5E">
Note:

In a DTLS engine, only handshake messages must be properly exchanged.
Application data can handle packet loss without the need for timers.

</div>
</div>
<!-- class="section" -->

</div>
<div class="sect6">
[]{#GUID-32494D9D-B0FC-4DFC-B747-F4115B6112E3}

###### Handling Retransmission in an Application {#JSSEC-GUID-32494D9D-B0FC-4DFC-B747-F4115B6112E3 .sect6}

<div>
`SSLEngine.unwrap()`{.codeph} and `SSLEngine.wrap()`{.codeph} can be
used together to handle retransmission in an application.

<div class="section">
[Figure
8-8](java-secure-socket-extension-jsse-reference-guide.htm#GUID-32494D9D-B0FC-4DFC-B747-F4115B6112E3__GUID-62CAEA17-2745-42AE-94C6-2E35852FC63A)
shows a typical scenario for handling DTLS handshaking retransmission:

<div class="figure" id="GUID-32494D9D-B0FC-4DFC-B747-F4115B6112E3__GUID-62CAEA17-2745-42AE-94C6-2E35852FC63A">
Figure 8-8 DTLS Handshake Retransmission State Flow

![This image illustrates the DTLS handshake retransmission state flow.
The flow is described in the numbered steps that follow the
image.](img/state-flow-need_unwrap_again_new.png "This image illustrates the DTLS handshake retransmission state flow. The flow is described in the numbered steps that follow the image.")

</div>
<!-- class="figure" -->

</div>
<!-- class="section" -->

1.  <span>Create and initialize an instance of DTLS
    `SSLEngine`{.codeph}. </span>
    <div>
    See [Creating an SSLEngine
    Object](java-secure-socket-extension-jsse-reference-guide.htm#GUID-16B697CD-77EB-468F-94A1-04254BA75FD7 "Use the SSLContext.createSSLEngine() method to create an SSLEngine object.").
    The DTLS handshake process begins. See [The DTLS
    Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-B62245D1-5337-4B51-B1F3-CA89099157C1 "Before application data can be sent or received, the DTLS protocol requires a handshake to establish cryptographic parameters. This handshake requires a series of back-and-forth messages between the client and server by the SSLEngine object.").
    </div>
2.  <span>If the handshake status is
    `HandshakeStatus.NEED_UNWRAP`{.codeph}, wait for data from
    network.</span>
3.  <span>If the timer times out, it indicates that the previous
    delivered handshake messages may have been lost.</span>

    <div>
    <div class="infoboxnote" id="GUID-32494D9D-B0FC-4DFC-B747-F4115B6112E3__GUID-39A9DD22-1E2F-4924-8960-9DCAF232DE86">
    Note:

    In DTLS handshaking retransmission, the determined handshake status
    isn't necessarily `HandshakeStatus.NEED_WRAP`{.codeph} for the call
    to `SSLEngine.wrap()`{.codeph}.

    </div>
    </div>
4.  <span>Call `SSLEngine.wrap()`{.codeph}.</span>
5.  <span>The wrapped packets are delivered.</span>

</div>
</div>
<div class="sect6">
[]{#GUID-F8FB4BE7-3A43-41FB-8642-07848FCA9381}

###### Handling a Buffered Handshake Message in an Application {#JSSEC-GUID-F8FB4BE7-3A43-41FB-8642-07848FCA9381 .sect6}

<div>
Datagram transport doesn't require or provide reliable or in-order
delivery of data. Handshake messages may be lost or need to be
reordered. In the DTLS implementation, a handshake message may need to
be buffered for future handling before all previous messages have been
received.

<div class="section">
The DTLS implementation of `SSLEngine`{.codeph} takes the responsibility
to reorder handshake messages. Handshake message buffering and
reordering are transparent to applications.

However, applications must manage
`HandshakeStatus.NEED_UNWRAP_AGAIN`{.codeph} status. This status
indicates that for the next
<span class="apiname">SSLEngine.unwrap()</span> operation no additional
data from the remote side is required.

[Figure
8-9](java-secure-socket-extension-jsse-reference-guide.htm#GUID-F8FB4BE7-3A43-41FB-8642-07848FCA9381__GUID-693172EF-782D-4676-BA14-27B0794F8B72)
shows a typical scenario for using the
`HandshakeStatus.NEED_UNWRAP_AGAIN`{.codeph}.

<div class="figure" id="GUID-F8FB4BE7-3A43-41FB-8642-07848FCA9381__GUID-693172EF-782D-4676-BA14-27B0794F8B72">
Figure 8-9 State Machine of DTLS Buffered Handshake with
NEED\_UNWRAP\_AGAIN

![This flowchart illustrates the sequence of messages that are exchanged
in the DTLS buffered handshake. Messages that are sent only in certain
situations are noted as optional. The sequence is described in the
numbered list that follows the
image.](img/dtls-buffered-handshake-message-new.png "This flowchart illustrates the sequence of messages that are exchanged in the DTLS buffered handshake. Messages that are sent only in certain situations are noted as optional. The sequence is described in the numbered list that follows the image.")

</div>
<!-- class="figure" -->

</div>
<!-- class="section" -->

1.  <span>Create and initialize an instance of DTLS
    `SSLEngine`{.codeph}.</span>
    <div>
    See [Creating an SSLEngine
    Object](java-secure-socket-extension-jsse-reference-guide.htm#GUID-16B697CD-77EB-468F-94A1-04254BA75FD7 "Use the SSLContext.createSSLEngine() method to create an SSLEngine object.").
    The DTLS handshake process begins, see [The DTLS
    Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-B62245D1-5337-4B51-B1F3-CA89099157C1 "Before application data can be sent or received, the DTLS protocol requires a handshake to establish cryptographic parameters. This handshake requires a series of back-and-forth messages between the client and server by the SSLEngine object.").
    </div>
2.  **Optional:** <span>If the handshake status is
    `HandshakeStatus.NEED_UNWRAP`{.codeph}, wait for data from
    network.</span>
3.  **Optional:** <span>If you received the network data, call
    <span class="apiname">SSLEngine.unwrap()</span>.</span>
4.  <span>Determine the handshake status for next processing. The
    handshake status can be
    `HandshakeStatus.NEED_UNWRAP_AGAIN`{.codeph},
    `HandshakeStatus.NEED_UNWRAP`{.codeph}, or
    `HandshakeStatus.NEED_WRAP`{.codeph}.</span>

    -   If the handshake status is
        `HandshakeStatus.NEED_UNWRAP_AGAIN`{.codeph}, call
        <span class="apiname">SSLEngine.unwrap()</span>.

    <div>
    <div class="infoboxnote" id="GUID-F8FB4BE7-3A43-41FB-8642-07848FCA9381__GUID-4201EFCD-11F7-4175-A530-80F779E79E05">
    Note:

    For `HandshakeStatus.NEED_UNWRAP_AGAIN`{.codeph} status, no
    additional data from the network is required for an
    <span class="apiname">SSLEngine.unwrap()</span> operation.

    </div>
    </div>
5.  <span>Determine the handshake status for further processing. The
    handshake status can be
    `HandshakeStatus.NEED_UNWRAP_AGAIN`{.codeph},
    `HandshakeStatus.NEED_UNWRAP`{.codeph}, or
    `HandshakeStatus.NEED_WRAP`{.codeph}.</span>

</div>
</div>
</div>
</div>
<div class="sect4">
[]{#GUID-4D854666-433A-4672-B902-565CC7AEE0BF}

#### Creating an SSLEngine Object for DTLS {#JSSEC-GUID-4D854666-433A-4672-B902-565CC7AEE0BF .sect4}

<div>
The following examples illustrate how to create an `SSLEngine`{.codeph}
object for DTLS.

<div class="p">
<div class="infoboxnote" id="GUID-4D854666-433A-4672-B902-565CC7AEE0BF__GUID-4E9C2C41-E06E-4412-A9C8-20DBFA93CC0B">
Note:

The server name and port number are not used for communicating with the
server (all transport is the responsibility of the application). They
are hints to the JSSE provider to use for DTLS session caching, and for
Kerberos-based cipher suite implementations to determine which server
credentials should be obtained.

</div>
</div>
<div class="example" id="GUID-4D854666-433A-4672-B902-565CC7AEE0BF__THEFOLLOWINGSAMPLECODECREATESASSLEN-225FCB3A">
Example 8-5 Sample Code for Creating an SSLEngine Client for DTLS with
PKCS12 as Keystore

The following sample code creates an
<span class="apiname">SSLEngine</span> client for DTLS that uses PKCS12
as keystore:

``` {.codeblock dir="ltr"}
    import javax.net.ssl.*;
    import java.security.*;

    // Create and initialize the SSLContext with key material
    char[] passphrase = "passphrase".toCharArray();

    // First initialize the key and trust material
    KeyStore ksKeys = KeyStore.getInstance("PKCS12");
    ksKeys.load(new FileInputStream("testKeys"), passphrase);
    KeyStore ksTrust = KeyStore.getInstance("PKCS12");
    ksTrust.load(new FileInputStream("testTrust"), passphrase);

    // KeyManagers decide which key material to use
    KeyManagerFactory kmf = KeyManagerFactory.getInstance("PKIX");
    kmf.init(ksKeys, passphrase);

    // TrustManagers decide whether to allow connections
    TrustManagerFactory tmf = TrustManagerFactory.getInstance("PKIX");
    tmf.init(ksTrust);

    // Get an instance of SSLContext for DTLS protocols
    sslContext = SSLContext.getInstance("DTLS");
    sslContext.init(kmf.getKeyManagers(), tmf.getTrustManagers(), null);

    // Create the engine
    SSLEngine engine = sslContext.createSSLengine(hostname, port);

    // Use engine as client
    engine.setUseClientMode(true);
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-4D854666-433A-4672-B902-565CC7AEE0BF__THEFOLLOWINGSAMPLECODECREATESASSLEN-225FC3CE">
Example 8-6 Sample Code for Creating an SSLEngine Server for DTLS with
PKCS12 as Keystore

The following sample code creates an
<span class="apiname">SSLEngine</span> server for DTLS that uses PKCS12
as keystore:

``` {.codeblock dir="ltr"}
    import javax.net.ssl.*;
    import java.security.*;

    // Create and initialize the SSLContext with key material
    char[] passphrase = "passphrase".toCharArray();

    // First initialize the key and trust material
    KeyStore ksKeys = KeyStore.getInstance("PKCS12");
    ksKeys.load(new FileInputStream("testKeys"), passphrase);
    KeyStore ksTrust = KeyStore.getInstance("PKCS12");
    ksTrust.load(new FileInputStream("testTrust"), passphrase);

    // KeyManagers decide which key material to use
    KeyManagerFactory kmf = KeyManagerFactory.getInstance("PKIX");
    kmf.init(ksKeys, passphrase);

    // TrustManagers decide whether to allow connections
    TrustManagerFactory tmf = TrustManagerFactory.getInstance("PKIX");
    tmf.init(ksTrust);

    // Get an SSLContext for DTLS Protocol without authentication
    sslContext = SSLContext.getInstance("DTLS");
    sslContext.init(null, null, null);

    // Create the engine
    SSLEngine engine = sslContext.createSSLeEngine(hostname, port);

    // Use the engine as server
    engine.setUseClientMode(false);

    // Require client authentication
    engine.setNeedClientAuth(true);
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-80EBB1BB-8A36-4B6F-BC35-AF235F30EF45}

#### Generating and Processing DTLS Data {#JSSEC-GUID-80EBB1BB-8A36-4B6F-BC35-AF235F30EF45 .sect4}

<div>
A DTLS handshake and a SSL/TLS handshake generate and process data
similarly. (See [Generating and Processing SSL/TLS
Data](java-secure-socket-extension-jsse-reference-guide.htm#GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4 "The two main SSLEngine methods are wrap() and unwrap(). They are responsible for generating and consuming network data respectively. Depending on the state of the SSLEngine object, this data might be handshake or application data.").)
They both use the <span class="apiname">SSLEngine.wrap()</span> and
<span class="apiname">SSLEngine.wrap()</span> methods to generate and
consume network data, respectively.

The following diagram shows the state machine during a typical DTLS
handshake, with corresponding messages and statuses:

<div class="figure" id="GUID-80EBB1BB-8A36-4B6F-BC35-AF235F30EF45__GUID-85F0E791-66C0-479B-855B-86509CE249FE">
Figure 8-10 State Machine during DTLS Handshake

![Description of Figure 8-10
follows](img/jsse-handshake-state-machine-new.png "Description of Figure 8-10 follows")\
[Description of \"Figure 8-10 State Machine during DTLS
Handshake\"](img_text/jsse-handshake-state-machine-new.htm)

</div>
<!-- class="figure" -->

<div class="section">
Difference Between the SSL/TLS and DTLS SSLEngine.wrap() Methods

<div class="p">
The `SSLEngine.wrap()`{.codeph} method for DTLS is different from
SSL/TLS as follows:

-   In the SSL/TLS implementation of `SSLEngine`{.codeph}, the output
    buffer of `SSLEngine.wrap()`{.codeph} contains one or more TLS
    records (due to the TLSv1 BEAST Cipher Block Chaining
    vulnerability).

-   In the DTLS implementation of `SSLEngine`{.codeph}, the output
    buffer of `SSLEngine.wrap()`{.codeph} contains at most one record,
    so that every DTLS record can be marshaled and delivered to the
    datagram layer individually.

<div class="infoboxnote" id="GUID-80EBB1BB-8A36-4B6F-BC35-AF235F30EF45__GUID-52C4A89B-A524-44E5-9626-136B0C65EB0C">
Note:

Each record produced by `SSLEngine.wrap()`{.codeph} should comply to the
maximum packet size limitation as specified by
`SSLParameters.getMaximumPacketSize()`{.codeph}.

</div>
 

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744}

#### Understanding SSLEngine Operation Statuses {#JSSEC-GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744 .sect4}

<div>
The status of the SSLEngine is represented by
`SSLEngineResult.Status`{.codeph}.

<div class="section">
To indicate the status of the engine and what actions the application
should take, the `SSLEngine.wrap()`{.codeph} and
`SSLEngine.unwrap()`{.codeph} methods return an
[`SSLEngineResult`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngineResult.html)
instance, as shown in [Example
8-2](java-secure-socket-extension-jsse-reference-guide.htm#GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4__GUID-223D79BF-70AD-4F6C-B472-81C28C010BD9).
This `SSLEngineResult`{.codeph} object contains two pieces of status
information: the overall status of the engine and the handshaking
status.

The possible overall statuses are represented by the
`SSLEngineResult.Status`{.codeph} enum. The following statuses are
available:

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-F79D56D5-8F54-4E4E-ACFB-4BEF8B9B9E7D}`OK`{.codeph}
:   There was no error.

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-55BEDBCE-8E29-45B8-98D1-9E6929540C3D}`CLOSED`{.codeph}
:   The operation closed the `SSLEngine`{.codeph} or the operation could
    not be completed because it was already closed.

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-C5AE7AA6-7EA1-447A-B443-6895062E1F87}`BUFFER_UNDERFLOW`{.codeph}
:   The input buffer had insufficient data, indicating that the
    application must obtain more data from the peer (for example, by
    reading more data from the network).

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-B67FEDA3-B9B6-4730-9C49-9D3D60E3255C}`BUFFER_OVERFLOW`{.codeph}
:   The output buffer had insufficient space to hold the result,
    indicating that the application must clear or enlarge the
    destination buffer.

[Example
8-7](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__EXAMPLE4HANDLINGBUFFER_UNDERFLOWAND-78F60126)
illustrates how to handle the `BUFFER_UNDERFLOW`{.codeph} and
`BUFFER_OVERFLOW`{.codeph} statuses of the `SSLEngine.unwrap()`{.codeph}
method. It uses `SSLSession.getApplicationBufferSize()`{.codeph} and
`SSLSession.getPacketBufferSize()`{.codeph} to determine how large to
make the byte buffers.

The possible handshaking statuses are represented by the
`SSLEngineResult.HandshakeStatus`{.codeph} enum. They represent whether
handshaking has completed, whether the caller must obtain more
handshaking data from the peer or send more handshaking data to the
peer, and so on. The following handshake statuses are available:

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-6738EEFA-1FE5-48B8-9E03-B99B688FD77F}`FINISHED`{.codeph}
:   The `SSLEngine`{.codeph} has just finished handshaking.

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-29199762-DA07-4595-B35D-A0271A229020}`NEED_TASK`{.codeph}
:   The `SSLEngine`{.codeph} needs the results of one (or more)
    delegated tasks before handshaking can continue.

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-DEFA0BD8-5FC5-41E8-AEB4-82542DDDF7CA}`NEED_UNWRAP`{.codeph}
:   The `SSLEngine`{.codeph} needs to receive data from the remote side
    before handshaking can continue.

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-C4CCD4B8-357E-4F8B-95E2-89B2A255D9E3}`NEED_UNWRAP_AGAIN`{.codeph}
:   The `SSLEngine`{.codeph} needs to unwrap before handshaking can
    continue. This value indicates that not-yet-interpreted data has
    been previously received from the remote side and does not need to
    be received again; the data has been brought into the JSSE framework
    but has not been processed yet.

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-2FCB0DC1-F723-4036-B8DA-0A885ECA17E7}`NEED_WRAP`{.codeph}
:   The `SSLEngine`{.codeph} must send data to the remote side before
    handshaking can continue, so
    <span class="apiname">SSLEngine.wrap()</span> should be called.

[<!-- -->]{#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-215B8B63-813A-4B80-98DE-3C16A0F2926A}`NOT_HANDSHAKING`{.codeph}
:   The `SSLEngine`{.codeph} is not currently handshaking.

Having two statuses per result allows the
<span class="apiname">SSLEngine</span> to indicate that the application
must take two actions: one in response to the handshaking and one
representing the overall status of the `wrap()`{.codeph} and
`unwrap()`{.codeph} methods. For example, the engine might, as the
result of a single `SSLEngine.unwrap()`{.codeph} call, return
`SSLEngineResult.Status.OK`{.codeph} to indicate that the input data was
processed successfully and
`SSLEngineResult.HandshakeStatus.NEED_UNWRAP`{.codeph} to indicate that
the application should obtain more SSL/TLS/DTLS encoded data from the
peer and supply it to `SSLEngine.unwrap()`{.codeph} again so that
handshaking can continue. As you can see, the previous examples were
greatly simplified; they would need to be expanded significantly to
properly handle all of these statuses.

[Example
8-9](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-CEB4C19E-7DB9-4CD8-8315-8FEDD212BAD3)
and [Example
8-8](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__EXAMPLE5CHECKINGANDPROCESSINGHANDSH-78F5FE16)
illustrate how to process handshaking data by checking handshaking
status and the overall status of the `wrap()`{.codeph} and
`unwrap()`{.codeph} methods.

</div>
<!-- class="section" -->

<div class="example" id="GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__EXAMPLE4HANDLINGBUFFER_UNDERFLOWAND-78F60126">
Example 8-7 Sample Code for Handling BUFFER\_UNDERFLOW and
BUFFER\_OVERFLOW

The following code sample illustrates how to handle BUFFER\_UNDERFLOW
and BUFFER\_OVERFLOW status:

``` {.codeblock dir="ltr"}
    SSLEngineResult res = engine.unwrap(peerNetData, peerAppData);
    switch (res.getStatus()) {

    case BUFFER_OVERFLOW:
            // Maybe need to enlarge the peer application data buffer.
        if (engine.getSession().getApplicationBufferSize() > peerAppData.capacity()) {
            // enlarge the peer application data buffer
        } else {
            // compact or clear the buffer
        }
        // retry the operation
    break;

    case BUFFER_UNDERFLOW:
        // Maybe need to enlarge the peer network packet buffer
        if (engine.getSession().getPacketBufferSize() > peerNetData.capacity()) {
        // enlarge the peer network packet buffer
        } else {
        // compact or clear the buffer
        }
        // obtain more inbound network data and then retry the operation
       break;

       // Handle other status: CLOSED, OK
       // ...
    }
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__EXAMPLE5CHECKINGANDPROCESSINGHANDSH-78F5FE16">
Example 8-8 Sample Code for Checking and Processing Handshaking Statuses
and Overall Statuses

The following code sample illustrates how to process handshaking data by
checking handshaking status and the overall status of the
<span class="apiname">wrap()</span> and
<span class="apiname">unwrap()</span> methods:

``` {.codeblock dir="ltr"}
void doHandshake(SocketChannel socketChannel, SSLEngine engine,
    ByteBuffer myNetData, ByteBuffer peerNetData) throws Exception {

    // Create byte buffers to use for holding application data
    int appBufferSize = engine.getSession().getApplicationBufferSize();
    ByteBuffer myAppData = ByteBuffer.allocate(appBufferSize);
    ByteBuffer peerAppData = ByteBuffer.allocate(appBufferSize);

    // Begin handshake
    engine.beginHandshake();
    SSLEngineResult.HandshakeStatus hs = engine.getHandshakeStatus();

    // Process handshaking message
    while (hs != SSLEngineResult.HandshakeStatus.FINISHED &&
        hs != SSLEngineResult.HandshakeStatus.NOT_HANDSHAKING) {

        switch (hs) {

        case NEED_UNWRAP:
            // Receive handshaking data from peer
            if (socketChannel.read(peerNetData) < 0) {
                // The channel has reached end-of-stream
            }

            // Process incoming handshaking data
            peerNetData.flip();
            SSLEngineResult res = engine.unwrap(peerNetData, peerAppData);
            peerNetData.compact();
            hs = res.getHandshakeStatus();

            // Check status
            switch (res.getStatus()) {
            case OK :
                // Handle OK status
                break;

            // Handle other status: BUFFER_UNDERFLOW, BUFFER_OVERFLOW, CLOSED
            // ...
            }
            break;

        case NEED_WRAP :
            // Empty the local network packet buffer.
            myNetData.clear();

            // Generate handshaking data
            res = engine.wrap(myAppData, myNetData);
            hs = res.getHandshakeStatus();

            // Check status
            switch (res.getStatus()) {
            case OK :
                myNetData.flip();

                // Send the handshaking data to peer
                while (myNetData.hasRemaining()) {
                    socketChannel.write(myNetData);
                }
                break;

            // Handle other status:  BUFFER_OVERFLOW, BUFFER_UNDERFLOW, CLOSED
            // ...
            }
            break;

        case NEED_TASK :
            // Handle blocking tasks
            break;

            // Handle other status:  // FINISHED or NOT_HANDSHAKING
            // ...
        }
    }

    // Processes after handshaking
    // ...
}
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744__GUID-CEB4C19E-7DB9-4CD8-8315-8FEDD212BAD3">
Example 8-9 Sample Code for Handling DTLS handshake Status and Overall
Status

The following code sample illustrates how to handle DTLS handshake
status:

``` {.oac_no_warn dir="ltr"}
void handshake(SSLEngine engine, DatagramSocket socket,
               SocketAddress peerAddr) throws Exception {
    boolean endLoops = false;
    // private static int MAX_HANDSHAKE_LOOPS = 60;
    int loops = MAX_HANDSHAKE_LOOPS;
    engine.beginHandshake();
    while (!endLoops && (serverException == null) && (clientException == null)) {
        if (--loops < 0) {
            throw new RuntimeException("Too many loops to produce handshake packets");
        }
        SSLEngineResult.HandshakeStatus hs = engine.getHandshakeStatus();
        if (hs == SSLEngineResult.HandshakeStatus.NEED_UNWRAP ||
                hs == SSLEngineResult.HandshakeStatus.NEED_UNWRAP_AGAIN) {
            ByteBuffer iNet;
            ByteBuffer iApp;
            if (hs == SSLEngineResult.HandshakeStatus.NEED_UNWRAP) {
                // receive ClientHello request and other SSL/TLS/DTLS records
                byte[] buf = new byte[1024];
                DatagramPacket packet = new DatagramPacket(buf, buf.length);
                try {
                    socket.receive(packet);
                } catch (SocketTimeoutException ste) {
                    // retransmit the packet if timeout
                    List <Datagrampacket> packets =
                        onReceiveTimeout(engine, peerAddr);
                    for (DatagramPacket p : packets) {
                        socket.send(p);
                    }
                    continue;
                }
                iNet = ByteBuffer.wrap(buf, 0, packet.getLength());
                iApp = ByteBuffer.allocate(1024);
            } else {
                iNet = ByteBuffer.allocate(0);
                iApp = ByteBuffer.allocate(1024);
            }
            SSLEngineResult r = engine.unwrap(iNet, iApp);
            SSLEngineResult.Status rs = r.getStatus();
            hs = r.getHandshakeStatus();
            if (rs == SSLEngineResult.Status.BUFFER_OVERFLOW) {
                // the client maximum fragment size config does not work?
                throw new Exception("Buffer overflow: " +
                                    "incorrect client maximum fragment size");
            } else if (rs == SSLEngineResult.Status.BUFFER_UNDERFLOW) {
                // bad packet, or the client maximum fragment size
                // config does not work?
                if (hs != SSLEngineResult.HandshakeStatus.NOT_HANDSHAKING) {
                    throw new Exception("Buffer underflow: " +
                                        "incorrect client maximum fragment size");
                } // otherwise, ignore this packet
            } else if (rs == SSLEngineResult.Status.CLOSED) {
                endLoops = true;
            }   // otherwise, SSLEngineResult.Status.OK:
            if (rs != SSLEngineResult.Status.OK) {
                continue;
            }
        } else if (hs == SSLEngineResult.HandshakeStatus.NEED_WRAP) {
            List <DatagramPacket> packets =
                // Call a function to produce handshake packets
                produceHandshakePackets(engine, peerAddr);
            for (DatagramPacket p : packets) {
                socket.send(p);
            }
        } else if (hs == SSLEngineResult.HandshakeStatus.NEED_TASK) {
            runDelegatedTasks(engine);
        } else if (hs == SSLEngineResult.HandshakeStatus.NOT_HANDSHAKING) {
            // OK, time to do application data exchange.
            endLoops = true;
        } else if (hs == SSLEngineResult.HandshakeStatus.FINISHED) {
            endLoops = true;
        }
    }
    SSLEngineResult.HandshakeStatus hs = engine.getHandshakeStatus();
    if (hs != SSLEngineResult.HandshakeStatus.NOT_HANDSHAKING) {
        throw new Exception("Not ready for application data yet");
    }
}
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-7ED13982-53B2-455B-9198-3289F19905B6}

#### Dealing With Blocking Tasks {#JSSEC-GUID-7ED13982-53B2-455B-9198-3289F19905B6 .sect4}

<div>
<div class="section">
During handshaking, an `SSLEngine`{.codeph} might encounter tasks that
can block or take a long time. For example, a `TrustManager`{.codeph}
may need to connect to a remote certificate validation service, or a
`KeyManager`{.codeph} might need to prompt a user to determine which
certificate to use as part of client authentication. To preserve the
nonblocking nature of `SSLEngine`{.codeph}, when the engine encounters
such a task, it will return
`SSLEngineResult.HandshakeStatus.NEED_TASK`{.codeph}. Upon receiving
this status, the application should invoke
`SSLEngine.getDelegatedTask()`{.codeph} to get the task, and then, using
the threading model appropriate for its requirements, process the task.
The application might, for example, obtain threads from a thread pool to
process the tasks, while the main thread handles other I/O.

The following code executes each task in a newly created thread:

``` {.codeblock dir="ltr"}
if (res.getHandshakeStatus() == SSLEngineResult.HandshakeStatus.NEED_TASK) {
    Runnable task;
    while ((task = engine.getDelegatedTask()) != null) {
        new Thread(task).start();
    }
}
```

The `SSLEngine`{.codeph} will block future `wrap()`{.codeph} and
`unwrap()`{.codeph} calls until all of the outstanding tasks are
completed.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-2B54A68F-75AF-4FEA-9339-F7082FE5DA33}

#### Shutting Down a SSL/TLS/DTLS Connection {#JSSEC-GUID-2B54A68F-75AF-4FEA-9339-F7082FE5DA33 .sect4}

<div>
<div class="section">
For an orderly shutdown of an SSL/TLS/DTLS connection, the SSL/TLS/DTLS
protocols require transmission of close messages. Therefore, when an
application is done with the SSL/TLS/DTLS connection, it should first
obtain the close messages from the `SSLEngine`{.codeph}, then transmit
them to the peer using its transport mechanism, and finally shut down
the transport mechanism. [Example
8-10](java-secure-socket-extension-jsse-reference-guide.htm#GUID-2B54A68F-75AF-4FEA-9339-F7082FE5DA33__SHUTTINGDOWNANSSLTLSCONNECTION-B4C0BC69)
illustrates this.

In addition to an application explicitly closing the
`SSLEngine`{.codeph}, the `SSLEngine`{.codeph} might be closed by the
peer (via receipt of a close message while it is processing handshake
data), or by the `SSLEngine`{.codeph} encountering an error while
processing application or handshake data, indicated by throwing an
`SSLException`{.codeph}. In such cases, the application should invoke
`SSLEngine.wrap()`{.codeph} to get the close message and send it to the
peer until `SSLEngine.isOutboundDone()`{.codeph} returns `true`{.codeph}
(as shown in [Example
8-10](java-secure-socket-extension-jsse-reference-guide.htm#GUID-2B54A68F-75AF-4FEA-9339-F7082FE5DA33__SHUTTINGDOWNANSSLTLSCONNECTION-B4C0BC69)),
or until the `SSLEngineResult.getStatus()`{.codeph} returns
`CLOSED`{.codeph}.

In addition to orderly shutdowns, there can also be unexpected shutdowns
when the transport link is severed before close messages are exchanged.
In the previous examples, the application might get `-1`{.codeph} or
`IOException`{.codeph} when trying to read from the nonblocking
`SocketChannel`{.codeph}, or get `IOException`{.codeph} when trying to
write to the non-blocking `SocketChannel`{.codeph}. When you get to the
end of your input data, you should call
`engine.closeInbound()`{.codeph}, which will verify with the
`SSLEngine`{.codeph} that the remote peer has closed cleanly from the
SSL/TLS/DTLS perspective. Then the application should still try to shut
down cleanly by using the procedure in [Example
8-10](java-secure-socket-extension-jsse-reference-guide.htm#GUID-2B54A68F-75AF-4FEA-9339-F7082FE5DA33__SHUTTINGDOWNANSSLTLSCONNECTION-B4C0BC69).
Obviously, unlike `SSLSocket`{.codeph}, the application using
`SSLEngine`{.codeph} must deal with more state transitions, statuses,
and programming. See [Sample Code Illustrating the Use of an
SSLEngine](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGTHEUSEOFANSSL-7D23A601).

</div>
<!-- class="section" -->

<div class="example" id="GUID-2B54A68F-75AF-4FEA-9339-F7082FE5DA33__SHUTTINGDOWNANSSLTLSCONNECTION-B4C0BC69">
Example 8-10 Sample Code for Shutting Down a SSL/TLS/DTLS Connection

The following code sample illustrates how to shut down a SSL/TLS/DTLS
connection:

``` {.codeblock dir="ltr"}
// Indicate that application is done with engine
engine.closeOutbound();

while (!engine.isOutboundDone()) {
    // Get close message
    SSLEngineResult res = engine.wrap(empty, myNetData);

    // Check res statuses

    // Send close message to peer
    while(myNetData.hasRemaining()) {
        int num = socketChannel.write(myNetData);
        if (num == 0) {
            // no bytes written; try again later
        }
        myNetData().compact();
    }
}

// Close transport
socketChannel.close();
```

</div>
<!-- class="example" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-AB362290-033A-4D3B-AAF3-1BFEB1CD472B}

### SSLSession and ExtendedSSLSession {#JSSEC-GUID-AB362290-033A-4D3B-AAF3-1BFEB1CD472B .sect3}

<div>
The `javax.net.ssl.SSLSession`{.codeph} interface represents a security
context negotiated between the two peers of an `SSLSocket`{.codeph} or
`SSLEngine`{.codeph} connection. After a session has been arranged, it
can be shared by future `SSLSocket`{.codeph} or `SSLEngine`{.codeph}
objects connected between the same two peers.

<div class="section">
In some cases, parameters negotiated during the handshake are needed
later in the handshake to make decisions about trust. For example, the
list of valid signature algorithms might restrict the certificate types
that can be used for authentication. The `SSLSession`{.codeph} can be
retrieved <span class="italic">during</span> the handshake by calling
`getHandshakeSession()`{.codeph} on an `SSLSocket`{.codeph} or
`SSLEngine`{.codeph}. Implementations of `TrustManager`{.codeph} or
`KeyManager`{.codeph} can use the `getHandshakeSession()`{.codeph}
method to get information about session parameters to help them make
decisions.

A fully initialized `SSLSession`{.codeph} contains the cipher suite that
will be used for communications over a secure socket as well as a
nonauthoritative hint as to the network address of the remote peer, and
management information such as the time of creation and last use. A
session also contains a shared master secret negotiated between the
peers that is used to create cryptographic keys for encrypting and
guaranteeing the integrity of the communications over an
`SSLSocket`{.codeph} or `SSLEngine`{.codeph} connection. The value of
this master secret is known only to the underlying secure socket
implementation and is not exposed through the `SSLSession`{.codeph} API.

`ExtendedSSLSession`{.codeph} extends the `SSLSession`{.codeph}
interface to support additional session attributes. The
`ExtendedSSLSession`{.codeph} class adds methods that describe the
signature algorithms that are supported by the local implementation and
the peer. The `getRequestedServerNames()`{.codeph} method called on an
`ExtendedSSLSession`{.codeph} instance is used to obtain a list of
`SNIServerName`{.codeph} objects in the requested [Server Name
Indication (SNI)
Extension](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F).
The server should use the requested server names to guide its selection
of an appropriate authentication certificate, and/or other aspects of
the security policy. The client should use the requested server names to
guide its endpoint identification of the peer\'s identity, and/or other
aspects of the security policy.

Calls to the `getPacketBufferSize()`{.codeph} and
`getApplicationBufferSize()`{.codeph} methods on `SSLSession`{.codeph}
are used to determine the appropriate buffer sizes used by
`SSLEngine`{.codeph}.

<div class="p">
<div class="infoboxnote" id="GUID-AB362290-033A-4D3B-AAF3-1BFEB1CD472B__GUID-17258111-C234-4640-B886-D85221CCE842">
Note:

The SSL/TLS protocols specify that implementations are to produce
packets containing at most 16 kilobytes (KB) of plain text. However,
some implementations violate the specification and generate large
records up to 32 KB. If the `SSLEngine.unwrap()`{.codeph} code detects
large inbound packets, then the buffer sizes returned by
`SSLSession`{.codeph} will be updated dynamically. Applications should
always check the BUFFER\_OVERFLOW and BUFFER\_UNDERFLOW statuses and
enlarge the corresponding buffers if necessary. See [Understanding
SSLEngine Operation
Statuses](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744 "The status of the SSLEngine is represented by SSLEngineResult.Status.").
SunJSSE will always send standard compliant 16 KB records and allow
incoming 32 KB records. For a workaround, see the System property
`jsse.SSLEngine.acceptLargeFragments`{.codeph} in [Customizing
JSSE](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9 "JSSE includes a standard implementation that can be customized by plugging in different implementations or specifying the default keystore, and so on.").

</div>
</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-A14E129D-4D9D-4F38-A9F0-ED6F97B18863}

### HttpsURLConnection Class {#JSSEC-GUID-A14E129D-4D9D-4F38-A9F0-ED6F97B18863 .sect3}

<div>
The `javax.net.ssl.HttpsURLConnection`{.codeph} class extends the
`java.net.HttpURLConnection`{.codeph} class and adds support for
HTTPS-specific features.

<div class="section">
The HTTPS protocol is similar to HTTP, but HTTPS first establishes a
secure channel via SSL/TLS sockets and then verifies the identity of the
peer (see [Cipher Suite Choice and Remote Entity
Verification](java-secure-socket-extension-jsse-reference-guide.htm#GUID-D6A538A2-8CEF-4C6D-9C44-295758E64E38))
before requesting or receiving data. The
`javax.net.ssl.HttpsURLConnection`{.codeph} class extends the
`java.net.HttpURLConnection`{.codeph} class and adds support for
HTTPS-specific features. To know more about how HTTPS URLs are
constructed and used, see
the[<span class="apiname">java.net.URL</span>](https://docs.oracle.com/javase/10/docs/api/java/net/URL.html),
[<span class="apiname">java.net.URLConnection</span>](https://docs.oracle.com/javase/10/docs/api/java/net/URLConnection.html),
[<span class="apiname">java.net.HttpURLConnection</span>](https://docs.oracle.com/javase/10/docs/api/java/net/HttpURLConnection.html),
and
[<span class="apiname">javax.net.ssl.HttpsURLConnection</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/HttpsURLConnection.html)
classes.

Upon obtaining an `HttpsURLConnection`{.codeph} instance, you can
configure a number of HTTP and HTTPS parameters before actually
initiating the network connection via the
`URLConnection.connect()`{.codeph} method. Of particular interest are:

-   [Setting the Assigned
    SSLSocketFactory](java-secure-socket-extension-jsse-reference-guide.htm#GUID-8BE4AE6F-21EF-4DF0-91D4-B2D36EF625CA)
-   [Setting the Assigned
    HostnameVerifier](java-secure-socket-extension-jsse-reference-guide.htm#GUID-ABE2057C-0F36-48E1-8E76-4FC8D72A6573)

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-8BE4AE6F-21EF-4DF0-91D4-B2D36EF625CA}

#### Setting the Assigned SSLSocketFactory {#JSSEC-GUID-8BE4AE6F-21EF-4DF0-91D4-B2D36EF625CA .sect4}

<div>
<div class="section">
In some situations, it is desirable to specify the
`SSLSocketFactory`{.codeph} that an `HttpsURLConnection`{.codeph}
instance uses. For example, you might want to tunnel through a proxy
type that is not supported by the default implementation. The new
`SSLSocketFactory`{.codeph} could return sockets that have already
performed all necessary tunneling, thus allowing
`HttpsURLConnection`{.codeph} to use additional proxies.

The `HttpsURLConnection`{.codeph} class has a default
`SSLSocketFactory`{.codeph} that is assigned when the class is loaded
(this is the factory returned by the
`SSLSocketFactory.getDefault()`{.codeph} method). Future instances of
`HttpsURLConnection`{.codeph} will inherit the current default
`SSLSocketFactory`{.codeph} until a new default
`SSLSocketFactory`{.codeph} is assigned to the class via the static
`HttpsURLConnection.setDefaultSSLSocketFactory()`{.codeph} method. Once
an instance of `HttpsURLConnection`{.codeph} has been created, the
inherited `SSLSocketFactory`{.codeph} on this instance can be overridden
with a call to the `setSSLSocketFactory()`{.codeph} method.

<div class="p">
<div class="infoboxnote" id="GUID-8BE4AE6F-21EF-4DF0-91D4-B2D36EF625CA__GUID-2DF8B087-98E2-490B-89EC-BA0A4E86DC57">
Note:

Changing the default static `SSLSocketFactory`{.codeph} has no effect on
existing instances of `HttpsURLConnection`{.codeph}. A call to the
`setSSLSocketFactory()`{.codeph} method is necessary to change the
existing instances.

</div>
</div>
You can obtain the per-instance or per-class `SSLSocketFactory`{.codeph}
by making a call to the `getSSLSocketFactory()`{.codeph} or
`getDefaultSSLSocketFactory()`{.codeph} method, respectively.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-ABE2057C-0F36-48E1-8E76-4FC8D72A6573}

#### Setting the Assigned HostnameVerifier {#JSSEC-GUID-ABE2057C-0F36-48E1-8E76-4FC8D72A6573 .sect4}

<div>
If the host name of the URL does not match the host name in the
credentials received as part of the SSL/TLS handshake, then it is
possible that URL spoofing has occurred. If the implementation cannot
determine a host name match with reasonable certainty, then the SSL
implementation performs a callback to the instance\'s assigned
<span class="apiname">HostnameVerifier</span> for further checking. The
host name verifier can take whatever steps are necessary to make the
determination, such as performing host name pattern matching or perhaps
opening an interactive dialog box. An unsuccessful verification by the
host name verifier closes the connection. For more information regarding
host name verification, see [RFC
2818](http://www.ietf.org/rfc/rfc2818.txt?number=2818).

The <span class="apiname">setHostnameVerifier()</span> and
<span class="apiname">setDefaultHostnameVerifier()</span> methods
operate in a similar manner to the
<span class="apiname">setSSLSocketFactory()</span> and
<span class="apiname">setDefaultSSLSocketFactory()</span> methods, in
that <span class="apiname">HostnameVerifier</span> objects are assigned
on a per-instance and per-class basis, and the current values can be
obtained by a call to the
<span class="apiname">getHostnameVerifier()</span> or
<span class="apiname">getDefaultHostnameVerifier()</span> method.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-AD2529FD-8778-4A02-B544-5F58E083774B}

### Support Classes and Interfaces {#JSSEC-GUID-AD2529FD-8778-4A02-B544-5F58E083774B .sect3}

<div>
The classes and interfaces in this section are provided to support the
creation and initialization of `SSLContext`{.codeph} objects, which are
used to create `SSLSocketFactory`{.codeph},
`SSLServerSocketFactory`{.codeph}, and `SSLEngine`{.codeph} objects. The
support classes and interfaces are part of the `javax.net.ssl`{.codeph}
package.

Three of the classes described in this section ([The SSLContext
Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C281CAF3-275F-4DE4-8B47-4A84363CF39F "The javax.net.ssl.SSLContext class is an engine class for an implementation of a secure socket protocol. An instance of this class acts as a factory for SSLSocket, SSLServerSocket, and SSLEngine. An SSLContext object holds all of the state information shared across all objects created under that context. For example, session state is associated with the SSLContext when it is negotiated through the handshake protocol by sockets created by socket factories provided by the context. These cached sessions can be reused and shared by other sockets created under the same context."),
[The KeyManagerFactory
Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-616A7E77-587C-44E0-9F69-92BEDF631D5F "The javax.net.ssl.KeyManagerFactory class is an engine class for a provider-based service that acts as a factory for one or more types of KeyManager objects. The SunJSSE provider implements a factory that can return a basic X.509 key manager. Because it is provider-based, additional factories can be implemented and configured to provide additional or alternative key managers."),
and [The TrustManagerFactory
Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AB5DA59B-B070-4AC5-A9C1-C3C30BF9209F "The javax.net.ssl.TrustManagerFactory is an engine class for a provider-based service that acts as a factory for one or more types of TrustManager objects. Because it is provider-based, additional factories can be implemented and configured to provide additional or alternative trust managers that provide more sophisticated services or that implement installation-specific authentication policies."))
are <span class="italic"><span>engine classes</span></span>. An engine
class is an API class for specific algorithms (or protocols, in the case
of `SSLContext`{.codeph}), for which implementations may be provided in
one or more Cryptographic Service Provider (provider) packages. See [JCA
Design
Principles](java-cryptography-architecture-jca-reference-guide.htm#GUID-71693272-7F57-4155-99F9-A2139271FD6D)
and [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.htm#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.").

The SunJSSE provider that comes standard with JSSE provides
`SSLContext`{.codeph}, `KeyManagerFactory`{.codeph}, and
`TrustManagerFactory`{.codeph} implementations, as well as
implementations for engine classes in the standard
`java.security`{.codeph} API. [Table
8-6](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AD2529FD-8778-4A02-B544-5F58E083774B__GUID-8487642F-B1E3-4DB7-BA5E-ABF8971F8A58 "The following table lists implementations supplied by SunJSSE.")
lists implementations supplied by SunJSSE.

<div class="tblformal" id="GUID-AD2529FD-8778-4A02-B544-5F58E083774B__GUID-8487642F-B1E3-4DB7-BA5E-ABF8971F8A58">
Table 8-6 Implementations Supplied by SunJSSE

  Engine Class Implemented         Algorithm or Protocol
  -------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `KeyStore`{.codeph}              PKCS12
  `KeyManagerFactory`{.codeph}     PKIX, SunX509
  `TrustManagerFactory`{.codeph}   PKIX (X509 or SunPKIX), SunX509
  `SSLContext`{.codeph}            SSLv3[\[1\]](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AD2529FD-8778-4A02-B544-5F58E083774B__FOOTNOTE1SSLV3ISENABLEDSTARTINGWITH-8E8BD3EF), TLSv1, TLSv1.1, TLSv1.2, DTLSv1.0, DTLSv1.2

</div>
<!-- class="inftblhruleinformal" -->

Footnote 1: Starting with JDK 8u31, the SSLv3 protocol (Secure Socket
Layer) has been deactivated and is not available by default. See the
`java.security.Security`{.codeph} property
`jdk.tls.disabledAlgorithms`{.codeph} in the
`<java_home>/conf/security/java.security`{.codeph} file. If SSLv3 is
absolutely required, the protocol can be reactivated by removing
`SSLv3`{.codeph} from the `jdk.tls.disabledAlgorithms`{.codeph} property
in the `java.security` file or by dynamically setting this Security
Property before JSSE is initialized. To enable SSLv3 protocol at deploy
level, after following the previous steps, add the line
`deployment.security.SSLv3=true`{.codeph} to the `deployment.properties`
file.

</div>
<div class="sect4">
[]{#GUID-C281CAF3-275F-4DE4-8B47-4A84363CF39F}

#### The SSLContext Class {#JSSEC-GUID-C281CAF3-275F-4DE4-8B47-4A84363CF39F .sect4}

<div>
The `javax.net.ssl.SSLContext`{.codeph} class is an engine class for an
implementation of a secure socket protocol. An instance of this class
acts as a factory for `SSLSocket`{.codeph}, `SSLServerSocket`{.codeph},
and `SSLEngine`{.codeph}. An `SSLContext`{.codeph} object holds all of
the state information shared across all objects created under that
context. For example, session state is associated with the
`SSLContext`{.codeph} when it is negotiated through the handshake
protocol by sockets created by socket factories provided by the context.
These cached sessions can be reused and shared by other sockets created
under the same context.

Each instance is configured through its `init`{.codeph} method with the
keys, certificate chains, and trusted root CA certificates that it needs
to perform authentication. This configuration is provided in the form of
key and trust managers. These managers provide support for the
authentication and key agreement aspects of the cipher suites supported
by the context.

Currently, only X.509-based managers are supported.

</div>
<div class="sect5">
[]{#GUID-1F3F9B1E-143A-4C05-922E-152EA1DFAE90}

##### Obtaining and Initializing the SSLContext Class {#JSSEC-GUID-1F3F9B1E-143A-4C05-922E-152EA1DFAE90 .sect5}

<div>
The `SSLContext`{.codeph} class is used to create the
`SSLSocketFactory`{.codeph} or `SSLServerSocketFactory`{.codeph} class.

There are two ways to obtain and initialize an `SSLContext`{.codeph}:

-   The simplest way is to call the static
    [`SSLContext.getDefault`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLContext.html#getDefault)
    method on either the `SSLSocketFactory`{.codeph} or
    `SSLServerSocketFactory`{.codeph} class. This method creates a
    default `SSLContext`{.codeph} with a default `KeyManager`{.codeph},
    `TrustManager`{.codeph}, and `SecureRandom`{.codeph} (a secure
    random number generator). A default `KeyManagerFactory`{.codeph} and
    `TrustManagerFactory`{.codeph} are used to create the
    `KeyManager`{.codeph} and `TrustManager`{.codeph}, respectively. The
    key material used is found in the default keystore and truststore,
    as determined by system properties described in [Customizing the
    Default Keystores and Truststores, Store Types, and Store
    Passwords](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150).
-   The approach that gives the caller the most control over the
    behavior of the created context is to call the static method
    [`SSLContext.getDefault`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLContext.html#getDefault)
    on the `SSLContext`{.codeph} class, and then initialize the context
    by calling the instance\'s proper `init()`{.codeph} method. One
    variant of the `init()`{.codeph} method takes three arguments: an
    array of `KeyManager`{.codeph} objects, an array of
    `TrustManager`{.codeph} objects, and a `SecureRandom`{.codeph}
    object. The `KeyManager`{.codeph} and `TrustManager`{.codeph}
    objects are created by either implementing the appropriate
    interfaces or using the `KeyManagerFactory`{.codeph} and
    `TrustManagerFactory`{.codeph} classes to generate implementations.
    The `KeyManagerFactory`{.codeph} and `TrustManagerFactory`{.codeph}
    can then each be initialized with key material contained in the
    `KeyStore`{.codeph} passed as an argument to the `init()`{.codeph}
    method of the `TrustManagerFactory`{.codeph} or
    `KeyManagerFactory`{.codeph} classes. Finally, the
    `getTrustManagers()`{.codeph} method (in
    `TrustManagerFactory`{.codeph}) and `getKeyManagers()`{.codeph}
    method (in `KeyManagerFactory`{.codeph}) can be called to obtain the
    array of trust managers or key managers, one for each type of trust
    or key material.

Once an SSL connection is established, an `SSLSession`{.codeph} is
created which contains various information, such as identities
established and cipher suite used. The `SSLSession`{.codeph} is then
used to describe an ongoing relationship and state information between
two entities. Each SSL connection involves one session at a time, but
that session may be used on many connections between those entities,
simultaneously or sequentially.

</div>
</div>
<div class="sect5">
[]{#GUID-9BAC1902-A203-4422-8163-61D64ADD2FF7}

##### Creating an SSLContext Object {#JSSEC-GUID-9BAC1902-A203-4422-8163-61D64ADD2FF7 .sect5}

<div>
Like other JCA provider-based engine classes, `SSLContext`{.codeph}
objects are created using the `getInstance()`{.codeph} factory methods
of the `SSLContext`{.codeph} class. These static methods each return an
instance that implements <span class="italic">at least</span> the
requested secure socket protocol. The returned instance may implement
other protocols, too. For example, `getInstance("TLSv1")`{.codeph} may
return an instance that implements TLSv1, TLSv1.1, and TLSv1.2. The
`getSupportedProtocols()`{.codeph} method returns a list of supported
protocols when an `SSLSocket`{.codeph}, `SSLServerSocket`{.codeph}, or
`SSLEngine`{.codeph} is created from this context. You can control which
protocols are actually enabled for an SSL connection by using the
`setEnabledProtocols(String[] protocols)`{.codeph} method.

<div class="section">
<div class="infoboxnote" id="GUID-9BAC1902-A203-4422-8163-61D64ADD2FF7__GUID-AEF580E3-5151-4C8F-A5DE-A21E08BC18A2">
Note:

An `SSLContext`{.codeph} object is automatically created, initialized,
and statically assigned to the `SSLSocketFactory`{.codeph} class when
you call the `SSLSocketFactory.getDefault()`{.codeph} method. Therefore,
you do not have to directly create and initialize an
<span class="apiname">SSLContext</span> object (unless you want to
override the default behavior).

</div>
To create an `SSLContext`{.codeph} object by calling the
`getInstance()`{.codeph} factory method, you must specify the protocol
name. You may also specify which provider you want to supply the
implementation of the requested protocol:

-   `public static SSLContext getInstance(String protocol);`{.codeph}
-   `public static SSLContext getInstance(String protocol, String provider);`{.codeph}
-   `public static SSLContext getInstance(String protocol, Provider provider);`{.codeph}

If just a protocol name is specified, then the system will determine
whether an implementation of the requested protocol is available in the
environment. If there is more than one implementation, then it will
determine whether there is a preferred one.

If both a protocol name and a provider are specified, then the system
will determine whether an implementation of the requested protocol is in
the provider requested. If there is no implementation, an exception will
be thrown.

A protocol is a string (such as `"TLS"`{.codeph}) that describes the
secure socket protocol desired. Common protocol names for
`SSLContext`{.codeph} objects are defined in [Java Security Standard
Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).

An `SSLContext`{.codeph} can be obtained as follows:

``` {.codeblock dir="ltr"}
SSLContext sc = SSLContext.getInstance("TLS");
```

A newly created `SSLContext`{.codeph} should be initialized by calling
the `init`{.codeph} method:

``` {.codeblock dir="ltr"}
public void init(KeyManager[] km, TrustManager[] tm, SecureRandom random);
```

If the `KeyManager[]`{.codeph} parameter is null, then an empty
`KeyManager`{.codeph} will be defined for this context. If the
`TrustManager[]`{.codeph} parameter is null, then the installed security
providers will be searched for the highest-priority implementation of
the <span class="apiname">TrustManagerFactory</span> class (see [The
TrustManagerFactory
Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AB5DA59B-B070-4AC5-A9C1-C3C30BF9209F "The javax.net.ssl.TrustManagerFactory is an engine class for a provider-based service that acts as a factory for one or more types of TrustManager objects. Because it is provider-based, additional factories can be implemented and configured to provide additional or alternative trust managers that provide more sophisticated services or that implement installation-specific authentication policies.")),
from which an appropriate `TrustManager`{.codeph} will be obtained.
Likewise, the `SecureRandom`{.codeph} parameter may be null, in which
case a default implementation will be used.

If the internal default context is used, (for example, an
`SSLContext`{.codeph} is created by
`SSLSocketFactory.getDefault()`{.codeph} or
`SSLServerSocketFactory.getDefault()`{.codeph}), then a [default
KeyManager and
TrustManager](java-secure-socket-extension-jsse-reference-guide.htm#GUID-0ACD9274-607C-49BE-AED9-BEE2B4F2BEF2)
are created. The default `SecureRandom`{.codeph} implementation is also
chosen.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-42CA1099-42AD-4772-BC4A-29C2A78E3EC9}

#### The TrustManager Interface {#JSSEC-GUID-42CA1099-42AD-4772-BC4A-29C2A78E3EC9 .sect4}

<div>
The primary responsibility of the `TrustManager`{.codeph} is to
determine whether the presented authentication credentials should be
trusted. If the credentials are not trusted, then the connection will be
terminated. To authenticate the remote identity of a secure socket peer,
you must initialize an `SSLContext`{.codeph} object with one or more
`TrustManager`{.codeph} objects. You must pass one
`TrustManager`{.codeph} for each authentication mechanism that is
supported. If null is passed into the `SSLContext`{.codeph}
initialization, then a trust manager will be created for you. Typically,
a single trust manager supports authentication based on X.509 public key
certificates (for example, `X509TrustManager`{.codeph}). Some secure
socket implementations may also support authentication based on shared
secret keys, Kerberos, or other mechanisms.

`TrustManager`{.codeph} objects are created either by a
`TrustManagerFactory`{.codeph}, or by providing a concrete
implementation of the interface.

</div>
</div>
<div class="sect4">
[]{#GUID-AB5DA59B-B070-4AC5-A9C1-C3C30BF9209F}

#### The TrustManagerFactory Class {#JSSEC-GUID-AB5DA59B-B070-4AC5-A9C1-C3C30BF9209F .sect4}

<div>
The `javax.net.ssl.TrustManagerFactory`{.codeph} is an engine class for
a provider-based service that acts as a factory for one or more types of
`TrustManager`{.codeph} objects. Because it is provider-based,
additional factories can be implemented and configured to provide
additional or alternative trust managers that provide more sophisticated
services or that implement installation-specific authentication
policies.

</div>
<div class="sect5">
[]{#GUID-CF1771C6-D881-48E3-BB0D-49DC3E7C893B}

##### Creating a TrustManagerFactory {#JSSEC-GUID-CF1771C6-D881-48E3-BB0D-49DC3E7C893B .sect5}

<div>
You create an instance of this class in a similar manner to
`SSLContext`{.codeph}, except for passing an algorithm name string
instead of a protocol name to the `getInstance()`{.codeph} method:

<div class="section">
``` {.codeblock dir="ltr"}
TrustManagerFactory tmf = TrustManagerFactory.getInstance(String algorithm);
TrustManagerFactory tmf = TrustManagerFactory.getInstance(String algorithm, String provider);
TrustManagerFactory tmf = TrustManagerFactory.getInstance(String algorithm, Provider provider);
```

A sample call is as follows:

``` {.codeblock dir="ltr"}
TrustManagerFactory tmf = TrustManagerFactory.getInstance("PKIX", "SunJSSE");
```

The preceding call creates an instance of the SunJSSE provider\'s PKIX
trust manager factory. This factory can be used to create trust managers
that provide X.509 PKIX-based certification path validity checking.

When initializing an `SSLContext`{.codeph}, you can use trust managers
created from a trust manager factory, or you can write your own trust
manager, for example, using the
[`CertPath`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/cert/CertPath.html)
API. See [Java PKI Programmer's
Guide](java-pki-programmers-guide.htm#GUID-E47B8A0E-6B3A-4B49-994D-CF185BF441EC "The CertPath class is an abstract class for certification paths. It defines the functionality shared by all certification path objects. Various certification path types can be implemented by subclassing the CertPath class, even though they may have different contents and ordering schemes.").
You do not need to use a trust manager factory if you implement a trust
manager using the
[`X509TrustManager`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/X509TrustManager.html)
interface.

A newly created factory should be initialized by calling one of the
`init()`{.codeph} methods:

``` {.codeblock dir="ltr"}
public void init(KeyStore ks);
public void init(ManagerFactoryParameters spec);
```

Call whichever `init()`{.codeph} method is appropriate for the
`TrustManagerFactory`{.codeph} you are using. If you are not sure, then
ask the provider vendor.

For many factories, such as the SunX509 `TrustManagerFactory`{.codeph}
from the SunJSSE provider, the `KeyStore`{.codeph} is the only
information required to initialize the `TrustManagerFactory`{.codeph}
and thus the first `init`{.codeph} method is the appropriate one to
call. The `TrustManagerFactory`{.codeph} will query the
`KeyStore`{.codeph} for information about which remote certificates
should be trusted during authorization checks.

Sometimes, initialization parameters other than a `KeyStore`{.codeph}
are needed by a provider. Users of that provider are expected to pass an
implementation of the appropriate `ManagerFactoryParameters`{.codeph} as
defined by the provider. The provider can then call the specified
methods in the `ManagerFactoryParameters`{.codeph} implementation to
obtain the needed information.

For example, suppose the `TrustManagerFactory`{.codeph} provider
requires initialization parameters B, R, and S from any application that
wants to use that provider. Like all providers that require
initialization parameters other than a `KeyStore`{.codeph}, the provider
requires the application to provide an instance of a class that
implements a particular `ManagerFactoryParameters`{.codeph}
subinterface. In the example, suppose that the provider requires the
calling application to implement and create an instance of
`MyTrustManagerFactoryParams`{.codeph} and pass it to the second
`init()`{.codeph} method. The following example illustrates what
`MyTrustManagerFactoryParams`{.codeph} can look like:

``` {.codeblock dir="ltr"}
public interface MyTrustManagerFactoryParams extends ManagerFactoryParameters {
  public boolean getBValue();
  public float getRValue();
  public String getSValue();
}
```

Some trust managers can make trust decisions without being explicitly
initialized with a `KeyStore`{.codeph} object or any other parameters.
For example, they may access trust material from a local directory
service via LDAP, use a remote online certificate status checking
server, or access default trust material from a standard local location.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect5">
[]{#GUID-ED23411A-B4AA-4E46-A5E9-619A0CF30151}

##### PKIX TrustManager Support {#JSSEC-GUID-ED23411A-B4AA-4E46-A5E9-619A0CF30151 .sect5}

<div>
The default trust manager algorithm is PKIX. It can be changed by
editing the `ssl.TrustManagerFactory.algorithm`{.codeph} property in the
`java.security`{.codeph} file.

The PKIX trust manager factory uses the CertPath PKIX implementation
(see [PKI Programmers Guide
Overview](java-pki-programmers-guide.htm#GUID-D6A18B1E-A2A8-4CA2-BD18-514CD807810E "The Java Certification Path API defines interfaces and abstract classes for creating, building, and validating certification paths.  Implementations may be plugged in using a provider-based interface."))
from an installed security provider. The trust manager factory can be
initialized using the normal `init(KeyStores)`{.codeph} method, or by
passing <span class="apiname">CertPath</span> parameters to the PKIX
trust manager using the
[<span class="apiname">CertPathTrustManagerParameters</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/CertPathTrustManagerParameters.html)
class.

[Example
8-11](java-secure-socket-extension-jsse-reference-guide.htm#GUID-ED23411A-B4AA-4E46-A5E9-619A0CF30151__EXAMPLE-1326-635DA89D)
illustrates how to get the trust manager to use a particular LDAP
certificate store and enable revocation checking.

If the `TrustManagerFactory.init(KeyStore)`{.codeph} method is used,
then default PKIX parameters are used with the exception that revocation
checking is disabled. It can be enabled by setting the
`com.sun.net.ssl.checkRevocation`{.codeph} system property to
`true`{.codeph}. This setting requires that the CertPath implementation
can locate revocation information by itself. The PKIX implementation in
the provider can do this in many cases but requires that the system
property `com.sun.security.enableCRLDP`{.codeph} be set to
`true`{.codeph}. Note that the
<span class="apiname">TrustManagerFactory.init(ManagerFactoryParameters)</span>
method has revocation checking enabled by default.

See [PKIX
Classes](java-pki-programmers-guide.htm#GUID-5BBEF087-CA8A-4287-97FB-BD88DCD12FE5 "The Java Certification Path API includes a set of algorithm-specific classes modeled for use with the PKIX certification path validation algorithm.")
and [The CertPath
Class](java-pki-programmers-guide.htm#GUID-E47B8A0E-6B3A-4B49-994D-CF185BF441EC "The CertPath class is an abstract class for certification paths. It defines the functionality shared by all certification path objects. Various certification path types can be implemented by subclassing the CertPath class, even though they may have different contents and ordering schemes.").

<div class="example" id="GUID-ED23411A-B4AA-4E46-A5E9-619A0CF30151__EXAMPLE-1326-635DA89D">
Example 8-11 Sample Code for Using a LDAP Certificate to Enable
Revocation Checking

The following example illustrates how to get the trust manager to use a
particular LDAP certificate store and enable revocation checking:

``` {.codeblock dir="ltr"}
    import javax.net.ssl.*;
    import java.security.cert.*;
    import java.security.KeyStore;
    import java.io.FileInputStream;
    ...
    
    // Obtain Keystore password
    char[] pass = System.console().readPassword("Password: ");

    // Create PKIX parameters
    KeyStore anchors = KeyStore.getInstance("JKS");
    anchors.load(new FileInputStream(anchorsFile, pass));
    PKIXBuilderParameters pkixParams = new PKIXBuilderParameters(anchors, new X509CertSelector());
    
    // Specify LDAP certificate store to use
    LDAPCertStoreParameters lcsp = new LDAPCertStoreParameters("ldap.imc.org", 389);
    pkixParams.addCertStore(CertStore.getInstance("LDAP", lcsp));
    
    // Specify that revocation checking is to be enabled
    pkixParams.setRevocationEnabled(true);
    
    // Wrap PKIX parameters as trust manager parameters
    ManagerFactoryParameters trustParams = new CertPathTrustManagerParameters(pkixParams);
    
    // Create TrustManagerFactory for PKIX-compliant trust managers
    TrustManagerFactory factory = TrustManagerFactory.getInstance("PKIX");
    
    // Pass parameters to factory to be passed to CertPath implementation
    factory.init(trustParams);
    
    // Use factory
    SSLContext ctx = SSLContext.getInstance("TLS");
    ctx.init(null, factory.getTrustManagers(), null);
```

</div>
<!-- class="example" -->

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-7932AB21-2FED-402E-A806-3088402BAEA6}

#### The X509TrustManager Interface {#JSSEC-GUID-7932AB21-2FED-402E-A806-3088402BAEA6 .sect4}

<div>
The `javax.net.ssl.X509TrustManager`{.codeph} interface extends the
general `TrustManager`{.codeph} interface. It must be implemented by a
trust manager when using X.509-based authentication.

To support X.509 authentication of remote socket peers through JSSE, an
instance of this interface must be passed to the `init`{.codeph} method
of an `SSLContext`{.codeph} object.

</div>
<div class="sect5">
[]{#GUID-32CF3420-56E8-4BC5-8D3B-1F6B4692A290}

##### Creating an X509TrustManager {#JSSEC-GUID-32CF3420-56E8-4BC5-8D3B-1F6B4692A290 .sect5}

<div>
You can either implement this interface directly yourself or obtain one
from a provider-based `TrustManagerFactory`{.codeph} (such as that
supplied by the SunJSSE provider). You could also implement your own
interface that delegates to a factory-generated trust manager. For
example, you might do this to filter the resulting trust decisions and
query an end-user through a graphical user interface.

<div class="section">
If a null KeyStore parameter is passed to the SunJSSE PKIX or SunX509
`TrustManagerFactory`{.codeph}, then the factory uses the following
process to try to find trust material:

1.  If the `javax.net.ssl.trustStore`{.codeph} property is defined, then
    the `TrustManagerFactory`{.codeph} attempts to find a file using the
    file name specified by that system property, and uses that file for
    the KeyStore parameter. If the
    `javax.net.ssl.trustStorePassword`{.codeph} system property is also
    defined, then its value is used to check the integrity of the data
    in the truststore before opening it.

    If the `javax.net.ssl.trustStore`{.codeph} property is defined but
    the specified file does not exist, then a default
    `TrustManager`{.codeph} using an empty keystore is created.

2.  If the `javax.net.ssl.trustStore`{.codeph} system property was not
    specified, then:
    -   if the file
        <span class="variable">java-home</span>`/lib/security/jssecacerts`{.codeph}
        exists, that file is used;
    -   if the file
        <span class="variable">java-home</span>`/lib/security/cacerts`{.codeph}
        exists, that file is used;
    -   if neither of these files exists, then the SSL cipher suite is
        anonymous, does not perform any authentication, and thus does
        not need a truststore.

To know more about what <span class="variable">java-home</span> refers
to, see [Terms and
Definitions](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329 "The following are commonly used cryptography terms and their definitions.").

The factory looks for a file specified via the
`javax.net.ssl.trustStore`{.codeph} Security Property or for the
`jssecacerts` file before checking for a `cacerts`{.codeph} file.
Therefore, you can provide a JSSE-specific set of trusted root
certificates separate from ones that might be present in `cacerts` for
code-signing purposes.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect5">
[]{#GUID-E1205974-3249-4E40-83C0-5F89C7375CF4}

##### Creating Your Own X509TrustManager {#JSSEC-GUID-E1205974-3249-4E40-83C0-5F89C7375CF4 .sect5}

<div>
If the supplied `X509TrustManager`{.codeph} behavior is not suitable for
your situation, then you can create your own `X509TrustManager`{.codeph}
by either creating and registering your own
`TrustManagerFactory`{.codeph} or by implementing the
`X509TrustManager`{.codeph} interface directly.

<div class="section">
[Example
8-12](java-secure-socket-extension-jsse-reference-guide.htm#GUID-E1205974-3249-4E40-83C0-5F89C7375CF4__EXAMPLE-1327-635DA68E)
illustrates a `MyX509TrustManager`{.codeph} class that enhances the
default SunJSSE `X509TrustManager`{.codeph} behavior by providing
alternative authentication logic when the default
`X509TrustManager`{.codeph} fails.

Once you have created such a trust manager, assign it to an
`SSLContext`{.codeph} via the `init()`{.codeph} method, as in the
following example. Future `SocketFactories`{.codeph} created from this
`SSLContext`{.codeph} will use your new `TrustManager`{.codeph} when
making trust decisions.

``` {.codeblock dir="ltr"}
TrustManager[] myTMs = new TrustManager[] { new MyX509TrustManager() };
SSLContext ctx = SSLContext.getInstance("TLS");
ctx.init(null, myTMs, null);
```

</div>
<!-- class="section" -->

<div class="example" id="GUID-E1205974-3249-4E40-83C0-5F89C7375CF4__EXAMPLE-1327-635DA68E">
Example 8-12 Sample Code for Creating a X509TrustManager

The following code sample illustrates `MyX509TrustManager`{.codeph}
class that enhances the default SunJSSE `X509TrustManager`{.codeph}
behavior by providing alternative authentication logic when the default
`X509TrustManager`{.codeph} fails:

``` {.codeblock dir="ltr"}
class MyX509TrustManager implements X509TrustManager {

     /*
      * The default PKIX X509TrustManager9.  Decisions are delegated
      * to it, and a fall back to the logic in this class is performed
      * if the default X509TrustManager does not trust it.
      */
     X509TrustManager pkixTrustManager;

     MyX509TrustManager() throws Exception {
         // create a "default" JSSE X509TrustManager.

         KeyStore ks = KeyStore.getInstance("JKS");
         ks.load(new FileInputStream("trustedCerts"), "passphrase".toCharArray());

         TrustManagerFactory tmf = TrustManagerFactory.getInstance("PKIX");
         tmf.init(ks);

         TrustManager tms [] = tmf.getTrustManagers();

         /*
          * Iterate over the returned trust managers, looking
          * for an instance of X509TrustManager.  If found,
          * use that as the default trust manager.
          */
         for (int i = 0; i < tms.length; i++) {
             if (tms[i] instanceof X509TrustManager) {
                 pkixTrustManager = (X509TrustManager) tms[i];
                 return;
             }
         }

         /*
          * Find some other way to initialize, or else the
          * constructor fails.
          */
         throw new Exception("Couldn't initialize");
     }

     /*
      * Delegate to the default trust manager.
      */
     public void checkClientTrusted(X509Certificate[] chain, String authType)
                 throws CertificateException {
         try {
             pkixTrustManager.checkClientTrusted(chain, authType);
         } catch (CertificateException excep) {
             // do any special handling here, or rethrow exception.
         }
     }

     /*
      * Delegate to the default trust manager.
      */
     public void checkServerTrusted(X509Certificate[] chain, String authType)
                 throws CertificateException {
         try {
             pkixTrustManager.checkServerTrusted(chain, authType);
         } catch (CertificateException excep) {
             /*
              * Possibly pop up a dialog box asking whether to trust the
              * cert chain.
              */
         }
     }

     /*
      * Merely pass this through.
      */
     public X509Certificate[] getAcceptedIssuers() {
         return pkixTrustManager.getAcceptedIssuers();
     }
}
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect5">
[]{#GUID-43F18232-8DDE-4F0C-B2AB-0EE4B472B15F}

##### Updating the Keystore Dynamically {#JSSEC-GUID-43F18232-8DDE-4F0C-B2AB-0EE4B472B15F .sect5}

<div>
You can enhance `MyX509TrustManager`{.codeph} to handle dynamic keystore
updates. When a `checkClientTrusted`{.codeph} or
`checkServerTrusted`{.codeph} test fails and does not establish a
trusted certificate chain, you can add the required trusted certificate
to the keystore. You must create a new `pkixTrustManager`{.codeph} from
the `TrustManagerFactory`{.codeph} initialized with the updated
keystore. When you establish a new connection (using the previously
initialized `SSLContext`{.codeph}), the newly added certificate will be
used when making trust decisions.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-BAAC4A6F-2705-4A16-874A-1CDF0E48B8E3}

#### X509ExtendedTrustManager Class {#JSSEC-GUID-BAAC4A6F-2705-4A16-874A-1CDF0E48B8E3 .sect4}

<div>
The `X509ExtendedTrustManager`{.codeph} class is an abstract
implementation of the `X509TrustManager`{.codeph} interface. It adds
methods for connection-sensitive trust management. In addition, it
enables endpoint verification at the TLS layer.

In TLS 1.2 and later, both client and server can specify which hash and
signature algorithms they will accept. To authenticate the remote side,
authentication decisions must be based on both X509 certificates and the
local accepted hash and signature algorithms. The local accepted hash
and signature algorithms can be obtained using the
`ExtendedSSLSession.getLocalSupportedSignatureAlgorithms()`{.codeph}
method.

The `ExtendedSSLSession`{.codeph} object can be retrieved by calling the
`SSLSocket.getHandshakeSession()`{.codeph} method or the
`SSLEngine.getHandshakeSession()`{.codeph} method.

The `X509TrustManager`{.codeph} interface is not connection-sensitive.
It provides no way to access `SSLSocket`{.codeph} or
`SSLEngine`{.codeph} session properties.

Besides TLS 1.2 support, the `X509ExtendedTrustManager`{.codeph} class
also supports algorithm constraints and SSL layer host name
verification. For JSSE providers and trust manager implementations, the
`X509ExtendedTrustManager`{.codeph} class is highly recommended over the
legacy `X509TrustManager`{.codeph} interface.

</div>
<div class="sect5">
[]{#GUID-A6B7B05A-3696-4F86-A05C-9500EEC91C2D}

##### Creating an X509ExtendedTrustManager {#JSSEC-GUID-A6B7B05A-3696-4F86-A05C-9500EEC91C2D .sect5}

<div>
You can either create an `X509ExtendedTrustManager`{.codeph} subclass
yourself (which is outlined in the following section) or obtain one from
a provider-based `TrustManagerFactory`{.codeph} (such as that supplied
by the SunJSSE provider). In Java SE 7, the PKIX or SunX509
`TrustManagerFactory`{.codeph} returns an
`X509ExtendedTrustManager`{.codeph} instance.

</div>
</div>
<div class="sect5">
[]{#GUID-AC443CF8-4CBD-4B77-8733-46D8DA2E3248}

##### Creating Your Own X509ExtendedTrustManager {#JSSEC-GUID-AC443CF8-4CBD-4B77-8733-46D8DA2E3248 .sect5}

<div>
This section outlines how to create a subclass of
`X509ExtendedTrustManager`{.codeph} in nearly the same way as described
for `X509TrustManager`{.codeph}.

<div class="section">
[Example
8-13](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AC443CF8-4CBD-4B77-8733-46D8DA2E3248__IMPORTJAVA.IO.IMPORTJAVA.NET.IMPORT-635DA3F9)
illustrates how to create a class that uses the PKIX
`TrustManagerFactory`{.codeph} to locate a default
`X509ExtendedTrustManager`{.codeph} that will be used to make decisions
about trust.

</div>
<!-- class="section" -->

<div class="example" id="GUID-AC443CF8-4CBD-4B77-8733-46D8DA2E3248__IMPORTJAVA.IO.IMPORTJAVA.NET.IMPORT-635DA3F9">
Example 8-13 Sample Code for Creating a PKIX TrustManagerFactory

The following code sample illustrates how to create a class that uses
the PKIX `TrustManagerFactory`{.codeph} to locate a default
`X509ExtendedTrustManager`{.codeph} that will be used to make decisions
about trust. If the default trust manager fails for any reason, then the
subclass can add other behavior. In the sample, these locations are
indicated by comments in the `catch`{.codeph} clauses.

``` {.codeblock dir="ltr"}
import java.io.*;
import java.net.*;
import java.security.*;
import java.security.cert.*;
import javax.net.ssl.*;
    
public class MyX509ExtendedTrustManager extends X509ExtendedTrustManager {

  /*
   * The default PKIX X509ExtendedTrustManager.  Decisions are
   * delegated to it, and a fall back to the logic in this class is
   * performed if the default X509ExtendedTrustManager does not
   * trust it.
   */
  
  X509ExtendedTrustManager pkixTrustManager;
    
  MyX509ExtendedTrustManager() throws Exception {
    // create a "default" JSSE X509ExtendedTrustManager.
    
    KeyStore ks = KeyStore.getInstance("JKS");
    ks.load(new FileInputStream("trustedCerts"), "passphrase".toCharArray());
    
    TrustManagerFactory tmf = TrustManagerFactory.getInstance("PKIX");
    tmf.init(ks);
    
    TrustManager tms [] = tmf.getTrustManagers();
    
    /*
     * Iterate over the returned trust managers, looking
     * for an instance of X509ExtendedTrustManager. If found,
     * use that as the default trust manager.
     */
    for (int i = 0; i < tms.length; i++) {
      if (tms[i] instanceof X509ExtendedTrustManager) {
        pkixTrustManager = (X509ExtendedTrustManager) tms[i];
        return;
      }
    }
    
    /*
     * Find some other way to initialize, or else we have to fail the
     * constructor.
     */
    throw new Exception("Couldn't initialize");
  }
    
  /*
   * Delegate to the default trust manager.
   */
  public void checkClientTrusted(X509Certificate[] chain, String authType)
    throws CertificateException {
    try {
      pkixTrustManager.checkClientTrusted(chain, authType);
    } catch (CertificateException excep) {
      // do any special handling here, or rethrow exception.
    }
  }
    
  /*
   * Delegate to the default trust manager.
   */
  public void checkServerTrusted(X509Certificate[] chain, String authType)
    throws CertificateException {
    try {
      pkixTrustManager.checkServerTrusted(chain, authType);
    } catch (CertificateException excep) {
      /*
       * Possibly pop up a dialog box asking whether to trust the
       * cert chain.
       */
    }
  }
    
  /*
   * Connection-sensitive verification.
   */
  public void checkClientTrusted(X509Certificate[] chain, String authType, Socket socket)
    throws CertificateException {
    try {
      pkixTrustManager.checkClientTrusted(chain, authType, socket);
    } catch (CertificateException excep) {
      // do any special handling here, or rethrow exception.
    }
  }
    
  public void checkClientTrusted(X509Certificate[] chain, String authType, SSLEngine engine)
    throws CertificateException {
    try {
      pkixTrustManager.checkClientTrusted(chain, authType, engine);
    } catch (CertificateException excep) {
      // do any special handling here, or rethrow exception.
    }
  }
    
  public void checkServerTrusted(X509Certificate[] chain, String authType, Socket socket)
    throws CertificateException {
    try {
      pkixTrustManager.checkServerTrusted(chain, authType, socket);
    } catch (CertificateException excep) {
      // do any special handling here, or rethrow exception.
    }
  }
    
  public void checkServerTrusted(X509Certificate[] chain, String authType, SSLEngine engine)
    throws CertificateException {
    try {
      pkixTrustManager.checkServerTrusted(chain, authType, engine);
    } catch (CertificateException excep) {
      // do any special handling here, or rethrow exception.
    }
  }
         
  /*
   * Merely pass this through.
   */
  public X509Certificate[] getAcceptedIssuers() {
    return pkixTrustManager.getAcceptedIssuers();
  }
}
```

</div>
<!-- class="example" -->

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-997AB098-DDD7-40E2-9FD0-5AA3C83E1702}

#### The KeyManager Interface {#JSSEC-GUID-997AB098-DDD7-40E2-9FD0-5AA3C83E1702 .sect4}

<div>
The primary responsibility of the `KeyManager`{.codeph} is to select the
authentication credentials that will eventually be sent to the remote
host. To authenticate yourself (a local secure socket peer) to a remote
peer, you must initialize an `SSLContext`{.codeph} object with one or
more `KeyManager`{.codeph} objects. You must pass one
`KeyManager`{.codeph} for each different authentication mechanism that
will be supported. If null is passed into the `SSLContext`{.codeph}
initialization, then an empty `KeyManager`{.codeph} will be created. If
the internal default context is used (for example, an
`SSLContext`{.codeph} created by
`SSLSocketFactory.getDefault()`{.codeph} or
`SSLServerSocketFactory.getDefault()`{.codeph}), then a default
`KeyManager`{.codeph} is created. See [Customizing the Default Keystores
and Truststores, Store Types, and Store
Passwords](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150).
Typically, a single key manager supports authentication based on X.509
public key certificates. Some secure socket implementations may also
support authentication based on shared secret keys, Kerberos, or other
mechanisms.

`KeyManager`{.codeph} objects are created either by a
`KeyManagerFactory`{.codeph}, or by providing a concrete implementation
of the interface.

</div>
</div>
<div class="sect4">
[]{#GUID-616A7E77-587C-44E0-9F69-92BEDF631D5F}

#### The KeyManagerFactory Class {#JSSEC-GUID-616A7E77-587C-44E0-9F69-92BEDF631D5F .sect4}

<div>
The `javax.net.ssl.KeyManagerFactory`{.codeph} class is an engine class
for a provider-based service that acts as a factory for one or more
types of `KeyManager`{.codeph} objects. The SunJSSE provider implements
a factory that can return a basic X.509 key manager. Because it is
provider-based, additional factories can be implemented and configured
to provide additional or alternative key managers.

</div>
<div class="sect5">
[]{#GUID-65A7A023-AE02-4A95-8210-386AE6F18EB5}

##### Creating a KeyManagerFactory {#JSSEC-GUID-65A7A023-AE02-4A95-8210-386AE6F18EB5 .sect5}

<div>
You create an instance of this class in a similar manner to
`SSLContext`{.codeph}, except for passing an algorithm name string
instead of a protocol name to the `getInstance()`{.codeph} method:

<div class="section">
``` {.codeblock dir="ltr"}
KeyManagerFactory kmf = getInstance(String algorithm);
KeyManagerFactory kmf = getInstance(String algorithm, String provider);
KeyManagerFactory kmf = getInstance(String algorithm, Provider provider);
```

A sample call as follows:

``` {.codeblock dir="ltr"}
KeyManagerFactory kmf = KeyManagerFactory.getInstance("SunX509", "SunJSSE");
```

The preceding call creates an instance of the SunJSSE provider\'s
default key manager factory, which provides basic X.509-based
authentication keys.

A newly created factory should be initialized by calling one of the
`init`{.codeph} methods:

``` {.codeblock dir="ltr"}
public void init(KeyStore ks, char[] password);
public void init(ManagerFactoryParameters spec);
```

Call whichever `init`{.codeph} method is appropriate for the
`KeyManagerFactory`{.codeph} you are using. If you are not sure, then
ask the provider vendor.

For many factories, such as the default SunX509
`KeyManagerFactory`{.codeph} from the SunJSSE provider, the
`KeyStore`{.codeph} and password are the only information required to
initialize the `KeyManagerFactory`{.codeph} and thus the first
`init`{.codeph} method is the appropriate one to call. The
`KeyManagerFactory`{.codeph} will query the `KeyStore`{.codeph} for
information about which private key and matching public key certificates
should be used for authenticating to a remote socket peer. The password
parameter specifies the password that will be used with the methods for
accessing keys from the `KeyStore`{.codeph}. All keys in the
`KeyStore`{.codeph} must be protected by the same password.

Sometimes initialization parameters other than a `KeyStore`{.codeph} and
password are needed by a provider. Users of that provider are expected
to pass an implementation of the appropriate
`ManagerFactoryParameters`{.codeph} as defined by the provider. The
provider can then call the specified methods in the
`ManagerFactoryParameters`{.codeph} implementation to obtain the needed
information.

Some factories can provide access to authentication material without
being initialized with a `KeyStore`{.codeph} object or any other
parameters. For example, they may access key material as part of a login
mechanism such as one based on JAAS, the Java Authentication and
Authorization Service.

As previously indicated, the SunJSSE provider supports a SunX509 factory
that must be initialized with a `KeyStore`{.codeph} parameter.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-9C8442E4-279D-4E60-B4D0-3B1558C99F4F}

#### The X509KeyManager Interface {#JSSEC-GUID-9C8442E4-279D-4E60-B4D0-3B1558C99F4F .sect4}

The `javax.net.ssl.X509KeyManager`{.codeph} interface extends the
general `KeyManager`{.codeph} interface. It must be implemented by a key
manager for X.509-based authentication. To support X.509 authentication
to remote socket peers through JSSE, an instance of this interface must
be passed to the `init()`{.codeph} method of an `SSLContext`{.codeph}
object.

<div class="sect5">
[]{#GUID-FEA439FF-8110-4F2D-82AF-54815002805E}

##### Creating an X509KeyManager {#JSSEC-GUID-FEA439FF-8110-4F2D-82AF-54815002805E .sect5}

<div>
You can either implement this interface directly yourself or obtain one
from a provider-based `KeyManagerFactory`{.codeph} (such as that
supplied by the SunJSSE provider). You could also implement your own
interface that delegates to a factory-generated key manager. For
example, you might do this to filter the resulting keys and query an
end-user through a graphical user interface.

</div>
</div>
<div class="sect5">
[]{#GUID-E0A44B4B-A888-4997-AB5E-5E0580FF87DE}

##### Creating Your Own X509KeyManager {#JSSEC-GUID-E0A44B4B-A888-4997-AB5E-5E0580FF87DE .sect5}

<div>
<div class="section">
If the default `X509KeyManager`{.codeph} behavior is not suitable for
your situation, then you can create your own `X509KeyManager`{.codeph}
in a way similar to that shown in [Creating Your Own
X509TrustManager](java-secure-socket-extension-jsse-reference-guide.htm#GUID-E1205974-3249-4E40-83C0-5F89C7375CF4 "If the supplied X509TrustManager behavior is not suitable for your situation, then you can create your own X509TrustManager by either creating and registering your own TrustManagerFactory or by implementing the X509TrustManager interface directly.").

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-5C4AC46A-DE04-4D72-B94A-35C1F1B94A41}

#### The X509ExtendedKeyManager Class {#JSSEC-GUID-5C4AC46A-DE04-4D72-B94A-35C1F1B94A41 .sect4}

<div>
The `X509ExtendedKeyManager`{.codeph} abstract class is an
implementation of the `X509KeyManager`{.codeph} interface that allows
for connection-specific key selection. It adds two methods that select a
key alias for client or server based on the key type, allowed issuers,
and current `SSLEngine`{.codeph}:

-   `public String chooseEngineClientAlias(String[] keyType, Principal[] issuers, SSLEngine engine)`{.codeph}
-   `public String chooseEngineServerAlias(String keyType, Principal[] issuers, SSLEngine engine)`{.codeph}

If a key manager is not an instance of the
`X509ExtendedKeyManager`{.codeph} class, then it will not work with the
`SSLEngine`{.codeph} class.

For JSSE providers and key manager implementations, the
`X509ExtendedKeyManager`{.codeph} class is highly recommended over the
legacy `X509KeyManager`{.codeph} interface.

In TLS 1.2 and later, both client and server can specify which hash and
signature algorithms they will accept. To pass the authentication
required by the remote side, local key selection decisions must be based
on both X509 certificates and the remote accepted hash and signature
algorithms. The remote accepted hash and signature algorithms can be
retrieved using the
`ExtendedSSLSession.getPeerSupportedSignatureAlgorithms()`{.codeph}
method.

You can create your own `X509ExtendedKeyManager`{.codeph} subclass in a
way similar to that shown in [Creating Your Own
X509TrustManager](java-secure-socket-extension-jsse-reference-guide.htm#GUID-E1205974-3249-4E40-83C0-5F89C7375CF4 "If the supplied X509TrustManager behavior is not suitable for your situation, then you can create your own X509TrustManager by either creating and registering your own TrustManagerFactory or by implementing the X509TrustManager interface directly.").

Support for the [Server Name Indication (SNI)
Extension](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F)
on the server side enables the key manager to check the server name and
select the appropriate key accordingly. For example, suppose there are
three key entries with certificates in the keystore:

-   `cn=www.example.com`{.codeph}
-   `cn=www.example.org`{.codeph}
-   `cn=www.example.net`{.codeph}

If the ClientHello message requests to connect to
`www.example.net`{.codeph} in the SNI extension, then the server should
be able to select the certificate with subject
`cn=www.example.net`{.codeph}.

</div>
</div>
<div class="sect4">
[]{#GUID-9D7375F9-D688-436D-A214-02653F50ED32}

#### Relationship Between a TrustManager and a KeyManager {#JSSEC-GUID-9D7375F9-D688-436D-A214-02653F50ED32 .sect4}

<div>
Historically, there has been confusion regarding the functionality of a
`TrustManager`{.codeph} and a `KeyManager`{.codeph}.

A `TrustManager`{.codeph} determines whether the remote authentication
credentials (and thus the connection) should be trusted.

A `KeyManager`{.codeph} determines which authentication credentials to
send to the remote host.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-1B0C19BB-0F27-4757-9CA5-D03037C4E658}

### Secondary Support Classes and Interfaces {#JSSEC-GUID-1B0C19BB-0F27-4757-9CA5-D03037C4E658 .sect3}

<div>
These classes are provided as part of the JSSE API to support the
creation, use, and management of secure sockets. They are less likely to
be used by secure socket applications than are the core and support
classes. The secondary support classes and interfaces are part of the
`javax.net.ssl`{.codeph} and `javax.security.cert`{.codeph} packages.

</div>
<div class="sect4">
[]{#GUID-BC9AD59B-05B6-4ACA-9CDD-D18ACEA3840D}

#### The SSLParameters Class {#JSSEC-GUID-BC9AD59B-05B6-4ACA-9CDD-D18ACEA3840D .sect4}

<div>
The `SSLParameters`{.codeph} class encapsulates the following parameters
that affect a SSL/TLS/DTLS connection:

-   The list of cipher suites to be accepted in an SSL/TLS/DTLS
    handshake
-   The list of protocols to be allowed
-   The endpoint identification algorithm during SSL/TLS/DTLS
    handshaking
-   The server names and server name matchers (see [Server Name
    Indication (SNI)
    Extension](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F))
-   The cipher suite preference to be used in an SSL/TLS/DTLS handshake
-   Algorithm during SSL/TLS/DTLS handshaking
-   The Server Name Indication (SNI)
-   The maximum network packet size
-   The algorithm constraints and whether SSL/TLS/DTLS servers should
    request or require client authentication

You can retrieve the current `SSLParameters`{.codeph} for an
`SSLSocket`{.codeph} or `SSLEngine`{.codeph} by using the following
methods:

-   `getSSLParameters()`{.codeph} in an `SSLSocket`{.codeph},
    `SSLServerSocket`{.codeph}, and `SSLEngine`{.codeph}
-   `getDefaultSSLParameters()`{.codeph} and
    `getSupportedSSLParamters()`{.codeph} in an `SSLContext`{.codeph}

You can assign `SSLParameters`{.codeph} with the
`setSSLParameters()`{.codeph} method in an `SSLSocket`{.codeph},
`SSLServerSocket`{.codeph} and `SSLEngine`{.codeph}.

You can explicitly set the server name indication with the
`SSLParameters.setServerNames()`{.codeph} method. The server name
indication in client mode also affects endpoint identification. In the
implementation of `X509ExtendedTrustManager`{.codeph}, it uses the
server name indication retrieved by the
`ExtendedSSLSession.getRequestedServerNames()`{.codeph} method. See
[Example
8-14](java-secure-socket-extension-jsse-reference-guide.htm#GUID-BC9AD59B-05B6-4ACA-9CDD-D18ACEA3840D__SAMPLECODETOSETTHESERVERNAMEINDICAT-6A7C526D).

<div class="example" id="GUID-BC9AD59B-05B6-4ACA-9CDD-D18ACEA3840D__SAMPLECODETOSETTHESERVERNAMEINDICAT-6A7C526D">
Example 8-14 Sample Code to Set Server Name Indication

This example uses the host name in the server name indication
(`www.example.com`{.codeph}) to make endpoint identification against the
peer\'s identity presented in the end-entity\'s X.509 certificate.

``` {.codeblock dir="ltr"}
    SSLSocketFactory factory = ...
    SSLSocket sslSocket = factory.createSocket("172.16.10.6", 443);
    // SSLEngine sslEngine = sslContext.createSSLEngine("172.16.10.6", 443);

    SNIHostName serverName = new SNIHostName("www.example.com");
    List<SNIServerName> serverNames = new ArrayList<>(1);
    serverNames.add(serverName);
 
    SSLParameters params = sslSocket.getSSLParameters();
    params.setServerNames(serverNames);
    sslSocket.setSSLParameters(params);
    // sslEngine.setSSLParameters(params);
```

</div>
<!-- class="example" -->

</div>
<div class="sect5">
[]{#GUID-EFC2FACC-680C-42CE-A3A9-E9A6673EA813}

##### Cipher Suite Preference {#JSSEC-GUID-EFC2FACC-680C-42CE-A3A9-E9A6673EA813 .sect5}

<div>
During TLS handshaking, the client requests to negotiate a cipher suite
from a list of cryptographic options that it supports, starting with its
first preference. Then, the server selects a single cipher suite from
the list of cipher suites requested by the client. Normally, the
selection honors the client\'s preference. However, to mitigate the
risks of using weak cipher suites, the server may select cipher suites
based on its own preference rather than the client\'s preference, by
invoking the method
`SSLParameters.setUseCipherSuitesOrder(true)`{.codeph}.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-4E20A067-B139-4754-B4B3-AAF372F76D02}

#### The SSLSessionContext Interface {#JSSEC-GUID-4E20A067-B139-4754-B4B3-AAF372F76D02 .sect4}

<div>
The `javax.net.ssl.SSLSessionContext`{.codeph} interface is a grouping
of
[SSLSession](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AB362290-033A-4D3B-AAF3-1BFEB1CD472B "The javax.net.ssl.SSLSession interface represents a security context negotiated between the two peers of an SSLSocket or SSLEngine connection. After a session has been arranged, it can be shared by future SSLSocket or SSLEngine objects connected between the same two peers.")
objects associated with a single entity. For example, it could be
associated with a server or client that participates in many sessions
concurrently. The methods in this interface enable the enumeration of
all sessions in a context and allow lookup of specific sessions via
their session IDs.

An `SSLSessionContext`{.codeph} may optionally be obtained from an
`SSLSession`{.codeph} by calling the SSLSession
`getSessionContext()`{.codeph} method. The context may be unavailable in
some environments, in which case the `getSessionContext()`{.codeph}
method returns null.

</div>
</div>
<div class="sect4">
[]{#GUID-F2F8AC17-849A-40EE-A385-FD15328999B6}

#### The SSLSessionBindingListener Interface {#JSSEC-GUID-F2F8AC17-849A-40EE-A385-FD15328999B6 .sect4}

<div>
The `javax.net.ssl.SSLSessionBindingListener`{.codeph} interface is
implemented by objects that are notified when they are being bound or
unbound from an
[SSLSession](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AB362290-033A-4D3B-AAF3-1BFEB1CD472B "The javax.net.ssl.SSLSession interface represents a security context negotiated between the two peers of an SSLSocket or SSLEngine connection. After a session has been arranged, it can be shared by future SSLSocket or SSLEngine objects connected between the same two peers.").

</div>
</div>
<div class="sect4">
[]{#GUID-C32994C1-0F5E-42D0-9CB6-EF4422024730}

#### The SSLSessionBindingEvent Class {#JSSEC-GUID-C32994C1-0F5E-42D0-9CB6-EF4422024730 .sect4}

<div>
The `javax.net.ssl.SSLSessionBindingEvent`{.codeph} class defines the
event communicated to an
<span class="apiname">SSLSessionBindingListener</span> (see [The
SSLSessionBindingListener
Interface](java-secure-socket-extension-jsse-reference-guide.htm#GUID-F2F8AC17-849A-40EE-A385-FD15328999B6))
when it is bound or unbound from an
<span class="apiname">SSLSession</span> (see [SSLSession and
ExtendedSSLSession](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AB362290-033A-4D3B-AAF3-1BFEB1CD472B "The javax.net.ssl.SSLSession interface represents a security context negotiated between the two peers of an SSLSocket or SSLEngine connection. After a session has been arranged, it can be shared by future SSLSocket or SSLEngine objects connected between the same two peers.")).

</div>
</div>
<div class="sect4">
[]{#GUID-DFBAA9D1-C08B-48C9-88FE-F88003A6A6C7}

#### The HandShakeCompletedListener Interface {#JSSEC-GUID-DFBAA9D1-C08B-48C9-88FE-F88003A6A6C7 .sect4}

<div>
The `javax.net.ssl.HandShakeCompletedListener`{.codeph} interface is an
interface implemented by any class that is notified of the completion of
an SSL protocol handshake on a given `SSLSocket`{.codeph} connection.

</div>
</div>
<div class="sect4">
[]{#GUID-F242B876-6932-4B17-A755-1D9AFA25E54B}

#### The HandShakeCompletedEvent Class {#JSSEC-GUID-F242B876-6932-4B17-A755-1D9AFA25E54B .sect4}

<div>
The `javax.net.ssl.HandShakeCompletedEvent`{.codeph} class defines the
event communicated to a
<span class="apiname">HandShakeCompletedListener</span> (see [The
HandShakeCompletedListener
Interface](java-secure-socket-extension-jsse-reference-guide.htm#GUID-DFBAA9D1-C08B-48C9-88FE-F88003A6A6C7 "The javax.net.ssl.HandShakeCompletedListener interface is an interface implemented by any class that is notified of the completion of an SSL protocol handshake on a given SSLSocket connection."))
upon completion of an SSL protocol handshake on a given
`SSLSocket`{.codeph} connection.

</div>
</div>
<div class="sect4">
[]{#GUID-9E46E5AA-FE3E-48D7-B616-98A143F74587}

#### The HostnameVerifier Interface {#JSSEC-GUID-9E46E5AA-FE3E-48D7-B616-98A143F74587 .sect4}

<div>
If the SSL/TLS implementation\'s standard host name verification logic
fails, then the implementation calls the `verify()`{.codeph} method of
the class that implements this interface and is assigned to this
`HttpsURLConnection`{.codeph} instance. If the callback class can
determine that the host name is acceptable given the parameters, it
reports that the connection should be allowed. An unacceptable response
causes the connection to be terminated. See [Example
8-15](java-secure-socket-extension-jsse-reference-guide.htm#GUID-9E46E5AA-FE3E-48D7-B616-98A143F74587__SAMPLECODEFORHOSTNAMEVERIFIERINTERF-6A7C5993).

See
[`HttpsURLConnection`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/HttpsURLConnection.html)
for more information about how to assign the `HostnameVerifier`{.codeph}
to the `HttpsURLConnection`{.codeph}.

<div class="example" id="GUID-9E46E5AA-FE3E-48D7-B616-98A143F74587__SAMPLECODEFORHOSTNAMEVERIFIERINTERF-6A7C5993">
Example 8-15 Sample Code for Implementing the HostnameVerifier Interface

The following example illustrates a class that implements
`HostnameVerifier`{.codeph} interface:

``` {.codeblock dir="ltr"}
    public class MyHostnameVerifier implements HostnameVerifier {
    
        public boolean verify(String hostname, SSLSession session) {
            // pop up an interactive dialog box
            // or insert additional matching logic
            if (good_address) {
                return true;
            } else {
                return false;
            }
        }
    }
    
    //...deleted...
    
    HttpsURLConnection urlc = (HttpsURLConnection)
      (new URL("https://www.example.com/")).openConnection();
    urlc.setHostnameVerifier(new MyHostnameVerifier());
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-1B4C6B3B-CDB3-433D-8F24-41EF5DE2FA5F}

#### The X509Certificate Class {#JSSEC-GUID-1B4C6B3B-CDB3-433D-8F24-41EF5DE2FA5F .sect4}

<div>
Many secure socket protocols perform authentication using public key
certificates, also called X.509 certificates. This is the default
authentication mechanism for the SSL/TLS protocols.

The `java.security.cert.X509Certificate`{.codeph} abstract class
provides a standard way to access the attributes of X.509 certificates.

<div class="infoboxnote" id="GUID-1B4C6B3B-CDB3-433D-8F24-41EF5DE2FA5F__GUID-C14C49BA-6583-4041-87ED-DC62E7F52B5F">
Note:

The `javax.security.cert.X509Certificate`{.codeph} class is supported
only for backward compatibility with previous (1.0.x and 1.1.x) versions
of JSSE. New applications should use the
`java.security.cert.X509Certificate`{.codeph} class instead.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-54BC5FB3-3841-4005-A876-9FA2F49B2D0F}

#### The AlgorithmConstraints Interface {#JSSEC-GUID-54BC5FB3-3841-4005-A876-9FA2F49B2D0F .sect4}

<div>
The `java.security.AlgorithmConstraints`{.codeph} interface is used for
controlling allowed cryptographic algorithms.
`AlgorithmConstraints`{.codeph} defines three `permits()`{.codeph}
methods. These methods tell whether an algorithm name or a key is
permitted for certain cryptographic functions. Cryptographic functions
are represented by a set of `CryptoPrimitive`{.codeph}, which is an
enumeration containing fields like `STREAM_CIPHER`{.codeph},
`MESSAGE_DIGEST`{.codeph}, and `SIGNATURE`{.codeph}.

Thus, an `AlgorithmConstraints`{.codeph} implementation can answer
questions like: Can I use this key with this algorithm for the purpose
of a cryptographic operation?

An `AlgorithmConstraints`{.codeph} object can be associated with an
`SSLParameters`{.codeph} object by using the new
`setAlgorithmConstraints()`{.codeph} method. The current
`AlgorithmConstraints`{.codeph} object for an `SSLParameters`{.codeph}
object is retrieved using the `getAlgorithmConstraints()`{.codeph}
method.

</div>
</div>
<div class="sect4">
[]{#GUID-651B5070-F586-4504-A6CD-8BEB2D928D47}

#### The StandardConstants Class {#JSSEC-GUID-651B5070-F586-4504-A6CD-8BEB2D928D47 .sect4}

<div>
The `StandardConstants`{.codeph} class is used to represent standard
constants definitions in JSSE.

`StandardConstants.SNI_HOST_NAME`{.codeph} represents a domain name
server (DNS) host name in a [Server Name Indication
(SNI)](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F)
extension, which can be used when instantiating an
`SNIServerName`{.codeph} or `SNIMatcher`{.codeph} object.

</div>
</div>
<div class="sect4">
[]{#GUID-ADD484B7-244A-4FBC-AEF0-96873890CD6B}

#### The SNIServerName Class {#JSSEC-GUID-ADD484B7-244A-4FBC-AEF0-96873890CD6B .sect4}

<div>
An instance of the abstract `SNIServerName`{.codeph} class represents a
server name in the [Server Name Indication
(SNI)](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F)
extension. It is instantiated using the type and encoded value of the
specified server name.

You can use the `getType()`{.codeph} and `getEncoded()`{.codeph} methods
to return the server name type and a copy of the encoded server name
value, respectively. The `equals()`{.codeph} method can be used to check
if some other object is \"equal\" to this server name. The
`hashCode()`{.codeph} method returns a hash code value for this server
name. To get a string representation of the server name (including the
server name type and encoded server name value), use the
`toString()`{.codeph} method.

</div>
</div>
<div class="sect4">
[]{#GUID-073F0493-3DB8-4388-818B-83E92021EF45}

#### The SNIMatcher Class {#JSSEC-GUID-073F0493-3DB8-4388-818B-83E92021EF45 .sect4}

<div>
An instance of the abstract `SNIMatcher`{.codeph} class performs match
operations on an `SNIServerName`{.codeph} object. Servers can use
information from the [Server Name Indication
(SNI)](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F)
extension to decide if a specific `SSLSocket`{.codeph} or
`SSLEngine`{.codeph} should accept a connection. For example, when
multiple \"virtual\" or \"name-based\" servers are hosted on a single
underlying network address, the server application can use SNI
information to determine whether this server is the exact server that
the client wants to access. Instances of this class can be used by a
server to verify the acceptable server names of a particular type, such
as host names.

The `SNIMatcher`{.codeph} class is instantiated using the specified
server name type on which match operations will be performed. To match a
given `SNIServerName`{.codeph}, use the `matches()`{.codeph} method. To
return the server name type of the given `SNIMatcher`{.codeph} object,
use the `getType()`{.codeph} method.

</div>
</div>
<div class="sect4">
[]{#GUID-E10158C4-E808-41B7-9958-A119927743D8}

#### The SNIHostName Class {#JSSEC-GUID-E10158C4-E808-41B7-9958-A119927743D8 .sect4}

<div>
An instance of the `SNIHostName`{.codeph} class (which extends the
`SNIServerName`{.codeph} class) represents a server name of type
\"host\_name\" (see [The StandardConstants
Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-651B5070-F586-4504-A6CD-8BEB2D928D47 "The StandardConstants class is used to represent standard constants definitions in JSSE."))
in the [Server Name Indication (SNI)
Extension](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F).
To instantiate an `SNIHostName`{.codeph}, specify the fully qualified
DNS host name of the server (as understood by the client) as a
`String`{.codeph} argument. The argument is illegal in the following
cases:

-   The argument is empty.
-   The argument ends with a trailing period.
-   The argument is not a valid Internationalized Domain Name (IDN)
    compliant with the RFC 3490 specification.

You can also instantiate an `SNIHostName`{.codeph} by specifying the
encoded host name value as a byte array. This method is typically used
to parse the encoded name value in a requested SNI extension. Otherwise,
use the `SNIHostName(String hostname)`{.codeph} constructor. The
`encoded`{.codeph} argument is illegal in the following cases:

-   The argument is empty.
-   The argument ends with a trailing period.
-   The argument is not a valid Internationalized Domain Name (IDN)
    compliant with the RFC 3490 specification.
-   The argument is not encoded in UTF-8 or US-ASCII.

<div class="p">
<div class="infoboxnote" id="GUID-E10158C4-E808-41B7-9958-A119927743D8__GUID-7C99C76D-9832-47F9-8FF8-7FD2123DE7EC">
Note:

The `encoded`{.codeph} byte array passed in as an argument is cloned to
protect against subsequent modification.

</div>
</div>
To return the host name of an `SNIHostName`{.codeph} object in US-ASCII
encoding, use the `getAsciiName()`{.codeph} method. To compare a server
name to another object, use the `equals()`{.codeph} method (comparison
is <span class="italic">not</span> case-sensitive). To return a hash
code value of an `SNIHostName`{.codeph}, use the `hashCode()`{.codeph}
method. To return a string representation of an `SNIHostName`{.codeph},
including the DNS host name, use the `toString()`{.codeph} method.

You can create an `SNIMatcher`{.codeph} object for an
`SNIHostName`{.codeph} object by passing a regular expression
representing one or more host names to match to the
`createSNIMatcher()`{.codeph} method.

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9}

Customizing JSSE {#JSSEC-GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9 .sect2}
----------------

<div>
JSSE includes a standard implementation that can be customized by
plugging in different implementations or specifying the default
keystore, and so on.

<div class="section">
[Table
8-7](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__SECURITYPROPERTIESANDCUSTOMIZEITEMS-DCEC7645 "List of Security Properties and the customizable items.")
and [Table
8-8](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__SYSTEMPROPERTIESANDCUSTOMIZEITEMSIN-DCEEB591 "List of system properties and customized items.")
summarize which aspects can be customized, what the defaults are, and
which mechanisms are used to provide customization.

Some of the customizations are done by setting system property or
Security Property values. Sections following the table explain how to
set such property values.

<div class="p">
<div class="infoboxnote" id="GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__GUID-6E3ACF45-C569-4DA9-9905-08713A2D064C">
Note:

Many of the properties shown in this table are currently used by the
JSSE implementation, but there is no guarantee that they will continue
to have the same names and types (system or security) or even that they
will exist at all in future releases. All such properties are flagged
with an asterisk (\*). They are documented here for your convenience for
use with the JSSE implementation.

</div>
</div>
</div>
<!-- class="section" -->

<div class="section">
[Table
8-7](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__SECURITYPROPERTIESANDCUSTOMIZEITEMS-DCEC7645 "List of Security Properties and the customizable items.")
shows items that are customized by setting the
`java.security.Security`{.codeph} property. See [How to Specify a
java.security.Security
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-38CC6235-823B-49D7-A566-4BEA1B64C9C6)

<div class="tblformalwide" id="GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__SECURITYPROPERTIESANDCUSTOMIZEITEMS-DCEC7645">
Table 8-7 Security Properties and Customized Items

+-----------------+-----------------+-----------------+-----------------+
| Security        | Customized Item | Default Value   | Notes           |
| Property        |                 |                 |                 |
+:================+:================+:================+:================+
| `cert.provider. | [Customizing    | X509Certificate | None            |
| x509v1`{.codeph | the             | implementation  |                 |
| }               | X509Certificate | from Oracle     |                 |
|                 | Implementation] |                 |                 |
|                 | (java-secure-so |                 |                 |
|                 | cket-extension- |                 |                 |
|                 | jsse-reference- |                 |                 |
|                 | guide.htm#GUID- |                 |                 |
|                 | F196CEDD-DC14-4 |                 |                 |
|                 | 0EA-852A-133DB9 |                 |                 |
|                 | BA798B "The X50 |                 |                 |
|                 | 9Certificate im |                 |                 |
|                 | plementation re |                 |                 |
|                 | turned by the X |                 |                 |
|                 | 509Certificate. |                 |                 |
|                 | getInstance() m |                 |                 |
|                 | ethod is by def |                 |                 |
|                 | ault the implem |                 |                 |
|                 | entation from t |                 |                 |
|                 | he JSSE impleme |                 |                 |
|                 | ntation.")      |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| `jdk.tls.client | Client-side     | [Table          | <span class="bo |
| .cipherSuites`{ | default enabled | 4-11](oracle-pr | ld">Caution</sp |
| .codeph}        | cipher suites;  | oviders.htm#GUI | an>:            |
|                 | see [Specifying | D-7093246A-31A3 | These system    |
|                 | Default Enabled | -4304-AC5F-5FB6 | properties can  |
|                 | Cipher          | 400405E2__CIPHE | be used to      |
|                 | Suites](java-se | RSUITESSUPPORTE | configure weak  |
|                 | cure-socket-ext | DBYSUNJSSE-29E4 | cipher suites,  |
|                 | ension-jsse-ref | 60FE "List of c | or the          |
|                 | erence-guide.ht | ipher suites su | configured      |
|                 | m#GUID-D61663E8 | pported by SunJ | cipher suites   |
|                 | -2405-4B2D-A1F1 | SSE, whether th | may be weak in  |
|                 | -B8C7EA2688DB " | ey are enabled  | the future. It  |
|                 | You can specify | or disabled by  | is not          |
|                 |  the default en | default, and th | recommended     |
|                 | abled cipher su | e release in wh | that you use    |
|                 | ites in your ap | ich they were i | these system    |
|                 | plication or wi | ntroduced"),    | properties      |
|                 | th the system p | Cipher Suites   | without         |
|                 | roperties jdk.t | Supported by    | understanding   |
|                 | ls.client.ciphe | SunJSSE         | the risks.      |
|                 | rSuites and jdk |                 |                 |
|                 | .tls.server.cip |                 |                 |
|                 | herSuites.")    |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| `jdk.tls.server | Server-side     | [Table          | <span class="bo |
| .cipherSuites`{ | default enabled | 4-11](oracle-pr | ld">Caution</sp |
| .codeph}        | cipher suites;  | oviders.htm#GUI | an>:            |
|                 | see [Specifying | D-7093246A-31A3 | These system    |
|                 | Default Enabled | -4304-AC5F-5FB6 | properties can  |
|                 | Cipher          | 400405E2__CIPHE | be used to      |
|                 | Suites](java-se | RSUITESSUPPORTE | configure weak  |
|                 | cure-socket-ext | DBYSUNJSSE-29E4 | cipher suites,  |
|                 | ension-jsse-ref | 60FE "List of c | or the          |
|                 | erence-guide.ht | ipher suites su | configured      |
|                 | m#GUID-D61663E8 | pported by SunJ | cipher suites   |
|                 | -2405-4B2D-A1F1 | SSE, whether th | may be weak in  |
|                 | -B8C7EA2688DB " | ey are enabled  | the future. It  |
|                 | You can specify | or disabled by  | is not          |
|                 |  the default en | default, and th | recommended     |
|                 | abled cipher su | e release in wh | that you use    |
|                 | ites in your ap | ich they were i | these system    |
|                 | plication or wi | ntroduced"),    | properties      |
|                 | th the system p | Cipher Suites   | without         |
|                 | roperties jdk.t | Supported by    | understanding   |
|                 | ls.client.ciphe | SunJSSE         | the risks.      |
|                 | rSuites and jdk |                 |                 |
|                 | .tls.server.cip |                 |                 |
|                 | herSuites.")    |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| `security.provi | Cryptographic   | The first five  | Specify the     |
| der.n`{.codeph} | service         | providers in    | provider in the |
|                 | provider; see   | order of        | `security.provi |
|                 | [Customizing    | priority are:   | der.n=`{.codeph |
|                 | the Provider    |                 | }               |
|                 | Implementation] | 1.  SUN         | line in         |
|                 | (java-secure-so | 2.  SunRsaSign  | security        |
|                 | cket-extension- | 3.  SunEC       | properties      |
|                 | jsse-reference- | 4.  SunJSSE     | file, where     |
|                 | guide.htm#GUID- | 5.  SunJCE      | `n`{.codeph} is |
|                 | 8BC473B2-CD64-4 |                 | an integer      |
|                 | E8B-8136-80BB28 |                 | whose value is  |
|                 | 6091B1 "The JDK |                 | equal or        |
|                 |  comes with a J |                 | greater than 1. |
|                 | SSE Cryptograph |                 |                 |
|                 | ic Service Prov |                 |                 |
|                 | ider, or provid |                 |                 |
|                 | er for short, n |                 |                 |
|                 | amed SunJSSE. P |                 |                 |
|                 | roviders are es |                 |                 |
|                 | sentially packa |                 |                 |
|                 | ges that implem |                 |                 |
|                 | ent one or more |                 |                 |
|                 |  engine classes |                 |                 |
|                 |  for specific c |                 |                 |
|                 | ryptographic al |                 |                 |
|                 | gorithms.")     |                 |                 |
|                 | and             |                 |                 |
|                 | [Customizing    |                 |                 |
|                 | the Encryption  |                 |                 |
|                 | Algorithm       |                 |                 |
|                 | Providers](java |                 |                 |
|                 | -secure-socket- |                 |                 |
|                 | extension-jsse- |                 |                 |
|                 | reference-guide |                 |                 |
|                 | .htm#GUID-316FB |                 |                 |
|                 | 978-7588-442E-B |                 |                 |
|                 | 829-B4973DB3B58 |                 |                 |
|                 | 4 "The SunJSSE  |                 |                 |
|                 | provider uses t |                 |                 |
|                 | he SunJCE imple |                 |                 |
|                 | mentation for a |                 |                 |
|                 | ll its cryptogr |                 |                 |
|                 | aphic needs. Al |                 |                 |
|                 | though it is re |                 |                 |
|                 | commended that  |                 |                 |
|                 | you leave the p |                 |                 |
|                 | rovider at its  |                 |                 |
|                 | regular positio |                 |                 |
|                 | n, you can use  |                 |                 |
|                 | implementations |                 |                 |
|                 |  from other JCA |                 |                 |
|                 |  or JCE provide |                 |                 |
|                 | rs by registeri |                 |                 |
|                 | ng them before  |                 |                 |
|                 | the SunJCE prov |                 |                 |
|                 | ider.")         |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`ssl.SocketFa | Default         | `SSLSocketFacto | None            |
| ctory.provider` | `SSLSocketFacto | ry`{.codeph}    |                 |
| {.codeph}       | ry`{.codeph}    | implementation  |                 |
|                 | implementation  | from Oracle     |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`ssl.ServerSo | Default         | `SSLServerSocke | None            |
| cketFactory.pro | `SSLServerSocke | tFactory`{.code |                 |
| vider`{.codeph} | tFactory`{.code | ph}             |                 |
|                 | ph}             | implementation  |                 |
|                 | implementation  | from Oracle     |                 |
+-----------------+-----------------+-----------------+-----------------+
| `ssl.KeyManager | Default key     | SunX509         | None            |
| Factory.algorit | manager factory |                 |                 |
| hm`{.codeph}    | algorithm name  |                 |                 |
|                 | (see            |                 |                 |
|                 | [Customizing    |                 |                 |
|                 | the Default Key |                 |                 |
|                 | Managers and    |                 |                 |
|                 | Trust           |                 |                 |
|                 | Managers](java- |                 |                 |
|                 | secure-socket-e |                 |                 |
|                 | xtension-jsse-r |                 |                 |
|                 | eference-guide. |                 |                 |
|                 | htm#GUID-0ACD92 |                 |                 |
|                 | 74-607C-49BE-AE |                 |                 |
|                 | D9-BEE2B4F2BEF2 |                 |                 |
|                 | ))              |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`jdk.certpath | Disabled        | MD2, MD5, SHA1  | None            |
| .disabledAlgori | certificate     | jdkCA & usage   |                 |
| thms`{.codeph}  | verification    | TLSServer, RSA  |                 |
|                 | cryptographic   | keySize \<      |                 |
|                 | algorithm (see  | 1024, DSA       |                 |
|                 | [Disabled and   | keySize \<      |                 |
|                 | Restricted      | 1024, EC        |                 |
|                 | Cryptographic   | keySize \<      |                 |
|                 | Algorithms](jav | 224[^Foot 4^](# |                 |
|                 | a-secure-socket | GUID-A41282C3-1 |                 |
|                 | -extension-jsse | 9A3-400A-A40F-8 |                 |
|                 | -reference-guid | 6F4DA22ABA9__RE |                 |
|                 | e.htm#GUID-0A43 | STRICTED_ALGORI |                 |
|                 | 8179-32A7-4900- | THMS_MAY_CHANGE |                 |
|                 | A81C-29E3073E1E | _FOOTNOTE){#GUI |                 |
|                 | 90 "In some env | D-A41282C3-19A3 |                 |
|                 | ironments, cert | -400A-A40F-86F4 |                 |
|                 | ain algorithms  | DA22ABA9__RESTR |                 |
|                 | or key lengths  | ICTED_ALGORITHM |                 |
|                 | may be undesira | S_MAY_CHANGE_FO |                 |
|                 | ble when using  | OTNOTE}         |                 |
|                 | SSL/TLS/DTLS. T |                 |                 |
|                 | he Oracle JDK u |                 |                 |
|                 | ses the jdk.cer |                 |                 |
|                 | tpath.disabledA |                 |                 |
|                 | lgorithms and j |                 |                 |
|                 | dk.tls.disabled |                 |                 |
|                 | Algorithm Secur |                 |                 |
|                 | ity Properties  |                 |                 |
|                 | to disable algo |                 |                 |
|                 | rithms during S |                 |                 |
|                 | SL/TLS/DTLS pro |                 |                 |
|                 | tocol negotiati |                 |                 |
|                 | on, including v |                 |                 |
|                 | ersion negotiat |                 |                 |
|                 | ion, cipher sui |                 |                 |
|                 | tes selection,  |                 |                 |
|                 | peer authentica |                 |                 |
|                 | tion, and key e |                 |                 |
|                 | xchange mechani |                 |                 |
|                 | sms. Note that  |                 |                 |
|                 | these Security  |                 |                 |
|                 | Properties are  |                 |                 |
|                 | not guaranteed  |                 |                 |
|                 | to be used by o |                 |                 |
|                 | ther JDK implem |                 |                 |
|                 | entations. See  |                 |                 |
|                 | the <java-home> |                 |                 |
|                 | /conf/security/ |                 |                 |
|                 | java.security f |                 |                 |
|                 | ile for informa |                 |                 |
|                 | tion about the  |                 |                 |
|                 | syntax of these |                 |                 |
|                 |  Security Prope |                 |                 |
|                 | rties and their |                 |                 |
|                 |  current active |                 |                 |
|                 |  values."))     |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| `ssl.TrustManag | Default trust   | PKIX            | None            |
| erFactory.algor | manager factory |                 |                 |
| ithm`{.codeph}  | algorithm name  |                 |                 |
|                 | (see            |                 |                 |
|                 | [Customizing    |                 |                 |
|                 | the Default Key |                 |                 |
|                 | Managers and    |                 |                 |
|                 | Trust           |                 |                 |
|                 | Managers](java- |                 |                 |
|                 | secure-socket-e |                 |                 |
|                 | xtension-jsse-r |                 |                 |
|                 | eference-guide. |                 |                 |
|                 | htm#GUID-0ACD92 |                 |                 |
|                 | 74-607C-49BE-AE |                 |                 |
|                 | D9-BEE2B4F2BEF2 |                 |                 |
|                 | ))              |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| [JCE encryption | Give            | SunJCE          | None            |
| algorithms used | alternative JCE | implementations |                 |
| by the SunJSSE  | algorithm       |                 |                 |
| provider](java- | providers a     |                 |                 |
| secure-socket-e | higher          |                 |                 |
| xtension-jsse-r | preference      |                 |                 |
| eference-guide. | order than the  |                 |                 |
| htm#GUID-316FB9 | SunJCE provider |                 |                 |
| 78-7588-442E-B8 |                 |                 |                 |
| 29-B4973DB3B584 |                 |                 |                 |
|  "The SunJSSE p |                 |                 |                 |
| rovider uses th |                 |                 |                 |
| e SunJCE implem |                 |                 |                 |
| entation for al |                 |                 |                 |
| l its cryptogra |                 |                 |                 |
| phic needs. Alt |                 |                 |                 |
| hough it is rec |                 |                 |                 |
| ommended that y |                 |                 |                 |
| ou leave the pr |                 |                 |                 |
| ovider at its r |                 |                 |                 |
| egular position |                 |                 |                 |
| , you can use i |                 |                 |                 |
| mplementations  |                 |                 |                 |
| from other JCA  |                 |                 |                 |
| or JCE provider |                 |                 |                 |
| s by registerin |                 |                 |                 |
| g them before t |                 |                 |                 |
| he SunJCE provi |                 |                 |                 |
| der.")          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`jdk.tls.disa | [Disabled and   | SSLv3, RC4,     | Disables        |
| bledAlgorithms` | Restricted      | MD5withRSA, DH  | specific        |
| {.codeph}       | Cryptographic   | keySize \<      | algorithms      |
|                 | Algorithms](jav | 1024, EC        | (protocols      |
|                 | a-secure-socket | keySize \<      | versions,       |
|                 | -extension-jsse | 224[^Footref 4^ | cipher suites,  |
|                 | -reference-guid | ](#fnsrc_d10810 | key exchange    |
|                 | e.htm#GUID-0A43 | 6e6311){#fnsrc_ | mechanisms,     |
|                 | 8179-32A7-4900- | d108106e6311}   | etc.) that will |
|                 | A81C-29E3073E1E |                 | not be          |
|                 | 90 "In some env |                 | negotiated for  |
|                 | ironments, cert |                 | SSL/TLS/DTLS    |
|                 | ain algorithms  |                 | connections,    |
|                 | or key lengths  |                 | even if they    |
|                 | may be undesira |                 | are enabled     |
|                 | ble when using  |                 | explicitly in   |
|                 | SSL/TLS/DTLS. T |                 | an application  |
|                 | he Oracle JDK u |                 |                 |
|                 | ses the jdk.cer |                 |                 |
|                 | tpath.disabledA |                 |                 |
|                 | lgorithms and j |                 |                 |
|                 | dk.tls.disabled |                 |                 |
|                 | Algorithm Secur |                 |                 |
|                 | ity Properties  |                 |                 |
|                 | to disable algo |                 |                 |
|                 | rithms during S |                 |                 |
|                 | SL/TLS/DTLS pro |                 |                 |
|                 | tocol negotiati |                 |                 |
|                 | on, including v |                 |                 |
|                 | ersion negotiat |                 |                 |
|                 | ion, cipher sui |                 |                 |
|                 | tes selection,  |                 |                 |
|                 | peer authentica |                 |                 |
|                 | tion, and key e |                 |                 |
|                 | xchange mechani |                 |                 |
|                 | sms. Note that  |                 |                 |
|                 | these Security  |                 |                 |
|                 | Properties are  |                 |                 |
|                 | not guaranteed  |                 |                 |
|                 | to be used by o |                 |                 |
|                 | ther JDK implem |                 |                 |
|                 | entations. See  |                 |                 |
|                 | the <java-home> |                 |                 |
|                 | /conf/security/ |                 |                 |
|                 | java.security f |                 |                 |
|                 | ile for informa |                 |                 |
|                 | tion about the  |                 |                 |
|                 | syntax of these |                 |                 |
|                 |  Security Prope |                 |                 |
|                 | rties and their |                 |                 |
|                 |  current active |                 |                 |
|                 |  values.")      |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| `jdk.tls.server | Diffie-Hellman  | Safe prime      | Defines default |
| .defaultDHEPara | groups          | Diffie-Hellman  | finite field    |
| meters`{.codeph |                 | groups in       | Diffie-Hellman  |
| }               |                 | OpenJDK         | ephemeral (DHE) |
|                 |                 | SSL/TLS/DTLS    | parameters for  |
|                 |                 | implementation  | Transport Layer |
|                 |                 |                 | Security        |
|                 |                 |                 | (SSL/TLS/DTLS)  |
|                 |                 |                 | processing      |
+-----------------+-----------------+-----------------+-----------------+

</div>
<!-- class="inftblhruleinformal" -->

^Footnote 4^ The list of restricted algorithms specified in these
Security Properties may change; see the `java.security` file in your JDK
installation for the latest values.

\* <span>This System Property is currently used by the JSSE
implementation, but it is not guaranteed to be examined and used by
other implementations. If it <span class="variable">is</span> examined
by another implementation, then that implementation should handle it in
the same manner as the JSSE implementation does. There is no guarantee
the property will continue to exist or be of the same type (system or
security) in future releases.</span>

</div>
<!-- class="section" -->

<div class="section">
[Table
8-8](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__SYSTEMPROPERTIESANDCUSTOMIZEITEMSIN-DCEEB591 "List of system properties and customized items.")
shows items that are customized by setting `java.lang.System`{.codeph}
property. See [How to Specify a java.lang.System
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363).

<div class="tblformalwide" id="GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__SYSTEMPROPERTIESANDCUSTOMIZEITEMSIN-DCEEB591">
Table 8-8 System Properties and Customized Items

+-----------------+-----------------+-----------------+-----------------+
| System Property | Customized Item | Default         | Notes           |
+:================+:================+:================+:================+
| `java.protocol. | [Specifying an  | Implementation  | None            |
| handler.pkgs`{. | Alternative     | from Oracle     |                 |
| codeph}         | HTTPS Protocol  |                 |                 |
|                 | Implementation] |                 |                 |
|                 | (java-secure-so |                 |                 |
|                 | cket-extension- |                 |                 |
|                 | jsse-reference- |                 |                 |
|                 | guide.htm#GUID- |                 |                 |
|                 | 7EBD6A94-9ADE-4 |                 |                 |
|                 | 321-8915-17B376 |                 |                 |
|                 | 3F8E77 "You can |                 |                 |
|                 |  communicate se |                 |                 |
|                 | curely with an  |                 |                 |
|                 | SSL-enabled web |                 |                 |
|                 |  server by usin |                 |                 |
|                 | g the HTTPS URL |                 |                 |
|                 |  scheme for the |                 |                 |
|                 |  java.net.URL c |                 |                 |
|                 | lass. The JDK p |                 |                 |
|                 | rovides a defau |                 |                 |
|                 | lt HTTPS URL im |                 |                 |
|                 | plementation.") |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`javax.net.ss | Default         | None            | The value       |
| l.keyStore`{.co | keystore (see   |                 | `NONE`{.codeph} |
| deph}           | [Customizing    |                 | may be          |
|                 | the Default     |                 | specified. This |
|                 | Keystores and   |                 | setting is      |
|                 | Truststores,    |                 | appropriate if  |
|                 | Store Types,    |                 | the keystore is |
|                 | and Store       |                 | not file-based  |
|                 | Passwords](java |                 | (for example,   |
|                 | -secure-socket- |                 | it resides in a |
|                 | extension-jsse- |                 | hardware token) |
|                 | reference-guide |                 |                 |
|                 | .htm#GUID-7D9F4 |                 |                 |
|                 | 3B8-AABF-4C5B-9 |                 |                 |
|                 | 3E6-3AFB18B6615 |                 |                 |
|                 | 0))             |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`javax.net.ss | Default         | None            | It is           |
| l.keyStorePassw | keystore        |                 | inadvisable to  |
| ord`{.codeph}   | password (see   |                 | specify the     |
|                 | [Customizing    |                 | password in a   |
|                 | the Default     |                 | way that        |
|                 | Keystores and   |                 | exposes it to   |
|                 | Truststores,    |                 | discovery by    |
|                 | Store Types,    |                 | other users.    |
|                 | and Store       |                 |                 |
|                 | Passwords](java |                 | For example,    |
|                 | -secure-socket- |                 | specifying the  |
|                 | extension-jsse- |                 | password on the |
|                 | reference-guide |                 | command line.   |
|                 | .htm#GUID-7D9F4 |                 | To keep the     |
|                 | 3B8-AABF-4C5B-9 |                 | password        |
|                 | 3E6-3AFB18B6615 |                 | secure, have    |
|                 | 0))             |                 | the application |
|                 |                 |                 | prompt for the  |
|                 |                 |                 | password, or    |
|                 |                 |                 | specify the     |
|                 |                 |                 | password in a   |
|                 |                 |                 | properly        |
|                 |                 |                 | protected       |
|                 |                 |                 | option file     |
+-----------------+-----------------+-----------------+-----------------+
| \*`javax.net.ss | Default         | None            | None            |
| l.keyStoreProvi | keystore        |                 |                 |
| der`{.codeph}   | provider (see   |                 |                 |
|                 | [Customizing    |                 |                 |
|                 | the Default     |                 |                 |
|                 | Keystores and   |                 |                 |
|                 | Truststores,    |                 |                 |
|                 | Store Types,    |                 |                 |
|                 | and Store       |                 |                 |
|                 | Passwords](java |                 |                 |
|                 | -secure-socket- |                 |                 |
|                 | extension-jsse- |                 |                 |
|                 | reference-guide |                 |                 |
|                 | .htm#GUID-7D9F4 |                 |                 |
|                 | 3B8-AABF-4C5B-9 |                 |                 |
|                 | 3E6-3AFB18B6615 |                 |                 |
|                 | 0))             |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`javax.net.ss | Default         | `KeyStore.getDe | None            |
| l.keyStoreType` | keystore type   | faultType()`{.c |                 |
| {.codeph}       | (see            | odeph}          |                 |
|                 | [Customizing    |                 |                 |
|                 | the Default     |                 |                 |
|                 | Keystores and   |                 |                 |
|                 | Truststores,    |                 |                 |
|                 | Store Types,    |                 |                 |
|                 | and Store       |                 |                 |
|                 | Passwords](java |                 |                 |
|                 | -secure-socket- |                 |                 |
|                 | extension-jsse- |                 |                 |
|                 | reference-guide |                 |                 |
|                 | .htm#GUID-7D9F4 |                 |                 |
|                 | 3B8-AABF-4C5B-9 |                 |                 |
|                 | 3E6-3AFB18B6615 |                 |                 |
|                 | 0))             |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`javax.net.ss | Default         | `jssecacerts`{. | None            |
| l.trustStore`{. | truststore (see | codeph},        |                 |
| codeph}         | [Customizing    | if it exists.   |                 |
|                 | the Default     |                 |                 |
|                 | Keystores and   | Otherwise,      |                 |
|                 | Truststores,    | `cacerts`{.code |                 |
|                 | Store Types,    | ph}             |                 |
|                 | and Store       |                 |                 |
|                 | Passwords](java |                 |                 |
|                 | -secure-socket- |                 |                 |
|                 | extension-jsse- |                 |                 |
|                 | reference-guide |                 |                 |
|                 | .htm#GUID-7D9F4 |                 |                 |
|                 | 3B8-AABF-4C5B-9 |                 |                 |
|                 | 3E6-3AFB18B6615 |                 |                 |
|                 | 0))             |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`javax.net.ss | Default         | None            | It is           |
| l.trustStorePas | truststore      |                 | inadvisable to  |
| sword`{.codeph} | password (see   |                 | specify the     |
|                 | [Customizing    |                 | password in a   |
|                 | the Default     |                 | way that        |
|                 | Keystores and   |                 | exposes it to   |
|                 | Truststores,    |                 | discovery by    |
|                 | Store Types,    |                 | other users.    |
|                 | and Store       |                 |                 |
|                 | Passwords](java |                 | For example,    |
|                 | -secure-socket- |                 | specifying the  |
|                 | extension-jsse- |                 | password on the |
|                 | reference-guide |                 | command line.   |
|                 | .htm#GUID-7D9F4 |                 | To keep the     |
|                 | 3B8-AABF-4C5B-9 |                 | password        |
|                 | 3E6-3AFB18B6615 |                 | secure, have    |
|                 | 0))             |                 | the application |
|                 |                 |                 | prompt for the  |
|                 |                 |                 | password, or    |
|                 |                 |                 | specify the     |
|                 |                 |                 | password in a   |
|                 |                 |                 | properly        |
|                 |                 |                 | protected       |
|                 |                 |                 | option file     |
+-----------------+-----------------+-----------------+-----------------+
| \*`javax.net.ss | Default         | None            | None            |
| l.trustStorePro | truststore      |                 |                 |
| vider`{.codeph} | provider (see   |                 |                 |
|                 | [Customizing    |                 |                 |
|                 | the Default     |                 |                 |
|                 | Keystores and   |                 |                 |
|                 | Truststores,    |                 |                 |
|                 | Store Types,    |                 |                 |
|                 | and Store       |                 |                 |
|                 | Passwords](java |                 |                 |
|                 | -secure-socket- |                 |                 |
|                 | extension-jsse- |                 |                 |
|                 | reference-guide |                 |                 |
|                 | .htm#GUID-7D9F4 |                 |                 |
|                 | 3B8-AABF-4C5B-9 |                 |                 |
|                 | 3E6-3AFB18B6615 |                 |                 |
|                 | 0))             |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`javax.net.ss | Default         | `KeyStore.getDe | The value       |
| l.trustStoreTyp | truststore type | faultType()`{.c | `NONE`{.codeph} |
| e`{.codeph}     | (see            | odeph}          | may be          |
|                 | [Customizing    |                 | specified. This |
|                 | the Default     |                 | setting is      |
|                 | Keystores and   |                 | appropriate if  |
|                 | Truststores,    |                 | the truststore  |
|                 | Store Types,    |                 | is not          |
|                 | and Store       |                 | file-based (for |
|                 | Passwords](java |                 | example, it     |
|                 | -secure-socket- |                 | resides in a    |
|                 | extension-jsse- |                 | hardware token) |
|                 | reference-guide |                 |                 |
|                 | .htm#GUID-7D9F4 |                 |                 |
|                 | 3B8-AABF-4C5B-9 |                 |                 |
|                 | 3E6-3AFB18B6615 |                 |                 |
|                 | 0))             |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`https.proxyH | Default proxy   | None            | None            |
| ost`{.codeph}   | host            |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`https.proxyP | Default proxy   | 80              | None            |
| ort`{.codeph}   | port            |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`jsse.enableS | Server Name     | `true`{.codeph} | Server Name     |
| NIExtension`{.c | Indication      |                 | Indication      |
| odeph}          | option          |                 | (SNI) is a TLS  |
|                 |                 |                 | extension,      |
|                 |                 |                 | defined in [RFC |
|                 |                 |                 | 6066](http://ww |
|                 |                 |                 | w.ietf.org/rfc/ |
|                 |                 |                 | rfc6066.txt).   |
|                 |                 |                 | It enables TLS  |
|                 |                 |                 | connections to  |
|                 |                 |                 | virtual         |
|                 |                 |                 | servers, in     |
|                 |                 |                 | which multiple  |
|                 |                 |                 | servers for     |
|                 |                 |                 | different       |
|                 |                 |                 | network names   |
|                 |                 |                 | are hosted at a |
|                 |                 |                 | single          |
|                 |                 |                 | underlying      |
|                 |                 |                 | network         |
|                 |                 |                 | address. Some   |
|                 |                 |                 | very old        |
|                 |                 |                 | SSL/TLS vendors |
|                 |                 |                 | may not be able |
|                 |                 |                 | handle SSL/TLS  |
|                 |                 |                 | extensions. In  |
|                 |                 |                 | this case, set  |
|                 |                 |                 | this property   |
|                 |                 |                 | to              |
|                 |                 |                 | `false`{.codeph |
|                 |                 |                 | }               |
|                 |                 |                 | to disable the  |
|                 |                 |                 | SNI extension   |
+-----------------+-----------------+-----------------+-----------------+
| \*`https.cipher | Default cipher  | Determined by   | This contains a |
| Suites`{.codeph | suites          | the socket      | comma-separated |
| }               |                 | factory.        | list of cipher  |
|                 |                 |                 | suite names     |
|                 |                 |                 | specifying      |
|                 |                 |                 | which cipher    |
|                 |                 |                 | suites to       |
|                 |                 |                 | enable for use  |
|                 |                 |                 | on this         |
|                 |                 |                 | `HttpsURLConnec |
|                 |                 |                 | tion`{.codeph}. |
|                 |                 |                 | See the         |
|                 |                 |                 | [`SSLSocket.set |
|                 |                 |                 | EnabledCipherSu |
|                 |                 |                 | ites(String[])` |
|                 |                 |                 | {.codeph}](http |
|                 |                 |                 | s://docs.oracle |
|                 |                 |                 | .com/javase/10/ |
|                 |                 |                 | docs/api/javax/ |
|                 |                 |                 | net/ssl/SSLSock |
|                 |                 |                 | et.html#setEnab |
|                 |                 |                 | ledProtocols-ja |
|                 |                 |                 | va.lang.String: |
|                 |                 |                 | A-)             |
|                 |                 |                 | method. Note    |
|                 |                 |                 | that this       |
|                 |                 |                 | method sets the |
|                 |                 |                 | preference      |
|                 |                 |                 | order of the    |
|                 |                 |                 | ClientHello     |
|                 |                 |                 | cipher suites   |
|                 |                 |                 | directly from   |
|                 |                 |                 | the             |
|                 |                 |                 | <span class="ap |
|                 |                 |                 | iname">String</ |
|                 |                 |                 | span>           |
|                 |                 |                 | array passed to |
|                 |                 |                 | it.             |
+-----------------+-----------------+-----------------+-----------------+
| \*`https.protoc | Default         | Determined by   | This contains a |
| ols`{#GUID-A412 | handshaking     | the socket      | comma-separated |
| 82C3-19A3-400A- | protocols       | factory.        | list of         |
| A40F-86F4DA22AB |                 |                 | protocol suite  |
| A9__HTTPS.PROTO |                 |                 | names           |
| COLS_PROPERTY   |                 |                 | specifying      |
| .codeph}        |                 |                 | which protocol  |
|                 |                 |                 | suites to       |
|                 |                 |                 | enable on this  |
|                 |                 |                 | `HttpsURLConnec |
|                 |                 |                 | tion`{.codeph}. |
|                 |                 |                 | See             |
|                 |                 |                 | [`SSLSocket.set |
|                 |                 |                 | EnabledProtocol |
|                 |                 |                 | s(String[])`{.c |
|                 |                 |                 | odeph}](https:/ |
|                 |                 |                 | /docs.oracle.co |
|                 |                 |                 | m/javase/10/doc |
|                 |                 |                 | s/api/javax/net |
|                 |                 |                 | /ssl/SSLSocket. |
|                 |                 |                 | html#setEnabled |
|                 |                 |                 | CipherSuites-ja |
|                 |                 |                 | va.lang.String: |
|                 |                 |                 | A-)             |
+-----------------+-----------------+-----------------+-----------------+
| \* Customize    | Default HTTPS   | 443             | None            |
| via             | port            |                 |                 |
| `port`{.codeph} |                 |                 |                 |
| field in the    |                 |                 |                 |
| HTTPS URL.      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`jsse.SSLEngi | Default sizing  | None            | Setting this    |
| ne.acceptLargeF | buffers for     |                 | system property |
| ragments`{.code | large SSL/TLS   |                 | to              |
| ph}             | packets         |                 | `true`{.codeph} |
|                 |                 |                 | ,               |
|                 |                 |                 | `SSLSession`{.c |
|                 |                 |                 | odeph}          |
|                 |                 |                 | will size       |
|                 |                 |                 | buffers to      |
|                 |                 |                 | handle [large   |
|                 |                 |                 | data            |
|                 |                 |                 | packets](java-s |
|                 |                 |                 | ecure-socket-ex |
|                 |                 |                 | tension-jsse-re |
|                 |                 |                 | ference-guide.h |
|                 |                 |                 | tm#GUID-AB36229 |
|                 |                 |                 | 0-033A-4D3B-AAF |
|                 |                 |                 | 3-1BFEB1CD472B_ |
|                 |                 |                 | _GUID-17258111- |
|                 |                 |                 | C234-4640-B886- |
|                 |                 |                 | D85221CCE842)   |
|                 |                 |                 | by default.     |
|                 |                 |                 | This may cause  |
|                 |                 |                 | applications to |
|                 |                 |                 | allocate        |
|                 |                 |                 | unnecessarily   |
|                 |                 |                 | large           |
|                 |                 |                 | `SSLEngine`{.co |
|                 |                 |                 | deph}           |
|                 |                 |                 | buffers.        |
|                 |                 |                 | Instead,        |
|                 |                 |                 | applications    |
|                 |                 |                 | should          |
|                 |                 |                 | [dynamically    |
|                 |                 |                 | check for       |
|                 |                 |                 | buffer overflow |
|                 |                 |                 | conditions](jav |
|                 |                 |                 | a-secure-socket |
|                 |                 |                 | -extension-jsse |
|                 |                 |                 | -reference-guid |
|                 |                 |                 | e.htm#GUID-AC67 |
|                 |                 |                 | 00ED-ADC4-41EA- |
|                 |                 |                 | B111-2AEF2CBF77 |
|                 |                 |                 | 44 "The status  |
|                 |                 |                 | of the SSLEngin |
|                 |                 |                 | e is represente |
|                 |                 |                 | d by SSLEngineR |
|                 |                 |                 | esult.Status.") |
|                 |                 |                 | and resize      |
|                 |                 |                 | buffers as      |
|                 |                 |                 | appropriate     |
+-----------------+-----------------+-----------------+-----------------+
| \*`sun.security | Allow unsafe    | `false`{.codeph | Setting this    |
| .ssl.allowUnsaf | SSL/TLS         | }               | system property |
| eRenegotiation` | Renegotaions    |                 | to              |
| {.codeph}       | (see            |                 | `true`{.codeph} |
|                 | [Description of |                 | permits full    |
|                 | the Phase 2     |                 | (unsafe) legacy |
|                 | Fix](java-secur |                 | renegotiation.  |
|                 | e-socket-extens |                 |                 |
|                 | ion-jsse-refere |                 | This system     |
|                 | nce-guide.htm#G |                 | property is     |
|                 | UID-475E6316-28 |                 | <span>deprecate |
|                 | 3A-4A59-9B11-24 |                 | d               |
|                 | 79348C4629 "The |                 | and might be    |
|                 |  SunJSSE implem |                 | removed in a    |
|                 | entation reenab |                 | future JDK      |
|                 | les renegotiati |                 | release.</span> |
|                 | ons by default  |                 |                 |
|                 | for connections |                 |                 |
|                 |  to peers compl |                 |                 |
|                 | iant with RFC 5 |                 |                 |
|                 | 746. That is, b |                 |                 |
|                 | oth the client  |                 |                 |
|                 | and server must |                 |                 |
|                 |  support RFC 57 |                 |                 |
|                 | 46 in order to  |                 |                 |
|                 | securely renego |                 |                 |
|                 | tiate. SunJSSE  |                 |                 |
|                 | provides some i |                 |                 |
|                 | nteroperability |                 |                 |
|                 |  modes for conn |                 |                 |
|                 | ections with pe |                 |                 |
|                 | ers that have n |                 |                 |
|                 | ot been upgrade |                 |                 |
|                 | d, but users ar |                 |                 |
|                 | e strongly enco |                 |                 |
|                 | uraged to updat |                 |                 |
|                 | e both their cl |                 |                 |
|                 | ient and server |                 |                 |
|                 |  implementation |                 |                 |
|                 | s as soon as po |                 |                 |
|                 | ssible."))      |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| \*`sun.security | Allow legacy    | `true`{.codeph} | Setting this    |
| .ssl.allowLegac | Hello messages  |                 | system property |
| yHelloMessages` | (see            |                 | to true allows  |
| {.codeph}       | [Description of |                 | the peer to     |
|                 | the Phase 2     |                 | handshake       |
|                 | Fix](java-secur |                 | without         |
|                 | e-socket-extens |                 | requiring the   |
|                 | ion-jsse-refere |                 | proper RFC 5746 |
|                 | nce-guide.htm#G |                 | messages.       |
|                 | UID-475E6316-28 |                 |                 |
|                 | 3A-4A59-9B11-24 |                 | This system     |
|                 | 79348C4629 "The |                 | property is     |
|                 |  SunJSSE implem |                 | <span>deprecate |
|                 | entation reenab |                 | d               |
|                 | les renegotiati |                 | and might be    |
|                 | ons by default  |                 | removed in a    |
|                 | for connections |                 | future JDK      |
|                 |  to peers compl |                 | release.</span> |
|                 | iant with RFC 5 |                 |                 |
|                 | 746. That is, b |                 |                 |
|                 | oth the client  |                 |                 |
|                 | and server must |                 |                 |
|                 |  support RFC 57 |                 |                 |
|                 | 46 in order to  |                 |                 |
|                 | securely renego |                 |                 |
|                 | tiate. SunJSSE  |                 |                 |
|                 | provides some i |                 |                 |
|                 | nteroperability |                 |                 |
|                 |  modes for conn |                 |                 |
|                 | ections with pe |                 |                 |
|                 | ers that have n |                 |                 |
|                 | ot been upgrade |                 |                 |
|                 | d, but users ar |                 |                 |
|                 | e strongly enco |                 |                 |
|                 | uraged to updat |                 |                 |
|                 | e both their cl |                 |                 |
|                 | ient and server |                 |                 |
|                 |  implementation |                 |                 |
|                 | s as soon as po |                 |                 |
|                 | ssible."))      |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| `jdk.tls.client | [The SunJSSE    | None            | To enable       |
| .protocols`{#GU | Provider](oracl |                 | specific        |
| ID-A41282C3-19A | e-providers.htm |                 | `SunJSSE`{.code |
| 3-400A-A40F-86F | #GUID-7093246A- |                 | ph}             |
| 4DA22ABA9__JDK. | 31A3-4304-AC5F- |                 | protocols on    |
| TLS.CLIENT.PROT | 5FB6400405E2)   |                 | the client,     |
| OCOLS_PROPERTY  |                 |                 | specify them in |
| .codeph}        |                 |                 | a               |
|                 |                 |                 | comma-separated |
|                 |                 |                 | list within     |
|                 |                 |                 | quotation       |
|                 |                 |                 | marks; all      |
|                 |                 |                 | other supported |
|                 |                 |                 | protocols are   |
|                 |                 |                 | not enabled on  |
|                 |                 |                 | the client      |
|                 |                 |                 |                 |
|                 |                 |                 | <div class="p"> |
|                 |                 |                 | For example,    |
|                 |                 |                 |                 |
|                 |                 |                 | -   If          |
|                 |                 |                 |     `jdk.tls.cl |
|                 |                 |                 | ient.protocols= |
|                 |                 |                 | `{.codeph}`"TLS |
|                 |                 |                 | v1,TLSv1.1"`{.c |
|                 |                 |                 | odeph},         |
|                 |                 |                 |     then the    |
|                 |                 |                 |     default     |
|                 |                 |                 |     protocol    |
|                 |                 |                 |     settings on |
|                 |                 |                 |     the client  |
|                 |                 |                 |     for TLSv1   |
|                 |                 |                 |     and TLSv1.1 |
|                 |                 |                 |     are         |
|                 |                 |                 |     enabled,    |
|                 |                 |                 |     while       |
|                 |                 |                 |     SSLv3,      |
|                 |                 |                 |     TLSv1.2,    |
|                 |                 |                 |     and         |
|                 |                 |                 |     SSLv2Hello  |
|                 |                 |                 |     are not     |
|                 |                 |                 |     enabled     |
|                 |                 |                 |                 |
|                 |                 |                 | -   If          |
|                 |                 |                 |     `jdk.tls.cl |
|                 |                 |                 | ient.protocols= |
|                 |                 |                 | "DTLSv1.2"`{.co |
|                 |                 |                 | deph}           |
|                 |                 |                 |     , then the  |
|                 |                 |                 |     protocol    |
|                 |                 |                 |     setting on  |
|                 |                 |                 |     the client  |
|                 |                 |                 |     for DTLS1.2 |
|                 |                 |                 |     is enabled, |
|                 |                 |                 |     while       |
|                 |                 |                 |     DTLS1.0 is  |
|                 |                 |                 |     not enabled |
|                 |                 |                 |                 |
|                 |                 |                 | </div>          |
+-----------------+-----------------+-----------------+-----------------+
| `jdk.tls.epheme | [Customizing    | 1024 bits       | None            |
| ralDHKeySize`{. | Size of         |                 |                 |
| codeph}         | Ephemeral       |                 |                 |
|                 | Diffie-Hellman  |                 |                 |
|                 | Keys](java-secu |                 |                 |
|                 | re-socket-exten |                 |                 |
|                 | sion-jsse-refer |                 |                 |
|                 | ence-guide.htm# |                 |                 |
|                 | GUID-D9B216E8-3 |                 |                 |
|                 | EFC-4882-B76E-1 |                 |                 |
|                 | 7A87D8F2F9D "In |                 |                 |
|                 |  SSL/TLS/DTLS c |                 |                 |
|                 | onnections, eph |                 |                 |
|                 | emeral Diffie-H |                 |                 |
|                 | ellman (DH) key |                 |                 |
|                 | s may be used i |                 |                 |
|                 | nternally durin |                 |                 |
|                 | g the handshaki |                 |                 |
|                 | ng. The SunJSSE |                 |                 |
|                 |  provider provi |                 |                 |
|                 | des a flexible  |                 |                 |
|                 | approach to cus |                 |                 |
|                 | tomize the stre |                 |                 |
|                 | ngth of the eph |                 |                 |
|                 | emeral DH key s |                 |                 |
|                 | ize during SSL/ |                 |                 |
|                 | TLS/DTLS handsh |                 |                 |
|                 | aking.")        |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| `jsse.enableMFL | [Customizing    | false           | None            |
| NExtension`{.co | Maximum         |                 |                 |
| deph}           | Fragment Length |                 |                 |
|                 | Negotiation     |                 |                 |
|                 | (MFLN)          |                 |                 |
|                 | Extension](java |                 |                 |
|                 | -secure-socket- |                 |                 |
|                 | extension-jsse- |                 |                 |
|                 | reference-guide |                 |                 |
|                 | .htm#GUID-41D5F |                 |                 |
|                 | 11E-81BD-4C03-A |                 |                 |
|                 | 315-48016D9B9B3 |                 |                 |
|                 | 6 "In order to  |                 |                 |
|                 | negotiate small |                 |                 |
|                 | er maximum frag |                 |                 |
|                 | ment lengths, c |                 |                 |
|                 | lients have an  |                 |                 |
|                 | option to inclu |                 |                 |
|                 | de an extension |                 |                 |
|                 |  of type max_fr |                 |                 |
|                 | agment_length i |                 |                 |
|                 | n the ClientHel |                 |                 |
|                 | lo message. A s |                 |                 |
|                 | ystem property  |                 |                 |
|                 | jsse.enableMFLN |                 |                 |
|                 | Extension, can  |                 |                 |
|                 | be used to enab |                 |                 |
|                 | le or disable t |                 |                 |
|                 | he MFLN extensi |                 |                 |
|                 | on for SSL/TLS/ |                 |                 |
|                 | DTLS.")         |                 |                 |
+-----------------+-----------------+-----------------+-----------------+

</div>
<!-- class="inftblhruleinformal" -->

\* <span>This system property is currently used by the JSSE
implementation, but it is not guaranteed to be examined and used by
other implementations. If it <span class="variable">is</span> examined
by another implementation, then that implementation should handle it in
the same manner as the JSSE implementation does. There is no guarantee
the property will continue to exist or be of the same type (system or
security) in future releases.</span>

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363}

### How to Specify a java.lang.System Property {#JSSEC-GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363 .sect3}

<div>
<div class="section">
You can customize some aspects of JSSE by setting system properties.
There are several ways to set these properties:

</div>
<!-- class="section" -->

-   <span>To set a system property statically, use the `-D`{.codeph}
    option of the `java`{.codeph} command. For example, to run an
    application named MyApp and set the
    `javax.net.ssl.trustStore`{.codeph} system property to specify a
    truststore named MyCacertsFile. See
    [truststore](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150).
    Enter the following:</span>

    <div>
    ``` {.codeblock dir="ltr"}
            java -Djavax.net.ssl.trustStore=MyCacertsFile MyApp
                    
    ```

    </div>
-   <span>To set a system property dynamically, call the
    `java.lang.System.setProperty()`{.codeph} method in your
    code:</span>

    <div>
    ``` {.codeblock dir="ltr"}
            System.setProperty("propertyName", "propertyValue");
                    
    ```

    </div>
    <div>
    For example, a `setProperty()`{.codeph} call corresponding to the
    previous example for setting the `javax.net.ssl.trustStore`{.codeph}
    system property to specify a truststore named
    \"`MyCacertsFile`{.codeph}\" would be:

    ``` {.codeblock dir="ltr"}
            System.setProperty("javax.net.ssl.trustStore", "MyCacertsFile");
                    
    ```

    </div>
-   <span>In the Java Deployment environment (Plug-In/Web Start), there
    are several ways to set the system properties.</span>
    <div>
    -   Use the Java Control Panel to set the Runtime Environment
        Property on a local or per-VM basis. This creates a local
        `deployment.properties`{.codeph} file. Deployers can also
        distribute an enterprise wide `deployment.properties`{.codeph}
        file by using the `deployment.config`{.codeph} mechanism.

    -   To set a property for a specific applet, use the HTML subtag
        `<PARAM>`{.codeph} \"java\_arguments\" within the
        `<APPLET>`{.codeph} tag.

    -   To set the property in a specific Java Web Start application or
        applet using Plugin2, use the JNLP `property`{.codeph} sub
        element of the `resources`{.codeph} element. See [resources
        Element](olink:JSDPG-GUID-F32AB01F-C9AF-4D7B-B9CB-66ACE2771846)
        in the <span><cite>Java Platform, Standard Edition Deployment
        Guide</cite></span>.

    </div>

</div>
</div>
<div class="sect3">
[]{#GUID-38CC6235-823B-49D7-A566-4BEA1B64C9C6}

### How to Specify a java.security.Security Property {#JSSEC-GUID-38CC6235-823B-49D7-A566-4BEA1B64C9C6 .sect3}

<div>
<div class="section">
You can customize some aspects of JSSE by setting Security Properties.
You can set a Security Property either statically or dynamically:

</div>
<!-- class="section" -->

-   <span>To set a Security Property statically, add a line to the
    security properties file. The security properties file is located at
    `java-home/conf/security/java.security`</span>

    <div>

    [<!-- -->]{#GUID-38CC6235-823B-49D7-A566-4BEA1B64C9C6__GUID-548CD27A-7959-4905-8A44-EA4F9CE36641}<span class="variable">java-home</span>
    :   See [Terms and
        Definitions](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329 "The following are commonly used cryptography terms and their definitions.")

    To specify a Security Property value in the security properties
    file, you add a line of the following form:

    ``` {.codeblock dir="ltr"}
    propertyName=propertyValue
    ```

    </div>
    <div>
    For example, suppose that you want to specify a different key
    manager factory algorithm name than the default SunX509. You do this
    by specifying the algorithm name as the value of a Security Property
    named `ssl.KeyManagerFactory.algorithm`{.codeph}. For example, to
    set the value to MyX509, add the following line to the security
    properties file:

    ``` {.codeblock dir="ltr"}
    ssl.KeyManagerFactory.algorithm=MyX509
    ```

    </div>
-   <span>To set a Security Property dynamically, call the
    `java.security.Security.setProperty`{.codeph} method in your
    code:</span>

    <div>
    ``` {.codeblock dir="ltr"}
    Security.setProperty("propertyName," "propertyValue");
    ```

    </div>
    <div>
    For example, a call to the `setProperty()`{.codeph} method
    corresponding to the previous example for specifying the key manager
    factory algorithm name would be:

    ``` {.codeblock dir="ltr"}
    Security.setProperty("ssl.KeyManagerFactory.algorithm", "MyX509");
    ```

    </div>

</div>
</div>
<div class="sect3">
[]{#GUID-F196CEDD-DC14-40EA-852A-133DB9BA798B}

### Customizing the X509Certificate Implementation {#JSSEC-GUID-F196CEDD-DC14-40EA-852A-133DB9BA798B .sect3}

<div>
The X509Certificate implementation returned by the
`X509Certificate.getInstance()`{.codeph} method is by default the
implementation from the JSSE implementation.

<div class="section">
To cause a different implementation to be returned:

</div>
<!-- class="section" -->

<div class="section">
Specify the name (and package) of the other implementation\'s class as
the value of a [How to Specify a java.security.Security
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-38CC6235-823B-49D7-A566-4BEA1B64C9C6)
named `cert.provider.x509v1`{.codeph}.

</div>
<!-- class="section" -->

<div class="example" id="GUID-F196CEDD-DC14-40EA-852A-133DB9BA798B__GUID-79B9F37D-F567-454A-AD1C-7CEDD90571EE">
For example, if the class is called `MyX509CertificateImpl`{.codeph} and
it appears in the `com.cryptox`{.codeph} package, then you should add
the following line to the security properties file:

``` {.codeblock dir="ltr"}
    cert.provider.x509v1=com.cryptox.MyX509CertificateImpl
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-D61663E8-2405-4B2D-A1F1-B8C7EA2688DB}

### Specifying Default Enabled Cipher Suites {#JSSEC-GUID-D61663E8-2405-4B2D-A1F1-B8C7EA2688DB .sect3}

<div>
You can specify the default enabled cipher suites in your application or
with the system properties `jdk.tls.client.cipherSuites`{.codeph} and
`jdk.tls.server.cipherSuites`{.codeph}.

<div class="infoboxnote" id="GUID-D61663E8-2405-4B2D-A1F1-B8C7EA2688DB__GUID-02A9D641-DC20-473E-8C89-6BBC11F59960">
Note:

The actual use of enabled cipher suites is restricted by algorithm
constraints.

</div>
The set of cipher suites to enable by default is determined by one of
the following ways in this order of preference:

1.  Explicitly set by application
2.  Specified by system property
3.  Specified by JSSE provider defaults

For example, explicitly setting the default enabled cipher suites in
your application overrides settings specified in
`jdk.tls.client.cipherSuites`{.codeph} or
`jdk.tls.server.cipherSuites`{.codeph} as well as JSSE provider
defaults.

<div class="section">
Explicitly Set by Application

You can set which cipher suites are enabled with one of the following
methods:

-   [<span class="apiname">SSLSocket.setEnabledCipherSuites(String\[\])</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLSocket.html#setEnabledCipherSuites-java.lang.String:A-)
-   [<span class="apiname">SSLEngine.setEnabledCipherSuites(String\[\])</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngine.html#setEnabledCipherSuites-java.lang.String:A-)
-   [<span class="apiname">SSLServerSocket.setEnabledCipherSuites(String\[\])</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLServerSocket.html#setEnabledCipherSuites-java.lang.String:A-)
-   [<span class="apiname">SSLParameters(String\[\]
    cipherSuites)</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#SSLParameters-java.lang.String:A-)
-   [<span class="apiname">SSLParameters(String\[\] cipherSuites,
    String\[\]
    protocols)</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#SSLParameters-java.lang.String:A-java.lang.String:A-)
-   [<span class="apiname">SSLParameters.setCipherSuites(String\[\])</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#setCipherSuites-java.lang.String:A-)
-   `https.cipherSuites`{.codeph} system property for
    [<span class="apiname">HttpsURLConnection</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/HttpsURLConnection.html)

</div>
<!-- class="section" -->

<div class="section">
Specified by System Property

The system property `jdk.tls.client.cipherSuites`{.codeph} specifies the
default enabled cipher suites on the client side;
`jdk.tls.server.cipherSuites`{.codeph} specifies those on the server
side.

The syntax of the value of these two system properties is a
comma-separated list of supported cipher suite names. Unrecognized or
unsupported cipher suite names that are specified in these properties
are ignored. See [Java Security Standard
Algorithms](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
for standard JSSE cipher suite names.

<div class="infoboxnote" id="GUID-D61663E8-2405-4B2D-A1F1-B8C7EA2688DB__GUID-7976F3A1-6661-423E-9226-61DCF6E45E1F">
Note:

These system properties are currently supported by Oracle JDK and
OpenJDK. They are not guaranteed to be supported by other JDK
implementations.

</div>
<div class="infoboxnote" id="GUID-D61663E8-2405-4B2D-A1F1-B8C7EA2688DB__GUID-0AD1FE03-21D2-45CF-9E2C-9CC06C8D6F5C">
Caution:

These system properties can be used to configure weak cipher suites, or
the configured cipher suites may be weak in the future. It is not
recommended that you use these system properties without understanding
the risks.

</div>
</div>
<!-- class="section" -->

<div class="section">
Specified by JSSE Provider Defaults

Each JSSE provider has its own default enabled cipher suites. See [The
SunJSSE
Provider](oracle-providers.htm#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2)
in [JDK Providers
Documentation](oracle-providers.htm#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313 "This document contains the technical details of the providers that are included in the JDK. It is assumed that readers have a strong understanding of the Java Cryptography Architecture and Provider Architecture.")
for the cipher suite names supported by the SunJSSE provider and which
ones that are enabled by default.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-7EBD6A94-9ADE-4321-8915-17B3763F8E77}

### Specifying an Alternative HTTPS Protocol Implementation {#JSSEC-GUID-7EBD6A94-9ADE-4321-8915-17B3763F8E77 .sect3}

<div>
You can communicate securely with an SSL-enabled web server by using the
HTTPS URL scheme for the `java.net.URL`{.codeph} class. The JDK provides
a default HTTPS URL implementation.

If you want an alternative HTTPS protocol implementation to be used, set
the `java.protocol.handler.pkgs`{.codeph} [How to Specify a
java.lang.System
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363)
to include the new class name. This action causes the specified classes
to be found and loaded before the JDK default classes. See the
[<span class="apiname">URL</span>](https://docs.oracle.com/javase/10/docs/api/java/net/URL.html)
class for details.

<div class="p">
<div class="infoboxnote" id="GUID-7EBD6A94-9ADE-4321-8915-17B3763F8E77__GUID-E9529FD8-897B-4783-8470-001332442275">
Note:

In past JSSE releases, you had to set the
`java.protocol.handler.pkgs`{.codeph} system property during JSSE
installation. This step is no longer required unless you want to obtain
an instance of `com.sun.net.ssl.HttpsURLConnection`{.codeph}.

</div>
</div>
</div>
</div>
<div class="sect3">
[]{#GUID-8BC473B2-CD64-4E8B-8136-80BB286091B1}

### Customizing the Provider Implementation {#JSSEC-GUID-8BC473B2-CD64-4E8B-8136-80BB286091B1 .sect3}

<div>
The JDK comes with a JSSE Cryptographic Service Provider, or
<span class="variable">provider</span> for short, named SunJSSE.
Providers are essentially packages that implement one or more engine
classes for specific cryptographic algorithms.

The JSSE engine classes are `SSLContext`{.codeph},
`KeyManagerFactory`{.codeph}, and `TrustManagerFactory`{.codeph}. See
[Java Cryptography Architecture (JCA) Reference
Guide](java-cryptography-architecture-jca-reference-guide.htm#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.")
to know more about providers and engine classes.

Before it can be used, a provider must be registered, either statically
or dynamically. You do not need to register the SunJSSE provider because
it is preregistered. If you want to use other providers, read the
following sections to see how to register them.

</div>
</div>
<div class="sect3">
[]{#GUID-59723547-D466-44C9-B066-EC5098B508E6}

### Registering the Cryptographic Provider Statically {#JSSEC-GUID-59723547-D466-44C9-B066-EC5098B508E6 .sect3}

<div>
<div class="section">
Register a provider statically by adding a line of the following form to
the security properties file,
`<java-home>/conf/security/java.security`{.codeph}:

``` {.codeblock dir="ltr"}
security.provider.n=provName|className 
```

This declares a provider, and specifies its preference order
`n`{.codeph}. The preference order is the order in which providers are
searched for requested algorithms when no specific provider is
requested. The order is 1-based; 1 is the most preferred, followed by 2,
and so on.

`provName`{.codeph} is the provider\'s name and `className`{.codeph} is
the fully qualified class name of the provider.

Standard security providers are automatically registered for you in the
`java.security`{.codeph} security properties file.

To use another JSSE provider, add a line registering the other provider,
giving it whatever preference order you prefer.

You can have more than one JSSE provider registered at the same time.
The registered providers may include different implementations for
different algorithms for different engine classes, or they may have
support for some or all of the same types of algorithms and engine
classes. When a particular engine class implementation for a particular
algorithm is searched for, if no specific provider is specified for the
search, then the providers are searched in preference order and the
implementation from the first provider that supplies an implementation
for the specified algorithm is used.

See [Step 8.1: Configure the
Provider](howtoimplaprovider.htm#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 "Register your provider so that the JCE framework can find your provider, either with the ServiceLoader class or in the class path or module path.")
in [Steps to Implement and Integrate a
Provider](howtoimplaprovider.htm#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:").

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-D5D3557F-069E-48CE-8586-94BCC2B0203A}

### Registering the Cryptographic Service Provider Dynamically {#JSSEC-GUID-D5D3557F-069E-48CE-8586-94BCC2B0203A .sect3}

<div>
Instead of registering a provider statically, you can add the provider
dynamically at runtime by calling either the
<span class="apiname">addProvider</span> or
<span class="apiname">insertProviderAt</span> method in the
<span class="apiname">Security</span> class. Note that this type of
registration is not persistent and can only be done by code which is
granted the `insertProvider.<provider name>`{.codeph} permission.

<div class="section">
See [Step 8.1: Configure the
Provider](howtoimplaprovider.htm#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 "Register your provider so that the JCE framework can find your provider, either with the ServiceLoader class or in the class path or module path.")
in [Steps to Implement and Integrate a
Provider](howtoimplaprovider.htm#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:").

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-9F841002-E08F-48A6-BC57-7D15DE6575DA}

### Provider Configuration {#JSSEC-GUID-9F841002-E08F-48A6-BC57-7D15DE6575DA .sect3}

<div>
Some providers may require configuration. This is done using the
`configure`{.codeph} method of the `Provider`{.codeph} class, prior to
calling the `addProvider`{.codeph} method of the `Security`{.codeph}
class. See [SunPKCS11
Configuration](pkcs11-reference-guide1.htm#GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9)
for an example. The `Provider.configure()`{.codeph} method is new to
Java SE 9.

</div>
</div>
<div class="sect3">
[]{#GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58}

### Configuring the Preferred Provider for Specific Algorithms {#JSSEC-GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58 .sect3}

<div>
Specify the preferred provider for a specific algorithm in the
`jdk.security.provider.preferred`{.codeph} Security Property. By
specifying a preferred provider you can configure providers that offer
performance gains for specific algorithms but are not the best
performing provider for other algorithms. The ordered provider list
specified using the `security.provider.n`{.codeph} property is not
sufficient to order providers that offer performance gains for specific
algorithms but are not the best performing provider for other
algorithms. More flexibility is required for configuring the ordering of
provider list to achieve performance gains.

<div class="section">
The `jdk.security.provider.preferred`{.codeph} Security Property allows
specific algorithms, or service types to be selected from a preferred
set of providers before accessing the list of registered providers. See
[How to Specify a java.security.Security
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-38CC6235-823B-49D7-A566-4BEA1B64C9C6).

The `jdk.security.provider.preferred`{.codeph} Security Property does
not register the providers. The ordered provider list must be
[Registering the Cryptographic Provider
Statically](java-secure-socket-extension-jsse-reference-guide.htm#GUID-59723547-D466-44C9-B066-EC5098B508E6)
using the `security.provider.n`{.codeph} property. Any provider that is
not registered is ignored.

</div>
<!-- class="section" -->

<div class="section">
Specifying the Preferred Provider for an Algorithm

The syntax for specifying the preferred providers string in the
`jdk.security.provider.preferred `{.codeph} Security Property is a
comma-separated list of `ServiceType.Algorithm:Provider`{.codeph}

In this syntax:

[<!-- -->]{#GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58__GUID-A708BC0D-1E9B-4CA3-B30A-3765E2E886EA}ServiceType

:   The name of the service type. (for example:
    `"MessageDigest"`{.codeph})ServiceType is optional. If it isn't
    specified, the algorithm applies to all service types.

[<!-- -->]{#GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58__GUID-B68E7DD5-A337-4754-9BB7-3D4D406A4AC0}Algorithm

:   The standard algorithm name. See [Java Security Standard Algorithm
    Names
    Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).
    Algorithms can be specified as full standard name,
    (AES/CBC/PKCS5Padding) or as partial (AES, AES/CBC,
    AES//PKCS5Padding).

[<!-- -->]{#GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58__GUID-92F5CD6E-C1BC-44A1-996F-9E00A0EDAC23}Provider

:   The name of the provider. Any provider that isn't listed in the
    registered list will be ignored. See [JDK
    Providers](oracle-providers.htm#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313 "This document contains the technical details of the providers that are included in the JDK. It is assumed that readers have a strong understanding of the Java Cryptography Architecture and Provider Architecture.").

Entries containing errors such as parsing errors are ignored. Use the
command `java -Djava.security.debug=jca`{.codeph} to debug errors.

</div>
<!-- class="section" -->

<div class="section">
Preferred Providers and FIPS

If you add a FIPS provider to the `security.provider.n`{.codeph}
property, and specify the preferred provider ordering in the
`jdk.security.provider.preferred`{.codeph} property then the preferred
providers specified in `jdk.security.provider.preferred `{.codeph} are
selected first.

Hence, it is recommended that you don't configure
`jdk.security.provider.preferred`{.codeph} property for FIPS provider
configurations.

</div>
<!-- class="section" -->

<div class="section">
jdk.security.provider.preferred Default Values

The `jdk.security.provider.preferred`{.codeph} property is not set by
default and is used only for application performance tuning.

</div>
<!-- class="section" -->

<div class="example" id="GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58__GUID-A00A625D-2596-41C8-BA38-21C71416A1B2">
Example 8-16 Sample jdk.security.provider.preferred Property

The syntax for specifying the
`jdk.security.provider.preferred `{.codeph} property is as follows:

`jdk.security.provider.preferred=AES/GCM/NoPadding:SunJCE, MessageDigest.SHA-256:SUN`{.codeph}

<div class="p">
In this syntax:

[<!-- -->]{#GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58__GUID-28C00AE0-A9A6-45AE-A743-823716638A8D}ServiceType
:   MessageDigest

[<!-- -->]{#GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58__GUID-205A4B26-295A-4488-8B2F-5E47C4219023}Algorithm
:   AES/GCM/NoPadding, SHA-256

[<!-- -->]{#GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58__GUID-05DD7678-1FFD-425E-AE6E-EAFD4619E880}Provider
:   SunJCE, SUN

</div>
</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150}

### Customizing the Default Keystores and Truststores, Store Types, and Store Passwords {#JSSEC-GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150 .sect3}

<div>
<div class="section">
Whenever a default `SSLSocketFactory`{.codeph} or
`SSLServerSocketFactory`{.codeph} is created (via a call to
`SSLSocketFactory.getDefault`{.codeph} or
`SSLServerSocketFactory.getDefault`{.codeph}), and this default
`SSLSocketFactory`{.codeph} (or `SSLServerSocketFactory`{.codeph}) comes
from the JSSE reference implementation, a default `SSLContext`{.codeph}
is associated with the socket factory. (The default socket factory will
come from the JSSE implementation.)

This default `SSLContext`{.codeph} is initialized with a default
`KeyManager`{.codeph} and a default `TrustManager`{.codeph}. If a
keystore is specified by the `javax.net.ssl.keyStore`{.codeph} system
property and an appropriate `javax.net.ssl.keyStorePassword`{.codeph}
system property (see [How to Specify a java.lang.System
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363)),
then the `KeyManager`{.codeph} created by the default
`SSLContext`{.codeph} will be a `KeyManager`{.codeph} implementation for
managing the specified keystore. (The actual implementation will be as
specified in [Customizing the Default Key Managers and Trust
Managers](java-secure-socket-extension-jsse-reference-guide.htm#GUID-0ACD9274-607C-49BE-AED9-BEE2B4F2BEF2).)
If no such system property is specified, then the keystore managed by
the `KeyManager`{.codeph} will be a new empty keystore.

Generally, the peer acting as the server in the handshake will need a
keystore for its KeyManager in order to obtain credentials for
authentication to the client. However, if one of the anonymous cipher
suites is selected, then the server\'s `KeyManager`{.codeph} keystore is
not necessary. And, unless the server requires client authentication,
the peer acting as the client does not need a `KeyManager`{.codeph}
keystore. Thus, in these situations it may be OK if no
`javax.net.ssl.keyStore`{.codeph} system property value is defined.

Similarly, if a truststore is specified by the
`javax.net.ssl.trustStore`{.codeph} system property, then the
`TrustManager`{.codeph} created by the default `SSLContext`{.codeph}
will be a `TrustManager`{.codeph} implementation for managing the
specified truststore. In this case, if such a property exists but the
file it specifies does not, then no truststore is used. If no
`javax.net.ssl.trustStore`{.codeph} property exists, then a default
truststore is searched for. If a truststore named
`java-home/lib/security/jssecacerts` is found, it is used. If not, then
a truststore named `java-home/lib/security/cacerts` is searched for and
used (if it exists). Finally, if a truststore is still not found, then
the truststore managed by the `TrustManager`{.codeph} will be a new
empty truststore.

<div class="infoboxnote" id="GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150__GUID-D83B4C21-5CFE-4043-B74A-0AE5D5EF9F1A">
Note:

The JDK ships with a limited number of trusted root certificates in the
`java-home/lib/security/cacerts` file. As documented in
[keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) in
<span id="GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150__JSWOR"><cite>Java
Platform, Standard Edition Tools Reference</cite></span>, it is your
responsibility to maintain (that is, add and remove) the certificates
contained in this file if you use this file as a truststore.

Depending on the certificate configuration of the servers that you
contact, you may need to add additional root certificates. Obtain the
needed specific root certificates from the appropriate vendor.

</div>
If the `javax.net.ssl.keyStoreType`{.codeph} and/or
`javax.net.ssl.keyStorePassword`{.codeph} system properties are also
specified, then they are treated as the default `KeyManager`{.codeph}
keystore type and password, respectively. If no type is specified, then
the default type is that returned by the
`KeyStore.getDefaultType()`{.codeph} method, which is the value of the
`keystore.type`{.codeph} Security Property, or \"jks\" if no such
Security Property is specified. If no keystore password is specified,
then it is assumed to be a blank string \"\".

Similarly, if the `javax.net.ssl.trustStoreType`{.codeph} and/or
`javax.net.ssl.trustStorePassword`{.codeph} system properties are also
specified, then they are treated as the default truststore type and
password, respectively. If no type is specified, then the default type
is that returned by the `KeyStore.getDefaultType()`{.codeph} method. If
no truststore password is specified, then it is assumed to be a blank
string \"\".

<div class="infoboxnote" id="GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150__GUID-C6D20FF5-6487-4F16-8A53-FC954900DDD1">
Note:

This section describes the current JSSE reference implementation
behavior. The system properties described in this section are not
guaranteed to continue to have the same names and types (system or
security) or even to exist at all in future releases. They are also not
guaranteed to be examined and used by any other JSSE implementations. If
they <span class="variable">are</span> examined by an implementation,
then that implementation should handle them in the same manner as the
JSSE reference implementation does, as described herein.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-0ACD9274-607C-49BE-AED9-BEE2B4F2BEF2}

### Customizing the Default Key Managers and Trust Managers {#JSSEC-GUID-0ACD9274-607C-49BE-AED9-BEE2B4F2BEF2 .sect3}

<div>
<div class="section">
As noted in [Customizing the Default Keystores and Truststores, Store
Types, and Store
Passwords](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150),
whenever a default `SSLSocketFactory`{.codeph} or
`SSLServerSocketFactory`{.codeph} is created, and this default
`SSLSocketFactory`{.codeph} (or `SSLServerSocketFactory`{.codeph}) comes
from the JSSE reference implementation, a default `SSLContext`{.codeph}
is associated with the socket factory.

This default `SSLContext`{.codeph} is initialized with a
`KeyManager`{.codeph} and a `TrustManager`{.codeph}. The
`KeyManager`{.codeph} and/or `TrustManager`{.codeph} supplied to the
default `SSLContext`{.codeph} will be an implementation for managing the
specified keystore or truststore, as described in the aforementioned
section.

The `KeyManager`{.codeph} implementation chosen is determined by first
examining the `ssl.KeyManagerFactory.algorithm`{.codeph} [Security
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-38CC6235-823B-49D7-A566-4BEA1B64C9C6).
If such a property value is specified, then a
`KeyManagerFactory`{.codeph} implementation for the specified algorithm
is searched for. The implementation from the first provider that
supplies an implementation is used. Its `getKeyManagers()`{.codeph}
method is called to determine the `KeyManager`{.codeph} to supply to the
default `SSLContext`{.codeph}. Technically, `getKeyManagers()`{.codeph}
returns an array of `KeyManager`{.codeph} objects, one
`KeyManager`{.codeph} for each type of key material. If no such Security
Property value is specified, then the default value of SunX509 is used
to perform the search.

<div class="p">
<div class="infoboxnote" id="GUID-0ACD9274-607C-49BE-AED9-BEE2B4F2BEF2__GUID-D15B5C94-B4CF-4B9F-8C02-998660542B84">
Note:

A `KeyManagerFactory`{.codeph} implementation for the SunX509 algorithm
is supplied by the SunJSSE provider. The `KeyManager`{.codeph} that it
specifies is a `javax.net.ssl.X509KeyManager`{.codeph} implementation.

</div>
</div>
Similarly, the `TrustManager`{.codeph} implementation chosen is
determined by first examining the
`ssl.TrustManagerFactory.algorithm`{.codeph} Security Property. If such
a property value is specified, then a `TrustManagerFactory`{.codeph}
implementation for the specified algorithm is searched for. The
implementation from the first provider that supplies an implementation
is used. Its `getTrustManagers()`{.codeph} method is called to determine
the `TrustManager`{.codeph} to supply to the default
`SSLContext`{.codeph}. Technically, `getTrustManagers()`{.codeph}
returns an array of `TrustManager`{.codeph} objects, one
`TrustManager`{.codeph} for each type of trust material. If no such
Security Property value is specified, then the default value of PKIX is
used to perform the search.

<div class="p">
<div class="infoboxnote" id="GUID-0ACD9274-607C-49BE-AED9-BEE2B4F2BEF2__GUID-F1C8A2E0-258D-4164-8DC7-51E303FD09D9">
Note:

A `TrustManagerFactory`{.codeph} implementation for the PKIX algorithm
is supplied by the SunJSSE provider. The `TrustManager`{.codeph} that it
specifies is a `javax.net.ssl.X509TrustManager`{.codeph} implementation.

</div>
</div>
<div class="p">
<div class="infoboxnote" id="GUID-0ACD9274-607C-49BE-AED9-BEE2B4F2BEF2__GUID-053952E0-5D14-45BF-897A-9C6A561DE975">
Note:

This section describes the current JSSE reference implementation
behavior. The system properties described in this section are not
guaranteed to continue to have the same names and types (system or
security) or even to exist at all in future releases. They are also not
guaranteed to be examined and used by any other JSSE implementations. If
they <span class="variable">are</span> examined by an implementation,
then that implementation should handle them in the same manner as the
JSSE reference implementation does, as described herein.

</div>
</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-0A438179-32A7-4900-A81C-29E3073E1E90}

### Disabled and Restricted Cryptographic Algorithms {#JSSEC-GUID-0A438179-32A7-4900-A81C-29E3073E1E90 .sect3}

<div>
In some environments, certain algorithms or key lengths may be
undesirable when using SSL/TLS/DTLS. The Oracle JDK uses the
`jdk.certpath.disabledAlgorithms`{.codeph} and
`jdk.tls.disabledAlgorithm`{.codeph} Security Properties to disable
algorithms during SSL/TLS/DTLS protocol negotiation, including version
negotiation, cipher suites selection, peer authentication, and key
exchange mechanisms. Note that these Security Properties are not
guaranteed to be used by other JDK implementations. See the
`<java-home>/conf/security/java.security` file for information about the
syntax of these Security Properties and their current active values.

<div class="section">
-   <span class="bold">`jdk.certpath.disabledAlgorithms`{.codeph}
    Property</span>: <span class="apiname">CertPath</span> code uses the
    `jdk.certpath.disabledAlgorithms`{.codeph} Security Property to
    determine which algorithms should not be allowed during
    <span class="apiname">CertPath</span> checking. For example, when a
    TLS Server sends an identifying certificate chain, a client
    <span class="apiname">TrustManager</span> that uses a
    <span class="apiname">CertPath</span> implementation to verify the
    received chain will not allow the stated conditions. For example,
    the following line blocks any MD2-based certificate, as well as SHA1
    TLSServer certificates that chain to trust anchors that are
    pre-installed in the `cacaerts` keystore. Likewise, this line blocks
    any RSA key less than 1024 bits.

    ``` {.oac_no_warn dir="ltr"}
    jdk.certpath.disabledAlgorithms=MD2, SHA1 jdkCA & usage TLSServer, RSA keySize < 1024
    ```

-   <span class="bold">`jdk.tls.disabledAlgorithms`{.codeph}
    Property</span>: <span class="apiname">SunJSSE</span> code uses the
    `jdk.tls.disabledAlgorithms`{.codeph} Security Property to disable
    SSL/TLS/DTLS protocols, cipher suites, keys, and so on. The syntax
    is similar to the `jdk.certpath.disabledAlgorithms`{.codeph}
    Security Property. For example, the following line disables the
    SSLv3 algorithm and all of the TLS\_\*\_RC4\_\* cipher suites:

    ``` {.oac_no_warn dir="ltr"}
    jdk.tls.disabledAlgorithms=SSLv3, RC4
    ```

If you require a particular condition, you can reactivate it by either
removing the associated value in the Security Property in the
`java.security` file or dynamically setting the proper Security Property
before JSSE is initialized.

Note that these Security Properties effectively create a third set of
cipher suites, Disabled. The following list describes these three sets:

-   <span class="bold">Disabled</span>: If a cipher suite contains any
    components (for example, RC4) on the disabled list (for example, RC4
    is specified in the `jdk.tls.disabledAlgorithms`{.codeph} Security
    Property), then that cipher suite is disabled and will
    <span class="bold">not</span> be considered for a connection
    handshake.

-   <span class="bold">Enabled</span>: A list of specific cipher suites
    that will be considered for a connection.

-   <span class="bold">Not Enabled</span>: A list of non-disabled cipher
    suites that will <span class="bold">not</span> be considered for a
    connection. To re-enable these cipher suites, call the appropriate
    <span class="apiname">setEnabledCipherSuites()</span> or
    <span class="apiname">setSSLParameters()</span> methods.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-316FB978-7588-442E-B829-B4973DB3B584}

### Customizing the Encryption Algorithm Providers {#JSSEC-GUID-316FB978-7588-442E-B829-B4973DB3B584 .sect3}

<div>
The SunJSSE provider uses the SunJCE implementation for all its
cryptographic needs. Although it is recommended that you leave the
provider at its regular position, you can use implementations from other
JCA or JCE providers by registering them
<span class="italic">before</span> the SunJCE provider.

<div class="section">
The standard JCA mechanism (see [How Provider Implementations Are
Requested and
Supplied](java-cryptography-architecture-jca-reference-guide.htm#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741))
can be used to configure providers, either statically via the security
properties file `<java-home>/conf/security/java.security`{.codeph}, or
dynamically via the `addProvider()`{.codeph} or
`insertProviderAt()`{.codeph} method in the
`java.security.Security`{.codeph} class.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-D9B216E8-3EFC-4882-B76E-17A87D8F2F9D}

### Customizing Size of Ephemeral Diffie-Hellman Keys {#JSSEC-GUID-D9B216E8-3EFC-4882-B76E-17A87D8F2F9D .sect3}

<div>
In SSL/TLS/DTLS connections, ephemeral Diffie-Hellman (DH) keys may be
used internally during the handshaking. The SunJSSE provider provides a
flexible approach to customize the strength of the ephemeral DH key size
during SSL/TLS/DTLS handshaking.

<div class="section">
Diffie-Hellman (DH) keys of sizes less than 1024 bits have been
deprecated because of their insufficient strength. You can customize the
ephemeral DH key size with the system property
`jdk.tls.ephemeralDHKeySize`{.codeph}. This system property does not
impact DH key sizes in `ServerKeyExchange`{.codeph} messages for
exportable cipher suites. It impacts only the DHE\_RSA, DHE\_DSS, and
DH\_anon-based cipher suites in the JSSE Oracle provider.

You can specify one of the following values for this property:

-   Undefined: A DH key of size 1024 bits will be used always for
    non-exportable cipher suites. This is the default value for this
    property.
-   `legacy`{.codeph}: The JSSE Oracle provider preserves the legacy
    behavior (for example, using ephemeral DH keys of sizes 512 bits and
    768 bits) of JDK 7 and earlier releases.
-   `matched`{.codeph}: For non-exportable anonymous cipher suites, the
    DH key size in ServerKeyExchange messages is 1024 bits. For X.509
    certificate based authentication (of non-exportable cipher suites),
    the DH key size matching the corresponding authentication key is
    used, except that the size must be between 1024 bits and 2048 bits.
    For example, if the public key size of an authentication certificate
    is 2048 bits, then the ephemeral DH key size should be 2048 bits
    unless the cipher suite is exportable. This key sizing scheme keeps
    the cryptographic strength consistent between authentication keys
    and key-exchange keys.
-   A valid integer between 1024 and 2048, inclusively: A fixed
    ephemeral DH key size of the specified value, in bits, will be used
    for non-exportable cipher suites.

The following table summaries the minimum and maximum acceptable DH key
sizes for each of the possible values for the system property
`jdk.tls.ephemeralDHKeySize`{.codeph}:

<div class="tblformal" id="GUID-D9B216E8-3EFC-4882-B76E-17A87D8F2F9D__GUID-16528793-4333-4BC2-928E-787DFD2C1BA2">
Table 8-9 DH Key Sizes for the System Property
`jdk.tls.ephemeralDHKeySize`{.codeph}

+-------------+-------------+-------------+-------------+-------------+
| Value of    | Undefined   | legacy      | matched     | Integer     |
| jdk.tls.eph |             |             |             | value       |
| emeralDHKey |             |             |             | (fixed)     |
| Size        |             |             |             |             |
+:============+:============+:============+:============+:============+
| Exportable  | 512         | 512         | 512         | 512         |
| DH key size |             |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Non-exporta | 1024        | 768         | 1024        | The fixed   |
| ble         |             |             |             | key size is |
| anonymous   |             |             |             | specified   |
| cipher      |             |             |             | by a valid  |
| suites      |             |             |             | integer     |
|             |             |             |             | property    |
|             |             |             |             | value,      |
|             |             |             |             | which must  |
|             |             |             |             | be between  |
|             |             |             |             | 1024 and    |
|             |             |             |             | 2048,       |
|             |             |             |             | inclusively |
|             |             |             |             | .           |
+-------------+-------------+-------------+-------------+-------------+
| Authenticat | 1024        | 768         | The key     | The fixed   |
| ion         |             |             | size is the | key size is |
| certificate |             |             | same as the | specified   |
|             |             |             | authenticat | by a valid  |
|             |             |             | ion         | integer     |
|             |             |             | certificate | property    |
|             |             |             | ,           | value,      |
|             |             |             | but must be | which must  |
|             |             |             | between     | be between  |
|             |             |             | 1024 bits   | 1024 and    |
|             |             |             | and 2048    | 2048,       |
|             |             |             | bits,       | inclusively |
|             |             |             | inclusively | .           |
|             |             |             | .           |             |
|             |             |             | However,    |             |
|             |             |             | the only DH |             |
|             |             |             | key size    |             |
|             |             |             | that the    |             |
|             |             |             | SunJCE      |             |
|             |             |             | provider    |             |
|             |             |             | supports    |             |
|             |             |             | that is     |             |
|             |             |             | larger than |             |
|             |             |             | 1024 bits   |             |
|             |             |             | is 2048     |             |
|             |             |             | bits.       |             |
|             |             |             |             |             |
|             |             |             | Consequentl |             |
|             |             |             | y,          |             |
|             |             |             | you may use |             |
|             |             |             | the values  |             |
|             |             |             | 1024 or     |             |
|             |             |             | 2048 only.  |             |
+-------------+-------------+-------------+-------------+-------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-41D5F11E-81BD-4C03-A315-48016D9B9B36}

### Customizing Maximum Fragment Length Negotiation (MFLN) Extension {#JSSEC-GUID-41D5F11E-81BD-4C03-A315-48016D9B9B36 .sect3}

<div>
In order to negotiate smaller maximum fragment lengths, clients have an
option to include an extension of type `max_fragment_length` in the
ClientHello message. A system property
`jsse.enableMFLNExtension`{.codeph}, can be used to enable or disable
the MFLN extension for SSL/TLS/DTLS.

<div class="section">
Maximum Fragment Length Negotiation

It may be desirable for constrained SSL/TLS/DTLS clients to negotiate a
smaller maximum fragment length due to memory limitations or bandwidth
limitations. In order to negotiate smaller maximum fragment lengths,
clients have an option to include an extension of type
`max_fragment_length` in the (extended) ClientHello message. See [RFC
6066](http://www.rfc-base.org/txt/rfc-6066.txt).

Once a maximum fragment length has been successfully negotiated, the
SSL/TLS/DTLS client and server can immediately begin fragmenting
messages (including handshake messages) to ensure that no fragment
larger than the negotiated length is sent.

</div>
<!-- class="section" -->

<div class="section">
System Property jsse.enableMFLNExtension

A system property `jsse.enableMFLNExtension`{.codeph} is defined to
enable or disable the MFLN extension. The
`jsse.enableMFLNExtension`{.codeph} is disabled by default.

The value of the system property can be set as follows:

<div class="tblformal" id="GUID-41D5F11E-81BD-4C03-A315-48016D9B9B36__GUID-A6CDBCFE-D1FB-4CF8-84A4-C764B31CB09F">
Table 8-10 jsse.enableMFLNExtension system property

  System Property                             Description
  ------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `jsse.enableMFLNExtension`{.codeph}=true    Enable the MFLN extension. If the returned value of `SSLParameters.getMaximumPacketSize()`{.codeph} is less than (2\^12 + header-size) the maximum fragment length negotiation extension would be enabled.  
  `jsse.enableMFLNExtension`{.codeph}=false   Disable the MFLN extension.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-3C9ADC85-E82C-421E-808D-F06028838F47}

### Configuring the Maximum and Minimum Packet Size {#JSSEC-GUID-3C9ADC85-E82C-421E-808D-F06028838F47 .sect3}

<div>
<div class="section">
Set the maximum expected network packet size in bytes for a SSL/TLS/DTLS
record with the
[<span class="apiname">SSLParameters.setMaximumPacketSize</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#setMaximumPacketSize-int-)
method.

It is recommended that the packet size should not be less than 256 bytes
so that small handshake messages, such as HelloVerifyRequests, are not
fragmented.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-9C767872-3A6C-4AD1-9805-49F112A0FA28}

Transport Layer Security (TLS) Renegotiation Issue {#JSSEC-GUID-9C767872-3A6C-4AD1-9805-49F112A0FA28 .sect2}
--------------------------------------------------

<div>
In the fall of 2009, a flaw was discovered in the SSL/TLS protocols. A
fix to the protocol was developed by the IETF TLS Working Group, and
current versions of the JDK contain this fix. This section describes the
situation in much more detail, along with interoperability issues when
communicating with older implementations that do not contain this
protocol fix.

The vulnerability allowed for man-in-the-middle (MITM) attacks where
chosen plain text could be injected as a prefix to a TLS connection.
This vulnerability did not allow an attacker to decrypt or modify the
intercepted network communication once the client and server have
successfully negotiated a session between themselves.

<div class="p">
Refer to the following links to know more about the SSL/TLS
vulnerability:

-   [CVE-2009-3555](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2009-3555)
    (posted on Mitre\'s [Common Vulnerabilities and Exposures
    List](http://cve.mitre.org/index.html), 2009)

-   [Understanding the TLS Renegotiation
    Attack](http://www.educatedguesswork.org/2009/11/understanding_the_tls_renegoti.html)
    (posted on Eric Rescorla\'s blog, [Educated
    Guesswork](http://www.educatedguesswork.org/), November 5, 2009).

</div>
</div>
<div class="sect3">
[]{#GUID-E41EDAB4-D1D7-4224-B3A4-E08D74E9CE04}

### Phased Approach to Fixing This Issue {#JSSEC-GUID-E41EDAB4-D1D7-4224-B3A4-E08D74E9CE04 .sect3}

<div>
The fix for this issue was handled in two phases:

-   Phase 1: Until a protocol fix could be developed, an interim fix
    that disabled SSL/TLS renegotiations by default was made available
    in the [March 30, 2010 Java SE and Java for Business Critical Patch
    Update](http://www.oracle.com/technetwork/topics/security/javacpumar2010-083341.html).

-   Phase 2: The [IETF](http://www.ietf.org/) issued [RFC
    5746](http://www.ietf.org/rfc/rfc5746.txt), which addresses the
    renegotiation protocol flaw. The following table lists the JDK and
    JRE releases that include the fix which implements RFC 5746 and
    supports secure renegotiation.

    <div class="tblformalwide" id="GUID-E41EDAB4-D1D7-4224-B3A4-E08D74E9CE04__GUID-4734C38B-9F4B-4041-B47B-61F7A2B6010E">
    Table 8-11 JDK and JRE Releases With Fixes to the TLS Renegotiation
    Issue

      JDK Family          Vulnerable Releases     Phase 1 Fix (Disable Renegotiations)   Phase 2 Fix (RFC 5746)
      ------------------- ----------------------- -------------------------------------- ------------------------
      JDK and JRE 6       Update 18 and earlier   Updates 19 through 21                  Update 22
      JDK and JRE 5.0     Update 23 and earlier   Updates 24 through 25                  Update 26
      JDK and JRE 1.4.2   Update 25 and earlier   Updates 26 through 27                  Update 28

    </div>
    <!-- class="inftblhruleinformal" -->

<div class="infoboxnote" id="GUID-E41EDAB4-D1D7-4224-B3A4-E08D74E9CE04__GUID-D0A74075-A522-4C5D-A5C7-CDE0FA9B2FA6">
Note:

Applications that do not require renegotiations are not affected by the
Phase 2 default configuration. However applications that require
renegotiations (for example, web servers that initially allow for
anonymous client browsing, but later require SSL/TLS authenticated
clients):

-   Are not affected if the peer is also compliant with RFC 5746
-   Are affected if the peer has not been upgraded to RFC 5746 (see next
    section for details)

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-475E6316-283A-4A59-9B11-2479348C4629}

### Description of the Phase 2 Fix {#JSSEC-GUID-475E6316-283A-4A59-9B11-2479348C4629 .sect3}

<div>
The SunJSSE implementation reenables renegotiations by default for
connections to peers compliant with RFC 5746. That is, both the client
and server <span class="bold">must support RFC 5746</span> in order to
securely renegotiate. SunJSSE provides some interoperability modes for
connections with peers that have not been upgraded, but users are
<span class="bold">strongly encouraged to update both their client and
server implementations as soon as possible</span>.

With the Phase 2 fix, SunJSSE has three renegotiation interoperability
modes. Each mode fully supports the RFC 5746 secure renegotiation, but
has these added semantics when communicating with a peer that has not
been upgraded:

-   <span class="bold">Strict mode</span>: Requires both client and
    server be upgraded to RFC 5746 and to send the proper RFC 5746
    messages. If not, the initial (or subsequent) handshaking will fail
    and the connection will be terminated.

-   <span class="bold">Interoperable mode (default)</span>: Use of the
    proper RFC 5746 messages is optional; however, legacy (original
    SSL/TLS specifications) renegotiations are disabled if the proper
    messages are not used. Initial legacy connections are still allowed,
    but legacy renegotiations are disabled. This is the best mix of
    security and interoperability, and is the default setting.

-   <span class="bold">Insecure mode</span>: Permits full legacy
    renegotiation. Most interoperable with legacy peers but vulnerable
    to the original MITM attack.

The three mode distinctions only affect a connection with a peer that
has not been upgraded. Ideally, strict (full RFC 5746) mode should be
used for all clients and servers; however, it will take some time for
all deployed SSL/TLS implementations to support RFC 5746, because the
interoperable mode is the current default.

The following table contains interoperability information about the
modes for various cases in which the client and/or server are either
updated to support RFC 5746 or not.

<div class="tblformal" id="GUID-475E6316-283A-4A59-9B11-2479348C4629__GUID-F981C4B4-2215-4468-B05E-FCACEA0948E5">
Table 8-12 Interoperability Information

+-----------------------+-----------------------+-----------------------+
| Client                | Server                | Mode                  |
+:======================+:======================+:======================+
| Updated               | Updated               | Secure renegotiation  |
|                       |                       | in all modes.         |
+-----------------------+-----------------------+-----------------------+
| Legacy[^Foot 5^](#GUI | Updated               | -   <span class="bold |
| D-475E6316-283A-4A59- |                       | ">Strict</span>       |
| 9B11-2479348C4629__LE |                       |     If clients do not |
| GACYMEANSTHEORIGINALS |                       |     send the proper   |
| SLTLSSPECIFI-F2073938 |                       |     RFC 5746          |
| ){#GUID-475E6316-283A |                       |     messages, then    |
| -4A59-9B11-2479348C46 |                       |     initial           |
| 29__LEGACYMEANSTHEORI |                       |     connections will  |
| GINALSSLTLSSPECIFI-F2 |                       |     immediately be    |
| 073938}               |                       |     terminated by the |
|                       |                       |     server            |
|                       |                       |     (`SSLHandshakeExc |
|                       |                       | eption`{.codeph}      |
|                       |                       |     or                |
|                       |                       |     `handshake_failur |
|                       |                       | e`{.codeph}).         |
|                       |                       | -   <span class="bold |
|                       |                       | ">Interoperable</span |
|                       |                       | >                     |
|                       |                       |     Initial           |
|                       |                       |     connections from  |
|                       |                       |     legacy clients    |
|                       |                       |     are allowed       |
|                       |                       |     (missing RFC 5746 |
|                       |                       |     messages), but    |
|                       |                       |     renegotiations    |
|                       |                       |     will not be       |
|                       |                       |     allowed by the    |
|                       |                       |     server.           |
|                       |                       |     [^Foot 6^](#GUID- |
|                       |                       | 475E6316-283A-4A59-9B |
|                       |                       | 11-2479348C4629__FOOT |
|                       |                       | NOTE2SUNJSSEPHASE1IMP |
|                       |                       | LEMENTATIO-66D60E1C){ |
|                       |                       | #GUID-475E6316-283A-4 |
|                       |                       | A59-9B11-2479348C4629 |
|                       |                       | __FOOTNOTE2SUNJSSEPHA |
|                       |                       | SE1IMPLEMENTATIO-66D6 |
|                       |                       | 0E1C}[^Foot 7^](#GUID |
|                       |                       | -475E6316-283A-4A59-9 |
|                       |                       | B11-2479348C4629__FN- |
|                       |                       | 13310-F207417D){#GUID |
|                       |                       | -475E6316-283A-4A59-9 |
|                       |                       | B11-2479348C4629__FN- |
|                       |                       | 13310-F207417D}       |
|                       |                       | -   <span class="bold |
|                       |                       | ">Insecure</span>     |
|                       |                       |     Connections and   |
|                       |                       |     renegotiations    |
|                       |                       |     with legacy       |
|                       |                       |     clients are       |
|                       |                       |     allowed, but are  |
|                       |                       |     vulnerable to the |
|                       |                       |     original MITM     |
|                       |                       |     attack.           |
+-----------------------+-----------------------+-----------------------+
| Updated               | Legacy                | -   <span class="bold |
|                       | [^Footref 5^](#fnsrc_ | ">Strict</span>       |
|                       | d108106e8427){#fnsrc_ |     If the server     |
|                       | d108106e8427}         |     does not respond  |
|                       |                       |     with the proper   |
|                       |                       |     RFC 5746          |
|                       |                       |     messages, then    |
|                       |                       |     the client will   |
|                       |                       |     immediately       |
|                       |                       |     terminate the     |
|                       |                       |     connection        |
|                       |                       |     (`SSLHandshakeExc |
|                       |                       | eption`{.codeph}      |
|                       |                       |     or                |
|                       |                       |     `handshake_failur |
|                       |                       | e`{.codeph}).         |
|                       |                       | -   <span class="bold |
|                       |                       | ">Interoperable</span |
|                       |                       | >                     |
|                       |                       |     Initial           |
|                       |                       |     connections from  |
|                       |                       |     legacy servers    |
|                       |                       |     are allowed       |
|                       |                       |     (missing RFC 5746 |
|                       |                       |     messages), but    |
|                       |                       |     renegotiations    |
|                       |                       |     will not be       |
|                       |                       |     allowed by the    |
|                       |                       |     server.           |
|                       |                       |     [^Footref 6^](#fn |
|                       |                       | src_d108106e8446){#fn |
|                       |                       | src_d108106e8446}[^Fo |
|                       |                       | otref 7^](#fnsrc_d108 |
|                       |                       | 106e8448){#fnsrc_d108 |
|                       |                       | 106e8448}             |
|                       |                       | -   <span class="bold |
|                       |                       | ">Insecure</span>     |
|                       |                       |     Connections and   |
|                       |                       |     renegotiations    |
|                       |                       |     with legacy       |
|                       |                       |     servers are       |
|                       |                       |     allowed, but are  |
|                       |                       |     vulnerable to the |
|                       |                       |     original MITM     |
|                       |                       |     attack.           |
+-----------------------+-----------------------+-----------------------+
| Legacy                | Legacy                | Existing SSL/TLS      |
| [^Footref 5^](#fnsrc_ | [^Footref 5^](#fnsrc_ | behavior, vulnerable  |
| d108106e8459){#fnsrc_ | d108106e8463){#fnsrc_ | to the MITM attack.   |
| d108106e8459}         | d108106e8463}         |                       |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

^Footnote 5^ \"Legacy\" means the original SSL/TLS specifications (that
is, <span class="italic">not</span> RFC 5746).

^Footnote 6^ SunJSSE Phase 1 implementations reject renegotiations
unless specifically reenabled. If renegotiations are reenabled, then
they will be treated as \"Legacy\" by the peer that is compliant with
RFC 5746, because they do not send the proper RFC 5746 messages.

^Footnote 7^ In SSL/TLS, renegotiations can be initiated by either side.
Like the Phase 1 fix, applications communicating with a peer that has
not been upgraded in Interoperable mode and that attempt to initiate
renegotiation (via `SSLSocket.startHandshake()`{.codeph} or
`SSLEngine.beginHandshake()`{.codeph}) will receive an
`SSLHandshakeException`{.codeph} (`IOException`{.codeph}) and the
connection will be shut down (`handshake_failure`{.codeph}).
Applications that receive a renegotiation request from a peer that has
not been upgraded will respond according to the type of connection in
place:

-   <span class="bold">TLSv1</span> A warning alert message of type
    `no_renegotiation(100)`{.codeph} will be sent to the peer and the
    connection will remain open. Older versions of SunJSSE will shut
    down the connection when a `no_renegotiation`{.codeph} alert is
    received.
-   <span class="bold">SSLv3</span> The application will receive an
    `SSLHandshakeException`{.codeph}, and the connection will be closed
    (`handshake_failure`{.codeph}). The `no_renegotiation`{.codeph}
    alert is not defined in the SSLv3 specification.

</p>
Set the mode with the the following system properties (see [How to
Specify a java.lang.System
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363)):

-   `sun.security.ssl.allowUnsafeRenegotiation`{.codeph} (introduced in
    Phase 1) controls whether legacy (unsafe) renegotiations are
    permitted.
-   `sun.security.ssl.allowLegacyHelloMessages`{.codeph} (introduced in
    Phase 2) allows the peer to perform the handshake process without
    requiring the proper RFC 5746 messages.

<div class="infoboxnote" id="GUID-475E6316-283A-4A59-9B11-2479348C4629__GUID-5FBCCBBE-47BB-41D5-A373-488EBFEA62D1">
Note:

The system properties
`sun.security.ssl.allowUnsafeRenegotiation`{.codeph} and
`sun.security.ssl.allowLegacyHelloMessages`{.codeph} are
<span>deprecated and might be removed in a future JDK release.</span>

</div>
<div class="tblformalwide" id="GUID-475E6316-283A-4A59-9B11-2479348C4629__GUID-A65FA5E7-2EC9-42E6-8B17-32922AB612EE">
Table 8-13 Values of the System Properties for Setting the
Interoperability Mode

  Mode                      allowLegacyHelloMessages   allowUnsafeRenegotiation
  ------------------------- -------------------------- --------------------------
  Strict                    false                      false
  Interoperable (default)   true                       false
  Insecure                  true                       true

</div>
<!-- class="inftblhruleinformal" -->

<div class="p">
<div class="infoboxnote" id="GUID-475E6316-283A-4A59-9B11-2479348C4629__GUID-52D3E6CB-CD6F-4444-950B-9F06417DE474">
Caution:

Do not reenable the insecure SSL/TLS renegotiation, as this would
reestablish the vulnerability.

</div>
</div>
</div>
</div>
<div class="sect3">
[]{#GUID-D2B6262D-B052-4757-9087-3CBD61B3CE8A}

### Workarounds and Alternatives to SSL/TLS Renegotiation {#JSSEC-GUID-D2B6262D-B052-4757-9087-3CBD61B3CE8A .sect3}

<div>
All peers should be updated to RFC 5746-compliant implementation as soon
as possible. Even with this RFC 5746 fix, communications with peers that
have not been upgraded will be affected if a renegotiation is necessary.
Here are a few suggested options:

-   <span class="bold">Restructure the peer to not require
    renegotiation.</span>

    Renegotiations are typically used by web servers that initially
    allow for anonymous client browsing but later require SSL/TLS
    authenticated clients, or that may initially allow weak cipher
    suites but later need stronger ones. The alternative is to require
    client authentication or strong cipher suites during the
    <span class="italic">initial</span> negotiation. There are a couple
    of options for doing so:

    -   If an application has a browse mode until a certain point is
        reached and a renegotiation is required, then you can
        restructure the server to eliminate the browse mode and require
        all initial connections be strong.

    -   Break the server into two entities, with the browse mode
        occurring on one entity, and using a second entity for the more
        secure mode. When the renegotiation point is reached, transfer
        any relevant information between the servers.

    Both of these options require a fair amount of work, but will not
    reopen the original security flaw.

-   <span class="bold">Set renegotiation interoperability mode to
    \"insecure\" using the system properties.</span>

    See [Description of the Phase 2
    Fix](java-secure-socket-extension-jsse-reference-guide.htm#GUID-475E6316-283A-4A59-9B11-2479348C4629 "The SunJSSE implementation reenables renegotiations by default for connections to peers compliant with RFC 5746. That is, both the client and server must support RFC 5746 in order to securely renegotiate. SunJSSE provides some interoperability modes for connections with peers that have not been upgraded, but users are strongly encouraged to update both their client and server implementations as soon as possible.").

</div>
</div>
<div class="sect3">
[]{#GUID-7CC1B0FD-BDCB-4F56-847D-D4FDDC7F8747}

### TLS Implementation Details {#JSSEC-GUID-7CC1B0FD-BDCB-4F56-847D-D4FDDC7F8747 .sect3}

<div>
RFC 5746 defines two new data structures, which are mentioned here for
advanced users

-   A pseudo-cipher suite called the Signaling Cipher Suite Value
    (SCSV), \"TLS\_EMPTY\_RENEGOTIATION\_INFO\_SCSV\"
-   A TLS extension called the Renegotiation Info (RI).

Either of these can be used to signal that an implementation is RFC
5746-compliant and can perform secure renegotiations. See [IETF email
discussion](http://www.ietf.org/mail-archive/web/tls/current/maillist.html)
from November 2009 to February 2010.

RFC 5746 enables clients to send either an SCSV or RI in the first
`ClientHello`{.codeph}. For maximum interoperability, SunJSSE uses the
SCSV by default, as a few TLS/SSL servers do not handle unknown
extensions correctly. The presence of the SCSV in the enabled cipher
suites (`SSLSocket.setEnabledCipherSuites()`{.codeph} or
`SSLEngine.setEnabledCipherSuites()`{.codeph}) determines whether the
SCSV is sent in the initial `ClientHello`{.codeph}, or if an RI should
be sent instead.

SSLv2 does not support SSL/TLS extensions. If the `SSLv2Hello`{.codeph}
protocol is enabled, then the SCSV is sent in the initial
`ClientHello`{.codeph}.

</div>
</div>
<div class="sect3">
[]{#GUID-67842028-3E8F-49E0-A0C1-63F480408412}

### Description of the Phase 1 Fix {#JSSEC-GUID-67842028-3E8F-49E0-A0C1-63F480408412 .sect3}

<div>
As previously mentioned, the Phase 1 Fix was to disable renegotiations
by default until a fix compliant with RFC 5746 could be developed.
Renegotiations could be reenabled by setting the
`sun.security.ssl.allowUnsafeRenegotiation`{.codeph} system property.
The Phase 2 fix uses the same
`sun.security.ssl.allowUnsafeRenegotiation`{.codeph} system property,
but also requires it to use RFC 5746 messages.

All applications should upgrade to the Phase 2 RFC 5746 fix as soon as
possible.

<div class="infoboxnote" id="GUID-67842028-3E8F-49E0-A0C1-63F480408412__GUID-6C8C7DEF-DDAA-4FDE-BFC0-541D0A1A57D2">
Note:

The system properties
`sun.security.ssl.allowUnsafeRenegotiation`{.codeph} and
`sun.security.ssl.allowLegacyHelloMessages`{.codeph} are
<span>deprecated and might be removed in a future JDK release.</span>

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-9A577D22-9DED-407E-9F16-5C006E3F3BF3}

### Allow Unsafe Server Certificate Change in SSL/TLS Renegotiations {#JSSEC-GUID-9A577D22-9DED-407E-9F16-5C006E3F3BF3 .sect3}

<div>
Server certificate change in an SSL/TLS renegotiation may be unsafe:

1.  If endpoint identification is not enabled in an SSL/TLS handshaking;
    and

2.  If the previous handshake is a session-resumption abbreviated
    initial handshake; and

3.  If the identities represented by both certificates can be regarded
    as different.

Two certificates can be considered to represent the same identity:

1.  If the subject alternative names of IP address are present in both
    certificates, they should be identical; otherwise,

2.  If the subject alternative names of DNS name are present in both
    certificates, they should be identical; otherwise,

3.  If the subject fields are present in both certificates, the
    certificate subjects and issuers should be identical.

Starting with JDK 8u25, unsafe server certificate change in SSL/TLS
renegotiations is not allowed by default. The new system property
`jdk.tls.allowUnsafeServerCertChange,`{.codeph} can be used to define
whether unsafe server certificate change in an SSL/TLS renegotiation
should be restricted or not.

The default value of this system property is \"false\".

<div class="infoboxnote" id="GUID-9A577D22-9DED-407E-9F16-5C006E3F3BF3__GUID-2F2A46F1-D6DE-4859-9354-2EA1DC375881">
Caution:

DO NOT set the system property to \"true\" unless it is really
necessary, as this would re-establish the unsafe server certificate
change vulnerability.

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-3151D7C3-7CE3-41B6-BF65-295B259C63A6}

Hardware Acceleration and Smartcard Support {#JSSEC-GUID-3151D7C3-7CE3-41B6-BF65-295B259C63A6 .sect2}
-------------------------------------------

<div>
<div class="section">
The Java Cryptography Architecture (JCA) is a set of packages that
provides a framework and implementations for encryption, key generation
and key agreement, and message authentication code (MAC) algorithms.
(See [Java Cryptography Architecture (JCA) Reference
Guide](java-cryptography-architecture-jca-reference-guide.htm#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.").)
The SunJSSE provider uses JCA exclusively for all of its cryptographic
operations and can automatically take advantage of JCE features and
enhancements, including JCA\'s support for RSA
[PKCS\#11](http://www.emc.com/emc-plus/rsa-labs/standards-initiatives/pkcs-11-cryptographic-token-interface-standard.htm).
This support enables the SunJSSE provider to use hardware cryptographic
accelerators for significant performance improvements and to use
smartcards as keystores for greater flexibility in key and trust
management. .

Use of hardware cryptographic accelerators is automatic if JCA has been
configured to use the Oracle PKCS\#11 provider, which in turn has been
configured to use the underlying accelerator hardware. The provider must
be configured before any other JCA providers in the provider list. For
details on how to configure the Oracle PKCS\#11 provider, see [PKCS\#11
Reference
Guide](pkcs11-reference-guide1.htm#GUID-30E98B63-4910-40A1-A6DD-663EAF466991).

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-3412BD4D-9B6F-4FF0-A11C-ABA5945B40AE}

### Configuring JSSE to Use Smartcards as Keystores and Truststores {#JSSEC-GUID-3412BD4D-9B6F-4FF0-A11C-ABA5945B40AE .sect3}

<div>
Support for PKCS\#11 in JCA also enables access to smartcards as a
keystore. For details on how to configure the type and location of the
keystores to be used by JSSE, see [Customizing
JSSE](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9 "JSSE includes a standard implementation that can be customized by plugging in different implementations or specifying the default keystore, and so on.").
To use a smartcard as a keystore or truststore, set the
`javax.net.ssl.keyStoreType`{.codeph} and
`javax.net.ssl.trustStoreType`{.codeph} system properties, respectively,
to `pkcs11`{.codeph}, and set the `javax.net.ssl.keyStore`{.codeph} and
`javax.net.ssl.trustStore`{.codeph} system properties, respectively, to
`NONE`{.codeph}. To specify the use of a specific provider, use the
`javax.net.ssl.keyStoreProvider`{.codeph} and
`javax.net.ssl.trustStoreProvider`{.codeph} system properties (for
example, set them to `SunPKCS11-joe`{.codeph}). By using these
properties, you can configure an application that previously depended on
these properties to access a file-based keystore to use a smartcard
keystore with no changes to the application.

Some applications request the use of keystores programmatically. These
applications can continue to use the existing APIs to instantiate a
`Keystore`{.codeph} and pass it to its key manager and trust manager. If
the `Keystore`{.codeph} instance refers to a PKCS\#11 keystore backed by
a Smartcard, then the JSSE application will have access to the keys on
the smartcard.

</div>
</div>
<div class="sect3">
[]{#GUID-C236C41B-54CA-4095-986B-7C62BBC419FB}

### Multiple and Dynamic Keystores {#JSSEC-GUID-C236C41B-54CA-4095-986B-7C62BBC419FB .sect3}

<div>
Smartcards (and other removable tokens) have additional requirements for
an `X509KeyManager`{.codeph}. Different smartcards can be present in a
smartcard reader during the lifetime of a Java application, and they can
be protected using different passwords.

The
[`KeyStore.Builder`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/KeyStore.Builder.html)
class abstracts the construction and initialization of a
`KeyStore`{.codeph} object. It supports the use of
`CallbackHandler`{.codeph} for password prompting, and its subclasses
can be used to support additional features as desired by an application.
For example, it is possible to implement a `Builder`{.codeph} that
allows individual `KeyStore`{.codeph} entries to be protected with
different passwords. The
[`KeyStoreBuilderParameters`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/KeyStoreBuilderParameters.html)
class then can be used to initialize a `KeyManagerFactory`{.codeph}
using one or more of these `Builder`{.codeph} objects.

A `X509KeyManager`{.codeph} implementation in the SunJSSE provider
called NewSunX509 supports these parameters. If multiple certificates
are available, it attempts to pick a certificate with the appropriate
key usage and prefers valid to expired certificates.

[Example
8-17](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C236C41B-54CA-4095-986B-7C62BBC419FB__IMPORTJAVAX.NET.SSL.IMPORTJAVA.SECU-6B0B77DA)
illustrates how to tell JSSE to use both a PKCS\#11 keystore (which
might in turn use a smartcard) and a PKCS\#12 file-based keystore.

<div class="example" id="GUID-C236C41B-54CA-4095-986B-7C62BBC419FB__IMPORTJAVAX.NET.SSL.IMPORTJAVA.SECU-6B0B77DA">
Example 8-17 Sample Code to Use PKCS\#11 and PKCS\#12 File-based
Keystore

``` {.codeblock dir="ltr"}
import javax.net.ssl.*;
import java.security.KeyStore.*;
// ...

// Specify keystore builder parameters for PKCS#11 keystores
Builder scBuilder = Builder.newInstance("PKCS11", null,
    new CallbackHandlerProtection(myGuiCallbackHandler));

// Specify keystore builder parameters for a specific PKCS#12 keystore
Builder fsBuilder = Builder.newInstance("PKCS12", null,
    new File(pkcsFileName), new PasswordProtection(pkcsKsPassword));

// Wrap them as key manager parameters
ManagerFactoryParameters ksParams = new KeyStoreBuilderParameters(
    Arrays.asList(new Builder[] { scBuilder, fsBuilder }) );

// Create KeyManagerFactory
KeyManagerFactory factory = KeyManagerFactory.getInstance("NewSunX509");

// Pass builder parameters to factory
factory.init(ksParams);

// Use factory
SSLContext ctx = SSLContext.getInstance("TLS");
ctx.init(factory.getKeyManagers(), null, null);
```

</div>
<!-- class="example" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-67227445-EE66-4F33-BEED-535C548BCC73}

Kerberos Cipher Suites {#JSSEC-GUID-67227445-EE66-4F33-BEED-535C548BCC73 .sect2}
----------------------

<div>
<div class="p">
The SunJSSE provider has support for Kerberos cipher suites, as
described in [RFC 2712](http://www.ietf.org/rfc/rfc2712.txt). The
following cipher suites are supported but not enabled by default:

<div class="infoboxnote" id="GUID-67227445-EE66-4F33-BEED-535C548BCC73__GUID-A953A5B9-1424-47E2-AFF0-3D08183C0634">
Note:

According to [DTLS Version 1.0](http://tools.ietf.org/html/rfc4347) and
[DTLS Version 1.2](http://tools.ietf.org/html/rfc6347), RC4 cipher
suites must not be used with DTLS.

</div>
</div>
-   TLS\_KRB5\_WITH\_RC4\_128\_SHA
-   TLS\_KRB5\_WITH\_RC4\_128\_MD5
-   TLS\_KRB5\_WITH\_3DES\_EDE\_CBC\_SHA
-   TLS\_KRB5\_WITH\_3DES\_EDE\_CBC\_MD5
-   TLS\_KRB5\_WITH\_DES\_CBC\_SHA
-   TLS\_KRB5\_WITH\_DES\_CBC\_MD5
-   TLS\_KRB5\_EXPORT\_WITH\_RC4\_40\_SHA
-   TLS\_KRB5\_EXPORT\_WITH\_RC4\_40\_MD5
-   TLS\_KRB5\_EXPORT\_WITH\_DES\_CBC\_40\_SHA
-   TLS\_KRB5\_EXPORT\_WITH\_DES\_CBC\_40\_MD5

To enable the use of these cipher suites, you must do so explicitly. See
the API documentation for
[`SSLEngine.setEnabledCipherSuites(String[])`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngine.html#setEnabledCipherSuites-java.lang.String:A-)
and
[`SSLSocket.setEnabledCipherSuites(String[])`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLSocket.html#setEnabledProtocols-java.lang.String:A-)
methods. As with all other SSL/TLS/DTLS cipher suites, if a cipher suite
is not supported by the peer, then it will not be selected during cipher
negotiation. Furthermore, if the application and/or server cannot
acquire the necessary Kerberos credentials, then the Kerberos cipher
suites also will not be selected.

The following is an example of a TLS client that will only use the
`TLS_KRB5_WITH_DES_CBC_SHA`{.codeph} cipher suite:

``` {.codeblock dir="ltr"}
// Create socket
SSLSocketFactory sslsf = (SSLSocketFactory) SSLSocketFactory.getDefault();
SSLSocket sslSocket = (SSLSocket) sslsf.createSocket(tlsServer, serverPort);

// Enable only one cipher suite
String enabledSuites[] = { "TLS_KRB5_WITH_DES_CBC_SHA" };
sslSocket.setEnabledCipherSuites(enabledSuites);
```

</div>
<div class="sect3">
[]{#GUID-2CEBB012-B3E0-44FB-B935-8A95E184AF84}

### Kerberos Requirements {#JSSEC-GUID-2CEBB012-B3E0-44FB-B935-8A95E184AF84 .sect3}

<div>
You must have the Kerberos infrastructure set up in your deployment
environment before you can use the Kerberos cipher suites with JSSE. In
particular, both the TLS client and server must have accounts set up
with the Kerberos Key Distribution Center (KDC). At runtime, if one or
more of the Kerberos cipher suites have been enabled, then the TLS
client and server will acquire their Kerberos credentials associated
with their respective account from the KDC. For example, a TLS server
running on the machine `mach1.imc.org`{.codeph} in the Kerberos realm
`IMC.ORG`{.codeph} must have an account with the name
`host/mach1.imc.org@IMC.ORG`{.codeph} and be configured to use the KDC
for `IMC.ORG`{.codeph}. See [Kerberos
Requirements](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html).

An application can acquire its Kerberos credentials by using the [Java
Authentication and Authorization Service (JAAS) Reference
Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html)
and a Kerberos login module. The JDK comes with a
[<span class="apiname">Krb5LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/Krb5LoginModule.html).
You can use the Kerberos cipher suites with JSSE with or without JAAS
programming, similar to how you can use the [JAAS and Java GSS-API
Tutorial](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/BasicClientServer.html)
with or without JAAS programming.

To use the Kerberos cipher suites with JSSE without JAAS programming,
you must use the index names `com.sun.net.ssl.server`{.codeph} or
`other`{.codeph} for the TLS server JAAS configuration entry, and
`com.sun.net.ssl.client`{.codeph} or `other`{.codeph} for the TLS
client, and set the `javax.security.auth.useSubjectCredsOnly`{.codeph}
system property to false. For example, a TLS server that is not using
JAAS programming might have the following JAAS configuration file:

``` {.codeblock dir="ltr"}
com.sun.net.ssl.server {
  com.sun.security.auth.module.Krb5LoginModule required
    principal="host/mach1.imc.org@IMC.ORG"
    useKeyTab=true
    keyTab=mach1.keytab
    storeKey=true;
};
```

An example of how to use Java GSS and Kerberos without JAAS programming
is described in the tutorial [Use of Java GSS-API for Secure Message
Exchanges Without JAAS
Programming](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/BasicClientServer.html)
in the JDK 8 documentation. You can adapt it to use JSSE by replacing
Java GSS calls with JSSE calls.

To use the Kerberos cipher suites with JAAS programming, you can use any
index name because your application is responsible for creating the JAAS
`LoginContext`{.codeph} using the index name, and then wrapping the JSSE
calls inside of a `Subject.doAs()`{.codeph} or
`Subject.doAsPrivileged()`{.codeph} call. An example of how to use JAAS
with Java GSS and Kerberos is described in the tutorial [Use of JAAS
Login Utility and Java GSS-API for Secure Message
Exchange](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/ClientServer.html)
in the JDK 8 documentation. You can adapt it to use JSSE by replacing
Java GSS calls with JSSE calls.

If you have trouble using or configuring the JSSE application to use
Kerberos, see
[Troubleshooting](troubleshooting.htm#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE)
in [Introduction to JAAS and Java GSS-API
Tutorials](introduction-jaas-and-java-gss-api-tutorials1.htm).

</div>
</div>
<div class="sect3">
[]{#GUID-3D49787E-4D31-4D65-8FFE-CE19B6CAD3E2}

### Peer Identity Information {#JSSEC-GUID-3D49787E-4D31-4D65-8FFE-CE19B6CAD3E2 .sect3}

<div>
To determine the identity of the peer of an SSL/TLS/DTLS connection, use
the `getPeerPrincipal()`{.codeph} method in the following classes:

-   `javax.net.ssl.SSLSession`{.codeph}
-   `javax.net.ssl.HttpsURLConnection`{.codeph}
-   `javax.net.HandshakeCompletedEvent`{.codeph}

Similarly, to get the identity that was sent to the peer (to identify
the local entity), use the `getLocalPrincipal()`{.codeph} method in
these classes. For X509-based cipher suites, these methods will return
an instance of `javax.security.auth.x500.X500Principal`{.codeph}; for
Kerberos cipher suites, these methods will return an instance of
`javax.security.auth.kerberos.KerberosPrincipal`{.codeph}.

JSSE applications use `getPeerCertificates()`{.codeph} and similar
methods in `javax.net.ssl.SSLSession`{.codeph},
`javax.net.ssl.HttpsURLConnection`{.codeph}, and
`javax.net.HandshakeCompletedEvent`{.codeph} classes to obtain
information about the peer. When the peer does not have any
certificates, `SSLPeerUnverifiedException`{.codeph} is thrown.

If the application must determine only the identity of the peer or
identity sent to the peer, then it should use the
`getPeerPrincipal()`{.codeph} and `getLocalPrincipal()`{.codeph}
methods, respectively. It should use `getPeerCertificates()`{.codeph}
and `getLocalCertificates()`{.codeph} methods only if it must examine
the contents of those certificates. Furthermore, the application must be
prepared to handle the case where an authenticated peer might not have
any certificate.

</div>
</div>
<div class="sect3">
[]{#GUID-B583D760-8D38-4B3F-94FA-66E63AFCE1D1}

### Security Manager {#JSSEC-GUID-B583D760-8D38-4B3F-94FA-66E63AFCE1D1 .sect3}

<div>
When the security manager has been enabled, in addition to the
`SocketPermission`{.codeph} needed to communicate with the peer, a TLS
client application that uses the Kerberos cipher suites also needs the
following permission:

``` {.codeblock dir="ltr"}
javax.security.auth.kerberos.ServicePermission(serverPrincipal, "initiate");
```

Where,

[<!-- -->]{#GUID-B583D760-8D38-4B3F-94FA-66E63AFCE1D1__GUID-7ACB5C9F-BD18-47F8-AD59-CB37742F880F}<span class="variable">serverPrincipal</span>
:   Indicates the Kerberos principal name of the TLS server that the TLS
    client will be communicating with (such as
    `host/mach1.imc.org@IMC.ORG`{.codeph}).

A TLS server application needs the following permission:

``` {.codeblock dir="ltr"}
javax.security.auth.kerberos.ServicePermission(serverPrincipal, "accept");
```

Where,

[<!-- -->]{#GUID-B583D760-8D38-4B3F-94FA-66E63AFCE1D1__GUID-94BF5580-BBC5-45C3-AF32-5BFBA7B55261}<span class="variable">serverPrincipal</span>
:   Indicates the Kerberos principal name of the TLS server (such as
    `host/mach1.imc.org@IMC.ORG`{.codeph}).

If the server or client must contact the KDC (for example, if its
credentials are not cached locally), then it also needs the following
permission:

``` {.codeblock dir="ltr"}
javax.security.auth.kerberos.ServicePermission(tgtPrincipal, "initiate");
```

Where,

[<!-- -->]{#GUID-B583D760-8D38-4B3F-94FA-66E63AFCE1D1__GUID-CDD53994-5190-4630-A507-9F194840954E}<span class="italic">tgtPrincipal</span>
:   Indicates the principal name of the KDC (such as
    `krbtgt/IMC.ORG@IMC.ORG`{.codeph}).

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-93EBE6F4-1460-450A-8D9C-AF086C233BDF}

Additional Keystore Formats (PKCS12) {#JSSEC-GUID-93EBE6F4-1460-450A-8D9C-AF086C233BDF .sect2}
------------------------------------

<div>
The [PKCS\#12 (Personal Information Exchange Syntax
Standard)](http://www.emc.com/emc-plus/rsa-labs/standards-initiatives/pkcs12-personal-information-exchange-syntax-standard.htm)
specifies a portable format for storage and/or transport of a user\'s
private keys, certificates, miscellaneous secrets, and other items. The
SunJSSE provider supplies a complete implementation of the PKCS12
`java.security.KeyStore`{.codeph} format for reading and writing PKCS12
files. This format is also supported by other toolkits and applications
for importing and exporting keys and certificates, such as Mozilla
Firefox, Microsoft Internet Explorer, and OpenSSL. For example, these
implementations can export client certificates and keys into a file
using the .p12 file name extension.

With the SunJSSE provider, you can access PKCS12 keys through the
`KeyStore`{.codeph} API with a keystore type of PKCS12. In addition, you
can list the installed keys and associated certificates by using the
`keytool`{.codeph} command with the `-storetype`{.codeph} option set to
`pkcs12`{.codeph}. See
[keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) in
<span id="GUID-93EBE6F4-1460-450A-8D9C-AF086C233BDF__JSWOR"><cite>Java
Platform, Standard Edition Tools Reference</cite></span>.

</div>
</div>
<div class="sect2">
[]{#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F}

Server Name Indication (SNI) Extension {#JSSEC-GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F .sect2}
--------------------------------------

<div>
The SNI extension is a feature that extends the SSL/TLS/DTLS protocols
to indicate what server name the client is attempting to connect to
during handshaking. Servers can use server name indication information
to decide if specific `SSLSocket`{.codeph} or `SSLEngine`{.codeph}
instances should accept a connection. For example, when multiple virtual
or name-based servers are hosted on a single underlying network address,
the server application can use SNI information to determine whether this
server is the exact server that the client wants to access. Instances of
this class can be used by a server to verify the acceptable server names
of a particular type, such as host names. See section 3 of [TLS
Extensions (RFC 6066)](http://www.ietf.org/rfc/rfc6066.txt).

Developers of client applications can explicitly set the server name
indication using the
`SSLParameters.setServerNames(List<SNIServerName> serverNames)`{.codeph}
method. See [Example
8-18](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F__GUID-B5160B29-A377-41C0-A60D-4A3E0C89CCAF).

Developers of server applications can use the `SNIMatcher`{.codeph}
class to decide how to recognize server name indication. [Example
8-19](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F__GUID-6EACE6B2-E1A4-4A8B-82B1-7C122495CF0D)
and [Example
8-20](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F__GUID-E25CEBA5-2D07-484C-82EB-D280E32F7D08)
illustrate this functionality:

<div class="example" id="GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F__GUID-B5160B29-A377-41C0-A60D-4A3E0C89CCAF">
Example 8-18 Sample Code to Set the Server Name Indication

The following code sample illustrates how to set the server name
indication using the method
<span class="apiname">SSLParameters.setServerNames(List\<SNIServerName\>
serverNames)</span>:

``` {.oac_no_warn dir="ltr"}
SSLSocketFactory factory = ...
SSLSocket sslSocket = factory.createSocket("172.16.10.6", 443);
// SSLEngine sslEngine = sslContext.createSSLEngine("172.16.10.6", 443);

SNIHostName serverName = new SNIHostName("www.example.com");
List<SNIServerName> serverNames = new ArrayList<>(1);
serverNames.add(serverName);

SSLParameters params = sslSocket.getSSLParameters();
params.setServerNames(serverNames);
sslSocket.setSSLParameters(params);
// sslEngine.setSSLParameters(params);
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F__GUID-6EACE6B2-E1A4-4A8B-82B1-7C122495CF0D">
Example 8-19 Sample Code Using SSLSocket Class to Recognize SNI

The following code sample illustrates how the server applications can
use the `SNIMatcher`{.codeph} class to decide how to recognize server
name indication:

``` {.codeblock dir="ltr"}
SSLSocket sslSocket = sslServerSocket.accept();

SNIMatcher matcher = SNIHostName.createSNIMatcher("www\\.example\\.(com|org)");
Collection<SNIMatcher> matchers = new ArrayList<>(1);
matchers.add(matcher);

SSLParameters params = sslSocket.getSSLParameters();
params.setSNIMatchers(matchers);
sslSocket.setSSLParameters(params);
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F__GUID-E25CEBA5-2D07-484C-82EB-D280E32F7D08">
Example 8-20 Sample Code Using SSLServerSocket Class to Recognize SNI

The following code sample illustrates how the server applications can
use the `SNIMatcher`{.codeph} class to decide how to recognize server
name indication:

``` {.codeblock dir="ltr"}
 
SSLServerSocket sslServerSocket = ...;

SNIMatcher matcher = SNIHostName.createSNIMatcher("www\\.example\\.(com|org)");
Collection<SNIMatcher> matchers = new ArrayList<>(1);
matchers.add(matcher);

SSLParameters params = sslServerSocket.getSSLParameters();
params.setSNIMatchers(matchers);
sslServerSocket.setSSLParameters(params);

SSLSocket sslSocket = sslServerSocket.accept();
```

</div>
<!-- class="example" -->

<div class="section">
The following list provides examples for the behavior of the
`SNIMatcher`{.codeph} when receiving various server name indication
requests in the ClientHello message:

-   Matcher configured to `www\\.example\\.com`{.codeph}:

    -   If the requested host name is `www.example.com`{.codeph}, then
        it will be accepted and a confirmation will be sent in the
        ServerHello message.
    -   If the requested host name is `www.example.org`{.codeph}, then
        it will be rejected with an `unrecognized_name`{.codeph} fatal
        error.
    -   If there is no requested host name or it is empty, then the
        request will be accepted but no confirmation will be sent in the
        ServerHello message.

-   Matcher configured to `www\\.invalid\\.com`{.codeph}:

    -   If the requested host name is `www.example.com`{.codeph}, then
        it will be rejected with an `unrecognized_name`{.codeph} fatal
        error.
    -   If the requested host name is `www.example.org`{.codeph}, then
        it will be accepted and a confirmation will be sent in the
        ServerHello message.
    -   If there is no requested host name or it is empty, then the
        request will be accepted but no confirmation will be sent in the
        ServerHello message.

-   Matcher is not configured:

    Any requested host name will be accepted but no confirmation will be
    sent in the ServerHello message.

For descriptions of new classes that implement the SNI extension, see:

-   [The StandardConstants
    Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-651B5070-F586-4504-A6CD-8BEB2D928D47 "The StandardConstants class is used to represent standard constants definitions in JSSE.")
-   [The SNIServerName
    Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-ADD484B7-244A-4FBC-AEF0-96873890CD6B)
-   [The SNIMatcher
    Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-073F0493-3DB8-4388-818B-83E92021EF45)
-   [The SNIHostName
    Class](java-secure-socket-extension-jsse-reference-guide.htm#GUID-E10158C4-E808-41B7-9958-A119927743D8)

For examples, see [Using the Server Name Indication (SNI)
Extension](java-secure-socket-extension-jsse-reference-guide.htm#GUID-63945B45-E909-483F-B3A9-E26586737383).

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-DC583ED6-06AD-435C-BC9C-763F4642B2B3}

TLS Application Layer Protocol Negotiation {#JSSEC-GUID-DC583ED6-06AD-435C-BC9C-763F4642B2B3 .sect2}
------------------------------------------

<div>
Negotiate an application protocol for a TLS connection with Application
Layer Protocol Negotiation (ALPN).

<div class="section">
What is ALPN?

Some applications might want or need to negotiate a shared application
level value before a TLS handshake has completed. For example, HTTP/2
uses the Application Layer Protocol Negotiation mechanism to help
establish which HTTP version (\"h2\", \"spdy/3\", \"http/1.1\") can or
will be used on a particular TCP or UDP port. ALPN ([RFC
7301](https://www.rfc-editor.org/rfc/rfc7301.txt)) does this without
adding network round-trips between the client and the server. In the
case of HTTP/2 the protocol must be established before the connection is
negotiated, as client and server need to know what version of HTTP to
use before they start communicating. Without ALPN it would not be
possible to have application protocols HTTP/1 and HTTP/2 on the same
port.

The client uses the ALPN extension at the beginning of the TLS handshake
to send a list of supported application protocols to the server as part
of the `ClientHello`{.codeph}. The server reads the list of supported
application protocols in the `ClientHello`{.codeph}, and determines
which of the supported protocols it prefers. It then sends a
`ServerHello`{.codeph} message back to the client with the negotiation
result. The message may contain either the name of the protocol that has
been chosen or that no protocol has been chosen.

The application protocol negotiation can thus be accomplished within the
TLS handshake, without adding network round-trips, and allows the server
to associate a different certificate with each application protocol, if
desired.

Unlike many other TLS extensions, this extension does not establish
properties of the session, only of the connection. That\'s why you\'ll
find the negotiated values in the
`SSLSocket`{.codeph}/`SSLEngine`{.codeph}, not the
`SSLSession`{.codeph}. When session resumption or session tickets are
used (see [TLS Session Resumption without Server-Side
State](http://www.rfc-editor.org/rfc/rfc5077.txt)), the previously
negotiated values are irrelevant, and only the values in the new
handshake messages are considered.

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-CBFA212F-C726-4D58-A520-A4BE147D1290}

### Setting up ALPN on the Client {#JSSEC-GUID-CBFA212F-C726-4D58-A520-A4BE147D1290 .sect3}

<div>
Set the Application Layer Protocol Negotiation (ALPN) values supported
by the client. During the handshake with the server, the server will
read the client's list of application protocols and will determine which
is most suitable.

<div class="section">
For the client, use the
`SSLParameters.setApplicationProtocols(String[])`{.codeph} method,
followed by the `setSSLParameters`{.codeph} method of either
`SSLSocket`{.codeph} or `SSLEngine`{.codeph} to set up the application
protocols to send to the server.

</div>
<!-- class="section" -->

<div class="example" id="GUID-CBFA212F-C726-4D58-A520-A4BE147D1290__GUID-B3161CAE-62B4-48EE-A432-163199F08491">
Example 8-21 Sample Code for Setting and Getting ALPN Values in a Java
Client

For example, here are the steps to set ALPN values of `"three"`{.codeph}
and `"two"`{.codeph}, on the client.

To run the code the property `javax.net.ssl.trustStore`{.codeph} must be
set to a valid root certificate. (This can be done on the command line).

``` {.oac_no_warn dir="ltr"}
import java.io.*; 
import java.util.*;
import javax.net.ssl.*; 
public class SSLClient {
    public static void main(String[] args) throws Exception {

        // Code for creating a client side SSLSocket
        SSLSocketFactory sslsf = (SSLSocketFactory) SSLSocketFactory.getDefault();
        SSLSocket sslSocket = (SSLSocket) sslsf.createSocket("localhost", 9999);

        // Get an SSLParameters object from the SSLSocket
        SSLParameters sslp = sslSocket.getSSLParameters();

        // Populate SSLParameters with the ALPN values
        // On the client side the order doesn't matter as
        // when connecting to a JDK server, the server's list takes priority
        String[] clientAPs = {"three", "two"};
        sslp.setApplicationProtocols(clientAPs);

        // Populate the SSLSocket object with the SSLParameters object
        // containing the ALPN values
        sslSocket.setSSLParameters(sslp);

        sslSocket.startHandshake();

        // After the handshake, get the application protocol that has been negotiated
        String ap = sslSocket.getApplicationProtocol();
        System.out.println("Application Protocol client side: \"" + ap + "\"");

        // Do simple write/read
        InputStream sslIS = sslSocket.getInputStream();
        OutputStream sslOS = sslSocket.getOutputStream();
        sslOS.write(280);
        sslOS.flush();
        sslIS.read();
        sslSocket.close();
    }
}
```

<div class="p">
When this code is run and sends a `ClientHello`{.codeph} to a Java
server that has set the ALPN values `one`{.codeph}, `two`{.codeph}, and
`three`{.codeph}, the output will be:

``` {.oac_no_warn dir="ltr"}
Application Protocol client side: two
```

See [The SSL
Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B)
for further details on handshaking. It is also possible to check the
results of the negotiation during handshaking. See [Determining
Negotiated ALPN Value during
Handshaking](java-secure-socket-extension-jsse-reference-guide.htm#GUID-BB4A54B3-FBC2-4B32-91CA-A16F91467ED9 "To determine the ALPN value that has been negotiated during the handshaking, create a custom KeyManager or TrustManager class, and include in this custom class a call to the getHandshakeApplicationProtocol method.").

</div>
</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-59618539-24AD-431E-84E3-585C4C4BF4E5}

### Setting up Default ALPN on the Server {#JSSEC-GUID-59618539-24AD-431E-84E3-585C4C4BF4E5 .sect3}

<div>
Use the default ALPN mechanism to determine a suitable application
protocol by setting ALPN values on the server.

<div class="section">
To use the default mechanism for ALPN on the server, populate an
`SSLParameters`{.codeph} object with the ALPN values you wish to set,
and then use this `SSLParameters`{.codeph} object to populate either the
`SSLSocket`{.codeph} object or the `SSLEngine`{.codeph} object with
these parameters as you have done when you set up ALPN on the client
(see the section [Setting up ALPN on the
Client](java-secure-socket-extension-jsse-reference-guide.htm#GUID-CBFA212F-C726-4D58-A520-A4BE147D1290 "Set the Application Layer Protocol Negotiation (ALPN) values supported by the client. During the handshake with the server, the server will read the client’s list of application protocols and will determine which is most suitable.")).
The first value of the ALPN values set on the server that matches any of
the ALPN values contained in the `ClientHello`{.codeph} will be chosen
and returned to the client as part of the `ServerHello`{.codeph}.

</div>
<!-- class="section" -->

<div class="example" id="GUID-59618539-24AD-431E-84E3-585C4C4BF4E5__GUID-DE951D27-9578-429C-84F8-DED2C5A91DD3">
Example 8-22 Sample Code for Default ALPN Value Negotiation on the
Server

Here is the code for a Java server that uses the default approach for
protocol negotiation. To run the code the property
`javax.net.ssl.keyStore`{.codeph} must be set to a valid keystore. (This
can be done on the command line, see [Creating a Keystore to Use with
JSSE](java-secure-socket-extension-jsse-reference-guide.htm#GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F "The procedure as to how you can use the keytool utility to create a simple PKCS12 keystore suitable for use with JSSE.")).

``` {.oac_no_warn dir="ltr"}
import java.util.*; 
import javax.net.ssl.*; 
public class SSLServer {
    public static void main(String[] args) throws Exception {

        // Code for creating a server side SSLSocket
        SSLServerSocketFactory sslssf = 
            (SSLServerSocketFactory) SSLServerSocketFactory.getDefault();
        SSLServerSocket sslServerSocket = 
            (SSLServerSocket) sslssf.createServerSocket(9999);
        SSLSocket sslSocket = (SSLSocket) sslServerSocket.accept();

        // Get an SSLParameters object from the SSLSocket
        SSLParameters sslp = sslSocket.getSSLParameters();

        // Populate SSLParameters with the ALPN values
        // As this is server side, put them in order of preference
        String[] serverAPs ={ "one", "two", "three" };
        sslp.setApplicationProtocols(serverAPs);

        // If necessary at any time, get the ALPN values set on the 
        // SSLParameters object with:
        // String serverAPs = sslp.setApplicationProtocols();

        // Populate the SSLSocket object with the ALPN values
        sslSocket.setSSLParameters(sslp);

        sslSocket.startHandshake();

        // After the handshake, get the application protocol that 
        // has been negotiated

        String ap = sslSocket.getApplicationProtocol();
        System.out.println("Application Protocol server side: \"" + ap + "\"");

        // Continue with the work of the server
        InputStream sslIS = sslSocket.getInputStream();
        OutputStream sslOS = sslSocket.getOutputStream();
        sslIS.read();
        sslOS.write(85);
        sslOS.flush();
        sslSocket.close();
    }
}
```

<div class="p">
When this code is run and a Java client sends a `ClientHello`{.codeph}
with ALPN values `three`{.codeph} and `two`{.codeph}, the output is:

``` {.oac_no_warn dir="ltr"}
Application Protocol server side: two
```

See [The SSL
Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B)
for further details on handshaking. It is also possible to check the
results of the negotiation during handshaking. See [Determining
Negotiated ALPN Value during
Handshaking](java-secure-socket-extension-jsse-reference-guide.htm#GUID-BB4A54B3-FBC2-4B32-91CA-A16F91467ED9 "To determine the ALPN value that has been negotiated during the handshaking, create a custom KeyManager or TrustManager class, and include in this custom class a call to the getHandshakeApplicationProtocol method.").

</div>
</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-B17DF013-83BD-4A00-BF91-D9E1E0BE70D8}

### Setting up Custom ALPN on the Server {#JSSEC-GUID-B17DF013-83BD-4A00-BF91-D9E1E0BE70D8 .sect3}

<div>
Use the custom ALPN mechanism to determine a suitable application
protocol by setting up a callback method.

<div class="section">
If you do not want to use the server's default negotiation protocol, you
can use the `setHandshakeApplicationProtocolSelector`{.codeph} method of
`SSLEngine`{.codeph} or `SSLSocket`{.codeph} to register a
`BiFunction`{.codeph} (lambda) callback that can examine the handshake
state so far, and then make your selection based on the client's list of
application protocols and any other relevant information. For example,
you may consider using the cipher suite suggested, or the Server Name
Indication (SNI) or any other data you can obtain in making the choice.
If custom negotiation is used, the values set by the
`setApplicationProtocols`{.codeph} method (default negotiation) will be
ignored.

</div>
<!-- class="section" -->

<div class="example" id="GUID-B17DF013-83BD-4A00-BF91-D9E1E0BE70D8__GUID-DE951D27-9578-429C-84F8-DED2C5A91DD3">
Example 8-23 Sample Code for Custom ALPN Value Negotiation on the Server

Here is the code for a Java server that uses the custom mechanism for
protocol negotiation. To run the code the property
`javax.net.ssl.keyStore`{.codeph} must be set to a valid certificate.
(This can be done on the command line, see [Creating a Keystore to Use
with
JSSE](java-secure-socket-extension-jsse-reference-guide.htm#GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F "The procedure as to how you can use the keytool utility to create a simple PKCS12 keystore suitable for use with JSSE.")).

``` {.oac_no_warn dir="ltr"}
import java.util.*; 
import javax.net.ssl.*; 
public class SSLServer {
    public static void main(String[] args) throws Exception {

        // Code for creating a server side SSLSocket
        SSLServerSocketFactory sslssf =
            (SSLServerSocketFactory) SSLServerSocketFactory.getDefault();
        SSLServerSocket sslServerSocket = 
            (SSLServerSocket) sslssf.createServerSocket(9999);
        SSLSocket sslSocket = (SSLSocket) sslServerSocket.accept();

        // Code to set up a callback function
        // Pass in the current SSLSocket to be inspected and client AP values
        sslSocket.setHandshakeApplicationProtocolSelector(
            (serverSocket, clientProtocols) -> {
                SSLSession handshakeSession = serverSocket.getHandshakeSession();
                // callback function called with current SSLSocket and client AP values
                // plus any other useful information to help determine appropriate
                // application protocol. Here the protocol and ciphersuite are also
                // passed to the callback function.
                return chooseApplicationProtocol(
                    serverSocket,
                    clientProtocols,
                    handshakeSession.getProtocol(),
                    handshakeSession.getCipherSuite());
         }); 

        sslSocket.startHandshake();

        // After the handshake, get the application protocol that has been
        // returned from the callback method.

        String ap = sslSocket.getApplicationProtocol();
        System.out.println("Application Protocol server side: \"" + ap + "\"");

        // Continue with the work of the server
        InputStream sslIS = sslSocket.getInputStream();
        OutputStream sslOS = sslSocket.getOutputStream();
        sslIS.read();
        sslOS.write(85);
        sslOS.flush();
        sslSocket.close();
    }

    // The callback method. Note how the parameters match the call within 
    // the setHandshakeApplicationProtocolSelector method above.
    public static String chooseApplicationProtocol(SSLSocket serverSocket,
            List<String> clientProtocols, String protocol, String cipherSuite ) {
        // For example, check the cipher suite and return an application protocol
        // value based on that.
        if (cipherSuite.equals("<--a_particular_ciphersuite-->")) { 
            return "three";
        } else {
            return "";
        }
    } 
}
```

If the cipher suite matches the one you specify in the condition
statement when this code is run , then the value `three`{.codeph} will
be returned. Otherwise an empty string will be returned.

Note that the `BiFunction`{.codeph} object's return value is a
`String`{.codeph}, which will be the application protocol name, or null
to indicate that none of the advertised names are acceptable. If the
return value is an empty `String`{.codeph} then application protocol
indications will not be used. If the return value is null (no value
chosen) or is a value that was not advertised by the peer, the
underlying protocol will determine what action to take. (For example,
the server code will send a \"no\_application\_protocol\" alert and
terminate the connection.)

After handshaking completes on both client and server, you can check the
result of the negotiation by calling the
`getApplicationProtocol`{.codeph} method on either the
`SSLSocket`{.codeph} object or the `SSLEngine`{.codeph} object. See [The
SSL
Handshake](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B)
for further details on handshaking.

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-BB4A54B3-FBC2-4B32-91CA-A16F91467ED9}

### Determining Negotiated ALPN Value during Handshaking {#JSSEC-GUID-BB4A54B3-FBC2-4B32-91CA-A16F91467ED9 .sect3}

<div>
To determine the ALPN value that has been negotiated during the
handshaking, create a custom `KeyManager`{.codeph} or
`TrustManager`{.codeph} class, and include in this custom class a call
to the `getHandshakeApplicationProtocol`{.codeph} method.

<div class="section">
There are some use cases where the selected ALPN and SNI values will
affect the choices made by a `KeyManager`{.codeph} or
`TrustManager`{.codeph}. For example, an application might want to
select different certificate/private key sets depending on the
attributes of the server and the chosen ALPN/SNI/ciphersuite values.

The sample code given illustrates how to call the
`getHandshakeApplicationProtocol`{.codeph} method from within a custom
`X509ExtendedKeyManager`{.codeph} that you create and register as the
`KeyManager`{.codeph} object.

</div>
<!-- class="section" -->

<div class="example" id="GUID-BB4A54B3-FBC2-4B32-91CA-A16F91467ED9__GUID-57D815A8-4BF8-4F9F-9735-9240C4E6D718">
Example 8-24 Sample Code for a Custom KeyManager

This example shows the entire code for a custom `KeyManager`{.codeph}
that extends `X509ExtendedKeyManager`{.codeph}. Most methods simply
return the value returned from the `KeyManager`{.codeph} class that is
being wrapped by this `MyX509ExtendedKeyManager`{.codeph} class. However
the `chooseServerAlias`{.codeph} method calls the
`getHandshakeApplicationProtocol`{.codeph} on the `SSLSocket`{.codeph}
object and therefore can determine the current negotiated ALPN value.

``` {.oac_no_warn dir="ltr"}

import java.net.Socket;
import java.security.*;
import javax.net.ssl.*;

public class MyX509ExtendedKeyManager extends X509ExtendedKeyManager {

    // X509ExtendedKeyManager is an abstract class so your new class 
    // needs to implement all the abstract methods in this class. 
    // The easiest way to do this is to wrap an existing KeyManager
    // and call its methods for each of the methods you need to implement.   

    X509ExtendedKeyManager akm;
    
    public MyX509ExtendedKeyManager(X509ExtendedKeyManager akm) {
        this.akm = akm;
    }

    @Override
    public String[] getClientAliases(String keyType, Principal[] issuers) {
        return akm.getClientAliases(keyType, issuers);
    }

    @Override
    public String chooseClientAlias(String[] keyType, Principal[] issuers, 
        Socket socket) {
        return akm.chooseClientAlias(keyType, issuers, socket);
    }

    @Override
    public String chooseServerAlias(String keyType, Principal[] issuers, 
        Socket socket) {
        
        // This method has access to a Socket, so it is possible to call the
        // getHandshakeApplicationProtocol method here. Note the cast from 
        // a Socket to an SSLSocket
        String ap = ((SSLSocket) socket).getHandshakeApplicationProtocol();
        System.out.println("In chooseServerAlias, ap is: " + ap);
        return akm.chooseServerAlias(keyType, issuers, socket);
    }

    @Override
    public String[] getServerAliases(String keyType, Principal[] issuers) {
        return akm.getServerAliases(keyType, issuers);
    }

    @Override
    public X509Certificate[] getCertificateChain(String alias) {
        return akm.getCertificateChain(alias);
    }

    @Override
    public PrivateKey getPrivateKey(String alias) {
        return akm.getPrivateKey(alias);
    }
}
```

<div class="p">
When this code is registered as the `KeyManager`{.codeph} for a Java
server and a Java client sends a `ClientHello`{.codeph} with ALPN
values, the output will be:

``` {.oac_no_warn dir="ltr"}
    In chooseServerAlias, ap is: <negotiated value>
```

</div>
</div>
<!-- class="example" -->

<div class="example" id="GUID-BB4A54B3-FBC2-4B32-91CA-A16F91467ED9__GUID-264BBD9E-71BA-412C-AA77-EF0EC265D42B">
Example 8-25 Sample Code for Using a Custom KeyManager in a Java Server

This example shows a simple Java server that uses the default ALPN
negotiation strategy and the custom `KeyManager`{.codeph},
`MyX509ExtendedKeyManager`{.codeph}, shown in the prior code sample.

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.util.*;
import javax.net.ssl.*;
import java.security.KeyStore;

public class SSLServerHandshake {
    
    public static void main(String[] args) throws Exception {
        SSLContext ctx = SSLContext.getInstance("TLS");

        // You need to explicitly create a create a custom KeyManager

        // Keystores
        KeyStore keyKS = KeyStore.getInstance("PKCS12");
        keyKS.load(new FileInputStream("serverCert.p12"), 
            "password".toCharArray());

        // Generate KeyManager
        KeyManagerFactory kmf = KeyManagerFactory.getInstance("PKIX");
        kmf.init(keyKS, "password".toCharArray());
        KeyManager[] kms = kmf.getKeyManagers();

        // Code to substitute MyX509ExtendedKeyManager
        if (!(kms[0] instanceof X509ExtendedKeyManager)) {
            throw new Exception("kms[0] not X509ExtendedKeyManager");
        }

        // Create a new KeyManager array and set the first index 
        // of the array to an instance of MyX509ExtendedKeyManager.
        // Notice how creating this object is done by passing in the 
        // existing default X509ExtendedKeyManager 
        kms = new KeyManager[] { 
            new MyX509ExtendedKeyManager((X509ExtendedKeyManager) kms[0])};

        // Initialize SSLContext using the new KeyManager
        ctx.init(kms, null, null);

        // Instead of using SSLServerSocketFactory.getDefault(), 
        // get a SSLServerSocketFactory based on the SSLContext
        SSLServerSocketFactory sslssf = ctx.getServerSocketFactory();
        SSLServerSocket sslServerSocket = 
            (SSLServerSocket) sslssf.createServerSocket(9999);
        SSLSocket sslSocket = (SSLSocket) sslServerSocket.accept();
        SSLParameters sslp = sslSocket.getSSLParameters();
        String[] serverAPs ={"one","two","three"};
        sslp.setApplicationProtocols(serverAPs);
        sslSocket.setSSLParameters(sslp);
        sslSocket.startHandshake();

        String ap = sslSocket.getApplicationProtocol();
        System.out.println("Application Protocol server side: \"" + ap + "\"");

        InputStream sslIS = sslSocket.getInputStream();
        OutputStream sslOS = sslSocket.getOutputStream();
        sslIS.read();
        sslOS.write(85);
        sslOS.flush();

        sslSocket.close();
        sslServerSocket.close();
    }
}
```

With the custom `X509ExtendedKeyManager`{.codeph} in place, when
`chooseServerAlias`{.codeph} is called during handshaking the
`KeyManager`{.codeph} has the opportunity to examine the negotiated
application protocol value. In the case of the example shown, this value
is output to the console.

<div class="p">
For example, when this code is run and a Java client sends a
`ClientHello`{.codeph} with ALPN values `three`{.codeph} and
`two`{.codeph}, the output will be:

``` {.oac_no_warn dir="ltr"}
Application Protocol server side: two
```

</div>
</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-6D774DB6-FD5C-4066-B144-C1F10E2DD742}

### ALPN Related Classes and Methods {#JSSEC-GUID-6D774DB6-FD5C-4066-B144-C1F10E2DD742 .sect3}

<div>
These classes and methods are used when working with Application Layer
Protocol Negotiation (ALPN).

<div class="section">
Classes and Methods to Use

`SSLEngine`{.codeph} and `SSLSocket`{.codeph} contain the same ALPN
related methods and they have the same functionality.

<div class="tblformalwide" id="GUID-6D774DB6-FD5C-4066-B144-C1F10E2DD742__GUID-FE0C995B-14C9-493B-8716-D66B3FDD990A">
+-----------------------+-----------------------+-----------------------+
| Class                 | Method                | Purpose               |
+:======================+:======================+:======================+
| `SSLParameters`{.code | `public String[] getA | <span class="bold">Cl |
| ph}                   | pplicationProtocols() | ient-side             |
|                       | ;`{.codeph}           | and                   |
|                       |                       | server-side</span>:   |
|                       |                       | use the method to     |
|                       |                       | return a              |
|                       |                       | `String`{.codeph}     |
|                       |                       | array containing each |
|                       |                       | protocol set.         |
+-----------------------+-----------------------+-----------------------+
| `SSLParameters`{.code | `public void setAppli | <span class="bold">Cl |
| ph}                   | cationProtocols([] pr | ient-side</span>:     |
|                       | otocols);`{.codeph}   | use the method to set |
|                       |                       | the protocols that    |
|                       |                       | can be chosen by the  |
|                       |                       | server.               |
|                       |                       |                       |
|                       |                       | <span class="bold">Se |
|                       |                       | rver-side</span>:     |
|                       |                       | use the method to set |
|                       |                       | the protocols that    |
|                       |                       | the server can use.   |
|                       |                       | The String array      |
|                       |                       | should contain the    |
|                       |                       | protocols in order of |
|                       |                       | preference.           |
+-----------------------+-----------------------+-----------------------+
| `SSLEngine`{.codeph}  | `public String getApp | <span class="bold">Cl |
|                       | licationProtocol();`{ | ient-side             |
| `SSLSocket`{.codeph}  | .codeph}              | and                   |
|                       |                       | server-side</span>:   |
|                       |                       | use the method        |
|                       |                       | <span class="italic"> |
|                       |                       | after</span>          |
|                       |                       | TLS protocol          |
|                       |                       | negotiation has       |
|                       |                       | completed to return a |
|                       |                       | `String`{.codeph}     |
|                       |                       | containing the        |
|                       |                       | protocol that has     |
|                       |                       | been chosen for the   |
|                       |                       | connection.           |
+-----------------------+-----------------------+-----------------------+
| `SSLEngine`{.codeph}  | `public String getHan | <span class="bold">Cl |
|                       | dshakeApplicationProt | ient-side             |
| `SSLSocket`{.codeph}  | ocol();`{.codeph}     | and                   |
|                       |                       | server-side</span>:   |
|                       |                       | use the method        |
|                       |                       | <span class="italic"> |
|                       |                       | during</span>         |
|                       |                       | handshaking to return |
|                       |                       | a `String`{.codeph}   |
|                       |                       | containing the        |
|                       |                       | protocol that has     |
|                       |                       | been chosen for the   |
|                       |                       | connection. If this   |
|                       |                       | method is called      |
|                       |                       | before or after       |
|                       |                       | handshaking, it will  |
|                       |                       | return null. See      |
|                       |                       | [Determining          |
|                       |                       | Negotiated ALPN Value |
|                       |                       | during                |
|                       |                       | Handshaking](java-sec |
|                       |                       | ure-socket-extension- |
|                       |                       | jsse-reference-guide. |
|                       |                       | htm#GUID-BB4A54B3-FBC |
|                       |                       | 2-4B32-91CA-A16F91467 |
|                       |                       | ED9 "To determine the |
|                       |                       |  ALPN value that has  |
|                       |                       | been negotiated durin |
|                       |                       | g the handshaking, cr |
|                       |                       | eate a custom KeyMana |
|                       |                       | ger or TrustManager c |
|                       |                       | lass, and include in  |
|                       |                       | this custom class a c |
|                       |                       | all to the getHandsha |
|                       |                       | keApplicationProtocol |
|                       |                       |  method.")            |
|                       |                       | for instructions on   |
|                       |                       | how to call this      |
|                       |                       | method.               |
+-----------------------+-----------------------+-----------------------+
| `SSLEngine`{.codeph}  | `public void setHands | <span class="bold">Se |
|                       | hakeApplicationProtoc | rver-side</span>:     |
| `SSLSocket`{.codeph}  | olSelector(BiFunction | use the method to     |
|                       | ,String> selector)`{. | register a callback   |
|                       | codeph}               | function. The         |
|                       |                       | application protocol  |
|                       |                       | value can then be set |
|                       |                       | in the callback based |
|                       |                       | on any information    |
|                       |                       | available, for        |
|                       |                       | example the protocol  |
|                       |                       | or cipher suite. See  |
|                       |                       | [Setting up Custom    |
|                       |                       | ALPN on the           |
|                       |                       | Server](java-secure-s |
|                       |                       | ocket-extension-jsse- |
|                       |                       | reference-guide.htm#G |
|                       |                       | UID-B17DF013-83BD-4A0 |
|                       |                       | 0-BF91-D9E1E0BE70D8 " |
|                       |                       | Use the custom ALPN m |
|                       |                       | echanism to determine |
|                       |                       |  a suitable applicati |
|                       |                       | on protocol by settin |
|                       |                       | g up a callback metho |
|                       |                       | d.")                  |
|                       |                       | for instructions on   |
|                       |                       | how to use this       |
|                       |                       | method.               |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-D8F6E432-12F2-47B8-9FD0-CE57A4A4F2E1}

Troubleshooting JSSE {#JSSEC-GUID-D8F6E432-12F2-47B8-9FD0-CE57A4A4F2E1 .sect2}
--------------------

<div>
This section contains information for troubleshooting JSSE. It provides
solutions to common configuration problem.

First, it provides some common [Configuration
Problems](java-secure-socket-extension-jsse-reference-guide.htm#GUID-E8E3C6C4-5B7E-466F-B11C-35BF3B9F454D "Solutions to some common configuration problems.")
and ways to solve them, and then it describes helpful [Debugging
Utilities](java-secure-socket-extension-jsse-reference-guide.htm#GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF).

</div>
<div class="sect3">
[]{#GUID-E8E3C6C4-5B7E-466F-B11C-35BF3B9F454D}

### Configuration Problems {#JSSEC-GUID-E8E3C6C4-5B7E-466F-B11C-35BF3B9F454D .sect3}

<div>
Solutions to some common configuration problems.

</div>
<div class="sect4">
[]{#GUID-E87F514E-A7E8-4E79-90DE-D375FF64A908}

#### CertificateException While Handshaking {#JSSEC-GUID-E87F514E-A7E8-4E79-90DE-D375FF64A908 .sect4}

<div>
<span class="bold">Problem:</span> When negotiating an SSL/TLS/DTLS
connection, the client or server throws a
`CertificateException`{.codeph}.

<span class="bold">Cause 1:</span> This is generally caused by the
remote side sending a certificate that is unknown to the local side.

<span class="bold">Solution 1:</span> The best way to debug this type of
problem is to turn on debugging (see [Debugging
Utilities](java-secure-socket-extension-jsse-reference-guide.htm#GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF))
and watch as certificates are loaded and when certificates are received
via the network connection. Most likely, the received certificate is
unknown to the trust mechanism because the wrong trust file was loaded.

Refer to the following sections:

-   [JSSE Classes and
    Interfaces](java-secure-socket-extension-jsse-reference-guide.htm#GUID-B7AB25FA-7F0C-4EFA-A827-813B2CE7FBDC)
-   [The TrustManager
    Interface](java-secure-socket-extension-jsse-reference-guide.htm#GUID-42CA1099-42AD-4772-BC4A-29C2A78E3EC9 "The primary responsibility of the TrustManager is to determine whether the presented authentication credentials should be trusted. If the credentials are not trusted, then the connection will be terminated. To authenticate the remote identity of a secure socket peer, you must initialize an SSLContext object with one or more TrustManager objects. You must pass one TrustManager for each authentication mechanism that is supported. If null is passed into the SSLContext initialization, then a trust manager will be created for you. Typically, a single trust manager supports authentication based on X.509 public key certificates (for example, X509TrustManager). Some secure socket implementations may also support authentication based on shared secret keys, Kerberos, or other mechanisms.")
-   [The KeyManager
    Interface](java-secure-socket-extension-jsse-reference-guide.htm#GUID-997AB098-DDD7-40E2-9FD0-5AA3C83E1702)

<span class="bold">Cause 2:</span> The system clock is not set
correctly. In this case, the perceived time may be outside the validity
period on one of the certificates, and unless the certificate can be
replaced with a valid one from a truststore, the system must assume that
the certificate is invalid, and therefore throw the exception.

<span class="bold">Solution 2:</span> Correct the system clock time.

</div>
</div>
<div class="sect4">
[]{#GUID-48170215-4EF1-4653-B58F-81572E9FE23F}

#### Runtime Exception: SSL Service Not Available {#JSSEC-GUID-48170215-4EF1-4653-B58F-81572E9FE23F .sect4}

<div>
<div class="section">
<span class="bold">Problem:</span> When running a program that uses
JSSE, an exception occurs indicating that an SSL service is not
available. For example, an exception similar to one of the following is
thrown:

``` {.codeblock dir="ltr"}
    Exception in thread "main" java.net.SocketException:
        no SSL Server Sockets
    
    Exception in thread "main":
        SSL implementation not available
```

<span class="bold">Cause:</span> There was a problem with
`SSLContext`{.codeph} initialization, for example, due to an incorrect
password on a keystore or a corrupted keystore (a JDK vendor once
shipped a keystore in an unknown format, and that caused this type of
error).

<span class="bold">Solution:</span> Check initialization parameters.
Ensure that any keystores specified are valid and that the passwords
specified are correct. One way that you can check this is by trying to
use `keytool`{.codeph} to examine the keystores and the relevant
contents. See
[keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) in
<span id="GUID-48170215-4EF1-4653-B58F-81572E9FE23F__JSWOR"><cite>Java
Platform, Standard Edition Tools Reference</cite></span>.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-92715704-80F4-431A-BF99-D583EE61C4AB}

#### Runtime Exception: \"No available certificate corresponding to the SSL cipher suites which are enabled\" {#JSSEC-GUID-92715704-80F4-431A-BF99-D583EE61C4AB .sect4}

<div>
<div class="section">
<span class="bold">Problem:</span> When trying to run a simple SSL
server program, the following exception is thrown:

``` {.codeblock dir="ltr"}
    Exception in thread "main" javax.net.ssl.SSLException:
        No available certificate corresponding to the SSL cipher suites which are enabled...
```

<span class="bold">Cause:</span> Various cipher suites require certain
types of key material. For example, if an RSA cipher suite is enabled,
then an RSA `keyEntry`{.codeph} must be available in the keystore. If no
such key is available, then this cipher suite cannot be used. This
exception is thrown if there are no available key entries for all of the
cipher suites enabled.

<span class="bold">Solution:</span> Create key entries for the various
cipher suite types, or use an anonymous suite. Anonymous cipher suites
are inherently dangerous because they are vulnerable to MITM
(man-in-the-middle) attacks. See [RFC
2246](http://www.ietf.org/rfc/rfc2246.txt?number=2246).

Refer to the following sections to learn how to pass the correct
keystore and certificates:

-   [JSSE Classes and
    Interfaces](java-secure-socket-extension-jsse-reference-guide.htm#GUID-B7AB25FA-7F0C-4EFA-A827-813B2CE7FBDC)
-   [Customizing the Default Keystores and Truststores, Store Types, and
    Store
    Passwords](java-secure-socket-extension-jsse-reference-guide.htm#GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150)
-   [Additional Keystore Formats
    (PKCS12)](java-secure-socket-extension-jsse-reference-guide.htm#GUID-93EBE6F4-1460-450A-8D9C-AF086C233BDF)

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-1409C7FD-0E15-4367-93F5-EB327099D8B5}

#### Runtime Exception: No Cipher Suites in Common {#JSSEC-GUID-1409C7FD-0E15-4367-93F5-EB327099D8B5 .sect4}

<div>
<div class="section">
<span class="bold">Problem 1:</span> When handshaking, the client and/or
server throw this exception.

<span class="bold">Cause 1:</span> Both sides of an SSL connection must
agree on a common cipher suite. If the intersection of the client\'s
cipher suite set with the server\'s cipher suite set is empty, then you
will see this exception.

<span class="bold">Solution 1:</span> Configure the enabled cipher
suites to include common cipher suites, and be sure to provide an
appropriate `keyEntry`{.codeph} for asymmetric cipher suites. Also see
[Runtime Exception: \"No available certificate corresponding to the SSL
cipher suites which are
enabled\"](java-secure-socket-extension-jsse-reference-guide.htm#GUID-92715704-80F4-431A-BF99-D583EE61C4AB)
in this section.)

<span class="bold">Problem 2:</span> When using Mozilla Firefox or
Microsoft Internet Explorer to access files on a server that only has
DSA-based certificates, a runtime exception occurs indicating that there
are no cipher suites in common.

<span class="bold">Cause 2:</span> By default, `keyEntries`{.codeph}
created with `keytool`{.codeph} use DSA public keys. If only DSA
`keyEntries`{.codeph} exist in the keystore, then only DSA-based cipher
suites can be used. By default, Navigator and Internet Explorer send
only RSA-based cipher suites. Because the intersection of client and
server cipher suite sets is empty, this exception is thrown.

<span class="bold">Solution 2:</span> To interact with Navigator or
Internet Explorer, you should create certificates that use RSA-based
keys. To do this, specify the `-keyalg`{.codeph} RSA option when using
keytool. For example:

``` {.codeblock dir="ltr"}
keytool -genkeypair -alias duke -keystore testkeys -keyalg rsa
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-B20D551B-9558-43C5-94D8-BF5464C8F2B7}

#### Socket Disconnected After Sending ClientHello Message {#JSSEC-GUID-B20D551B-9558-43C5-94D8-BF5464C8F2B7 .sect4}

<div>
<div class="section">
<span class="bold">Problem:</span> A socket attempts to connect, sends a
ClientHello message, and is immediately disconnected.

<span class="bold">Cause:</span> Some SSL/TLS servers will disconnect if
a ClientHello message is received in a format they do not understand or
with a protocol version number that they do not support.

<span class="bold">Solution</span>: Try adjusting the enabled protocols
on the client side. This involves modifying or invoking some of the
following system properties and methods:

-   System property
    [`https.protocols`{.codeph}](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__HTTPS.PROTOCOLS_PROPERTY)
    for the `HttpsURLConnection`{.codeph}</a></code> class
-   System property
    [<span class="apiname">jdk.tls.client.protocols</span>](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9__JDK.TLS.CLIENT.PROTOCOLS_PROPERTY)
-   [`SSLContext.getInstance`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLContext.html#getInstance-java.lang.String-)
    method
-   [`SSLEngine.setEnabledProtocols`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngine.html#setEnabledProtocols-java.lang.String:A-)
    method
-   [`SSLSocket.setEnabledProtocols`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLSocket.html#setEnabledProtocols-java.lang.String:A-)
    method
-   [`SSLParameters.setProtocols`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#setProtocols-java.lang.String:A-)
    and
    [`SSLEngine.setSSLParameters`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLEngine.html#setProtocols-java.lang.String:A-)
    methods
-   [`SSLParameters.setProtocols`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLParameters.html#setProtocols-java.lang.String:A-)
    and
    [`SSLSocket.setSSLParameters`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLSocket.html#setProtocols-java.lang.String:A-)
    methods

For backwards compatibility, some SSL/TLS implementations (such as
SunJSSE) can send SSL/TLS ClientHello messages encapsulated in the SSLv2
ClientHello format. The SunJSSE provider supports this feature. If you
want to use this feature, add the \"SSLv2Hello\" protocol to the enabled
protocol list, if necessary. (See Protocols in the [JDK
Providers](oracle-providers.htm#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313 "This document contains the technical details of the providers that are included in the JDK. It is assumed that readers have a strong understanding of the Java Cryptography Architecture and Provider Architecture."),
which lists the protocols that are enabled by default for the SunJSSE
provider.)

The SSL/TLS RFC standards require that implementations negotiate to the
latest version both sides speak, but some non-conforming implementation
simply hang up if presented with a version they don\'t understand. For
example, some older server implementations that speak only SSLv3 will
shutdown if TLSv1.2 is requested. In this situation, consider using a
SSL/TLS version fallback scheme:

1.  Fall back from TLSv1.2 to TLSv1.1 if the server does not understand
    TLSv1.2.
2.  Fall back from TLSv1.1 to TLSv1.0 if the previous step does not
    work.

For example, if the enabled protocol list on the client is TLSv1,
TLSv1.1, and TLSv1.2, a typical SSL/TLS version fallback scheme may look
like:

1.  Try to connect to server. If server rejects the SSL/TLS connection
    request immediately, go to step 2.
2.  Try the version fallback scheme by removing the highest protocol
    version (for example, TLSv1.2 for the first failure) in the enabled
    protocol list.
3.  Try to connect to the server again. If server rejects the
    connection, go to step 2 unless there is no version to which the
    server can fall back.
4.  If the connection fails and SSLv2Hello is not on the enabled
    protocol list, restore the enable protocol list and enable
    SSLv2Hello. (For example, the enable protocol list should be
    SSLv2Hello, TLSv1, TLSv1.1, and TLSv1.2.) Start again from step 1.

<div class="p">
<div class="infoboxnote" id="GUID-B20D551B-9558-43C5-94D8-BF5464C8F2B7__GUID-879D0C74-6202-47A4-A56F-1A971ABD230D">
Note:

A fallback to a previous version normally means security strength
downgrading to a weaker protocol. It is not suggested to use a fallback
scheme unless it is really necessary, and you clearly know that the
server does not support a higher protocol version.

</div>
</div>
<div class="infoboxnote" id="GUID-B20D551B-9558-43C5-94D8-BF5464C8F2B7__GUID-FF293B29-F33E-41EF-909A-6350B9D35E23">
Note:

As part of disabling SSLv3, some servers have also disabled SSLv2Hello,
which means communications with SSLv2Hello-active clients (JDK 6u95)
will fail. Starting with JDK 7, SSLv2Hello default to disabled on
clients, enabled on servers.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-85667451-803E-4E07-B366-00E19790595B}

#### SunJSSE Cannot Find a JCA Provider That Supports a Required Algorithm and Causes a NoSuchAlgorithmException {#JSSEC-GUID-85667451-803E-4E07-B366-00E19790595B .sect4}

<div>
<div class="section">
<span class="bold">Problem:</span> A handshake is attempted and fails
when it cannot find a required algorithm. Examples might include:

``` {.codeblock dir="ltr"}
Exception in thread ...deleted...
    ...deleted...
    Caused by java.security.NoSuchAlgorithmException: Cannot find any
        provider supporting RSA/ECB/PKCS1Padding
```

or

``` {.codeblock dir="ltr"}
Caused by java.security.NoSuchAlgorithmException: Cannot find any
    provider supporting AES/CBC/NoPadding
```

<span class="bold">Cause:</span> SunJSSE uses JCE for all its
cryptographic algorithms. If the SunJCE provider has been deregistered
from the `Provider`{.codeph} mechanism and an alternative implementation
from JCE is not available, then this exception will be thrown.

<span class="bold">Solution:</span> Ensure that the SunJCE is available
by checking that the provider is registered with the `Provider`{.codeph}
interface. Try to run the following code in the context of your SSL
connection:

``` {.codeblock dir="ltr"}
import javax.crypto.*;

System.out.println("=====Where did you get AES=====");
Cipher c = Cipher.getInstance("AES/CBC/NoPadding");
System.out.println(c.getProvider());
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-BEA0A351-848D-4E0E-9B96-48B27FDED1BA}

#### FailedDownloadException Thrown When Trying to Obtain Application Resources from Web Server over SSL {#JSSEC-GUID-BEA0A351-848D-4E0E-9B96-48B27FDED1BA .sect4}

<div>
<div class="section">
<span class="bold">Problem:</span> If you receive a
`com.sun.deploy.net.FailedDownloadException`{.codeph} when trying to
obtain application resources from your web server over SSL, and your web
server uses the virtual host with Server Name Indication (SNI) extension
(such as Apache HTTP Server), then you may have not configured your web
server correctly.

<span class="bold">Cause:</span> Because Java SE 7 supports the SNI
extension in the JSSE client, the requested host name of the virtual
server is included in the first message sent from the client to the
server during the SSL handshake. The server may deny the client\'s
request for a connection if the requested host name (the server name
indication) does not match the expected server name, which should be
specified in the virtual host\'s configuration. This triggers an SSL
handshake unrecognized name alert, which results in a
`FailedDownloadException`{.codeph} being thrown.

<span class="bold">Solution:</span> To better diagnose the problem,
enable tracing through the Java Console. See
[Debugging](olink:JSDPG-GUID-11D4AE7F-84C4-4D2D-9665-2D3929BB4387) and
[Java Console](olink:JSDPG-GUID-8B1B0E20-8550-4A11-8327-297C06134D48) in
<span id="GUID-BEA0A351-848D-4E0E-9B96-48B27FDED1BA__JSDAP"><cite>Java
Platform, Standard Edition Deployment Guide</cite></span>. If the cause
of the problem is
`javax.net.ssl.SSLProtocolException: handshake alert: unrecognized_name`{.codeph},
it is likely that the virtual host configuration for SNI is incorrect.
If you are using Apache HTTP Server, see [Name-based Virtual Host
Support](https://httpd.apache.org/docs/trunk/vhosts/name-based.html)
about configuring virtual hosts. In particular, ensure that the
`ServerName`{.codeph} directive is configured properly in a
`<VirtualHost>`{.codeph} block.

See the following:

-   [SSL with Virtual Hosts Using
    SNI](https://wiki.apache.org/httpd/NameBasedSSLVHostsWithSNI) from
    [Apache HTTP Server Wiki](https://wiki.apache.org/httpd/FrontPage)
-   [SSL/TLS Strong Encryption:
    FAQ](https://httpd.apache.org/docs/trunk/ssl/ssl_faq.html) from
    [Apache HTTP Server Documentation](https://httpd.apache.org/docs/)
-   [RFC 3546, Transport Layer Security (TLS)
    Extensions](https://www.ietf.org/rfc/rfc3546.txt)
-   [Bug 7194590: SSL handshaking error caused by virtual server
    misconfiguration](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=7194590)

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-001B7524-87A4-4085-B8EF-929E0503DBEC}

#### IllegalArgumentException When RC4 Cipher Suites are Configured for DTLS {#JSSEC-GUID-001B7524-87A4-4085-B8EF-929E0503DBEC .sect4}

<div>
<div class="section">
<span class="bold">Problem: </span> An
`IllegalArgumentException`{.codeph} exception is thrown when RC4 cipher
suite algorithm is specified in
`SSLEngine.setEnabledCipherSuites(String[] suites)`{.codeph} method and
the <span class="apiname">SSLEngine</span> is a DTLS engine.

``` {.codeblock dir="ltr"}
sslContext = SSLContext.getInstance("DTLS");

// Create the engine
SSLEngine engine = sslContext.createSSLengine(hostname, port);

String enabledSuites[] = { "SSL_RSA_WITH_RC4_128_SHA" };
engine.setEnabledCipherSuites(enabledSuites);
```

<span class="bold">Cause:</span> According to [DTLS Version
1.0](http://tools.ietf.org/html/rfc4347) and [DTLS Version
1.2](http://tools.ietf.org/html/rfc6347), RC4 cipher suites must not be
used with DTLS.

<span class="bold">Solution:</span> Do not use RC4 based cipher suites
for DTLS connections. See <span class="q">\"JSSE Cipher Suite
Names\"</span> in [Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF}

### Debugging Utilities {#JSSEC-GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF .sect3}

<div>
<div class="section">
JSSE provides dynamic debug tracing support. This is similar to the
support used for debugging access control failures in the Java SE
platform. The generic Java dynamic debug tracing support is accessed
with the `java.security.debug`{.codeph} system property, whereas the
JSSE-specific dynamic debug tracing support is accessed with the
`javax.net.debug`{.codeph} system property.

<div class="p">
<div class="infoboxnote" id="GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF__GUID-0889B6AB-3EA2-4B6B-844D-652AFF24B968">
Note:

The `debug`{.codeph} utility is not an officially supported feature of
JSSE.

</div>
</div>
To view the options of the JSSE dynamic debug utility, use the following
command-line option on the `java`{.codeph} command:

``` {.codeblock dir="ltr"}
-Djavax.net.debug=help
```

<div class="infoboxnote" id="GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF__GUID-E45A25FE-5D18-4728-9014-F977BD07BE7D">
Note:

If you specify the value `help`{.codeph} with either dynamic debug
utility when running a program that does not use any classes that the
utility was designed to debug, you will not get the debugging options.

</div>
The following complete example shows how to get a list of the debug
options for an application named `MyApp`{.codeph} that uses some of the
JSSE classes:

``` {.codeblock dir="ltr"}
java -Djavax.net.debug=help MyApp
```

The `MyApp`{.codeph} application will not run after the debug help
information is printed, as the help code causes the application to exit.

Current options are:

-   `all`{.codeph}: Turn on all debugging
-   `ssl`{.codeph}: Turn on SSL debugging

The following can be used with the `ssl`{.codeph} option:

-   `record`{.codeph}: Enable per-record tracing
-   `handshake`{.codeph}: Print each handshake message
-   `keygen`{.codeph}: Print key generation data
-   `session`{.codeph}: Print session activity
-   `defaultctx`{.codeph}: Print default SSL initialization
-   `sslctx`{.codeph}: Print `SSLContext`{.codeph} tracing
-   `sessioncache`{.codeph}: Print session cache tracing
-   `keymanager`{.codeph}: Print key manager tracing
-   `trustmanager`{.codeph}: Print trust manager tracing

Messages generated from the `handshake`{.codeph} option can be widened
with these options:

-   `data`{.codeph}: Hex dump of each handshake message
-   `verbose`{.codeph}: Verbose handshake message printing

Messages generated from the `record`{.codeph} option can be widened with
these options:

-   `plaintext`{.codeph}: Hex dump of record plaintext
-   `packet`{.codeph}: Print raw SSL/TLS packets

The `javax.net.debug`{.codeph} property value must be either
`all`{.codeph} or `ssl`{.codeph}, optionally followed by debug
specifiers. You can use one or more options. You do
<span class="variable">not</span> have to have a separator between
options, although a separator such as a colon (:) or a comma (,) helps
readability. It does not matter what separators you use, and the
ordering of the option keywords is also not important.

For an introduction to reading this debug information, see the guide,
[Debugging SSL/TLS
Connections](java-secure-socket-extension-jsse-reference-guide.htm#GUID-4D421910-C36D-40A2-8BA2-7D42CCBED3C6 "Understanding SSL/TLS connection problems can sometimes be difficult, especially when it is not clear what messages are actually being sent and received. JSSE has a built-in debug facility and is activated by the System property javax.net.debug.").

The following are examples of using the `javax.net.debug`{.codeph}
property:

-   To view all debugging messages:

    ``` {.codeblock dir="ltr"}
    java -Djavax.net.debug=all MyApp        
    ```

-   To view the hexadecimal dumps of each handshake message, enter the
    following (the colons are optional):

    ``` {.codeblock dir="ltr"}
    java -Djavax.net.debug=ssl:handshake:data MyApp
    ```

-   To view the hexadecimal dumps of each handshake message, and to
    print trust manager tracing, enter the following (the commas are
    optional):

    ``` {.codeblock dir="ltr"}
    java -Djavax.net.debug=SSL,handshake,data,trustmanager MyApp
    ```

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-4D421910-C36D-40A2-8BA2-7D42CCBED3C6}

#### Debugging SSL/TLS Connections {#JSSEC-GUID-4D421910-C36D-40A2-8BA2-7D42CCBED3C6 .sect4}

<div>
Understanding SSL/TLS connection problems can sometimes be difficult,
especially when it is not clear what messages are actually being sent
and received. JSSE has a built-in debug facility and is activated by the
System property `javax.net.debug`{.codeph}.

<div class="section">
To know more about `javax.net.debug`{.codeph} System property, see
[Debugging
Utilities](java-secure-socket-extension-jsse-reference-guide.htm#GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF).

What follows is a brief example how to read the debug output. Please be
aware that the output is non-standard, and may change from release to
release. We are using the default JSSE X509KeyManager and
X509TrustManager which prints debug information.

This example assumes a basic understanding of the SSL/TLS protocol. To
know more about protocols (handshake messages, etc.), see [Secure
Sockets Layer (SSL) Protocol
Overview](java-secure-socket-extension-jsse-reference-guide.htm#GUID-69ECD56C-3B20-47F4-AEF0-A06EFA13A61D "Secure Sockets Layer (SSL) is the most widely used protocol for implementing cryptography on the web. SSL uses a combination of cryptographic processes to provide secure communication over a network. This section provides an introduction to SSL and the cryptographic processes it uses.").

In this example, we first run the `ClassFileServer`{.codeph} sample
application from <span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span>. This is a simple HTTPS server that
requires client authentication. This example runs
`ClassFileServer`{.codeph} on the host
`myremoteserver.example.com`{.codeph}:

`java -Djavax.net.ssl.trustStore=/my_home_directory/jssesamples/samples/samplecacerts -Djavax.net.ssl.trustStorePassword=changeit ClassFileServer 2002 /my_home_directory/jssesamples/samples/ TLS true`{.codeph}

Then, we connect to this HTTPS server using the
`SSLSocketClientWithClientAuth`{.codeph} sample application from
<span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> (on a host other than
`myremoteserver.example.com`{.codeph}), which sends an HTTPS request and
receives the reply:

`java SSLSocketClientWithClientAuth -Djavax.nex.debug=all -Djavax.net.ssl.trustStore=/my_home_directory/jssesamples/samples/samplecacerts myremoteserver.example.com 2002 /index.html`{.codeph}

First, the X509KeyManager is initialized and discovers there is one
keyEntry in the supplied KeyStore for a subject called \"duke\". If a
server requests a client to authenticate itself, the X509KeyManager will
search its list of keyEntries for an appropriate credential.

``` {.oac_no_warn dir="ltr"}
***
found key for : duke
chain [0] = [
[
  Version: V1
  Subject: CN=Duke, OU=Java Software, O="Sun Microsystems, Inc.", L=Cupertino, ST=CA, C=US
  Signature Algorithm: MD5withRSA, OID = 1.2.840.113549.1.1.4

  Key:  Sun RSA public key, 1024 bits
  modulus: 134968166047563266914058280571444028986498087544923991226919517667593269213420979048109900052353578998293280426361122296881234393722020704208851688212064483570055963805034839797994154526862998272017486468599962268346037652120279791547218281230795146025359480589335682217749874703510467348902637769973696151441
  public exponent: 65537
  Validity: [From: Tue May 22 19:46:46 EDT 2001,
               To: Sun May 22 19:46:46 EDT 2011]
  Issuer: CN=Duke, OU=Java Software, O="Sun Microsystems, Inc.", L=Cupertino, ST=CA, C=US
  SerialNumber: [    3b0afa66]

]
  Algorithm: [MD5withRSA]
  Signature:
0000: 5F B5 62 E9 A0 26 1D 8E   A2 7E 7C 02 08 36 3A 3E  _.b..&.......6:>
0010: C9 C2 45 03 DD F9 BC 06   FC 25 CF 30 92 91 B1 4E  ..E......%.0...N
0020: 62 17 08 48 14 68 80 CF   DD 89 11 EA 92 7F CE DD  b..H.h..........
0030: B4 FD 12 A8 71 C7 9E D7   C3 D0 E3 BD BB DE 20 92  ....q......... .
0040: C2 3B C8 DE CB 25 23 C0   8B B6 92 B9 0B 64 80 63  .;...%#......d.c
0050: D9 09 25 2D 7A CF 0A 31   B6 E9 CA C1 37 93 BC 0D  ..%-z..1....7...
0060: 4E 74 95 4F 58 31 DA AC   DF D8 BD 89 BD AF EC C8  Nt.OX1..........
0070: 2D 18 A2 BC B2 15 4F B7   28 6F D3 00 E1 72 9B 6C  -.....O.(o...r.l

]
***
```

The X509TrustManager is next initialized, and finds several certificates
for a Certificate Authority (CA), including one named \"localhost\". Any
server presenting <span class="bold">valid</span> credentials signed by
these CAs will be trusted.

``` {.oac_no_warn dir="ltr"}
***
trustStore is: /my_home_directory/jssesamples/samples/samplecacerts
trustStore type is: pkcs12
trustStore provider is: 
the last modified time is: Tue Dec 11 06:43:38 EST 2012
Reload the trust store
Reload trust certs
Reloaded 32 trust certs

...

adding as trusted cert:
  Subject: CN=localhost, OU=Widget Development Group, O="Ficticious Widgets, Inc.", L=Sunnyvale, ST=CA, C=US
  Issuer:  CN=localhost, OU=Widget Development Group, O="Ficticious Widgets, Inc.", L=Sunnyvale, ST=CA, C=US
  Algorithm: RSA; Serial number: 0x41004446
  Valid from Thu Jul 22 18:48:38 EDT 2004 until Sun May 22 18:48:38 EDT 2011

...
```

We finish some additional initialization code, and after this, we are
now finally ready to make the connection to the server.

``` {.oac_no_warn dir="ltr"}
trigger seeding of SecureRandom
done seeding SecureRandom
Allow unsafe renegotiation: false
Allow legacy hello messages: true
Is initial handshake: true
Is secure renegotiation: false
Ignoring unsupported cipher suite: TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 for TLSv1
Ignoring unsupported cipher suite: TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 for TLSv1
Ignoring unsupported cipher suite: TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 for TLSv1
...
Ignoring unsupported cipher suite: TLS_ECDH_RSA_WITH_AES_256_CBC_SHA384 for TLSv1.1
Ignoring unsupported cipher suite: TLS_DHE_RSA_WITH_AES_256_CBC_SHA256 for TLSv1.1
Ignoring unsupported cipher suite: TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 for TLSv1.1
%% No cached client session
update handshake state: client_hello[1]
upcoming handshake states: server_hello[2]
```

The connection to the server is made, and we see the initial ClientHello
message, which contains:

-   random information to initialize the cryptographic routines,
-   the SessionID, which if non-null, would be used in reestablishing a
    previous session,
-   the list of ciphersuites that the client requests,
-   and no compression algorithms.

This is followed by the output of various filters, such as encapsulating
the TLSv1.2 header into the SSLv2Hello header format (See
setEnabledProtocols()).

``` {.oac_no_warn dir="ltr"}
update handshake state: client_hello[1]
upcoming handshake states: server_hello[2]
*** ClientHello, TLSv1.2
RandomCookie:  random_bytes = {BA FA 1D F1 56 A3 7C FF B9 43 76 71 98 F5 A9 B4 0E 6B DF 7B 52 B8 F3 92 CC F4 C1 8A AA 71 8A 3F}
Session ID:  {}
Cipher Suites: [TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384, TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256, TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384, TLS_RSA_WITH_AES_256_GCM_SHA384, TLS_ECDH_ECDSA_WITH_AES_256_GCM_SHA384, TLS_ECDH_RSA_WITH_AES_256_GCM_SHA384, TLS_DHE_RSA_WITH_AES_256_GCM_SHA384, TLS_DHE_DSS_WITH_AES_256_GCM_SHA384, TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256, TLS_RSA_WITH_AES_128_GCM_SHA256, TLS_ECDH_ECDSA_WITH_AES_128_GCM_SHA256, TLS_ECDH_RSA_WITH_AES_128_GCM_SHA256, TLS_DHE_RSA_WITH_AES_128_GCM_SHA256, TLS_DHE_DSS_WITH_AES_128_GCM_SHA256, TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384, TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384, TLS_RSA_WITH_AES_256_CBC_SHA256, TLS_ECDH_ECDSA_WITH_AES_256_CBC_SHA384, TLS_ECDH_RSA_WITH_AES_256_CBC_SHA384, TLS_DHE_RSA_WITH_AES_256_CBC_SHA256, TLS_DHE_DSS_WITH_AES_256_CBC_SHA256, TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA, TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA, TLS_RSA_WITH_AES_256_CBC_SHA, TLS_ECDH_ECDSA_WITH_AES_256_CBC_SHA, TLS_ECDH_RSA_WITH_AES_256_CBC_SHA, TLS_DHE_RSA_WITH_AES_256_CBC_SHA, TLS_DHE_DSS_WITH_AES_256_CBC_SHA, TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256, TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256, TLS_RSA_WITH_AES_128_CBC_SHA256, TLS_ECDH_ECDSA_WITH_AES_128_CBC_SHA256, TLS_ECDH_RSA_WITH_AES_128_CBC_SHA256, TLS_DHE_RSA_WITH_AES_128_CBC_SHA256, TLS_DHE_DSS_WITH_AES_128_CBC_SHA256, TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA, TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA, TLS_RSA_WITH_AES_128_CBC_SHA, TLS_ECDH_ECDSA_WITH_AES_128_CBC_SHA, TLS_ECDH_RSA_WITH_AES_128_CBC_SHA, TLS_DHE_RSA_WITH_AES_128_CBC_SHA, TLS_DHE_DSS_WITH_AES_128_CBC_SHA, TLS_ECDHE_ECDSA_WITH_3DES_EDE_CBC_SHA, TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA, SSL_RSA_WITH_3DES_EDE_CBC_SHA, TLS_ECDH_ECDSA_WITH_3DES_EDE_CBC_SHA, TLS_ECDH_RSA_WITH_3DES_EDE_CBC_SHA, SSL_DHE_RSA_WITH_3DES_EDE_CBC_SHA, SSL_DHE_DSS_WITH_3DES_EDE_CBC_SHA, TLS_EMPTY_RENEGOTIATION_INFO_SCSV]
Compression Methods:  { 0 }
Extension elliptic_curves, curve names: {secp256r1, secp384r1, secp521r1, sect283k1, sect283r1, sect409k1, sect409r1, sect571k1, sect571r1, secp256k1}
Extension ec_point_formats, formats: [uncompressed]
Extension signature_algorithms, signature_algorithms: SHA512withECDSA, SHA512withRSA, SHA384withECDSA, SHA384withRSA, SHA256withECDSA, SHA256withRSA, SHA256withDSA, SHA1withECDSA, SHA1withRSA, SHA1withDSA
Extension server_name, server_name: [type=host_name (0), value=sc11152716.us.oracle.com]
Extension status_request_v2
CertStatusReqItemV2: ocsp_multi, OCSPStatusRequest
    ResponderIds: <EMPTY>
    Extensions: <EMPTY>
CertStatusReqItemV2: ocsp, OCSPStatusRequest
    ResponderIds: <EMPTY>
    Extensions: <EMPTY>
Extension status_request: ocsp, OCSPStatusRequest
    ResponderIds: <EMPTY>
    Extensions: <EMPTY>
***
main, WRITE: TLSv1.2 Handshake, length = 265
```

Section labeled \"\[Raw write\]\" represent the actual data sent to the
raw output object (in this case, an OutputStream).

``` {.oac_no_warn dir="ltr"}
[Raw write]: length = 270
0000: 16 03 03 01 09 01 00 01   05 03 03 BA FA 1D F1 56  ...............V
0010: A3 7C FF B9 43 76 71 98   F5 A9 B4 0E 6B DF 7B 52  ....Cvq.....k..R
0020: B8 F3 92 CC F4 C1 8A AA   71 8A 3F 00 00 64 C0 2C  ........q.?..d.,
...
```

After sending the initial ClientHello, we wait for the server\'s
response, a ServerHello. \"\[Raw read\]\" displays the raw data read
from the input device (InputStream), before any processing has been
performed.

``` {.oac_no_warn dir="ltr"}
[Raw read]: length = 5
0000: 16 03 03 16 A5                                     .....
[Raw read]: length = 1024
0000: 02 00 00 4D 03 03 5A 4E   F9 E3 0C C5 C3 FE B6 50  ...M..ZN.......P
0010: ED 3E 40 2D 5D 75 27 12   B7 C0 FB CA C5 DD 6E 79  .>@-]u'.......ny
0020: DB FF AE C8 32 63 20 5A   4E F9 E3 35 7F A1 8D A1  ....2c ZN..5....
...
main, READ: TLSv1.2 Handshake, length = 5797
```

The data is unpackaged, and if the message is in the SSL/TLS format, it
is parsed into a ServerHello. If you connected to a non-SSL/TLS socket
(plaintext?), the received data will not be in SSL/TLS format, and
you\'ll have problems connecting.

The ServerHello specifies several things:

-   The server\'s random data, also used to initialize the cryptographic
    algorithms,
-   the identifier of this session (if the client wants to try to rejoin
    this session using a different connection, it can send this ID in
    its ClientHello. If the client session ID equals the server session
    ID, an abbreviated handshake takes place, and the previously
    established parameters are used),
-   the selected cipher suite,
-   and the compression method (none in this case).

Lastly note that the ServerHello has specified that the connection
should use \"TLSv1.2\", rather than \"SSLv3.\"

``` {.oac_no_warn dir="ltr"}
check handshake state: server_hello[2]
*** ServerHello, TLSv1.2
RandomCookie:  random_bytes = {5A 4E F9 E3 0C C5 C3 FE B6 50 ED 3E 40 2D 5D 75 27 12 B7 C0 FB CA C5 DD 6E 79 DB FF AE C8 32 63}
Session ID:  {90, 78, 249, 227, 53, 127, 161, 141, 161, 33, 124, 107, 167, 128, 131, 252, 2, 170, 193, 168, 50, 40, 183, 150, 161, 217, 57, 214, 248, 78, 138, 158}
Cipher Suite: TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
Compression Method: 0
Extension renegotiation_info, renegotiated_connection: <empty>
***
%% Initialized:  [Session-2, TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256]
** TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
update handshake state: server_hello[2]
upcoming handshake states: server certificate[11]
upcoming handshake states: server_key_exchange[12](optional)
upcoming handshake states: certificate_request[13](optional)
upcoming handshake states: server_hello_done[14]
upcoming handshake states: client certificate[11](optional)
upcoming handshake states: client_key_exchange[16]
upcoming handshake states: certificate_verify[15](optional)
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
check handshake state: certificate[11]
update handshake state: certificate[11]
upcoming handshake states: server_key_exchange[12](optional)
upcoming handshake states: certificate_request[13](optional)
upcoming handshake states: server_hello_done[14]
upcoming handshake states: client certificate[11](optional)
upcoming handshake states: client_key_exchange[16]
upcoming handshake states: certificate_verify[15](optional)
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
```

The server next identifies itself to the client by passing a Certificate
chain. In this example, we have a certificate for the subject
\"localhost\", signed by the issuer \"Ficticious Widgets, Inc.\". We
know that \"Ficticious Widgets, Inc.\" is a trusted CA, so if the
certificate chain verifies correctly by our X509TrustManager, we can
accept this connection.

There are many different ways of establishing trust, so if the default
X509TrustManager is not doing the types of trust management you need,
you can supply your own X509TrustManager to the SSLContext.

``` {.oac_no_warn dir="ltr"}
*** Certificate chain
chain [0] = [
[
  Version: V1
  Subject: CN=localhost, OU=Widget Development Group, O="Ficticious Widgets, Inc.", L=Sunnyvale, ST=CA, C=US
  Signature Algorithm: MD5withRSA, OID = 1.2.840.113549.1.1.4

  Key:  Sun RSA public key, 1024 bits
  modulus: 143033747930138472247486887271140056230073515145002178273967677351609615363370290762769276637999437478831560066065849659757291378862662902990827165994331807749557591488695685710009935444457827978925129834206313905790623318272163063103561366855275108040861594659236689181320854743400330625121610498756440722549
  public exponent: 65537
  Validity: [From: Thu Jul 22 18:48:38 EDT 2004,
               To: Sun May 22 18:48:38 EDT 2011]
  Issuer: CN=localhost, OU=Widget Development Group, O="Ficticious Widgets, Inc.", L=Sunnyvale, ST=CA, C=US
  SerialNumber: [    41004446]

]
  Algorithm: [MD5withRSA]
  Signature:
0000: BB 83 25 91 F3 8F 20 B5   C3 BD E4 FE B1 AB E8 CD  ..%... .........
0010: 6F 5C C4 13 86 E9 AB 3E   97 DC AC BF D6 5A 38 42  o\.....>.....Z8B
0020: 39 70 CD 56 F8 82 7B B7   D7 9F 2C 40 52 2B 32 37  9p.V......,@R+27
0030: 5E B0 ED 50 5D D4 F2 5A   80 C6 8D FD 01 FA 8E 2B  ^..P]..Z.......+
0040: 4E 4E DB D8 96 75 CC BE   B7 69 49 22 EC 8A B1 58  NN...u...iI"...X
0050: E6 7E A9 9F 0B 4F 77 4E   EF 89 B0 8D 98 B9 2E E0  .....OwN........
0060: 4D 08 26 13 C5 2E 12 6B   7D 64 4A C9 89 C5 A6 D9  M.&....k.dJ.....
0070: CF 85 AB 27 D3 C9 CE 4C   85 0A 5E B7 B8 0E B1 63  ...'...L..^....c

]
```

We recognize this cert! We can trust it, and continue on with the
handshake.

``` {.oac_no_warn dir="ltr"}
***
Found trusted certificate:
[
[
  Version: V1
  Subject: CN=localhost, OU=Widget Development Group, O="Ficticious Widgets, Inc.", L=Sunnyvale, ST=CA, C=US
  Signature Algorithm: MD5withRSA, OID = 1.2.840.113549.1.1.4

  Key:  Sun RSA public key, 1024 bits
  modulus: 143033747930138472247486887271140056230073515145002178273967677351609615363370290762769276637999437478831560066065849659757291378862662902990827165994331807749557591488695685710009935444457827978925129834206313905790623318272163063103561366855275108040861594659236689181320854743400330625121610498756440722549
  public exponent: 65537
  Validity: [From: Thu Jul 22 18:48:38 EDT 2004,
               To: Sun May 22 18:48:38 EDT 2011]
  Issuer: CN=localhost, OU=Widget Development Group, O="Ficticious Widgets, Inc.", L=Sunnyvale, ST=CA, C=US
  SerialNumber: [    41004446]

]
  Algorithm: [MD5withRSA]
  Signature:
0000: BB 83 25 91 F3 8F 20 B5   C3 BD E4 FE B1 AB E8 CD  ..%... .........
0010: 6F 5C C4 13 86 E9 AB 3E   97 DC AC BF D6 5A 38 42  o\.....>.....Z8B
0020: 39 70 CD 56 F8 82 7B B7   D7 9F 2C 40 52 2B 32 37  9p.V......,@R+27
0030: 5E B0 ED 50 5D D4 F2 5A   80 C6 8D FD 01 FA 8E 2B  ^..P]..Z.......+
0040: 4E 4E DB D8 96 75 CC BE   B7 69 49 22 EC 8A B1 58  NN...u...iI"...X
0050: E6 7E A9 9F 0B 4F 77 4E   EF 89 B0 8D 98 B9 2E E0  .....OwN........
0060: 4D 08 26 13 C5 2E 12 6B   7D 64 4A C9 89 C5 A6 D9  M.&....k.dJ.....
0070: CF 85 AB 27 D3 C9 CE 4C   85 0A 5E B7 B8 0E B1 63  ...'...L..^....c

]
check handshake state: server_key_exchange[12]
update handshake state: server_key_exchange[12]
upcoming handshake states: certificate_request[13](optional)
upcoming handshake states: server_hello_done[14]
upcoming handshake states: client certificate[11](optional)
upcoming handshake states: client_key_exchange[16]
upcoming handshake states: certificate_verify[15](optional)
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
*** ECDH ServerKeyExchange
Signature Algorithm SHA512withRSA
Server key: Sun EC public key, 256 bits
  public x coord: 63946569761028817730470946709618245239665208702310658540834640572976024458986
  public y coord: 95117373197468111348087774631874920178563710193262620110729461870051247081115
  parameters: secp256r1 [NIST P-256, X9.62 prime256v1] (1.2.840.10045.3.1.7)
check handshake state: certificate_request[13]
```

The server is asking the client to identify itself with a X509
certificate subject having the common name (CN=) \"Duke\". The server\'s
X509TrustManager has the option of rejecting any credentials provided by
the client (or lack thereof). In a real-world situation, you\'d probably
use a certificate signed by a CA, and the list of trusted CA\'s would be
included in this message instead.

``` {.oac_no_warn dir="ltr"}
*** CertificateRequest
Cert Types: RSA, DSS, ECDSA
Supported Signature Algorithms: SHA512withECDSA, SHA512withRSA, SHA384withECDSA, SHA384withRSA, SHA256withECDSA, SHA256withRSA, Unknown (hash:0x3, signature:0x3), Unknown (hash:0x3, signature:0x1), SHA1withECDSA, SHA1withRSA, SHA1withDSA, MD5withRSA
Cert Authorities:
<CN=VeriSign Class 3 Public Primary Certification Authority - G3, OU="(c) 1999 VeriSign, Inc. - For authorized use only", OU=VeriSign Trust Network, O="VeriSign, Inc.", C=US>
<CN=VeriSign Class 2 Public Primary Certification Authority - G3, OU="(c) 1999 VeriSign, Inc. - For authorized use only", OU=VeriSign Trust Network, O="VeriSign, Inc.", C=US>
<OU=Equifax Secure eBusiness CA-2, O=Equifax Secure, C=US>
<CN=Equifax Secure eBusiness CA-1, O=Equifax Secure Inc., C=US>
<EMAILADDRESS=server-certs@thawte.com, CN=Thawte Server CA, OU=Certification Services Division, O=Thawte Consulting cc, L=Cape Town, ST=Western Cape, C=ZA>
<CN=Duke, OU=Java Software, O="Sun Microsystems, Inc.", L=Cupertino, ST=CA, C=US>
<CN=VeriSign Class 1 Public Primary Certification Authority - G3, OU="(c) 1999 VeriSign, Inc. - For authorized use only", OU=VeriSign Trust Network, O="VeriSign, Inc.", C=US>
<OU=Class 2 Public Primary Certification Authority, O="VeriSign, Inc.", C=US>
<CN=Baltimore CyberTrust Code Signing Root, OU=CyberTrust, O=Baltimore, C=IE>
<EMAILADDRESS=personal-freemail@thawte.com, CN=Thawte Personal Freemail CA, OU=Certification Services Division, O=Thawte Consulting, L=Cape Town, ST=Western Cape, C=ZA>
<OU=VeriSign Trust Network, OU="(c) 1998 VeriSign, Inc. - For authorized use only", OU=Class 3 Public Primary Certification Authority - G2, O="VeriSign, Inc.", C=US>
<CN=Equifax Secure Global eBusiness CA-1, O=Equifax Secure Inc., C=US>
<EMAILADDRESS=personal-premium@thawte.com, CN=Thawte Personal Premium CA, OU=Certification Services Division, O=Thawte Consulting, L=Cape Town, ST=Western Cape, C=ZA>
<EMAILADDRESS=personal-basic@thawte.com, CN=Thawte Personal Basic CA, OU=Certification Services Division, O=Thawte Consulting, L=Cape Town, ST=Western Cape, C=ZA>
<CN=GTE CyberTrust Root, O=GTE Corporation, C=US>
<OU=Class 3 Public Primary Certification Authority, O="VeriSign, Inc.", C=US>
<CN=localhost, OU=Widget Development Group, O="Ficticious Widgets, Inc.", L=Sunnyvale, ST=CA, C=US>
<CN=Entrust.net Client Certification Authority, OU=(c) 2000 Entrust.net Limited, OU=www.entrust.net/GCCA_CPS incorp. by ref. (limits liab.), O=Entrust.net>
<CN=GTE CyberTrust Global Root, OU="GTE CyberTrust Solutions, Inc.", O=GTE Corporation, C=US>
<CN=Entrust.net Client Certification Authority, OU=(c) 1999 Entrust.net Limited, OU=www.entrust.net/Client_CA_Info/CPS incorp. by ref. limits liab., O=Entrust.net, C=US>
<OU=Equifax Secure Certificate Authority, O=Equifax, C=US>
<CN=Entrust.net Secure Server Certification Authority, OU=(c) 2000 Entrust.net Limited, OU=www.entrust.net/SSL_CPS incorp. by ref. (limits liab.), O=Entrust.net>
<OU=Secure Server Certification Authority, O="RSA Data Security, Inc.", C=US>
<OU=VeriSign Trust Network, OU="(c) 1998 VeriSign, Inc. - For authorized use only", OU=Class 2 Public Primary Certification Authority - G2, O="VeriSign, Inc.", C=US>
<EMAILADDRESS=premium-server@thawte.com, CN=Thawte Premium Server CA, OU=Certification Services Division, O=Thawte Consulting cc, L=Cape Town, ST=Western Cape, C=ZA>
<CN=GeoTrust Global CA, O=GeoTrust Inc., C=US>
<OU=VeriSign Trust Network, OU="(c) 1998 VeriSign, Inc. - For authorized use only", OU=Class 1 Public Primary Certification Authority - G2, O="VeriSign, Inc.", C=US>
<CN=Baltimore CyberTrust Root, OU=CyberTrust, O=Baltimore, C=IE>
<CN=Entrust.net Secure Server Certification Authority, OU=(c) 1999 Entrust.net Limited, OU=www.entrust.net/CPS incorp. by ref. (limits liab.), O=Entrust.net, C=US>
<OU=Class 1 Public Primary Certification Authority, O="VeriSign, Inc.", C=US>
<CN=Entrust.net Certification Authority (2048), OU=(c) 1999 Entrust.net Limited, OU=www.entrust.net/CPS_2048 incorp. by ref. (limits liab.), O=Entrust.net>
<CN=GTE CyberTrust Root 5, OU="GTE CyberTrust Solutions, Inc.", O=GTE Corporation, C=US>
update handshake state: certificate_request[13]
upcoming handshake states: server_hello_done[14]
upcoming handshake states: client certificate[11](optional)
upcoming handshake states: client_key_exchange[16]
upcoming handshake states: certificate_verify[15](optional)
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
check handshake state: server_hello_done[14]
update handshake state: server_hello_done[14]
upcoming handshake states: client certificate[11](optional)
upcoming handshake states: client_key_exchange[16]
upcoming handshake states: certificate_verify[15](optional)
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
*** ServerHelloDone
```

We need to send client credentials back to the server, so the client\'s
X509KeyManager is now consulted. We look for a match between the list of
accepted issuers (above), and the certificates we have in our KeyStore.
In this case (luckily?), there is a match: we have credentials for
\"duke\". It\'s now up to the server\'s X509TrustManager to decide
whether to accept these credentials.

``` {.oac_no_warn dir="ltr"}
matching alias: duke
*** Certificate chain
chain [0] = [
[
  Version: V1
  Subject: CN=Duke, OU=Java Software, O="Sun Microsystems, Inc.", L=Cupertino, ST=CA, C=US
  Signature Algorithm: MD5withRSA, OID = 1.2.840.113549.1.1.4

  Key:  Sun RSA public key, 1024 bits
  modulus: 134968166047563266914058280571444028986498087544923991226919517667593269213420979048109900052353578998293280426361122296881234393722020704208851688212064483570055963805034839797994154526862998272017486468599962268346037652120279791547218281230795146025359480589335682217749874703510467348902637769973696151441
  public exponent: 65537
  Validity: [From: Tue May 22 19:46:46 EDT 2001,
               To: Sun May 22 19:46:46 EDT 2011]
  Issuer: CN=Duke, OU=Java Software, O="Sun Microsystems, Inc.", L=Cupertino, ST=CA, C=US
  SerialNumber: [    3b0afa66]

]
  Algorithm: [MD5withRSA]
  Signature:
0000: 5F B5 62 E9 A0 26 1D 8E   A2 7E 7C 02 08 36 3A 3E  _.b..&.......6:>
0010: C9 C2 45 03 DD F9 BC 06   FC 25 CF 30 92 91 B1 4E  ..E......%.0...N
0020: 62 17 08 48 14 68 80 CF   DD 89 11 EA 92 7F CE DD  b..H.h..........
0030: B4 FD 12 A8 71 C7 9E D7   C3 D0 E3 BD BB DE 20 92  ....q......... .
0040: C2 3B C8 DE CB 25 23 C0   8B B6 92 B9 0B 64 80 63  .;...%#......d.c
0050: D9 09 25 2D 7A CF 0A 31   B6 E9 CA C1 37 93 BC 0D  ..%-z..1....7...
0060: 4E 74 95 4F 58 31 DA AC   DF D8 BD 89 BD AF EC C8  Nt.OX1..........
0070: 2D 18 A2 BC B2 15 4F B7   28 6F D3 00 E1 72 9B 6C  -.....O.(o...r.l

]
***
update handshake state: certificate[11]
upcoming handshake states: client_key_exchange[16]
upcoming handshake states: certificate_verify[15](optional)
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
*** ECDHClientKeyExchange
ECDH Public value:  { 4, 122, 237, 144, 182, 238, 209, 254, 65, 55, 177, 247, 57, 161, 72, 21, 29, 94, 215, 195, 63, 129, 193, 247, 74, 136, 229, 16, 8, 243, 189, 119, 9, 138, 167, 148, 227, 237, 217, 160, 220, 105, 193, 152, 164, 23, 104, 56, 164, 67, 49, 118, 182, 237, 49, 113, 35, 239, 236, 170, 58, 208, 168, 84, 90 }
update handshake state: client_key_exchange[16]
upcoming handshake states: certificate_verify[15](optional)
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
```

In the case of this particular cipher suite, we must now pass a message
called a ECDHClientKeyExchange, which helps establish a shared secret
between the two parties.

All of this data is eventually collected and written to the raw device.

``` {.oac_no_warn dir="ltr"}
*** ECDHClientKeyExchange
ECDH Public value:  { 4, 122, 237, 144, 182, 238, 209, 254, 65, 55, 177, 247, 57, 161, 72, 21, 29, 94, 215, 195, 63, 129, 193, 247, 74, 136, 229, 16, 8, 243, 189, 119, 9, 138, 167, 148, 227, 237, 217, 160, 220, 105, 193, 152, 164, 23, 104, 56, 164, 67, 49, 118, 182, 237, 49, 113, 35, 239, 236, 170, 58, 208, 168, 84, 90 }
update handshake state: client_key_exchange[16]
upcoming handshake states: certificate_verify[15](optional)
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
main, WRITE: TLSv1.2 Handshake, length = 690
[Raw write]: length = 695
0000: 16 03 03 02 B2 0B 00 02   68 00 02 65 00 02 62 30  ........h..e..b0
0010: 82 02 5E 30 82 01 C7 02   04 3B 0A FA 66 30 0D 06  ..^0.....;..f0..
0020: 09 2A 86 48 86 F7 0D 01   01 04 05 00 30 76 31 0B  .*.H........0v1.
...
```

At this point, we have everything we need to generate the actual
secrets.

``` {.oac_no_warn dir="ltr"}
SESSION KEYGEN:
PreMaster Secret:
0000: 7B 30 E5 1B 16 56 24 A8   48 A1 14 22 18 80 6B 37  .0...V$.H.."..k7
0010: 33 87 5B AC 88 7E 3A AF   75 62 30 48 DA 6F 52 4E  3.[...:.ub0H.oRN
CONNECTION KEYGEN:
Client Nonce:
0000: BA FA 1D F1 56 A3 7C FF   B9 43 76 71 98 F5 A9 B4  ....V....Cvq....
0010: 0E 6B DF 7B 52 B8 F3 92   CC F4 C1 8A AA 71 8A 3F  .k..R........q.?
Server Nonce:
0000: 5A 4E F9 E3 0C C5 C3 FE   B6 50 ED 3E 40 2D 5D 75  ZN.......P.>@-]u
0010: 27 12 B7 C0 FB CA C5 DD   6E 79 DB FF AE C8 32 63  '.......ny....2c
Master Secret:
0000: A0 DD C7 3A 6C CD CF 01   9E 8D 38 E6 74 D0 93 51  ...:l.....8.t..Q
0010: CD E4 DB AE 3C BB 64 5D   3D 9D 1C 24 14 A0 9E B8  ....<.d]=..$....
0020: 97 6B 8E 74 C5 6A 07 53   8D B0 5F CE 63 E6 2A B2  .k.t.j.S.._.c.*.
... no MAC keys used for this cipher
Client write key:
0000: 03 81 01 4E 4B 73 AC 71   A7 FC EF 32 99 11 39 D7  ...NKs.q...2..9.
Server write key:
0000: C0 41 60 66 69 0A E0 62   AE CC CA 59 55 84 13 BE  .A`fi..b...YU...
Client write IV:
0000: 92 A8 F6 29                                        ...)
Server write IV:
0000: A3 81 9D 8A           
```

Send a quick confirmation to the server verifying that we know the
private key corresponding to the client certificate we just sent.

``` {.oac_no_warn dir="ltr"}
*** CertificateVerify
Signature Algorithm SHA512withRSA
update handshake state: certificate_verify[15]
upcoming handshake states: client change_cipher_spec[-1]
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
main, WRITE: TLSv1.2 Handshake, length = 136
[Raw write]: length = 141
0000: 16 03 03 00 88 0F 00 00   84 06 01 00 80 21 D7 EB  .............!..
0010: 85 55 D2 18 10 34 4A 67   62 35 67 E0 FD D7 76 0F  .U...4Jgb5g...v.
0020: 72 4D 12 C5 9D 9D 2A DF   AD 61 8D 8E E0 4D 20 47  rM....*..a...M G
0030: F9 19 D5 AC A8 40 25 8E   C3 71 E9 07 E1 04 C8 A8  .....@%..q......
0040: 42 20 2D 9C EB 4A 64 8B   20 BD 72 B5 BB 75 88 8B  B -..Jd. .r..u..
0050: FF 63 13 B5 20 8B F3 93   3C 55 BD A0 E4 9B B1 C0  .c.. ...<U......
0060: 26 14 32 79 29 C9 C4 63   4F 95 F5 8F B5 56 B6 96  &.2y)..cO....V..
0070: B3 E3 72 CC 6A A2 C7 3F   7D DD 54 9B FF 1E 66 2D  ..r.j..?..T...f-
0080: 2C 8F 87 3E 6D 95 A0 61   B3 72 6B C9 36           ,..>m..a.rk.6
update handshake state: change_cipher_spec
upcoming handshake states: client finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
```

Almost finished! Tell the server we\'re changing to the newly
established cipher suite. All further messages will be encrypted using
the parameters we just established. We send an encrypted Finished
message to verify everything worked.

``` {.oac_no_warn dir="ltr"}
main, WRITE: TLSv1.2 Change Cipher Spec, length = 1
[Raw write]: length = 6
0000: 14 03 03 00 01 01                                  ......
*** Finished
verify_data:  { 203, 239, 43, 159, 111, 5, 204, 127, 182, 48, 181, 121 }
***
update handshake state: finished[20]
upcoming handshake states: server change_cipher_spec[-1]
upcoming handshake states: server finished[20]
main, WRITE: TLSv1.2 Handshake, length = 24
Padded plaintext before ENCRYPTION:  len = 16
0000: 14 00 00 0C CB EF 2B 9F   6F 05 CC 7F B6 30 B5 79  ......+.o....0.y
```

Note next that when the message above is actually written to the raw
output device (following the 5 bytes of header information), the message
is now encrypted.

``` {.oac_no_warn dir="ltr"}
[Raw write]: length = 45
0000: 16 03 03 00 28 00 00 00   00 00 00 00 00 A9 56 B7  ....(.........V.
0010: 91 8D A5 4E 3E AD 9F 68   7D 8F 5D 69 C3 B6 63 C9  ...N>..h..]i..c.
0020: 83 CC D5 1C 1E A2 09 A4   5F 19 38 2B 35           ........_.8+5
```

We now wait for the server to send the same (Change Cipher
Spec/Finshed), so we can know it completed negotiations successfully.

``` {.oac_no_warn dir="ltr"}
[Raw read]: length = 5
0000: 14 03 03 00 01                                     .....
[Raw read]: length = 1
0000: 01                                                 .
main, READ: TLSv1.2 Change Cipher Spec, length = 1
update handshake state: change_cipher_spec
upcoming handshake states: server finished[20]
[Raw read]: length = 5
0000: 16 03 03 00 28                                     ....(
[Raw read]: length = 40
0000: 00 00 00 00 00 00 00 00   7C 67 B6 32 AC 15 50 98  .........g.2..P.
0010: FE A6 4E E1 A0 4B E8 D3   84 DE 82 02 32 DF 54 13  ..N..K......2.T.
0020: 57 24 66 55 4D 49 92 FB                            W$fUMI..
main, READ: TLSv1.2 Handshake, length = 40
Padded plaintext after DECRYPTION:  len = 16
0000: 14 00 00 0C 3A 78 03 E5   A4 9A 9D ED 9D 0E 78 55  ....:x........xU
check handshake state: finished[20]
update handshake state: finished[20]
*** Finished
verify_data:  { 58, 120, 3, 229, 164, 154, 157, 237, 157, 14, 120, 85 }
***
```

Everything completed successfully! Let\'s cache the established session
in case we want to reestablish this session after this connection is
dropped.

At this point, a SSL/TLS client should examine the credentials of the
peer to make sure that it is communicating with the expected server. A
HttpsURLConnection would check the hostname and call HostnameVerifier if
there was a problem, but the raw SSLSocket doesn\'t. This verification
should be done by hand, but we\'re ignoring this for now.

So, after all that, we\'re finally ready to exchange application data.
We send a \"GET /index.html HTTP1.0\" command.

``` {.oac_no_warn dir="ltr"}
%% Cached client session: [Session-2, TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256]
main, WRITE: TLSv1.2 Application Data, length = 36
Padded plaintext before ENCRYPTION:  len = 28
0000: 47 45 54 20 2F 69 6E 64   65 78 2E 68 74 6D 6C 20  GET /index.html 
0010: 48 54 54 50 2F 31 2E 30   0D 0A 0D 0A              HTTP/1.0....
```

Note again the data over the wire is encrypted (skipping the 5 header
bytes).

``` {.oac_no_warn dir="ltr"}
[Raw write]: length = 57
0000: 17 03 03 00 34 00 00 00   00 00 00 00 01 62 BA 68  ....4........b.h
0010: 66 BB 0E FC 6D C4 13 43   C5 98 A1 EC 73 96 0C 28  f...m..C....s..(
0020: 72 4F BB FD 44 85 D5 03   40 82 0B F8 D3 9B B2 4A  rO..D...@......J
0030: 07 6B 0A B8 90 8F DC 82   41                       .k......A
```

We get the application data back. First the HTTPS header, then the
actual data.

``` {.oac_no_warn dir="ltr"}
[Raw read]: length = 5
0000: 17 03 03 00 5A                                     ....Z
[Raw read]: length = 90
0000: 00 00 00 00 00 00 00 01   C4 87 18 10 4F 64 C2 B0  ............Od..
0010: A3 CE 53 C6 3D 0C 0C 5E   E6 FE D2 05 64 39 C6 5C  ..S.=..^....d9.\
0020: BC BE 1B B2 C3 5D E0 5C   B9 34 AD B7 E3 2D 79 08  .....].\.4...-y.
0030: B0 88 D6 33 89 46 23 4C   4D A0 9D 6C AA 79 3C 61  ...3.F#LM..l.y<a
0040: 27 39 65 7D 91 6C 08 C4   FB DD 1F 27 3D 3F 53 D1  '9e..l.....'=?S.
0050: 2A 7C 26 5F 6A 11 05 F4   FF 6B                    *.&_j....k
main, READ: TLSv1.2 Application Data, length = 90
Padded plaintext after DECRYPTION:  len = 66
0000: 48 54 54 50 2F 31 2E 30   20 32 30 30 20 4F 4B 0D  HTTP/1.0 200 OK.
0010: 0A 43 6F 6E 74 65 6E 74   2D 4C 65 6E 67 74 68 3A  .Content-Length:
0020: 20 32 35 37 37 0D 0A 43   6F 6E 74 65 6E 74 2D 54   2577..Content-T
0030: 79 70 65 3A 20 74 65 78   74 2F 68 74 6D 6C 0D 0A  ype: text/html..
0040: 0D 0A                                              ..
HTTP/1.0 200 OK
Content-Length: 2577
Content-Type: text/html

[Raw read]: length = 5
0000: 17 03 03 0A 29                                     ....)
[Raw read]: length = 1024
...
[Raw read]: length = 1024
...
[Raw read]: length = 553
...
main, READ: TLSv1.2 Application Data, length = 2601
Padded plaintext after DECRYPTION:  len = 2577

0000: 3C 21 44 4F 43 54 59 50   45 20 68 74 6D 6C 20 50  <!DOCTYPE html P
0010: 55 42 4C 49 43 20 22 2D   2F 2F 57 33 43 2F 2F 44  UBLIC "-//W3C//D
0020: 54 44 20 58 48 54 4D 4C   20 31 2E 30 20 54 72 61  TD XHTML 1.0 Tra
0030: 6E 73 69 74 69 6F 6E 61   6C 2F 2F 45 4E 22 0A 20  nsitional//EN". 
0040: 20 20 20 22 68 74 74 70   3A 2F 2F 77 77 77 2E 77     "http://www.w
0050: 33 2E 6F 72 67 2F 54 52   2F 78 68 74 6D 6C 31 2F  3.org/TR/xhtml1/
0060: 44 54 44 2F 78 68 74 6D   6C 31 2D 74 72 61 6E 73  DTD/xhtml1-trans
0070: 69 74 69 6F 6E 61 6C 2E   64 74 64 22 3E 0A 3C 68  itional.dtd">.<h
0080: 74 6D 6C 20 6C 61 6E 67   3D 22 65 6E 2D 55 53 22  tml lang="en-US"
0090: 20 78 6D 6C 6E 73 3D 22   68 74 74 70 3A 2F 2F 77   xmlns="http://w
00A0: 77 77 2E 77 33 2E 6F 72   67 2F 31 39 39 39 2F 78  ww.w3.org/1999/x
00B0: 68 74 6D 6C 22 20 78 6D   6C 3A 6C 61 6E 67 3D 0A  html" xml:lang=.
00C0: 22 65 6E 2D 55 53 22 3E   0A 3C 68 65 61 64 3E 0A  "en-US">.<head>.
00D0: 3C 74 69 74 6C 65 3E 4A   53 53 45 20 53 61 6D 70  <title>JSSE Samp
00E0: 6C 65 20 43 6F 64 65 3C   2F 74 69 74 6C 65 3E 0A  le Code</title>.
...
0A00: 0A 3C 2F 62 6F 64 79 3E   0A 3C 2F 68 74 6D 6C 3E  .</body>.</html>
0A10: 0A                                                 .
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html lang="en-US" xmlns="http://www.w3.org/1999/xhtml" xml:lang=
"en-US">
<head>
<title>JSSE Sample Code</title>
</head>
<body>
<center>
<h1>JSSE Sample Code</h1>
</center>
<p>This directory contains subdirectories with JSSE sample files.</p>
...
</body>
</html>
```

Read from the socket again to see if there is any more data. We get a
close\_notify message, which means this connection is shutting down
properly. We send our own in turn, then close the socket.

``` {.oac_no_warn dir="ltr"}
[Raw read]: length = 5
0000: 15 03 03 00 1A                                     .....
[Raw read]: length = 26
0000: 00 00 00 00 00 00 00 03   6E D8 FA E8 B7 A7 01 7F  ........n.......
0010: EB C1 88 DC 30 34 BC 57   31 6D                    ....04.W1m
main, READ: TLSv1.2 Alert, length = 26
Padded plaintext after DECRYPTION:  len = 2
0000: 01 00                                              ..
main, RECV TLSv1.2 ALERT:  warning, close_notify
main, called closeInternal(false)
main, SEND TLSv1.2 ALERT:  warning, description = close_notify
main, WRITE: TLSv1.2 Alert, length = 10
Padded plaintext before ENCRYPTION:  len = 2
0000: 01 00                                              ..
[Raw write]: length = 31
0000: 15 03 03 00 1A 00 00 00   00 00 00 00 02 AA B8 0A  ................
0010: A1 3F 72 58 22 71 07 0B   83 DD 65 8B 6F 78 3B     .?rX"q....e.ox;
main, called closeSocket(false)
main, called close()
main, called closeInternal(true)
main, called close()
main, called closeInternal(true)
main, called close()
main, called closeInternal(true)
```

</div>
<!-- class="section" -->

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-0573BCE4-05C4-429C-8ECC-3D3D8CA807F4}

Code Examples {#JSSEC-GUID-0573BCE4-05C4-429C-8ECC-3D3D8CA807F4 .sect2}
-------------

<div>
The following code examples are included in this section:

<div class="section">
Topics

-   [Converting an Unsecure Socket to a Secure
    Socket](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AB802E5F-07CE-468D-AC7C-7EBCAAE119AD "Code examples that illustrate how to use JSSE to convert an unsecure socket connection to a secure socket connection. The code samples are excerpted from the book Java SE 6 Network Security by Marco Pistoia, et. al.")

-   [Running the JSSE Sample
    Code](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA "The JSSE sample programs illustrate how to use JSSE.")

-   [Creating a Keystore to Use with
    JSSE](java-secure-socket-extension-jsse-reference-guide.htm#GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F "The procedure as to how you can use the keytool utility to create a simple PKCS12 keystore suitable for use with JSSE.")

-   [Using the Server Name Indication (SNI)
    Extension](java-secure-socket-extension-jsse-reference-guide.htm#GUID-63945B45-E909-483F-B3A9-E26586737383)

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-AB802E5F-07CE-468D-AC7C-7EBCAAE119AD}

### Converting an Unsecure Socket to a Secure Socket {#JSSEC-GUID-AB802E5F-07CE-468D-AC7C-7EBCAAE119AD .sect3}

<div>
Code examples that illustrate how to use JSSE to convert an unsecure
socket connection to a secure socket connection. The code samples are
excerpted from the book Java SE 6 Network Security by Marco Pistoia, et.
al.

[Example
8-26](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AB802E5F-07CE-468D-AC7C-7EBCAAE119AD__SOCKETEXAMPLEWITHOUTSSL-6B1057A9)
shows sample code that can be used to set up communication between a
client and a server using unsecure sockets. This code is then modified
in [Example
8-27](java-secure-socket-extension-jsse-reference-guide.htm#GUID-AB802E5F-07CE-468D-AC7C-7EBCAAE119AD__SOCKETEXAMPLEWITHSSL-6B10547E)
to use JSSE to set up secure socket communication.

<div class="example" id="GUID-AB802E5F-07CE-468D-AC7C-7EBCAAE119AD__SOCKETEXAMPLEWITHOUTSSL-6B1057A9">
Example 8-26 Socket Example Without SSL

The following examples demonstrates server-side and client-side code for
setting up an unsecure socket connection.

In a Java program that acts as a server and communicates with a client
using sockets, the socket communication is set up with code similar to
the following:

``` {.codeblock dir="ltr"}
    import java.io.*;
    import java.net.*;
    
    . . .
    
    int port = availablePortNumber;
    
    ServerSocket s;
    
    try {
        s = new ServerSocket(port);
        Socket c = s.accept();
    
        OutputStream out = c.getOutputStream();
        InputStream in = c.getInputStream();
    
        // Send messages to the client through
        // the OutputStream
        // Receive messages from the client
        // through the InputStream
    } catch (IOException e) { }
```

The client code to set up communication with a server using sockets is
similar to the following:

``` {.codeblock dir="ltr"}
    import java.io.*;
    import java.net.*;
    
    . . .
    
    int port = availablePortNumber;
    String host = "hostname";
    
    try {
        s = new Socket(host, port);
    
        OutputStream out = s.getOutputStream();
        InputStream in = s.getInputStream();
    
        // Send messages to the server through
        // the OutputStream
        // Receive messages from the server
        // through the InputStream
    } catch (IOException e) { }
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-AB802E5F-07CE-468D-AC7C-7EBCAAE119AD__SOCKETEXAMPLEWITHSSL-6B10547E">
Example 8-27 Socket Example with SSL

The following examples demonstrate server-side and client-side code for
setting up a secure socket connection.

In a Java program that acts as a server and communicates with a client
using secure sockets, the socket communication is set up with code
similar to the following. Differences between this program and the one
for communication using unsecure sockets are highlighted in bold.

``` {.codeblock dir="ltr"}
    import java.io.*;
    import javax.net.ssl.*;
    
    . . .
    
    int port = availablePortNumber;
    
    SSLServerSocket s;
    
    try {
        SSLServerSocketFactory sslSrvFact =
            (SSLServerSocketFactory)SSLServerSocketFactory.getDefault();
        s = (SSLServerSocket)sslSrvFact.createServerSocket(port);
    
        SSLSocket c = (SSLSocket)s.accept();
    
        OutputStream out = c.getOutputStream();
        InputStream in = c.getInputStream();
    
        // Send messages to the client through
        // the OutputStream
        // Receive messages from the client
        // through the InputStream
    }
    
    catch (IOException e) {
    }
```

The client code to set up communication with a server using secure
sockets is similar to the following, where differences with the unsecure
version are highlighted in bold:

``` {.codeblock dir="ltr"}
    import java.io.*;
    import javax.net.ssl.*;
    
    . . .
    
    int port = availablePortNumber;
    String host = "hostname";
    
    try {
        SSLSocketFactory sslFact =
            (SSLSocketFactory)SSLSocketFactory.getDefault();
        SSLSocket s = (SSLSocket)sslFact.createSocket(host, port);
    
        OutputStream out = s.getOutputStream();
        InputStream in = s.getInputStream();
    
        // Send messages to the server through
        // the OutputStream
        // Receive messages from the server
        // through the InputStream
    }
    
    catch (IOException e) {
    }
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA}

### Running the JSSE Sample Code {#JSSEC-GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA .sect3}

<div>
The JSSE sample programs illustrate how to use JSSE.

<div class="section">
-   [Sample Code Illustrating a Secure Socket Connection Between a
    Client and a
    Server](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGASECURESOCKET-82CE8421)
-   [Sample Code Illustrating HTTPS
    Connections](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGHTTPSCONNECTI-7D238310)
-   [Sample Code Illustrating a Secure RMI
    Connection](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGASECURERMICON-F9A2C933)
-   [Sample Code Illustrating the Use of an
    SSLEngine](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGTHEUSEOFANSSL-7D23A601)

When you use the sample code, be aware that the sample programs are
designed to illustrate how to use JSSE. They are not designed to be
robust applications.

<div class="p">
<div class="infoboxnote" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__GUID-D989BF26-8A0F-46AD-A2E6-83C41C9642B3">
Note:

Setting up secure communications involves complex algorithms. The sample
programs provide no feedback during the setup process. When you run the
programs, be patient: you may not see any output for a while. If you run
the programs with the `javax.net.debug`{.codeph} system property set to
`all`{.codeph}, you will see more feedback. For an introduction to
reading this debug information, see [Debugging SSL/TLS
Connections](java-secure-socket-extension-jsse-reference-guide.htm#GUID-4D421910-C36D-40A2-8BA2-7D42CCBED3C6 "Understanding SSL/TLS connection problems can sometimes be difficult, especially when it is not clear what messages are actually being sent and received. JSSE has a built-in debug facility and is activated by the System property javax.net.debug.").

</div>
</div>
</div>
<!-- class="section" -->

<div class="section">
Where to Find the Sample Code

<span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> lists all the sample code files and
text files. That page also provides a link to a ZIP file that you can
download to obtain all the sample code files.

The following sections describe the samples.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGASECURESOCKET-82CE8421">
Sample Code Illustrating a Secure Socket Connection Between a Client and
a Server

The sample programs in the `samples/sockets`{.codeph} directory
illustrate how to set up a secure socket connection between a client and
a server.

When running the sample client programs, you can communicate with an
existing server, such as a web server, or you can communicate with the
sample server program, `ClassFileServer`{.codeph}. You can run the
sample client and the sample server programs on different machines
connected to the same network, or you can run them both on one machine
but from different terminal windows.

All the sample `SSLSocketClient*`{.codeph} programs in the
samples/sockets/client directory (and `URLReader*`{.codeph} programs
described in [Sample Code Illustrating HTTPS
Connections](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGHTTPSCONNECTI-7D238310))
can be run with the `ClassFileServer`{.codeph} sample server program. An
example of how to do this is shown in [Running
SSLSocketClientWithClientAuth with
ClassFileServer](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGSSLSOCKETCLIENTWITHCLIENTAUT-7D23BC0C).
You can make similar changes to run `URLReader`{.codeph},
`SSLSocketClient`{.codeph}, or `SSLSocketClientWithTunneling`{.codeph}
with `ClassFileServer`{.codeph}.

If an authentication error occurs during communication between the
client and the server (whether using a web server or
`ClassFileServer`{.codeph}), it is most likely because the necessary
keys are not in the truststore (trust key database). See [Terms and
Definitions](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329 "The following are commonly used cryptography terms and their definitions.").
For example, the `ClassFileServer`{.codeph} uses a keystore called
`testkeys`{.codeph} containing the private key for `localhost`{.codeph}
as needed during the SSL handshake. The `testkeys`{.codeph} keystore is
included in the same samples/sockets/server directory as the
`ClassFileServer`{.codeph} source. If the client cannot find a
certificate for the corresponding public key of `localhost`{.codeph} in
the truststore it consults, then an authentication error will occur. Be
sure to use the `samplecacerts`{.codeph} truststore (which contains the
public key and certificate of the `localhost`{.codeph}), as described in
the next section.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__CONFIGURATIONREQUIREMENTS-82CE87BD">
Configuration Requirements

When running the sample programs that create a secure socket connection
between a client and a server, you will need to make the appropriate
certificates file (truststore) available. For both the client and the
server programs, you should use the certificates file
`samplecacerts`{.codeph} from the `samples`{.codeph} directory. Using
this certificates file will allow the client to authenticate the server.
The file contains all the common Certificate Authority (CA) certificates
shipped with the JDK (in the cacerts file), plus a certificate for
`localhost`{.codeph} needed by the client to authenticate
`localhost`{.codeph} when communicating with the sample server
`ClassFileServer`{.codeph}. The `ClassFileServer`{.codeph} uses a
keystore containing the private key for `localhost`{.codeph} that
corresponds to the public key in `samplecacerts`{.codeph}.

To make the `samplecacerts`{.codeph} file available to both the client
and the server, you can either copy it to the file
`java-home/lib/security/jssecacerts`, rename it to cacerts, and use it
to replace the `java-home/lib/security/cacerts` file, or add the
following option to the command line when running the `java`{.codeph}
command for both the client and the server:

``` {.codeblock dir="ltr"}
-Djavax.net.ssl.trustStore=path_to_samplecacerts_file
```

To know more about <span class="variable">java-home</span>, see [Terms
and
Definitions](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329 "The following are commonly used cryptography terms and their definitions.").

The password for the `samplecacerts`{.codeph} truststore is
`changeit`{.codeph}. You can substitute your own certificates in the
samples by using the `keytool`{.codeph} utility.

If you use a browser, such as Mozilla Firefox or Microsoft Internet
Explorer, to access the sample SSL server provided in the
`ClassFileServer`{.codeph} example, then a dialog box may pop up with
the message that it does not recognize the certificate. This is normal
because the certificate used with the sample programs is self-signed and
is for testing only. You can accept the certificate for the current
session. After testing the SSL server, you should exit the browser,
which deletes the test certificate from the browser\'s namespace.

For client authentication, a separate `duke`{.codeph} certificate is
available in the appropriate directories. The public key and certificate
is also stored in the `samplecacerts`{.codeph} file.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGSSLSOCKETCLIENT-82CE8C59">
Running SSLSocketClient

The `SSLSocketClient.java`{.codeph} program in <span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> demonstrates how to create a client
that uses an `SSLSocket`{.codeph} to send an HTTP request and to get a
response from an HTTPS server. The output of this program is the HTML
source for `https://www.verisign.com/index.html`{.codeph}.

You must not be behind a firewall to run this program as provided. If
you run it from behind a firewall, you will get an
`UnknownHostException`{.codeph} because JSSE cannot find a path through
your firewall to `www.verisign.com`{.codeph}. To create an equivalent
client that can run from behind a firewall, set up proxy tunneling as
illustrated in the sample program
`SSLSocketClientWithTunneling`{.codeph}.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGSSLSOCKETCLIENTWITHTUNNELING-82CE8F98">
Running SSLSocketClientWithTunneling

The `SSLSocketClientWithTunneling.java`{.codeph} program in <span>[JSSE
Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> illustrates how to do proxy tunneling
to access a secure web server from behind a firewall. To run this
program, you must set the following Java system properties to the
appropriate values:

``` {.codeblock dir="ltr"}
java -Dhttps.proxyHost=webproxy
-Dhttps.proxyPort=ProxyPortNumber
SSLSocketClientWithTunneling
```

<div class="p">
<div class="infoboxnote" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__GUID-12EDAEC4-5DE4-4BD8-A68C-E096E92AE49B">
Note:

Proxy specifications with the `-D`{.codeph} options are optional.
Replace <span class="variable">webproxy</span> with the name of your
proxy host and <span class="variable">ProxyPortNumber</span> with the
appropriate port number.

</div>
</div>
The program will return the HTML source file from
`https://www.verisign.com/index.html`{.codeph}.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGSSLSOCKETCLIENTWITHCLIENTAUT-7D23C25E">
Running SSLSocketClientWithClientAuth

The `SSLSocketClientWithClientAuth.java` program in <span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> shows how to set up a key manager to
do client authentication if required by a server. This program also
assumes that the client is not outside a firewall. You can modify the
program to connect from inside a firewall by following the example in
`SSLSocketClientWithTunneling`{.codeph}.

To run this program, you must specify three parameters: host, port, and
requested file path. To mirror the previous examples, you can run this
program without client authentication by setting the host to
`www.verisign.com`{.codeph}, the port to `443`{.codeph}, and the
requested file path to `https://www.verisign.com/`{.codeph}. The output
when using these parameters is the HTML for the website
`https://www.verisign.com/`{.codeph}.

To run `SSLSocketClientWithClientAuth`{.codeph} to do client
authentication, you must access a server that requests client
authentication. You can use the sample program
`ClassFileServer`{.codeph} as this server. This is described in the
following sections.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGCLASSFILESERVER-7D23BEFC">
Running ClassFileServer

The program referred to herein as `ClassFileServer`{.codeph} is made up
of two files: `ClassFileServer.java` and `ClassServer.java` in
<span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span>.

To execute them, run `ClassFileServer.class`{.codeph}, which requires
the following parameters:

-   `port`{.codeph} can be any available unused port number, for
    example, you can use the number `2001`{.codeph}.
-   `docroot`{.codeph} indicates the directory on the server that
    contains the file you want to retrieve. For example, on Solaris, you
    can use /home/<span class="variable">userid</span>/ (where
    <span class="variable">userid</span> refers to your particular UID),
    whereas on Microsoft Windows systems, you can use c:\\.
-   `TLS`{.codeph} is an optional parameter that indicates that the
    server is to use SSL or TLS.
-   `true`{.codeph} is an optional parameter that indicates that client
    authentication is required. This parameter is only consulted if the
    TLS parameter is set.

<div class="infoboxnote" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__GUID-4635E921-C2B5-4FD5-9480-6478D6C33FC0">
Note:

The `TLS`{.codeph} and `true`{.codeph} parameters are optional. If you
omit them, indicating that an ordinary (not TLS) file server should be
used, without authentication, then nothing happens. This is because one
side (the client) is trying to negotiate with TLS, while the other (the
server) is not, so they cannot communicate.

</div>
<div class="infoboxnote" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__GUID-F17E9E88-69BB-4873-AC14-BA2B42917D05">
Note:

The server expects GET requests in the form
`GET /path_to_file`{.codeph}.

</div>
</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGSSLSOCKETCLIENTWITHCLIENTAUT-7D23BC0C">
Running SSLSocketClientWithClientAuth with ClassFileServer

You can use the sample programs `SSLSocketClientWithClientAuth.java` and
`ClassFileServer`{.codeph} in <span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> to set up authenticated communication,
where the client and server are authenticated to each other. You can run
both sample programs on different machines connected to the same
network, or you can run them both on one machine but from different
terminal windows or command prompt windows. To set up both the client
and the server, do the following:

1.  Run the program `ClassFileServer`{.codeph} from one machine or
    terminal window.

    See [Running
    ClassFileServer](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGCLASSFILESERVER-7D23BEFC).

2.  Run the program `SSLSocketClientWithClientAuth`{.codeph} on another
    machine or terminal window. `SSLSocketClientWithClientAuth`{.codeph}
    requires the following parameters:
    -   `host`{.codeph} is the host name of the machine that you are
        using to run `ClassFileServer`{.codeph}.
    -   `port`{.codeph} is the same port that you specified for
        `ClassFileServer`{.codeph}.
    -   `requestedfilepath`{.codeph} indicates the path to the file that
        you want to retrieve from the server. You must give this
        parameter as `/filepath`{.codeph}. Forward slashes are required
        in the file path because it is used as part of a GET statement,
        which requires forward slashes regardless of what type of
        operating system you are running. The statement is formed as
        follows:

        ``` {.codeblock dir="ltr"}
        "GET " + requestedfilepath + " HTTP/1.0"
        ```

<div class="infoboxnote" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__GUID-80571B4D-FD52-412D-80AF-BB6FF98147C3">
Note:

You can modify the other `SSLClient*`{.codeph} applications\'
`GET`{.codeph} commands to connect to a local machine running
`ClassFileServer`{.codeph}.

</div>
</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGHTTPSCONNECTI-7D238310">
Sample Code Illustrating HTTPS Connections

There are two primary APIs for accessing secure communications through
JSSE. One way is through a socket-level API that can be used for
arbitrary secure communications, as illustrated by the
`SSLSocketClient`{.codeph}, `SSLSocketClientWithTunneling`{.codeph}, and
`SSLSocketClientWithClientAuth`{.codeph} (with and without
`ClassFileServer`{.codeph}) sample programs.

A second, and often simpler, way is through the standard Java URL API.
You can communicate securely with an SSL-enabled web server by using the
HTTPS URL protocol or scheme using the `java.net.URL`{.codeph} class.

Support for HTTPS URL schemes is implemented in many of the common
browsers, which allows access to secured communications without
requiring the socket-level API provided with JSSE.

An example URL is `https://www.verisign.com`{.codeph}.

The trust and key management for the HTTPS URL implementation is
environment-specific. The JSSE implementation provides an HTTPS URL
implementation. To use a different HTTPS protocol implementation, set
the `java.protocol.handler.pkgs`{.codeph}. See [How to Specify a
java.lang.System
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363)
to the package name. See the `java.net.URL`{.codeph} class documentation
for details.

The samples that you can download with JSSE include two sample programs
that illustrate how to create an HTTPS connection. Both of these sample
programs (`URLReader.java` and `URLReaderWithOptions.java` ) are in the
`samples/urls`{.codeph} directory.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGURLREADER-7D238A63">
Running URLReader

The `URLReader.java` program in <span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> illustrates using the URL class to
access a secure site. The output of this program is the HTML source for
`https://www.verisign.com/`{.codeph}. By default, the HTTPS protocol
implementation included with JSSE is used. To use a different
implementation, set the system property
`java.protocol.handler.pkgs`{.codeph} value to be the name of the
package containing the implementation.

If you are running the sample code behind a firewall, then you must set
the `https.proxyHost`{.codeph} and `https.proxyPort`{.codeph} system
properties. For example, to use the proxy host \"webproxy\" on port
8080, you can use the following options for the `java`{.codeph} command:

``` {.codeblock dir="ltr"}
-Dhttps.proxyHost=webproxy
-Dhttps.proxyPort=8080
```

Alternatively, you can set the system properties within the source code
with the `java.lang.System`{.codeph} method `setProperty()`{.codeph}.
For example, instead of using the command-line options, you can include
the following lines in your program:

``` {.codeblock dir="ltr"}
System.setProperty("java.protocol.handler.pkgs", "com.ABC.myhttpsprotocol");
System.setProperty("https.proxyHost", "webproxy");
System.setProperty("https.proxyPort", "8080");
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGURLREADERWITHOPTIONS-7D238F45">
Running URLReaderWithOptions

The `URLReaderWithOptions.java` program in <span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> is essentially the same as the
`URLReader.java`{.codeph} program, except that it allows you to
optionally input any or all of the following system properties as
arguments to the program when you run it:

-   `java.protocol.handler.pkgs`{.codeph}
-   `https.proxyHost`{.codeph}
-   `https.proxyPort`{.codeph}
-   `https.cipherSuites`{.codeph}

To run `URLReaderWithOptions`{.codeph}, enter the following command:

``` {.codeblock dir="ltr"}
java URLReaderWithOptions [-h proxyhost -p proxyport] [-k protocolhandlerpkgs] [-c ciphersarray]
```

<div class="infoboxnote" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__GUID-91B04C04-7256-438A-8976-CFF5EC570A16">
Note:

Multiple protocol handlers can be included in the
`protocolhandlerpkgs`{.codeph} argument as a list with items separated
by vertical bars. Multiple SSL cipher suite names can be included in the
`ciphersarray`{.codeph} argument as a list with items separated by
commas. The possible cipher suite names are the same as those returned
by the `SSLSocket.getSupportedCipherSuites()`{.codeph} method. The suite
names are taken from the SSL and TLS protocol specifications.

</div>
You need a `protocolhandlerpkgs`{.codeph} argument only if you want to
use an HTTPS protocol handler implementation other than the default one
provided by Oracle.

If you are running the sample code behind a firewall, then you must
include arguments for the proxy host and the proxy port. Additionally,
you can include a list of cipher suites to enable.

Here is an example of running `URLReaderWithOptions`{.codeph} and
specifying the proxy host \"webproxy\" on port 8080:

``` {.codeblock dir="ltr"}
java URLReaderWithOptions -h webproxy -p 8080
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGASECURERMICON-F9A2C933">
Sample Code Illustrating a Secure RMI Connection

The sample code in the `samples/rmi` directory illustrates how to create
a secure Java Remote Method Invocation (RMI) connection. The sample code
is basically a \"Hello World\" example modified to install and use a
custom RMI socket factory.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGTHEUSEOFANSSL-7D23A601">
Sample Code Illustrating the Use of an SSLEngine

`SSLEngine`{.codeph} gives application developers flexibility when
choosing I/O and compute strategies. Rather than tie the SSL/TLS
implementation to a specific I/O abstraction (such as single-threaded
`SSLSockets`{.codeph}), `SSLEngine`{.codeph} removes the I/O and compute
constraints from the SSL/TLS implementation.

As mentioned earlier, `SSLEngine`{.codeph} is an advanced API, and is
not appropriate for casual use. Some introductory sample code is
provided here that helps illustrate its use. The first demo removes most
of the I/O and threading issues, and focuses on many of the SSLEngine
methods. The second demo is a more realistic example showing how
`SSLEngine`{.codeph} might be combined with Java NIO to create a
rudimentary HTTP/HTTPS server.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGSSLENGINESIMPLEDEMO-7D240794">
Running SSLEngineSimpleDemo

The `SSLEngineSimpleDemo.java` program in <span>[JSSE Sample
Code](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/index.html)
in the JDK 8 documentation</span> is a very simple application that
focuses on the operation of the `SSLEngine`{.codeph} while simplifying
the I/O and threading issues. This application creates two
`SSLEngine`{.codeph} objects that exchange SSL/TLS messages via common
`ByteBuffer`{.codeph} objects. A single loop serially performs all of
the engine operations and demonstrates how a secure connection is
established (handshaking), how application data is transferred, and how
the engine is closed.

The `SSLEngineResult`{.codeph} provides a great deal of information
about the current state of the `SSLEngine`{.codeph}. This example does
not examine all of the states. It simplifies the I/O and threading
issues to the point that this is not a good example for a production
environment; nonetheless, it is useful to demonstrate the overall
function of the `SSLEngine`{.codeph}.

</div>
<!-- class="section" -->

<div class="section" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGTHENIO-BASEDSERVER-7D23AE05">
Running the NIO-Based Server

To fully exploit the flexibility provided by `SSLEngine`{.codeph}, you
must first understand complementary APIs, such as I/O and threading
models.

An I/O model that large-scale application developers find of use is the
NIO `SocketChannel`{.codeph}. NIO was introduced in part to solve some
of the scaling problem inherent in the `java.net.Socket`{.codeph} API.
`SocketChannel`{.codeph} has many different modes of operation
including:

-   Blocking
-   Nonblocking
-   Nonblocking with selectors

Sample code for a basic HTTP server is provided that not only
demonstrates many of the new NIO APIs, but also shows how
`SSLEngine`{.codeph} can be employed to create a secure HTTPS server.
The server is not production quality, but does show many of these new
APIs in action.

Inside the samples directory is a `README.txt` file that introduces the
server, explains how to build and configure the server, and provides a
brief overview of the code layout. The files of most interest for
`SSLEngine`{.codeph} users are `ChannelIO.java` and
`ChannelIOSecure.java`.

<div class="infoboxnote" id="GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__GUID-EE5A58AA-A4BC-44CE-8ED0-63D0F3B86E0A">
Note:

The server example discussed in this section is included in the JDK. You
can find the code bundled in the `jdk-home/samples/nio/server`{.codeph}
directory.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F}

### Creating a Keystore to Use with JSSE {#JSSEC-GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F .sect3}

<div>
The procedure as to how you can use the `keytool`{.codeph} utility to
create a simple PKCS12 keystore suitable for use with JSSE.

<div class="section">
First you make a `keyEntry`{.codeph} (with public and private keys) in
the keystore, and then you make a corresponding
`trustedCertEntry`{.codeph} (public keys only) in a truststore. For
client authentication, you follow a similar process for the client\'s
certificates.

<div class="p">
<div class="infoboxnote" id="GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F__GUID-9D016F06-C132-4185-83B2-B1EB279D05F0">
Note:

Storing trust anchors and secret keys in PKCS12 is supported since JDK
8.

</div>
</div>
<div class="p">
<div class="infoboxnote" id="GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F__GUID-5FE9AE11-8CB4-4B6C-8BA9-D17AB01633BC">
Note:

It is beyond the scope of this example to explain each step in detail.
See [keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549).

</div>
</div>
User input is shown in bold.

1.  Create a new keystore and self-signed certificate with corresponding
    public and private keys.

    ``` {.codeblock dir="ltr"}
        % keytool -genkeypair -alias duke -keyalg RSA -validity 7 -keystore keystore 
        
        Enter keystore password:  <password>
        What is your first and last name?
        [Unknown]:  Duke
        What is the name of your organizational unit?
        [Unknown]:  Java Software
        What is the name of your organization?
        [Unknown]:  Oracle, Inc.
        What is the name of your City or Locality?
        [Unknown]:  Palo Alto
        What is the name of your State or Province?
        [Unknown]:  CA
        What is the two-letter country code for this unit?
        [Unknown]:  US
        Is CN=Duke, OU=Java Software, O="Oracle, Inc.",
        L=Palo Alto, ST=CA, C=US correct?
        [no]:  yes
    ```

2.  Examine the keystore. Notice that the entry type is
    `PrivatekeyEntry`{.codeph}, which means that this entry has a
    private key associated with it).

    ``` {.codeblock dir="ltr"}
        % keytool -list -v -keystore keystore
        
        Enter keystore password:  <password>
        
        Keystore type: PKCS12
        Keystore provider: SUN

        Your keystore contains 1 entry

        Alias name: duke
        Creation date: Jul 25, 2016
        Entry type: PrivateKeyEntry
        Certificate chain length: 1
        Certificate[1]:
        Owner: CN=Duke, OU=Java Software, O="Oracle, Inc.", L=Palo Alto, ST=CA, C=US
        Issuer: CN=Duke, OU=Java Software, O="Oracle, Inc.", L=Palo Alto, ST=CA, C=US
        Serial number: 210cccfc
        Valid from: Mon Jul 25 10:33:27 IST 2016 until: Mon Aug 01 10:33:27 IST 2016
        Certificate fingerprints:
             SHA1: 80:E5:8A:47:7E:4F:5A:70:83:97:DD:F4:DA:29:3D:15:6B:2A:45:1F
             SHA256: ED:3C:70:68:4E:86:35:9C:63:CC:B9:59:35:58:94:1F:7E:B8:B0:EE:D2:
        4B:9D:80:31:67:8A:D4:B4:7A:B5:12
        Signature algorithm name: SHA256withRSA
        Subject Public Key Algorithm: RSA (2048)
        Version: 3

        Extensions:

       #1: ObjectId: 2.5.29.14 Criticality=false
       SubjectKeyIdentifier [
       KeyIdentifier [
       0000: 7F C9 95 48 42 8D 68 91   BA 1E E6 5C 2C 6B FF 75  ...HB.h....\,k.u
       0010: 5F 19 78 43                                        _.xC
       ]
       ]
    ```

3.  Export and examine the self-signed certificate.

    ``` {.codeblock dir="ltr"}
        % keytool -export -alias duke -keystore keystore -rfc -file duke.cer
        Enter keystore password:  <password>
        Certificate stored in file <duke.cer>
        % cat duke.cer
        -----BEGIN CERTIFICATE-----
        MIIDdzCCAl+gAwIBAgIEIQzM/DANBgkqhkiG9w0BAQsFADBsMQswCQYDVQQGEwJV
        UzELMAkGA1UECBMCQ0ExEjAQBgNVBAcTCVBhbG8gQWx0bzEVMBMGA1UEChMMT3Jh
        Y2xlLCBJbmMuMRYwFAYDVQQLEw1KYXZhIFNvZnR3YXJlMQ0wCwYDVQQDEwREdWtl
        MB4XDTE2MDcyNTA1MDMyN1oXDTE2MDgwMTA1MDMyN1owbDELMAkGA1UEBhMCVVMx
        CzAJBgNVBAgTAkNBMRIwEAYDVQQHEwlQYWxvIEFsdG8xFTATBgNVBAoTDE9yYWNs
        ZSwgSW5jLjEWMBQGA1UECxMNSmF2YSBTb2Z0d2FyZTENMAsGA1UEAxMERHVrZTCC
        ASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAJ7+Yeu6HDZgWwkGlG4iKH9w
        vGKrxXVR57FaFyheMevrgj1ovVnQVFhfdMvjPkjWmpqLg6rfTqU4bKbtoMWV6+Rn
        uQrCw2w9xNC93hX9PxRa20UKrSRDKnUSvi1wjlaxfj0KUKuMwbbY9S8x/naYGeTL
        lwbHiiMvkoFkP2kzhVgeqHjIwSz4HRN8vWHCwgIDFWX/ZlS+LbvB4TSZkS0ZcQUV
        vJWTocOd8RB90W3bkibWkWq166XYGE1Nq1L4WIhrVJwbav6ual69yJsEpVcshVkx
        E1WKzJg7dGb03to4agbReb6+aoCUwb2vNUudNWasSrxoEFArVFGD/ZkPT0esfqEC
        AwEAAaMhMB8wHQYDVR0OBBYEFH/JlUhCjWiRuh7mXCxr/3VfGXhDMA0GCSqGSIb3
        DQEBCwUAA4IBAQAmcTm2ahsIJLayajsvm8yPzQsHA7kIwWfPPHCoHmNbynG67oHB
        fleaNvrgm/raTT3TrqQkg0525qI6Cqaoyy8JA2fAp3i+hmyoGHaIlo14bKazaiPS
        RCCqk0J8vwY3CY9nVal1XlHJMEcYV7X1sxKbuAKFoAJ29E/p6ie0JdHtQe31M7X9
        FNLYzt8EpJYUtWo13B9Oufz/Guuex9PQ7aC93rbO32MxtnnCGMxQHlaHLLPygc/x
        cffGz5Xe5s+NEm78CY7thgN+drI7icBYmv4navsnr2OQaD3AfnJ4WYSQyyUUCPxN
        zuk+B0fbLn7PCCcQspmqfgzIpgbEM9M1/yav
        -----END CERTIFICATE-----    
    ```

    Alternatively, you could generate a Certificate Signing Request
    (CSR) with `-certreq`{.codeph} and send that to a Certificate
    Authority (CA) for signing, but that is beyond the scope of this
    example.

4.  Import the certificate into a new truststore.

    ``` {.codeblock dir="ltr"}
        % keytool -import -alias dukecert -file duke.cer -keystore truststore
        Enter keystore password:  <password>
        Re-enter new password:
        Owner: CN=Duke, OU=Java Software, O="Oracle, Inc.", L=Palo Alto, ST=CA, C=US
        Issuer: CN=Duke, OU=Java Software, O="Oracle, Inc.", L=Palo Alto, ST=CA, C=US
        Serial number: 210cccfc
        Valid from: Mon Jul 25 10:33:27 IST 2016 until: Mon Aug 01 10:33:27 IST 2016
        Certificate fingerprints:
             SHA1: 80:E5:8A:47:7E:4F:5A:70:83:97:DD:F4:DA:29:3D:15:6B:2A:45:1F
             SHA256: ED:3C:70:68:4E:86:35:9C:63:CC:B9:59:35:58:94:1F:7E:B8:B0:EE:D2:
        4B:9D:80:31:67:8A:D4:B4:7A:B5:12
        Signature algorithm name: SHA256withRSA
        Subject Public Key Algorithm: RSA (2048)
        Version: 3

        Extensions:

        #1: ObjectId: 2.5.29.14 Criticality=false
        SubjectKeyIdentifier [
        KeyIdentifier [
        0000: 7F C9 95 48 42 8D 68 91   BA 1E E6 5C 2C 6B FF 75  ...HB.h....\,k.u
        0010: 5F 19 78 43                                        _.xC
        ]
        ]

        Trust this certificate? [no]:  yes
        Certificate was added to keystore

        
    ```

5.  Examine the truststore. Note that the entry type is
    `trustedCertEntry`{.codeph}, which means that a private key is not
    available for this entry. It also means that this file is not
    suitable as a keystore of the `KeyManager`{.codeph}.

    ``` {.codeblock dir="ltr"}
        % keytool -list -v -keystore truststore
        Enter keystore password:  <password>
        
        Keystore type: PKCS12
        Keystore provider: SUN
        
        Your keystore contains 1 entry

        Alias name: dukecert
        Creation date: Jul 25, 2016
        Entry type: trustedCertEntry

        Owner: CN=Duke, OU=Java Software, O="Oracle, Inc.", L=Palo Alto, ST=CA, C=US
        Issuer: CN=Duke, OU=Java Software, O="Oracle, Inc.", L=Palo Alto, ST=CA, C=US
        Serial number: 210cccfc
        Valid from: Mon Jul 25 10:33:27 IST 2016 until: Mon Aug 01 10:33:27 IST 2016
        Certificate fingerprints:
             SHA1: 80:E5:8A:47:7E:4F:5A:70:83:97:DD:F4:DA:29:3D:15:6B:2A:45:1F
             SHA256: ED:3C:70:68:4E:86:35:9C:63:CC:B9:59:35:58:94:1F:7E:B8:B0:EE:D2:
        4B:9D:80:31:67:8A:D4:B4:7A:B5:12
        Signature algorithm name: SHA256withRSA
        Subject Public Key Algorithm: RSA (2048)
        Version: 3

        Extensions:

        #1: ObjectId: 2.5.29.14 Criticality=false
        SubjectKeyIdentifier [
        KeyIdentifier [
        0000: 7F C9 95 48 42 8D 68 91   BA 1E E6 5C 2C 6B FF 75  ...HB.h....\,k.u
        0010: 5F 19 78 43                                        _.xC
        ]
        ]



        *******************************************
        *******************************************
    ```

6.  Now run your applications with the appropriate keystores. Because
    this example assumes that the default `X509KeyManager`{.codeph} and
    `X509TrustManager`{.codeph} are used, you select the keystores using
    the system properties described in [Customizing
    JSSE](java-secure-socket-extension-jsse-reference-guide.htm#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9 "JSSE includes a standard implementation that can be customized by plugging in different implementations or specifying the default keystore, and so on.").

    ``` {.codeblock dir="ltr"}
        % java -Djavax.net.ssl.keyStore=keystore -Djavax.net.ssl.keyStorePassword=password Server
        
        % java -Djavax.net.ssl.trustStore=truststore -Djavax.net.ssl.trustStorePassword=trustword Client
        
    ```

<div class="p">
<div class="infoboxnote" id="GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F__GUID-3E0172AD-F4CF-44DD-BEFF-4EFE7006F0E5">
Note:

This example authenticated the server only. For client authentication,
provide a similar keystore for the client\'s keys and an appropriate
truststore for the server.

</div>
</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-63945B45-E909-483F-B3A9-E26586737383}

### Using the Server Name Indication (SNI) Extension {#JSSEC-GUID-63945B45-E909-483F-B3A9-E26586737383 .sect3}

<div>
<div class="section">
These examples illustrate how you can use the [Server Name Indication
(SNI)
Extension](java-secure-socket-extension-jsse-reference-guide.htm#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F)
for client-side and server-side applications, and how it can be applied
to a virtual infrastructure.

For all examples in this section, to apply the parameters after you set
them, call the `setSSLParameters(SSLParameters)`{.codeph} method on the
corresponding `SSLSocket`{.codeph}, `SSLEngine`{.codeph}, or
`SSLServerSocket`{.codeph} object.

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-BCCE0D1F-08D8-4608-8A5A-5BFA54FED2C0}

#### Typical Client-Side Usage Examples {#JSSEC-GUID-BCCE0D1F-08D8-4608-8A5A-5BFA54FED2C0 .sect4}

<div>
The following is a list of use cases that require understanding of the
SNI extension for developing a client application:

-   Case 1. The client wants to access `www.example.com`{.codeph}.

    Set the host name explicitly:

    ``` {.codeblock dir="ltr"}
        SNIHostName serverName = new SNIHostName("www.example.com");
        sslParameters.setServerNames(Collections.singletonList(serverName)); 
    ```

    The client should always specify the host name explicitly.

-   Case 2. The client does not want to use SNI because the server does
    not support it.

    Disable SNI with an empty server name list:

    ``` {.codeblock dir="ltr"}
        sslParameters.setServerNames(Collections.emptyList());        
    ```

-   Case 3. The client wants to access URL
    `https://www.example.com`{.codeph}.

    Oracle providers will set the host name in the SNI extension by
    default, but third-party providers may not support the default
    server name indication. To keep your application
    provider-independent, always set the host name explicitly.

-   Case 4. The client wants to switch a socket from server mode to
    client mode.

    First switch the mode with the following method:
    `sslSocket.setUseClientMode(true)`{.codeph}. Then reset the server
    name indication parameters on the socket.

</div>
</div>
<div class="sect4">
[]{#GUID-FA9C8332-B6D9-48E6-AF66-700E00B829D2}

#### Typical Server-Side Usage Examples {#JSSEC-GUID-FA9C8332-B6D9-48E6-AF66-700E00B829D2 .sect4}

<div>
The following is a list of use cases that require understanding of the
SNI extension for developing a server application:

-   Case 1. The server wants to accept all server name indication types.

    If you do not have any code dealing with the SNI extension, then the
    server ignores all server name indication types.

-   Case 2. The server wants to deny all server name indications of type
    `host_name`{.codeph}.

    Set an invalid server name pattern for `host_name`{.codeph}:

    ``` {.codeblock dir="ltr"}
        SNIMatcher matcher = SNIHostName.createSNIMatcher("");
        Collection<SNIMatcher> matchers = new ArrayList<>(1);
        matchers.add(matcher);
        sslParameters.setSNIMatchers(matchers);        
    ```

    Another way is to create an `SNIMatcher`{.codeph} subclass with a
    `matches()`{.codeph} method that always returns `false`{.codeph}:

    ``` {.codeblock dir="ltr"}
        class DenialSNIMatcher extends SNIMatcher {
            DenialSNIMatcher() {
                super(StandardConstants.SNI_HOST_NAME);
            }
        
            @Override
            public boolean matches(SNIServerName serverName) {
                return false;
            }
        }
        
        SNIMatcher matcher = new DenialSNIMatcher();
        Collection<SNIMatcher> matchers = new ArrayList<>(1);
        matchers.add(matcher);
        sslParameters.setSNIMatchers(matchers);        
    ```

-   Case 3. The server wants to accept connections to any host names in
    the `example.com`{.codeph} domain.

    Set the recognizable server name for `host_name`{.codeph} as a
    pattern that includes all `*.example.com`{.codeph} addresses:

    ``` {.codeblock dir="ltr"}
        SNIMatcher matcher = SNIHostName.createSNIMatcher("(.*\\.)*example\\.com");
        Collection<SNIMatcher> matchers = new ArrayList<>(1);
        matchers.add(matcher);
        sslParameters.setSNIMatchers(matchers);
    ```

-   Case 4. The server wants to switch a socket from client mode to
    server mode.

    First switch the mode with the following method:
    `sslSocket.setUseClientMode(false)`{.codeph}. Then reset the server
    name indication parameters on the socket.

</div>
</div>
<div class="sect4">
[]{#GUID-0D1E93B9-F63F-46E6-B8A9-0E3AF3207445}

#### Working with Virtual Infrastructures {#JSSEC-GUID-0D1E93B9-F63F-46E6-B8A9-0E3AF3207445 .sect4}

<div>
This section describes how to use the Server Name Indication (SNI)
extension from within a virtual infrastructure. It illustrates how to
create a parser for ClientHello messages from a socket, provides
examples of virtual server dispatchers using `SSLSocket`{.codeph} and
`SSLEngine`{.codeph}, describes what happens when the SNI extension is
not available, and demonstrates how to create a failover
`SSLContext`{.codeph}.

<div class="section">
Preparing the ClientHello Parser

Applications must implement an API to parse the ClientHello messages
from a socket. The following examples illustrate the
`SSLCapabilities`{.codeph} and `SSLExplorer`{.codeph} classes that can
perform these functions.

[SSLSocketClient.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/sockets/client/SSLSocketClient.java)
encapsulates the SSL/TLS/DTLS security capabilities during handshaking
(that is, the list of cipher suites to be accepted in an SSL/TLS/DTLS
handshake, the record version, the hello version, and the server name
indication). It can be retrieved by exploring the network data of an
SSL/TLS/DTLS connection via the `SSLExplorer.explore()`{.codeph} method.

[SSLExplorer.java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/samples/sni/SSLExplorer.java)
explores the initial ClientHello message from a TLS client, but it does
not initiate handshaking or consume network data. The
`SSLExplorer.explore()`{.codeph} method parses the ClientHello message,
and retrieves the security parameters into `SSLCapabilities`{.codeph}.
The method must be called before handshaking occurs on any TLS
connections.

</div>
<!-- class="section" -->

<div class="section">
Virtual Server Dispatcher Based on SSLSocket

This section describes the procedure for using a virtual server
dispatcher based on `SSLSocket`{.codeph}.

1.  <span class="bold">Register the server name handler.</span>

    At this step, the application may create different
    `SSLContext`{.codeph} objects for different server name indications,
    or link a certain server name indication to a specified virtual
    machine or distributed system.

    For example, if the server name is `www.example.org`{.codeph}, then
    the registered server name handler may be for a local virtual
    hosting web service. The local virtual hosting web service will use
    the specified `SSLContext`{.codeph}. If the server name is
    `www.example.com`{.codeph}, then the registered server name handler
    may be for a virtual machine hosting on `10.0.0.36`{.codeph}. The
    handler may map this connection to the virtual machine.

2.  <span class="bold">Create a `ServerSocket`{.codeph} and accept the
    new connection.</span>

    ``` {.codeblock dir="ltr"}
    ServerSocket serverSocket = new ServerSocket(serverPort);
    Socket socket = serverSocket.accept();
    ```

3.  <span class="bold">Read and buffer bytes from the socket input
    stream, and then explore the buffered bytes.</span>

    ``` {.codeblock dir="ltr"}
    InputStream ins = socket.getInputStream();
    byte[] buffer = new byte[0xFF];
    int position = 0;
    SSLCapabilities capabilities = null;
        
    // Read the header of TLS record
    while (position < SSLExplorer.RECORD_HEADER_SIZE) {
        int count = SSLExplorer.RECORD_HEADER_SIZE - position;
        int n = ins.read(buffer, position, count);
        if (n < 0) {
            throw new Exception("unexpected end of stream!");
        }
        position += n;
    }
        
    // Get the required size to explore the SSL capabilities
    int recordLength = SSLExplorer.getRequiredSize(buffer, 0, position);
    if (buffer.length < recordLength) {
        buffer = Arrays.copyOf(buffer, recordLength);
    }
        
    while (position < recordLength) {
        int count = recordLength - position;
        int n = ins.read(buffer, position, count);
        if (n < 0) {
            throw new Exception("unexpected end of stream!");
        }
        position += n;
    }
        
    // Explore
    capabilities = SSLExplorer.explore(buffer, 0, recordLength);
    if (capabilities != null) {
        System.out.println("Record version: " + capabilities.getRecordVersion());
        System.out.println("Hello version: " + capabilities.getHelloVersion());
    }
    ```

4.  <span class="bold">Get the requested server name from the explored
    capabilities.</span>

    ``` {.codeblock dir="ltr"}
    List<SNIServerName> serverNames = capabilities.getServerNames();
    ```

5.  <span class="bold">Look for the registered server name handler for
    this server name indication.</span>

    If the service of the host name is resident in a virtual machine or
    another distributed system, then the application must forward the
    connection to the destination. The application will need to read and
    write the raw internet data, rather then the SSL application from
    the socket stream.

    ``` {.codeblock dir="ltr"}
    Socket destinationSocket = new Socket(serverName, 443);
    // Forward buffered bytes and network data from the current socket to the destinationSocket.
    ```

    If the service of the host name is resident in the same process, and
    the host name service can use the `SSLSocket`{.codeph} directly,
    then the application will need to set the `SSLSocket`{.codeph}
    instance to the server:

    ``` {.codeblock dir="ltr"}
    // Get service context from registered handler
    // or create the context
    SSLContext serviceContext = ...

    SSLSocketFactory serviceSocketFac = serviceContext.getSSLSocketFactory();

    // wrap the buffered bytes
    ByteArrayInputStream bais = new ByteArrayInputStream(buffer, 0, position);
    SSLSocket serviceSocket = (SSLSocket)serviceSocketFac.createSocket(socket, bais, true);

    // Now the service can use serviceSocket as usual.
    ```

</div>
<!-- class="section" -->

<div class="section">
Virtual Server Dispatcher Based on SSLEngine

This section describes the procedure for using a virtual server
dispatcher based on `SSLEngine`{.codeph}.

1.  <span class="bold">Register the server name handler.</span>

    At this step, the application may create different
    `SSLContext`{.codeph} objects for different server name indications,
    or link a certain server name indication to a specified virtual
    machine or distributed system.

    For example, if the server name is `www.example.org`{.codeph}, then
    the registered server name handler may be for a local virtual
    hosting web service. The local virtual hosting web service will use
    the specified `SSLContext`{.codeph}. If the server name is
    `www.example.com`{.codeph}, then the registered server name handler
    may be for a virtual machine hosting on `10.0.0.36`{.codeph}. The
    handler may map this connection to the virtual machine.

2.  <span class="bold">Create a `ServerSocket`{.codeph} or
    `ServerSocketChannel`{.codeph} and accept the new connection.</span>

    ``` {.codeblock dir="ltr"}
    ServerSocketChannel serverSocketChannel = ServerSocketChannel.open();
    serverSocketChannel.bind(...);
    ...
    SocketChannel socketChannel = serverSocketChannel.accept();
    ```

3.  <span class="bold">Read and buffer bytes from the socket input
    stream, and then explore the buffered bytes.</span>

    ``` {.codeblock dir="ltr"}
    ByteBuffer buffer = ByteBuffer.allocate(0xFF);
    SSLCapabilities capabilities = null;
    while (true) {
        // ensure the capacity
        if (buffer.remaining() == 0) {
            ByteBuffer oldBuffer = buffer;
            buffer = ByteBuffer.allocate(buffer.capacity() + 0xFF);
            buffer.put(oldBuffer);
        }

        int n = sc.read(buffer);
        if (n < 0) {
            throw new Exception("unexpected end of stream!");
        }

        int position = buffer.position();
        buffer.flip();
        capabilities = explorer.explore(buffer);
        buffer.rewind();
        buffer.position(position);
        buffer.limit(buffer.capacity());
        if (capabilities != null) {
            System.out.println("Record version: " +
                capabilities.getRecordVersion());
            System.out.println("Hello version: " +
                capabilities.getHelloVersion());
            break;
        }
    }

    buffer.flip();  // reset the buffer position and limitation 
    ```

4.  <span class="bold">Get the requested server name from the explored
    capabilities.</span>

    ``` {.codeblock dir="ltr"}
    List<SNIServerName> serverNames = capabilities.getServerNames();
    ```

5.  <span class="bold">Look for the registered server name handler for
    this server name indication.</span>

    If the service of the host name is resident in a virtual machine or
    another distributed system, then the application must forward the
    connection to the destination. The application will need to read and
    write the raw internet data, rather then the SSL application from
    the socket stream.

    ``` {.codeblock dir="ltr"}
    Socket destinationSocket = new Socket(serverName, 443);
    // Forward buffered bytes and network data from the current socket to the destinationSocket.
    ```

    If the service of the host name is resident in the same process, and
    the host name service can use the `SSLEngine`{.codeph} directly,
    then the application will simply feed the net data to the
    `SSLEngine`{.codeph} instance:

    ``` {.codeblock dir="ltr"}
    // Get service context from registered handler
    // or create the context
    SSLContext serviceContext = ...
        
    SSLEngine serviceEngine = serviceContext.createSSLEngine();
    // Now the service can use the buffered bytes and other byte buffer as usual.
    ```

</div>
<!-- class="section" -->

<div class="section">
No SNI Extension Available

If there is no server name indication in a ClientHello message, then
there is no way to select the proper service according to SNI. For such
cases, the application may need to specify a default service, so that
the connection can be delegated to it if there is no server name
indication.

</div>
<!-- class="section" -->

<div class="section">
Failover SSLContext

The `SSLExplorer.explore()`{.codeph} method does not check the validity
of SSL/TLS/DTLS contents. If the record format does not comply with
SSL/TLS/DTLS specification, or the `explore()`{.codeph} method is
invoked after handshaking has started, then the method may throw an
`IOException`{.codeph} and be unable to produce network data. In such
cases, handle the exception thrown by `SSLExplorer.explore()`{.codeph}
by using a failover `SSLContext`{.codeph}, which is not used to
negotiate an SSL/TLS/DTLS connection, but to close the connection with
the proper alert message. The following example illustrates a failover
`SSLContext`{.codeph}. You can find an example of the
`DenialSNIMatcher`{.codeph} class in Case 2 in [Typical Server-Side
Usage
Examples](java-secure-socket-extension-jsse-reference-guide.htm#GUID-FA9C8332-B6D9-48E6-AF66-700E00B829D2).

``` {.codeblock dir="ltr"}
byte[] buffer = ...       // buffered network data
boolean failed = true;    // SSLExplorer.explore() throws an exception

SSLContext context = SSLContext.getInstance("TLS");
// the failover SSLContext
    
context.init(null, null, null);
SSLSocketFactory sslsf = context.getSocketFactory();
ByteArrayInputStream bais = new ByteArrayInputStream(buffer, 0, position);
SSLSocket sslSocket = (SSLSocket)sslsf.createSocket(socket, bais, true);

SNIMatcher matcher = new DenialSNIMatcher();
Collection<SNIMatcher> matchers = new ArrayList<>(1);
matchers.add(matcher);
SSLParameters params = sslSocket.getSSLParameters();
params.setSNIMatchers(matchers);    // no recognizable server name
sslSocket.setSSLParameters(params);

try {
    InputStream sslIS = sslSocket.getInputStream();
    sslIS.read();
} catch (Exception e) {
    System.out.println("Server exception " + e);
} finally {
    sslSocket.close();
}
```

</div>
<!-- class="section" -->

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-847CA40C-F439-4A31-A7FA-C37B4DEC2190}

Standard Names {#JSSEC-GUID-847CA40C-F439-4A31-A7FA-C37B4DEC2190 .sect2}
--------------

<div>
<div class="section">
The JDK Security API requires and uses a set of standard names for
algorithms, certificates and keystore types. See [Java Security Standard
Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).
Find specific provider information in [JDK Providers
Documentation](oracle-providers.htm#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313 "This document contains the technical details of the providers that are included in the JDK. It is assumed that readers have a strong understanding of the Java Cryptography Architecture and Provider Architecture.").

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-08173142-567C-495C-A48F-32D0FCED466B}

Provider Pluggability {#JSSEC-GUID-08173142-567C-495C-A48F-32D0FCED466B .sect2}
---------------------

<div>
JSSE is fully pluggable and does not restrict the use of third-party
JSSE providers in any way.

</div>
</div>
<div class="sect2">
[]{#GUID-09C3A453-AAAB-4D8B-830A-558B3F30BDF3}

JSSE Cipher Suite Parameters {#JSSEC-GUID-09C3A453-AAAB-4D8B-830A-558B3F30BDF3 .sect2}
----------------------------

<div>
<div class="section">
[Table
8-14](java-secure-socket-extension-jsse-reference-guide.htm#GUID-09C3A453-AAAB-4D8B-830A-558B3F30BDF3__GUID-BB21E6D0-F0C1-4C70-8D6C-F3E56009C51C "List of JSSE Cipher Suite Parameters")
contains a list of additional JSSE cipher suite names related
parameters. See [Java Security Standard Algorithm
Names](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).

</div>
<!-- class="section" -->

<div class="section">
<div class="tblformalwide" id="GUID-09C3A453-AAAB-4D8B-830A-558B3F30BDF3__GUID-BB21E6D0-F0C1-4C70-8D6C-F3E56009C51C">
Table 8-14 JSSE Cipher Suite Parameters

+-----------------+-----------------+-----------------+-----------------+
| Standard Name   | Key Exchange    | Bulk Cipher     | Message         |
| (IANA name if   | Algorithm       | Algorithm       | Authentication  |
| different)      |                 |                 | Code Algorithm  |
+:================+:================+:================+:================+
| SSL\_NULL\_WITH | K\_NULL         | B\_NULL         | M\_NULL         |
| \_NULL\_NULL    |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_NULL\_WITH |                 |                 |                 |
| \_NULL\_NULL    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_WITH\ | RSA             | B\_NULL         | MD5             |
| _NULL\_MD5      |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_WITH\ |                 |                 |                 |
| _NULL\_MD5      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_WITH\ | RSA             | B\_NULL         | SHA-1           |
| _NULL\_SHA      |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_WITH\ |                 |                 |                 |
| _NULL\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_EXPOR | RSA\_EXPORT     | RC4\_40         | MD5             |
| T\_WITH\_RC4\_4 |                 |                 |                 |
| 0\_MD5          |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_EXPOR |                 |                 |                 |
| T\_WITH\_RC4\_4 |                 |                 |                 |
| 0\_MD5          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_WITH\ | RSA             | RC4             | MD5             |
| _RC4\_128\_MD5  |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_WITH\ |                 |                 |                 |
| _RC4\_128\_MD5  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_WITH\ | RSA             | RC4             | SHA-1           |
| _RC4\_128\_SHA  |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_WITH\ |                 |                 |                 |
| _RC4\_128\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_EXPOR | RSA\_EXPORT     | RC2\_CBC\_40    | MD5             |
| T\_WITH\_RC2\_C |                 |                 |                 |
| BC\_40\_MD5     |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_EXPOR |                 |                 |                 |
| T\_WITH\_RC2\_C |                 |                 |                 |
| BC\_40\_MD5     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_WITH\ | RSA             | IDEA\_CBC       | SHA-1           |
| _IDEA\_CBC\_SHA |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_WITH\ |                 |                 |                 |
| _IDEA\_CBC\_SHA |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_EXPOR | RSA\_EXPORT     | DES40\_CBC      | SHA-1           |
| T\_WITH\_DES40\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_EXPOR |                 |                 |                 |
| T\_WITH\_DES40\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_WITH\ | RSA             | DES\_CBC        | SHA-1           |
| _DES\_CBC\_SHA  |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_WITH\ |                 |                 |                 |
| _DES\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_RSA\_WITH\ | RSA             | 3DES\_EDE\_CBC  | SHA-1           |
| _3DES\_EDE\_CBC |                 |                 |                 |
| \_SHA           |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_RSA\_WITH\ |                 |                 |                 |
| _3DES\_EDE\_CBC |                 |                 |                 |
| \_SHA           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_DSS\_E | DH\_DSS         | DES40\_CBC      | SHA-1           |
| XPORT\_WITH\_DE |                 |                 |                 |
| S40\_CBC\_SHA   |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_DSS\_E |                 |                 |                 |
| XPORT\_WITH\_DE |                 |                 |                 |
| S40\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_DSS\_W | DH\_DSS         | DES\_CBC        | SHA-1           |
| ITH\_DES\_CBC\_ |                 |                 |                 |
| SHA             |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_DSS\_W |                 |                 |                 |
| ITH\_DES\_CBC\_ |                 |                 |                 |
| SHA             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_DSS\_W | DH\_DSS         | 3DES\_EDE\_CBC  | SHA-1           |
| ITH\_3DES\_EDE\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_DSS\_W |                 |                 |                 |
| ITH\_3DES\_EDE\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_RSA\_E | DH\_RSA\_EXPORT | DES40\_CBC      | SHA-1           |
| XPORT\_WITH\_DE |                 |                 |                 |
| S40\_CBC\_SHA   |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_RSA\_E |                 |                 |                 |
| XPORT\_WITH\_DE |                 |                 |                 |
| S40\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_RSA\_W | DH\_RSA         | DES\_CBC        | SHA-1           |
| ITH\_DES\_CBC\_ |                 |                 |                 |
| SHA             |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_RSA\_W |                 |                 |                 |
| ITH\_DES\_CBC\_ |                 |                 |                 |
| SHA             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_RSA\_W | DH\_RSA         | 3DES\_EDE\_CBC  | SHA-1           |
| ITH\_3DES\_EDE\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_RSA\_W |                 |                 |                 |
| ITH\_3DES\_EDE\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DHE\_DSS\_ | DHE\_DSS\_EXPOR | DES40\_CBC      | SHA-1           |
| EXPORT\_WITH\_D | T               |                 |                 |
| ES40\_CBC\_SHA  |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DHE\_DSS\_ |                 |                 |                 |
| EXPORT\_WITH\_D |                 |                 |                 |
| ES40\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DHE\_DSS\_ | DHE\_DSS        | DES\_CBC        | SHA-1           |
| WITH\_DES\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DHE\_DSS\_ |                 |                 |                 |
| WITH\_DES\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DHE\_DSS\_ | DHE\_DSS        | 3DES\_EDE\_CBC  | SHA-1           |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DHE\_DSS\_ |                 |                 |                 |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DHE\_RSA\_ | DHE\_RSA\_EXPOR | DES40\_CBC      | SHA-1           |
| EXPORT\_WITH\_D | T               |                 |                 |
| ES40\_CBC\_SHA  |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DHE\_RSA\_ |                 |                 |                 |
| EXPORT\_WITH\_D |                 |                 |                 |
| ES40\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DHE\_RSA\_ | DHE\_RSA        | DES\_CBC        | SHA-1           |
| WITH\_DES\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DHE\_RSA\_ |                 |                 |                 |
| WITH\_DES\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DHE\_RSA\_ | DHE\_RSA        | 3DES\_EDE\_CBC  | SHA-1           |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DHE\_RSA\_ |                 |                 |                 |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_anon\_ | DH\_anon\_EXPOR | RC4\_40         | MD5             |
| EXPORT\_WITH\_R | T               |                 |                 |
| C4\_40\_MD5     |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_anon\_ |                 |                 |                 |
| EXPORT\_WITH\_R |                 |                 |                 |
| C4\_40\_MD5     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_anon\_ | DH\_anon        | RC4             | MD5             |
| WITH\_RC4\_128\ |                 |                 |                 |
| _MD5            |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_anon\_ |                 |                 |                 |
| WITH\_RC4\_128\ |                 |                 |                 |
| _MD5            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_anon\_ | DH\_anon        | DES40\_CBC      | SHA-1           |
| EXPORT\_WITH\_D |                 |                 |                 |
| ES40\_CBC\_SHA  |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_anon\_ |                 |                 |                 |
| EXPORT\_WITH\_D |                 |                 |                 |
| ES40\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_anon\_ | DH\_anon        | DES\_CBC        | SHA-1           |
| WITH\_DES\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_anon\_ |                 |                 |                 |
| WITH\_DES\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| SSL\_DH\_anon\_ | DH\_anon        | 3DES\_EDE\_CBC  | SHA-1           |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
|                 |                 |                 |                 |
| IANA:           |                 |                 |                 |
| TLS\_DH\_anon\_ |                 |                 |                 |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_WITH | KRB5            | DES\_CBC        | SHA-1           |
| \_DES\_CBC\_SHA |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_WITH | KRB5            | 3DES\_EDE\_CBC  | SHA-1           |
| \_3DES\_EDE\_CB |                 |                 |                 |
| C\_SHA          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_WITH | KRB5            | RC4             | SHA-1           |
| \_RC4\_128\_SHA |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_WITH | KRB5            | IDEA\_CBC       | SHA-1           |
| \_IDEA\_CBC\_SH |                 |                 |                 |
| A               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_WITH | KRB5            | DES\_CBC        | MD5             |
| \_DES\_CBC\_MD5 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_WITH | KRB5            | 3DES\_EDE\_CBC  | MD5             |
| \_3DES\_EDE\_CB |                 |                 |                 |
| C\_MD5          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_WITH | KRB5            | RC4             | MD5             |
| \_RC4\_128\_MD5 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_WITH | KRB5            | IDEA\_CBC       | MD5             |
| \_IDEA\_CBC\_MD |                 |                 |                 |
| 5               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_EXPO | KRB5\_EXPORT    | DES\_CBC        | SHA-1           |
| RT\_WITH\_DES\_ |                 |                 |                 |
| CBC\_40\_SHA    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_EXPO | KRB5\_EXPORT    | RC2\_CBC\_40    | SHA-1           |
| RT\_WITH\_RC2\_ |                 |                 |                 |
| CBC\_40\_SHA    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_EXPO | KRB5\_EXPORT    | RC4\_40         | SHA-1           |
| RT\_WITH\_RC4\_ |                 |                 |                 |
| 40\_SHA         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_EXPO | KRB5\_EXPORT    | DES\_CBC        | MD5             |
| RT\_WITH\_DES\_ |                 |                 |                 |
| CBC\_40\_MD5    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_EXPO | KRB5\_EXPORT    | RC2\_CBC\_40    | MD5             |
| RT\_WITH\_RC2\_ |                 |                 |                 |
| CBC\_40\_MD5    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_KRB5\_EXPO | KRB5\_EXPORT    | RC4\_40         | MD5             |
| RT\_WITH\_RC4\_ |                 |                 |                 |
| 40\_MD5         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | B\_NULL         | SHA-1           |
| _NULL\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | B\_NULL         | SHA-1           |
| WITH\_NULL\_SHA |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | B\_NULL         | SHA-1           |
| WITH\_NULL\_SHA |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_128\_CBC   | SHA-1           |
| _AES\_128\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | AES\_128\_CBC   | SHA-1           |
| ITH\_AES\_128\_ |                 |                 |                 |
| CBC\_SHA        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | AES\_128\_CBC   | SHA-1           |
| ITH\_AES\_128\_ |                 |                 |                 |
| CBC\_SHA        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | AES\_128\_CBC   | SHA-1           |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_128\_CBC   | SHA-1           |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | AES\_128\_CBC   | SHA-1           |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_256\_CBC   | SHA-1           |
| _AES\_256\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | AES\_256\_CBC   | SHA-1           |
| ITH\_AES\_256\_ |                 |                 |                 |
| CBC\_SHA        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | AES\_256\_CBC   | SHA-1           |
| ITH\_AES\_256\_ |                 |                 |                 |
| CBC\_SHA        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | AES\_256\_CBC   | SHA-1           |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_256\_CBC   | SHA-1           |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | AES\_256\_CBC   | SHA-1           |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | B\_NULL         | SHA-1           |
| _NULL\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_128\_CBC   | SHA-256         |
| _AES\_128\_CBC\ |                 |                 |                 |
| _SHA256         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_256\_CBC   | SHA-256         |
| _AES\_256\_CBC\ |                 |                 |                 |
| _SHA256         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | AES\_128\_CBC   | SHA-256         |
| ITH\_AES\_128\_ |                 |                 |                 |
| CBC\_SHA256     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | AES\_128\_CBC   | SHA-256         |
| ITH\_AES\_128\_ |                 |                 |                 |
| CBC\_SHA256     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | AES\_128\_CBC   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | CAMELLIA\_128\_ | SHA-1           |
| _CAMELLIA\_128\ |                 | CBC             |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | CAMELLIA\_128\_ | SHA-1           |
| ITH\_CAMELLIA\_ |                 | CBC             |                 |
| 128\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | CAMELLIA\_128\_ | SHA-1           |
| ITH\_CAMELLIA\_ |                 | CBC             |                 |
| 128\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | CAMELLIA\_128\_ | SHA-1           |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _128\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | CAMELLIA\_128\_ | SHA-1           |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _128\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | CAMELLIA\_128\_ | SHA-1           |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _128\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_128\_CBC   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | AES\_256\_CBC   | SHA-256         |
| ITH\_AES\_256\_ |                 |                 |                 |
| CBC\_SHA256     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | AES\_256\_CBC   | SHA-256         |
| ITH\_AES\_256\_ |                 |                 |                 |
| CBC\_SHA256     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | AES\_256\_CBC   | SHA-256         |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_256\_CBC   | SHA-256         |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | AES\_128\_CBC   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | AES\_256\_CBC   | SHA-256         |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | CAMELLIA\_256\_ | SHA-1           |
| _CAMELLIA\_256\ |                 | CBC             |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | CAMELLIA\_256\_ | SHA-1           |
| ITH\_CAMELLIA\_ |                 | CBC             |                 |
| 256\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | CAMELLIA\_256\_ | SHA-1           |
| ITH\_CAMELLIA\_ |                 | CBC             |                 |
| 256\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | CAMELLIA\_256\_ | SHA-1           |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _256\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | CAMELLIA\_256\_ | SHA-1           |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _256\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | CAMELLIA\_256\_ | SHA-1           |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _256\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | RC4             | SHA-1           |
| _RC4\_128\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | 3DES\_EDE\_CBC  | SHA-1           |
| _3DES\_EDE\_CBC |                 |                 |                 |
| \_SHA           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_128\_CBC   | SHA-1           |
| _AES\_128\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_256\_CBC   | SHA-1           |
| _AES\_256\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | RC4             | SHA-1           |
| WITH\_RC4\_128\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | 3DES\_EDE\_CBC  | SHA-1           |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_128\_CBC   | SHA-1           |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_256\_CBC   | SHA-1           |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | RC4             | SHA-1           |
| WITH\_RC4\_128\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | 3DES\_EDE\_CBC  | SHA-1           |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | AES\_128\_CBC   | SHA-1           |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | AES\_256\_CBC   | SHA-1           |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | SEED\_CBC       | SHA-1           |
| _SEED\_CBC\_SHA |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | SEED\_CBC       | SHA-1           |
| ITH\_SEED\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | SEED\_CBC       | SHA-1           |
| ITH\_SEED\_CBC\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | SEED\_CBC       | SHA-1           |
| WITH\_SEED\_CBC |                 |                 |                 |
| \_SHA           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | SEED\_CBC       | SHA-1           |
| WITH\_SEED\_CBC |                 |                 |                 |
| \_SHA           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | SEED\_CBC       | SHA-1           |
| WITH\_SEED\_CBC |                 |                 |                 |
| \_SHA           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_128\_GCM   | SHA-256         |
| _AES\_128\_GCM\ |                 |                 |                 |
| _SHA256         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_256\_GCM   | SHA-384         |
| _AES\_256\_GCM\ |                 |                 |                 |
| _SHA384         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_128\_GCM   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_256\_GCM   | SHA-384         |
| WITH\_AES\_256\ |                 |                 |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | AES\_128\_GCM   | SHA-256         |
| ITH\_AES\_128\_ |                 |                 |                 |
| GCM\_SHA256     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | AES\_256\_GCM   | SHA-384         |
| ITH\_AES\_256\_ |                 |                 |                 |
| GCM\_SHA384     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | AES\_128\_GCM   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | AES\_256\_GCM   | SHA-384         |
| WITH\_AES\_256\ |                 |                 |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | AES\_128\_GCM   | SHA-256         |
| ITH\_AES\_128\_ |                 |                 |                 |
| GCM\_SHA256     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | AES\_256\_GCM   | SHA-384         |
| ITH\_AES\_256\_ |                 |                 |                 |
| GCM\_SHA384     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | AES\_128\_GCM   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | AES\_256\_GCM   | SHA-384         |
| WITH\_AES\_256\ |                 |                 |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_128\_GCM   | SHA-256         |
| _AES\_128\_GCM\ |                 |                 |                 |
| _SHA256         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_256\_GCM   | SHA-384         |
| _AES\_256\_GCM\ |                 |                 |                 |
| _SHA384         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_128\_GCM   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_256\_GCM   | SHA-384         |
| WITH\_AES\_256\ |                 |                 |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | AES\_128\_GCM   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | AES\_256\_GCM   | SHA-384         |
| WITH\_AES\_256\ |                 |                 |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_128\_CBC   | SHA-256         |
| _AES\_128\_CBC\ |                 |                 |                 |
| _SHA256         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_256\_CBC   | SHA-384         |
| _AES\_256\_CBC\ |                 |                 |                 |
| _SHA384         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | B\_NULL         | SHA-256         |
| _NULL\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | B\_NULL         | SHA-384         |
| _NULL\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_128\_CBC   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_256\_CBC   | SHA-384         |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | B\_NULL         | SHA-256         |
| WITH\_NULL\_SHA |                 |                 |                 |
| 256             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | B\_NULL         | SHA-384         |
| WITH\_NULL\_SHA |                 |                 |                 |
| 384             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | AES\_128\_CBC   | SHA-256         |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | AES\_256\_CBC   | SHA-384         |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | B\_NULL         | SHA-256         |
| WITH\_NULL\_SHA |                 |                 |                 |
| 256             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | B\_NULL         | SHA-384         |
| WITH\_NULL\_SHA |                 |                 |                 |
| 384             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | CAMELLIA\_128\_ | SHA-256         |
| _CAMELLIA\_128\ |                 | CBC             |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | CAMELLIA\_128\_ | SHA-256         |
| ITH\_CAMELLIA\_ |                 | CBC             |                 |
| 128\_CBC\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | CAMELLIA\_128\_ | SHA-256         |
| ITH\_CAMELLIA\_ |                 | CBC             |                 |
| 128\_CBC\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _128\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _128\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _128\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | CAMELLIA\_256\_ | SHA-256         |
| _CAMELLIA\_256\ |                 | CBC             |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | CAMELLIA\_256\_ | SHA-256         |
| ITH\_CAMELLIA\_ |                 | CBC             |                 |
| 256\_CBC\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | CAMELLIA\_256\_ | SHA-256         |
| ITH\_CAMELLIA\_ |                 | CBC             |                 |
| 256\_CBC\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | CAMELLIA\_256\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _256\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | CAMELLIA\_256\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _256\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | CAMELLIA\_256\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _256\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_EMPTY\_REN | Not applicable  | Not applicable  | Not applicable  |
| EGOTIATION\_INF |                 |                 |                 |
| O\_SCSV         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_FALLBACK\_ | Not applicable  | Not applicable  | Not applicable  |
| SCSV            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | B\_NULL         | SHA-1           |
| A\_WITH\_NULL\_ |                 |                 |                 |
| SHA             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | RC4             | SHA-1           |
| A\_WITH\_RC4\_1 |                 |                 |                 |
| 28\_SHA         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | 3DES\_EDE\_CBC  | SHA-1           |
| A\_WITH\_3DES\_ |                 |                 |                 |
| EDE\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | AES\_128\_CBC   | SHA-1           |
| A\_WITH\_AES\_1 |                 |                 |                 |
| 28\_CBC\_SHA    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | AES\_256\_CBC   | SHA-1           |
| A\_WITH\_AES\_2 |                 |                 |                 |
| 56\_CBC\_SHA    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | B\_NULL         | SHA-1           |
| SA\_WITH\_NULL\ |                 |                 |                 |
| _SHA            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | RC4             | SHA-1           |
| SA\_WITH\_RC4\_ |                 |                 |                 |
| 128\_SHA        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | 3DES\_EDE\_CBC  | SHA-1           |
| SA\_WITH\_3DES\ |                 |                 |                 |
| _EDE\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_128\_CBC   | SHA-1           |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 128\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_256\_CBC   | SHA-1           |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 256\_CBC\_SHA   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | B\_NULL         | SHA-1           |
| _WITH\_NULL\_SH |                 |                 |                 |
| A               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | RC4             | SHA-1           |
| _WITH\_RC4\_128 |                 |                 |                 |
| \_SHA           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | 3DES\_EDE\_CBC  | SHA-1           |
| _WITH\_3DES\_ED |                 |                 |                 |
| E\_CBC\_SHA     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | AES\_128\_CBC   | SHA-1           |
| _WITH\_AES\_128 |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | AES\_256\_CBC   | SHA-1           |
| _WITH\_AES\_256 |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | B\_NULL         | SHA-1           |
| \_WITH\_NULL\_S |                 |                 |                 |
| HA              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | RC4             | SHA-1           |
| \_WITH\_RC4\_12 |                 |                 |                 |
| 8\_SHA          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | 3DES\_EDE\_CBC  | SHA-1           |
| \_WITH\_3DES\_E |                 |                 |                 |
| DE\_CBC\_SHA    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | AES\_128\_CBC   | SHA-1           |
| \_WITH\_AES\_12 |                 |                 |                 |
| 8\_CBC\_SHA     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | AES\_256\_CBC   | SHA-1           |
| \_WITH\_AES\_25 |                 |                 |                 |
| 6\_CBC\_SHA     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_anon | ECDH\_anon      | B\_NULL         | SHA-1           |
| \_WITH\_NULL\_S |                 |                 |                 |
| HA              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_anon | ECDH\_anon      | RC4             | SHA-1           |
| \_WITH\_RC4\_12 |                 |                 |                 |
| 8\_SHA          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_anon | ECDH\_anon      | 3DES\_EDE\_CBC  | SHA-1           |
| \_WITH\_3DES\_E |                 |                 |                 |
| DE\_CBC\_SHA    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_anon | ECDH\_anon      | AES\_128\_CBC   | SHA-1           |
| \_WITH\_AES\_12 |                 |                 |                 |
| 8\_CBC\_SHA     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_anon | ECDH\_anon      | AES\_256\_CBC   | SHA-1           |
| \_WITH\_AES\_25 |                 |                 |                 |
| 6\_CBC\_SHA     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | 3DES\_EDE\_CBC  | SHA-1           |
| WITH\_3DES\_EDE |                 |                 |                 |
| \_CBC\_SHA      |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | 3DES\_EDE\_CBC  | SHA-1           |
| RSA\_WITH\_3DES |                 |                 |                 |
| \_EDE\_CBC\_SHA |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | 3DES\_EDE\_CBC  | SHA-1           |
| DSS\_WITH\_3DES |                 |                 |                 |
| \_EDE\_CBC\_SHA |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | AES\_128\_CBC   | SHA-1           |
| WITH\_AES\_128\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | AES\_128\_CBC   | SHA-1           |
| RSA\_WITH\_AES\ |                 |                 |                 |
| _128\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | AES\_128\_CBC   | SHA-1           |
| DSS\_WITH\_AES\ |                 |                 |                 |
| _128\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | AES\_256\_CBC   | SHA-1           |
| WITH\_AES\_256\ |                 |                 |                 |
| _CBC\_SHA       |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | AES\_256\_CBC   | SHA-1           |
| RSA\_WITH\_AES\ |                 |                 |                 |
| _256\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_SRP\_SHA\_ | SRP\_SHA        | AES\_256\_CBC   | SHA-1           |
| DSS\_WITH\_AES\ |                 |                 |                 |
| _256\_CBC\_SHA  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_128\_CBC   | SHA-256         |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 128\_CBC\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_256\_CBC   | SHA-384         |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 256\_CBC\_SHA38 |                 |                 |                 |
| 4               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | AES\_128\_CBC   | SHA-256         |
| A\_WITH\_AES\_1 |                 |                 |                 |
| 28\_CBC\_SHA256 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | AES\_256\_CBC   | SHA-384         |
| A\_WITH\_AES\_2 |                 |                 |                 |
| 56\_CBC\_SHA384 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | AES\_128\_CBC   | SHA-256         |
| \_WITH\_AES\_12 |                 |                 |                 |
| 8\_CBC\_SHA256  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | AES\_256\_CBC   | SHA-384         |
| \_WITH\_AES\_25 |                 |                 |                 |
| 6\_CBC\_SHA384  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | AES\_128\_CBC   | SHA-256         |
| _WITH\_AES\_128 |                 |                 |                 |
| \_CBC\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | AES\_256\_CBC   | SHA-384         |
| _WITH\_AES\_256 |                 |                 |                 |
| \_CBC\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_128\_GCM   | SHA-256         |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 128\_GCM\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_256\_GCM   | SHA-384         |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 256\_GCM\_SHA38 |                 |                 |                 |
| 4               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | AES\_128\_GCM   | SHA-256         |
| A\_WITH\_AES\_1 |                 |                 |                 |
| 28\_GCM\_SHA256 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | AES\_256\_GCM   | SHA-384         |
| A\_WITH\_AES\_2 |                 |                 |                 |
| 56\_GCM\_SHA384 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | AES\_128\_GCM   | SHA-256         |
| \_WITH\_AES\_12 |                 |                 |                 |
| 8\_GCM\_SHA256  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | AES\_256\_GCM   | SHA-384         |
| \_WITH\_AES\_25 |                 |                 |                 |
| 6\_GCM\_SHA384  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | AES\_128\_GCM   | SHA-256         |
| _WITH\_AES\_128 |                 |                 |                 |
| \_GCM\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | AES\_256\_GCM   | SHA-384         |
| _WITH\_AES\_256 |                 |                 |                 |
| \_GCM\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | RC4             | SHA-1           |
| \_WITH\_RC4\_12 |                 |                 |                 |
| 8\_SHA          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | 3DES\_EDE\_CBC  | SHA-1           |
| \_WITH\_3DES\_E |                 |                 |                 |
| DE\_CBC\_SHA    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | AES\_128\_CBC   | SHA-1           |
| \_WITH\_AES\_12 |                 |                 |                 |
| 8\_CBC\_SHA     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | AES\_256\_CBC   | SHA-1           |
| \_WITH\_AES\_25 |                 |                 |                 |
| 6\_CBC\_SHA     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | AES\_128\_CBC   | SHA-256         |
| \_WITH\_AES\_12 |                 |                 |                 |
| 8\_CBC\_SHA256  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | AES\_256\_CBC   | SHA-384         |
| \_WITH\_AES\_25 |                 |                 |                 |
| 6\_CBC\_SHA384  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | B\_NULL         | SHA-1           |
| \_WITH\_NULL\_S |                 |                 |                 |
| HA              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | B\_NULL         | SHA-256         |
| \_WITH\_NULL\_S |                 |                 |                 |
| HA256           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | B\_NULL         | SHA-384         |
| \_WITH\_NULL\_S |                 |                 |                 |
| HA384           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | ARIA\_128\_CBC  | SHA-256         |
| _ARIA\_128\_CBC |                 |                 |                 |
| \_SHA256        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | ARIA\_256\_CBC  | SHA-384         |
| _ARIA\_256\_CBC |                 |                 |                 |
| \_SHA384        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | ARIA\_128\_CBC  | SHA-256         |
| ITH\_ARIA\_128\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | ARIA\_256\_CBC  | SHA-384         |
| ITH\_ARIA\_256\ |                 |                 |                 |
| _CBC\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | ARIA\_128\_CBC  | SHA-256         |
| ITH\_ARIA\_128\ |                 |                 |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | ARIA\_256\_CBC  | SHA-384         |
| ITH\_ARIA\_256\ |                 |                 |                 |
| _CBC\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | ARIA\_128\_CBC  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_CBC\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | ARIA\_256\_CBC  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_CBC\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | ARIA\_128\_CBC  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_CBC\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | ARIA\_256\_CBC  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_CBC\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | ARIA\_128\_CBC  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_CBC\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | ARIA\_256\_CBC  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_CBC\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | ARIA\_128\_CBC  | SHA-256         |
| SA\_WITH\_ARIA\ |                 |                 |                 |
| _128\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | ARIA\_256\_CBC  | SHA-384         |
| SA\_WITH\_ARIA\ |                 |                 |                 |
| _256\_CBC\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | ARIA\_128\_CBC  | SHA-256         |
| A\_WITH\_ARIA\_ |                 |                 |                 |
| 128\_CBC\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | ARIA\_256\_CBC  | SHA-384         |
| A\_WITH\_ARIA\_ |                 |                 |                 |
| 256\_CBC\_SHA38 |                 |                 |                 |
| 4               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | ARIA\_128\_CBC  | SHA-256         |
| \_WITH\_ARIA\_1 |                 |                 |                 |
| 28\_CBC\_SHA256 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | ARIA\_256\_CBC  | SHA-384         |
| \_WITH\_ARIA\_2 |                 |                 |                 |
| 56\_CBC\_SHA384 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | ARIA\_128\_CBC  | SHA-256         |
| _WITH\_ARIA\_12 |                 |                 |                 |
| 8\_CBC\_SHA256  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | ARIA\_256\_CBC  | SHA-384         |
| _WITH\_ARIA\_25 |                 |                 |                 |
| 6\_CBC\_SHA384  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | ARIA\_128\_GCM  | SHA-256         |
| _ARIA\_128\_GCM |                 |                 |                 |
| \_SHA256        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | ARIA\_256\_GCM  | SHA-384         |
| _ARIA\_256\_GCM |                 |                 |                 |
| \_SHA384        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | ARIA\_128\_GCM  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_GCM\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | ARIA\_256\_GCM  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_GCM\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | ARIA\_128\_GCM  | SHA-256         |
| ITH\_ARIA\_128\ |                 |                 |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | ARIA\_256\_GCM  | SHA-384         |
| ITH\_ARIA\_256\ |                 |                 |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | ARIA\_128\_GCM  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_GCM\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | ARIA\_256\_GCM  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_GCM\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | ARIA\_128\_GCM  | SHA-256         |
| ITH\_ARIA\_128\ |                 |                 |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | ARIA\_256\_GCM  | SHA-384         |
| ITH\_ARIA\_256\ |                 |                 |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | ARIA\_128\_GCM  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_GCM\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | ARIA\_256\_GCM  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_GCM\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | ARIA\_128\_GCM  | SHA-256         |
| SA\_WITH\_ARIA\ |                 |                 |                 |
| _128\_GCM\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | ARIA\_256\_GCM  | SHA-384         |
| SA\_WITH\_ARIA\ |                 |                 |                 |
| _256\_GCM\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | ARIA\_128\_GCM  | SHA-256         |
| A\_WITH\_ARIA\_ |                 |                 |                 |
| 128\_GCM\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | ARIA\_256\_GCM  | SHA-384         |
| A\_WITH\_ARIA\_ |                 |                 |                 |
| 256\_GCM\_SHA38 |                 |                 |                 |
| 4               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | ARIA\_128\_GCM  | SHA-256         |
| \_WITH\_ARIA\_1 |                 |                 |                 |
| 28\_GCM\_SHA256 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | ARIA\_256\_GCM  | SHA-384         |
| \_WITH\_ARIA\_2 |                 |                 |                 |
| 56\_GCM\_SHA384 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | ARIA\_128\_GCM  | SHA-256         |
| _WITH\_ARIA\_12 |                 |                 |                 |
| 8\_GCM\_SHA256  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | ARIA\_256\_GCM  | SHA-384         |
| _WITH\_ARIA\_25 |                 |                 |                 |
| 6\_GCM\_SHA384  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | ARIA\_128\_CBC  | SHA-256         |
| _ARIA\_128\_CBC |                 |                 |                 |
| \_SHA256        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | ARIA\_256\_CBC  | SHA-384         |
| _ARIA\_256\_CBC |                 |                 |                 |
| \_SHA384        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | ARIA\_128\_CBC  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_CBC\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | ARIA\_256\_CBC  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_CBC\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | ARIA\_128\_CBC  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_CBC\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | ARIA\_256\_CBC  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_CBC\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | ARIA\_128\_GCM  | SHA-256         |
| _ARIA\_128\_GCM |                 |                 |                 |
| \_SHA256        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | ARIA\_256\_GCM  | SHA-384         |
| _ARIA\_256\_GCM |                 |                 |                 |
| \_SHA384        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | ARIA\_128\_GCM  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_GCM\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | ARIA\_256\_GCM  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_GCM\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | ARIA\_128\_GCM  | SHA-256         |
| WITH\_ARIA\_128 |                 |                 |                 |
| \_GCM\_SHA256   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | ARIA\_256\_GCM  | SHA-384         |
| WITH\_ARIA\_256 |                 |                 |                 |
| \_GCM\_SHA384   |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | ARIA\_128\_CBC  | SHA-256         |
| \_WITH\_ARIA\_1 |                 |                 |                 |
| 28\_CBC\_SHA256 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | ARIA\_256\_CBC  | SHA-384         |
| \_WITH\_ARIA\_2 |                 |                 |                 |
| 56\_CBC\_SHA384 |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | CAMELLIA\_128\_ | SHA-256         |
| SA\_WITH\_CAMEL |                 | CBC             |                 |
| LIA\_128\_CBC\_ |                 |                 |                 |
| SHA256          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | CAMELLIA\_256\_ | SHA-384         |
| SA\_WITH\_CAMEL |                 | CBC             |                 |
| LIA\_256\_CBC\_ |                 |                 |                 |
| SHA384          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | CAMELLIA\_128\_ | SHA-256         |
| A\_WITH\_CAMELL |                 | CBC             |                 |
| IA\_128\_CBC\_S |                 |                 |                 |
| HA256           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | CAMELLIA\_256\_ | SHA-384         |
| A\_WITH\_CAMELL |                 | CBC             |                 |
| IA\_256\_CBC\_S |                 |                 |                 |
| HA384           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | CAMELLIA\_128\_ | SHA-256         |
| \_WITH\_CAMELLI |                 | CBC             |                 |
| A\_128\_CBC\_SH |                 |                 |                 |
| A256            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | CAMELLIA\_256\_ | SHA-384         |
| \_WITH\_CAMELLI |                 | CBC             |                 |
| A\_256\_CBC\_SH |                 |                 |                 |
| A384            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | CAMELLIA\_128\_ | SHA-256         |
| _WITH\_CAMELLIA |                 | CBC             |                 |
| \_128\_CBC\_SHA |                 |                 |                 |
| 256             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | CAMELLIA\_256\_ | SHA-384         |
| _WITH\_CAMELLIA |                 | CBC             |                 |
| \_256\_CBC\_SHA |                 |                 |                 |
| 384             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | CAMELLIA\_128\_ | SHA-256         |
| _CAMELLIA\_128\ |                 | GCM             |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | CAMELLIA\_256\_ | SHA-384         |
| _CAMELLIA\_256\ |                 | GCM             |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _128\_GCM\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | CAMELLIA\_256\_ | SHA-384         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _256\_GCM\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | CAMELLIA\_128\_ | SHA-256         |
| ITH\_CAMELLIA\_ |                 | GCM             |                 |
| 128\_GCM\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_RSA\_W | DH\_RSA         | CAMELLIA\_256\_ | SHA-384         |
| ITH\_CAMELLIA\_ |                 | GCM             |                 |
| 256\_GCM\_SHA38 |                 |                 |                 |
| 4               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _128\_GCM\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_DSS\_ | DHE\_DSS        | CAMELLIA\_256\_ | SHA-384         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _256\_GCM\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | CAMELLIA\_128\_ | SHA-256         |
| ITH\_CAMELLIA\_ |                 | GCM             |                 |
| 128\_GCM\_SHA25 |                 |                 |                 |
| 6               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_DSS\_W | DH\_DSS         | CAMELLIA\_256\_ | SHA-384         |
| ITH\_CAMELLIA\_ |                 | GCM             |                 |
| 256\_GCM\_SHA38 |                 |                 |                 |
| 4               |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _128\_GCM\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DH\_anon\_ | DH\_anon        | CAMELLIA\_256\_ | SHA-384         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _256\_GCM\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | CAMELLIA\_128\_ | SHA-256         |
| SA\_WITH\_CAMEL |                 | GCM             |                 |
| LIA\_128\_GCM\_ |                 |                 |                 |
| SHA256          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | CAMELLIA\_256\_ | SHA-384         |
| SA\_WITH\_CAMEL |                 | GCM             |                 |
| LIA\_256\_GCM\_ |                 |                 |                 |
| SHA384          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | CAMELLIA\_128\_ | SHA-256         |
| A\_WITH\_CAMELL |                 | GCM             |                 |
| IA\_128\_GCM\_S |                 |                 |                 |
| HA256           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_ECDS | ECDH\_ECDSA     | CAMELLIA\_256\_ | SHA-384         |
| A\_WITH\_CAMELL |                 | GCM             |                 |
| IA\_256\_GCM\_S |                 |                 |                 |
| HA384           |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | CAMELLIA\_128\_ | SHA-256         |
| \_WITH\_CAMELLI |                 | GCM             |                 |
| A\_128\_GCM\_SH |                 |                 |                 |
| A256            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | CAMELLIA\_256\_ | SHA-384         |
| \_WITH\_CAMELLI |                 | GCM             |                 |
| A\_256\_GCM\_SH |                 |                 |                 |
| A384            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | CAMELLIA\_128\_ | SHA-256         |
| _WITH\_CAMELLIA |                 | GCM             |                 |
| \_128\_GCM\_SHA |                 |                 |                 |
| 256             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDH\_RSA\ | ECDH\_RSA       | CAMELLIA\_256\_ | SHA-384         |
| _WITH\_CAMELLIA |                 | GCM             |                 |
| \_256\_GCM\_SHA |                 |                 |                 |
| 384             |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | CAMELLIA\_128\_ | SHA-256         |
| _CAMELLIA\_128\ |                 | GCM             |                 |
| _GCM\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | CAMELLIA\_256\_ | SHA-384         |
| _CAMELLIA\_256\ |                 | GCM             |                 |
| _GCM\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _128\_GCM\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | CAMELLIA\_256\_ | SHA-384         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _256\_GCM\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _128\_GCM\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | CAMELLIA\_256\_ | SHA-384         |
| WITH\_CAMELLIA\ |                 | GCM             |                 |
| _256\_GCM\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | CAMELLIA\_128\_ | SHA-256         |
| _CAMELLIA\_128\ |                 | CBC             |                 |
| _CBC\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | CAMELLIA\_256\_ | SHA-384         |
| _CAMELLIA\_256\ |                 | CBC             |                 |
| _CBC\_SHA384    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _128\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | CAMELLIA\_256\_ | SHA-384         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _256\_CBC\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | CAMELLIA\_128\_ | SHA-256         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _128\_CBC\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | CAMELLIA\_256\_ | SHA-384         |
| WITH\_CAMELLIA\ |                 | CBC             |                 |
| _256\_CBC\_SHA3 |                 |                 |                 |
| 84              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | CAMELLIA\_128\_ | SHA-256         |
| \_WITH\_CAMELLI |                 | CBC             |                 |
| A\_128\_CBC\_SH |                 |                 |                 |
| A256            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | CAMELLIA\_256\_ | SHA-384         |
| \_WITH\_CAMELLI |                 | CBC             |                 |
| A\_256\_CBC\_SH |                 |                 |                 |
| A384            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_128\_CCM   | CCM             |
| _AES\_128\_CCM  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_256\_CCM   | CCM             |
| _AES\_256\_CCM  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_128\_CCM   | CCM             |
| WITH\_AES\_128\ |                 |                 |                 |
| _CCM            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_256\_CCM   | CCM             |
| WITH\_AES\_256\ |                 |                 |                 |
| _CCM            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_128\_CCM   | CCM\_8          |
| _AES\_128\_CCM\ |                 |                 |                 |
| _8              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_WITH\ | RSA             | AES\_256\_CCM   | CCM\_8          |
| _AES\_256\_CCM\ |                 |                 |                 |
| _8              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_128\_CCM   | CCM\_8          |
| WITH\_AES\_128\ |                 |                 |                 |
| _CCM\_8         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AES\_256\_CCM   | CCM\_8          |
| WITH\_AES\_256\ |                 |                 |                 |
| _CCM\_8         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_128\_CCM   | CCM             |
| _AES\_128\_CCM  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_256\_CCM   | CCM             |
| _AES\_256\_CCM  |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_128\_CCM   | CCM             |
| WITH\_AES\_128\ |                 |                 |                 |
| _CCM            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_256\_CCM   | CCM             |
| WITH\_AES\_256\ |                 |                 |                 |
| _CCM            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_128\_CCM   | CCM\_8          |
| _AES\_128\_CCM\ |                 |                 |                 |
| _8              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AES\_256\_CCM   | CCM\_8          |
| _AES\_256\_CCM\ |                 |                 |                 |
| _8              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_128\_CCM   | CCM\_8          |
| WITH\_AES\_128\ |                 |                 |                 |
| _CCM\_8         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AES\_256\_CCM   | CCM\_8          |
| WITH\_AES\_256\ |                 |                 |                 |
| _CCM\_8         |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_128\_CCM   | CCM             |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 128\_CCM        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_256\_CCM   | CCM             |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 256\_CCM        |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_128\_CCM   | CCM\_8          |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 128\_CCM\_8     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AES\_256\_CCM   | CCM\_8          |
| SA\_WITH\_AES\_ |                 |                 |                 |
| 256\_CCM\_8     |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_RSA | ECDHE\_RSA      | AEAD\_CHACHA20\ | SHA-256         |
| \_WITH\_CHACHA2 |                 | _POLY1305       |                 |
| 0\_POLY1305\_SH |                 |                 |                 |
| A256            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_ECD | ECDHE\_ECDSA    | AEAD\_CHACHA20\ | SHA-256         |
| SA\_WITH\_CHACH |                 | _POLY1305       |                 |
| A20\_POLY1305\_ |                 |                 |                 |
| SHA256          |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_RSA\_ | DHE\_RSA        | AEAD\_CHACHA20\ | SHA-256         |
| WITH\_CHACHA20\ |                 | _POLY1305       |                 |
| _POLY1305\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_PSK\_WITH\ | PSK             | AEAD\_CHACHA20\ | SHA-256         |
| _CHACHA20\_POLY |                 | _POLY1305       |                 |
| 1305\_SHA256    |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_ECDHE\_PSK | ECDHE\_PSK      | AEAD\_CHACHA20\ | SHA-256         |
| \_WITH\_CHACHA2 |                 | _POLY1305       |                 |
| 0\_POLY1305\_SH |                 |                 |                 |
| A256            |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_DHE\_PSK\_ | DHE\_PSK        | AEAD\_CHACHA20\ | SHA-256         |
| WITH\_CHACHA20\ |                 | _POLY1305       |                 |
| _POLY1305\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+
| TLS\_RSA\_PSK\_ | RSA\_PSK        | AEAD\_CHACHA20\ | SHA-256         |
| WITH\_CHACHA20\ |                 | _POLY1305       |                 |
| _POLY1305\_SHA2 |                 |                 |                 |
| 56              |                 |                 |                 |
+-----------------+-----------------+-----------------+-----------------+

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
| ------------- ------ | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| ------------------ - | l | dcommon/gifs/toc.gif |
| -                    | e | )\                   |
|                [![Pr | L |             <span cl |
| evious](../../dcommo | o | ass="icon">Contents< |
| n/gifs/leftnav.gif)\ | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|      [![Next](../../ | ] | -------------------- |
| dcommon/gifs/rightna | ( | -------------------- |
| v.gif)\              | . | ---                  |
|    <span class="icon | . |                      |
| ">Previous</span>](k | / |                      |
| erberos-5-gss-api-me | . |                      |
| chanism.htm)   <span | . |                      |
|  class="icon">Next</ | / |                      |
| span>](running-jsse- | d |                      |
| sample-code1.htm)    | c |                      |
|   ------------------ | o |                      |
| -------------------- | m |                      |
| -------------------- | m |                      |
| ------------- ------ | o |                      |
| -------------------- | n |                      |
| -------------------- | / |                      |
| ------------------ - | g |                      |
| -                    | i |                      |
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
