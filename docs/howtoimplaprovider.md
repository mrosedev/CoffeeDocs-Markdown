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

  --------------------------------------------------------------------------------------------- ------------------------------------------------------- --
                          [![Previous](../../dcommon/gifs/leftnav.gif)\                               [![Next](../../dcommon/gifs/rightnav.gif)\        
   <span class="icon">Previous</span>](java-cryptography-architecture-jca-reference-guide.htm)   <span class="icon">Next</span>](oracle-providers.htm)  
  --------------------------------------------------------------------------------------------- ------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-C485394F-08C9-4D35-A245-1B82CDDBC031}<!-- End Header -->

<span class="enumeration_chapter">3 </span>How to Implement a Provider in the Java Cryptography Architecture {#JSSEC-GUID-C485394F-08C9-4D35-A245-1B82CDDBC031 .sect1}
============================================================================================================

<div>
This document describes what you need to do in order to integrate your
provider into Java SE so that algorithms and other services can be found
when Java Security API clients request them.

</div>
<div class="sect2">
[]{#GUID-75AFEAAB-BDEE-4857-9637-9D72D6C42DED}

Who Should Read This Document {#JSSEC-GUID-75AFEAAB-BDEE-4857-9637-9D72D6C42DED .sect2}
-----------------------------

<div>
Programmers that only need to use the Java Security APIs (see [Core
Classes and
Interfaces](java-cryptography-architecture-jca-reference-guide.html#GUID-5C9A28FC-8B6B-45BA-8A71-6BEEA34EC27F "The following are the core classes and interfaces provided in the JCA.")
in [Java Cryptography Architecture (JCA) Reference
Guide](java-cryptography-architecture-jca-reference-guide.html#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few."))
to access existing cryptography algorithms and other services do
<span class="variable">not</span> need to read this document.

This document is intended for experienced programmers wishing to create
their own provider packages supplying cryptographic service
implementations. It documents what you need to do in order to integrate
your provider into Java so that your algorithms and other services can
be found when Java Security API clients request them.

</div>
</div>
<div class="sect2">
[]{#GUID-2D03228D-7B79-44F8-9D24-A3DCF71B12E4}

Notes on Terminology {#JSSEC-GUID-2D03228D-7B79-44F8-9D24-A3DCF71B12E4 .sect2}
--------------------

<div>
Throughout this document, the terms <span class="variable">JCA</span> by
itself refers to the JCA framework. Whenever this document notes a
specific JCA provider, it will be referred to explicitly by the provider
name.

<div class="section">
-   Prior to JDK 1.4, the JCE was an unbundled product, and as such, the
    JCA and JCE were regularly referred to as separate, distinct
    components. As JCE is now bundled in JDK, the distinction is
    becoming less apparent. Since the JCE uses the same architecture as
    the JCA, the JCE should be more properly thought of as a subset of
    the JCA.
-   The JCA within the JDK includes two software components:
    -   the framework that defines and supports cryptographic services
        for which providers supply implementations. This framework
        includes packages such as `java.security`{.codeph},
        `javax.crypto`{.codeph}, `javax.crypto.spec`{.codeph}, and
        `javax.crypto.interfaces`{.codeph}.
    -   the actual providers such as <span class="variable">Sun</span>,
        <span class="variable">SunRsaSign</span>,
        <span class="variable">SunJCE</span>, which contain the actual
        cryptographic implementations.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-42A646A7-E42A-4DA4-A84E-F4862510E3E8}

Introduction to Implementing Providers {#JSSEC-GUID-42A646A7-E42A-4DA4-A84E-F4862510E3E8 .sect2}
--------------------------------------

<div>
The Java platform defines a set of APIs spanning major security areas,
including cryptography, public key infrastructure, authentication,
secure communication, and access control. These APIs allow developers to
easily integrate security into their application code. They were
designed around the following principles:

-   <span class="bold">Implementation independence</span>: Applications
    do not need to implement security themselves. Rather, they can
    request security services from the Java platform. Security services
    are implemented in providers (see below), which are plugged into the
    Java platform via a standard interface. An application may rely on
    multiple independent providers for security functionality.

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

A Cryptographic Service Provider (provider) refers to a package (or a
set of packages) that supply a concrete implementation of a subset of
the cryptography aspects of the JDK Security API.

The <span class="apiname">java.security.Provider</span> class
encapsulates the notion of a security provider in the Java platform. It
specifies the provider\'s name and lists the security services it
implements. Multiple providers may be configured at the same time, and
are listed in order of preference. When a security service is requested,
the highest priority provider that implements that service is selected.
See [Security
Providers](java-security-overview1.html#GUID-74E1EFEA-F1DD-466C-B61A-CB5E89FA50DE "The java.security.Provider class encapsulates the notion of a security provider in the Java platform. It specifies the provider's name and lists the security services it implements. Multiple providers may be configured at the same time and are listed in order of preference. When a security service is requested, the highest priority provider that implements that service is selected."),
which illustrates how a provider selects a requested security service.

</div>
</div>
<div class="sect2">
[]{#GUID-B35E3749-0A12-42C3-BA0B-C444D7E140BB}

Engine Classes and Corresponding Service Provider Interface Classes {#JSSEC-GUID-B35E3749-0A12-42C3-BA0B-C444D7E140BB .sect2}
-------------------------------------------------------------------

<div>
An engine class defines a cryptographic service in an abstract fashion
(without a concrete implementation). A cryptographic service is always
associated with a particular algorithm or type.

A <span class="variable">cryptographic service</span> either provides
cryptographic operations (like those for digital signatures or message
digests, ciphers or key agreement protocols); generates or supplies the
cryptographic material (keys or parameters) required for cryptographic
operations; or generates data objects (keystores or certificates) that
encapsulate cryptographic keys (which can be used in a cryptographic
operation) in a secure fashion.

For example, here are four engine classes:

-   `Signature`{.codeph} class provides access to the functionality of a
    digital signature algorithm.
-   A DSA `KeyFactory`{.codeph} class supplies a DSA private or public
    key (from its encoding or transparent specification) in a format
    usable by the initSign or initVerify methods, respectively, of a DSA
    Signature object.
-   `Cipher`{.codeph} class provides access to the functionality of an
    encryption algorithm (such as AES)
-   `KeyAgreement`{.codeph} class provides access to the functionality
    of a key agreement protocol (such as Diffie-Hellman)

The Java Cryptography Architecture encompasses the classes comprising
the Security package that relate to cryptography, including the engine
classes. Users of the API request and utilize instances of the engine
classes to carry out corresponding operations. The JDK defines the
following engine classes:

-   `MessageDigest`{.codeph} - used to calculate the message digest
    (hash) of specified data.
-   `Signature`{.codeph} - used to sign data and verify digital
    signatures.
-   `KeyPairGenerator`{.codeph} - used to generate a pair of public and
    private keys suitable for a specified algorithm.
-   `KeyFactory`{.codeph} - used to convert opaque cryptographic keys of
    type `Key`{.codeph} into <span class="variable">key
    specifications</span> (transparent representations of the underlying
    key material), and vice versa.
-   `KeyStore`{.codeph} - used to create and manage a
    <span class="variable">keystore</span>. A keystore is a database of
    keys. Private keys in a keystore have a certificate chain associated
    with them, which authenticates the corresponding public key. A
    keystore also contains certificates from trusted entities.
-   `CertificateFactory`{.codeph} - used to create public key
    certificates and Certificate Revocation Lists (CRLs).
-   `AlgorithmParameters`{.codeph} - used to manage the parameters for a
    particular algorithm, including parameter encoding and decoding.
-   `AlgorithmParameterGenerator`{.codeph} - used to generate a set of
    parameters suitable for a specified algorithm.
-   `SecureRandom`{.codeph} - used to generate random or pseudo-random
    numbers.
-   `Cipher`{.codeph} - used to encrypt or decrypt some specified data.
-   `KeyAgreement`{.codeph} - used to execute a key agreement (key
    exchange) protocol between 2 or more parties.
-   `KeyGenerator`{.codeph} - used to generate a secret (symmetric) key
    suitable for a specified algorithm.
-   `Mac`{.codeph}: used to compute the <span class="variable">message
    authentication code</span> of some specified data.
-   `SecretKeyFactory`{.codeph} - used to convert opaque cryptographic
    keys of type `SecretKey`{.codeph} into <span class="variable">key
    specifications</span> (transparent representations of the underlying
    key material), and vice versa.
-   `CertPathBuilder`{.codeph} - used to create public key certificates
    and Certificate Revocation Lists (CRLs).
-   `CertPathValidator`{.codeph} - used to validate certificate chains.
-   `CertStore`{.codeph} - used to retrieve Certificates and CRLs from a
    repository.
-   `ExemptionMechanism`{.codeph} - used to provide the functionality of
    an exemption mechanism such as <span class="variable">key
    recovery</span>, <span class="variable">key weakening</span>,
    <span class="variable">key escrow</span>, or any other (custom)
    exemption mechanism. Applications or applets that use an exemption
    mechanism may be granted stronger encryption capabilities than those
    which don\'t. However, please note that cryptographic restrictions
    are no longer required for most countries, and thus exemption
    mechanisms may only be useful in those few countries whose
    governments mandate restrictions.

<div class="infoboxnote" id="GUID-B35E3749-0A12-42C3-BA0B-C444D7E140BB__GUID-4ADAF14D-B1E3-451D-9708-F21608DCC42A">
Note:

A <span class="variable">generator</span> creates objects with brand-new
contents, whereas a <span class="variable">factory</span> creates
objects from existing material (for example, an encoding).

</div>
An <span class="variable">engine</span> class provides the interface to
the functionality of a specific type of cryptographic service
(independent of a particular cryptographic algorithm). It defines
<span class="variable">Application Programming Interface</span> (API)
methods that allow applications to access the specific type of
cryptographic service it provides. The actual implementations (from one
or more providers) are those for specific algorithms. For example, the
Signature engine class provides access to the functionality of a digital
signature algorithm. The actual implementation supplied in a
`SignatureSpi`{.codeph} subclass (see next paragraph) would be that for
a specific kind of signature algorithm, such as SHA256withDSA or
SHA512withRSA.

The application interfaces supplied by an engine class are implemented
in terms of a <span class="bold">Service Provider Interface
(SPI)</span>. That is, for each engine class, there is a corresponding
abstract SPI class, which defines the Service Provider Interface methods
that cryptographic service providers must implement.

<div class="figure" id="GUID-B35E3749-0A12-42C3-BA0B-C444D7E140BB__GUID-FD9BD684-1D1B-4621-A7A1-4732D79AB756">
Figure 3-1 Engine Classes

![Description of Figure 3-1
follows](img/architecture-service-provider-interface.gif "Description of Figure 3-1 follows")\
[Description of \"Figure 3-1 Engine
Classes\"](img_text/architecture-service-provider-interface.htm)

</div>
<!-- class="figure" -->

An instance of an engine class, the \"API object\", encapsulates (as a
private field) an instance of the corresponding SPI class, the \"SPI
object\". All API methods of an API object are declared \"final\", and
their implementations invoke the corresponding SPI methods of the
encapsulated SPI object. An instance of an engine class (and of its
corresponding SPI class) is created by a call to the
<span class="apiname">getInstance</span> factory method of the engine
class.

The name of each SPI class is the same as that of the corresponding
engine class, followed by \"Spi\". For example, the SPI class
corresponding to the Signature engine class is the
`SignatureSpi`{.codeph} class.

Each SPI class is abstract. To supply the implementation of a particular
type of service and for a specific algorithm, a provider must subclass
the corresponding SPI class and provide implementations for all the
abstract methods.

Another example of an engine class is the `MessageDigest`{.codeph}
class, which provides access to a message digest algorithm. Its
implementations, in `MessageDigestSpi`{.codeph} subclasses, may be those
of various message digest algorithms such as SHA256 or SHA384.

As a final example, the `KeyFactory`{.codeph} engine class supports the
conversion from opaque keys to transparent key specifications, and vice
versa. See [Key Specification Interfaces and Classes Required by Key
Factories](howtoimplaprovider.html#GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6 "A key factory provides bi-directional conversions between opaque keys (of type Key) and key specifications. If you implement a key factory, you thus need to understand and utilize key specifications. In some cases, you also need to implement your own key specifications.").
The actual implementation supplied in a `KeyFactorySpi`{.codeph}
subclass would be that for a specific type of keys, e.g., DSA public and
private keys.

</div>
</div>
<div class="sect2">
[]{#GUID-CC161921-EBD2-48C6-B543-A956658B68B6}

Steps to Implement and Integrate a Provider {#JSSEC-GUID-CC161921-EBD2-48C6-B543-A956658B68B6 .sect2}
-------------------------------------------

<div>
Follow these steps to implement a provider and integrate it into the JCA
framework:

-   [Step 1: Write your Service Implementation
    Code](howtoimplaprovider.html#GUID-1D2FDA77-743C-47CB-9CCB-2585FEC0607A "When instantiating a provider's implementation (class) of a Cipher, KeyAgreement, KeyGenerator, MAC, or SecretKey factory, the framework will determine the provider's codebase (JAR file) and verify its signature. In this way, JCA authenticates the provider and ensures that only providers signed by a trusted entity can be plugged into the JCA. Thus, one requirement for encryption providers is that they must be signed, as described in later steps.")
-   [Step 2: Give your Provider a
    Name](howtoimplaprovider.html#GUID-7241AB0C-71DC-408C-8726-B8E0225DDBCE)
-   [Step 3: Write Your Master Class, a Subclass of
    Provider](howtoimplaprovider.html#GUID-1C82EDB9-96CA-44AB-8590-E299814D6A46 "Create a subclass of the java.security.Provider class. This is essentially a lookup table that advertises the algorithms that your provider implements.")
-   [Step 4: Create a Module Declaration for Your
    Provider](howtoimplaprovider.html#GUID-7C304A79-6D0B-438B-A02E-51648C909876 "This step is optional but recommended; it enables you to package your provider in a named module. A modular JDK can then locate your provider in the module path as opposed to the class path. The module system can more thoroughly check for dependencies in modules in the module path. Note that you can use named modules in a non-modular JDK; the module declaration will be ignored. Also, you can still package your providers in unnamed or automatic modules.")
-   [Step 5: Compile Your
    Code](howtoimplaprovider.html#GUID-83742677-6E39-4A8D-BF0F-BC743E3AE43C)
-   [Step 6: Place Your Provider in a JAR
    File](howtoimplaprovider.html#GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F)
-   [Step 7: Sign Your JAR File, If
    Necessary](howtoimplaprovider.html#GUID-2D4432F9-1C3C-4A91-8612-2B2840188B36)
-   [Step 8: Prepare for
    Testing](howtoimplaprovider.html#GUID-FB9C6DB2-DE9A-4EFE-89B4-C2C168C5982D "The next steps describe how to install and configure your new provider so that it is available via the JCA.")
-   [Step 9: Write and Compile Your Test
    Programs](howtoimplaprovider.html#GUID-C6054169-FE6E-4837-B2BD-382DFEB955C0 "Write and compile one or more test programs that test your provider's incorporation into the Security API as well as the correctness of its algorithm(s). Create any supporting files needed, such as those for test data to be encrypted.")
-   [Step 10: Run Your Test
    Programs](howtoimplaprovider.html#GUID-3FD26072-6982-4DCE-932C-DE152C463992 "When you run your test applications, the required java command options will vary depending on factors such as whether you packaged your provider as a named, automatic, or unnamed module and if you configured it so that the ServiceLoader class can search for it.")
-   [Step 11: Apply for U.S. Government Export Approval If
    Required](howtoimplaprovider.html#GUID-A62916EE-BE09-4229-9D05-3D6AF303CA4E "All U.S. vendors whose providers may be exported outside the U.S. should apply to the Bureau of Industry and Security in the U.S. Department of Commerce for export approval.")
-   [Step 12: Document Your Provider and Its Supported
    Services](howtoimplaprovider.html#GUID-912FAB1D-628A-47EA-A1DD-A216F2DD4245)
-   [Step 13: Make Your Class Files and Documentation Available to
    Clients](howtoimplaprovider.html#GUID-3521E2A8-93B5-4D0F-AE2D-DC1B5E6857B7 "After writing, configuring, testing, installing and documenting your provider software, make documentation available to your customers.")

</div>
<div class="sect3">
[]{#GUID-1D2FDA77-743C-47CB-9CCB-2585FEC0607A}

### Step 1: Write your Service Implementation Code {#JSSEC-GUID-1D2FDA77-743C-47CB-9CCB-2585FEC0607A .sect3}

<div>
<div class="section">
The first thing you need to do is to write the code that provides
algorithm-specific implementations of the cryptographic services you
want to support. Your provider may supply implementations of
cryptographic services already available in one or more of the security
components of the JDK.

For cryptographic services not defined in JCA (for example, signatures
and message digests), see [Engine Classes and
Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.").

For each cryptographic service you wish to implement, create a subclass
of the appropriate SPI class. JCA defines the following engine classes:

-   `SignatureSpi`{.codeph}
-   `MessageDigestSpi`{.codeph}
-   `KeyPairGeneratorSpi`{.codeph}
-   `SecureRandomSpi`{.codeph}
-   `AlgorithmParameterGeneratorSpi`{.codeph}
-   `AlgorithmParametersSpi`{.codeph}
-   `KeyFactorySpi`{.codeph}
-   `CertificateFactorySpi`{.codeph}
-   `KeyStoreSpi`{.codeph}
-   `CipherSpi`{.codeph}
-   `KeyAgreementSpi`{.codeph}
-   `KeyGeneratorSpi`{.codeph}
-   `MacSpi`{.codeph}
-   `SecretKeyFactorySpi`{.codeph}
-   `ExemptionMechanismSpi`{.codeph}

To know more about the JCA and other cryptographic classes, see [Engine
Classes and Corresponding Service Provider Interface
Classes](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212 "An engine class provides the interface to a specific type of cryptographic service, independent of a particular cryptographic algorithm or provider.").

In the subclass, you need to:

</div>
<!-- class="section" -->

1.  <span>Supply implementations for the abstract methods, whose names
    usually begin with `engine`{.codeph}. See [Further Implementation
    Details and
    Requirements](howtoimplaprovider.html#GUID-C8B79D46-6EA9-4E27-8083-7CB967732BB3 "This section provides additional information about alias names, service interdependencies, algorithm parameter generators and algorithm parameters.").</span>
2.  <span>Depending on how you write your provider and register its
    algorithms (using either <span class="apiname">String</span> objects
    or the <span class="apiname">Provider.Service</span> class), the
    provider either:</span>
    -   Ensure that there is a public constructor without any arguments.
        Here\'s why: When one of your services is requested, Java
        Security looks up the subclass implementing that service, as
        specified by a property in your \"master class\" (see [Step 3:
        Write Your Master Class, a Subclass of
        Provider](howtoimplaprovider.html#GUID-1C82EDB9-96CA-44AB-8590-E299814D6A46 "Create a subclass of the java.security.Provider class. This is essentially a lookup table that advertises the algorithms that your provider implements.")).
        Java Security then creates the `Class`{.codeph} object
        associated with your subclass, and creates an instance of your
        subclass by calling the `newInstance`{.codeph} method on that
        `Class`{.codeph} object. `newInstance`{.codeph} requires your
        subclass to have a public constructor without any parameters. (A
        default constructor without arguments will automatically be
        generated if your subclass doesn\'t have any constructors. But
        if your subclass defines any constructors, you must explicitly
        define a public constructor without arguments.)
    -   Override the <span class="apiname">newInstance()</span> method
        in the registered <span class="apiname">Provider.Service</span>.
        This is the preferred mechanism in JDK 9 and later.

</div>
<div class="sect4">
[]{#GUID-AEE5234F-24F1-4899-B490-C79F0C2D8D59}

#### Step 1.1: Consider Additional JCA Provider Requirements and Recommendations for Encryption Implementations {#JSSEC-GUID-AEE5234F-24F1-4899-B490-C79F0C2D8D59 .sect4}

<div>
When instantiating a provider\'s implementation (class) of a
`Cipher`{.codeph}, `KeyAgreement`{.codeph}, `KeyGenerator`{.codeph},
`MAC`{.codeph}, or `SecretKey`{.codeph} factory, the framework will
determine the provider\'s codebase (JAR file) and verify its signature.
In this way, JCA authenticates the provider and ensures that only
providers signed by a trusted entity can be plugged into the JCA. Thus,
one requirement for encryption providers is that they must be signed, as
described in later steps.

<div class="section">
In order for provider classes to become unusable if instantiated by an
application directly, bypassing JCA, providers should implement the
following:

-   All SPI implementation classes in a provider package should be
    declared `final`{.codeph} (so that they cannot be subclassed), and
    their (SPI) implementation methods should be declared
    `protected`{.codeph}.
-   All crypto-related helper classes in a provider package should have
    package-private scope, so that they cannot be accessed from outside
    the provider package.

For providers that may be exported outside the U.S.,
`CipherSpi`{.codeph} implementations must include an implementation of
the `engineGetKeySize`{.codeph} method which, given a `Key`{.codeph},
returns the key size. If there are restrictions on available
cryptographic strength specified in jurisdiction policy files, each
`Cipher`{.codeph} initialization method calls
`engineGetKeySize`{.codeph} and then compares the result with the
maximum allowable key size for the particular location and circumstances
of the applet or application being run. If the key size is too large,
the initialization method throws an exception.

Additional <span class="variable">optional</span> features that
providers may implement are:

</div>
<!-- class="section" -->

-   **Optional:** <span>The `engineWrap`{.codeph} and
    `engineUnwrap`{.codeph} methods of `CipherSpi`{.codeph}. Wrapping a
    key enables secure transfer of the key from one place to another.
    Information about wrapping and unwrapping keys is provided in the
    [`wrap`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/Cipher.html#wrap-java.security.Key-).</span>
-   **Optional:** <span>One or more <span class="variable">exemption
    mechanisms</span>. An exemption mechanism is something such as key
    recovery, key escrow, or key weakening which, if implemented and
    enforced, may enable reduced cryptographic restrictions for an
    application (or applet) that uses it. To know more about the
    requirements for apps that utilize exemption mechanisms, see [How to
    Make Applications Exempt from Cryptographic
    Restrictions](java-cryptography-architecture-jca-reference-guide.html#GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D).</span>

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-7241AB0C-71DC-408C-8726-B8E0225DDBCE}

### Step 2: Give your Provider a Name {#JSSEC-GUID-7241AB0C-71DC-408C-8726-B8E0225DDBCE .sect3}

<div>
Decide on a unique name for your provider. This is the name to be used
by client applications to refer to your provider, and it must not
conflict with any other provider names.

</div>
</div>
<div class="sect3">
[]{#GUID-1C82EDB9-96CA-44AB-8590-E299814D6A46}

### Step 3: Write Your Master Class, a Subclass of Provider {#JSSEC-GUID-1C82EDB9-96CA-44AB-8590-E299814D6A46 .sect3}

<div>
Create a subclass of the `java.security.Provider`{.codeph} class. This
is essentially a lookup table that advertises the algorithms that your
provider implements.

<div class="section">
You can use the following coding styles to subclass the
<span class="apiname">Provider</span> class:

-   Create a provider that registers its services with
    <span class="apiname">String</span> objects to store algorithm names
    and their associated implementation class name. These are stored in
    the <span class="apiname">Hashtable\<Object,Object\></span>
    superclass of <span class="apiname">java.security.Provider</span>.

-   Create a provider that uses the
    <span class="apiname">Provider.Service</span> class, which uses a
    different method to store algorithm names and create new objects.
    The <span class="apiname">Provider.Service</span> class enables you
    customize how the JCE framework requests services from your
    provider, such as how the framework creates new instances of your
    provider\'s services. This coding style is recommended, especially
    when using modules.

A provider can use either style, or even use both styles at the same
time. Regardless of which style you choose, your subclass should be
`final`{.codeph}.

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-AB9C2460-0CF2-48BA-B9FE-7059071344CE}

#### Step 3.1: Create a Provider That Uses String Objects to Register Its Services {#JSSEC-GUID-AB9C2460-0CF2-48BA-B9FE-7059071344CE .sect4}

<div>
<div class="section">
The following is an example of a provider that uses
<span class="apiname">String</span> objects to store implemented
algorithm names:

``` {.oac_no_warn dir="ltr"}
package p;
public final class MyProvider extends Provider {
    public MyProvider() {
        super("MyProvider", "1.0",
            "Some info about my provider and which algorithms it supports");
        // com.my.crypto.provider.MyCipher extends CipherSPI
        put("Cipher.MyCipher", "com.my.crypto.provider.MyCipher");
    }
}
```

To create a provider with this coding style, do the following:

</div>
<!-- class="section" -->

-   <span>Call `super`{.codeph}, specifying the provider name (see [Step
    2: Give your Provider a
    Name](howtoimplaprovider.html#GUID-7241AB0C-71DC-408C-8726-B8E0225DDBCE))
    version number, and a string of information about the provider and
    algorithms it supports.</span>

    <div>
    ``` {.codeblock dir="ltr"}
       super("MyProvider", "1.0",
            "Some info about my provider and which algorithms it supports");
    ```

    </div>
-   <span>Set the values of various properties that are required for the
    Java Security API to look up the cryptographic services implemented
    by the provider.</span>

    <div>
    For each service implemented by the provider, there must be a
    property whose name is the type of service followed by a period and
    the name of the algorithm to which the service applies. The property
    value must specify the fully qualified name of the class
    implementing the service.

    For example, this following statement sets a property named
    `Cipher.MyCypher`{.codeph} whose value is
    `com.my.crypto.provider.MyCipher`{.codeph}, a class that extends
    `CipherSPI`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
            put("Cipher.MyCipher", "com.my.crypto.provider.MyCipher");
    ```

    The following list shows the various types of JCA services, where
    the actual algorithm name is substituted for `algName`{.codeph}:

    -   `Signature.algName`{.codeph}
    -   `MessageDigest.algName`{.codeph}
    -   `KeyPairGenerator.algName`{.codeph}
    -   `SecureRandom.algName`{.codeph}
    -   `AlgorithmParameterGenerator.algName`{.codeph}
    -   `AlgorithmParameters.algName`{.codeph}
    -   `KeyFactory.algName`{.codeph}
    -   `CertificateFactory.algName`{.codeph}
    -   `KeyStore.algName`{.codeph}
    -   `Cipher.algName`{.codeph}: `algName`{.codeph} may actually
        represent a <span class="variable">transformation</span>, and
        may be composed of an algorithm name, a particular mode, and a
        padding scheme. See [Java Security Standard Algorithm Names
        Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
    -   `KeyAgreement.algName`{.codeph}
    -   `KeyGenerator.algName`{.codeph}
    -   `Mac.algName`{.codeph}
    -   `SecretKeyFactory.algName`{.codeph}
    -   `ExemptionMechanism.algName`{.codeph}: `algName`{.codeph} refers
        to the name of the exemption mechanism, which can be one of the
        following: `KeyRecovery`{.codeph}, `KeyEscrow`{.codeph}, or
        `KeyWeakening`{.codeph}. Case does
        <span class="variable">not</span> matter.

    In all of these except `ExemptionMechanism`{.codeph} and
    `Cipher`{.codeph}, `algName`{.codeph} is the \"standard\" name of
    the algorithm, certificate type, or keystore type. See [Java
    Security Standard Algorithm Names
    Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
    for the standard names that should be used.

    The value of each property must be the fully qualified name of the
    class implementing the specified algorithm, certificate type, or
    keystore type. That is, it must be the package name followed by the
    class name, where the two are separated by a period.

    As an example, the default provider named
    <span class="variable">SUN</span> implements the Digital Signature
    Algorithm (whose standard name is `SHA256withDSA`{.codeph}) in a
    class named `DSA`{.codeph} in the `sun.security.provider`{.codeph}
    package. Its subclass of `Provider`{.codeph} (which is the Sun class
    in the `sun.security.provider package`{.codeph}) sets the
    `Signature.SHA256withDSA`{.codeph} property to have the value
    `sun.security.provider.DSA`{.codeph} via the following:

    ``` {.codeblock dir="ltr"}
    put("Signature.SHA256withDSA", "sun.security.provider.DSA")
    ```

    The list below shows more properties that can be defined for the
    various types of services, where the actual algorithm name is
    substituted for <span class="variable">algName</span>, certificate
    type for <span class="variable">certType,</span> keystore type for
    <span class="variable">storeType</span>, and attribute name for
    <span class="variable">attrName</span>:

    -   `Signature.algName [one or more spaces] attrName`{.codeph}
    -   `MessageDigest.algName [one or more spaces] attrName`{.codeph}
    -   `KeyPairGenerator.algName [one or more spaces] attrName`{.codeph}
    -   `SecureRandom.algName [one or more spaces] attrName`{.codeph}
    -   `KeyFactory.algName [one or more spaces] attrName`{.codeph}
    -   `CertificateFactory.certType [one or more spaces] attrName`{.codeph}
    -   `KeyStore.storeType [one or more spaces] attrName`{.codeph}
    -   `AlgorithmParameterGenerator.algName [one or more spaces] attrName`{.codeph}
    -   `AlgorithmParameters.algName [one or more spaces] attrName`{.codeph}
    -   `Cipher.algName [one or more spaces] attrName`{.codeph}
    -   `KeyAgreement.algName [one or more spaces] attrName`{.codeph}
    -   `KeyGenerator.algName [one or more spaces] attrName`{.codeph}
    -   `Mac.algName [one or more spaces] attrName`{.codeph}
    -   `SecretKeyFactory.algName [one or more spaces] attrName`{.codeph}
    -   `ExemptionMechanism.algName [one or more spaces] attrName`{.codeph}

    In each of these, `attrName`{.codeph} is the \"standard\" name of
    the algorithm, certificate type, keystore type, or attribute. (See
    [Java Security Standard Algorithm Names
    Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
    for the standard names that should be used.)

    For a property in the above format, the value of the property must
    be the value for the corresponding attribute. (See [Java Security
    Standard Algorithm Names
    Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
    for the definition of each standard attribute.)

    For further master class property setting examples, see the JDK 9
    source code for the
    [<span class="apiname">sun.security.provider.Sun</span>](http://hg.openjdk.java.net/jdk9/jdk9/jdk/file/65464a307408/src/java.base/share/classes/sun/security/provider/Sun.java)
    and
    [<span class="apiname">com.sun.crypto.provider.SunJCE</span>](http://hg.openjdk.java.net/jdk9/jdk9/jdk/file/65464a307408/src/java.base/share/classes/com/sun/crypto/provider/SunJCE.java)
    classes. They show how the Sun and SunJCE providers set properties.

    As an example, the default provider named SUN implements the
    `SHA256withDSA`{.codeph} Digital Signature Algorithm in software.
    The class <span class="apiname">sun.security.provider.Sun</span>
    calls the method <span class="apiname">SunEntries.putEntries</span>,
    which sets the properties for the SUN provider, including setting
    the property `Signature.SHA256withDSA ImplementedIn`{.codeph} to
    have the value `Software`{.codeph}:

    ``` {.codeblock dir="ltr"}
        put("Signature.SHA256withDSA ImplementedIn", "Software");
    ```

    <div class="infoboxnote" id="GUID-AB9C2460-0CF2-48BA-B9FE-7059071344CE__GUID-609B98BF-623E-457F-A8A5-EA3B62BCBA5D">
    Note:

    For examples of this coding style, see the source code for
    <span class="apiname">sun.security.provider.Sun</span> and
    <span class="apiname">sun.security.provider.SunEntries</span>
    classes.

    </div>
    </div>

</div>
</div>
<div class="sect4">
[]{#GUID-CB446B7A-CEA2-4F4A-A4AF-4D492CB58733}

#### Step 3.2: Create a Provider That Uses Provider.Service {#JSSEC-GUID-CB446B7A-CEA2-4F4A-A4AF-4D492CB58733 .sect4}

<div>
<div class="section">
The following is an example of a provider that uses a
<span class="apiname">Provider.Service</span> class:

``` {.oac_no_warn dir="ltr"}
package p;
 
public final class MyProvider extends Provider {
     
    public MyProvider() {
        super("MyProvider", "1.0",
            "Some info about my provider and which algorithms it supports");
        putService(new ProviderService(this, "Cipher", "MyCipher", "p.MyCipher"));
    }
     
    private static final class ProviderService extends Provider.Service {
        ProviderService(Provider p, String type, String algo, String cn) {
            super(p, type, algo, cn, null, null);
        }
         
        @Override
        public Object newInstance(Object ctrParamObj)
            throws NoSuchAlgorithmException {
            String type = getType();
            String algo = getAlgorithm();
            try {
                if (type.equals("Cipher")) {
                    if (algo.equals("MyCipher")) {
                        return new MyCipher();
                    }
                }
            } catch (Exception ex) {
                throw new NoSuchAlgorithmException(
                    "Error constructing " + type + " for "
                    + algo + " using SunMSCAPI", ex);
            }
            throw new ProviderException("No impl for " + algo + " " + type);
        }
    }
}
```

To create a provider with this coding style, do the following:

</div>
<!-- class="section" -->

-   <span>For each algorithm your provider supports, call
    <span class="apiname">putService</span> with an instance of
    <span class="apiname">Provider.Service</span>; the arguments of the
    <span class="apiname">Provider.Service</span> constructor represent
    a supported algorithm.</span>

    <div>
    The following statement adds a service named `MyCipher`{.codeph} of
    type `Cipher`{.codeph}; the name of the class implementing this
    service is `p.MyCipher`{.codeph}. The argument of
    `putService`{.codeph} is a subclass of
    <span class="apiname">Provider.Service</span>:

    ``` {.oac_no_warn dir="ltr"}
            putService(new ProviderService(this, "Cipher", "MyCipher", "p.MyCipher"));
    ```

    This example uses a subclass of
    <span class="apiname">Provider.Service</span> named
    `ProviderService`{.codeph} (rather than
    <span class="apiname">Provider.Service</span> itself) as it
    customizes how the JCE framework instantiates services. If you
    don\'t need to customize the behavior of
    <span class="apiname">Provider.Service</span>, then you can call the
    <span class="apiname">Provider.Service</span> constructor directly:

    ``` {.oac_no_warn dir="ltr"}
    public final class MyProvider extends Provider {   
        public MyProvider() {
            super("MyProvider", "1.0",
                "Some info about my provider and which algorithms it supports");
            putService(new Provider.Service(
                this, "Cipher", "MyCipher", "p.MyCipher", null, null));
        }
    }
    ```

    Note that this example is essentially the same as the example
    described in [Step 3.1: Create a Provider That Uses String Objects
    to Register Its
    Services](howtoimplaprovider.html#GUID-AB9C2460-0CF2-48BA-B9FE-7059071344CE).

    </div>
-   <span>Override any method in
    <span class="apiname">Provider.Service</span>, such as
    <span class="apiname">newInstance</span>, to customize how the JCE
    framework handles the services in your provider.</span>

    <div>
    The example at the beginning of this section overrides the method
    <span class="apiname">Provider.Service.newInstance</span>. The
    method returns an instance of `MyCipher`{.codeph} only if the
    requested service is `MyCipher`{.codeph}. If not, it throws a
    `NoSuchAlgorithmException`{.codeph} and a
    `ProviderException`{.codeph}.

    For more information about other methods you can override, see [The
    Provider.Service
    Class](howtoimplaprovider.html#GUID-B1428B09-5542-4D36-9C0D-D78A8B2B3C00 "Provider.Service class offers an alternative way for providers to advertise their services and supports additional features.").

    <div class="infoboxnote" id="GUID-CB446B7A-CEA2-4F4A-A4AF-4D492CB58733__GUID-62864B28-DA3B-492B-8079-F83B7004D2AC">
    Note:

    For examples of this coding style, see the JDK 9 source code
    contained in the
    [<span class="apiname">sun.security.mscapi</span>](http://hg.openjdk.java.net/jdk9/jdk9/jdk/file/65464a307408/src/jdk.crypto.mscapi/windows/classes/sun/security/mscapi)
    package.

    </div>
    </div>

</div>
</div>
<div class="sect4">
[]{#GUID-E1800256-2F1C-471D-96B5-A39ABA751461}

#### Step 3.3: Specify Additional Information for Cipher Implementations {#JSSEC-GUID-E1800256-2F1C-471D-96B5-A39ABA751461 .sect4}

<div>
As mentioned above, in the case of a `Cipher`{.codeph} property,
<span class="variable">algName</span> may actually represent a
<span class="variable">transformation</span>. A
<span class="variable">transformation</span> is a string that describes
the operation (or set of operations) to be performed by a
`Cipher`{.codeph} object on some given input. A transformation always
includes the name of a cryptographic algorithm (e.g.,
<span class="variable">AES</span>), and may be followed by a mode and a
padding scheme.

<div class="section">
A transformation is of the form:

-   <span class="variable">algorithm/mode/padding</span>, or
-   <span class="variable">algorithm</span>

(In the latter case, provider-specific default values for the mode and
padding scheme are used). For example, the following is a valid
transformation:

``` {.codeblock dir="ltr"}
    Cipher c = Cipher.getInstance("AES/CBC/PKCS5Padding"); 
```

When requesting a block cipher in stream cipher mode (for example;
`AES`{.codeph} in `CFB`{.codeph} or `OFB`{.codeph} mode), a client may
optionally specify the number of bits to be processed at a time, by
appending this number to the mode name as shown in the following sample
transformations:

``` {.codeblock dir="ltr"}
    Cipher c1 = Cipher.getInstance("AES/CFB8/NoPadding");
    Cipher c2 = Cipher.getInstance("AES/OFB32/PKCS5Padding");
```

If a number does not follow a stream cipher mode, a provider-specific
default is used. (For example, the <span class="variable">SunJCE</span>
provider uses a default of 128 bits.)

A provider may supply a separate class for each combination of
<span class="variable">algorithm/mode/padding</span>. Alternatively, a
provider may decide to provide more generic classes representing
sub-transformations corresponding to
<span class="variable">algorithm</span> or
<span class="variable">algorithm/mode</span> or
<span class="variable">algorithm//padding</span> (note the double
slashes); in this case the requested mode and/or padding are set
automatically by the `getInstance`{.codeph} methods of
`Cipher`{.codeph}, which invoke the `engineSetMode`{.codeph} and
`engineSetPadding`{.codeph} methods of the provider\'s subclass of
`CipherSpi`{.codeph}.

That is, a `Cipher`{.codeph} property in a provider master class may
have one of the formats shown in the table below.

<div class="tblformalwide" id="GUID-E1800256-2F1C-471D-96B5-A39ABA751461__GUID-98373D6F-2FC2-405D-A54E-8D730E6025D5">
Table 3-1 Cipher Property Format

  `Cipher`{.codeph} Property Format                                      Description
  ---------------------------------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  `Cipher.`{.codeph}<span class="variable">algName</span>                A provider\'s subclass of `CipherSpi`{.codeph} implements <span class="variable">algName</span> with pluggable mode and padding
  `Cipher.`{.codeph}<span class="variable">algName/mode</span>           A provider\'s subclass of `CipherSpi`{.codeph} implements <span class="variable">algName</span> in the specified <span class="variable">mode</span>, with pluggable padding
  `Cipher.`{.codeph}<span class="variable">algName//padding</span>       A provider\'s subclass of `CipherSpi`{.codeph} implements <span class="variable">algName</span> with the specified <span class="variable">padding</span>, with pluggable mode
  `Cipher.`{.codeph}<span class="variable">algName/mode/padding</span>   A provider\'s subclass of `CipherSpi`{.codeph} implements <span class="variable">algName</span> with the specified <span class="variable">mode</span> and <span class="variable">padding</span>

</div>
<!-- class="inftblhruleinformal" -->

(See [Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html)
for the standard algorithm names, modes, and padding schemes that should
be used.)

For example, a provider may supply a subclass of `CipherSpi`{.codeph}
that implements <span class="variable">AES/ECB/PKCS5Padding</span>, one
that implements <span class="variable">AES/CBC/PKCS5Padding</span>, one
that implements <span class="variable">AES/CFB/PKCS5Padding</span>, and
yet another one that implements
<span class="variable">AES/OFB/PKCS5Padding</span>. That provider would
have the following `Cipher`{.codeph} properties in its master class:

-   `Cipher.AES/ECB/PKCS5Padding`{.codeph}
-   `Cipher.AES/CBC/PKCS5Padding`{.codeph}
-   `Cipher.AES/CFB/PKCS5Padding`{.codeph}
-   `Cipher.AES/OFB/PKCS5Padding`{.codeph}

Another provider may implement a class for each of the above modes
(i.e., one class for <span class="variable">ECB</span>, one for
<span class="variable">CBC</span>, one for
<span class="variable">CFB</span>, and one for
<span class="variable">OFB</span>), one class for
<span class="variable">PKCS5Padding</span>, and a generic
<span class="variable">AES</span> class that subclasses from
`CipherSpi`{.codeph}. That provider would have the following
`Cipher`{.codeph} properties in its master class:

-   `Cipher.AES`{.codeph}
-   `Cipher.AES SupportedModes`{.codeph}
    -   Example: `"ECB|CBC|CFB|OFB"`{.codeph}

-   `Cipher.AES SupportedPaddings`{.codeph}
    -   Example: `"NOPADDING|PKCS5Padding"`{.codeph}

The `getInstance`{.codeph} factory method of the `Cipher`{.codeph}
engine class follows these rules in order to instantiate a provider\'s
implementation of `CipherSpi`{.codeph} for a transformation of the form
\"<span class="variable">algorithm</span>\":

</div>
<!-- class="section" -->

1.  <span>Check if the provider has registered a subclass of
    `CipherSpi`{.codeph} for the specified
    \"<span class="variable">algorithm</span>\".</span>
    -   If the answer is YES, instantiate this class, for whose mode and
        padding scheme default values (as supplied by the provider) are
        used.
    -   If the answer is NO, throw a `NoSuchAlgorithmException`{.codeph}
        exception.
2.  <span>The `getInstance`{.codeph} factory method of the
    `Cipher`{.codeph} engine class follows these rules in order to
    instantiate a provider\'s implementation of `CipherSpi`{.codeph} for
    a transformation of the form
    \"<span class="variable">algorithm/mode/padding</span>\":</span>
    a.  <span>Check if the provider has registered a subclass of
        `CipherSpi`{.codeph} for the specified
        \"<span class="variable">algorithm/mode/padding</span>\"
        transformation.</span>
        <div>
        -   If the answer is YES, instantiate it.

        -   If the answer is NO, go to the next step.

        </div>
    b.  <span>Check if the provider has registered a subclass of
        `CipherSpi`{.codeph} for the sub-transformation
        \"<span class="variable">algorithm/mode</span>\".</span>
        <div>
        -   If the answer is YES, instantiate it, and call
            `engineSetPadding(padding)`{.codeph} on the new instance.

        -   If the answer is NO, go to the next step.

        </div>
    c.  <span>Check if the provider has registered a subclass of
        `CipherSpi`{.codeph} for the sub-transformation
        \"<span class="variable">algorithm//padding</span>\" (note the
        double slashes)</span>
        <div>
        -   If the answer is YES, instantiate it, and call
            `engineSetMode(mode)`{.codeph} on the new instance.

        -   If the answer is NO, go to the next step.

        </div>
    d.  <span>Check if the provider has registered a subclass of
        `CipherSpi`{.codeph} for the sub-transformation
        \"<span class="variable">algorithm</span>\".</span>
        <div>
        -   If the answer is YES, instantiate it, and call
            `engineSetMode(mode)`{.codeph} and
            `engineSetPadding(padding)`{.codeph} on the new instance.

        -   If the answer is NO, throw a
            `NoSuchAlgorithmException`{.codeph} exception.

        </div>

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-7C304A79-6D0B-438B-A02E-51648C909876}

### Step 4: Create a Module Declaration for Your Provider {#JSSEC-GUID-7C304A79-6D0B-438B-A02E-51648C909876 .sect3}

<div>
This step is optional but recommended; it enables you to package your
provider in a named module. A modular JDK can then locate your provider
in the module path as opposed to the class path. The module system can
more thoroughly check for dependencies in modules in the module path.
Note that you can use named modules in a non-modular JDK; the module
declaration will be ignored. Also, you can still package your providers
in unnamed or automatic modules.

<div class="section">
Create a module declaration for your provider and save it in a file
named `module-info.java`. This module declaration includes the
following:

-   The name of your module.

-   Any module upon which your provider depends.

-   A `provides`{.codeph} directive if your module provides a service
    implementation.

The following example module declaration defines a module named
`com.foo.MyProvider`{.codeph}. `p.MyProvider`{.codeph} is the fully
qualified class name of a service implementation. Suppose that, in this
example, `p.MyProvider`{.codeph} uses API in the package
<span class="apiname">javax.security.auth.kerberos</span>, which is in
the module <span class="apiname">java.security.jgss</span>. Thus, the
directive `requires java.security.jgss`{.codeph} appears in the module
declaration.

``` {.oac_no_warn dir="ltr"}
module com.foo.MyProvider {
    provides java.security.Provider with p.MyProvider;
    requires java.security.jgss;
}
```

You can package a provider in three different kinds of modules:

-   Named or explicit module: A module that appears on the module path
    and contains module configuration information in the
    `module-info.class` file.

    The JCE framework can use the
    [<span class="apiname">ServiceLoader</span>](https://docs.oracle.com/javase/10/docs/api/java/util/ServiceLoader.html)
    class (which simplifies provider configuration) to search for
    providers in explicit modules without any additional changes to the
    module. See [Step 8.1: Configure the
    Provider](howtoimplaprovider.html#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 "Register your provider so that the JCE framework can find your provider, either with the ServiceLoader class or in the class path or module path.")
    and [Step 10: Run Your Test
    Programs](howtoimplaprovider.html#GUID-3FD26072-6982-4DCE-932C-DE152C463992 "When you run your test applications, the required java command options will vary depending on factors such as whether you packaged your provider as a named, automatic, or unnamed module and if you configured it so that the ServiceLoader class can search for it.").

-   Automatic module:  A module that appears on the module path, but
    does not contain module configuration information in a
    `module-info.class` file (essentially a \"regular\" JAR file).

-   Unnamed module: A module that appears on the class path. It may or
    may not have a `module-info.class` file; this file is ignored.

It is recommended that you package your providers in named modules as
they provide better performance, stronger encapsulation, simpler
configuration and greater flexibility.

You have a lot of flexibility when it comes to packaging and configuring
your providers. However, this impacts how you start applications that
use them. For example, you might have to specify additional
`--add-exports`{.codeph} or `--add-modules`{.codeph} options. Named
modules, in general, require fewer of these additional options. In
addition named modules offer more flexibility. You can use them with
non-modular JDKs or even as unnamed modules by specifying them in a
modular JDK\'s class path. For more information about modules, see [The
State of the Module
System](http://openjdk.java.net/projects/jigsaw/spec/sotms/) and [JEP
261: Module System](http://openjdk.java.net/jeps/261).

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-83742677-6E39-4A8D-BF0F-BC743E3AE43C}

### Step 5: Compile Your Code {#JSSEC-GUID-83742677-6E39-4A8D-BF0F-BC743E3AE43C .sect3}

<div>
After you have created your implementation code ([Step 1: Write your
Service Implementation
Code](howtoimplaprovider.html#GUID-1D2FDA77-743C-47CB-9CCB-2585FEC0607A "When instantiating a provider's implementation (class) of a Cipher, KeyAgreement, KeyGenerator, MAC, or SecretKey factory, the framework will determine the provider's codebase (JAR file) and verify its signature. In this way, JCA authenticates the provider and ensures that only providers signed by a trusted entity can be plugged into the JCA. Thus, one requirement for encryption providers is that they must be signed, as described in later steps.")),
given your provider a name ([Step 2: Give your Provider a
Name](howtoimplaprovider.html#GUID-7241AB0C-71DC-408C-8726-B8E0225DDBCE)),
created the master class ([Step 3: Write Your Master Class, a Subclass
of
Provider](howtoimplaprovider.html#GUID-1C82EDB9-96CA-44AB-8590-E299814D6A46 "Create a subclass of the java.security.Provider class. This is essentially a lookup table that advertises the algorithms that your provider implements.")),
and created a module declaration ([Step 4: Create a Module Declaration
for Your
Provider](howtoimplaprovider.html#GUID-7C304A79-6D0B-438B-A02E-51648C909876 "This step is optional but recommended; it enables you to package your provider in a named module. A modular JDK can then locate your provider in the module path as opposed to the class path. The module system can more thoroughly check for dependencies in modules in the module path. Note that you can use named modules in a non-modular JDK; the module declaration will be ignored. Also, you can still package your providers in unnamed or automatic modules.")),
use the Java compiler to compile your files.

</div>
</div>
<div class="sect3">
[]{#GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F}

### Step 6: Place Your Provider in a JAR File {#JSSEC-GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F .sect3}

<div>
<div class="section" id="GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F__ADDTHEFILEJAVA.SECURITY.PROVIDERTOU-025DFEDB">
Add the File java.security.Provider to Use the ServiceLoader Class to
Search for Providers

If your provider is packaged in an automatic or unnamed module (you did
not create a module declaration as described in [Step 4: Create a Module
Declaration for Your
Provider](howtoimplaprovider.html#GUID-7C304A79-6D0B-438B-A02E-51648C909876 "This step is optional but recommended; it enables you to package your provider in a named module. A modular JDK can then locate your provider in the module path as opposed to the class path. The module system can more thoroughly check for dependencies in modules in the module path. Note that you can use named modules in a non-modular JDK; the module declaration will be ignored. Also, you can still package your providers in unnamed or automatic modules."))
and you want the use the
<span class="apiname">java.util.ServiceLoader</span> to search for your
providers, then add the file `META-INF/services/java.security.Provider`
to the JAR file and ensure that the file contains the fully qualified
class name of your provider implementation.

The security provider loading mechanism uses the
[<span class="apiname">ServiceLoader</span>](https://docs.oracle.com/javase/10/docs/api/java/util/ServiceLoader.html)
class to search for providers before consulting the class path.

For example, if the fully qualified class name of your provider is
`p.Provider`{.codeph} and all the compiled code of your provider is in
the directory `classes`, then create a file named
`classes/META-INF/services/java.security.Provider` that contains the
following line:

``` {.oac_no_warn dir="ltr"}
p.MyProvider
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F__RUNTHEJARCOMMANDTOCREATEAMODULEJARF-025E01A6">
Run the jar Command to Create a JAR File

The following command creates a JAR file named `MyProvider.jar`. All the
compiled code for the module JAR file is in the directory `classes`. In
addition, the module descriptor, `module-info.class`, is in the
directory `classes`:

``` {.oac_no_warn dir="ltr"}
jar --create --file MyProvider.jar --module-version 1.0 -C classes
```

<div class="infoboxnote" id="GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F__GUID-FC0BD0DE-0B46-47DD-88FD-BBE643CECA04">
Note:

The `module-info.class` file and the `--module-version`{.codeph} option
are optional. However, the `module-info.class` file is required if you
want to create a modular JAR file. (A modular JAR file is a regular JAR
file that has a `module-info.class` file in its top-level directory.)

</div>
See [jar](olink:JSWOR614) in <span><cite>Java Platform, Standard Edition
Tools Reference</cite></span>.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-2D4432F9-1C3C-4A91-8612-2B2840188B36}

### Step 7: Sign Your JAR File, If Necessary {#JSSEC-GUID-2D4432F9-1C3C-4A91-8612-2B2840188B36 .sect3}

<div>
If your provider is supplying encryption algorithms through the
<span class="apiname">Cipher</span>,
<span class="apiname">KeyAgreement</span>,
<span class="apiname">KeyGenerator</span>,
<span class="apiname">Mac</span>, or
<span class="apiname">SecretKeyFactory</span> classes, you must sign
your JAR file so that the JCA can authenticate the code at run time; see
[Step 1.1: Consider Additional JCA Provider Requirements and
Recommendations for Encryption
Implementations](howtoimplaprovider.html#GUID-AEE5234F-24F1-4899-B490-C79F0C2D8D59 "When instantiating a provider's implementation (class) of a Cipher, KeyAgreement, KeyGenerator, MAC, or SecretKey factory, the framework will determine the provider's codebase (JAR file) and verify its signature. In this way, JCA authenticates the provider and ensures that only providers signed by a trusted entity can be plugged into the JCA. Thus, one requirement for encryption providers is that they must be signed, as described in later steps.").
If you are not providing an implementation of this type, then you can
skip this step.

</div>
<div class="sect4">
[]{#GUID-434AACF7-0D2C-494A-B32A-508A6B605F62}

#### Step 7.1: Get a Code-Signing Certificate {#JSSEC-GUID-434AACF7-0D2C-494A-B32A-508A6B605F62 .sect4}

<div>
The next step is to request a code-signing certificate so that you can
use it to sign your provider prior to testing. The certificate will be
good for both testing and production. It will be valid for 5 years.

<div class="section">
Below are the steps you should use to get a code-signing certificate.
See [keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) in
the <span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

</div>
<!-- class="section" -->

1.  [<span>Use <span class="bold">keytool</span> to generate a RSA
    keypair, using RSA algorithm as an example:
    </span>]{#GUID-434AACF7-0D2C-494A-B32A-508A6B605F62__USEKEYTOOLTOGENERATEADSAKEYPAIRUSIN-7569AAA1}

    <div>
    ``` {.codeblock dir="ltr"}
    keytool -genkeypair -alias <alias> \
            -keyalg RSA -keysize 2048 \
            -dname "cn=<Company Name>, \
            ou=Java Software Code Signing, \
            o=Oracle Corporation" \
            -keystore <keystore file name> \  
            -storepass <keystore password>
    ```

    </div>
    <div>
    This will generate a DSA keypair (a public key and an associated
    private key) and store it in an entry in the specified keystore. The
    public key is stored in a self-signed certificate. The keystore
    entry can subsequently be accessed using the specified alias.

    The option values in angle brackets (\"\<\" and \"\>\") represent
    the actual values that must be supplied. For example,
    `<alias>`{.codeph} must be replaced with whatever alias name you
    wish to be used to refer to the newly-generated keystore entry in
    the future, and `<keystore file name>`{.codeph} must be replaced
    with the name of the keystore to be used.

    <div class="infobox-tip" id="GUID-434AACF7-0D2C-494A-B32A-508A6B605F62__GUID-BFAEADA0-1705-445D-9874-DF195A5DF8FB">
    Tip:

    Do not surround actual values with angle brackets. For example, if
    you want your alias to be `myTestAlias`{.codeph}, specify the
    `-alias`{.codeph} option as follows:

    ``` {.codeblock dir="ltr"}
        -alias myTestAlias
    ```

    </div>
    If you specify a keystore that doesn\'t yet exist, it will be
    created.

    <div class="infoboxnote" id="GUID-434AACF7-0D2C-494A-B32A-508A6B605F62__GUID-AABAAA98-A479-4148-AABB-245A84439DBA">
    Note:

    If command lines you type are not allowed to be as long as the
    `keytool -genkeypair`{.codeph} command you want to execute (for
    example, if you are typing to a Microsoft Windows DOS prompt), you
    can create and execute a plain-text batch file containing the
    command. That is, create a new text file that contains nothing but
    the full `keytool -genkeypair`{.codeph} command. (Remember to type
    it all on one line.) Save the file with a .bat extension. Then in
    your DOS window, type the file name (with its path, if necessary).
    This will cause the command in the batch file to be executed.

    </div>
    </div>
2.  <span>Use <span class="bold">keytool</span> to generate a
    certificate signing request. </span>

    <div>
    ``` {.codeblock dir="ltr"}
        keytool -certreq -alias <alias> \
            -file <csr file name> \
            -keystore <keystore file name> \
            -storepass <keystore password> 
    ```

    Here, `<alias>`{.codeph} is the alias for the DSA keypair entry
    created in the previous step. This command generates a Certificate
    Signing Request (CSR), using the PKCS\#10 format. It stores the CSR
    in the file whose name is specified in `<csr file name>`{.codeph}.

    </div>
3.  <span>Send the CSR, contact information, and other required
    documentation to the JCA Code Signing Certification Authority. See
    [JCA Code Signing Certification
    Authority](http://www.oracle.com/technetwork/java/javase/tech/getcodesigningcertificate-361306.html#jcacodesigning)
    for contact information.</span>
4.  <span>After the JCA Code Signing Certification Authority has
    received your email message, they will send you a request number via
    email. Once you receive this request number, you should print, fill
    out and send the Certification Form for CSPs. See [Sending
    Certification Form for
    CSPs](http://www.oracle.com/technetwork/java/javase/tech/getcodesigningcertificate-361306.html#sendingcertificationform)
    for contact information.</span>
5.  <span>Use <span class="bold">keytool</span> to import the
    certificates received from the CA.</span>

    <div>
    Once you have received the two certificates from the JCA Code
    Signing Certification Authority, you can use
    <span class="bold">keytool</span> to import them into your keystore.
    First import the CA\'s certificate as a \"trusted certificate\":

    ``` {.codeblock dir="ltr"}
        keytool -import -alias <alias for the CA cert> \
            -file <CA cert file name> \
            -keystore <keystore file name> \
            -storepass <keystore password>
    ```

    Then import the code-signing certificate:

    ``` {.codeblock dir="ltr"}
        keytool -import -alias <alias> \
            -file <code-signing cert file name> \
            -keystore <keystore file name> \
            -storepass <keystore password>
    ```

    `<alias>`{.codeph} is the same alias as that which you created in
    [Step
    1](howtoimplaprovider.html#GUID-434AACF7-0D2C-494A-B32A-508A6B605F62__USEKEYTOOLTOGENERATEADSAKEYPAIRUSIN-7569AAA1)
    where you generated a DSA keypair. This command replaces the
    self-signed certificate in the keystore entry specified by
    `<alias>`{.codeph} with the one signed by the JCA Code Signing
    Certification Authority.

    </div>

<div class="section">
Now that you have in your keystore a certificate from an entity trusted
by JCA (the JCA Code Signing Certification Authority), you can place
your provider code in a JAR file ([Step 6: Place Your Provider in a JAR
File](howtoimplaprovider.html#GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F))
and then use that certificate to sign the JAR file ([Step 7.2: Sign Your
Provider](howtoimplaprovider.html#GUID-CF5F0E7D-BA0E-494C-8A5A-B228FF839AEF)).

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-CF5F0E7D-BA0E-494C-8A5A-B228FF839AEF}

#### Step 7.2: Sign Your Provider {#JSSEC-GUID-CF5F0E7D-BA0E-494C-8A5A-B228FF839AEF .sect4}

<div>
<div class="section">
Sign the JAR file created in [Step 6: Place Your Provider in a JAR
File](howtoimplaprovider.html#GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F)
with the code-signing certificate obtained in [Step 7.1: Get a
Code-Signing
Certificate](howtoimplaprovider.html#GUID-434AACF7-0D2C-494A-B32A-508A6B605F62 "The next step is to request a code-signing certificate so that you can use it to sign your provider prior to testing. The certificate will be good for both testing and production. It will be valid for 5 years.").
See [jarsigner](olink:JSWOR-GUID-925E7A1B-B3F3-44D2-8B49-0B3FA2C54864)
in <span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

``` {.codeblock dir="ltr"}
    jarsigner -keystore <keystore file name> \
        -storepass <keystore password> \
        <JAR file name> <alias>
```

Here, `<alias>`{.codeph} is the alias into the keystore for the entry
containing the code-signing certificate received from the JCA Code
Signing Certification Authority (the same alias as that specified in the
commands in [Step 7.1: Get a Code-Signing
Certificate](howtoimplaprovider.html#GUID-434AACF7-0D2C-494A-B32A-508A6B605F62 "The next step is to request a code-signing certificate so that you can use it to sign your provider prior to testing. The certificate will be good for both testing and production. It will be valid for 5 years.")).

You can test verification of the signature via the following:

``` {.codeblock dir="ltr"}
    jarsigner -verify <JAR file name> 
```

The text \"jar verified\" will be displayed if the verification was
successful.

<div class="infoboxnote" id="GUID-CF5F0E7D-BA0E-494C-8A5A-B228FF839AEF__GUID-9AA0BF43-A226-4E46-9B26-5B3B9AD53531">
Note:

-   If you bundle a signed JCE provider as part of an RIA (applet or
    webstart application), for the best user experience, you should
    apply a second signature to the JCE provider JAR with the same
    certificate/key that you used to sign the applet or webstart
    application. See [Deployment Configuration File and
    Properties](olink:JSDPG747) to know about deploying RIAs, and
    [jarsigner](olink:JSWOR-GUID-925E7A1B-B3F3-44D2-8B49-0B3FA2C54864)
    in <span><cite>Java Platform, Standard Edition Tools
    Reference</cite></span> for applying multiple signatures to a JAR
    file.

-   You cannot package signed providers in JMOD files.

-   Providers don\'t need to be signed.

-   You can link a provider in a custom runtime image with the
    `jlink`{.codeph} command as long as it doesn\'t have a Cipher,
    KeyAgreement, or MAC implementation.

</div>
</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-FB9C6DB2-DE9A-4EFE-89B4-C2C168C5982D}

### Step 8: Prepare for Testing {#JSSEC-GUID-FB9C6DB2-DE9A-4EFE-89B4-C2C168C5982D .sect3}

<div>
The next steps describe how to install and configure your new provider
so that it is available via the JCA.

</div>
<div class="sect4">
[]{#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33}

#### Step 8.1: Configure the Provider {#JSSEC-GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 .sect4}

<div>
Register your provider so that the JCE framework can find your provider,
either with the <span class="apiname">ServiceLoader</span> class or in
the class path or module path.

1.  <span>Open the `java.security` file in an editor:</span>
    <div>
    -   Solaris, Linux, or macOS:
        `<java-home>/conf/security/java.security`{.codeph}

    -   Windows: `<java-home>\conf\security\java.security`{.codeph}

    </div>
2.  <span>In the `java.security` file, find the section where standard
    providers such as SUN, SunRsaSign, and SunJCE are configured as
    static providers; it looks like the following:</span>

    <div>
    ``` {.codeblock dir="ltr"}
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
    security.provider.13=SunPKCS11
    ```

    Each line in this section has the following form:

    ``` {.codeblock dir="ltr"}
    security.provider.n=provName|className 
    ```

    This declares a provider, and specifies its preference order
    `n`{.codeph}. The preference order is the order in which providers
    are searched for requested algorithms when no specific provider is
    requested. The order is 1-based; 1 is the most preferred, followed
    by 2, and so on.

    `provName`{.codeph} is the provider\'s name and `className`{.codeph}
    is the fully qualified class name of the provider. You can use
    either of these two names.

    </div>
3.  <span>Register your provider by adding to the `java.security` file a
    line with the form
    `security.provider.n=provName|className`{.codeph}.</span>

    <div>
    If you configured your provider so that the
    [<span class="apiname">ServiceLoader</span>](https://docs.oracle.com/javase/10/docs/api/java/util/ServiceLoader.html)
    class can search for it (because you packaged the provider in a
    named module as described in [Step 4: Create a Module Declaration
    for Your
    Provider](howtoimplaprovider.html#GUID-7C304A79-6D0B-438B-A02E-51648C909876 "This step is optional but recommended; it enables you to package your provider in a named module. A modular JDK can then locate your provider in the module path as opposed to the class path. The module system can more thoroughly check for dependencies in modules in the module path. Note that you can use named modules in a non-modular JDK; the module declaration will be ignored. Also, you can still package your providers in unnamed or automatic modules.")
    or added a `java.security.Provider` file as described in [Add the
    File java.security.Provider to Use the ServiceLoader Class to Search
    for
    Providers](howtoimplaprovider.html#GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F__ADDTHEFILEJAVA.SECURITY.PROVIDERTOU-025DFEDB)),
    then specify just the provider\'s name.

    If you have not configured your provider so that
    <span class="apiname">ServiceLoader</span> class can search for it,
    which means that the JCE framework will search for it in the class
    path or module path, then specify the fully qualified class name of
    your provider.

    For example, the highlighted line registers the provider
    `MyProvider`{.codeph} (whose fully qualified class name is
    `p.MyProvider`{.codeph} and has been configured so that the
    <span class="apiname">ServiceLoader</span> class can search for it)
    as the 14th preferred provider:

    ``` {.codeblock dir="ltr"}
    # ...
    security.provider.11=JdkSASL
    security.provider.12=SunMSCAPI
    security.provider.13=SunPKCS11
    security.provider.14=MyProvider
    ```

    If you are not sure if the
    <span class="apiname">ServiceLoader</span> mechanism will be used,
    or if you\'ll be deploying on a non-modular system, then you can
    also register the provider again, this time using the full class
    name:

    ``` {.oac_no_warn dir="ltr"}
    security.provider.15=p.MyProvider
    ```

    </div>

<div class="section">
Alternatively, you can register providers dynamically. To do so, a
program (such as your test program, to be written in [Step 9: Write and
Compile Your Test
Programs](howtoimplaprovider.html#GUID-C6054169-FE6E-4837-B2BD-382DFEB955C0 "Write and compile one or more test programs that test your provider's incorporation into the Security API as well as the correctness of its algorithm(s). Create any supporting files needed, such as those for test data to be encrypted."))
call either the `addProvider`{.codeph} or `insertProviderAt`{.codeph}
method in the `Security`{.codeph} class:

``` {.oac_no_warn dir="ltr"}
ServiceLoader<Provider> sl = ServiceLoader.load(java.security.Provider.class);
for (Provider p : sl) {
    System.out.println(p);
    if (p.getName().equals("MyProvider")) {
        Security.addProvider(p);
    }
}
```

This type of registration is not persistent and can only be done by code
which is granted the following permission:

``` {.codeblock dir="ltr"}
java.security.SecurityPermission "insertProvider.<provider name>"
```

For example, if the provider name is MyJCE, and if the provider\'s code
is in the `myjce_provider.jar`{.codeph} file in the
`/localWork`{.codeph} directory, then the following is a sample policy
file that contains a `grant`{.codeph} statement that grants that
permission:

``` {.codeblock dir="ltr"}
    grant codeBase "file:/localWork/myjce_provider.jar" {
        permission java.security.SecurityPermission
            "insertProvider.MyJCE";
    };
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-6E267101-15F4-4E7B-A6EB-64E36AAD1285}

#### Step 8.2: Set Provider Permissions {#JSSEC-GUID-6E267101-15F4-4E7B-A6EB-64E36AAD1285 .sect4}

<div>
<div class="section">
[Permissions](java-security-overview1.html#GUID-7A49C00B-BEA6-4050-9E32-6168211585F7 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.")
must be granted for when applications are run while a security manager
is installed. A security manager may be installed for an application
either through code in the application itself or through a command-line
argument.

</div>
<!-- class="section" -->

1.  <span>Your provider may need the following permissions granted to it
    in the client environment:</span>
    <div>
    -   `java.lang.RuntimePermission`{.codeph} to get class protection
        domains. The provider may need to get its own protection domain
        in the process of doing self-integrity checking.
    -   `java.security.SecurityPermission`{.codeph} to set provider
        properties.

    </div>
2.  <span>To ensure your provider works when a security manager is
    installed, you need to test such an installation and execution
    environment. In addition, prior to testing your need to grant
    appropriate permissions to your provider and to any other providers
    it uses.</span>

    <div>
    For example, a sample statement granting permissions to a provider
    whose name is MyJCE and whose code is in
    `myjce_provider.jar`{.codeph} appears below. Such a statement could
    appear in a policy file. In this example, the
    `myjce_provider.jar`{.codeph} file is assumed to be in the
    `/localWork`{.codeph} directory.

    ``` {.codeblock dir="ltr"}
        grant codeBase "file:/localWork/myjce_provider.jar" {
            permission java.lang.RuntimePermission "getProtectionDomain";
            permission java.security.SecurityPermission
                "putProviderProperty.MyJCE";
        };
    ```

    </div>

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-C6054169-FE6E-4837-B2BD-382DFEB955C0}

### Step 9: Write and Compile Your Test Programs {#JSSEC-GUID-C6054169-FE6E-4837-B2BD-382DFEB955C0 .sect3}

<div>
Write and compile one or more test programs that test your provider\'s
incorporation into the Security API as well as the correctness of its
algorithm(s). Create any supporting files needed, such as those for test
data to be encrypted.

1.  <span>The first tests your program should perform are ones to ensure
    that your provider is found, and that its name, version number, and
    additional information is as expected.</span>

    <div>
    To do so, you could write code like the following, substituting your
    provider name for `MyPro`{.codeph}:

    ``` {.codeblock dir="ltr"}
        import java.security.*;

        Provider p = Security.getProvider("MyPro");

        System.out.println("MyPro provider name is " + p.getName());
        System.out.println("MyPro provider version # is " + p.getVersion());
        System.out.println("MyPro provider info is " + p.getInfo());
    ```

    </div>
2.  <span>You should ensure that your services are found.</span>

    <div>
    For instance, if you implemented the AES encryption algorithm, you
    could check to ensure it\'s found when requested by using the
    following code (again substituting your provider name for
    \"MyPro\"):

    ``` {.codeblock dir="ltr"}
        Cipher c = Cipher.getInstance("AES", "MyPro");

        System.out.println("My Cipher algorithm name is " + c.getAlgorithm());
    ```

    </div>
3.  **Optional:** <span>If you don\'t specify a provider name in the
    call to `getInstance`{.codeph}, all registered providers will be
    searched, in preference order (see [Step 8.1: Configure the
    Provider](howtoimplaprovider.html#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 "Register your provider so that the JCE framework can find your provider, either with the ServiceLoader class or in the class path or module path.")),
    until one implementing the algorithm is found.</span>
4.  **Optional:** <span>If your provider implements an exemption
    mechanism, you should write a test applet or application that uses
    the exemption mechanism. Such an applet/application also needs to be
    signed, and needs to have a \"permission policy file\" bundled with
    it.</span>
    <div>
    See [How to Make Applications Exempt from Cryptographic
    Restrictions](java-cryptography-architecture-jca-reference-guide.html#GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D)
    for complete information on creating and testing such an
    application.
    </div>

</div>
</div>
<div class="sect3">
[]{#GUID-3FD26072-6982-4DCE-932C-DE152C463992}

### Step 10: Run Your Test Programs {#JSSEC-GUID-3FD26072-6982-4DCE-932C-DE152C463992 .sect3}

<div>
When you run your test applications, the required `java`{.codeph}
command options will vary depending on factors such as whether you
packaged your provider as a named, automatic, or unnamed module and if
you configured it so that the <span class="apiname">ServiceLoader</span>
class can search for it.

<div class="section">
If you packaged your provider as a named module and have configured it
so that the <span class="apiname">ServiceLoader</span> class can search
for it (by registering it with its name in the `java.security` as
described in [Step 8.1: Configure the
Provider](howtoimplaprovider.html#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 "Register your provider so that the JCE framework can find your provider, either with the ServiceLoader class or in the class path or module path.")),
then run your test program with the following command:

``` {.oac_no_warn dir="ltr"}
java --module-path "jars" <other java options>
```

The directory `jars` contains your provider.

You may require more options depending on your provider code style (see
[Step 3.1: Create a Provider That Uses String Objects to Register Its
Services](howtoimplaprovider.html#GUID-AB9C2460-0CF2-48BA-B9FE-7059071344CE)
and [Step 3.2: Create a Provider That Uses
Provider.Service](howtoimplaprovider.html#GUID-CB446B7A-CEA2-4F4A-A4AF-4D492CB58733)),
if you packaged your provider in a different kind of module, or if you
have not configured it for the
<span class="apiname">ServiceLoader</span> class. The following table
describes these options.

For the `java`{.codeph} commands, the name of the provider is
`MyProvider`{.codeph}, its fully qualified class name is
`p.MyProvider`{.codeph}, and it is packaged in the file
`com.foo.MyProvider.jar`, which is in the directory `jars`.

<div class="tblformalwide" id="GUID-3FD26072-6982-4DCE-932C-DE152C463992__GUID-BC884FEB-0E59-4323-BB7E-5AFEE114EB77">
Table 3-2 Expected Java Runtime Options for Various Provider
Implementation Styles

+-------------+-------------+-------------+-------------+-------------+
| Module Type | Provider    | Configured  | Provider    | java        |
|             | Code Style  | for         | Name Used   | Command     |
|             |             | ServiceLoad | in          |             |
|             |             | er          | java.securi |             |
|             |             | Class?      | ty          |             |
|             |             |             | File        |             |
+:============+:============+:============+:============+:============+
| Unnamed     | <span class | No          | Fully       | `java -cp " |
|             | ="apiname"> |             | qualified   | jars/com.fo |
|             | String</spa |             | class name  | o.MyProvide |
|             | n>          |             |             | r.jar" <oth |
|             | objects or  |             |             | er java opt |
|             | <span class |             |             | ions>`{.cod |
|             | ="apiname"> |             |             | eph}        |
|             | Provider.Se |             |             |             |
|             | rvice</span |             |             |             |
|             | >           |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Unnamed     | <span class | Yes         | Fully       | `java -cp " |
|             | ="apiname"> |             | qualified   | jars/com.fo |
|             | String</spa |             | class name  | o.MyProvide |
|             | n>          |             | or provider | r.jar" <oth |
|             | objects or  |             | name        | er java opt |
|             | <span class |             |             | ions>`{.cod |
|             | ="apiname"> |             |             | eph}        |
|             | Provider.Se |             |             |             |
|             | rvice</span |             |             |             |
|             | >           |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Automatic   | <span class | No          | Fully       | `java --mod |
|             | ="apiname"> |             | qualified   | ule–path "j |
|             | String</spa |             | class name  | ars/com.foo |
|             | n>          |             |             | .MyProvider |
|             | objects or  |             |             | .jar" --add |
|             | <span class |             |             | –modules=co |
|             | ="apiname"> |             |             | m.foo.MyPro |
|             | Provider.Se |             |             | vider <othe |
|             | rvice</span |             |             | r java opti |
|             | >           |             |             | ons>`{.code |
|             |             |             |             | ph}         |
+-------------+-------------+-------------+-------------+-------------+
| Automatic   | <span class | Yes         | Fully       | `java --mod |
|             | ="apiname"> |             | qualified   | ule–path "j |
|             | String</spa |             | class name  | ars/com.foo |
|             | n>          |             | or provider | .MyProvider |
|             | objects or  |             | name        | .jar" <othe |
|             | <span class |             |             | r java opti |
|             | ="apiname"> |             |             | ons>`{.code |
|             | Provider.Se |             |             | ph}         |
|             | rvice</span |             |             |             |
|             | >           |             |             |             |
+-------------+-------------+-------------+-------------+-------------+
| Named       | <span class | No          | Fully       | `java --mod |
|             | ="apiname"> |             | qualified   | ule–path "j |
|             | String</spa |             | class name  | ars" --add– |
|             | n>          |             |             | modules=com |
|             | objects or  |             |             | .foo.MyProv |
|             | <span class |             |             | ider --add– |
|             | ="apiname"> |             |             | exports=com |
|             | Provider.Se |             |             | .foo.MyProv |
|             | rvice</span |             |             | ider/p=java |
|             | >           |             |             | .base <othe |
|             |             |             |             | r java opti |
|             |             |             |             | ons>`{.code |
|             |             |             |             | ph}         |
|             |             |             |             |             |
|             |             |             |             | You can     |
|             |             |             |             | remove the  |
|             |             |             |             | `--add-expo |
|             |             |             |             | rts`{.codep |
|             |             |             |             | h}          |
|             |             |             |             | option if   |
|             |             |             |             | you add     |
|             |             |             |             | `exports p` |
|             |             |             |             | {.codeph}   |
|             |             |             |             | in the      |
|             |             |             |             | module      |
|             |             |             |             | declaration |
|             |             |             |             | .           |
+-------------+-------------+-------------+-------------+-------------+
| Named       | <span class | Yes         | Fully       | `java --mod |
|             | ="apiname"> |             | qualified   | ule–path "j |
|             | String</spa |             | class name  | ars" --add– |
|             | n>          |             |             | exports=com |
|             | objects     |             |             | .foo.MyProv |
|             |             |             |             | ider/p=java |
|             |             |             |             | .base <othe |
|             |             |             |             | r java opti |
|             |             |             |             | ons>`{.code |
|             |             |             |             | ph}         |
|             |             |             |             |             |
|             |             |             |             | You can     |
|             |             |             |             | remove the  |
|             |             |             |             | `--add-expo |
|             |             |             |             | rts`{.codep |
|             |             |             |             | h}          |
|             |             |             |             | option if   |
|             |             |             |             | you add     |
|             |             |             |             | `exports p` |
|             |             |             |             | {.codeph}   |
|             |             |             |             | in the      |
|             |             |             |             | module      |
|             |             |             |             | declaration |
|             |             |             |             | .           |
+-------------+-------------+-------------+-------------+-------------+
| Named       | <span class | Yes         | Provider    | `java --mod |
|             | ="apiname"> |             | name        | ule–path "j |
|             | String</spa |             |             | ars" --add– |
|             | n>          |             |             | exports=com |
|             | objects     |             |             | .foo.MyProv |
|             |             |             |             | ider/p=java |
|             |             |             |             | .base <othe |
|             |             |             |             | r java opti |
|             |             |             |             | ons>`{.code |
|             |             |             |             | ph}         |
|             |             |             |             |             |
|             |             |             |             | You can     |
|             |             |             |             | remove the  |
|             |             |             |             | `--add-expo |
|             |             |             |             | rts`{.codep |
|             |             |             |             | h}          |
|             |             |             |             | option if   |
|             |             |             |             | you add     |
|             |             |             |             | `exports p` |
|             |             |             |             | {.codeph}   |
|             |             |             |             | in the      |
|             |             |             |             | module      |
|             |             |             |             | declaration |
|             |             |             |             | .           |
+-------------+-------------+-------------+-------------+-------------+
| Named       | <span class | Yes         | Fully       | `java --mod |
|             | ="apiname"> |             | qualified   | ule–path "j |
|             | Provider.Se |             | class name  | ars" --add– |
|             | rvice</span |             |             | exports=com |
|             | >           |             |             | .foo.MyProv |
|             |             |             |             | ider/p=java |
|             |             |             |             | .base<other |
|             |             |             |             |  java optio |
|             |             |             |             | ns>`{.codep |
|             |             |             |             | h}          |
|             |             |             |             |             |
|             |             |             |             | You can     |
|             |             |             |             | remove the  |
|             |             |             |             | `--add-expo |
|             |             |             |             | rts`{.codep |
|             |             |             |             | h}          |
|             |             |             |             | option if   |
|             |             |             |             | you add     |
|             |             |             |             | `exports p` |
|             |             |             |             | {.codeph}   |
|             |             |             |             | in the      |
|             |             |             |             | module      |
|             |             |             |             | declaration |
|             |             |             |             | .           |
+-------------+-------------+-------------+-------------+-------------+
| Named       | <span class | Yes         | Provider    | `java --mod |
|             | ="apiname"> |             | name        | ule–path "j |
|             | Provider.Se |             |             | ars" <other |
|             | rvice</span |             |             |  java optio |
|             | >           |             |             | ns>`{.codep |
|             |             |             |             | h}          |
+-------------+-------------+-------------+-------------+-------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="p">
Once you have determined the proper `java`{.codeph} options for your
test programs, run them. Debug your code and continue testing as needed.
If the Java runtime cannot seem to find one of your algorithms, review
the previous steps and ensure that they are all completed.

Be sure to include testing of your programs using different installation
options (for example, configured to use the
<span class="apiname">ServiceLoader</span> class or to be found in the
class path or module path) and execution environments (with or without a
security manager running).

</div>
<!-- class="section" -->

<div class="p">
</div>
<!-- class="section" -->

1.  [**Optional:** <span>If you find during testing that your code needs
    modification, make the changes and recompile [Step 5: Compile Your
    Code](howtoimplaprovider.html#GUID-83742677-6E39-4A8D-BF0F-BC743E3AE43C).</span>]{#GUID-3FD26072-6982-4DCE-932C-DE152C463992__IFYOUFINDDURINGTESTINGTHATYOURCODEN-7568E2A4}
2.  <span>Place the updated provider code in a JAR file ([Step 6: Place
    Your Provider in a JAR
    File](howtoimplaprovider.html#GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F)).</span>
3.  <span>Sign the JAR file ([Step 7: Sign Your JAR File, If
    Necessary](howtoimplaprovider.html#GUID-2D4432F9-1C3C-4A91-8612-2B2840188B36)).</span>
4.  <span>Re-configure the provider ([Step 8.1: Configure the
    Provider](howtoimplaprovider.html#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 "Register your provider so that the JCE framework can find your provider, either with the ServiceLoader class or in the class path or module path.")).</span>
5.  **Optional:** <span>If needed, fix or add to the permissions ([Step
    8.2: Set Provider
    Permissions](howtoimplaprovider.html#GUID-6E267101-15F4-4E7B-A6EB-64E36AAD1285)).</span>
6.  [<span>Run your
    programs.</span>]{#GUID-3FD26072-6982-4DCE-932C-DE152C463992__RE-TESTYOURPROGRAMS.-7568E6BE}
7.  **Optional:** <span>If required, repeat steps 1 to 6.</span>

</div>
</div>
<div class="sect3">
[]{#GUID-A62916EE-BE09-4229-9D05-3D6AF303CA4E}

### Step 11: Apply for U.S. Government Export Approval If Required {#JSSEC-GUID-A62916EE-BE09-4229-9D05-3D6AF303CA4E .sect3}

<div>
All U.S. vendors whose providers may be exported outside the U.S. should
apply to the Bureau of Industry and Security in the U.S. Department of
Commerce for export approval.

<div class="section">
Please consult your export counsel for more information.

<div class="p">
<div class="infoboxnote" id="GUID-A62916EE-BE09-4229-9D05-3D6AF303CA4E__GUID-1600EB10-8AAE-40E5-8BFB-3CB61D506E4B">
Note:

If your provider calls `Cipher.getInstance()`{.codeph} and the returned
`Cipher`{.codeph} object needs to perform strong cryptography regardless
of what cryptographic strength is allowed by the user\'s downloaded
jurisdiction policy files, you should include a copy of the
`cryptoPerms`{.codeph} permission policy file which you intend to bundle
in the JAR file for your provider and which specifies an appropriate
permission for the required cryptographic strength. The necessity for
this file is just like the requirement that applets and applications
\"exempt\" from cryptographic restrictions must include a
`cryptoPerms`{.codeph} permission policy file in their JAR file. See
[How to Make Applications Exempt from Cryptographic
Restrictions](java-cryptography-architecture-jca-reference-guide.html#GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D).

</div>
</div>
Here are two URLs that may be useful:

-   [US Department of Commerce](http://www.commerce.gov)
-   [Bureau of Industry and Security](http://www.bis.doc.gov)

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-912FAB1D-628A-47EA-A1DD-A216F2DD4245}

### Step 12: Document Your Provider and Its Supported Services {#JSSEC-GUID-912FAB1D-628A-47EA-A1DD-A216F2DD4245 .sect3}

<div>
<div class="section">
The next step is to write documentation for your clients. At the
minimum, you need to specify:

</div>
<!-- class="section" -->

-   <span>The name programs should use to refer to your provider.</span>

    <div>
    <div class="infoboxnote" id="GUID-912FAB1D-628A-47EA-A1DD-A216F2DD4245__GUID-49816D37-1A18-4121-A552-CB368FB6ABA6">
    Note:

    As of this writing, provider name searches are
    <span class="bold">case-sensitive</span>. That is, if your master
    class specifies your provider name as \"CryptoX\" but a user
    requests \"CRYPTOx\", your provider will not be found. This behavior
    may change in the future, but for now be sure to warn your clients
    to use the exact case you specify.

    </div>
    </div>
-   <span>The types of algorithms and other services implemented by your
    provider.</span>
-   <span>Instructions for installing the provider, similar to those
    provided in [Step 8.1: Configure the
    Provider](howtoimplaprovider.html#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33 "Register your provider so that the JCE framework can find your provider, either with the ServiceLoader class or in the class path or module path."),
    except that the information and examples should be specific to your
    provider.</span>
-   <span>The permissions your provider will require if a security
    manager is run, as described in [Step 8.2: Set Provider
    Permissions](howtoimplaprovider.html#GUID-6E267101-15F4-4E7B-A6EB-64E36AAD1285).</span>

<div class="section">
In addition, your documentation should specify anything else of interest
to clients, such as any default algorithm parameters.

</div>
<!-- class="section" -->

</div>
<div class="sect4">
[]{#GUID-CC2277C4-14EA-45A8-BC81-8A0715FDC8E9}

#### Step 12.1: Indicate Whether Your Implementation is Cloneable for Message Digests and MACs {#JSSEC-GUID-CC2277C4-14EA-45A8-BC81-8A0715FDC8E9 .sect4}

<div>
For each Message Digest and MAC algorithm, indicate whether or not your
implementation is cloneable. This is not technically necessary, but it
may save clients some time and coding by telling them whether or not
intermediate Message Digests or MACs may be possible through cloning.

<div class="section">
Clients who do not know whether or not a `MessageDigest`{.codeph} or
`Mac`{.codeph} implementation is cloneable can find out by attempting to
clone the object and catching the potential exception, as illustrated by
the following example:

``` {.codeblock dir="ltr"}
    try {
        // try and clone it
        /* compute the MAC for i1 */
        mac.update(i1);
        byte[] i1Mac = mac.clone().doFinal();

        /* compute the MAC for i1 and i2 */
        mac.update(i2);
        byte[] i12Mac = mac.clone().doFinal();

        /* compute the MAC for i1, i2 and i3 */
        mac.update(i3);
        byte[] i123Mac = mac.doFinal();
    } catch (CloneNotSupportedException cnse) {
        // have to use an approach not involving cloning
    } 
```

Where,

[<!-- -->]{#GUID-CC2277C4-14EA-45A8-BC81-8A0715FDC8E9__GUID-7F81CA19-A39F-4982-BEE5-24482BB92369}`mac`{.codeph}
:   Indicates the MAC object they received when they requested one via a
    call to `Mac.getInstance`{.codeph}

[<!-- -->]{#GUID-CC2277C4-14EA-45A8-BC81-8A0715FDC8E9__GUID-68D66E9E-92AD-4A6F-B888-6E46A19A0330}`i1`{.codeph}, `i2`{.codeph} and `i3`{.codeph}
:   Indicates input byte arrays, and they want to calculate separate
    hashes for:
    -   `i1`{.codeph}
    -   `i1 and i2`{.codeph}
    -   `i1, i2, and i3`{.codeph}

</div>
<!-- class="section" -->

<div class="section">
Key Pair Generators

For a key pair generator algorithm, in case the client does not
explicitly initialize the key pair generator (via a call to an
`initialize`{.codeph} method), each provider must supply and document a
default initialization.

For example, the Diffie-Hellman key pair generator supplied by the
<span class="variable">SunJCE</span> provider uses a default prime
modulus size (`keysize`{.codeph}) of 2048 bits.

</div>
<!-- class="section" -->

<div class="section">
Key Factories

A provider should document all the key specifications supported by its
(secret-)key factory.

</div>
<!-- class="section" -->

<div class="section">
Algorithm Parameter Generators

In case the client does not explicitly initialize the algorithm
parameter generator (via a call to an `init`{.codeph} method in the
`AlgorithmParameterGenerator`{.codeph} engine class), each provider must
supply and document a default initialization.

For example, the <span class="variable">SunJCE</span> provider uses a
default prime modulus size (`keysize`{.codeph}) of 2048 bits for the
generation of Diffie-Hellman parameters, the
<span class="variable">Sun</span> provider a default modulus prime size
of 2048 bits for the generation of DSA parameters.

</div>
<!-- class="section" -->

<div class="section">
Signature Algorithms

If you implement a signature algorithm, you should document the format
in which the signature (generated by one of the `sign`{.codeph} methods)
is encoded.

For example, the SHA256withDSA signature algorithm supplied by the
\"SUN\" provider encodes the signature as a standard
`ASN.1 SEQUENCE`{.codeph} of two integers, `r`{.codeph} and
`s`{.codeph}.

</div>
<!-- class="section" -->

<div class="section">
Random Number Generation (SecureRandom) Algorithms

For a random number generation algorithm, provide information regarding
how \"random\" the numbers generated are, and the quality of the seed
when the random number generator is self-seeding. Also note what happens
when a `SecureRandom`{.codeph} object (and its encapsulated
`SecureRandomSpi`{.codeph} implementation object) is deserialized: If
subsequent calls to the `nextBytes`{.codeph} method (which invokes the
`engineNextBytes`{.codeph} method of the encapsulated
`SecureRandomSpi`{.codeph} object) of the restored object yield the
exact same (random) bytes as the original object would, then let users
know that if this behavior is undesirable, they should seed the restored
random object by calling its `setSeed`{.codeph} method.

</div>
<!-- class="section" -->

<div class="section">
Certificate Factories

A provider should document what types of certificates (and their version
numbers, if relevant), can be created by the factory.

</div>
<!-- class="section" -->

<div class="section">
Keystores

A provider should document any relevant information regarding the
keystore implementation, such as its underlying data format.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-3521E2A8-93B5-4D0F-AE2D-DC1B5E6857B7}

### Step 13: Make Your Class Files and Documentation Available to Clients {#JSSEC-GUID-3521E2A8-93B5-4D0F-AE2D-DC1B5E6857B7 .sect3}

<div>
After writing, configuring, testing, installing and documenting your
provider software, make documentation available to your customers.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-C8B79D46-6EA9-4E27-8083-7CB967732BB3}

Further Implementation Details and Requirements {#JSSEC-GUID-C8B79D46-6EA9-4E27-8083-7CB967732BB3 .sect2}
-----------------------------------------------

<div>
This section provides additional information about alias names, service
interdependencies, algorithm parameter generators and algorithm
parameters.

</div>
<div class="sect3">
[]{#GUID-735A3CD6-0EE5-423C-B5BA-61500BA20854}

### Alias Names {#JSSEC-GUID-735A3CD6-0EE5-423C-B5BA-61500BA20854 .sect3}

<div>
In the JDK, the aliasing scheme enables clients to use aliases when
referring to algorithms or types, rather than the standard names.

For many cryptographic algorithms and types, there is a single official
\"standard name\" defined in the [Java Security Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).

For example, \"SHA-256\" is the standard name for the SHA-256 Message
Digest algorithm defined in RFC 1321. `DiffieHellman`{.codeph} is the
standard for the Diffie-Hellman key agreement algorithm defined in
PKCS3.

In the JDK, there is an aliasing scheme that enables clients to use
aliases when referring to algorithms or types, rather than their
standard names.

For example, the \"SUN\" provider\'s master class (`Sun.java`{.codeph})
defines the alias `"SHA1/DSA"`{.codeph} for the algorithm whose standard
name is `"SHA1withDSA"`{.codeph}. Thus, the following statements are
equivalent:

``` {.codeblock dir="ltr"}
    Signature sig = Signature.getInstance("SHA1withDSA", "SUN");

    Signature sig = Signature.getInstance("SHA1/DSA", "SUN");
```

Aliases can be defined in your \"master class\" (see [Step 3: Write Your
Master Class, a Subclass of
Provider](howtoimplaprovider.html#GUID-1C82EDB9-96CA-44AB-8590-E299814D6A46 "Create a subclass of the java.security.Provider class. This is essentially a lookup table that advertises the algorithms that your provider implements.")).
To define an alias, create a property named

``` {.codeblock dir="ltr"}
    Alg.Alias.engineClassName.aliasName
```

where <span class="variable">engineClassName</span> is the name of an
engine class (e.g., `Signature`{.codeph}), and
<span class="variable">aliasName</span> is your alias name. The
<span class="variable">value</span> of the property must be the standard
algorithm (or type) name for the algorithm (or type) being aliased.

As an example, the \"SUN\" provider defines the alias
`"SHA1/DSA"`{.codeph} for the signature algorithm whose standard name is
`"SHA1withDSA"`{.codeph} by setting a property named
`Alg.Alias.Signature.SHA1/DSA`{.codeph} to have the value
`SHA1withDSA`{.codeph} via the following:

``` {.codeblock dir="ltr"}
    put("Alg.Alias.Signature.SHA1/DSA", "SHA1withDSA");
```

<div class="infoboxnote" id="GUID-735A3CD6-0EE5-423C-B5BA-61500BA20854__GUID-A60FE441-C25A-4F2E-B63D-944121E2B674">
Note:

The aliases defined by one provider are available only to that provider
and not to any other providers. Thus, aliases defined by the
<span class="variable">SunJCE</span> provider are available only to the
<span class="variable">SunJCE</span> provider.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-8ED3CE1A-B25A-4E16-B45D-4EB36C9A7406}

### Service Interdependencies {#JSSEC-GUID-8ED3CE1A-B25A-4E16-B45D-4EB36C9A7406 .sect3}

<div>
Some algorithms require the use of other types of algorithms. For
example, a PBE algorithm usually needs to use a message digest algorithm
in order to transform a password into a key.

If you are implementing one type of algorithm that requires another, you
can do one of the following:

-   Provide your own implementations for both.

-   Let your implementation of one algorithm use an instance of the
    other type of algorithm, as supplied by the default
    <span class="variable">Sun</span> provider that is included with
    every Java SE Platform installation. For example, if you are
    implementing a PBE algorithm that requires a message digest
    algorithm, you can obtain an instance of a class implementing the
    SHA256 message digest algorithm by calling:

    ``` {.oac_no_warn dir="ltr"}
        MessageDigest.getInstance("SHA256", "SUN")
    ```

-   Let your implementation of one algorithm use an instance of the
    other type of algorithm, as supplied by another specific provider.
    This is only appropriate if you are sure that all clients who will
    use your provider will also have the other provider installed.

-   Let your implementation of one algorithm use an instance of the
    other type of algorithm, as supplied by another (unspecified)
    provider. That is, you can request an algorithm by name, but without
    specifying any particular provider, as in:

    ``` {.oac_no_warn dir="ltr"}
        MessageDigest.getInstance("SHA256")
    ```

    This is only appropriate if you are sure that there will be at least
    one implementation of the requested algorithm (in this case, SHA256)
    installed on each Java platform where your provider will be used.

Here are some common types of algorithm interdependencies:

<div class="section">
Signature and Message Digest Algorithms

A signature algorithm often requires use of a message digest algorithm.
For example, the SHA256withDSA signature algorithm requires the SHA256
message digest algorithm.

</div>
<!-- class="section" -->

<div class="section">
Signature and (Pseudo-)Random Number Generation Algorithms

A signature algorithm often requires use of a (pseudo-)random number
generation algorithm. For example, such an algorithm is required in
order to generate a DSA signature.

</div>
<!-- class="section" -->

<div class="section">
Key Pair Generation and Message Digest Algorithms

A key pair generation algorithm often requires use of a message digest
algorithm. For example, DSA keys are generated using the SHA-256 message
digest algorithm.

</div>
<!-- class="section" -->

<div class="section">
Algorithm Parameter Generation and Message Digest Algorithms

An algorithm parameter generator often requires use of a message digest
algorithm. For example, DSA parameters are generated using the SHA-256
message digest algorithm.

</div>
<!-- class="section" -->

<div class="section">
Keystores and Message Digest Algorithms

A keystore implementation will often utilize a message digest algorithm
to compute keyed hashes (where the key is a user-provided password) to
check the integrity of a keystore and make sure that the keystore has
not been tampered with.

</div>
<!-- class="section" -->

<div class="section">
Key Pair Generation Algorithms and Algorithm Parameter Generators

A key pair generation algorithm sometimes needs to generate a new set of
algorithm parameters. It can either generate the parameters directly, or
use an algorithm parameter generator.

</div>
<!-- class="section" -->

<div class="section">
Key Pair Generation, Algorithm Parameter Generation, and (Pseudo-)Random
Number Generation Algorithms

A key pair generation algorithm may require a source of randomness in
order to generate a new key pair and possibly a new set of parameters
associated with the keys. That source of randomness is represented by a
<span class="apiname">SecureRandom</span> object. The implementation of
the key pair generation algorithm may generate the key parameters
itself, or may use an algorithm parameter generator to generate them, in
which case it may or may not initialize the algorithm parameter
generator with a source of randomness.

</div>
<!-- class="section" -->

<div class="section">
Algorithm Parameter Generators and Algorithm Parameters

An algorithm parameter generator\'s
<span class="apiname">engineGenerateParameters</span> method must return
an <span class="apiname">AlgorithmParameters</span> instance.

</div>
<!-- class="section" -->

<div class="section">
Signature and Key Pair Generation Algorithms or Key Factories

If you are implementing a signature algorithm, your implementation\'s
<span class="apiname">engineInitSign</span> and
<span class="apiname">engineInitVerify</span> methods will require
passed-in keys that are valid for the underlying algorithm (e.g., DSA
keys for the DSS algorithm). You can do one of the following:

-   Also create your own classes implementing appropriate interfaces
    (e.g. classes implementing the
    <span class="apiname">DSAPrivateKey</span> and
    <span class="apiname">DSAPublicKey</span> interfaces from the
    package <span class="apiname">java.security.interfaces</span>), and
    create your own key pair generator and/or key factory returning keys
    of those types. Require the keys passed to
    <span class="apiname">engineInitSign</span> and
    <span class="apiname">engineInitVerify</span> to be the types of
    keys you have implemented, that is, keys generated from your key
    pair generator or key factory. Or you can,

-   Accept keys from other key pair generators or other key factories,
    as long as they are instances of appropriate interfaces that enable
    your signature implementation to obtain the information it needs
    (such as the private and public keys and the key parameters). For
    example, the <span class="apiname">engineInitSign</span> method for
    a DSS <span class="apiname">Signature</span> class could accept any
    private keys that are instances of
    <span class="apiname">java.security.interfaces.DSAPrivateKey</span>.

</div>
<!-- class="section" -->

<div class="section">
Keystores and Key and Certificate Factories

A keystore implementation will often utilize a key factory to parse the
keys stored in the keystore, and a certificate factory to parse the
certificates stored in the keystore.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-A46F72E3-DFF4-4864-8BBC-30684ADF78BA}

### Default Initialization {#JSSEC-GUID-A46F72E3-DFF4-4864-8BBC-30684ADF78BA .sect3}

<div>
In case the client does not explicitly initialize a key pair generator
or an algorithm parameter generator, each provider of such a service
must supply (and document) a default initialization.

<div class="example" id="GUID-A46F72E3-DFF4-4864-8BBC-30684ADF78BA__GUID-9E8C5B1A-BE08-456F-AD70-62B0CFD8764F">
For example, the <span class="variable">Sun</span> provider uses a
default modulus size (strength) of 1024 bits for the generation of DSA
parameters, and the \"SunJCE\" provider uses a default modulus size
(keysize) of 2048 bits for the generation of Diffie-Hellman parameters.

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-A80C8BAC-AD25-4328-AE62-987F805B6BAF}

### Default Key Pair Generator Parameter Requirements {#JSSEC-GUID-A80C8BAC-AD25-4328-AE62-987F805B6BAF .sect3}

<div>
If you implement a key pair generator, your implementation should supply
default parameters that are used when clients don\'t specify parameters.

<div class="section">
The documentation you supply ([Step 12: Document Your Provider and Its
Supported
Services](howtoimplaprovider.html#GUID-912FAB1D-628A-47EA-A1DD-A216F2DD4245))
should state what the default parameters are.

For example, the DSA key pair generator in the
<span class="variable">Sun</span> provider supplies a set of
pre-computed `p`{.codeph}, `q`{.codeph}, and `g`{.codeph} default values
for the generation of 512, 768, 1024, and 2048-bit key pairs. The
following `p`{.codeph}, `q`{.codeph}, and `g`{.codeph} values are used
as the default values for the generation of 1024-bit DSA key pairs:

``` {.codeblock dir="ltr"}
p = fd7f5381 1d751229 52df4a9c 2eece4e7 f611b752 3cef4400 c31e3f80
    b6512669 455d4022 51fb593d 8d58fabf c5f5ba30 f6cb9b55 6cd7813b
    801d346f f26660b7 6b9950a5 a49f9fe8 047b1022 c24fbba9 d7feb7c6
    1bf83b57 e7c6a8a6 150f04fb 83f6d3c5 1ec30235 54135a16 9132f675
    f3ae2b61 d72aeff2 2203199d d14801c7

q = 9760508f 15230bcc b292b982 a2eb840b f0581cf5

g = f7e1a085 d69b3dde cbbcab5c 36b857b9 7994afbb fa3aea82 f9574c0b
    3d078267 5159578e bad4594f e6710710 8180b449 167123e8 4c281613
    b7cf0932 8cc8a6e1 3c167a8b 547c8d28 e0a3ae1e 2bb3a675 916ea37f
    0bfa2135 62f1fb62 7a01243b cca4f1be a8519089 a883dfe1 5ae59f06
    928b665e 807b5525 64014c3b fecf492a
```

(The `p`{.codeph} and `q`{.codeph} values given here were generated by
the prime generation standard, using the 160-bit

``` {.codeblock dir="ltr"}
SEED:  8d515589 4229d5e6 89ee01e6 018a237e 2cae64cd
```

With this seed, the algorithm found `p`{.codeph} and `q`{.codeph} when
the counter was at 92.)

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-B1428B09-5542-4D36-9C0D-D78A8B2B3C00}

### The Provider.Service Class {#JSSEC-GUID-B1428B09-5542-4D36-9C0D-D78A8B2B3C00 .sect3}

<div>
`Provider.Service`{.codeph} class offers an alternative way for
providers to advertise their services and supports additional features.

<div class="section">
Since its introduction, security providers have published their service
information via appropriately formatted key-value String pairs they put
in their Hashtable entries. While this mechanism is simple and
convenient, it limits the amount customization possible. As a result,
JDK 5.0 introduced a second option, the `Provider.Service`{.codeph}
class. It offers an alternative way for providers to advertise their
services and supports additional features as described below. Note that
this addition is fully compatible with the older method of using String
valued Hashtable entries. A provider on JDK 5.0 can choose either method
as it prefers, or even use both at the same time.

A `Provider.Service`{.codeph} object encapsulates all information about
a service. This is the provider that offers the service, its type (e.g.
`MessageDigest`{.codeph} or `Signature`{.codeph}), the algorithm name,
and the name of the class that implements the service. Optionally, it
also includes a list of alternate algorithm names for this service
(aliases) and attributes, which are a map of (name, value) String pairs.
In addition, it defines the methods `newInstance()`{.codeph} and
`supportsParameter()`{.codeph}. They have default implementations, but
can be overridden by providers if needed, as may be the case with
providers that interface with hardware security tokens.

The `newInstance()`{.codeph} method is used by the security framework
when it needs to construct new implementation instances. The default
implementation uses reflection to invoke the standard constructor for
the respective type of service. For all standard services except
`CertStore`{.codeph}, this is the no-args constructor. The
`constructorParameter`{.codeph} to
<span class="apiname">newInstance()</span> must be null in theses cases.
For services of type `CertStore`{.codeph}, the constructor that takes a
`CertStoreParameters`{.codeph} object is invoked, and
`constructorParameter`{.codeph} must be a non-null instance of
`CertStoreParameters.`{.codeph} A security provider can override the
<span class="apiname">newInstance()</span> method to implement
instantiation as appropriate for that implementation. It could use
direct invocation or call a constructor that passes additional
information specific to the Provider instance or token. For example, if
multiple Smartcard readers are present on the system, it might pass
information about which reader the newly created service is to be
associated with. However, despite customization all implementations must
follow the conventions about `constructorParameter`{.codeph} described
above.

The <span class="apiname">supportsParameter()</span> tests whether the
Service can use the specified parameter. It returns false if this
service cannot use the parameter. It returns true if this service can
use the parameter, if a fast test is infeasible, or if the status is
unknown. It is used by the security framework with some types of
services to quickly exclude non-matching implementations from
consideration. It is currently only defined for the following standard
services: `Signature`{.codeph}, `Cipher`{.codeph}, `Mac`{.codeph}, and
`KeyAgreement`{.codeph}. The `parameter`{.codeph} must be an instance of
`Key`{.codeph} in these cases. For example, for `Signature`{.codeph}
services, the framework tests whether the service can use the supplied
Key before instantiating the service. The default implementation
examines the attributes `SupportedKeyFormats`{.codeph} and
`SupportedKeyClasses`{.codeph} as described below. Again, a provider may
override this methods to implement additional tests.

The `SupportedKeyFormats`{.codeph} attribute is a list of the supported
formats for encoded keys (as returned by `key.getFormat()`{.codeph})
separated by the \"\|\" (pipe) character. For example,
`X.509|PKCS#8`{.codeph}. The `SupportedKeyClasses`{.codeph} attribute is
a list of the names of classes of interfaces separated by the \"\|\"
character. A key object is considered to be acceptable if it is
assignable to at least one of those classes or interfaces named. In
other words, if the class of the key object is a subclass of one of the
listed classes (or the class itself) or if it implements the listed
interface. An example value is
`"java.security.interfaces.RSAPrivateKey|java.security.interfaces.RSAPublicKey"`{.codeph}
.

Four methods have been added to the Provider class for adding and
looking up Services. As mentioned earlier, the implementation of those
methods and also of the existing Properties methods have been
specifically designed to ensure compatibility with existing Provider
subclasses. This is achieved as follows:

If legacy Properties methods are used to add entries, the Provider class
makes sure that the property strings are parsed into equivalent Service
objects prior to lookup via <span class="apiname">getService()</span>.
Similarly, if the <span class="apiname">putService()</span> method is
used, equivalent property strings are placed into the provider\'s
hashtable at the same time. If a provider implementation overrides any
of the methods in the Provider class, it has to ensure that its
implementation does not interfere with this conversion. To avoid
problems, we recommend that implementations do not override any of the
methods in the `Provider`{.codeph} class.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-604DD293-1F38-487D-A2F9-F9E95F5D727C}

### Signature Formats {#JSSEC-GUID-604DD293-1F38-487D-A2F9-F9E95F5D727C .sect3}

<div>
The signature algorithm should specify the format in which the signature
is encoded.

<div class="section">
If you implement a signature algorithm, the documentation you supply
([Step 12: Document Your Provider and Its Supported
Services](howtoimplaprovider.html#GUID-912FAB1D-628A-47EA-A1DD-A216F2DD4245))
should specify the format in which the signature (generated by one of
the `sign`{.codeph} methods) is encoded.

For example, the <span class="variable">SHA1withDSA</span> signature
algorithm supplied by the <span class="variable">Sun</span> provider
encodes the signature as a standard ASN.1 sequence of two
`ASN.1 INTEGER`{.codeph} values: `r`{.codeph} and `s`{.codeph}, in that
order:

``` {.codeblock dir="ltr"}
SEQUENCE ::= {
        r INTEGER,
        s INTEGER }
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9}

### DSA Interfaces and their Required Implementations {#JSSEC-GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9 .sect3}

<div>
The Java Security API contains interfaces (in the
`java.security.interfaces`{.codeph} package) for the convenience of
programmers implementing DSA services.

<div class="section">
The Java Security API contains the following interfaces:

-   [`Interface DSAKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAKey.html)

-   [`Interface DSAKeyPairGenerator`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAKeyPairGenerator.html)

-   [`Interface DSAParams`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAParams.html)

-   [`Interface DSAPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAPrivateKey.html)

-   [`Interface DSAPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAPublicKey.html)

The following sections discuss requirements for implementations of these
interfaces.

</div>
<!-- class="section" -->

<div class="section" id="GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9__DSAKEYPAIRGENERATOR-7140AF61">
DSAKeyPairGenerator

The interface
[`Interface DSAKeyPairGenerator`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAKeyPairGenerator.html)
is obsolete. It used to be needed to enable clients to provide
DSA-specific parameters to be used rather than the default parameters
your implementation supplies. However, in Java it is no longer
necessary; a new `KeyPairGenerator`{.codeph} `initialize`{.codeph}
method that takes an `AlgorithmParameterSpec`{.codeph} parameter enables
clients to indicate algorithm-specific parameters.

</div>
<!-- class="section" -->

<div class="section" id="GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9__DSAPARAMSIMPLEMENTATION-7140B38E">
DSAParams Implementation

If you are implementing a DSA key pair generator, you need a class
implementing
[`Interface DSAParams`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAParams.html)
for holding and returning the `p`{.codeph}, `q`{.codeph}, and
`g`{.codeph} parameters.

A `DSAParams`{.codeph} implementation is also required if you implement
the `DSAPrivateKey`{.codeph} and `DSAPublicKey`{.codeph} interfaces.
`DSAPublicKey`{.codeph} and `DSAPrivateKey`{.codeph} both extend the
DSAKey interface, which contains a `getParams`{.codeph} method that must
return a `DSAParams`{.codeph} object.

<div class="p">
<div class="infoboxnote" id="GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9__GUID-421108DE-1D1A-4A5F-BB41-D64F0B5B8B38">
Note:

There is a `DSAParams`{.codeph} implementation built into the JDK: the
`java.security.spec.DSAParameterSpec`{.codeph} class.

</div>
</div>
</div>
<!-- class="section" -->

<div class="section" id="GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9__DSAPRIVATEKEYANDDSAPUBLICKEYIMPLEME-7140B6D2">
DSAPrivateKey and DSAPublicKey Implementations

If you implement a DSA key pair generator or key factory, you need to
create classes implementing the
[`Interface DSAPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAPrivateKey.html)
and
[`Interface DSAPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAPublicKey.html)
interfaces.

If you implement a DSA key pair generator, your
`generateKeyPair`{.codeph} method (in your
`KeyPairGeneratorSpi`{.codeph} subclass) will return instances of your
implementations of those interfaces.

If you implement a DSA key factory, your
`engineGeneratePrivate`{.codeph} method (in your
`KeyFactorySpi`{.codeph} subclass) will return an instance of your
`DSAPrivateKey`{.codeph} implementation, and your
`engineGeneratePublic`{.codeph} method will return an instance of your
`DSAPublicKey`{.codeph} implementation.

Also, your `engineGetKeySpec`{.codeph} and `engineTranslateKey`{.codeph}
methods will expect the passed-in key to be an instance of a
`DSAPrivateKey`{.codeph} or `DSAPublicKey`{.codeph} implementation. The
`getParams`{.codeph} method provided by the interface implementations is
useful for obtaining and extracting the parameters from the keys and
then using the parameters, for example as parameters to the
`DSAParameterSpec`{.codeph} constructor called to create a parameter
specification from parameter values that could be used to initialize a
`KeyPairGenerator`{.codeph} object for DSA.

If you implement a DSA signature algorithm, your
`engineInitSign`{.codeph} method (in your `SignatureSpi`{.codeph}
subclass) will expect to be passed a `DSAPrivateKey`{.codeph} and your
`engineInitVerify`{.codeph} method will expect to be passed a
`DSAPublicKey`{.codeph}.

Please note: The `DSAPublicKey`{.codeph} and `DSAPrivateKey`{.codeph}
interfaces define a very generic, provider-independent interface to DSA
public and private keys, respectively. The `engineGetKeySpec`{.codeph}
and `engineTranslateKey`{.codeph} methods (in your
`KeyFactorySpi`{.codeph} subclass) could additionally check if the
passed-in key is actually an instance of their provider\'s own
implementation of `DSAPrivateKey`{.codeph} or `DSAPublicKey`{.codeph},
e.g., to take advantage of provider-specific implementation details. The
same is true for the DSA signature algorithm `engineInitSign`{.codeph}
and `engineInitVerify`{.codeph} methods (in your `SignatureSpi`{.codeph}
subclass).

To see what methods need to be implemented by classes that implement the
`DSAPublicKey`{.codeph} and `DSAPrivateKey`{.codeph} interfaces, first
note the following interface signatures:

In the `java.security.interfaces`{.codeph} package:

``` {.codeblock dir="ltr"}
   public interface DSAPrivateKey extends DSAKey,
                java.security.PrivateKey

   public interface DSAPublicKey extends DSAKey,
                java.security.PublicKey

   public interface DSAKey 
```

In the `java.security`{.codeph} package:

``` {.codeblock dir="ltr"}
   public interface PrivateKey extends Key

   public interface PublicKey extends Key

   public interface Key extends java.io.Serializable 
```

In order to implement the `DSAPrivateKey`{.codeph} and
`DSAPublicKey`{.codeph} interfaces, you must implement the methods they
define as well as those defined by interfaces they extend, directly or
indirectly.

Thus, for private keys, you need to supply a class that implements

-   The `getX`{.codeph} method from the
    [`Interface DSAPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAPrivateKey.html)
    interface.
-   The `getParams`{.codeph} method from the
    [`Interface DSAKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAKey.html)
    interface, since `DSAPrivateKey`{.codeph} extends `DSAKey`{.codeph}.
    Note: The `getParams`{.codeph} method returns a `DSAParams`{.codeph}
    object, so you must also have a [`DSAParams`{.codeph}
    implementation](howtoimplaprovider.html#GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9__DSAPARAMSIMPLEMENTATION-7140B38E).
-   The `getAlgorithm`{.codeph}, `getEncoded`{.codeph}, and
    `getFormat`{.codeph} methods from the
    [`Interface Key`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Key.html)
    interface, since `DSAPrivateKey`{.codeph} extends
    `java.security.PrivateKey`{.codeph}, and `PrivateKey`{.codeph}
    extends `Key`{.codeph}.

    Similarly, for public DSA keys, you need to supply a class that
    implements:

    -   The `getY`{.codeph} method from the
        [`Interface DSAPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAPublicKey.html)
        interface.
    -   The `getParams`{.codeph} method from the
        [`Interface DSAKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/DSAKey.html)
        interface, since `DSAPublicKey`{.codeph} extends DSAKey.

        <div class="infoboxnote" id="GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9__GUID-9A51D01D-705B-4488-976E-73983D4591CF">
        Note:

        The `getParams`{.codeph} method returns a `DSAParams`{.codeph}
        object, so you must also have a [DSAParams
        Implementation](howtoimplaprovider.html#GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9__DSAPARAMSIMPLEMENTATION-7140B38E).

        </div>
    -   The `getAlgorithm`{.codeph}, `getEncoded`{.codeph}, and
        `getFormat`{.codeph} methods from the
        [`Interface Key`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Key.html),
        since `DSAPublicKey`{.codeph} extends
        `java.security.PublicKey`{.codeph}, and `PublicKey`{.codeph}
        extends `Key`{.codeph}.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-353BF021-CABC-4CB4-A019-927D423B4627}

### RSA Interfaces and their Required Implementations {#JSSEC-GUID-353BF021-CABC-4CB4-A019-927D423B4627 .sect3}

<div>
The Java Security API contains the interfaces (in the
`java.security.interfaces`{.codeph} package) for the convenience of
programmers implementing RSA services.

<div class="section">
-   [`Interface RSAPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPrivateKey.html)

-   [`Interface RSAPrivateCrtKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPrivateCrtKey.html)

-   [`Interface RSAPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPublicKey.html)

The following sections discuss requirements for implementations of these
interfaces.

</div>
<!-- class="section" -->

<div class="section">
RSAPrivateKey, RSAPrivateCrtKey, and RSAPublicKey Implementations

If you implement an RSA key pair generator or key factory, you need to
create classes implementing the
[`Interface RSAPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPublicKey.html)
(and/or
[`Interface RSAPrivateCrtKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPrivateCrtKey.html))
and
[`Interface RSAPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPublicKey.html)
interfaces. (`RSAPrivateCrtKey`{.codeph} is the interface to an RSA
private key, using the <span class="variable">Chinese Remainder
Theorem</span> (CRT) representation.)

If you implement an RSA key pair generator, your
`generateKeyPair`{.codeph} method (in your
`KeyPairGeneratorSpi`{.codeph} subclass) will return instances of your
implementations of those interfaces.

If you implement an RSA key factory, your
`engineGeneratePrivate`{.codeph} method (in your
`KeyFactorySpi`{.codeph} subclass) will return an instance of your
`RSAPrivateKey`{.codeph} (or `RSAPrivateCrtKey`{.codeph})
implementation, and your `engineGeneratePublic`{.codeph} method will
return an instance of your `RSAPublicKey`{.codeph} implementation.

Also, your `engineGetKeySpec`{.codeph} and `engineTranslateKey`{.codeph}
methods will expect the passed-in key to be an instance of an
`RSAPrivateKey`{.codeph}, `RSAPrivateCrtKey`{.codeph}, or
`RSAPublicKey`{.codeph} implementation.

If you implement an RSA signature algorithm, your
`engineInitSign`{.codeph} method (in your `SignatureSpi`{.codeph}
subclass) will expect to be passed either an `RSAPrivateKey`{.codeph} or
an `RSAPrivateCrtKey`{.codeph}, and your `engineInitVerify`{.codeph}
method will expect to be passed an `RSAPublicKey`{.codeph}.

Please note: The `RSAPublicKey`{.codeph}, `RSAPrivateKey`{.codeph}, and
`RSAPrivateCrtKey`{.codeph} interfaces define a very generic,
provider-independent interface to RSA public and private keys. The
`engineGetKeySpec`{.codeph} and `engineTranslateKey`{.codeph} methods
(in your `KeyFactorySpi`{.codeph} subclass) could additionally check if
the passed-in key is actually an instance of their provider\'s own
implementation of `RSAPrivateKey`{.codeph}, `RSAPrivateCrtKey`{.codeph},
or `RSAPublicKey`{.codeph}, e.g., to take advantage of provider-specific
implementation details. The same is true for the RSA signature algorithm
`engineInitSign`{.codeph} and `engineInitVerify`{.codeph} methods (in
your `SignatureSpi`{.codeph} subclass).

To see what methods need to be implemented by classes that implement the
`RSAPublicKey`{.codeph}, `RSAPrivateKey`{.codeph}, and
`RSAPrivateCrtKey`{.codeph} interfaces, first note the following
interface signatures:

In the `java.security.interfaces`{.codeph} package:

``` {.codeblock dir="ltr"}
    public interface RSAPrivateKey extends java.security.PrivateKey

    public interface RSAPrivateCrtKey extends RSAPrivateKey

    public interface RSAPublicKey extends java.security.PublicKey
```

In the `java.security`{.codeph} package:

``` {.codeblock dir="ltr"}
    public interface PrivateKey extends Key

    public interface PublicKey extends Key

    public interface Key extends java.io.Serializable
```

In order to implement the `RSAPrivateKey`{.codeph},
`RSAPrivateCrtKey`{.codeph}, and `RSAPublicKey`{.codeph} interfaces, you
must implement the methods they define as well as those defined by
interfaces they extend, directly or indirectly.

Thus, for RSA private keys, you need to supply a class that implements:

-   The `getModulus`{.codeph} and `getPrivateExponent`{.codeph} methods
    from the
    [`Interface RSAPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPrivateKey.html)
    interface.
-   The `getAlgorithm`{.codeph}, `getEncoded`{.codeph}, and
    `getFormat`{.codeph} methods from the
    [`Interface Key`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Key.html)
    interface, since `RSAPrivateKey`{.codeph} extends
    `java.security.PrivateKey`{.codeph}, and `PrivateKey`{.codeph}
    extends `Key`{.codeph}.

Similarly, for RSA private keys using the <span class="variable">Chinese
Remainder Theorem</span> (CRT) representation, you need to supply a
class that implements:

-   All the methods listed above for RSA private keys, since
    `RSAPrivateCrtKey`{.codeph} extends
    `java.security.interfaces.RSAPrivateKey`{.codeph}.
-   The `getPublicExponent`{.codeph}, `getPrimeP`{.codeph},
    `getPrimeQ`{.codeph}, `getPrimeExponentP`{.codeph},
    `getPrimeExponentQ`{.codeph}, and `getCrtCoefficient`{.codeph}
    methods from the
    [`Interface RSAPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPrivateKey.html)
    interface.

For public RSA keys, you need to supply a class that implements:

-   The `getModulus`{.codeph} and `getPublicExponent`{.codeph} methods
    from the
    [`Interface RSAPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/interfaces/RSAPublicKey.html)
    interface.
-   The `getAlgorithm`{.codeph}, `getEncoded`{.codeph}, and
    `getFormat`{.codeph} methods from the
    [`Interface Key`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Key.html)
    interface, since `RSAPublicKey`{.codeph} extends
    `java.security.PublicKey`{.codeph}, and `PublicKey`{.codeph} extends
    `Key`{.codeph}.

JCA contains a number of `AlgorithmParameterSpec`{.codeph}
implementations for the most frequently used cipher and key agreement
algorithm parameters. If you are operating on algorithm parameters that
should be for a different type of algorithm not provided by JCA, you
will need to supply your own `AlgorithmParameterSpec`{.codeph}
implementation appropriate for that type of algorithm.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-E63F9312-ED15-41D5-8F62-93C6137D5F06}

### Diffie-Hellman Interfaces and their Required Implementations {#JSSEC-GUID-E63F9312-ED15-41D5-8F62-93C6137D5F06 .sect3}

<div>
JCA contains interfaces (in the `javax.crypto.interfaces`{.codeph}
package) for the convenience of programmers implementing Diffie-Hellman
services.

<div class="section">
-   [`Interface DHPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHPublicKey.html)

-   [`Interface DHKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHKey.html)

-   [`Interface DHPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHPrivateKey.html)

The following sections discuss requirements for implementations of these
interfaces.

</div>
<!-- class="section" -->

<div class="section">
DHPrivateKey and DHPublicKey Implementations

If you implement a Diffie-Hellman key pair generator or key factory, you
need to create classes implementing the
[`Interface DHPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHPrivateKey.html)
and
[`Interface DHPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHPublicKey.html)
interfaces.

If you implement a Diffie-Hellman key pair generator, your
`generateKeyPair`{.codeph} method (in your
`KeyPairGeneratorSpi`{.codeph} subclass) will return instances of your
implementations of those interfaces.

If you implement a Diffie-Hellman key factory, your
`engineGeneratePrivate`{.codeph} method (in your
`KeyFactorySpi`{.codeph} subclass) will return an instance of your
`DHPrivateKey`{.codeph} implementation, and your
`engineGeneratePublic`{.codeph} method will return an instance of your
`DHPublicKey`{.codeph} implementation.

Also, your `engineGetKeySpec`{.codeph} and `engineTranslateKey`{.codeph}
methods will expect the passed-in key to be an instance of a
`DHPrivateKey`{.codeph} or `DHPublicKey`{.codeph} implementation. The
`getParams`{.codeph} method provided by the interface implementations is
useful for obtaining and extracting the parameters from the keys. You
can then use the parameters, for example, as parameters to the
`DHParameterSpec`{.codeph} constructor called to create a parameter
specification from parameter values used to initialize a
`KeyPairGenerator`{.codeph} object for Diffie-Hellman.

If you implement the Diffie-Hellman key agreement algorithm, your
`engineInit`{.codeph} method (in your `KeyAgreementSpi`{.codeph}
subclass) will expect to be passed a `DHPrivateKey`{.codeph} and your
`engineDoPhase`{.codeph} method will expect to be passed a
`DHPublicKey`{.codeph}.

<div class="p">
<div class="infoboxnote" id="GUID-E63F9312-ED15-41D5-8F62-93C6137D5F06__GUID-53C9A9A7-1921-4ABC-A1D6-AB8E2714B75B">
Note:

The `DHPublicKey`{.codeph} and `DHPrivateKey`{.codeph} interfaces define
a very generic, provider-independent interface to Diffie-Hellman public
and private keys, respectively. The `engineGetKeySpec`{.codeph} and
`engineTranslateKey`{.codeph} methods (in your
<span class="apiname">KeyFactorySpi</span> subclass) could additionally
check if the passed-in key is actually an instance of their provider\'s
own implementation of `DHPrivateKey`{.codeph} or `DHPublicKey`{.codeph},
e.g., to take advantage of provider-specific implementation details. The
same is true for the Diffie-Hellman algorithm `engineInit`{.codeph} and
`engineDoPhase`{.codeph} methods (in your `KeyAgreementSpi`{.codeph}
subclass).

</div>
</div>
To see what methods need to be implemented by classes that implement the
`DHPublicKey`{.codeph} and `DHPrivateKey`{.codeph} interfaces, first
note the following interface signatures:

In the `javax.crypto.interfaces`{.codeph} package:

``` {.codeblock dir="ltr"}
    public interface DHPrivateKey extends DHKey, java.security.PrivateKey

    public interface DHPublicKey extends DHKey, java.security.PublicKey

    public interface DHKey 
```

In the `java.security`{.codeph} package:

``` {.codeblock dir="ltr"}
    public interface PrivateKey extends Key

    public interface PublicKey extends Key

    public interface Key extends java.io.Serializable 
```

To implement the `DHPrivateKey`{.codeph} and `DHPublicKey`{.codeph}
interfaces, you must implement the methods they define as well as those
defined by interfaces they extend, directly or indirectly.

Thus, for private keys, you need to supply a class that implements:

-   The `getX`{.codeph} method from the
    [`Interface DHPrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHPrivateKey.html)
    interface.
-   The `getParams`{.codeph} method from the
    [`Interface DHKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHKey.html)
    interface, since `DHPrivateKey`{.codeph} extends `DHKey`{.codeph}.
-   The `getAlgorithm`{.codeph}, `getEncoded`{.codeph}, and
    `getFormat`{.codeph} methods from the
    [`Interface Key`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Key.html)
    interface, since `DHPrivateKey`{.codeph} extends
    `java.security.PrivateKey`{.codeph}, and `PrivateKey`{.codeph}
    extends `Key`{.codeph}.

Similarly, for public Diffie-Hellman keys, you need to supply a class
that implements:

-   The `getY`{.codeph} method from the
    [`Interface DHPublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHPublicKey.html)
    interface.
-   The `getParams`{.codeph} method from the
    [`Interface DHKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/interfaces/DHKey.html)
    interface, since `DHPublicKey`{.codeph} extends `DHKey`{.codeph}.
-   The `getAlgorithm`{.codeph}, `getEncoded`{.codeph}, and
    `getFormat`{.codeph} methods from the
    [`Interface Key`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Key.html)
    interface, since `DHPublicKey`{.codeph} extends
    `java.security.PublicKey`{.codeph}, and `PublicKey`{.codeph} extends
    `Key`{.codeph}.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-6F87545B-E4EF-4EA7-8EAF-0FEA9DB2495E}

### Interfaces for Other Algorithm Types {#JSSEC-GUID-6F87545B-E4EF-4EA7-8EAF-0FEA9DB2495E .sect3}

<div>
As noted above, the Java Security API contains interfaces for the
convenience of programmers implementing services like DSA, RSA and ECC.
If there are services without API support, you need to define your own
APIs.

<div class="section">
If you are implementing a key pair generator for a different algorithm,
you should create an interface with one or more `initialize`{.codeph}
methods that clients can call when they want to provide
algorithm-specific parameters to be used rather than the default
parameters your implementation supplies. Your subclass of
`KeyPairGeneratorSpi`{.codeph} should implement this interface.

For algorithms without direct API support, it is recommended that you
create similar interfaces and provide implementation classes. Your
public key interface should extend the
[`Interface PublicKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/PublicKey.html)
interface. Similarly, your private key interface should extend the
[`Interface PrivateKey`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/PrivateKey.html)
interface.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9}

### Algorithm Parameter Specification Interfaces and Classes {#JSSEC-GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9 .sect3}

<div>
An algorithm parameter specification is a transparent representation of
the sets of parameters used with an algorithm.

<div class="section">
A <span class="variable">transparent</span> representation of parameters
means that you can access each value individually, through one of the
<span class="variable">get</span> methods defined in the corresponding
specification class (e.g., `DSAParameterSpec`{.codeph} defines
`getP`{.codeph}, `getQ`{.codeph}, and `getG`{.codeph} methods, to access
the p, q, and g parameters, respectively).

This is contrasted with an <span class="variable">opaque</span>
representation, as supplied by the `AlgorithmParameters`{.codeph} engine
class, in which you have no direct access to the key material values;
you can only get the name of the algorithm associated with the parameter
set (via `getAlgorithm`{.codeph}) and some kind of encoding for the
parameter set (via `getEncoded`{.codeph}).

If you supply an `AlgorithmParametersSpi`{.codeph},
`AlgorithmParameterGeneratorSpi`{.codeph}, or
`KeyPairGeneratorSpi`{.codeph} implementation, you must utilize the
`AlgorithmParameterSpec`{.codeph} interface, since each of those classes
contain methods that take an `AlgorithmParameterSpec`{.codeph}
parameter. Such methods need to determine which actual implementation of
that interface has been passed in, and act accordingly.

JCA contains a number of `AlgorithmParameterSpec`{.codeph}
implementations for the most frequently used signature, cipher and key
agreement algorithm parameters. If you are operating on algorithm
parameters that should be for a different type of algorithm not provided
by JCA, you will need to supply your own
`AlgorithmParameterSpec`{.codeph} implementation appropriate for that
type of algorithm.

Java defines the following algorithm parameter specification interfaces
and classes in the `java.security.spec`{.codeph} and
`javax.crypto.spec`{.codeph} packages:

</div>
<!-- class="section" -->

<div class="section">
The AlgorithmParameterSpec Interface

`AlgorithmParameterSpec`{.codeph} is an interface to a transparent
specification of cryptographic parameters.

This interface contains no methods or constants. Its only purpose is to
group (and provide type safety for) all parameter specifications. All
parameter specifications must implement this interface.

</div>
<!-- class="section" -->

<div class="section">
The DSAParameterSpec Class

This class (which implements the `AlgorithmParameterSpec`{.codeph} and
`DSAParams`{.codeph} interfaces) specifies the set of parameters used
with the DSA algorithm. It has the following methods:

``` {.codeblock dir="ltr"}
    public BigInteger getP()

    public BigInteger getQ()

    public BigInteger getG()
```

These methods return the DSA algorithm parameters: the prime
`p`{.codeph}, the sub-prime `q`{.codeph}, and the base `g`{.codeph}.

Many types of DSA services will find this class useful - for example, it
is utilized by the DSA signature, key pair generator, algorithm
parameter generator, and algorithm parameters classes implemented by the
<span class="variable">Sun</span> provider. As a specific example, an
algorithm parameters implementation must include an implementation for
the `getParameterSpec`{.codeph} method, which returns an
`AlgorithmParameterSpec`{.codeph}. The DSA algorithm parameters
implementation supplied by <span class="variable">Sun</span> returns an
instance of the `DSAParameterSpec`{.codeph} class.

</div>
<!-- class="section" -->

<div class="section">
The IvParameterSpec Class

This class (which implements the `AlgorithmParameterSpec`{.codeph}
interface) specifies the initialization vector (IV) used with a cipher
in feedback mode.

<div class="tblformal" id="GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9__GUID-560C045E-D56F-441E-B87B-566DF016C49E">
Table 3-3 Method in `IvParameterSpec`{.codeph}

  Method                      Description
  --------------------------- -----------------------------------------
  `byte[] getIV()`{.codeph}   Returns the initialization vector (IV).

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The OAEPParameterSpec Class

This class specifies the set of parameters used with OAEP Padding, as
defined in the PKCS \#1 standard.

<div class="tblformal" id="GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9__GUID-651DADDC-41F1-4D6F-BB06-AD0FF59E73B7">
Table 3-4 Methods in `OAEPParameterSpec`{.codeph}

  Method                                                 Description
  ------------------------------------------------------ ----------------------------------------------------------
  `String getDigestAlgorithm()`{.codeph}                 Returns the message digest algorithm name.
  `String getMGFAlgorithm()`{.codeph}                    Returns the mask generation function algorithm name.
  `AlgorithmParameterSpec getMGFParameters()`{.codeph}   Returns the parameters for the mask generation function.
  `PSource getPSource()`{.codeph}                        Returns the source of encoding input P.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The PBEParameterSpec Class

This class (which implements the `AlgorithmParameterSpec`{.codeph}
interface) specifies the set of parameters used with a password-based
encryption (PBE) algorithm.

<div class="tblformal" id="GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9__GUID-C45AE15E-8842-4E64-93AA-5CA8BF26BA57">
Table 3-5 Methods in `PBEParameterSpec`{.codeph}

  Method                               Description
  ------------------------------------ ------------------------------
  `int getIterationCount()`{.codeph}   Returns the iteration count.
  `byte[] getSalt()`{.codeph}          Returns the salt.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The RC2ParameterSpec Class

This class (which implements the `AlgorithmParameterSpec`{.codeph}
interface) specifies the set of parameters used with the RC2 algorithm.

<div class="tblformal" id="GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9__GUID-2694D9E7-97F1-4FF7-ADA4-2CA01AD507BD">
Table 3-6 Methods in `RC2ParameterSpec`{.codeph}

  Method                                  Description
  --------------------------------------- ----------------------------------------------------------------------
  `boolean equals(Object obj)`{.codeph}   Tests for equality between the specified object and this object.
  `int getEffectiveKeyBits()`{.codeph}    Returns the effective key size in bits.
  `byte[] getIV()`{.codeph}               Returns the IV or null if this parameter set does not contain an IV.
  `int hashCode()`{.codeph}               Calculates a hash code value for the object.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The RC5ParameterSpec Class

This class (which implements the `AlgorithmParameterSpec`{.codeph}
interface) specifies the set of parameters used with the RC5 algorithm.

<div class="tblformal" id="GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9__GUID-EA4BD83F-60B2-4A21-AAAE-249AD07DF7C5">
Table 3-7 Methods in `RC5ParameterSpec`{.codeph}

  Method                                  Description
  --------------------------------------- ----------------------------------------------------------------------
  `boolean equals(Object obj)`{.codeph}   Tests for equality between the specified object and this object.
  `byte[] getIV()`{.codeph}               Returns the IV or null if this parameter set does not contain an IV.
  `int getRounds()`{.codeph}              Returns the number of rounds.
  `int getVersion()`{.codeph}             Returns the version.
  `int getWordSize()`{.codeph}            Returns the word size in bits.
  `int hashCode()`{.codeph}               Calculates a hash code value for the object.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The DHParameterSpec Class

This class (which implements the `AlgorithmParameterSpec`{.codeph}
interface) specifies the set of parameters used with the Diffie-Hellman
algorithm.

<div class="tblformal" id="GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9__GUID-AD371F63-DD89-44FE-8288-02BD1F92E3E0">
Table 3-8 Methods in DHParameterSpec

  Method                         Description
  ------------------------------ ---------------------------------------------------------------------------------
  `BigInteger getG()`{.codeph}   Returns the base generator `g`{.codeph}.
  `int getL()`{.codeph}          Returns the size in bits, `l`{.codeph}, of the random exponent (private value).
  `BigInteger getP()`{.codeph}   Returns the prime modulus `p`{.codeph}.

</div>
<!-- class="inftblhruleinformal" --> Many types of Diffie-Hellman
services will find this class useful; for example, it is used by the
Diffie-Hellman key agreement, key pair generator, algorithm parameter
generator, and algorithm parameters classes implemented by the
\"SunJCE\" provider. As a specific example, an algorithm parameters
implementation must include an implementation for the
`getParameterSpec`{.codeph} method, which returns an
`AlgorithmParameterSpec`{.codeph}. The Diffie-Hellman algorithm
parameters implementation supplied by \"SunJCE\" returns an instance of
the `DHParameterSpec`{.codeph} class.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6}

### Key Specification Interfaces and Classes Required by Key Factories {#JSSEC-GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6 .sect3}

<div>
A key factory provides bi-directional conversions between opaque keys
(of type `Key`{.codeph}) and key specifications. If you implement a key
factory, you thus need to understand and utilize key specifications. In
some cases, you also need to implement your own key specifications.

<div class="section">
Key specifications are transparent representations of the key material
that constitutes a key. If the key is stored on a hardware device, its
specification may contain information that helps identify the key on the
device.

A <span class="variable">transparent</span> representation of keys means
that you can access each key material value individually, through one of
the <span class="variable">get</span> methods defined in the
corresponding specification class. For example,
`java.security.spec.DSAPrivateKeySpec`{.codeph} defines `getX`{.codeph},
`getP`{.codeph}, `getQ`{.codeph}, and `getG`{.codeph} methods, to access
the private key `x`{.codeph}, and the DSA algorithm parameters used to
calculate the key: the prime `p`{.codeph}, the sub-prime `q`{.codeph},
and the base `g`{.codeph}.

This is contrasted with an <span class="variable">opaque</span>
representation, as defined by the Key interface, in which you have no
direct access to the parameter fields. In other words, an \"opaque\"
representation gives you limited access to the key - just the three
methods defined by the Key interface: `getAlgorithm`{.codeph},
`getFormat`{.codeph}, and `getEncoded`{.codeph}.

A key may be specified in an algorithm-specific way, or in an
algorithm-independent encoding format (such as ASN.1). For example, a
DSA private key may be specified by its components `x`{.codeph},
`p`{.codeph}, `q`{.codeph}, and `g`{.codeph} (see
[`DSAPrivateKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/DSAPrivateKeySpec.html)),
or it may be specified using its DER encoding (see
[`PKCS8EncodedKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/spec/PKCS8EncodedKeySpec.html)).

Java defines the following key specification interfaces and classes in
the `java.security.spec`{.codeph} and `javax.crypto.spec`{.codeph}
packages:

</div>
<!-- class="section" -->

<div class="section" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__THEKEYSPECINTERFACE-73DA08B1">
The `KeySpec`{.codeph} Interface

This interface contains no methods or constants. Its only purpose is to
group (and provide type safety for) all key specifications. All key
specifications must implement this interface.

Java supplies several classes implementing the
<span class="apiname">KeySpec</span> interface:

-   [<span class="apiname">DSAPrivateKeySpec</span>](https://docs.oracle.com/javase/10/docs/api/java/security/spec/DSAPrivateKeySpec.html)
-   [<span class="apiname">DSAPublicKeySpec</span>](https://docs.oracle.com/javase/10/docs/api/java/security/spec/DSAPublicKeySpec.html)
-   [<span class="apiname">RSAPrivateKeySpec</span>](https://docs.oracle.com/javase/10/docs/api/java/security/spec/RSAPrivateKeySpec.html)
-   [<span class="apiname">RSAPublicKeySpec</span>](https://docs.oracle.com/javase/10/docs/api/java/security/spec/RSAPublicKeySpec.html)
-   [<span class="apiname">EncodedKeySpec</span>](https://docs.oracle.com/javase/10/docs/api/java/security/spec/EncodedKeySpec.html)
-   [<span class="apiname">PKCS8EncodedKeySpec</span>](https://docs.oracle.com/javase/10/docs/api/java/security/spec/PKCS8EncodedKeySpec.html)
-   [<span class="apiname">X509EncodedKeySpec</span>](https://docs.oracle.com/javase/10/docs/api/java/security/spec/X509EncodedKeySpec.html)

If your provider uses key types (e.g., `Your_PublicKey_type`{.codeph}
and `Your_PrivateKey_type`{.codeph}) for which the JDK does not already
provide corresponding `KeySpec`{.codeph} classes, there are two possible
scenarios, one of which requires that you implement your own key
specifications:

1.  If your users will never have to access specific key material values
    of your key type, you will not have to provide any
    `KeySpec`{.codeph} classes for your key type.

    In this scenario, your users will always create
    `Your_PublicKey_type`{.codeph} and `Your_PrivateKey_type`{.codeph}
    keys through the appropriate `KeyPairGenerator`{.codeph} supplied by
    your provider for that key type. If they want to store the generated
    keys for later usage, they retrieve the keys\' encodings (using the
    `getEncoded`{.codeph} method of the `Key`{.codeph} interface). When
    they want to create an `Your_PublicKey_type`{.codeph} or
    `Your_PrivateKey_type`{.codeph} key from the encoding (e.g., in
    order to initialize a Signature object for signing or verification),
    they create an instance of `X509EncodedKeySpec`{.codeph} or
    `PKCS8EncodedKeySpec`{.codeph} from the encoding, and feed it to the
    appropriate `KeyFactory`{.codeph} supplied by your provider for that
    algorithm, whose `generatePublic`{.codeph} and
    `generatePrivate`{.codeph} methods will return the requested
    `PublicKey`{.codeph} (an instance of `Your_PublicKey_type`{.codeph})
    or `PrivateKey`{.codeph} (an instance of
    `Your_PrivateKey_type`{.codeph}) object, respectively.

2.  If you anticipate a need for users to access specific key material
    values of your key type, or to construct a key of your key type from
    key material and associated parameter values, rather than from its
    encoding (as in the above case), you have to specify new
    `KeySpec`{.codeph} classes (classes that implement the
    `KeySpec`{.codeph} interface) with the appropriate constructor
    methods and <span class="variable">get</span> methods for returning
    key material fields and associated parameter values for your key
    type. You will specify those classes in a similar manner as is done
    by the `DSAPrivateKeySpec`{.codeph} and `DSAPublicKeySpec`{.codeph}
    classes. You need to ship those classes along with your provider
    classes, for example, as part of your provider JAR file.

</div>
<!-- class="section" -->

<div class="section">
The DSAPrivateKeySpec Class

This class (which implements the `KeySpec`{.codeph} Interface) specifies
a DSA private key with its associated parameters. It has the following
methods:

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-1EE9B5E3-B8FD-4DCE-847E-9180552A0296">
Table 3-9 Methods in DSAPrivateKeySpec

  Method in DSAPrivateKeySpec           Description
  ------------------------------------- ----------------------------
  `public BigInteger getX()`{.codeph}   Returns the private key x.
  `public BigInteger getP()`{.codeph}   Returns the prime p.
  `public BigInteger getQ()`{.codeph}   Returns the sub-prime q.
  `public BigInteger getG()`{.codeph}   Returns the base g.

</div>
<!-- class="inftblhruleinformal" -->

These methods return the private key `x`{.codeph}, and the DSA algorithm
parameters used to calculate the key: the prime `p`{.codeph}, the
sub-prime `q`{.codeph}, and the base `g`{.codeph}.

</div>
<!-- class="section" -->

<div class="section">
The DSAPublicKeySpec Class

This class (which implements the `KeySpec`{.codeph} Interface) specifies
a DSA public key with its associated parameters. It has the following
methods:

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-5E1FD16D-0364-485E-A50F-AACEA77F5D68">
Table 3-10 Methods in DSAPublicKeySpec

  Method in DSAPublicKeySpec            Description
  ------------------------------------- ---------------------------
  `public BigInteger getY()`{.codeph}   returns the public key y.
  `public BigInteger getP()`{.codeph}   Returns the prime p.
  `public BigInteger getQ()`{.codeph}   Returns the sub-prime q.
  `public BigInteger getG()`{.codeph}   Returns the base g.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The RSAPrivateKeySpec Class

This class (which implements the `KeySpec`{.codeph} Interface) specifies
an RSA private key. It has the following methods:

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-F824E25B-B667-4E68-8327-FCAC9718815E">
Table 3-11 Methods in RSAPrivateKeySpec

  Method in RSAPrivateKeySpec                         Description
  --------------------------------------------------- -------------------------------
  `public BigInteger getModulus()`{.codeph}           Returns the modulus.
  `public BigInteger getPrivateExponent()`{.codeph}   Returns the private exponent.

</div>
<!-- class="inftblhruleinformal" -->

These methods return the RSA modulus `n`{.codeph} and private exponent
`d`{.codeph} values that constitute the RSA private key.

</div>
<!-- class="section" -->

<div class="section">
The RSAPrivateCrtKeySpec Class

This class (which extends the `RSAPrivateKeySpec`{.codeph} class)
specifies an RSA private key, as defined in the PKCS\#1 standard, using
the <span class="variable">Chinese Remainder Theorem</span> (CRT)
information values. It has the following methods (in addition to the
methods inherited from its superclass `RSAPrivateKeySpec`{.codeph} ):

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-BCAE5CFB-F7CA-4C49-B623-2F381316FC3F">
Table 3-12 Methods in RSAPrivateCrtKeySpec

  Method in RSAPrivateCrtKeySpec                     Description
  -------------------------------------------------- ------------------------------
  `public BigInteger getPublicExponent()`{.codeph}   Returns the public exponent.
  `public BigInteger getPrimeP()`{.codeph}           Returns the prime P.
  `public BigInteger getPrimeQ()`{.codeph}           Returns the prime Q.
  `public BigInteger getPrimeExponentP()`{.codeph}   Returns the primeExponentP.
  `public BigInteger getPrimeExponentQ()`{.codeph}   Returns the primeExponentQ.
  `public BigInteger getCrtCoefficient()`{.codeph}   Returns the crtCoefficient.

</div>
<!-- class="inftblhruleinformal" -->

These methods return the public exponent `e`{.codeph} and the CRT
information integers: the prime factor `p`{.codeph} of the modulus
`n`{.codeph}, the prime factor `q`{.codeph} of `n`{.codeph}, the
exponent `d mod (p-1)`{.codeph}, the exponent `d mod (q-1)`{.codeph},
and the Chinese Remainder Theorem coefficient
`(inverse of q) mod p`{.codeph}.

An RSA private key logically consists of only the modulus and the
private exponent. The presence of the CRT values is intended for
efficiency.

</div>
<!-- class="section" -->

<div class="section">
The RSAPublicKeySpec Class

This class (which implements the `KeySpec`{.codeph} Interface) specifies
an RSA public key. It has the following methods:

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-E171C644-B094-4DDC-B4EB-08E76AC4543D">
Table 3-13 Methods in RSAPublicKeySpec

  Method in RSAPublicKeySpec                         Description
  -------------------------------------------------- ------------------------------
  `public BigInteger getModulus()`{.codeph}          Returns the modulus.
  `public BigInteger getPublicExponent()`{.codeph}   Returns the public exponent.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The EncodedKeySpec Class

This abstract class (which implements the `KeySpec`{.codeph} Interface)
represents a public or private key in encoded format.

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-60FAE739-4095-4FC5-94C7-A9B65AC04C85">
Table 3-14 Methods in EncodedKeySpec

  Method in EncodedKeySpec                         Description
  ------------------------------------------------ ------------------------------------------
  `public abstract byte[] getEncoded()`{.codeph}   Returns the encoded key.
  `public abstract String getFormat()`{.codeph}    Returns the name of the encoding format.

</div>
<!-- class="inftblhruleinformal" -->

The JDK supplies two classes implementing the `EncodedKeySpec`{.codeph}
interface: `PKCS8EncodedKeySpec`{.codeph} and
`X509EncodedKeySpec`{.codeph}. If desired, you can supply your own
`EncodedKeySpec`{.codeph} implementations for those or other types of
key encodings.

</div>
<!-- class="section" -->

<div class="section">
The PKCS8EncodedKeySpec Class

This class, which is a subclass of `EncodedKeySpec`{.codeph}, represents
the DER encoding of a private key, according to the format specified in
the PKCS \#8 standard.

Its `getEncoded`{.codeph} method returns the key bytes, encoded
according to the PKCS \#8 standard. Its `getFormat`{.codeph} method
returns the string \"PKCS\#8\".

</div>
<!-- class="section" -->

<div class="section">
The X509EncodedKeySpec Class

This class, which is a subclass of `EncodedKeySpec`{.codeph}, represents
the DER encoding of a public or private key, according to the format
specified in the X.509 standard.

Its `getEncoded`{.codeph} method returns the key bytes, encoded
according to the X.509 standard. Its `getFormat`{.codeph} method returns
the string \"X.509\".`DHPrivateKeySpec`{.codeph},
`DHPublicKeySpec`{.codeph}, `DESKeySpec`{.codeph},
`DESedeKeySpec`{.codeph}, `PBEKeySpec`{.codeph}, and
`SecretKeySpec`{.codeph}.

</div>
<!-- class="section" -->

<div class="section">
The DHPrivateKeySpec Class

This class (which implements the `KeySpec`{.codeph} interface) specifies
a Diffie-Hellman private key with its associated parameters.

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-18467DAF-8EF1-42DA-B4D5-7CBB4EA96CD5">
Table 3-15 Methods in DHPrviateKeySpec

  Method in DHPrivateKeySpec     Description
  ------------------------------ ------------------------------------------
  `BigInteger getG()`{.codeph}   Returns the base generator `g`{.codeph}.
  `BigInteger getP()`{.codeph}   Returns the prime modulus `p`{.codeph}.
  `BigInteger getX()`{.codeph}   Returns the private value `x`{.codeph}.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The DHPublicKeySpec Class

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-EB5C5B01-8EEC-4D46-BE8F-248BFC0548A3">
Table 3-16 Methods in DHPublicKeySpec

  Method in DHPublicKeySpec      Description
  ------------------------------ ------------------------------------------
  `BigInteger getG()`{.codeph}   Returns the base generator `g`{.codeph}.
  `BigInteger getP()`{.codeph}   Returns the prime modulus `p`{.codeph}.
  `BigInteger getY()`{.codeph}   Returns the public value `y`{.codeph}.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The DESKeySpec Class

This class (which implements the `KeySpec`{.codeph} interface) specifies
a DES key.

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-6F7067FE-280E-4C76-B742-9611CF17DB3F">
Table 3-17 Methods in DESKeySpec

  Method in DESKeySpec                                                 Description
  -------------------------------------------------------------------- ------------------------------------------------------------
  `byte[] getKey()`{.codeph}                                           Returns the DES key bytes.
  `static boolean isParityAdjusted(byte[] key, int offset)`{.codeph}   Checks if the given DES key material is parity-adjusted.
  `static boolean isWeak(byte[] key, int offset)`{.codeph}             Checks if the given DES key material is weak or semi-weak.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The DESedeKeySpec Class

This class (which implements the `KeySpec`{.codeph} interface) specifies
a DES-EDE (Triple DES) key.

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-6760BDD0-C8AE-4EE6-ADAD-A66B108A0BBF">
Table 3-18 Methods in DESedeKeySpec

  Method in DESedeKeySpec                                              Description
  -------------------------------------------------------------------- -----------------------------------------------------
  `byte[] getKey()`{.codeph}                                           Returns the DES-EDE key.
  `static boolean isParityAdjusted(byte[] key, int offset)`{.codeph}   Checks if the given DES-EDE key is parity-adjusted.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The PBEKeySpec Class

This class implements the `KeySpec`{.codeph} interface. A user-chosen
password can be used with password-based encryption (PBE); the password
can be viewed as a type of raw key material. An encryption mechanism
that uses this class can derive a cryptographic key from the raw key
material.

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-4DCC8AC8-3BB2-4441-9127-CE623BED2997">
Table 3-19 Methods in PBEKeySpec

  Method in PBEKeySpec               Description
  ---------------------------------- -------------------------------------------------------------
  `void clearPassword`{.codeph}      Clears the internal copy of the password.
  `int getIterationCount`{.codeph}   Returns the iteration count or 0 if not specified.
  `int getKeyLength`{.codeph}        Returns the to-be-derived key length or 0 if not specified.
  `char[] getPassword`{.codeph}      Returns a copy of the password.
  `byte[] getSalt`{.codeph}          Returns a copy of the salt or null if not specified.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section">
The SecretKeySpec Class

This class implements the `KeySpec`{.codeph} interface. Since it also
implements the `SecretKey`{.codeph} interface, it can be used to
construct a `SecretKey`{.codeph} object in a provider-independent
fashion, i.e., without having to go through a provider-based
`SecretKeyFactory`{.codeph}.

<div class="tblformal" id="GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6__GUID-7DAE6B47-86D9-443B-8353-15A44F2D1A1C">
Table 3-20 Methods in SecretKeySpec

  Method in SecretKeySpec                  Description
  ---------------------------------------- --------------------------------------------------------------------
  `boolean equals (Object obj)`{.codeph}   Indicates whether some other object is \"equal to\" this one.
  `String getAlgorithm()`{.codeph}         Returns the name of the algorithm associated with this secret key.
  `byte[] getEncoded()`{.codeph}           Returns the key material of this secret key.
  `String getFormat()`{.codeph}            Returns the name of the encoding format for this secret key.
  `int hashCode()`{.codeph}                Calculates a hash code value for the object.

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-63A770A3-398A-41C4-B2C9-894D76567F5C}

### Secret-Key Generation {#JSSEC-GUID-63A770A3-398A-41C4-B2C9-894D76567F5C .sect3}

<div>
If you provide a secret-key generator (subclass of
`javax.crypto.KeyGeneratorSpi`{.codeph}) for a particular secret-key
algorithm, you may return the generated secret-key object.

<div class="section">
The generated secret-key object (which must be an instance of
`javax.crypto.SecretKey`{.codeph}, see
[engineGenerateKey](https://docs.oracle.com/javase/10/docs/api/javax/crypto/KeyGeneratorSpi.html#engineGenerateKey--))
can be returned in one of the following ways:

-   You implement a class whose instances represent secret-keys of the
    algorithm associated with your key generator. Your key generator
    implementation returns instances of that class. This approach is
    useful if the keys generated by your key generator have
    provider-specific properties.
-   Your key generator returns an instance of
    [`SecretKeySpec`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/crypto/spec/SecretKeySpec.html),
    which already implements the `javax.crypto.SecretKey`{.codeph}
    interface. You pass the (raw) key bytes and the name of the
    secret-key algorithm associated with your key generator to the
    `SecretKeySpec`{.codeph} constructor. This approach is useful if the
    underlying (raw) key bytes can be represented as a byte array and
    have no key-parameters associated with them.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-5A41A05A-B8F0-4E24-A61B-347721809A8B}

### Adding New Object Identifiers {#JSSEC-GUID-5A41A05A-B8F0-4E24-A61B-347721809A8B .sect3}

<div>
The following information applies to providers who supply an algorithm
that is not listed as one of the standard algorithms in [Java Security
Standard Algorithm Names
Specification](https://docs.oracle.com/javase/10/docs/specs/security/standard-names.html).

<div class="section">
Mapping from OID to Name

Sometimes the JCA needs to instantiate a cryptographic algorithm
implementation from an algorithm identifier (for example, as encoded in
a certificate), which by definition includes the object identifier (OID)
of the algorithm. For example, in order to verify the signature on an
X.509 certificate, the JCA determines the signature algorithm from the
signature algorithm identifier that is encoded in the certificate,
instantiates a Signature object for that algorithm, and initializes the
Signature object for verification.

For the JCA to find your algorithm, you must provide the object
identifier of your algorithm as an alias entry for your algorithm in the
provider master file.

``` {.codeblock dir="ltr"}
    put("Alg.Alias.<engine_type>.1.2.3.4.5.6.7.8",
        "<algorithm_alias_name>");
```

Note that if your algorithm is known under more than one object
identifier, you need to create an alias entry for each object identifier
under which it is known.

An example of where the JCA needs to perform this type of mapping is
when your algorithm (\"`Foo`{.codeph}\") is a signature algorithm and
users run the `keytool`{.codeph} command and specify your (signature)
algorithm alias.

``` {.codeblock dir="ltr"}
    % keytool -genkeypair -sigalg 1.2.3.4.5.6.7.8
```

In this case, your provider master file should contain the following
entries:

``` {.codeblock dir="ltr"}
    put("Signature.Foo", "com.xyz.MyFooSignatureImpl");
    put("Alg.Alias.Signature.1.2.3.4.5.6.7.8", "Foo");
```

Other examples of where this type of mapping is performed are (1) when
your algorithm is a keytype algorithm and your program parses a
certificate (using the X.509 implementation of the SUN provider) and
extracts the public key from the certificate in order to initialize a
Signature object for verification, and (2) when `keytool`{.codeph} users
try to access a private key of your keytype (for example, to perform a
digital signature) after having generated the corresponding keypair. In
these cases, your provider master file should contain the following
entries:

``` {.codeblock dir="ltr"}
    put("KeyFactory.Foo", "com.xyz.MyFooKeyFactoryImpl");
    put("Alg.Alias.KeyFactory.1.2.3.4.5.6.7.8", "Foo");
```

</div>
<!-- class="section" -->

<div class="section">
Mapping from Name to OID

If the JCA needs to perform the inverse mapping (that is, from your
algorithm name to its associated OID), you need to provide an alias
entry of the following form for one of the OIDs under which your
algorithm should be known:

``` {.codeblock dir="ltr"}
    put("Alg.Alias.Signature.OID.1.2.3.4.5.6.7.8", "MySigAlg");
```

If your algorithm is known under more than one object identifier, prefix
the preferred one with \"OID.\"

An example of where the JCA needs to perform this kind of mapping is
when users run `keytool`{.codeph} in any mode that takes a
`-sigalg`{.codeph} option. For example, when the `-genkeypair`{.codeph}
and `-certreq`{.codeph} commands are invoked, the user can specify your
(signature) algorithm with the `-sigalg`{.codeph} option.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-ECCC1170-B552-4CF9-BD00-64A70DEC2AC6}

### Ensuring Exportability {#JSSEC-GUID-ECCC1170-B552-4CF9-BD00-64A70DEC2AC6 .sect3}

<div>
A key feature of JCA is the exportability of the JCA framework and of
the provider cryptography implementations if certain conditions are met.

By default, an application can use cryptographic algorithms of any
strength. However, due to import regulations in some countries, you may
have to limit those algorithms\' strength. You do this with jurisdiction
policy files; see [Cryptographic Strength
Configuration](java-cryptography-architecture-jca-reference-guide.html#GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1).
The JCA framework will enforce the restrictions specified in the
installed jurisdiction policy files.

As noted elsewhere, you can write just one version of your provider
software, implementing cryptography of maximum strength. It is up to
JCA, not your provider, to enforce any jurisdiction policy file-mandated
restrictions regarding the cryptographic algorithms and maximum
cryptographic strengths available to applets/applications in different
locations.

The conditions that must be met by your provider in order to enable it
to be plugged into JCA are the following:

-   The provider code should be written in such a way that provider
    classes become unusable if instantiated by an application directly,
    bypassing JCA. See [Step 1: Write your Service Implementation
    Code](howtoimplaprovider.html#GUID-1D2FDA77-743C-47CB-9CCB-2585FEC0607A "When instantiating a provider's implementation (class) of a Cipher, KeyAgreement, KeyGenerator, MAC, or SecretKey factory, the framework will determine the provider's codebase (JAR file) and verify its signature. In this way, JCA authenticates the provider and ensures that only providers signed by a trusted entity can be plugged into the JCA. Thus, one requirement for encryption providers is that they must be signed, as described in later steps.")
    in [Steps to Implement and Integrate a
    Provider](howtoimplaprovider.html#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:").
-   The provider package must be signed by an entity trusted by the JCA
    framework. (See [Step 7.1: Get a Code-Signing
    Certificate](howtoimplaprovider.html#GUID-434AACF7-0D2C-494A-B32A-508A6B605F62 "The next step is to request a code-signing certificate so that you can use it to sign your provider prior to testing. The certificate will be good for both testing and production. It will be valid for 5 years.")
    through [Step 7.2: Sign Your
    Provider](howtoimplaprovider.html#GUID-CF5F0E7D-BA0E-494C-8A5A-B228FF839AEF).)
    U.S. vendors whose providers may be exported outside the U.S. first
    need to apply for U.S. government export approval. (See [Step 11:
    Apply for U.S. Government Export Approval If
    Required](howtoimplaprovider.html#GUID-A62916EE-BE09-4229-9D05-3D6AF303CA4E "All U.S. vendors whose providers may be exported outside the U.S. should apply to the Bureau of Industry and Security in the U.S. Department of Commerce for export approval.").)

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137}

Sample Code for MyProvider {#JSSEC-GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137 .sect2}
--------------------------

<div>
The following is the complete source code for an example provider,
MyProvider. It\'s a portable provider; you can specify it in a class or
module path. It consists of two modules:

-   `com.example.MyProvider`{.codeph}: Contains an example provider that
    demonstrate how to write a provider with the
    <span class="apiname">Provider.Service</span> mechanism. You must
    compile, package, and sign the provider, then specify it in your
    class or module path as described in [Steps to Implement and
    Integrate a
    Provider](howtoimplaprovider.html#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:").

-   `com.example.MyApp`{.codeph}: Contains a sample application that
    uses the MyProvider provider. It finds and loads this provider with
    the <span class="apiname">ServiceLoader</span> mechanism, and then
    registers it dynamically with the
    <span class="apiname">Security.addProvider()</span> method.

This example consists of the following files:

-   `src/com.example.MyProvider/module-info.java`{.codeph}
-   `src/com.example.MyProvider/com/example/MyProvider/MyProvider.java`{.codeph}
-   `src/com.example.MyProvider/com/example/MyProvider/MyCipher.java`{.codeph}
-   `src/com.example.MyProvider/META-INF/services/java.security.Provider`{.codeph}
-   `src/com.example.MyApp/module-info.java`{.codeph}
-   `src/com.example.MyApp/com/example/MyApp/MyApp.java`{.codeph}
-   `RunTest.sh`{.codeph}

<div class="section" id="GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137__MYPROVIDER_EXAMPLE_MYPROVIDER_MODULE-INFO.JAVA">
src/com.example.MyProvider/module-info.java

See [Step 4: Create a Module Declaration for Your
Provider](howtoimplaprovider.html#GUID-7C304A79-6D0B-438B-A02E-51648C909876 "This step is optional but recommended; it enables you to package your provider in a named module. A modular JDK can then locate your provider in the module path as opposed to the class path. The module system can more thoroughly check for dependencies in modules in the module path. Note that you can use named modules in a non-modular JDK; the module declaration will be ignored. Also, you can still package your providers in unnamed or automatic modules.")
for information about the module declaration, which is specified in
<span class="apiname">module-info.java</span>.

``` {.oac_no_warn dir="ltr"}
module com.example.MyProvider {
    provides java.security.Provider with com.example.MyProvider.MyProvider;
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137__MYPROVIDER_EXAMPLE_MYPROVIDER.JAVA">
src/com.example.MyProvider/com/example/MyProvider/MyProvider.java

</div>
<!-- class="section" -->

The <span class="apiname">MyProvider</span> class is an example of a
provider that uses the <span class="apiname">Provider.Service</span>
class. See [Step 3.2: Create a Provider That Uses
Provider.Service](howtoimplaprovider.html#GUID-CB446B7A-CEA2-4F4A-A4AF-4D492CB58733).

``` {.oac_no_warn dir="ltr"}
package com.example.MyProvider;

import java.security.*;
import java.util.*;

/**
 * Test JCE provider.
 *
 * Registers services using Provider.Service and overrides newInstance().
 */
public final class MyProvider extends Provider {

    public MyProvider() {
        super("MyProvider", "1.0", "My JCE provider");

        final Provider p = this;

        AccessController.doPrivileged((PrivilegedAction<Void>) () -> {
            putService(new ProviderService(p, "Cipher",
                    "MyCipher", "com.example.MyProvider.MyCipher"));
            return null;
        });
    }

    private static final class ProviderService extends Provider.Service {

        ProviderService(Provider p, String type, String algo, String cn) {
            super(p, type, algo, cn, null, null);
        }

        ProviderService(Provider p, String type, String algo, String cn,
                String[] aliases, HashMap<String, String> attrs) {
            super(p, type, algo, cn,
                    (aliases == null ? null : Arrays.asList(aliases)), attrs);
        }

        @Override
        public Object newInstance(Object ctrParamObj)
                throws NoSuchAlgorithmException {

            String type = getType();
            if (ctrParamObj != null) {
                throw new InvalidParameterException(
                        "constructorParameter not used with " + type
                        + " engines");
            }
            String algo = getAlgorithm();
            try {
                if (type.equals("Cipher")) {
                    if (algo.equals("MyCipher")) {
                        return new MyCipher();
                    }
                }
            } catch (Exception ex) {
                throw new NoSuchAlgorithmException(
                        "Error constructing " + type + " for "
                        + algo + " using SunMSCAPI", ex);
            }
            throw new ProviderException("No impl for " + algo
                    + " " + type);
        }
    }

    @Override
    public String toString() {
        return "MyProvider [getName()=" + getName()
                + ", getVersionStr()=" + getVersionStr() + ", getInfo()="
                + getInfo() + "]";
    }
}
```

<div class="section" id="GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137__MYPROVIDER_EXAMPLE_MYCIPHER.JAVA">
src/com.example.MyProvider/com/example/MyProvider/MyCipher.java

The <span class="apiname">MyCipher</span> class extends the
<span class="apiname">CipherSPI</span>, which is a Server Provider
Interface (SPI). Each cryptographic service that a provider implements
has a subclass of the appropriate SPI. See [Step 1: Write your Service
Implementation
Code](howtoimplaprovider.html#GUID-1D2FDA77-743C-47CB-9CCB-2585FEC0607A "When instantiating a provider's implementation (class) of a Cipher, KeyAgreement, KeyGenerator, MAC, or SecretKey factory, the framework will determine the provider's codebase (JAR file) and verify its signature. In this way, JCA authenticates the provider and ensures that only providers signed by a trusted entity can be plugged into the JCA. Thus, one requirement for encryption providers is that they must be signed, as described in later steps.").

<div class="infoboxnote" id="GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137__GUID-53A626BF-DDDB-4135-98C4-B94A602BBBEB">
Note:

This code is only a stub provider that demonstrates how to write a
provider; it\'s missing the actual cryptographic algorithm
implementation. The `MyCipher`{.codeph} class would contain an actual
cryptographic algorithm implementation if MyProvider were a real
security provider.

</div>
``` {.oac_no_warn dir="ltr"}
package com.example.MyProvider;

import java.security.*;
import java.security.spec.*;
import javax.crypto.*;

/**
 * Implementation represents a test Cipher.
 *
 * All are stubs.
 */
public class MyCipher extends CipherSpi {

    @Override
    protected byte[] engineDoFinal(byte[] input, int inputOffset, int inputLen)
            throws IllegalBlockSizeException, BadPaddingException {
        return null;
    }

    @Override
    protected int engineDoFinal(byte[] input, int inputOffset, int inputLen,
            byte[] output, int outputOffset) throws ShortBufferException,
            IllegalBlockSizeException, BadPaddingException {
        return 0;
    }

    @Override
    protected int engineGetBlockSize() {
        return 0;
    }

    @Override
    protected byte[] engineGetIV() {
        return null;
    }

    @Override
    protected int engineGetOutputSize(int inputLen) {
        return 0;
    }

    @Override
    protected AlgorithmParameters engineGetParameters() {
        return null;
    }

    @Override
    protected void engineInit(int opmode, Key key, SecureRandom random)
            throws InvalidKeyException {
    }

    @Override
    protected void engineInit(int opmode, Key key,
            AlgorithmParameterSpec params, SecureRandom random)
            throws InvalidKeyException, InvalidAlgorithmParameterException {
    }

    @Override
    protected void engineInit(int opmode, Key key, AlgorithmParameters params,
            SecureRandom random) throws InvalidKeyException,
            InvalidAlgorithmParameterException {
    }

    @Override
    protected void engineSetMode(String mode) throws NoSuchAlgorithmException {
    }

    @Override
    protected void engineSetPadding(String padding)
            throws NoSuchPaddingException {
    }

    @Override
    protected int engineGetKeySize(Key key)
            throws InvalidKeyException {
        return 0;
    }

    @Override
    protected byte[] engineUpdate(byte[] input, int inputOffset, int inputLen) {
        return null;
    }

    @Override
    protected int engineUpdate(byte[] input, int inputOffset, int inputLen,
            byte[] output, int outputOffset) throws ShortBufferException {
        return 0;
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137__MYPROVIDER_EXAMPLE_JAVA.SECURITY.PROVIDER">
src/com.example.MyProvider/META-INF/services/java.security.Provider

The `java.security.Provider` file enables automatic or unnamed modules
to use the <span class="apiname">ServiceLoader</span> class to search
for your providers. See [Step 6: Place Your Provider in a JAR
File](howtoimplaprovider.html#GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F).

``` {.oac_no_warn dir="ltr"}
com.example.MyProvider.MyProvider
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137__MYAPP_MODULE-INFO">
src/com.example.MyApp/module-info.java

This file contains a <span class="apiname">uses</span> directive, which
specifies a service that the module requires. This directive helps the
module system locate providers and ensure that they run reliably. This
is the complement to the `provides`{.codeph} directive in the
`MyProvider`{.codeph} module definition.

``` {.oac_no_warn dir="ltr"}
module com.example.MyApp {
    uses java.security.Provider;
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137__MYPROVIDER_EXAMPLE_MYAPP.JAVA">
src/com.example.MyApp/com/example/MyApp/MyApp.java

``` {.oac_no_warn dir="ltr"}
package com.example.MyApp;

import java.util.*;
import java.security.*;
import javax.crypto.*;

/**
 * A simple JCE test client to access a simple test Provider/Cipher
 * implementation in a signed modular jar.
 */
public class MyApp {

    private static final String PROVIDER = "MyProvider";
    private static final String CIPHER = "MyCipher";

    public static void main(String[] args) throws Exception {

        /*
         * Registers MyProvider dynamically.
         *
         * Could do statically by editing the java.security file.
         * Use the first form if using ServiceLoader ("uses" or
         * META-INF/service), the second if using the traditional class
         * lookup method.  Both if provider could be deployed to either.
         *
         * security.provider.14=MyProvider
         * security.provider.15=com.example.MyProvider.MyProvider
         */
        ServiceLoader<Provider> sl =
            ServiceLoader.load(java.security.Provider.class);
        for (Provider p : sl) {
            if (p.getName().equals(PROVIDER)) {
                System.out.println("Registering the Provider");
                Security.addProvider(p);
            }
        }

        /*
         * Get a MyCipher from MyProvider and initialize it.
         */
        Cipher cipher = Cipher.getInstance(CIPHER, PROVIDER);
        cipher.init(Cipher.ENCRYPT_MODE, (Key) null);

        /*
         * What Provider did we get?
         */
        Provider p = cipher.getProvider();
        Class c = p.getClass();
        Module m = c.getModule();
        System.out.println(p.getName() + ": version "
            + p.getVersionStr() + "\n"
            + p.getInfo() + "\n    "
            + ((m.getName() == null) ? "<UNNAMED>" : m.getName())
            + "/" + c.getName());
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137__MYPROVIDER_EXAMPLE_RUNTEST.SH">
RunTest.sh

``` {.oac_no_warn dir="ltr"}
#!/bin/sh

#
# A simple example to show how a JCE provider could be developed in a
# modular JDK, for deployment as either Named/Unnamed modules.
#

#
# Edit as appropriate
#
JDK_DIR=d:/java/jdk9
KEYSTORE=YourKeyStore
STOREPASS=YourStorePass
SIGNER=YourAlias

echo "-----------"
echo "Clean/Init"
echo "-----------"
rm -rf mods jars
mkdir mods jars

echo "--------------------"
echo "Compiling MyProvider"
echo "--------------------"
${JDK_DIR}/bin/javac.exe \
    --module-source-path src \
    -d mods \
    $(find src/com.example.MyProvider -name '*.java' -print)

echo "------------------------------------"
echo "Packaging com.example.MyProvider.jar"
echo "------------------------------------"
${JDK_DIR}/bin/jar.exe --create \
    --file jars/com.example.MyProvider.jar \
    --verbose \
    --module-version=1.0 \
    -C mods/com.example.MyProvider . \
    -C src/com.example.MyProvider META-INF/services

echo "----------------------------------"
echo "Signing com.example.MyProvider.jar"
echo "----------------------------------"
${JDK_DIR}/bin/jarsigner.exe \
    -keystore ${KEYSTORE} \
    -storepass ${STOREPASS} \
    jars/com.example.MyProvider.jar ${SIGNER}

echo "---------------"
echo "Compiling MyApp"
echo "---------------"
${JDK_DIR}/bin/javac.exe \
    --module-source-path src \
    -d mods \
    $(find src/com.example.MyApp -name '*.java' -print)

echo "-------------------------------"
echo "Packaging com.example.MyApp.jar"
echo "-------------------------------"
${JDK_DIR}/bin/jar.exe --create \
    --file jars/com.example.MyApp.jar \
    --verbose \
    --module-version=1.0 \
    -C mods/com.example.MyApp .

echo "------------------------"
echo "Test1                   "
echo "Named Provider/Named App"
echo "------------------------"
${JDK_DIR}/bin/java.exe \
    --module-path 'jars' \
    -m com.example.MyApp/com.example.MyApp.MyApp

echo "--------------------------"
echo "Test2                     "
echo "Named Provider/Unnamed App"
echo "--------------------------"
${JDK_DIR}/bin/java.exe \
    --module-path 'jars/com.example.MyProvider.jar' \
    --class-path 'jars/com.example.MyApp.jar' \
    com.example.MyApp.MyApp

echo "--------------------------"
echo "Test3                     "
echo "Unnamed Provider/Named App"
echo "--------------------------"
${JDK_DIR}/bin/java.exe \
    --module-path 'jars/com.example.MyApp.jar' \
    --class-path 'jars/com.example.MyProvider.jar' \
    -m com.example.MyApp/com.example.MyApp.MyApp

echo "----------------------------"
echo "Test4                       "
echo "Unnamed Provider/Unnamed App"
echo "----------------------------"
${JDK_DIR}/bin/java.exe \
    --class-path \
        'jars/com.example.MyProvider.jar;jars/com.example.MyApp.jar' \
    com.example.MyApp.MyApp
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
| -------------------- | r | ---                  |
| --------------- ---- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ----------- --       | e | )\                   |
|                      | L |             <span cl |
|       [![Previous](. | o | ass="icon">Contents< |
| ./../dcommon/gifs/le | g | /span>](toc.htm)     |
| ftnav.gif)\          | o |   -- --------------- |
|                      | ] | -------------------- |
|   [![Next](../../dco | ( | -------------------- |
| mmon/gifs/rightnav.g | . | ---                  |
| if)\                 | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](j | . |                      |
| ava-cryptography-arc | . |                      |
| hitecture-jca-refere | / |                      |
| nce-guide.htm)   <sp | d |                      |
| an class="icon">Next | c |                      |
| </span>](oracle-prov | o |                      |
| iders.htm)           | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| -------------------- | / |                      |
| --------------- ---- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ----------- --       | s |                      |
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
