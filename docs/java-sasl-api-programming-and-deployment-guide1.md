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

  --------------------------------------------------------------------- ------------------------------------------------------------------------------------------- --
              [![Previous](../../dcommon/gifs/leftnav.gif)\                                     [![Next](../../dcommon/gifs/rightnav.gif)\                          
   <span class="icon">Previous</span>](java-pki-programmers-guide.htm)   <span class="icon">Next</span>](java-xml-digital-signature-api-overview-and-tutorial.htm)  
  --------------------------------------------------------------------- ------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-6D78EE33-62E6-4D85-9695-322EED493F72}<!-- End Header -->

<span class="enumeration_chapter">11 </span>Java SASL API Programming and Deployment Guide {#JSSEC-GUID-6D78EE33-62E6-4D85-9695-322EED493F72 .sect1}
==========================================================================================

<div>
Simple Authentication and Security Layer, or SASL, is an Internet
standard ([RFC 2222](http://www.ietf.org/rfc/rfc2222.txt)) that
specifies a protocol for authentication and optional establishment of a
security layer between client and server applications. SASL defines how
authentication data is to be exchanged but does not itself specify the
contents of that data. It is a framework into which specific
authentication mechanisms that specify the contents and semantics of the
authentication data can fit.

SASL is used by protocols, such as the [Lightweight Directory Access
Protocol, version 3 (LDAP v3)](http://www.ietf.org/rfc/rfc2251.txt), and
the [Internet Message Access Protocol, version 4 (IMAP
v4)](http://www.ietf.org/rfc/rfc2060.txt) to enable pluggable
authentication. Instead of hardwiring an authentication method into the
protocol, LDAP v3 and IMAP v4 use SASL to perform authentication, thus
enabling authentication via various SASL mechanisms.

There are a number of standard SASL mechanisms defined by the Internet
community for various levels of security and deployment scenarios. These
range from no security (for example, anonymous authentication) to high
security (for example, Kerberos authentication) and levels in between.

<div class="section">
The Java SASL API

The Java SASL API defines classes and interfaces for applications that
use SASL mechanisms. It is defined to be mechanism-neutral: the
application that uses the API need not be hardwired into using any
particular SASL mechanism. The API supports both client and server
applications. It allows applications to select the mechanism to use
based on desired security features, such as whether they are susceptible
to passive dictionary attacks or whether they accept anonymous
authentication.

The Java SASL API also allows developers to use their own, custom SASL
mechanisms. SASL mechanisms are installed by using the Java Cryptography
Architecture (JCA); see [Java Cryptography Architecture (JCA) Reference
Guide](java-cryptography-architecture-jca-reference-guide.html#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190 "The Java Cryptography Architecture (JCA) is a major piece of the platform, and contains a "provider" architecture and a set of APIs for digital signatures, message digests (hashes), certificates and certificate validation, encryption (symmetric/asymmetric block/stream ciphers), key generation and management, and secure random number generation, to name a few.").

</div>
<!-- class="section" -->

<div class="section">
When to Use SASL

SASL provides a pluggable authentication and security layer for network
applications. There are other features in Java SE that provide similar
functionality, including Java Secure Socket Extension (JSSE) (see [Java
Secure Socket Extension (JSSE) Reference
Guide](java-secure-socket-extension-jsse-reference-guide.html#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345 "The Java Secure Socket Extension (JSSE) enables secure Internet communications. It provides a framework and an implementation for a Java version of the SSL, TLS, and DTLS protocols and includes functionality for data encryption, server authentication, message integrity, and optional client authentication."))
and the [Java Generic Security
Service](http://www.ietf.org/rfc/rfc2853.txt). JSSE provides a framework
and an implementation for a Java language version of the SSL, TLS, and
DTLS protocols. Java GSS is the Java language bindings for the [Generic
Security Service Application Programming Interface
(GSS-API)](http://www.ietf.org/rfc/rfc2743.txt). The only mechanism
currently supported underneath this API on Java SE is Kerberos v5.

With the exception of defining and building protocols from scratch,
protocol definition is often the biggest factor that goes into
determining which API to use. When compared with JSSE and Java GSS, SASL
is relatively lightweight and is popular among some protocols. It also
has the advantage that several popular, lightweight (in terms of
infrastructure support) SASL mechanisms have been defined. Primary JSSE
and Java GSS mechanisms, on the other hand, have relatively heavyweight
mechanisms that require more elaborate infrastructures (Public Key
Infrastructure and Kerberos, respectively).

SASL, JSSE, and Java GSS are often used together. For example, a common
pattern is for an application to use JSSE for establishing a secure
channel, and to use SASL for client, username/password-based
authentication. There are also SASL mechanisms layered on top of GSS-API
mechanisms; one popular example is a SASL GSS-API/Kerberos v5 mechanism
that is used with LDAP.

With the exception of defining and building protocols from scratch,
protocol definition is often the biggest factor in determining which API
to use. For example, LDAP and IMAP are defined to use SASL, so software
related to these protocols should use the Java SASL API. When building
Kerberos applications and services, the API to use is Java GSS. When
building applications and services that use SSL/TLS as their protocol,
the API to use is JSSE.

</div>
<!-- class="section" -->

</div>
<div class="sect2">
[]{#GUID-6F735DD5-1648-4BB7-A4BC-D001DC3B82AC}

Java SASL API Overview {#JSSEC-GUID-6F735DD5-1648-4BB7-A4BC-D001DC3B82AC .sect2}
----------------------

<div>
SASL is a challenge-response protocol. The server issues a challenge to
the client, and the client sends a response based on the challenge. This
exchange continues until the server is satisfied and issues no further
challenge. These challenges and responses are binary tokens of arbitrary
length. The encapsulating protocol (such as LDAP or IMAP) specifies how
these tokens are encoded and exchanged. For example, LDAP specifies how
SASL tokens are encapsulated within LDAP bind requests and responses.

The Java SASL API is modeled according to this style of interaction and
usage. It has interfaces, `SaslClient`{.codeph} and
`SaslServer`{.codeph}, that represent client-side and server-side
mechanisms, respectively. The application interacts with the mechanisms
via byte arrays that represent the challenges and responses. The
server-side mechanism iterates, issuing challenges and processing
responses, until it is satisfied, while the client-side mechanism
iterates, evaluating challenges and issuing responses, until the server
is satisfied. The application that is using the mechanism drives each
iteration. That is, it extracts the challenge or response from a
protocol packet and supplies it to the mechanism, and then puts the
response or challenge returned by the mechanism into a protocol packet
and sends it to the peer.

</div>
<div class="sect3">
[]{#GUID-7CFF731F-8330-40D6-8841-C1FB07C73655}

### Creating the Mechanisms {#JSSEC-GUID-7CFF731F-8330-40D6-8841-C1FB07C73655 .sect3}

<div>
The client and server code that use the SASL mechanisms are not
hardwired to use specific mechanism(s). In many protocols that use SASL,
the server advertises (either statically or dynamically) a list of SASL
mechanisms that it supports. The client then selects one of these based
on its security requirements.

<div class="section">
The
[<span class="apiname">Sasl</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/Sasl.html)
class is used for creating instances of
[<span class="apiname">SaslClient</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslClient.html)
and
[<span class="apiname">SaslServer</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslServer.html).
Here is an example of how an application creates a SASL client mechanism
using a list of possible SASL mechanisms.

``` {.codeblock dir="ltr"}
    String[] mechanisms = new String[]{"DIGEST-MD5", "PLAIN"}; 
    SaslClient sc = Sasl.createSaslClient(
        mechanisms, authzid, protocol, serverName, props, callbackHandler);
```

Based on the availability of the mechanisms supported by the platform
and other configuration information provided via the parameters, the
Java SASL framework selects one of the listed mechanisms and return an
instance of
[<span class="apiname">SaslClient</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslClient.html).

The name of the selected mechanism is usually transmitted to the server
via the application protocol. Upon receiving the mechanism name, the
server creates a corresponding
[<span class="apiname">SaslServer</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslServer.html)
object to process client-sent responses. Here is an example of how the
server would create an instance of
[<span class="apiname">SaslServer</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslServer.html).

``` {.codeblock dir="ltr"}
    SaslServer ss = Sasl.createSaslServer(
        mechanism, protocol, myName, props, callbackHandler);
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-90092190-14A7-48F9-923A-A37FDCC28D6B}

### Passing Input to the Mechanisms {#JSSEC-GUID-90092190-14A7-48F9-923A-A37FDCC28D6B .sect3}

<div>
Because the Java SASL API is a general framework, it must be able to
accommodate many different types of mechanisms. Each mechanism needs to
be initialized with input and may need input to make progress. The API
provides three means by which an application gives input to a mechanism:

1.  <span class="bold">Common input parameters</span>: The application
    uses predefined parameters to supply information that are defined by
    the SASL specification and commonly required by mechanisms.
    For[<span class="apiname">SaslClient</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslClient.html)
    mechanisms, the input parameters are authorization id, protocol id,
    and server name.
    For[<span class="apiname">SaslServer</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslServer.html)
    mechanisms, the common input parameters are protocol id and (its own
    fully qualified) server name.

2.  <span class="bold">Properties parameter</span>: The application uses
    the properties parameter, a mapping of property names to (possibly
    non-string) property values, to supply configuration information.
    The Java SASL API defines some standard properties, such as
    [<span class="apiname">Sasl.QOP</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/Sasl.html#QOP)
    (quality-of-protection),
    [<span class="apiname">Sasl.STRENGTH</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/Sasl.html#STRENGTH)
    (cipher strength), and
    [<span class="apiname">Sasl.MAX\_BUFFER</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/Sasl.html#MAX_BUFFER)
    (maximum buffer size). The parameter can also be used to pass in
    non-standard properties that are specific to particular mechanisms.

3.  <span class="bold">Callbacks</span>: The application uses the
    [<span class="apiname">CallbackHandler</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/CallbackHandler.html)
    parameter to supply input that cannot be predetermined or might not
    be common across mechanisms. When a mechanism requires input data,
    it uses the callback handler supplied by the application to collect
    the data, possibly from the end-user of the application. For
    example, a mechanism might require the end-user of the application
    to supply a name and password.

    Mechanisms can use the callbacks defined in the
    [<span class="apiname">javax.security.auth.callback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/package-summary.html)
    package; these are generic callbacks useful for building
    applications that perform authentication. Mechanisms might also need
    SASL-specific callbacks, such as those for collecting realm and
    authorization information, or even (non-standardized)
    mechanism-specific callbacks. The application should be able to
    accommodate a variety of mechanisms. Consequently, its callback
    handler must be able to service all of the callbacks that the
    mechanisms might request. This is not possible in general for
    arbitrary mechanisms, but is usually feasible due to the limited
    number of mechanisms that are typically deployed and used.

</div>
</div>
<div class="sect3">
[]{#GUID-F3774782-A395-48C9-A9BD-10C9F25FFE50}

### Using the Mechanisms {#JSSEC-GUID-F3774782-A395-48C9-A9BD-10C9F25FFE50 .sect3}

<div>
<div class="section">
Once the application has created a mechanism, it uses the mechanism to
obtain SASL tokens to exchange with the peer. The client typically
indicates to the server via the application protocol which mechanism to
use. Some protocols allow the client to accompany the request with an
optional initial response for mechanisms that have an initial response.
This feature can be used to lower the number of message exchanges
required for authentication. Here is an example of how a client might
use
[<span class="apiname">SaslClient</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslClient.html)
for authentication.

``` {.codeblock dir="ltr"}
    // Get optional initial response
    byte[] response = 
        (sc.hasInitialResponse() ? sc.evaluateChallenge(new byte[]) : null);

    String mechanism = sc.getMechanismName();

    // Send selected mechanism name and optional initial response to server
    send(mechanism, response);

    // Read response
    msg = receive();
    while (!sc.isComplete() && (msg.status == CONTINUE || msg.status == SUCCESS)) {
        // Evaluate server challenge
        response = sc.evaluateChallenge(msg.contents);

        if (msg.status == SUCCESS) {
            // done; server doesn't expect any more SASL data
             if (response != null) {
                throw new IOException(
                    "Protocol error: attempting to send response after completion");
            } 
            break;
        } else {
            send(mechanism, response);
            msg = receive();
        }
    }  
```

The client application iterates through each step of the authentication
by using the mechanism (`sc`{.codeph}) to evaluate the challenge gotten
from the server and to get a response to send back to the server. It
continues this cycle until either the mechanism or application-level
protocol indicates that the authentication has completed, or if the
mechanism cannot evaluate a challenge. If the mechanism cannot evaluate
the challenge, it throws an exception to indicate the error and
terminates the authentication. Disagreement between the mechanism and
protocol about the completion state must be treated as an error because
it might indicate a compromise of the authentication exchange.

Here is an example of how a server might use
[<span class="apiname">SaslServer</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslServer.html).

``` {.codeblock dir="ltr"}
    // Read request that contains mechanism name and optional initial response
    msg.receive();

    // Obtain a SaslServer to perform authentication
    SaslServer ss = Sasl.createSaslServer(msg.mechanism, 
        protocol, myName, props, callbackHandler);

    // Perform authentication steps until done
    while (!ss.isComplete()) {
        try {
            // Process response
            byte[] challenge = sc.evaluateResponse(msg.contents);

            if (ss.isComplete()) {
                send(mechanism, challenge, SUCCESS);
            } else {
                send(mechanism, challenge, CONTINUE);
                msg.receive();
            } 
        } catch (SaslException e) {
            send(ERROR);
            sc.dispose();
            break;
        }
    }
```

The server application iterates through each step of the authentication
by giving the client\'s response to the mechanism (`ss`{.codeph}) to
process. If the response is incorrect, the mechanism indicates the error
by throwing a
[<span class="apiname">SaslException</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslException.html)
so that the server can report the error and terminate the
authentication. If the response is correct, the mechanism returns
challenge data to be sent to the client and indicates whether the
authentication is complete. Note that challenge data can accompany a
\"success\" indication. This might be used, for example, to tell the
client to finalize some negotiated state.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-762BDD49-6EE8-419C-A45E-540462CB192B}

### Using the Negotiated Security Layer {#JSSEC-GUID-762BDD49-6EE8-419C-A45E-540462CB192B .sect3}

<div>
Some SASL mechanisms support only authentication while others support
use of a negotiated security layer after authentication. The security
layer feature is often not used when the application uses some other
means, such as SSL/TLS, to communicate securely with the peer.

<div class="section">
When a security layer has been negotiated, all subsequent communication
with the peer must take place using the security layer. To determine
whether a security layer has been negotiated, get the negotiated
[`Sasl.QOP`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/Sasl.html#QOP)
from the mechanism. Here is an example of how to determine whether a
security layer has been negotiated.

``` {.codeblock dir="ltr"}
String qop = (String) sc.getNegotiatedProperty(Sasl.QOP);
boolean hasSecurityLayer = (qop != null && 
    (qop.equals("auth-int") || qop.equals("auth-conf")));
```

A security layer has been negotiated if the
[`Sasl.QOP`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/Sasl.html#QOP)
property indicates that either integrity and/or confidentiality has been
negotiated.

To communicate with the peer using the negotiated layer, the application
first uses the
[`wrap`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslClient.html#wrap-byte:A-int-int-)
method to encode the data to be sent to the peer to produce a
\"wrapped\" buffer. It then transfers a length field representing the
number of octets in the wrapped buffer followed by the contents of the
wrapped buffer to the peer. The peer receiving the stream of octets
passes the buffer (without the length field) to
[`unwrap`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/SaslClient.html#unwrap-byte:A-int-int-)
to obtain the decoded bytes sent by the peer. Details of this protocol
are described in [RFC 2222](http://www.ietf.org/rfc/rfc2222.txt).
[Example
11-1](java-sasl-api-programming-and-deployment-guide1.html#GUID-762BDD49-6EE8-419C-A45E-540462CB192B__SAMPLECODEFORSASLCLIENTSENDANDRECEI-7547A249)
illustrates how a client application sends and receives application data
using a security layer.

</div>
<!-- class="section" -->

<div class="example" id="GUID-762BDD49-6EE8-419C-A45E-540462CB192B__SAMPLECODEFORSASLCLIENTSENDANDRECEI-7547A249">
Example 11-1 Sample Code for SASL Client Send and Receive Data

``` {.codeblock dir="ltr"}
// Send outgoing application data to peer
byte[] outgoing = ...;
byte[] netOut = sc.wrap(outgoing, 0, outgoing.length);

send(netOut.length, netOut);   // send to peer

// Receive incoming application data from peer
byte[] netIn = receive();      // read length and ensuing bytes from peer

byte[] incoming = sc.unwrap(netIn, 0, netIn.length);
```

</div>
<!-- class="example" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-93982F1C-AFFE-47B9-B4BA-41551ECCE2D2}

How SASL Mechanisms are Installed and Selected {#JSSEC-GUID-93982F1C-AFFE-47B9-B4BA-41551ECCE2D2 .sect2}
----------------------------------------------

<div>
SASL mechanism implementations are provided by SASL security providers.
Each provider may support one or more SASL mechanisms and is registered
with the JCA.

<div class="section">
By default, the SunSASL provider is automatically registered as a JCA
provider. To remove it or reorder its priority as a JCA provider, change
the line

``` {.codeblock dir="ltr"}
security.provider.7=SunSASL
```

in the Java security properties file
(`java-home/conf/security/java.security`).

To add or remove a SASL provider, you add or remove the corresponding
line in the security properties file. For example, if you want to add a
SASL provider and have its mechanisms be chosen over the same ones
implemented by the SunSASL provider, then you would add a line to the
security properties file with a lower number.

``` {.codeblock dir="ltr"}
security.provider.7=com.example.MyProvider
security.provider.8=SunSASL
```

Alternatively, you can programmatically add your own provider using the
`java.security.Security`{.codeph} class. For example, the following
sample code registers the `com.example.MyProvider`{.codeph} to the list
of available SASL security providers.

``` {.codeblock dir="ltr"}
Security.addProvider(new com.example.MyProvider());
```

See [Step 8: Prepare for
Testing](howtoimplaprovider.html#GUID-FB9C6DB2-DE9A-4EFE-89B4-C2C168C5982D "The next steps describe how to install and configure your new provider so that it is available via the JCA.")
in [Steps to Implement and Integrate a
Provider](howtoimplaprovider.html#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:")
for more information about adding providers to the security properties
file and programmatically adding your own providers.

When an application requests a SASL mechanism by supplying one or more
mechanism names, the SASL framework looks for registered SASL providers
that support that mechanism by going through, in order, the list of
registered providers. The providers must then determine whether the
requested mechanism matches the selection policy properties in the
[`Sasl`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/Sasl.html)
and if so, return an implementation for the mechanism.

The selection policy properties specify the security aspects of a
mechanism, such as its susceptibility to certain attacks. These are
characteristics of the mechanism (definition), rather than its
implementation so all providers should come to the same conclusion about
a particular mechanism. For example, the PLAIN mechanism is susceptible
to plaintext attacks regardless of how it is implemented. If no
selection policy properties are supplied, there are no restrictions on
the selected mechanism. Using these properties, an application can
ensure that it does not use unsuitable mechanisms that might be deployed
in the execution environment. For example, an application might use the
following sample code if it does not want to allow the use of mechanisms
susceptible to plaintext attacks.

``` {.codeblock dir="ltr"}
    Map<String, String> props = new HashMap<>();
    props.put(Sasl.POLICY_NOPLAINTEXT, "true");
    SaslClient sc = Sasl.createSaslClient(
        mechanisms, authzid, protocol, serverName, props, callbackHandler);
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-2F50B103-FE9F-459F-9EC5-B708358A7B59}

The SunSASL Provider {#JSSEC-GUID-2F50B103-FE9F-459F-9EC5-B708358A7B59 .sect2}
--------------------

<div>
<div class="section">
The SunSASL provider supports the following client and server
mechanisms:

-   Client Mechanisms
    -   PLAIN ([RFC 2595](http://www.ietf.org/rfc/rfc2595.txt)). This
        mechanism supports cleartext user name/password authentication.
    -   CRAM-MD5 ([RFC 2195](http://www.ietf.org/rfc/rfc2195.txt)). This
        mechanism supports a hashed user name/password authentication
        scheme.
    -   DIGEST-MD5 ([RFC 2831](http://www.ietf.org/rfc/rfc2831.txt)).
        This mechanism defines how HTTP Digest Authentication can be
        used as a SASL mechanism.
    -   EXTERNAL ([RFC 2222](http://www.ietf.org/rfc/rfc2222.txt)). This
        mechanism obtains authentication information from an external
        channel (such as TLS or IPsec).
    -   NTLM. This mechanism supports NTLM authentication.
-   Server Mechanisms
    -   CRAM-MD5
    -   DIGEST-MD5
    -   NTLM

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-681CD78D-D2E4-43DE-9225-249AA83FF177}

### The SunSASL Provider Client Mechanisms {#JSSEC-GUID-681CD78D-D2E4-43DE-9225-249AA83FF177 .sect3}

<div>
The SunSASL provider supports several SASL client mechanisms used in
popular protocols such as LDAP, IMAP, and SMTP.

<div class="section">
The following table summarizes the client mechanisms and their required
input.

<div class="tblformalwide" id="GUID-681CD78D-D2E4-43DE-9225-249AA83FF177__GUID-1D69316D-2076-406F-B36F-A36E7FF429FA">
Table 11-1 SunSASL Provider Client Mechanisms

+-------------+-------------+-------------+-------------+-------------+
| Client      | Parameters/ | Callbacks   | Configurati | Selection   |
| Mechanism   | Input       |             | on          | Policy      |
| Name        |             |             | Properties  |             |
+:============+:============+:============+:============+:============+
| [CRAM-MD5]( | authorizati | [<span clas |  None       | [<span clas |
| java-sasl-a | on id       | s="apiname" |             | s="apiname" |
| pi-programm | (as default | >PasswordCa |             | >Sasl.POLIC |
| ing-and-dep | user name)  | llback</spa |             | Y\_NOANONYM |
| loyment-gui |             | n>](https:/ |             | OUS</span>] |
| de1.html#GUI |             | /docs.oracl |             | (https://do |
| D-681CD78D- |             | e.com/javas |             | cs.oracle.c |
| D2E4-43DE-9 |             | e/10/docs/a |             | om/javase/1 |
| 225-249AA83 |             | pi/javax/se |             | 0/docs/api/ |
| FF177__CRAM |             | curity/auth |             | javax/secur |
| -MD5-20E3E2 |             | /callback/P |             | ity/sasl/Sa |
| 7A)         |             | asswordCall |             | sl.html#POL |
|             |             | back.html)  |             | ICY_NOANONY |
|             |             |             |             | MOUS)       |
|             |             | [<span clas |             |             |
|             |             | s="apiname" |             | [<span clas |
|             |             | >NameCallba |             | s="apiname" |
|             |             | ck</span>]( |             | >Sasl.POLIC |
|             |             | https://doc |             | Y\_NOPLAINT |
|             |             | s.oracle.co |             | EXT</span>] |
|             |             | m/javase/10 |             | (https://do |
|             |             | /docs/api/j |             | cs.oracle.c |
|             |             | avax/securi |             | om/javase/1 |
|             |             | ty/auth/cal |             | 0/docs/api/ |
|             |             | lback/NameC |             | javax/secur |
|             |             | allback.html |             | ity/sasl/Sa |
|             |             | l)          |             | sl.html#POL |
|             |             |             |             | ICY_NOPLAIN |
|             |             |             |             | TEXT)       |
+-------------+-------------+-------------+-------------+-------------+
| [DIGEST-MD5 | authorizati | [<span clas | [<span clas | [<span clas |
| ](java-sasl | on id       | s="apiname" | s="apiname" | s="apiname" |
| -api-progra |             | >NameCallba | >Sasl.QOP</ | >Sasl.POLIC |
| mming-and-d | protocol id | ck</span>]( | span>](http | Y\_NOANONYM |
| eployment-g |             | https://doc | s://docs.or | OUS</span>] |
| uide1.html#G | server name | s.oracle.co | acle.com/ja | (https://do |
| UID-681CD78 |             | m/javase/10 | vase/10/doc | cs.oracle.c |
| D-D2E4-43DE |             | /docs/api/j | s/api/javax | om/javase/1 |
| -9225-249AA |             | avax/securi | /security/s | 0/docs/api/ |
| 83FF177__DI |             | ty/auth/cal | asl/Sasl.ht | javax/secur |
| GEST-MD5-20 |             | lback/NameC | ml#QOP)     | ity/sasl/Sa |
| E3E4D3)     |             | allback.html |             | sl.html#POL |
|             |             | l)          | [<span clas | ICY_NOANONY |
|             |             |             | s="apiname" | MOUS)       |
|             |             | [<span clas | >Sasl.STREN |             |
|             |             | s="apiname" | GTH</span>] | [<span clas |
|             |             | >PasswordCa | (https://do | s="apiname" |
|             |             | llback</spa | cs.oracle.c | >Sasl.POLIC |
|             |             | n>](https:/ | om/javase/1 | Y\_NOPLAINT |
|             |             | /docs.oracl | 0/docs/api/ | EXT</span>] |
|             |             | e.com/javas | javax/secur | (https://do |
|             |             | e/10/docs/a | ity/sasl/Sa | cs.oracle.c |
|             |             | pi/javax/se | sl.html#STR | om/javase/1 |
|             |             | curity/auth | ENGTH)      | 0/docs/api/ |
|             |             | /callback/P |             | javax/secur |
|             |             | asswordCall | [<span clas | ity/sasl/Sa |
|             |             | back.html)  | s="apiname" | sl.html#POL |
|             |             |             | >Sasl.MAX\_ | ICY_NOPLAIN |
|             |             | [<span clas | BUFFER</spa | TEXT)       |
|             |             | s="apiname" | n>](https:/ |             |
|             |             | >RealmCallb | /docs.oracl |             |
|             |             | ack</span>] | e.com/javas |             |
|             |             | (https://do | e/10/docs/a |             |
|             |             | cs.oracle.c | pi/javax/se |             |
|             |             | om/javase/1 | curity/sasl |             |
|             |             | 0/docs/api/ | /Sasl.html# |             |
|             |             | javax/secur | MAX_BUFFER) |             |
|             |             | ity/sasl/Re |             |             |
|             |             | almCallback | [<span clas |             |
|             |             | .html)      | s="apiname" |             |
|             |             |             | >Sasl.SERVE |             |
|             |             | [<span clas | R\_AUTH</sp |             |
|             |             | s="apiname" | an>](https: |             |
|             |             | >RealmChoic | //docs.orac |             |
|             |             | eCallback</ | le.com/java |             |
|             |             | span>](http | se/10/docs/ |             |
|             |             | s://docs.or | api/javax/s |             |
|             |             | acle.com/ja | ecurity/sas |             |
|             |             | vase/10/doc | l/Sasl.html |             |
|             |             | s/api/javax | #SERVER_AUT |             |
|             |             | /security/s | H)          |             |
|             |             | asl/RealmCh |             |             |
|             |             | oiceCallbac | `javax.secu |             |
|             |             | k.html)     | rity.sasl.s |             |
|             |             |             | endmaxbuffe |             |
|             |             |             | r`{.codeph} |             |
|             |             |             |             |             |
|             |             |             | `com.sun.se |             |
|             |             |             | curity.sasl |             |
|             |             |             | .digest.cip |             |
|             |             |             | her`{.codep |             |
|             |             |             | h}          |             |
+-------------+-------------+-------------+-------------+-------------+
| EXTERNAL    | authorizati |  None       | None        | [<span clas |
|             | on id       |             |             | s="apiname" |
|             |             |             |             | >Sasl.POLIC |
|             | external ch |             |             | Y\_NOPLAINT |
|             | annel       |             |             | EXT</span>] |
|             |             |             |             | (https://do |
|             |             |             |             | cs.oracle.c |
|             |             |             |             | om/javase/1 |
|             |             |             |             | 0/docs/api/ |
|             |             |             |             | javax/secur |
|             |             |             |             | ity/sasl/Sa |
|             |             |             |             | sl.html#POL |
|             |             |             |             | ICY_NOPLAIN |
|             |             |             |             | TEXT)       |
|             |             |             |             |             |
|             |             |             |             | [<span clas |
|             |             |             |             | s="apiname" |
|             |             |             |             | >Sasl.POLIC |
|             |             |             |             | Y\_NOACTIVE |
|             |             |             |             | </span>](ht |
|             |             |             |             | tps://docs. |
|             |             |             |             | oracle.com/ |
|             |             |             |             | javase/10/d |
|             |             |             |             | ocs/api/jav |
|             |             |             |             | ax/security |
|             |             |             |             | /sasl/Sasl. |
|             |             |             |             | html#POLICY |
|             |             |             |             | _NOACTIVE)  |
|             |             |             |             |             |
|             |             |             |             | [<span clas |
|             |             |             |             | s="apiname" |
|             |             |             |             | >Sasl.POLIC |
|             |             |             |             | Y\_NODICTIO |
|             |             |             |             | NARY</span> |
|             |             |             |             | ](https://d |
|             |             |             |             | ocs.oracle. |
|             |             |             |             | com/javase/ |
|             |             |             |             | 10/docs/api |
|             |             |             |             | /javax/secu |
|             |             |             |             | rity/sasl/S |
|             |             |             |             | asl.html#PO |
|             |             |             |             | LICY_NODICT |
|             |             |             |             | IONARY)     |
+-------------+-------------+-------------+-------------+-------------+
| [NTLM](java | authzId (as | [<span clas | [<span clas | [<span clas |
| -sasl-api-p | default     | s="apiname" | s="apiname" | s="apiname" |
| rogramming- | user name)  | >RealmCallb | >Sasl.QOP</ | >Sasl.POLIC |
| and-deploym |             | ack</span>] | span>](http | Y\_NOANONYM |
| ent-guide1. | serverName  | (https://do | s://docs.or | OUS</span>] |
| htm#GUID-68 | (as default | cs.oracle.c | acle.com/ja | (https://do |
| 1CD78D-D2E4 | domain)     | om/javase/1 | vase/10/doc | cs.oracle.c |
| -43DE-9225- |             | 0/docs/api/ | s/api/javax | om/javase/1 |
| 249AA83FF17 |             | javax/secur | /security/s | 0/docs/api/ |
| 7__NTLM-231 |             | ity/sasl/Re | asl/Sasl.ht | javax/secur |
| 9A6BE)      |             | almCallback | ml#QOP)     | ity/sasl/Sa |
|             |             | .html)      |             | sl.html#POL |
|             |             |             | `com.sun.se | ICY_NOANONY |
|             |             | [<span clas | curity.sasl | MOUS)       |
|             |             | s="apiname" | .ntlm.versi |             |
|             |             | >NameCallba | on`{.codeph | [<span clas |
|             |             | ck</span>]( | }           | s="apiname" |
|             |             | https://doc |             | >Sasl.POLIC |
|             |             | s.oracle.co | `com.sun.se | Y\_NOPLAINT |
|             |             | m/javase/10 | curity.sasl | EXT</span>] |
|             |             | /docs/api/j | .ntlm.rando | (https://do |
|             |             | avax/securi | m`{.codeph} | cs.oracle.c |
|             |             | ty/auth/cal |             | om/javase/1 |
|             |             | lback/NameC | `com.sun.se | 0/docs/api/ |
|             |             | allback.html | curity.sasl | javax/secur |
|             |             | l)          | .ntlm.hostn | ity/sasl/Sa |
|             |             |             | ame`{.codep | sl.html#POL |
|             |             | [<span clas | h}          | ICY_NOPLAIN |
|             |             | s="apiname" |             | TEXT)       |
|             |             | >PasswordCa |             |             |
|             |             | llback</spa |             |             |
|             |             | n>](https:/ |             |             |
|             |             | /docs.oracl |             |             |
|             |             | e.com/javas |             |             |
|             |             | e/10/docs/a |             |             |
|             |             | pi/javax/se |             |             |
|             |             | curity/auth |             |             |
|             |             | /callback/P |             |             |
|             |             | asswordCall |             |             |
|             |             | back.html)  |             |             |
+-------------+-------------+-------------+-------------+-------------+
| PLAIN       | authorizati | [`NameCallb |  None       | [`Sasl.POLI |
|             | on id       | ack`{.codep |             | CY_NOANONYM |
|             |             | h}](https:/ |             | OUS`{.codep |
|             |             | /docs.oracl |             | h}](https:/ |
|             |             | e.com/javas |             | /docs.oracl |
|             |             | e/10/docs/a |             | e.com/javas |
|             |             | pi/javax/se |             | e/10/docs/a |
|             |             | curity/auth |             | pi/javax/se |
|             |             | /callback/N |             | curity/sasl |
|             |             | ameCallback |             | /Sasl.html# |
|             |             | .html)      |             | POLICY_NOAN |
|             |             |             |             | ONYMOUS)    |
|             |             | [<span clas |             |             |
|             |             | s="apiname" |             |             |
|             |             | >PasswordCa |             |             |
|             |             | llback</spa |             |             |
|             |             | n>](https:/ |             |             |
|             |             | /docs.oracl |             |             |
|             |             | e.com/javas |             |             |
|             |             | e/10/docs/a |             |             |
|             |             | pi/javax/se |             |             |
|             |             | curity/auth |             |             |
|             |             | /callback/P |             |             |
|             |             | asswordCall |             |             |
|             |             | back.html)  |             |             |
+-------------+-------------+-------------+-------------+-------------+

</div>
<!-- class="inftblhruleinformal" -->

An application that uses these mechanisms from the SunSASL provider must
supply the required parameters, callbacks and properties. The properties
have reasonable defaults and only need to be set if the application
wants to override the defaults. Most of the parameters, callbacks, and
properties are described in the API documentation. The following
sections describe mechanism-specific behaviors and parameters not
already covered by the API documentation.

</div>
<!-- class="section" -->

<div class="section" id="GUID-681CD78D-D2E4-43DE-9225-249AA83FF177__CRAM-MD5-20E3E27A">
Cram-MD5

The Cram-MD5 client mechanism uses the authorization id parameter, if
supplied, as the default user name in the `NameCallback`{.codeph} to
solicit the application/end-user for the authentication id. The
authorization id is otherwise not used by the Cram-MD5 mechanism; only
the authentication id is exchanged with the server.

</div>
<!-- class="section" -->

<div class="section" id="GUID-681CD78D-D2E4-43DE-9225-249AA83FF177__DIGEST-MD5-20E3E4D3">
Digest-MD5

The Digest-MD5 mechanism is used for digest authentication and optional
establishment of a security layer. It specifies the following ciphers
for use with the security layer: Triple DES, DES and RC4 (128, 56, and
40 bits). The Digest-MD5 mechanism can support only ciphers that are
available on the platform. For example, if the platform does not support
the RC4 ciphers, then the Digest-MD5 mechanism will not use those
ciphers.

The `Sasl.STRENGTH`{.codeph} property supports `high`{.codeph},
`medium`{.codeph}, and `low`{.codeph} settings; its default is
`high,medium,low`{.codeph}. The ciphers are mapped to the strength
settings as follows:

<div class="tblformalwide" id="GUID-681CD78D-D2E4-43DE-9225-249AA83FF177__GUID-F294490C-564E-4074-BE8B-B011BD34F308">
Table 11-2 Cipher Strength

+-----------------------+-----------------------+-----------------------+
| Strength              | Cipher                | Cipher Id             |
+:======================+:======================+:======================+
| high                  | Triple DES            | 3des rc4              |
|                       |                       |                       |
|                       | RC4 128 bits          |                       |
+-----------------------+-----------------------+-----------------------+
| medium                | DES                   | des rc4-56            |
|                       |                       |                       |
|                       | RC4 56 bits           |                       |
+-----------------------+-----------------------+-----------------------+
| low                   | RC4 40 bits           | rc4-40                |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

When there is more than one choice for a particular strength, the cipher
selected depends on the availability of the ciphers in the underlying
platform. To explicitly name the cipher to use, set the
`com.sun.security.sasl.digest.cipher`{.codeph} property to the
corresponding cipher id. Note that this property setting must be
compatible with `Sasl.STRENGTH`{.codeph} and the ciphers available in
the underlying platform. For example, `Sasl.STRENGTH`{.codeph} being set
to `low`{.codeph} and `com.sun.security.sasl.digest.cipher`{.codeph}
being set to `3des`{.codeph} are incompatible. The
`com.sun.security.sasl.digest.cipher`{.codeph} property has no default.

The `javax.security.sasl.sendmaxbuffer`{.codeph}property specifies (the
string representation of) the maximum send buffer size in bytes. The
default is 65536. The actual maximum number of bytes will be the minimum
of this number and the peer\'s maximum receive buffer size.

</div>
<!-- class="section" -->

<div class="section" id="GUID-681CD78D-D2E4-43DE-9225-249AA83FF177__NTLM-2319A6BE">
NTLM

<div class="infoboxnote" id="GUID-681CD78D-D2E4-43DE-9225-249AA83FF177__GUID-4D1CC0B8-4639-4805-AEF7-C774E8AD23D4">
Note:

This section applies both to the NTLM client mechanism and the NTLM
server mechanism.

</div>
NT LAN Manager (NTLM) is an security protocol from Microsoft used to
access their various services such as IIS Web Server and Exchange Mail
Server. As a SASL mechanism, it can be used to access Microsoft Exchange
Server. It is also useful for HTTP authentication with the NTLM scheme.

The NTLM mechanism is used for NTLM authentication. It does not provide
a security layer. This means that you can only set the
`javax.security.sasl.qop`{.codeph} environment property to
`auth`{.codeph}.

If the LMCompatibilityLevel registry value is set to a high value on the
server, certain low value requests are not supported. However, there\'s
no protocol for the server to inform the client to use a higher version,
so the user must manually choose the correct version on the client side.

Set the system property <span class="apiname">ntlm.debug</span> to any
value to turn on debugging

Provide the following information either at mechanism creation or
through callbacks:

<div class="tblformalwide" id="GUID-681CD78D-D2E4-43DE-9225-249AA83FF177__GUID-5B82E4DA-2BED-4FD0-B054-705FBEF1D69F">
Table 11-3 NTLM Required Information

+-----------------+-----------------+-----------------+-----------------+
| Information     | Type            | Required or     | Description     |
|                 |                 | Optional        |                 |
+:================+:================+:================+:================+
| Name            | <span class="ap | Required        | Provided        |
|                 | iname">String</ |                 | through         |
|                 | span>           |                 | [<span class="a |
|                 |                 |                 | piname">NameCal |
|                 |                 |                 | lback</span>](h |
|                 |                 |                 | ttps://docs.ora |
|                 |                 |                 | cle.com/javase/ |
|                 |                 |                 | 10/docs/api/jav |
|                 |                 |                 | ax/security/aut |
|                 |                 |                 | h/callback/Name |
|                 |                 |                 | Callback.html)  |
|                 |                 |                 | with the        |
|                 |                 |                 | <span class="ap |
|                 |                 |                 | iname">authzid< |
|                 |                 |                 | /span>          |
|                 |                 |                 | input argument  |
|                 |                 |                 | as the default  |
|                 |                 |                 | value           |
+-----------------+-----------------+-----------------+-----------------+
| Password        | <span class="ap | Required        | Provided        |
|                 | iname">char\[\] |                 | through         |
|                 | </span>         |                 | [<span class="a |
|                 |                 |                 | piname">Passwor |
|                 |                 |                 | dCallback</span |
|                 |                 |                 | >](https://docs |
|                 |                 |                 | .oracle.com/jav |
|                 |                 |                 | ase/10/docs/api |
|                 |                 |                 | /javax/security |
|                 |                 |                 | /auth/callback/ |
|                 |                 |                 | PasswordCallbac |
|                 |                 |                 | k.html)         |
|                 |                 |                 |                 |
|                 |                 |                 | If the password |
|                 |                 |                 | contains        |
|                 |                 |                 | non-ASCII       |
|                 |                 |                 | characters, the |
|                 |                 |                 | original LM     |
|                 |                 |                 | version might   |
|                 |                 |                 | fail. In this   |
|                 |                 |                 | case, do not    |
|                 |                 |                 | choose          |
|                 |                 |                 | <span class="ap |
|                 |                 |                 | iname">LM</span |
|                 |                 |                 | >               |
|                 |                 |                 | as the version. |
+-----------------+-----------------+-----------------+-----------------+
| Domain          | <span class="ap | Optional        | Provided        |
|                 | iname">String</ |                 | through         |
|                 | span>           |                 | [<span class="a |
|                 |                 |                 | piname">RealmCa |
|                 |                 |                 | llback</span>]( |
|                 |                 |                 | https://docs.or |
|                 |                 |                 | acle.com/javase |
|                 |                 |                 | /10/docs/api/ja |
|                 |                 |                 | vax/security/sa |
|                 |                 |                 | sl/RealmCallbac |
|                 |                 |                 | k.html)         |
|                 |                 |                 | with the        |
|                 |                 |                 | <span class="ap |
|                 |                 |                 | iname">serverNa |
|                 |                 |                 | me</span>       |
|                 |                 |                 | input argument  |
|                 |                 |                 | as the default  |
|                 |                 |                 | value.          |
|                 |                 |                 |                 |
|                 |                 |                 | The domain      |
|                 |                 |                 | provided on the |
|                 |                 |                 | client side is  |
|                 |                 |                 | used to create  |
|                 |                 |                 | the Type 1      |
|                 |                 |                 | message. The    |
|                 |                 |                 | negotiated      |
|                 |                 |                 | property        |
|                 |                 |                 | `com.sun.securi |
|                 |                 |                 | ty.sasl.ntlm.do |
|                 |                 |                 | main`{.codeph}  |
|                 |                 |                 | is determined   |
|                 |                 |                 | by the          |
|                 |                 |                 | server\'s Type  |
|                 |                 |                 | 2 message.      |
+-----------------+-----------------+-----------------+-----------------+
| NTLM version    | <span class="ap | Optional        | Specifies a     |
|                 | iname">String</ |                 | specific        |
|                 | span>           |                 | version to use. |
|                 |                 |                 | Provided        |
|                 |                 |                 | through the     |
|                 |                 |                 | `com.sun.securi |
|                 |                 |                 | ty.sasl.ntlm.ve |
|                 |                 |                 | rsion`{.codeph} |
|                 |                 |                 | property. It    |
|                 |                 |                 | can have one of |
|                 |                 |                 | the following   |
|                 |                 |                 | values:         |
|                 |                 |                 |                 |
|                 |                 |                 | -   `LM/NTLM`{. |
|                 |                 |                 | codeph}:        |
|                 |                 |                 |     Original    |
|                 |                 |                 |     NTLM v1     |
|                 |                 |                 | -   `LM`{.codep |
|                 |                 |                 | h}:             |
|                 |                 |                 |     Original    |
|                 |                 |                 |     NTLM v1, LM |
|                 |                 |                 |     only        |
|                 |                 |                 | -   `NTLM`{.cod |
|                 |                 |                 | eph}:           |
|                 |                 |                 |     Original    |
|                 |                 |                 |     NTLM v1,    |
|                 |                 |                 |     NTLM only   |
|                 |                 |                 | -   `NTLM2`{.co |
|                 |                 |                 | deph}:          |
|                 |                 |                 |     NTLM v1     |
|                 |                 |                 |     with Client |
|                 |                 |                 |     Challenge   |
|                 |                 |                 | -   `LMv2/NTLMv |
|                 |                 |                 | 2`{.codeph}:    |
|                 |                 |                 |     NTLM v2     |
|                 |                 |                 | -   `LMv2`{.cod |
|                 |                 |                 | eph}:           |
|                 |                 |                 |     NTLM v2, LM |
|                 |                 |                 |     only        |
|                 |                 |                 | -   `NTLMv2`{.c |
|                 |                 |                 | odeph}:         |
|                 |                 |                 |     NTLM v2,    |
|                 |                 |                 |     NTLM only   |
|                 |                 |                 |                 |
|                 |                 |                 | If not          |
|                 |                 |                 | provided, then  |
|                 |                 |                 | the system      |
|                 |                 |                 | property        |
|                 |                 |                 | <span class="ap |
|                 |                 |                 | iname">ntlm.ver |
|                 |                 |                 | sion</span>     |
|                 |                 |                 | is used. If     |
|                 |                 |                 | still not       |
|                 |                 |                 | provided, then  |
|                 |                 |                 | the value       |
|                 |                 |                 | `LMv2/NTLMv2`{. |
|                 |                 |                 | codeph}         |
|                 |                 |                 | is used, and on |
|                 |                 |                 | the server      |
|                 |                 |                 | side, all       |
|                 |                 |                 | values are      |
|                 |                 |                 | accepted.       |
|                 |                 |                 |                 |
|                 |                 |                 | Note: these     |
|                 |                 |                 | types are only  |
|                 |                 |                 | different on    |
|                 |                 |                 | the client      |
|                 |                 |                 | side. On the    |
|                 |                 |                 | server side,    |
|                 |                 |                 | because         |
|                 |                 |                 | authentication  |
|                 |                 |                 | succeeds if     |
|                 |                 |                 | only one of LM  |
|                 |                 |                 | (or LMv2) or    |
|                 |                 |                 | NTLM (or        |
|                 |                 |                 | NTLMv2) is      |
|                 |                 |                 | verified, the   |
|                 |                 |                 | first three     |
|                 |                 |                 | types are       |
|                 |                 |                 | effectively the |
|                 |                 |                 | same; this is   |
|                 |                 |                 | also true for   |
|                 |                 |                 | the last three  |
|                 |                 |                 | types.          |
+-----------------+-----------------+-----------------+-----------------+
| Host name       | <span class="ap | Optional        | Provided        |
|                 | iname">String</ |                 | through the     |
|                 | span>           |                 | `com.sun.securi |
|                 |                 |                 | ty.sasl.ntlm.ho |
|                 |                 |                 | stname`{.codeph |
|                 |                 |                 | }               |
|                 |                 |                 | property, which |
|                 |                 |                 | will be sent to |
|                 |                 |                 | the server. If  |
|                 |                 |                 | not provided,   |
|                 |                 |                 | then the system |
|                 |                 |                 | will            |
|                 |                 |                 | automatically   |
|                 |                 |                 | derive a host   |
|                 |                 |                 | name. This      |
|                 |                 |                 | property is     |
|                 |                 |                 | only used on    |
|                 |                 |                 | the client      |
|                 |                 |                 | side.           |
+-----------------+-----------------+-----------------+-----------------+
| Random source   | <span class="ap | Optional        | Used as random  |
|                 | iname">java.uti |                 | source to       |
|                 | l.Random</span> |                 | derive nonce    |
|                 |                 |                 | bytes. Provided |
|                 |                 |                 | through the     |
|                 |                 |                 | `com.sun.securi |
|                 |                 |                 | ty.sasl.ntlm.ra |
|                 |                 |                 | ndom`{.codeph}  |
|                 |                 |                 | property. If    |
|                 |                 |                 | not provided,   |
|                 |                 |                 | then an         |
|                 |                 |                 | internal        |
|                 |                 |                 | <span class="ap |
|                 |                 |                 | iname">java.uti |
|                 |                 |                 | l.Random</span> |
|                 |                 |                 | object is used. |
+-----------------+-----------------+-----------------+-----------------+

</div>
<!-- class="inftblhruleinformal" -->

After authentication, the client will receive a negotiated property
named `com.sun.security.sasl.html.domain`{.codeph}, which is provided by
the server, and the server will receive a negotiated property named
`com.sun.security.sasl.ntlm.hostname`{.codeph}, which is he host name
the client used to access this server.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-0D61D8E5-31E8-4F26-9BD2-9AF92F5318F9}

### The SunSASL Provider Server Mechanisms {#JSSEC-GUID-0D61D8E5-31E8-4F26-9BD2-9AF92F5318F9 .sect3}

<div>
The SunSASL provider supports several SASL server mechanisms used in
popular protocols such as LDAP, IMAP, and SMTP.

<div class="section">
The following table summarizes the server mechanisms and the required
input:

<div class="tblformalwide" id="GUID-0D61D8E5-31E8-4F26-9BD2-9AF92F5318F9__GUID-FD50A5C2-E577-4CFC-AF11-5324E08ACA0A">
Table 11-4 Server Mechanisms

+-------------+-------------+-------------+-------------+-------------+
| Server      | Parameters/ | Callbacks   | Configurati | Selection   |
| Mechanism   | Input       |             | on          | Policy      |
| Name        |             |             | Properties  |             |
+:============+:============+:============+:============+:============+
| [CRAM-MD5]( | server name | [<span clas |  None       | [<span clas |
| java-sasl-a |             | s="apiname" |             | s="apiname" |
| pi-programm |             | >AuthorizeC |             | >Sasl.POLIC |
| ing-and-dep |             | allback</sp |             | Y\_NOANONYM |
| loyment-gui |             | an>](https: |             | OUS</span>] |
| de1.html#GUI |             | //docs.orac |             | (https://do |
| D-0D61D8E5- |             | le.com/java |             | cs.oracle.c |
| 31E8-4F26-9 |             | se/10/docs/ |             | om/javase/1 |
| BD2-9AF92F5 |             | api/javax/s |             | 0/docs/api/ |
| 318F9__CRAM |             | ecurity/sas |             | javax/secur |
| -MD5-20E430 |             | l/Authorize |             | ity/sasl/Sa |
| 3C)         |             | Callback.ht |             | sl.html#POL |
|             |             | ml)         |             | ICY_NOANONY |
|             |             |             |             | MOUS)       |
|             |             | [<span clas |             |             |
|             |             | s="apiname" |             | [<span clas |
|             |             | >NameCallba |             | s="apiname" |
|             |             | ck</span>]( |             | >Sasl.POLIC |
|             |             | https://doc |             | Y\_NOPLAINT |
|             |             | s.oracle.co |             | EXT</span>] |
|             |             | m/javase/10 |             | (https://do |
|             |             | /docs/api/j |             | cs.oracle.c |
|             |             | avax/securi |             | om/javase/1 |
|             |             | ty/auth/cal |             | 0/docs/api/ |
|             |             | lback/NameC |             | javax/secur |
|             |             | allback.html |             | ity/sasl/Sa |
|             |             | l)          |             | sl.html#POL |
|             |             |             |             | ICY_NOPLAIN |
|             |             | [<span clas |             | TEXT)       |
|             |             | s="apiname" |             |             |
|             |             | >PasswordCa |             |             |
|             |             | llback</spa |             |             |
|             |             | n>](https:/ |             |             |
|             |             | /docs.oracl |             |             |
|             |             | e.com/javas |             |             |
|             |             | e/10/docs/a |             |             |
|             |             | pi/javax/se |             |             |
|             |             | curity/auth |             |             |
|             |             | /callback/P |             |             |
|             |             | asswordCall |             |             |
|             |             | back.html)  |             |             |
+-------------+-------------+-------------+-------------+-------------+
| [DIGEST-MD5 | protocol id | [<span clas | [<span clas | [<span clas |
| ](java-sasl |             | s="apiname" | s="apiname" | s="apiname" |
| -api-progra | server name | >AuthorizeC | >Sasl.QOP</ | >Sasl.POLIC |
| mming-and-d |             | allback</sp | span>](http | Y\_NOANONYM |
| eployment-g |             | an>](https: | s://docs.or | OUS</span>] |
| uide1.html#G |             | //docs.orac | acle.com/ja | (https://do |
| UID-0D61D8E |             | le.com/java | vase/10/doc | cs.oracle.c |
| 5-31E8-4F26 |             | se/10/docs/ | s/api/javax | om/javase/1 |
| -9BD2-9AF92 |             | api/javax/s | /security/s | 0/docs/api/ |
| F5318F9__DI |             | ecurity/sas | asl/Sasl.ht | javax/secur |
| GEST-MD5-20 |             | l/Authorize | ml#QOP)     | ity/sasl/Sa |
| E43288)     |             | Callback.ht |             | sl.html#POL |
|             |             | ml)         | [<span clas | ICY_NOANONY |
|             |             |             | s="apiname" | MOUS)       |
|             |             | [<span clas | >Sasl.STREN |             |
|             |             | s="apiname" | GTH</span>] | [<span clas |
|             |             | >NameCallba | (https://do | s="apiname" |
|             |             | ck</span>]( | cs.oracle.c | >Sasl.POLIC |
|             |             | https://doc | om/javase/1 | Y\_NOPLAINT |
|             |             | s.oracle.co | 0/docs/api/ | EXT</span>] |
|             |             | m/javase/10 | javax/secur | (https://do |
|             |             | /docs/api/j | ity/sasl/Sa | cs.oracle.c |
|             |             | avax/securi | sl.html#STR | om/javase/1 |
|             |             | ty/auth/cal | ENGTH)      | 0/docs/api/ |
|             |             | lback/NameC |             | javax/secur |
|             |             | allback.html | [<span clas | ity/sasl/Sa |
|             |             | l)          | s="apiname" | sl.html#POL |
|             |             |             | >Sasl.MAX\_ | ICY_NOPLAIN |
|             |             | [<span clas | BUFFER</spa | TEXT)       |
|             |             | s="apiname" | n>](https:/ |             |
|             |             | >PasswordCa | /docs.oracl |             |
|             |             | llback</spa | e.com/javas |             |
|             |             | n>](https:/ | e/10/docs/a |             |
|             |             | /docs.oracl | pi/javax/se |             |
|             |             | e.com/javas | curity/sasl |             |
|             |             | e/10/docs/a | /Sasl.html# |             |
|             |             | pi/javax/se | MAX_BUFFER) |             |
|             |             | curity/auth |             |             |
|             |             | /callback/P | `javax.secu |             |
|             |             | asswordCall | rity.sasl.s |             |
|             |             | back.html)  | endmaxbuffe |             |
|             |             |             | r`{.codeph} |             |
|             |             | [<span clas |             |             |
|             |             | s="apiname" | `com.sun.se |             |
|             |             | >RealmCallb | curity.sasl |             |
|             |             | ack</span>] | .digest.rea |             |
|             |             | (https://do | lm`{.codeph |             |
|             |             | cs.oracle.c | }           |             |
|             |             | om/javase/1 |             |             |
|             |             | 0/docs/api/ | `com.sun.se |             |
|             |             | javax/secur | curity.sasl |             |
|             |             | ity/sasl/Re | .digest.utf |             |
|             |             | almCallback | 8`{.codeph} |             |
|             |             | .html)      |             |             |
+-------------+-------------+-------------+-------------+-------------+
| [NTLM](java | serverName  | [<span clas | [<span clas | [<span clas |
| -sasl-api-p | (as domain, | s="apiname" | s="apiname" | s="apiname" |
| rogramming- | can be      | >RealmCallb | >Sasl.QOP</ | >Sasl.POLIC |
| and-deploym | overridden  | ack</span>] | span>](http | Y\_NOANONYM |
| ent-guide1. | by          | (https://do | s://docs.or | OUS</span>] |
| htm#GUID-68 | properties) | cs.oracle.c | acle.com/ja | (https://do |
| 1CD78D-D2E4 |             | om/javase/1 | vase/10/doc | cs.oracle.c |
| -43DE-9225- |             | 0/docs/api/ | s/api/javax | om/javase/1 |
| 249AA83FF17 |             | javax/secur | /security/s | 0/docs/api/ |
| 7__NTLM-231 |             | ity/sasl/Re | asl/Sasl.ht | javax/secur |
| 9A6BE)      |             | almCallback | ml#QOP)     | ity/sasl/Sa |
|             |             | .html),     |             | sl.html#POL |
|             |             | providing   | `com.sun.se | ICY_NOANONY |
|             |             | request     | curity.sasl | MOUS)       |
|             |             | user\'s     | .ntlm.rando |             |
|             |             | domain      | m`{.codeph} | [<span clas |
|             |             |             |             | s="apiname" |
|             |             | [<span clas | `com.sun.se | >Sasl.POLIC |
|             |             | s="apiname" | curity.sasl | Y\_NOPLAINT |
|             |             | >NameCallba | .ntlm.versi | EXT</span>] |
|             |             | ck</span>]( | on`{.codeph | (https://do |
|             |             | https://doc | }           | cs.oracle.c |
|             |             | s.oracle.co |             | om/javase/1 |
|             |             | m/javase/10 | `com.sun.se | 0/docs/api/ |
|             |             | /docs/api/j | curity.sasl | javax/secur |
|             |             | avax/securi | .ntlm.domai | ity/sasl/Sa |
|             |             | ty/auth/cal | n`{.codeph} | sl.html#POL |
|             |             | lback/NameC |             | ICY_NOPLAIN |
|             |             | allback.html |             | TEXT)       |
|             |             | l),         |             |             |
|             |             | providing   |             |             |
|             |             | request     |             |             |
|             |             | user\'s     |             |             |
|             |             | name        |             |             |
|             |             |             |             |             |
|             |             | [<span clas |             |             |
|             |             | s="apiname" |             |             |
|             |             | >PasswordCa |             |             |
|             |             | llback</spa |             |             |
|             |             | n>](https:/ |             |             |
|             |             | /docs.oracl |             |             |
|             |             | e.com/javas |             |             |
|             |             | e/10/docs/a |             |             |
|             |             | pi/javax/se |             |             |
|             |             | curity/auth |             |             |
|             |             | /callback/P |             |             |
|             |             | asswordCall |             |             |
|             |             | back.html)  |             |             |
+-------------+-------------+-------------+-------------+-------------+

</div>
<!-- class="inftblhruleinformal" -->

An application that uses these mechanisms from the SunSASL provider must
supply the required parameters, callbacks and properties. The properties
have reasonable defaults and only need to be set if the application
wants to override the defaults.

All users of server mechanisms must have a callback handler that deals
with the `AuthorizeCallback`{.codeph}. This is used by the mechanisms to
determine whether the authenticated user is allowed to act on behalf of
the requested authorization id, and also to obtain the canonicalized
name of the authorized user (if canonicalization is applicable).

Most of the parameters, callbacks, and properties are described in the
API documentation. The following sections describe mechanism-specific
behaviors and parameters not already covered by the API documentation.

</div>
<!-- class="section" -->

<div class="section" id="GUID-0D61D8E5-31E8-4F26-9BD2-9AF92F5318F9__CRAM-MD5-20E4303C">
Cram-MD5

The Cram-MD5 server mechanism uses the `NameCallback`{.codeph} and
`PasswordCallback`{.codeph} to obtain the password required to verify
the SASL client\'s response. The callback handler should use the
`NameCallback.getDefaultName()`{.codeph} as the key to fetch the
password.

</div>
<!-- class="section" -->

<div class="section" id="GUID-0D61D8E5-31E8-4F26-9BD2-9AF92F5318F9__DIGEST-MD5-20E43288">
Digest-MD5

The Digest-MD5 server mechanism uses the `RealmCallback`{.codeph},
`NameCallback`{.codeph}, and `PasswordCallback`{.codeph} to obtain the
password required to verify the SASL client\'s response. The callback
handler should use `RealmCallback.getDefaultText()`{.codeph} and
`NameCallback.getDefaultName()`{.codeph} as keys to fetch the password.

The `javax.security.sasl.sendmaxbuffer`{.codeph} property specifies (the
string representation of) the maximum send buffer size in bytes. The
default is 65536. The actual maximum number of bytes will be the minimum
of this number and the peer\'s maximum receive buffer size.

The `com.sun.security.sasl.digest.realm`{.codeph} property is used to
specify a list of space-separated realm names that the server supports.
The list is sent to the client as part of the challenge. If this
property has not been set, the default realm is the server\'s name
(supplied as a parameter).

The c`om.sun.security.sasl.digest.utf8`{.codeph} property is used to
specify the character encoding to use. The value `true`{.codeph} means
to use UTF-8 encoding; the value `false`{.codeph} means to use ISO Latin
1 (ISO-8859-1). The default value is `true`{.codeph}.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-B6A1E089-0C59-413F-ABF6-E73F44F89E6A}

The JdkSASL Provider {#JSSEC-GUID-B6A1E089-0C59-413F-ABF6-E73F44F89E6A .sect2}
--------------------

<div>
<div class="section">
The JdkSASL provider supports the following client and server
mechanisms:

-   Client Mechanisms
    -   GSSAPI ([RFC 2222](http://www.ietf.org/rfc/rfc2222.txt)). This
        mechanism uses the [GSSAPI](http://www.ietf.org/rfc/rfc2078.txt)
        for obtaining authentication information. It supports Kerberos
        v5 authentication.
-   Server Mechanisms
    -   GSSAPI (Kerberos v5)

</div>
<!-- class="section" -->

</div>
<div class="sect3">
[]{#GUID-6B2412AB-D5BC-4C8A-9DA7-515E32DDE971}

### The JdkSASL Provider Client Mechanism {#JSSEC-GUID-6B2412AB-D5BC-4C8A-9DA7-515E32DDE971 .sect3}

<div>
The JdkSASL provider supports the GSSAPI client mechanism used in
popular protocols such as LDAP, IMAP, and SMTP.

<div class="section">
The following table summarizes the GSSAPI client mechanism and its
required input.

<div class="tblformalwide" id="GUID-6B2412AB-D5BC-4C8A-9DA7-515E32DDE971__GUID-1D69316D-2076-406F-B36F-A36E7FF429FA">
Table 11-5 JdkSASL Provider Client Mechanism

+-------------+-------------+-------------+-------------+-------------+
| Client      | Parameters/ | Callbacks   | Configurati | Selection   |
| Mechanism   | Input       |             | on          | Policy      |
| Name        |             |             | Properties  |             |
+:============+:============+:============+:============+:============+
| [GSSAPI](ja | JAAS Subjec |  None       | [<span clas | [<span clas |
| va-sasl-api | t           |             | s="apiname" | s="apiname" |
| -programmin |             |             | >Sasl.QOP</ | >Sasl.POLIC |
| g-and-deplo | authorizati |             | span>](http | Y\_NOACTIVE |
| yment-guide | on id       |             | s://docs.or | </span>](ht |
| 1.html#GUID- |             |             | acle.com/ja | tps://docs. |
| 6B2412AB-D5 | protocol id |             | vase/10/doc | oracle.com/ |
| BC-4C8A-9DA |             |             | s/api/javax | javase/10/d |
| 7-515E32DDE | server name |             | /security/s | ocs/api/jav |
| 971__GSSAPI |             |             | asl/Sasl.ht | ax/security |
| -20E4086B)  |             |             | ml#QOP)     | /sasl/Sasl. |
|             |             |             |             | html#POLICY |
|             |             |             | [<span clas | _NOACTIVE)  |
|             |             |             | s="apiname" |             |
|             |             |             | >Sasl.MAX\_ | [<span clas |
|             |             |             | BUFFER</spa | s="apiname" |
|             |             |             | n>](https:/ | >Sasl.POLIC |
|             |             |             | /docs.oracl | Y\_NOANONYM |
|             |             |             | e.com/javas | OUS</span>] |
|             |             |             | e/10/docs/a | (https://do |
|             |             |             | pi/javax/se | cs.oracle.c |
|             |             |             | curity/sasl | om/javase/1 |
|             |             |             | /Sasl.html# | 0/docs/api/ |
|             |             |             | MAX_BUFFER) | javax/secur |
|             |             |             |             | ity/sasl/Sa |
|             |             |             | [<span clas | sl.html#POL |
|             |             |             | s="apiname" | ICY_NOANONY |
|             |             |             | >Sasl.SERVE | MOUS)       |
|             |             |             | R\_AUTH</sp |             |
|             |             |             | an>](https: | [<span clas |
|             |             |             | //docs.orac | s="apiname" |
|             |             |             | le.com/java | >Sasl.POLIC |
|             |             |             | se/10/docs/ | Y\_NOPLAINT |
|             |             |             | api/javax/s | EXT</span>] |
|             |             |             | ecurity/sas | (https://do |
|             |             |             | l/Sasl.html | cs.oracle.c |
|             |             |             | #SERVER_AUT | om/javase/1 |
|             |             |             | H)          | 0/docs/api/ |
|             |             |             |             | javax/secur |
|             |             |             | `javax.secu | ity/sasl/Sa |
|             |             |             | rity.sasl.s | sl.html#POL |
|             |             |             | endmaxbuffe | ICY_NOPLAIN |
|             |             |             | r`{.codeph} | TEXT)       |
+-------------+-------------+-------------+-------------+-------------+

</div>
<!-- class="inftblhruleinformal" -->

An application that uses the GSSAPI mechanism from the JdkSASL provider
must supply the required parameters, callbacks and properties. The
properties have reasonable defaults and only need to be set if the
application wants to override the defaults. Most of the parameters,
callbacks, and properties are described in the API documentation. The
following section describes further GSSAPI behaviors and parameters not
already covered by the API documentation.

</div>
<!-- class="section" -->

<div class="section" id="GUID-6B2412AB-D5BC-4C8A-9DA7-515E32DDE971__GSSAPI-20E4086B">
GSSAPI

<div class="infoboxnote" id="GUID-6B2412AB-D5BC-4C8A-9DA7-515E32DDE971__GUID-1B681CA8-3E44-42D6-8391-D6BEA10FB863">
Note:

The GSSAPI server mechanism has the same requirements as the GSSAPI
client mechanism in terms of Kerberos credentials and the
<span class="apiname">javax.security.sasl.sendmaxbuffer</span> property.

</div>
The GSSAPI mechanism is used for Kerberos v5 authentication and optional
establishment of a security layer. The mechanism expects the calling
thread\'s `Subject`{.codeph} to contain the client\'s Kerberos
credentials or that the credentials could be obtained by implicitly
logging in to Kerberos. To obtain the client\'s Kerberos credentials,
use the Java Authentication and Authorization Service (JAAS) to log in
using the Kerberos login module. See [Introduction to JAAS and Java
GSS-API
Tutorials](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/index.html)
in the JDK 8 documentation for details and examples. After using JAAS
authentication to obtain the Kerberos credentials, you put the code that
uses the SASL GSSAPI mechanism within `doAs`{.codeph} or
`doAsPrivileged`{.codeph}.

``` {.codeblock dir="ltr"}
LoginContext lc = new LoginContext("JaasSample", new TextCallbackHandler());
lc.login();
lc.getSubject().doAs(new SaslAction());

class SaslAction implements java.security.PrivilegedAction<Void> {
   public Void run() {
       // ...
       String[] mechanisms = new String[]{"GSSAPI"};
       SaslClient sc = Sasl.createSaslClient(
           mechanisms, authzid, protocol, serverName, props, callbackHandler);
       // ...
   }
}
```

To obtain Kerberos credentials without doing explicit JAAS programming,
see [Use of Java GSS-API for Secure Message Exchanges Without JAAS
Programming](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/BasicClientServer.html)
in the JDK 8 documentation. When using this approach, there is no need
to wrap the code within `doAs`{.codeph} or `doAsPrivileged`{.codeph}

The `javax.security.sasl.sendmaxbuffer`{.codeph} property specifies (the
string representation of) the maximum send buffer size in bytes. The
default is 65536. The actual maximum number of bytes will be the minimum
of this number and the peer\'s maximum receive buffer size.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-F815A77D-744E-4914-9963-886A1B10FC3C}

### The JdkSASL Provider Server Mechanism {#JSSEC-GUID-F815A77D-744E-4914-9963-886A1B10FC3C .sect3}

<div>
The JdkSASL provider supports the GSSAPI mechanism used in popular
protocols such as LDAP, IMAP, and SMTP.

<div class="section">
The following table summarizes the GSSAPI server mechanism and the
required input:

<div class="tblformalwide" id="GUID-F815A77D-744E-4914-9963-886A1B10FC3C__GUID-FD50A5C2-E577-4CFC-AF11-5324E08ACA0A">
Table 11-6 Server mechanism

+-------------+-------------+-------------+-------------+-------------+
| Server      | Parameters/ | Callbacks   | Configurati | Selection   |
| Mechanism   | Input       |             | on          | Policy      |
| Name        |             |             | Properties  |             |
+:============+:============+:============+:============+:============+
| [GSSAPI](ja | [<span clas | [<span clas | [<span clas | [<span clas |
| va-sasl-api | s="apiname" | s="apiname" | s="apiname" | s="apiname" |
| -programmin | >Subject</s | >AuthorizeC | >Sasl.QOP</ | >Sasl.POLIC |
| g-and-deplo | pan>](https | allback</sp | span>](http | Y\_NOACTIVE |
| yment-guide | ://docs.ora | an>](https: | s://docs.or | </span>](ht |
| 1.html#GUID- | cle.com/jav | //docs.orac | acle.com/ja | tps://docs. |
| 6B2412AB-D5 | ase/10/docs | le.com/java | vase/10/doc | oracle.com/ |
| BC-4C8A-9DA | /api/javax/ | se/10/docs/ | s/api/javax | javase/10/d |
| 7-515E32DDE | security/au | api/javax/s | /security/s | ocs/api/jav |
| 971__GSSAPI | th/Subject. | ecurity/sas | asl/Sasl.ht | ax/security |
| -20E4086B)  | html)       | l/Authorize | ml#QOP)     | /sasl/Sasl. |
|             |             | Callback.ht |             | html#POLICY |
|             | protocol id | ml)         | [<span clas | _NOACTIVE)  |
|             |             |             | s="apiname" |             |
|             | server name |             | >Sasl.MAX\_ | [<span clas |
|             |             |             | BUFFER</spa | s="apiname" |
|             |             |             | n>](https:/ | >Sasl.POLIC |
|             |             |             | /docs.oracl | Y\_NOANONYM |
|             |             |             | e.com/javas | OUS</span>] |
|             |             |             | e/10/docs/a | (https://do |
|             |             |             | pi/javax/se | cs.oracle.c |
|             |             |             | curity/sasl | om/javase/1 |
|             |             |             | /Sasl.html# | 0/docs/api/ |
|             |             |             | MAX_BUFFER) | javax/secur |
|             |             |             |             | ity/sasl/Sa |
|             |             |             | `javax.secu | sl.html#POL |
|             |             |             | rity.sasl.s | ICY_NOANONY |
|             |             |             | endmaxbuffe | MOUS)       |
|             |             |             | r`{.codeph} |             |
|             |             |             |             | [<span clas |
|             |             |             |             | s="apiname" |
|             |             |             |             | >Sasl.POLIC |
|             |             |             |             | Y\_NOPLAINT |
|             |             |             |             | EXT</span>] |
|             |             |             |             | (https://do |
|             |             |             |             | cs.oracle.c |
|             |             |             |             | om/javase/1 |
|             |             |             |             | 0/docs/api/ |
|             |             |             |             | javax/secur |
|             |             |             |             | ity/sasl/Sa |
|             |             |             |             | sl.html#POL |
|             |             |             |             | ICY_NOPLAIN |
|             |             |             |             | TEXT)       |
+-------------+-------------+-------------+-------------+-------------+

</div>
<!-- class="inftblhruleinformal" -->

An application that uses the GSSAPI mechanism from the JdkSASL provider
must supply the required parameters, callbacks and properties. The
properties have reasonable defaults and only need to be set if the
application wants to override the defaults.

All users of server mechanism must have a callback handler that deals
with the `AuthorizeCallback`{.codeph}. This is used by the mechanism to
determine whether the authenticated user is allowed to act on behalf of
the requested authorization id, and also to obtain the canonicalized
name of the authorized user (if canonicalization is applicable).

Most of the parameters, callbacks, and properties are described in the
API documentation.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-10BCFA2D-E33C-4A11-BDD4-012B5713F430}

Debugging and Monitoring {#JSSEC-GUID-10BCFA2D-E33C-4A11-BDD4-012B5713F430 .sect2}
------------------------

<div>
<div class="section">
The SunSASL and JdkSASL providers uses the Logging APIs to provide
implementation logging output. This output can be controlled by using
the logging configuration file and programmatic API
([<span class="apiname">java.util.logging</span>](https://docs.oracle.com/javase/10/docs/api/java/util/logging/package-summary.html)).
The logger name used by the SunSASL provider is
`javax.security.sasl`{.codeph}. Here is a sample logging configuration
file that enables the `FINEST`{.codeph} logging level for the SunSASL
provider:

``` {.codeblock dir="ltr"}
javax.security.sasl.level=FINEST
handlers=java.util.logging.ConsoleHandler
java.util.logging.ConsoleHandler.level=FINEST
```

The table below shows the mechanisms and the logging output that they
generate:

<div class="tblformalwide" id="GUID-10BCFA2D-E33C-4A11-BDD4-012B5713F430__GUID-767DB7F7-241D-465E-AEFC-D91959675CEE">
Table 11-7 Logging Output

  Mechanism    Logging Level                                                                                                          Information Logged
  ------------ ---------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------
  CRAM-MD5     [<span class="apiname">FINE</span>](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Level.html#FINE)       Configuration properties; challenge/response messages
  DIGEST-MD5   [<span class="apiname">INFO</span>](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Level.html#INFO)       Message discarded due to encoding problem (for example, unmatched MACs, incorrect padding)
  DIGEST-MD5   [<span class="apiname">FINE</span>](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Level.html#FINE)       Configuration properties; challenge/response messages
  DIGEST-MD5   [<span class="apiname">FINER</span>](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Level.html#FINER)     More detailed information about challenge/response messages
  DIGEST-MD5   [<span class="apiname">FINEST</span>](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Level.html#FINEST)   Buffers exchanged at the security layer
  GSSAPI       [<span class="apiname">FINE</span>](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Level.html#FINE)       Configuration properties; challenge/response messages
  GSSAPI       [<span class="apiname">FINER</span>](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Level.html#FINER)     More detailed information about challenge/response messages
  GSSAPI       [<span class="apiname">FINEST</span>](https://docs.oracle.com/javase/8/docs/api/java/util/logging/Level.html#FINEST)   Buffers exchanged at the security layer

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-A21D50AD-3730-4FE6-A13B-75529607E068}

Implementing a SASL Security Provider {#JSSEC-GUID-A21D50AD-3730-4FE6-A13B-75529607E068 .sect2}
-------------------------------------

<div>
<div class="section">
There are three basic steps in implementing a SASL security provider:

</div>
<!-- class="section" -->

1.  <span>Write a class that implements the `SaslClient`{.codeph} or
    `SaslServer`{.codeph} interface.</span>

    <div>
    This involves providing an implementation for the SASL mechanism. To
    implement a client mechanism, you need to implement the methods
    declared in the `SaslClient`{.codeph} interface. Similarly, for a
    server mechanism, you need to implement the methods declared in the
    `SaslServer`{.codeph} interface. For the purposes of this
    discussion, suppose you are developing an implementation for the
    client mechanism \"SAMPLE-MECH\", implemented by the class,
    `com.example.SampleMechClient`{.codeph}. You must decide what input
    are needed by the mechanism and how the implementation is going to
    collect them. For example, if the mechanism is
    username/password-based, then the implementation would likely need
    to collect that information via the callback handler parameter.

    </div>
2.  <span>Write a factory class (that implements
    `SaslClientFactory`{.codeph} or `SaslServerFactory`{.codeph}) that
    creates instances of the class.</span>

    <div>
    This involves providing a factory class that will create instances
    of `com.example.SampleMechClient`{.codeph}. The factory needs to
    determine the characteristics of the mechanism that it supports (as
    described by the ` Sasl.POLICY_*`{.codeph} properties) so that it
    can return an instance of the mechanism when the API user requests
    it using compatible policy properties. The factory may also check
    for validity of the parameters before creating the mechanism. For
    the purposes of this discussion, suppose the factory class is named
    `com.example.MySampleClientFactory`{.codeph}. Although our sample
    factory is responsible for only one mechanism, a single factory can
    be responsible for any number of mechanisms.

    </div>
3.  <span>Write a JCA provider that registers the factory.</span>

    <div>
    This involves creating a JCA provider. The steps for creating a JCA
    provider is described in detail in [Steps to Implement and Integrate
    a
    Provider](howtoimplaprovider.html#GUID-CC161921-EBD2-48C6-B543-A956658B68B6 "Follow these steps to implement a provider and integrate it into the JCA framework:").
    SASL client factories are registered using property names of the
    form
    `SaslClientFactory.`{.codeph}<span class="italic">mechName</span>
    while SASL server factories are registered using property names of
    the form
    `SaslServerFactory.`{.codeph}<span class="italic">mechName</span>

    <span class="italic">mechName</span> is the SASL mechanism\'s name.
    This is what\'s returned by `SaslClient.getMechanismName()`{.codeph}
    and `SaslServer.getMechanismName()`{.codeph}. Continuing with our
    example, here is how the provider would register the \"SAMPLE-MECH\"
    mechanism.

    ``` {.codeblock dir="ltr"}
        put("SaslClientFactory.SAMPLE-MECH", "com.example.MySampleClientFactory");
    ```

    A single SASL provider might be responsible for many mechanisms.
    Therefore, it might have many invocations of `put`{.codeph} to
    register the relevant factories. The completed SASL provider can
    then be made available to applications using the instructions
    described in [How SASL Mechanisms are Installed and
    Selected](java-sasl-api-programming-and-deployment-guide1.html#GUID-93982F1C-AFFE-47B9-B4BA-41551ECCE2D2 "SASL mechanism implementations are provided by SASL security providers. Each provider may support one or more SASL mechanisms and is registered with the JCA.").

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
| ----------- -------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| --- --               | L |             <span cl |
|               [![Pre | o | ass="icon">Contents< |
| vious](../../dcommon | g | /span>](toc.htm)     |
| /gifs/leftnav.gif)\  | o |   -- --------------- |
|                      | ] | -------------------- |
|                 [![N | ( | -------------------- |
| ext](../../dcommon/g | . | ---                  |
| ifs/rightnav.gif)\   | . |                      |
|                      | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](j | / |                      |
| ava-pki-programmers- | d |                      |
| guide.htm)   <span c | c |                      |
| lass="icon">Next</sp | o |                      |
| an>](java-xml-digita | m |                      |
| l-signature-api-over | m |                      |
| view-and-tutorial.ht | o |                      |
| m)                   | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| ----------- -------- | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| --- --               | a |                      |
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
