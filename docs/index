
[]{#top}
[Go to primary content](#BEGIN)
+-----------------------------------+----------------------------------:+ | **Java Platform, Standard Edition | -- | | Security Developer's Guide**\ | -- | | **Release 11**\ | | | E94828-01 | | +-----------------------------------+-----------------------------------+

Next\
Next

[]{#BEGIN}
Contents {#contents .toc}
Title and Copyright Information {#title-and-copyright-information .tocheader}
Preface {#preface .tocheader}

    Audience
    Documentation Accessibility
    Related Documents
    Conventions

1 General Security {#general-security .tocheader}

    Java Security Overview
        Introduction to Java Security
        Java Language Security and Bytecode Verification
        Basic Security Architecture
            Security Providers
            File Locations
        Java Cryptography
        Public Key Infrastructure
            Key and Certificate Storage
            Public Key Infrastructure Tools
        Authentication
        Secure Communication
            SSL, TLS, and DTLS Protocols
            Simple Authentication and Security Layer (SASL)
            Generic Security Service API and Kerberos
        Access Control
            Permissions
            Security Policy
            Access Control Enforcement
        XML Signature
        Additional Information about Java Security
        Java Security Classes Summary
        Deprecated Security APIs Marked for Removal
        Security Tools Summary
        Built-In Providers
    Java SE Platform Security Architecture
        Introduction
            The Original Sandbox Model
            Evolving the Sandbox Model
        Protection Mechanisms -- Overview of Basic Concepts
        Permissions and Security Policy
            The Permission Classes
                java.security.Permission
                java.security.PermissionCollection
                java.security.Permissions
                java.security.UnresolvedPermission
                java.io.FilePermission
                java.net.SocketPermission
                java.security.BasicPermission
                java.util.PropertyPermission
                java.lang.RuntimePermission
                java.awt.AWTPermission
                java.net.NetPermission
                java.lang.reflect.ReflectPermission
                java.io.SerializablePermission
                java.security.SecurityPermission
                java.security.AllPermission
                javax.security.auth.AuthPermission
                Discussion of Permission Implications
                How To Create New Types of Permissions
            java.security.CodeSource
            java.security.Policy
                Policy File Format
                Property Expansion in Policy Files
                General Expansion in Policy Files
                Assigning Permissions
                Default System and User Policy Files
                Customizing Policy Evaluation
            java.security.GeneralSecurityException
        Access Control Mechanisms and Algorithms
            java.security.ProtectionDomain
            java.security.AccessController
                Algorithm for Checking Permissions
                Handling Privileges
            Inheritance of Access Control Context
            java.security.AccessControlContext
        Secure Class Loading
            Class Loader Class Hierarchies
            The Primordial Class Loader
            Class Loader Delegation
            Class Resolution Algorithm
        Security Management
            Managing Applets and Applications
            SecurityManager versus AccessController
            Auxiliary Tools
                The Key and Certificate Management Tool
                The JAR Signing and Verification Tool
        GuardedObject and SignedObject
            java.security.GuardedObject and java.security.Guard
            java.security.SignedObject
        Discussion and Future Directions
            Resource Consumption Management
            Arbitrary Grouping of Permissions
            Object-Level Protection
            Subdividing Protection Domains
            Running Applets with Signed Content
        Appendix A: API for Privileged Blocks
            Using the doPrivileged API
                No Return Value, No Exception Thrown
                Returning Values
                Accessing Local Variables
                Handling Exceptions
                Asserting a Subset of Privileges
                Least Privilege
                More Privilege
            What It Means to Have Privileged Code
            Reflection
        Appendix B: Acknowledgments
        Appendix C: References
    Standard Algorithm Names
    Permissions in the JDK
        Permission Descriptions and Risks
            Methods and the Permissions They Require
            java.lang.SecurityManager Method Permission Checks
        Default Policy Implementation and Policy File Syntax
            Default Policy Implementation
            Default Policy File Locations
            Modifying the Policy Implementation
            Policy File Syntax
                Keystore Entry
                Grant Entries
                The SignedBy, Principal, and CodeBase Fields
                KeyStore Alias Replacement
                The Permission Entries
                File Path Specifications on Windows Systems
            Policy File Examples
            Property Expansion in Policy Files
            Windows Systems, File Paths, and Property Expansion
            General Expansion in Policy Files
        Appendix A: FilePermission Path Name Canonicalization Disabled By Default
    Troubleshooting Security

2 Java Cryptography Architecture (JCA) Reference Guide {#java-cryptography-architecture-jca-reference-guide .tocheader}

    Introduction to Java Cryptography Architecture
        JCA Design Principles
        Provider Architecture
            Cryptographic Service Providers
            How Providers Are Actually Implemented
            Keystores
        Engine Classes and Algorithms
    Core Classes and Interfaces
        The Provider Class
            How Provider Implementations Are Requested and Supplied
            Installing Providers
            Provider Class Methods
        The Security Class
            Managing Providers
            Security Properties
        The SecureRandom Class
            Creating a SecureRandom Object
            Seeding or Re-Seeding the SecureRandom Object
            Using a SecureRandom Object
            Generating Seed Bytes
        The MessageDigest Class
            Creating a MessageDigest Object
            Updating a Message Digest Object
            Computing the Digest
        The Signature Class
            Signature Object States
            Creating a Signature Object
            Initializing a Signature Object
            Signing with a Signature Object
            Verifying with a Signature Object
        The Cipher Class
        Other Cipher-based Classes
            The Cipher Stream Classes
            The SealedObject Class
        The Mac Class
        Key Interfaces
        The KeyPair Class
        Key Specification Interfaces and Classes
            The KeySpec Interface
            The KeySpec Subinterfaces
            The EncodedKeySpec Class
                The PKCS8EncodedKeySpec Class
                The X509EncodedKeySpec Class
        Generators and Factories
            The KeyFactory Class
            The SecretKeyFactory Class
            The KeyPairGenerator Class
            The KeyGenerator Class
        The KeyAgreement Class
        Key Management
            The KeyStore Class
        Algorithm Parameters Classes
            The AlgorithmParameterSpec Interface
            The AlgorithmParameters Class
            The AlgorithmParameterGenerator Class
        The CertificateFactory Class
    How the JCA Might Be Used in a SSL/TLS Implementation
    Cryptographic Strength Configuration
    Jurisdiction Policy File Format
    How to Make Applications Exempt from Cryptographic Restrictions
    Standard Names
    Packaging Your Application
    Additional JCA Code Samples
        Computing a MessageDigest Object
        Generating a Pair of Keys
        Generating and Verifying a Signature Using Generated Keys
        Generating/Verifying Signatures Using Key Specifications and KeyFactory
        Generating Random Numbers
        Determining If Two Keys Are Equal
        Reading Base64-Encoded Certificates
        Parsing a Certificate Reply
        Using Encryption
        Using Password-Based Encryption
    Sample Programs for Diffie-Hellman Key Exchange, AES/GCM, and HMAC-SHA256
        Diffie-Hellman Key Exchange between 2 Parties
        Diffie-Hellman Key Exchange between 3 Parties
        AES/GCM Example
        HMAC-SHA256 Example

3 How to Implement a Provider in the Java Cryptography Architecture {#how-to-implement-a-provider-in-the-java-cryptography-architecture .tocheader}

    Who Should Read This Document
    Notes on Terminology
    Introduction to Implementing Providers
    Engine Classes and Corresponding Service Provider Interface Classes
    Steps to Implement and Integrate a Provider
        Step 1: Write your Service Implementation Code
            Step 1.1: Consider Additional JCA Provider Requirements and Recommendations for Encryption Implementations
        Step 2: Give your Provider a Name
        Step 3: Write Your Master Class, a Subclass of Provider
            Step 3.1: Create a Provider That Uses String Objects to Register Its Services
            Step 3.2: Create a Provider That Uses Provider.Service
            Step 3.3: Specify Additional Information for Cipher Implementations
        Step 4: Create a Module Declaration for Your Provider
        Step 5: Compile Your Code
        Step 6: Place Your Provider in a JAR File
        Step 7: Sign Your JAR File, If Necessary
            Step 7.1: Get a Code-Signing Certificate
            Step 7.2: Sign Your Provider
        Step 8: Prepare for Testing
            Step 8.1: Configure the Provider
            Step 8.2: Set Provider Permissions
        Step 9: Write and Compile Your Test Programs
        Step 10: Run Your Test Programs
        Step 11: Apply for U.S. Government Export Approval If Required
        Step 12: Document Your Provider and Its Supported Services
            Step 12.1: Indicate Whether Your Implementation is Cloneable for Message Digests and MACs
        Step 13: Make Your Class Files and Documentation Available to Clients
    Further Implementation Details and Requirements
        Alias Names
        Service Interdependencies
        Default Initialization
        Default Key Pair Generator Parameter Requirements
        The Provider.Service Class
        Signature Formats
        DSA Interfaces and their Required Implementations
        RSA Interfaces and their Required Implementations
        Diffie-Hellman Interfaces and their Required Implementations
        Interfaces for Other Algorithm Types
        Algorithm Parameter Specification Interfaces and Classes
        Key Specification Interfaces and Classes Required by Key Factories
        Secret-Key Generation
        Adding New Object Identifiers
        Ensuring Exportability
    Sample Code for MyProvider

4 JDK Providers Documentation {#jdk-providers-documentation .tocheader}

    Introduction to JDK Providers
    Import Limits on Cryptographic Algorithms
    Cipher Transformations
    SecureRandom Implementations
    The SunPKCS11 Provider
    The SUN Provider
    The SunRsaSign Provider
    The SunJSSE Provider
    The SunJCE Provider
    The SunJGSS Provider
    The SunSASL Provider
    The XMLDSig Provider
    The SunPCSC Provider
    The SunMSCAPI Provider
    The SunEC Provider
    The OracleUcrypto Provider
    The Apple Provider
    The JdkLDAP Provider
    The JdkSASL Provider

5 PKCS#11 Reference Guide {#pkcs11-reference-guide .tocheader}

    SunPKCS11 Provider
    SunPKCS11 Requirements
    SunPKCS11 Configuration
    Accessing Network Security Services (NSS)
    Troubleshooting PKCS#11
    Disabling PKCS#11 Providers and/or Individual PKCS#11 Mechanisms
    Application Developers
        Token Login
        Token Keys
        Delayed Provider Selection
        JAAS KeyStoreLoginModule
        Tokens as JSSE Keystore and Trust Stores
    Using keytool and jarsigner with PKCS#11 Tokens
    Policy Tool
    Provider Developers
        Provider Services
        Parameter Support
    SunPKCS11 Provider Supported Algorithms
    SunPKCS11 Provider KeyStore Requirements
    Example Provider

6 Java Authentication and Authorization Service (JAAS) {#java-authentication-and-authorization-service-jaas .tocheader}

    Java Authentication and Authorization Service (JAAS) Reference Guide
        Who Should Read This Document
        Related Documentation
        Core Classes and Interfaces
            Common Classes
                Subject
                Principals
                Credentials
            Authentication Classes and Interfaces
                LoginContext
                LoginModule
                CallbackHandler
                Callback
            Authorization Classes
                Policy
                AuthPermission
                PrivateCredentialPermission
        JAAS Tutorials and Sample Programs
        Appendix A: JAAS Settings in the java.security Security Properties File
            Login Configuration Provider
            Login Configuration URLs
            Policy Provider
            Policy File URLs
        Appendix B: JAAS Login Configuration File
            Login Configuration File Structure and Contents
            Where to Specify Which Login Configuration File Should Be Used
    JAAS Tutorials
        JAAS Authentication Tutorial
            The Authentication Tutorial Code
                SampleAcn.java
                SampleLoginModule.java and SamplePrincipal.java
            The Login Configuration
                The Login Configuration File for the JAAS Authentication Tutorial
            Running the Code
            Running the Code with a Security Manager
        JAAS Authorization Tutorial
            What is JAAS Authorization?
            How is JAAS Authorization Performed?
                How Do You Make Principal-Based Policy File Statements?
                How Do You Associate a Subject with an Access Control Context?
            The Authorization Tutorial Code
                SampleAzn.java
                SampleAction.java
            The Login Configuration File for the JAAS Authorization Tutorial
            The Policy File
                Permissions Required by SampleAzn
                Permissions Required by SampleAction
                Permissions Required by SampleLoginModule
                The Full Policy File
                Running the Authorization Tutorial Code
    Java Authentication and Authorization Service (JAAS): LoginModule Developer's Guide
        Introduction to LoginModule
        Steps to Implement a LoginModule
            Step 1: Understand the Authentication Technology
            Step 2: Name the LoginModule Implementation
            Step 3: Implement the Abstract LoginModule Methods
            Step 4: Choose or Write a Sample Application
            Step 5: Compile the LoginModule and Application
            Step 6: Prepare for Testing
            Step 7: Test Use of the LoginModule
            Step 8: Document Your LoginModule Implementation
            Step 9: Make LoginModule JAR File and Documents Available

7 Java Generic Security Services (Java GSS-API) {#java-generic-security-services-java-gss-api .tocheader}

    Introduction to JAAS and Java GSS-API Tutorials
        When to Use Java GSS-API Versus JSSE
        Use of Java GSS-API for Secure Message Exchanges Without JAAS Programming
            Overview of the Client and Server Applications
            The SampleClient and SampleServer Code
                Obtaining the Command-Line Arguments
                Establishing a Socket Connection for Message Exchanges
                Establishing a Security Context
                Exchanging Messages Securely
                Clean Up
            Kerberos User and Service Principal Names
                When the Realm Is Required in Principal Names
            The Login Configuration File
            The useSubjectCredsOnly System Property
            Running the SampleClient and SampleServer Programs
                Prepare SampleServer for Execution
                Prepare SampleClient for Execution
                Execute SampleServer
                Execute SampleClient
        JAAS Authentication
            The Authentication Tutorial Code
                Instantiating a LoginContext
                Calling the LoginContext's login Method
            The Login Configuration
                The Login Configuration File for This Tutorial
            Running the Code
            Running the Code with a Security Manager
        JAAS Authorization
            What is JAAS Authorization?
            How Is JAAS Authorization Performed?
                How Do You Make Principal-Based Policy File Statements?
                How Do You Associate a Subject with an Access Control Context?
            The Authorization Tutorial Code
                JaasAzn.java
                SampleAction.java
            The Login Configuration File
            The Policy File
                Permissions Required by JaasAzn
                Permissions Required by SampleAction
            Running the Authorization Tutorial Code
        Use of JAAS Login Utility
            What You Need to Know About the Login Utility
            Application and Other File Requirements
                Application Requirements
                Login Configuration File Requirements
                Policy File Requirements
            The Sample Application Program
            The Login Configuration File
            The Policy File
                Permissions Required by the Login and MyAction Classes
                Permissions Required by Sample
            Running the Sample Program with the Login Utility
        Use of JAAS Login Utility and Java GSS-API for Secure Message Exchanges
            Before You Start: Recommended Reading
            Overview of the Client and Server Applications
            Kerberos User and Service Principal Names
                When the Realm is Required in Principal Names
            The Login Configuration File
            The Policy Files
                The Client Policy File
                The Server Policy File
            Running the SampleClient and SampleServer Programs
                Prepare SampleServer for Execution
                Prepare SampleClient for Execution
                Execute SampleServer
                Execute SampleClient
        More Things You Can Do with Java GSS-API and JAAS
            Executing Code on Behalf of the Client User
                Basic Approach
                Sample Code and Policy File
                Running the Sample Code
            Using Credentials Delegated from the Client
            Permission Required In Order to Delegate Credentials
        Kerberos Requirements
            Setting Properties to Indicate the Default Realm and KDC
            Locating the krb5.conf Configuration File
            Naming Conventions for Realm Names and Hostnames
            Cross-Realm Authentication
        Troubleshooting
        Source Code for JAAS and Java GSS-API Tutorials
        Related Documentation
    Single Sign-on Using Kerberos in Java
        Abstract
        Introduction
        Kerberos V5
        Java Authentication and Authorization Service (JAAS)
            Pluggable and Stackable Framework
            Authentication and Authorization
            Subject
            doAs and doAsPrivileged
            LoginContext
            Callbacks
            LoginModules
            The Kerberos Login Module
            Kerberos Classes
            Authorization
        Java Generic Security Service Application Program Interface (Java GSS-API)
            Generic Security Service API (GSS-API)
            Java GSS-API
            The GSSName Interface
            The GSSCredential Interface
            The GSSContext Interface
            Message Protection
            Credential Delegation
        Default Credential Acquisition Model
        Exceptions to the Model
        Web Browser Integration
        Security Risks
            Credential Acquisition
            Context Establishment
            Credential Delegation
        Conclusions
        Acknowledgements
        References
    Advanced Security Programming in Java SE Authentication, Secure Communication and Single Sign-On
        Part I : Secure Authentication using the Java Authentication and Authorization Service (JAAS)
            Exercise 1: Using the JAAS API
            Exercise 2: Configuring JAAS for Kerberos Authentication
        Part II : Secure Communications using the Java SE Security API
            Exercise 3: Using the Java Generic Security Service (GSS) API
            Exercise 4: Using the Java SASL API
            Exercise 5: Using the Java Secure Socket Extension with Kerberos
        Part III : Deploying for Single Sign-On in a Kerberos Environment
            Exercise 6: Deploying for Single Sign-On
        Part IV : Secure Communications Using Stronger Encryption Algorithms
            Exercise 7: Configuring to Use Stronger Encryption Algorithms in a Kerberos Environment, to Secure the Communication
        Part V : Secure Authentication Using SPNEGO Java GSS Mechanism
            Exercise 8: Using the Java Generic Security Services (GSS) API with SPNEGO
        Part VI: HTTP/SPNEGO Authentication
            Exercise 9: Using HTTP/SPNEGO Authentication
                What is HTTP SPNEGO
                How to use HTTP/SPNEGO Authentication
                HTTP/SPNEGO Authentication Example
        Source Code for Advanced Security Programming in Java SE Authentication, Secure Communication and Single Sign-On
        Appendix A: Setting up Kerberos Accounts
    The Kerberos 5 GSS-API Mechanism

8 Java Secure Socket Extension (JSSE) Reference Guide {#java-secure-socket-extension-jsse-reference-guide .tocheader}

    Introduction to JSSE
        JSSE Features and Benefits
        JSSE Standard API
        SunJSSE Provider
        JSSE Related Documentation
    Terms and Definitions
    Secure Sockets Layer (SSL) Protocol Overview
        Why Use SSL?
        How SSL Works
        Cryptographic Processes
            Secret-Key Cryptography
            Public-Key Cryptography
            Comparison Between Secret-Key and Public-Key Cryptography
            Public Key Certificates
            Cryptographic Hash Functions
            Message Authentication Code
            Digital Signatures
        The SSL Handshake
        The SSL Protocol
            Handshaking Again (Renegotiation)
            Cipher Suite Choice and Remote Entity Verification
    Client-Driven OCSP and OCSP Stapling
        Client-Driven OCSP and Certificate Revocation
            Setting up a Java Client to use Client-Driven OCSP
        OCSP Stapling and Certificate Revocation
            Setting Up a Java Client to Use OCSP Stapling
            Setting Up a Java Server to Use OCSP Stapling
        OCSP Stapling Configuration Properties
    JSSE Classes and Interfaces
        JSSE Core Classes and Interfaces
        SocketFactory and ServerSocketFactory Classes
        SSLSocketFactory and SSLServerSocketFactory Classes
            Obtaining an SSLSocketFactory
        SSLSocket and SSLServerSocket Classes
            Obtaining an SSLSocket
        SSLEngine Class
            Creating an SSLEngine Object
            Generating and Processing SSL/TLS Data
            Datagram Transport Layer Security (DTLS) Protocol
                The DTLS Handshake
                Handling Retransmissions in DTLS Connections
            Creating an SSLEngine Object for DTLS
            Generating and Processing DTLS Data
            Understanding SSLEngine Operation Statuses
            Dealing With Blocking Tasks
            Shutting Down a SSL/TLS/DTLS Connection
        SSLSession and ExtendedSSLSession
        HttpsURLConnection Class
            Setting the Assigned SSLSocketFactory
            Setting the Assigned HostnameVerifier
        Support Classes and Interfaces
            The SSLContext Class
                Obtaining and Initializing the SSLContext Class
                Creating an SSLContext Object
            The TrustManager Interface
            The TrustManagerFactory Class
                Creating a TrustManagerFactory
                PKIX TrustManager Support
            The X509TrustManager Interface
                Creating an X509TrustManager
                Creating Your Own X509TrustManager
                Updating the Keystore Dynamically
            X509ExtendedTrustManager Class
                Creating an X509ExtendedTrustManager
                Creating Your Own X509ExtendedTrustManager
            The KeyManager Interface
            The KeyManagerFactory Class
                Creating a KeyManagerFactory
            The X509KeyManager Interface
                Creating an X509KeyManager
                Creating Your Own X509KeyManager
            The X509ExtendedKeyManager Class
            Relationship Between a TrustManager and a KeyManager
        Secondary Support Classes and Interfaces
            The SSLParameters Class
                Cipher Suite Preference
            The SSLSessionContext Interface
            The SSLSessionBindingListener Interface
            The SSLSessionBindingEvent Class
            The HandShakeCompletedListener Interface
            The HandShakeCompletedEvent Class
            The HostnameVerifier Interface
            The X509Certificate Class
            The AlgorithmConstraints Interface
            The StandardConstants Class
            The SNIServerName Class
            The SNIMatcher Class
            The SNIHostName Class
    Customizing JSSE
        How to Specify a java.lang.System Property
        How to Specify a java.security.Security Property
        Customizing the X509Certificate Implementation
        Specifying Default Enabled Cipher Suites
        Specifying an Alternative HTTPS Protocol Implementation
        Customizing the Provider Implementation
        Registering the Cryptographic Provider Statically
        Registering the Cryptographic Service Provider Dynamically
        Provider Configuration
        Configuring the Preferred Provider for Specific Algorithms
        Customizing the Default Keystores and Truststores, Store Types, and Store Passwords
        Customizing the Default Key Managers and Trust Managers
        Disabled and Restricted Cryptographic Algorithms
        Customizing the Encryption Algorithm Providers
        Customizing Size of Ephemeral Diffie-Hellman Keys
        Customizing Maximum Fragment Length Negotiation (MFLN) Extension
        Configuring the Maximum and Minimum Packet Size
    Transport Layer Security (TLS) Renegotiation Issue
        Phased Approach to Fixing This Issue
        Description of the Phase 2 Fix
        Workarounds and Alternatives to SSL/TLS Renegotiation
        TLS Implementation Details
        Description of the Phase 1 Fix
        Allow Unsafe Server Certificate Change in SSL/TLS Renegotiations
    Hardware Acceleration and Smartcard Support
        Configuring JSSE to Use Smartcards as Keystores and Truststores
        Multiple and Dynamic Keystores
    Kerberos Cipher Suites
        Kerberos Requirements
        Peer Identity Information
        Security Manager
    Additional Keystore Formats (PKCS12)
    Server Name Indication (SNI) Extension
    TLS Application Layer Protocol Negotiation
        Setting up ALPN on the Client
        Setting up Default ALPN on the Server
        Setting up Custom ALPN on the Server
        Determining Negotiated ALPN Value during Handshaking
        ALPN Related Classes and Methods
    Troubleshooting JSSE
        Configuration Problems
            CertificateException While Handshaking
            Runtime Exception: SSL Service Not Available
            Runtime Exception: "No available certificate corresponding to the SSL cipher suites which are enabled"
            Runtime Exception: No Cipher Suites in Common
            Socket Disconnected After Sending ClientHello Message
            SunJSSE Cannot Find a JCA Provider That Supports a Required Algorithm and Causes a NoSuchAlgorithmException
            FailedDownloadException Thrown When Trying to Obtain Application Resources from Web Server over SSL
            IllegalArgumentException When RC4 Cipher Suites are Configured for DTLS
        Debugging Utilities
            Debugging SSL/TLS Connections
    Code Examples
        Converting an Unsecure Socket to a Secure Socket
        Running the JSSE Sample Code
        Creating a Keystore to Use with JSSE
        Using the Server Name Indication (SNI) Extension
            Typical Client-Side Usage Examples
            Typical Server-Side Usage Examples
            Working with Virtual Infrastructures
    Standard Names
    Provider Pluggability
    JSSE Cipher Suite Parameters

9 Running the JSSE Sample Code {#running-the-jsse-sample-code .tocheader}

    Sample Truststores
    Sample Code Illustrating a Secure Socket Connection Between a Client and a Server
        Configuration Requirements for SSL Socket Samples
        Running SSLSocketClient
        Running SSLSocketClientWithTunnelling
        Running SSLSocketClientWithClientAuth
        Running ClassFileServer
        Running SSLSocketClientWithClientAuth with ClassFileServer
    Sample Code Illustrating HTTPS Connections
        Running URLReader
        Running URLReaderWithOptions
    Sample Code Illustrating a Secure RMI Connection
    Sample Code Illustrating the Use of an SSLEngine
        Running SSLEngineSimpleDemo
    Troubleshooting JSSE Sample Code

10 Java PKI Programmers Guide {#java-pki-programmers-guide .tocheader}

    PKI Programmers Guide Overview
        Introduction to Public Key Certificates
        X.509 Certificates and Certificate Revocation Lists (CRLs)
    Core Classes and Interfaces
        Basic Certification Path Classes
            The CertPath Class
            The CertificateFactory Class
            The CertPathParameters Interface
        Certification Path Validation Classes
            The CertPathValidator Class
            The CertPathValidatorResult Interface
        Certification Path Building Classes
            The CertPathBuilder Class
            The CertPathBuilderResult Interface
        Certificate/CRL Storage Classes
            The CertStore Class
            The CertStoreParameters Interface
            The CertSelector and CRLSelector Interfaces
                The X509CertSelector Class
                The X509CRLSelector Class
        PKIX Classes
            The TrustAnchor Class
            The PKIXParameters Class
            The PKIXCertPathValidatorResult Class
            The PolicyNode Interface and PolicyQualifierInfo Class
            The PKIXBuilderParameters Class
            The PKIXCertPathBuilderResult Class
            The PKIXCertPathChecker Class
            Using PKIXCertPathChecker in Certificate Path Validation
                Check Revocation Status of Certificates with PKIXRevocationChecker Class
    Implementing a Service Provider
        Steps to Implement and Integrate a Provider
            Service Interdependencies
            Certification Path Parameter Specification Interfaces
            Certification Path Result Specification Interfaces
            Certification Path Exception Classes
    Appendix A: Standard Names
    Appendix B: CertPath Implementation in SUN Provider
    Appendix C: OCSP Support
    Appendix D: CertPath Implementation in JdkLDAP Provider
    Appendix E: Disabling Cryptographic Algorithms

11 Java SASL API Programming and Deployment Guide {#java-sasl-api-programming-and-deployment-guide .tocheader}

    Java SASL API Overview
        Creating the Mechanisms
        Passing Input to the Mechanisms
        Using the Mechanisms
        Using the Negotiated Security Layer
    How SASL Mechanisms are Installed and Selected
    The SunSASL Provider
        The SunSASL Provider Client Mechanisms
        The SunSASL Provider Server Mechanisms
    The JdkSASL Provider
        The JdkSASL Provider Client Mechanism
        The JdkSASL Provider Server Mechanism
    Debugging and Monitoring
    Implementing a SASL Security Provider

12 XML Digital Signature API Overview and Tutorial {#xml-digital-signature-api-overview-and-tutorial .tocheader}

    Package Hierarchy
    Service Providers
    Introduction to XML Signatures
        Example of an XML Signature
    XML Signature Secure Validation Mode
    XML Digital Signature API Examples
        Validate Example
            Validating an XML Signature
            Instantiating the Document that Contains the Signature
            Specifying the Signature Element to be Validated
            Creating a Validation Context
            Unmarshalling the XML Signature
            Validating the XML Signature
                What If the XML Signature Fails to Validate?
            Using KeySelectors
        GenEnveloped Example
            Generating an XML Signature
            Instantiating the Document to be Signed
            Creating a Public Key Pair
            Creating a Signing Context
            Assembling the XML Signature
            Generating the XML Signature
            Printing or Displaying the Resulting Document

13 Security API Specification {#security-api-specification .tocheader}
14 Deprecated Security APIs Marked for Removal {#deprecated-security-apis-marked-for-removal .tocheader}
15 Security Tools {#security-tools .tocheader}
16 Related Security Topics {#related-security-topics .tocheader}

+----------------------+---+---------------------:+ | ------------------ | ! | -- | | -------------------- | [ | -- | | ------ -- | O | | | [![Next](../../dc | r | | | ommon/gifs/rightnav. | a | | | gif)\ | c | | | Next](title | e | | | .htm) | L | | | ------------------ | o | | | -------------------- | g | | | ------ -- | o | | | | ] | | | | ( | | | | . | | | | . | | | | / | | | | . | | | | . | | | | / | | | | d | | | | c | | | | o | | | | m | | | | m | | | | o | | | | n | | | | / | | | | g | | | | i | | | | f | | | | s | | | | / | | | | o | | | | r | | | | a | | | | c | | | | l | | | | e | | | | . | | | | g | | | | i | | | | f | | | | ) | | | | { | | | | . | | | | c | | | | o | | | | p | | | | y | | | | r | | | | i | | | | g | | | | h | | | | t | | | | l | | | | o | | | | g | | | | o | | | | } | | | | [ | | | | \ | | | | < | | | | s | | | | p | | | | a | | | | n | | | | | | | | c | | | | l | | | | a | | | | s | | | | s | | | | = | | | | " | | | | c | | | | o | | | | p | | | | y | | | | r | | | | i | | | | g | | | | h | | | | t | | | | l | | | | o | | | | g | | | | o | | | | " | | | | > | | | | C | | | | o | | | | p | | | | y | | | | r | | | | i | | | | g | | | | h | | | | t | | | |   | | | | © | | | |   | | | | 1 | | | | 9 | | | | 9 | | | | 3 | | | | , | | | | 2 | | | | 0 | | | | 1 | | | | 8 | | | | , | | | | O | | | | r | | | | a | | | | c | | | | l | | | | e | | | |   | | | | a | | | | n | | | | d | | | | / | | | | o | | | | r | | | |   | | | | i | | | | t | | | | s | | | |   | | | | a | | | | f | | | | f | | | | i | | | | l | | | | i | | | | a | | | | t | | | | e | | | | s | | | | . | | | |   | | | | A | | | | l | | | | l | | | |   | | | | r | | | | i | | | | g | | | | h | | | | t | | | | s | | | |   | | | | r | | | | e | | | | s | | | | e | | | | r | | | | v | | | | e | | | | d | | | | . | | | | < | | | | / | | | | s | | | | p | | | | a | | | | n | | | | > | | | | ] | | | | ( | | | | . | | | | . | | | | / | | | | . | | | | . | | | | / | | | | d | | | | c | | | | o | | | | m | | | | m | | | | o | | | | n | | | | / | | | | h | | | | t | | | | m | | | | l | | | | / | | | | c | | | | p | | | | y | | | | r | | | | . | | | | h | | | | t | | | | m | | | | ) | | +----------------------+---+----------------------+

