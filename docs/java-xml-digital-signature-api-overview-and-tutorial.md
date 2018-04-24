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

  ------------------------------------------------------------------------------------------ ------------------------------------------------------------------ --
                        [![Previous](../../dcommon/gifs/leftnav.gif)\                                    [![Next](../../dcommon/gifs/rightnav.gif)\             
   <span class="icon">Previous</span>](java-sasl-api-programming-and-deployment-guide1.htm)   <span class="icon">Next</span>](security-api-specification1.htm)  
  ------------------------------------------------------------------------------------------ ------------------------------------------------------------------ --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-DB46A001-6DBD-4571-BDBC-1BBC394BF61E}<!-- End Header -->

<span class="enumeration_chapter">12 </span>XML Digital Signature API Overview and Tutorial {#JSSEC-GUID-DB46A001-6DBD-4571-BDBC-1BBC394BF61E .sect1}
===========================================================================================

<div>
The Java XML Digital Signature API is a standard Java API for generating
and validating XML Signatures. This API was defined under the Java
Community Process as [JSR 105](http://www.jcp.org/en/jsr/detail?id=105).

XML Signatures can be applied to data of any type, XML or binary (see
[XML Signature Syntax and
Processing](http://www.w3.org/TR/xmldsig-core/)). The resulting
signature is represented in XML. An XML Signature can be used to secure
your data and provide data integrity, message authentication, and signer
authentication.

After providing a brief overview of XML Signatures and the XML Digital
Signature API, this document presents two examples that demonstrate how
to use the API to validate and generate an XML Signature. This document
assumes that you have a basic knowledge of cryptography and digital
signatures.

The API is designed to support all of the required or recommended
features of the W3C Recommendation for XML-Signature Syntax and
Processing. The API is extensible and pluggable and is based on the Java
Cryptography Service Provider Architecture; see [Java Cryptography
Architecture (JCA) Reference
Guide](java-cryptography-architecture-jca-reference-guide.htm#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.").
The API is designed for two types of developers:

-   Developers who want to use the XML Digital Signature API to generate
    and validate XML signatures
-   Developers who want to create a concrete implementation of the XML
    Digital Signature API and register it as a cryptographic service of
    a JCA provider (see [The Provider
    Class](java-cryptography-architecture-jca-reference-guide.htm#GUID-D8E30FE5-66B4-4F6A-88B7-280789E68307 "In order to be used, a cryptographic provider must first be installed, then registered either statically or dynamically. There are a variety of Sun providers shipped with this release (SUN, SunJCE, SunJSSE, SunRsaSign, etc.) that are already installed and registered. The following sections describe how to install and register additional providers.Each Provider class instance has a (currently case-sensitive) name, a version number, and a string description of the provider and its services.")).

</div>
<div class="sect2">
[]{#GUID-BBFA7B90-3EA2-49DE-964B-8A60D4134343}

Package Hierarchy {#JSSEC-GUID-BBFA7B90-3EA2-49DE-964B-8A60D4134343 .sect2}
-----------------

<div>
The following six packages, which are contained in the
[<span class="apiname">java.xml.crypto</span>](https://docs.oracle.com/javase/10/docs/api/java.xml.crypto-summary.html)
module, comprise the XML Digital Signature API:

-   <span class="apiname">javax.xml.crypto</span>
-   <span class="apiname">javax.xml.crypto.dsig</span>
-   <span class="apiname">javax.xml.crypto.dsig.keyinfo</span>
-   <span class="apiname">javax.xml.crypto.dsig.spec</span>
-   <span class="apiname">javax.xml.crypto.dom</span>
-   <span class="apiname">javax.xml.crypto.dsig.dom</span>

The
[<span class="apiname">javax.xml.crypto</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/package-summary.html)
package contains common classes that are used to perform XML
cryptographic operations, such as generating an XML signature or
encrypting XML data. Two notable classes in this package are the
[<span class="apiname">KeySelector</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/KeySelector.html)
class, which allows developers to supply implementations that locate and
optionally validate keys using the information contained in a
<span class="apiname">KeyInfo</span> object, and the
[<span class="apiname">URIDereferencer</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/URIDereferencer.html)
class, which allows developers to create and specify their own URI
dereferencing implementations.

The
[<span class="apiname">javax.xml.crypto.dsig</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/package-summary.html)
package includes interfaces that represent the core elements defined in
the W3C XML digital signature specification. Of primary significance is
the
[<span class="apiname">XMLSignature</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLSignature.html)
class, which allows you to sign and validate an XML digital signature.
Most of the XML signature structures or elements are represented by a
corresponding interface (except for the KeyInfo structures, which are
included in their own package and are discussed in the next paragraph).
These interfaces include:
[<span class="apiname">SignedInfo</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/SignedInfo.html),
[<span class="apiname">CanonicalizationMethod</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/CanonicalizationMethod.html),
[<span class="apiname">SignatureMethod</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/SignatureMethod.html),
[<span class="apiname">Reference</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/Reference.html),
[<span class="apiname">Transform</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/Transform.html),
[<span class="apiname">DigestMethod</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/DigestMethod.html),
[<span class="apiname">XMLObject</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLObject.html),
[<span class="apiname">Manifest</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/Manifest.html),
[<span class="apiname">SignatureProperty</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/SignatureProperty.html),
and
[<span class="apiname">SignatureProperties</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/SignatureProperties.html).
The
[<span class="apiname">XMLSignatureFactory</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLSignatureFactory.html)
class is an abstract factory that is used to create objects that
implement these interfaces.

The
[<span class="apiname">javax.xml.crypto.dsig.keyinfo</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/package-summary.html)
package contains interfaces that represent most of the
<span class="apiname">KeyInfo</span> structures defined in the W3C XML
digital signature recommendation, including
[<span class="apiname">KeyInfo</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyInfo.html),
[<span class="apiname">KeyName</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyName.html),
[<span class="apiname">KeyValue</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyValue.html),
[<span class="apiname">X509Data</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/X509Data.html),
[<span class="apiname">X509IssuerSerial</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/X509IssuerSerial.html),
[<span class="apiname">RetrievalMethod</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/RetrievalMethod.html),
and
[<span class="apiname">PGPData</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/PGPData.html).
The
[<span class="apiname">KeyInfoFactory</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyInfoFactory.html)
class is an abstract factory that is used to create objects that
implement these interfaces.

The
[<span class="apiname">javax.xml.crypto.dsig.spec</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/spec/package-summary.html)
package contains interfaces and classes representing input parameters
for the digest, signature, transform, or canonicalization algorithms
used in the processing of XML signatures.

Finally, the
[<span class="apiname">javax.xml.crypto.dom</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dom/package-summary.html)
and
[<span class="apiname">javax.xml.crypto.dsig.dom</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/dom/package-summary.html)
packages contains DOM-specific classes for the
[<span class="apiname">javax.xml.crypto</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/package-summary.html)
and
[<span class="apiname">javax.xml.crypto.dsig</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/package-summary.html)
packages, respectively. Only developers and users who are creating or
using a DOM-based
[<span class="apiname">XMLSignatureFactory</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLSignatureFactory.html)
or
[<span class="apiname">KeyInfoFactory</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyInfoFactory.html)
implementation will need to make direct use of these packages.

</div>
</div>
<div class="sect2">
[]{#GUID-A32C5AC5-08F9-4316-9D63-0CDEAC3A5405}

Service Providers {#JSSEC-GUID-A32C5AC5-08F9-4316-9D63-0CDEAC3A5405 .sect2}
-----------------

<div>
A Java XML Signature is a concrete implementation of the abstract
[<span class="apiname">XMLSignatureFactory</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/XMLSignatureFactory.html)
and
[<span class="apiname">KeyInfoFactory</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/keyinfo/KeyInfoFactory.html)
classes and is responsible for creating objects and algorithms that
parse, generate and validate XML Signatures and
<span class="apiname">KeyInfo</span> structures. A concrete
implementation of <span class="apiname">XMLSignatureFactory</span> must
provide support for each of the required algorithms as specified by the
W3C recommendation for XML Signatures. It can optionally support other
algorithms as defined by the W3C recommendation or other specifications.

The Java XML Digital Signature API leverages the JCA provider model for
registering and loading <span class="apiname">XMLSignatureFactory</span>
and <span class="apiname">KeyInfoFactory</span> implementations.

Each concrete <span class="apiname">XMLSignatureFactory</span> or
<span class="apiname">KeyInfoFactory</span> implementation supports a
specific XML mechanism type that identifies the XML processing mechanism
that an implementation uses internally to parse and generate XML
signature and <span class="apiname">KeyInfo</span> structures. This JSR
supports one standard type, DOM. The XML Digital Signature provider
implementation that is bundled with the JDK supports the DOM mechanism.

An XML Digital Signature API implementation should use underlying JCA
engine classes, such as
[<span class="apiname">java.security.Signature</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Signature.html)
and
[<span class="apiname">java.security.MessageDigest</span>](https://docs.oracle.com/javase/10/docs/api/java/security/MessageDigest.html),
to perform cryptographic operations.

In addition to the <span class="apiname">XMLSignatureFactory</span> and
<span class="apiname">KeyInfoFactory</span> classes, JSR 105 supports a
service provider interface for transform and canonicalization
algorithms. The
[<span class="apiname">TransformService</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/crypto/dsig/TransformService.html)
class allows you to develop and plug in an implementation of a specific
transform or canonicalization algorithm for a particular XML mechanism
type. The <span class="apiname">TransformService</span> class uses the
standard JCA provider model for registering and loading implementations.
Each JSR 105 implementation should use the
<span class="apiname">TransformService</span> class to find a provider
that supports transform and canonicalization algorithms in XML
Signatures that it is generating or validating.

</div>
</div>
<div class="sect2">
[]{#GUID-E11E6051-5F30-4DDA-A4EE-5F9C1AB1F7B8}

Introduction to XML Signatures {#JSSEC-GUID-E11E6051-5F30-4DDA-A4EE-5F9C1AB1F7B8 .sect2}
------------------------------

<div>
You can use an XML Signature to sign any arbitrary data, whether it is
XML or binary. The data is identified via URIs in one or more Reference
elements. XML Signatures are described in one or more of three forms:
detached, enveloping, or enveloped. A detached signature is over data
that is external, or outside of the signature element itself. Enveloping
signatures are signatures over data that is inside the signature
element, and an enveloped signature is a signature that is contained
inside the data that it is signing.

</div>
<div class="sect3">
[]{#GUID-E5A89234-A67A-4999-8E31-6D6C26B9BAAF}

### Example of an XML Signature {#JSSEC-GUID-E5A89234-A67A-4999-8E31-6D6C26B9BAAF .sect3}

<div>
The easiest way to describe the contents of an XML Signature is to show
an actual sample and describe each component in more detail. [Example
12-3](java-xml-digital-signature-api-overview-and-tutorial.htm#GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0__GUID-4DCD9F0B-02C7-4C00-AB66-096C7F262ACF)
is an enveloped XML Signature generated over the contents of an XML
document. The root element, `Envelop`{.codeph}, contains a
`Signature`{.codeph} element:

``` {.oac_no_warn dir="ltr"}
<Envelope xmlns="urn:envelope">
  <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
    <!-- ... -->
  </Signature>
</Envelope> 
```

This `Signature`{.codeph} element has been inserted inside the content
that it is signing, thereby making it an enveloped signature. The
required `SignedInfo`{.codeph} element contains the information that is
actually signed:

``` {.oac_no_warn dir="ltr"}
<Envelope xmlns="urn:envelope">
  <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
    <SignedInfo>
      <CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315#WithComments"/>
      <SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"/>
      <Reference URI="">
        <Transforms>
          <Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
        </Transforms>
        <DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"/>
        <DigestValue>/juoQ4bDxElf1M+KJauO20euW+QAvvPP0nDCruCQooM=</DigestValue>
      </Reference>
    </SignedInfo>
    <!-- ... -->
  </Signature>
</Envelope> 
```

The required `CanonicalizationMethod`{.codeph} element defines the
algorithm used to canonicalize the `SignedInfo`{.codeph} element before
it is signed or validated. Canonicalization is the process of converting
XML content to a canonical form, to take into account changes that can
invalidate a signature over that data. Canonicalization is necessary due
to the nature of XML and the way it is parsed by different processors
and intermediaries, which can change the data such that the signature is
no longer valid but the signed data is still logically equivalent.

The required `SignatureMethod`{.codeph} element defines the digital
signature algorithm used to generate the signature, in this case RSA
with SHA-256.

One or more `Reference`{.codeph} elements identify the data that is
digested. Each `Reference`{.codeph} element identifies the data via a
URI. In this example, the value of the URI is the empty String (\"\"),
which indicates the root of the document. The optional
`Transforms`{.codeph} element contains a list of one or more
`Transform`{.codeph} elements, each of which describes a transformation
algorithm used to transform the data before it is digested. In this
example, there is one Transform element for the enveloped transform
algorithm. The enveloped transform is required for enveloped signatures
so that the signature element itself is removed before calculating the
signature value. The required `DigestMethod`{.codeph} element defines
the algorithm used to digest the data, in this case SHA-256. Finally the
required `DigestValue`{.codeph} element contains the actual
base64-encoded digested value.

The required `SignatureValue`{.codeph} element contains the
base64-encoded signature value of the signature over the
`SignedInfo`{.codeph} element.

The optional `KeyInfo`{.codeph} element contains information about the
key that is needed to validate the signature:

``` {.oac_no_warn dir="ltr"}
    <KeyInfo>
      <KeyValue>
        <RSAKeyValue>
          <Modulus>
9hSmAKw/4TTw/1l1u1pYzdFm6lOjRB/5NfdGWl/fB8iAa/tiK0f1u/VWoK6SMtogYgSDKqQThbAu
9dy9rRnOWRGY2He1JtpOvGh0WCmIFUEs2P22HvEf+JGKVEpkoP4hv53ucT69T+7nKGK3/bjxgp+T
C7fbnVj651+jAHuDFlC8Txt1R8ZymfN5cUeHIH96dvNFrtai/uwZDbVMfhV9chL//+Vyhx4O5nHv
jfS+0So9Qi52YAbEyLu6+BLdu8wnMWapC88CfXsRwrpx8b6aCU0e6QSZyOvdgXWz3+9ifVTBDIxE
kjhL5OASx0qjvc+dPUOMvq7fJE05RRZLyb0YJw==
          </Modulus>
          <Exponent>AQAB</Exponent>
        </RSAKeyValue>
      </KeyValue>
    </KeyInfo>
```

This `KeyInfo`{.codeph} element contains a `KeyValue`{.codeph} element,
which in turn contains a `RSAKeyValue`{.codeph} element consisting of
the public key needed to validate the signature. `KeyInfo`{.codeph} can
contain various content such as X.509 certificates and PGP key
identifiers. See [The `KeyInfo`{.codeph}
Element](http://www.w3.org/TR/xmldsig-core/#sec-KeyInfo) in [XML
Signature Syntax and Processing](https://www.w3.org/TR/xmldsig-core/)
for more information on the different `KeyInfo`{.codeph} types.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-8618C294-3BFE-45C3-9A1E-C4629E337E68}

XML Signature Secure Validation Mode {#JSSEC-GUID-8618C294-3BFE-45C3-9A1E-C4629E337E68 .sect2}
------------------------------------

<div>
XML Signature secure validation mode can protect you from XML Signatures
that may contain potentially hostile constructs that can cause
denial-of-service or other types of security issues.

XML Signature secure validation mode is enabled by default when you run
your application with a security manager.

You can also enable XML Signature secure validation mode by setting the
`org.jcp.xml.dsig.secureValidation`{.codeph} property to
`TRUE`{.codeph}. You must set this property to `TRUE`{.codeph} before
validating an XML Signature.

To set this property in an application, call the
<span class="apiname">javax.xml.crypto.dsig.dom.DOMValidateContext.setProperty</span>
method:

``` {.oac_no_warn dir="ltr"}
    DOMValidateContext context = new DOMValidateContext(key, element);
    context.setProperty("org.jcp.xml.dsig.secureValidation", Boolean.TRUE);
```

When XML Signature secure validation mode is enabled, XML Signatures are
processed more securely. Limits are set on various XML Signature
constructs to avoid conditions such as denial-of-service attacks. By
default, it enforces the following restrictions:

-   Forbids the use of XSLT transforms
-   Restricts the number of `SignedInfo`{.codeph} or `Manifest`{.codeph}
    `Reference`{.codeph} elements to 30 or less
-   Restricts the number of `Reference`{.codeph} transforms to 5 or less
-   Forbids the use of MD5-related signatures or MAC algorithms
-   Ensures that `Reference`{.codeph} IDs are unique to help prevent
    signature wrapping attacks
-   Forbids `Reference`{.codeph} URIs of type `http`{.codeph},
    `https`{.codeph}, or `file`{.codeph}
-   Does not allow a `RetrievalMethod`{.codeph} element to reference
    another `RetrievalMethod`{.codeph} element
-   Forbids RSA or DSA keys less than 1024 bits

In addition, you can use the
`jdk.xml.dsig.secureValidationPolicy`{.codeph} Security Property to
control and fine-tune the restrictions listed previously or add
additional restrictions. See the definition of this Security Property in
the `java.security` file for more information.

</div>
</div>
<div class="sect2">
[]{#GUID-E7E9239F-C973-4D05-AC3F-53F714C259DB}

XML Digital Signature API Examples {#JSSEC-GUID-E7E9239F-C973-4D05-AC3F-53F714C259DB .sect2}
----------------------------------

<div>
The following sections describe two examples that show how to use the
XML Digital Signature API:

</div>
<div class="sect3">
[]{#GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0}

### Validate Example {#JSSEC-GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0 .sect3}

<div>
To compile and run the example, execute the following commands:

``` {.oac_no_warn dir="ltr"}
$ javac Validate.java 
$ java Validate signature.xml
```

The sample program will validate the signature in the file
`signature.xml` in the current working directory.

<div class="example" id="GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0__GUID-CCB8BC57-84D6-4EC2-A81A-A9760B4CD190">
Example 12-1 Validate.java

``` {.oac_no_warn dir="ltr"}
import javax.xml.crypto.*;
import javax.xml.crypto.dsig.*;
import javax.xml.crypto.dom.*;
import javax.xml.crypto.dsig.dom.DOMValidateContext;
import javax.xml.crypto.dsig.keyinfo.*;
import java.io.FileInputStream;
import java.security.*;
import java.util.Collections;
import java.util.Iterator;
import java.util.List;
import javax.xml.parsers.DocumentBuilderFactory;
import org.w3c.dom.Document;
import org.w3c.dom.NodeList;

/**
 * This is a simple example of validating an XML Signature using
 * the XML Signature API. It assumes the key needed to validate
 * the signature is contained in a KeyValue KeyInfo.
 */
public class Validate {

    //
    // Synopsis: java Validate [document]
    //
    //    where "document" is the name of a file containing the XML document
    //    to be validated.
    //
    public static void main(String[] args) throws Exception {

        // Instantiate the document to be validated
        DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
        dbf.setNamespaceAware(true);
        Document doc = null;
        try (FileInputStream fis = new FileInputStream(args[0])) {
            doc = dbf.newDocumentBuilder().parse(fis);
        }

        // Find Signature element
        NodeList nl =
            doc.getElementsByTagNameNS(XMLSignature.XMLNS, "Signature");
        if (nl.getLength() == 0) {
            throw new Exception("Cannot find Signature element");
        }

        // Create a DOM XMLSignatureFactory that will be used to unmarshal the
        // document containing the XMLSignature
        XMLSignatureFactory fac = XMLSignatureFactory.getInstance("DOM");

        // Create a DOMValidateContext and specify a KeyValue KeySelector
        // and document context
        DOMValidateContext valContext = new DOMValidateContext
            (new KeyValueKeySelector(), nl.item(0));

        // unmarshal the XMLSignature
        XMLSignature signature = fac.unmarshalXMLSignature(valContext);

        // Validate the XMLSignature (generated above)
        boolean coreValidity = signature.validate(valContext);

        // Check core validation status
        if (coreValidity == false) {
            System.err.println("Signature failed core validation");
            boolean sv = signature.getSignatureValue().validate(valContext);
            System.out.println("signature validation status: " + sv);
            // check the validation status of each Reference
            Iterator<Reference> i =
                signature.getSignedInfo().getReferences().iterator();
            for (int j=0; i.hasNext(); j++) {
                boolean refValid = i.next().validate(valContext);
                System.out.println("ref["+j+"] validity status: " + refValid);
            }
        } else {
            System.out.println("Signature passed core validation");
        }
    }

    /**
     * KeySelector which retrieves the public key out of the
     * KeyValue element and returns it.
     * NOTE: If the key algorithm doesn't match signature algorithm,
     * then the public key will be ignored.
     */
    private static class KeyValueKeySelector extends KeySelector {
        public KeySelectorResult select(KeyInfo keyInfo,
                                        KeySelector.Purpose purpose,
                                        AlgorithmMethod method,
                                        XMLCryptoContext context)
            throws KeySelectorException {
            if (keyInfo == null) {
                throw new KeySelectorException("Null KeyInfo object!");
            }
            SignatureMethod sm = (SignatureMethod) method;
            List<XMLStructure> list = keyInfo.getContent();

            for (int i = 0; i < list.size(); i++) {
                XMLStructure xmlStructure = list.get(i);
                if (xmlStructure instanceof KeyValue) {
                    PublicKey pk = null;
                    try {
                        pk = ((KeyValue)xmlStructure).getPublicKey();
                    } catch (KeyException ke) {
                        throw new KeySelectorException(ke);
                    }
                    // make sure algorithm is compatible with method
                    if (algEquals(sm.getAlgorithm(), pk.getAlgorithm())) {
                        return new SimpleKeySelectorResult(pk);
                    }
                }
            }
            throw new KeySelectorException("No KeyValue element found!");
        }

        static boolean algEquals(String algURI, String algName) {
            if (algName.equalsIgnoreCase("DSA") &&
                algURI.equalsIgnoreCase("http://www.w3.org/2009/xmldsig11#dsa-sha256")) {
                return true;
            } else if (algName.equalsIgnoreCase("RSA") &&
                       algURI.equalsIgnoreCase("http://www.w3.org/2001/04/xmldsig-more#rsa-sha256")) {
                return true;
            } else {
                return false;
            }
        }
    }

    private static class SimpleKeySelectorResult implements KeySelectorResult {
        private PublicKey pk;
        SimpleKeySelectorResult(PublicKey pk) {
            this.pk = pk;
        }

        public Key getKey() { return pk; }
    }
}
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0__GUID-A82408FF-EC50-46A6-8D22-3B06B85AB588">
Example 12-2 envelope.xml

``` {.oac_no_warn dir="ltr"}
<Envelope xmlns="urn:envelope">
</Envelope>
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0__GUID-4DCD9F0B-02C7-4C00-AB66-096C7F262ACF">
Example 12-3 signature.xml

This file has been indented and formatted for readability.

``` {.oac_no_warn dir="ltr"}
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<Envelope xmlns="urn:envelope">
  <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
    <SignedInfo>
      <CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315#WithComments"/>
      <SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"/>
      <Reference URI="">
        <Transforms>
          <Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
        </Transforms>
        <DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"/>
        <DigestValue>/juoQ4bDxElf1M+KJauO20euW+QAvvPP0nDCruCQooM=</DigestValue>
      </Reference>
    </SignedInfo>
    <SignatureValue>
Vorr4nABCD7eWOjh4jn8pdM5iseGJPt4BmlgjEbxr05TsR9ObHq7WLVOBOtJfb3M6pXv6NnTucpH
e/97zHbuUMaNeGxCs/gN7YDUGOkQE1Gs4HAbGwXuTcif3pw+066ZW4uxyzapwS6lZHmqIm7PRl8I
NIQXVL4dezLe+rx77Kh+rZRheVe4UlTTP+TmIOaBZo93GQ5FudreMhSiuIC0Nx2SP7mAkt6+8kVH
luZouFbqriSvyhzIxDgyOXpm/PHCuuPU2scCokwjEZBtlZXDOl6lIWGllnyrptWntQ6F/ngQObI5
c2+npgCshq1svGuS/xx18MAFHGWi98Vj+07QCg==
    </SignatureValue>
    <KeyInfo>
      <KeyValue>
        <RSAKeyValue>
          <Modulus>
9hSmAKw/4TTw/1l1u1pYzdFm6lOjRB/5NfdGWl/fB8iAa/tiK0f1u/VWoK6SMtogYgSDKqQThbAu
9dy9rRnOWRGY2He1JtpOvGh0WCmIFUEs2P22HvEf+JGKVEpkoP4hv53ucT69T+7nKGK3/bjxgp+T
C7fbnVj651+jAHuDFlC8Txt1R8ZymfN5cUeHIH96dvNFrtai/uwZDbVMfhV9chL//+Vyhx4O5nHv
jfS+0So9Qi52YAbEyLu6+BLdu8wnMWapC88CfXsRwrpx8b6aCU0e6QSZyOvdgXWz3+9ifVTBDIxE
kjhL5OASx0qjvc+dPUOMvq7fJE05RRZLyb0YJw==
          </Modulus>
          <Exponent>AQAB</Exponent>
        </RSAKeyValue>
      </KeyValue>
    </KeyInfo>
  </Signature>
</Envelope>
```

</div>
<!-- class="example" -->

</div>
<div class="sect4">
[]{#GUID-28D86779-8D2A-4741-8D78-49830EFF9473}

#### Validating an XML Signature {#JSSEC-GUID-28D86779-8D2A-4741-8D78-49830EFF9473 .sect4}

<div>
This example shows you how to validate an XML Signature using the Java
XML Digital Signature API. The example uses DOM (the Document Object
Model) to parse an XML document containing a Signature element and a DOM
implementation to validate the signature.

</div>
</div>
<div class="sect4">
[]{#GUID-B2651FD1-F5CD-49D1-8541-466ABAB7ECA8}

#### Instantiating the Document that Contains the Signature {#JSSEC-GUID-B2651FD1-F5CD-49D1-8541-466ABAB7ECA8 .sect4}

<div>
First we use a JAXP <span class="apiname">DocumentBuilderFactory</span>
to parse the XML document containing the
<span class="apiname">Signature</span>. An application obtains the
default implementation for
<span class="apiname">DocumentBuilderFactory</span> by calling the
following line of code:

``` {.oac_no_warn dir="ltr"}
    DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
```

We must also make the factory namespace-aware:

``` {.oac_no_warn dir="ltr"}
    dbf.setNamespaceAware(true);
```

Next, we use the factory to get an instance of a
<span class="apiname">DocumentBuilder</span>, which is used to parse the
document:

``` {.oac_no_warn dir="ltr"}
    Document doc = null;
    try (FileInputStream fis = new FileInputStream(args[0])) {
        doc = dbf.newDocumentBuilder().parse(fis);
    }
```

</div>
</div>
<div class="sect4">
[]{#GUID-66D2F1B6-2D1E-4721-B70B-4BA32103A79E}

#### Specifying the Signature Element to be Validated {#JSSEC-GUID-66D2F1B6-2D1E-4721-B70B-4BA32103A79E .sect4}

<div>
We need to specify the <span class="apiname">Signature</span> element
that we want to validate, since there could be more than one in the
document. We use the DOM method
<span class="apiname">Document.getElementsByTagNameNS</span>, passing it
the XML Signature namespace URI and the tag name of the
<span class="apiname">Signature</span> element, as shown:

``` {.oac_no_warn dir="ltr"}
    NodeList nl =
        doc.getElementsByTagNameNS(XMLSignature.XMLNS, "Signature");
    if (nl.getLength() == 0) {
        throw new Exception("Cannot find Signature element");
    } 
```

This returns a list of all <span class="apiname">Signature</span>
elements in the document. In this example, there is only one
<span class="apiname">Signature</span> element.

</div>
</div>
<div class="sect4">
[]{#GUID-FCBFE214-3F87-412D-BC0F-EC4CE1519529}

#### Creating a Validation Context {#JSSEC-GUID-FCBFE214-3F87-412D-BC0F-EC4CE1519529 .sect4}

<div>
We create an <span class="apiname">XMLValidateContext</span> instance
containing input parameters for validating the signature. Since we are
using DOM, we instantiate a
<span class="apiname">DOMValidateContext</span> instance (a subclass of
<span class="apiname">XMLValidateContext</span>), and pass it two
parameters, a <span class="apiname">KeyValueKeySelector</span> object
and a reference to the Signature element to be validated (which is the
first entry of the <span class="apiname">NodeList</span> we generated
earlier):

``` {.oac_no_warn dir="ltr"}
    DOMValidateContext valContext = new DOMValidateContext
        (new KeyValueKeySelector(), nl.item(0));
```

The <span class="apiname">KeyValueKeySelector</span> is explained in
greater detail in [Using
KeySelectors](java-xml-digital-signature-api-overview-and-tutorial.htm#GUID-26946ED1-1BBE-4AFD-B1CA-5A6A46FD7354).

</div>
</div>
<div class="sect4">
[]{#GUID-B5297B69-8989-4D40-994D-C40ED0C71C94}

#### Unmarshalling the XML Signature {#JSSEC-GUID-B5297B69-8989-4D40-994D-C40ED0C71C94 .sect4}

<div>
We extract the contents of the <span class="apiname">Signature</span>
element into an <span class="apiname">XMLSignature</span> object. This
process is called unmarshalling. The
<span class="apiname">Signature</span> element is unmarshalled using an
<span class="apiname">XMLSignatureFactory</span> object. An application
can obtain a DOM implementation of
<span class="apiname">XMLSignatureFactory</span> by calling the
following line of code:

``` {.oac_no_warn dir="ltr"}
    XMLSignatureFactory fac = XMLSignatureFactory.getInstance("DOM");
```

We then invoke the <span class="apiname">unmarshalXMLSignature</span>
method of the factory to unmarshal an
<span class="apiname">XMLSignature</span> object, and pass it the
validation context we created earlier:

``` {.oac_no_warn dir="ltr"}
    XMLSignature signature = fac.unmarshalXMLSignature(valContext);
```

</div>
</div>
<div class="sect4">
[]{#GUID-CF8C37C4-7360-4833-83FB-6A2948C26818}

#### Validating the XML Signature {#JSSEC-GUID-CF8C37C4-7360-4833-83FB-6A2948C26818 .sect4}

<div>
Now we are ready to validate the signature. We do this by invoking the
validate method on the <span class="apiname">XMLSignature</span> object,
and pass it the validation context as follows:

``` {.oac_no_warn dir="ltr"}
    boolean coreValidity = signature.validate(valContext);
```

The validate method returns \"true\" if the signature validates
successfully according to the core validation rules in the W3C XML
Signature Recommendation, and false otherwise.

</div>
<div class="sect5">
[]{#GUID-20CF389E-3F3F-4156-B8A3-CFB411E75274}

##### What If the XML Signature Fails to Validate? {#JSSEC-GUID-20CF389E-3F3F-4156-B8A3-CFB411E75274 .sect5}

<div>
If the <span class="apiname">XMLSignature.validate</span> method returns
false, we can try to narrow down the cause of the failure. There are two
phases in core XML Signature validation:

-   Signature validation (the cryptographic verification of the
    signature)
-   Reference validation (the verification of the digest of each
    reference in the signature)

Each phase must be successful for the signature to be valid. To check if
the signature failed to cryptographically validate, we can check the
status, as follows:

``` {.oac_no_warn dir="ltr"}
    boolean sv = signature.getSignatureValue().validate(valContext);
    System.out.println("signature validation status: " + sv);
```

We can also iterate over the references and check the validation status
of each one, as follows:

``` {.oac_no_warn dir="ltr"}
    Iterator<Reference> i =
        signature.getSignedInfo().getReferences().iterator();
    for (int j=0; i.hasNext(); j++) {
        boolean refValid = i.next().validate(valContext);
        System.out.println("ref["+j+"] validity status: " + refValid);
    }
```

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-26946ED1-1BBE-4AFD-B1CA-5A6A46FD7354}

#### Using KeySelectors {#JSSEC-GUID-26946ED1-1BBE-4AFD-B1CA-5A6A46FD7354 .sect4}

<div>
<span class="apiname">KeySelector</span>s are used to find and select
keys that are needed to validate an
<span class="apiname">XMLSignature</span>. Earlier, when we created a
<span class="apiname">DOMValidateContext</span> object, we passed a
`KeyValueKeySelector`{.codeph} object as the first argument:

``` {.oac_no_warn dir="ltr"}
    DOMValidateContext valContext = new DOMValidateContext
        (new KeyValueKeySelector(), nl.item(0));
```

Alternatively, we could have passed a
<span class="apiname">PublicKey</span> as the first argument if we
already knew what key is needed to validate the signature. However, we
often don\'t know.

The `KeyValueKeySelector`{.codeph} class is a concrete implementation of
the abstract <span class="apiname">KeySelector</span> class. The
`KeyValueKeySelector`{.codeph} implementation tries to find an
appropriate validation key using the data contained in
<span class="apiname">KeyValue</span> elements of the
<span class="apiname">KeyInfo</span> element of an
<span class="apiname">XMLSignature</span>. It does not determine if the
key is trusted. This is a very simple
<span class="apiname">KeySelector</span> implementation, designed for
illustration rather than real-world usage. A more practical example of a
<span class="apiname">KeySelector</span> is one that searches a
<span class="apiname">KeyStore</span> for trusted keys that match
<span class="apiname">X509Data</span> information (for example,
<span class="apiname">X509SubjectName</span>,
<span class="apiname">X509IssuerSerial</span>,
<span class="apiname">X509SKI</span>, or
<span class="apiname">X509Certificate</span> elements) contained in a
<span class="apiname">KeyInfo</span>.

The implementation of the `KeyValueKeySelector`{.codeph} class is as
follows:

``` {.oac_no_warn dir="ltr"}
    private static class KeyValueKeySelector extends KeySelector {
        public KeySelectorResult select(KeyInfo keyInfo,
                                        KeySelector.Purpose purpose,
                                        AlgorithmMethod method,
                                        XMLCryptoContext context)
            throws KeySelectorException {
            if (keyInfo == null) {
                throw new KeySelectorException("Null KeyInfo object!");
            }
            SignatureMethod sm = (SignatureMethod) method;
            List<XMLStructure> list = keyInfo.getContent();

            for (int i = 0; i < list.size(); i++) {
                XMLStructure xmlStructure = list.get(i);
                if (xmlStructure instanceof KeyValue) {
                    PublicKey pk = null;
                    try {
                        pk = ((KeyValue)xmlStructure).getPublicKey();
                    } catch (KeyException ke) {
                        throw new KeySelectorException(ke);
                    }
                    // make sure algorithm is compatible with method
                    if (algEquals(sm.getAlgorithm(), pk.getAlgorithm())) {
                        return new SimpleKeySelectorResult(pk);
                    }
                }
            }
            throw new KeySelectorException("No KeyValue element found!");
        }

        static boolean algEquals(String algURI, String algName) {
            if (algName.equalsIgnoreCase("DSA") &&
                algURI.equalsIgnoreCase("http://www.w3.org/2009/xmldsig11#dsa-sha256")) {
                return true;
            } else if (algName.equalsIgnoreCase("RSA") &&
                       algURI.equalsIgnoreCase("http://www.w3.org/2001/04/xmldsig-more#rsa-sha256")) {
                return true;
            } else {
                return false;
            }
        }
    }

    private static class SimpleKeySelectorResult implements KeySelectorResult {
        private PublicKey pk;
        SimpleKeySelectorResult(PublicKey pk) {
            this.pk = pk;
        }

        public Key getKey() { return pk; }
    }
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108}

### GenEnveloped Example {#JSSEC-GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108 .sect3}

<div>
To compile and run this sample, execute the following command:

``` {.oac_no_warn dir="ltr"}
$ javac GenEnveloped.java
$ java GenEnveloped envelope.xml envelopedSignature.xml
```

The sample program will generate an enveloped signature of the document
in the file `envelope.xml` and store it in the file
`envelopedSignature.xml` in the current working directory.

<div class="example" id="GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108__GUID-6CB4162E-30CE-41BF-8767-2C5B88063D8F">
Example 12-4 GenEnveloped.java

``` {.oac_no_warn dir="ltr"}
import javax.xml.crypto.dsig.*;
import javax.xml.crypto.dsig.dom.DOMSignContext;
import javax.xml.crypto.dsig.keyinfo.*;
import javax.xml.crypto.dsig.spec.*;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.security.*;
import java.util.List;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.transform.*;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
import org.w3c.dom.Document;

/**
 * This is a simple example of generating an Enveloped XML
 * Signature using the Java XML Digital Signature API. The
 * resulting signature will look like (key and signature
 * values will be different):
 *
 * <pre><code>
 *<Envelope xmlns="urn:envelope">
 * <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
 *   <SignedInfo>
 *     <CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315"/>
 *     <SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"/>
 *     <Reference URI="">
 *       <Transforms>
 *         <Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
 *       </Transforms>
 *       <DigestMethod Algorithm="http://www.w3.org/2001/04/xmlenc#sha256"/>
 *       <DigestValue>/juoQ4bDxElf1M+KJauO20euW+QAvvPP0nDCruCQooM=<DigestValue>
 *     </Reference>
 *   </SignedInfo>
 *   <SignatureValue>
 *     YeS+F0uiYv0h946M69Q9pKFNnD6dxUwLA8QT3GX/0H3cSPKRnNFyZiR4RPgaA1ir/ztb4rt6Lqb8
 *     hgwPERIa5qhoGUJyHDfUTcQ0Xqn1jYCVoC3ho+oUgJPXNVgtMAtpvOgxcWXUPATYdyimO6RrHF8+
 *     JXDkeICI9BPA4NKN1i77CAy6JJbaA87aNIpMJPImwJf8CM7mYsXremZz+RsafNE2cXXRzAoNOynC
 *     pi4oPYpE7CBLzhd23gf7zYRoyT06/bVIj4j3qOlVY1TQofsQ20NtAz6PbqAs7QkNoDzkX1CYlDSJ
 *     U8cGHuwXpul/UIpOiL6MZF8I/YI4ZlJn+O8Mvg==
 *   </SignatureValue>
 *   <KeyInfo>
 *     <KeyValue>
 *       <RSAKeyValue>
 *         <Modulus>
 *           mH0S/iw2K2tFTFHI75BtB67pzjR52HvQ8K7Xi5UX3NJm0oA+KX2mm0IrVcUuv609vbAAyQoW7CWm
 *           4kswVgStCm68dlw36309cxrEmPhG+PKBmUaGuBmRzwityjXRyRZJ6yaLenE8SJO/DC5ntQvmHqQQ
 *           qeOJYvz2Cbi2bi6x9XwmpqOfZCE5iTvYwioEsrglhP1uLG9fiXyNR2PXUTyLqD91HLhZFj1CEiU7
 *           aE++WfkKaowIx5p8e3F6hQ+VFRNXjtemK5aajuL0gwU+Oujg9ijgbyMh19vBoI8LruJoMOBrYFNN
 *           2boQJ3wP0Ek7CPIqAzQB5MnmvKc9jICKiiZVZw==
 *         </Modulus>
 *         <Exponent>AQAB</Exponent>
 *       </RSAKeyValue>
 *     </KeyValue>
 *   </KeyInfo>
 * </Signature>
 *</Envelope>
 * </code></pre>
 */
public class GenEnveloped {

    //
    // Synopsis: java GenEnveloped [document] [output]
    //
    //    where "document" is the name of a file containing the XML document
    //    to be signed, and "output" is the name of the file to store the
    //    signed document. The 2nd argument is optional - if not specified,
    //    standard output will be used.
    //
    public static void main(String[] args) throws Exception {
        
        // Instantiate the document to be signed
        DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
        dbf.setNamespaceAware(true);
        Document doc = null;
        try (FileInputStream fis = new FileInputStream(args[0])) {
            doc = dbf.newDocumentBuilder().parse(fis);
        }
        
        // Create a RSA KeyPair
        KeyPairGenerator kpg = KeyPairGenerator.getInstance("RSA");
        kpg.initialize(2048);
        KeyPair kp = kpg.generateKeyPair();
        
        // Create a DOMSignContext and specify the RSA PrivateKey and
        // location of the resulting XMLSignature's parent element
        DOMSignContext dsc = new DOMSignContext
            (kp.getPrivate(), doc.getDocumentElement());
      
        // Create a DOM XMLSignatureFactory that will be used to generate the
        // enveloped signature
        XMLSignatureFactory fac = XMLSignatureFactory.getInstance("DOM");

        // Create a Reference to the enveloped document (in this case we are
        // signing the whole document, so a URI of "" signifies that) and
        // also specify the SHA256 digest algorithm and the ENVELOPED Transform.
        Reference ref = fac.newReference
            ("", fac.newDigestMethod(DigestMethod.SHA256, null),
             List.of
              (fac.newTransform
                (Transform.ENVELOPED, (TransformParameterSpec) null)),
             null, null);

        // Create the SignedInfo
        SignedInfo si = fac.newSignedInfo
            (fac.newCanonicalizationMethod
             (CanonicalizationMethod.INCLUSIVE_WITH_COMMENTS,
              (C14NMethodParameterSpec) null),
             fac.newSignatureMethod("http://www.w3.org/2001/04/xmldsig-more#rsa-sha256", null),
             List.of(ref));

        // Create a KeyValue containing the RSA PublicKey that was generated
        KeyInfoFactory kif = fac.getKeyInfoFactory();
        KeyValue kv = kif.newKeyValue(kp.getPublic());

        // Create a KeyInfo and add the KeyValue to it
        KeyInfo ki = kif.newKeyInfo(List.of(kv));

        // Create the XMLSignature (but don't sign it yet)
        XMLSignature signature = fac.newXMLSignature(si, ki);

        // Marshal, generate (and sign) the enveloped signature
        signature.sign(dsc);

        // output the resulting document
        OutputStream os;
        if (args.length > 1) {
           os = new FileOutputStream(args[1]);
        } else {
           os = System.out;
        }

        TransformerFactory tf = TransformerFactory.newInstance();
        Transformer trans = tf.newTransformer();
        trans.transform(new DOMSource(doc), new StreamResult(os));
    }
}
```

</div>
<!-- class="example" -->

<div class="example" id="GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108__GUID-EB71567E-2E84-4301-98EC-65664665A996">
Example 12-5 envelope.xml

``` {.oac_no_warn dir="ltr"}
<Envelope xmlns="urn:envelope">
</Envelope>
```

</div>
<!-- class="example" -->

</div>
<div class="sect4">
[]{#GUID-177088CC-2CFD-477D-BB05-E8B9C48AE270}

#### Generating an XML Signature {#JSSEC-GUID-177088CC-2CFD-477D-BB05-E8B9C48AE270 .sect4}

<div>
This example shows you how to generate an XML Signature using the XML
Digital Signature API. More specifically, the example generates an
enveloped XML Signature of an XML document. An enveloped signature is a
signature that is contained inside the content that it is signing. The
example uses DOM (the Document Object Model) to parse the XML document
to be signed and a DOM implementation to generate the resulting
signature.

A basic knowledge of XML Signatures and their different components is
helpful for understanding this section. See [XML Signature Syntax and
Processing Version 1.1](https://www.w3.org/TR/xmldsig-core/) for more
information.

</div>
</div>
<div class="sect4">
[]{#GUID-37E2785A-6ACD-4E09-9A72-4F6AE9A641D9}

#### Instantiating the Document to be Signed {#JSSEC-GUID-37E2785A-6ACD-4E09-9A72-4F6AE9A641D9 .sect4}

<div>
First, we use a JAXP <span class="apiname">DocumentBuilderFactory</span>
to parse the XML document that we want to sign. An application obtains
the default implementation for
<span class="apiname">DocumentBuilderFactory</span> by calling the
following line of code:

``` {.oac_no_warn dir="ltr"}
    DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
```

We must also make the factory namespace-aware:

``` {.oac_no_warn dir="ltr"}
    dbf.setNamespaceAware(true);
```

Next, we use the factory to get an instance of a
<span class="apiname">DocumentBuilder</span>, which is used to parse the
document:

``` {.oac_no_warn dir="ltr"}
    Document doc = null;
    try (FileInputStream fis = new FileInputStream(args[0])) {
        doc = dbf.newDocumentBuilder().parse(fis);
    }
```

</div>
</div>
<div class="sect4">
[]{#GUID-A0C0D616-CD13-441C-A1A2-122431692B9F}

#### Creating a Public Key Pair {#JSSEC-GUID-A0C0D616-CD13-441C-A1A2-122431692B9F .sect4}

<div>
We generate a public key pair. Later in the example, we will use the
private key to generate the signature. We create the key pair with a
<span class="apiname">KeyPairGenerator</span>. In this example, we will
create a RSA <span class="apiname">KeyPair</span> with a length of 2048
bytes:

``` {.oac_no_warn dir="ltr"}
    KeyPairGenerator kpg = KeyPairGenerator.getInstance("RSA");
    kpg.initialize(2048);
    KeyPair kp = kpg.generateKeyPair();
```

In practice, the private key is usually previously generated and stored
in a <span class="apiname">KeyStore</span> file with an associated
public key certificate.

</div>
</div>
<div class="sect4">
[]{#GUID-2FA5FBA6-8DB7-460D-BDEA-2BF38B14BC19}

#### Creating a Signing Context {#JSSEC-GUID-2FA5FBA6-8DB7-460D-BDEA-2BF38B14BC19 .sect4}

<div>
We create an <span class="apiname">XMLSignContext</span> containing
input parameters for generating the signature. Since we are using DOM,
we instantiate a <span class="apiname">DOMSignContext</span> (a subclass
of <span class="apiname">XMLSignContext</span>), and pass it two
parameters, the private key that will be used to sign the document and
the root of the document to be signed:

``` {.oac_no_warn dir="ltr"}
    DOMSignContext dsc = new DOMSignContext
        (kp.getPrivate(), doc.getDocumentElement());
```

</div>
</div>
<div class="sect4">
[]{#GUID-3DEB54D1-220A-4140-832D-DD42976057B6}

#### Assembling the XML Signature {#JSSEC-GUID-3DEB54D1-220A-4140-832D-DD42976057B6 .sect4}

<div>
We assemble the different parts of the Signature element into an
<span class="apiname">XMLSignature</span> object. These objects are all
created and assembled using an
<span class="apiname">XMLSignatureFactory</span> object. An application
obtains a DOM implementation of
<span class="apiname">XMLSignatureFactory</span> by calling the
following line of code:

``` {.oac_no_warn dir="ltr"}
    XMLSignatureFactory fac = XMLSignatureFactory.getInstance("DOM");
```

We then invoke various factory methods to create the different parts of
the <span class="apiname">XMLSignature</span> object as shown below. We
create a <span class="apiname">Reference</span> object, passing to it
the following:

-   The URI of the object to be signed (We specify a URI of \"\", which
    implies the root of the document.)

<!-- -->

-   The <span class="apiname">DigestMethod</span> (we use SHA256)

<!-- -->

-   A single <span class="apiname">Transform</span>, the enveloped
    <span class="apiname">Transform</span>, which is required for
    enveloped signatures so that the signature itself is removed before
    calculating the signature value

``` {.oac_no_warn dir="ltr"}
    Reference ref = fac.newReference
        ("", fac.newDigestMethod(DigestMethod.SHA256, null),
         List.of
          (fac.newTransform
            (Transform.ENVELOPED, (TransformParameterSpec) null)),
         null, null);
```

Next, we create the <span class="apiname">SignedInfo</span> object,
which is the object that is actually signed, as shown below. When
creating the <span class="apiname">SignedInfo</span>, we pass as
parameters:

-   The <span class="apiname">CanonicalizationMethod</span> (we use
    inclusive and preserve comments)

<!-- -->

-   The <span class="apiname">SignatureMethod</span> (we use RSA)

<!-- -->

-   A list of <span class="apiname">References</span> (in this case,
    only one)

``` {.oac_no_warn dir="ltr"}
    SignedInfo si = fac.newSignedInfo
        (fac.newCanonicalizationMethod
         (CanonicalizationMethod.INCLUSIVE_WITH_COMMENTS,
          (C14NMethodParameterSpec) null),
         fac.newSignatureMethod("http://www.w3.org/2001/04/xmldsig-more#rsa-sha256", null),
         List.of(ref));
```

Next, we create the optional <span class="apiname">KeyInfo</span>
object, which contains information that enables the recipient to find
the key needed to validate the signature. In this example, we add a
<span class="apiname">KeyValue</span> object containing the public key.
To create <span class="apiname">KeyInfo</span> and its various subtypes,
we use a <span class="apiname">KeyInfoFactory</span> object, which can
be obtained by invoking the
<span class="apiname">getKeyInfoFactory</span> method of the
<span class="italic">XMLSignatureFactory</span>, as follows:

``` {.oac_no_warn dir="ltr"}
    KeyInfoFactory kif = fac.getKeyInfoFactory();
```

We then use the <span class="apiname">KeyInfoFactory</span> to create
the <span class="apiname">KeyValue</span> object and add it to a
<span class="apiname">KeyInfo</span> object:

``` {.oac_no_warn dir="ltr"}
    KeyValue kv = kif.newKeyValue(kp.getPublic());
    KeyInfo ki = kif.newKeyInfo(List.of(kv));
```

Finally, we create the <span class="apiname">XMLSignature</span> object,
passing as parameters the <span class="apiname">SignedInfo</span> and
<span class="apiname">KeyInfo</span> objects that we created earlier:

``` {.oac_no_warn dir="ltr"}
    XMLSignature signature = fac.newXMLSignature(si, ki);
```

Notice that we haven\'t actually generated the signature yet; we\'ll do
that in the next step.

</div>
</div>
<div class="sect4">
[]{#GUID-3B6E8DE8-AC10-46B2-BC89-9E0B2CE8634C}

#### Generating the XML Signature {#JSSEC-GUID-3B6E8DE8-AC10-46B2-BC89-9E0B2CE8634C .sect4}

<div>
Now we are ready to generate the signature, which we do by invoking the
sign method on the <span class="apiname">XMLSignature</span> object, and
pass it the signing context as follows:

``` {.oac_no_warn dir="ltr"}
    signature.sign(dsc);
```

The resulting document now contains a signature, which has been inserted
as the last child element of the root element.

</div>
</div>
<div class="sect4">
[]{#GUID-1D6C3745-9E04-400A-ADD1-65E5FD3ADB5C}

#### Printing or Displaying the Resulting Document {#JSSEC-GUID-1D6C3745-9E04-400A-ADD1-65E5FD3ADB5C .sect4}

<div>
You can use the following code to print the resulting signed document to
a file or standard output:

``` {.oac_no_warn dir="ltr"}
    OutputStream os;
    if (args.length > 1) {
       os = new FileOutputStream(args[1]);
    } else {
       os = System.out;
    }

    TransformerFactory tf = TransformerFactory.newInstance();
    Transformer trans = tf.newTransformer();
    trans.transform(new DOMSource(doc), new StreamResult(os));
```

</div>
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
| -------------------- | r | ---                  |
| ------------ ------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------  | e | )\                   |
| --                   | L |             <span cl |
|                      | o | ass="icon">Contents< |
|     [![Previous](../ | g | /span>](toc.htm)     |
| ../dcommon/gifs/left | o |   -- --------------- |
| nav.gif)\            | ] | -------------------- |
|                      | ( | -------------------- |
|      [![Next](../../ | . | ---                  |
| dcommon/gifs/rightna | . |                      |
| v.gif)\              | / |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](j | . |                      |
| ava-sasl-api-program | / |                      |
| ming-and-deployment- | d |                      |
| guide1.htm)   <span  | c |                      |
| class="icon">Next</s | o |                      |
| pan>](security-api-s | m |                      |
| pecification1.htm)   | m |                      |
|   ------------------ | o |                      |
| -------------------- | n |                      |
| -------------------- | / |                      |
| -------------------- | g |                      |
| ------------ ------- | i |                      |
| -------------------- | f |                      |
| -------------------- | s |                      |
| -------------------  | / |                      |
| --                   | o |                      |
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
