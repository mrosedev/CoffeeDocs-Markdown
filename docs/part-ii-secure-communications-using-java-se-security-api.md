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

  -------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------ --
                                           [![Previous](../../dcommon/gifs/leftnav.gif)\                                                                   [![Next](../../dcommon/gifs/rightnav.gif)\                         
   <span class="icon">Previous</span>](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm)   <span class="icon">Next</span>](part-iii-deploying-single-sign-kerberos-environment.htm)  
  -------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------ --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-98B02DB0-13DB-4175-9485-3449E1A241B5}<!-- End Header -->

Part II : Secure Communications using the Java SE Security API {#JSSEC-GUID-98B02DB0-13DB-4175-9485-3449E1A241B5 .sect1}
==============================================================

<div>
This part shows you how to build applications that perform secure
communications. The Java SE platform provides three standard APIs that
allow applications to perform secure communications: The Java Generic
Security Service (GSS), the Java SASL API, and the Java Secure Socket
Extension (JSSE). When building an application, which of these APIs
should you use? The answer depends on many factors, including
requirements of the protocol or service, deployment infrastructure, and
integration with other security services. For example, if you are
building an LDAP client library, you would need to use the Java SASL API
because use of SASL is part of LDAP\'s protocol definition. As an other
example, if the service supports SSL, then the client application
attempting to access the service would need to use JSSE.

</div>
<div class="sect2">
[]{#GUID-1E4E43BA-EC38-435E-A426-7A88E52F34DF}

Exercise 3: Using the Java Generic Security Service (GSS) API {#JSSEC-GUID-1E4E43BA-EC38-435E-A426-7A88E52F34DF .sect2}
-------------------------------------------------------------

<div>
<div class="section">
Goal of This Exercise

The goal of this exercise is to learn how to use the Java GSS API  to
perform secure authentication and communication.

</div>
<!-- class="section" -->

<div class="section">
Background for This Exercise

The Generic Security Service API provides a uniform C-language interface
to access various security services, such as authentication, message
integrity, and message confidentiality. The Java GSS API provides the
corresponding interface for Java applications.  It allows applications
to perform authentication and establish secure communication with the
peer. One of the most common security service accessed via the GSS-API
and Java GSS-API is Kerberos.

</div>
<!-- class="section" -->

<div class="section">
Resources for This Exercise

-   [Introduction to JAAS and Java GSS-API
    Tutorials](introduction-jaas-and-java-gss-api-tutorials1.htm)
-   [Generic Security Service API Version 2: Java Bindings
    (RFC 2853)](http://www.ietf.org/rfc/rfc2853.txt)
-   Java GSS Javadoc API documentation:
    [<span class="apiname">org.ietf.jgss</span>](https://docs.oracle.com/javase/10/docs/api/org/ietf/jgss/package-summary.html).

</div>
<!-- class="section" -->

<div class="section">
Overview of This Exercise

This exercise is a client-server application that demonstrates how to
communicate securely using the Java GSS API. The client and server parts
first authenticate to Kerberos, as shown in [Exercise 1: Using the JAAS
API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
This stores the credentials in the subject. The application then
executes an action that performs Java GSS operations (with Kerberos as
the underlying GSS mechanism) inside of a
<span class="apiname">Subject.doAs</span> using the subject. The Java
GSS Kerberos mechanism, because it is executing inside the
<span class="apiname">doAs</span>, obtains the Kerberos credentials from
the subject, and uses them to authenticate with the peer and to exchange
messages securely.

</div>
<!-- class="section" -->

<div class="section">
Steps to Follow

1.  Read the
    [`GssServer.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__GSSSERVER.JAVA-338B6349)
    code.

    This code fragment defines the action to execute after the service
    principal has authenticated to the KDC. It replaces the
    `MyAction`{.codeph} in [Exercise 1: Using the JAAS
    API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
    The code first creates an instance of
    <span class="bold"><span class="apiname">GSSManager</span></span>,
    which it uses to obtain its own credentials and to create an
    instance of <span class="apiname">GSSContext</span>. It uses this
    context to perform authentication. Upon completing authentication,
    it accepts encrypted input from the client and uses the established
    security context to decrypt the data. It then uses the security
    context to encrypt a reply containing the original input and the
    date, and then sends it back to the client.

2.  Compile the sample code.

3.  Read the
    [`GssClient.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__GSSCLIENT.JAVA-338B6631)
    code.

    This code fragment defines the action to execute after the client
    principal has authenticated to the KDC. It replaces the
    `MyAction`{.codeph} in [Exercise 1: Using the JAAS
    API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
    The code first creates an instance of
    <span class="bold"><span class="apiname">GSSManager</span></span>,
    which it uses to obtain a principal name for the service that it is
    going to communicate with. It then creates an instance of
    <span class="apiname">GSSContext</span> to perform authentication
    with the service. Upon completing authentication, it uses the
    established security context to encrypt a message, and sends it to
    the server. It then reads an encrypted message from the server and
    decodes it using the established security context.

4.  Compile the sample code.

5.  Launch a new window and start the server:

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf GssServer
    ```

6.  Run the client application. <span class="apiname">GssClient</span>
    takes two parameters: the service name and the name of the server
    that the service is running on. For example, if the service is host
    running on the machine j1hol-001, you would enter the following:

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf GssClient host j1hol-001
    ```

    When prompted for the password, enter `change_it`{.codeph}.

7.  Observe the following output in the respective client and server
    applications\' windows.

    Output for running <span class="apiname">GssServer</span> example:

    ``` {.oac_no_warn dir="ltr"}
    Authenticated principal: [host/j1hol-001@J1LABS.EXAMPLE.COM]
    Waiting for incoming connections..
    Got connection from client /192.0.2.102
    Context Established!
    Client principal is test@J1LABS.EXAMPLE.COM
    Server principal is host/j1hol-001@J1LABS.EXAMPLE.COM
    Mutual authentication took place!
    Received data "Hello There!" of length 12
    Confidentiality applied: true
    Sending: Hello There! Thu May 06 12:11:15 PDT 2005
    ```

    Output for running <span class="apiname">GssClient</span> example:

    ``` {.oac_no_warn dir="ltr"}
    Kerberos password for test: change_it
    Authenticated principal: [test@J1LABS.EXAMPLE.COM]
    Connected to address j1hol-001/192.0.2.102
    Context Established!
    Client principal is test@J1LABS.EXAMPLE.COM
    Server principal is host@j1hol-001
    Mutual authentication took place!
    Sending message: Hello There!
    Will read token of size 93
    Received message: Hello There! Thu May 06 12:11:15 PDT 2005
    ```

</div>
<!-- class="section" -->

<div class="section">
Summary

In this exercise, you learned how to write a client-server application
that uses the Java GSS API to authenticate and communicate securely with
each other.

</div>
<!-- class="section" -->

<div class="section">
Next Steps

1.  Proceed to [Exercise 4: Using the Java SASL
    API](part-ii-secure-communications-using-java-se-security-api.htm#GUID-727C5CDB-8701-40B3-8355-00C8314590A3)
    to learn how to write a client/server application that uses the Java
    SASL API to authenticate and communicate securely with each other.

2.  Proceed to [Exercise 5: Using the Java Secure Socket Extension with
    Kerberos](part-ii-secure-communications-using-java-se-security-api.htm#GUID-9AAFC7BB-8562-4E3E-B5EF-E33F30E779D1)
    to learn how to write a client/server application that uses the JSSE
    to authenticate and communicate securely with each other.

3.  Proceed to [Exercise 6: Deploying for Single
    Sign-On](part-iii-deploying-single-sign-kerberos-environment.htm#GUID-5D0B8FD9-FF12-44E7-B7E9-7620E95E784C)
    to learn how to configure the sample programs that you have just
    used to achieve single sign-on in a Kerberos environment.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-727C5CDB-8701-40B3-8355-00C8314590A3}

Exercise 4: Using the Java SASL API {#JSSEC-GUID-727C5CDB-8701-40B3-8355-00C8314590A3 .sect2}
-----------------------------------

<div>
<div class="section">
Goal of This Exercise

The goal of this exercise is to learn how to use the Java SASL API  to
perform secure authentication and communication.

</div>
<!-- class="section" -->

<div class="section">
Background for This Exercise

Simple Authentication and Security Layer (SASL) specifies a
challenge-response protocol in which data is exchanged between the
client and the server for the purposes of authentication and (optional)
establishment of a security layer on which to carry on subsequent
communications. SASL allows different mechanisms to be used; each such
mechanism is identified by a profile that defines the data to be
exchanged and a name. SASL is used with connection-based protocols such
as LDAPv3 and IMAPv4. SASL is described in [RFC
4422](http://www.ietf.org/rfc/rfc4422.txt).

The Java SASL API defines an API for applications to use SASL in a
mechanism-independent way. For example, if you are writing a library for
a networking protocol that uses SASL, you can use the Java SASL API to
generate the data to be exchanged with the peer. When the library is
deployed, you can dynamically configure the mechanisms to use with the
library.

In addition to authentication, you can use SASL to negotiate a security
layer to be used after authentication. But unlike the GSS-API, the
properties of the security layer (such as whether you want integrity or
confidentiality) is decided at negotiation time. (the GSS-API allows
confidentiality to be turned on or off per message).

</div>
<!-- class="section" -->

<div class="section">
Resources for This Exercise

-   [Java SASL API Programming and Deployment
    Guide](java-sasl-api-programming-and-deployment-guide1.htm#GUID-6D78EE33-62E6-4D85-9695-322EED493F72)
-   [ <span class="apiname">javax.security.sasl</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/sasl/package-summary.html)
-   [Simple Authentication and Security Layer (SASL)
    (RFC 4422)](http://www.ietf.org/rfc/rfc4422.txt)

</div>
<!-- class="section" -->

<div class="section">
Overview of This Exercise

This exercise is a client-server application that demonstrates how to
communicate securely using the Java SASL API. The client and server
parts first authenticate to Kerberos using [Exercise 1: Using the JAAS
API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
This stores the credentials in the subject. The application then
executes an action that performs Java SASL API operations (with Kerberos
as the underlying SASL mechanism) inside of a
<span class="apiname">Subject.doAs</span> using the subject. The
SASL/Kerberos mechanism, because it is executing inside the
<span class="apiname">doAs</span>, obtains the Kerberos credentials from
the subject, and uses them to authenticate with the peer and to exchange
messages securely.

This example uses a simple protocol implemented by the
[`AppConnection`{.codeph}](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__APPCONNECTION.JAVA-338B5FD0)
class. This protocol exchanges authentication commands and data
commands. Each command consists of a type (e.g.,
`AppConnection.AUTH_CMD`{.codeph}), the length of the data to follow,
and the data itself. The data is a SASL buffer if it is for
authentication or encrypted/integrity-protected application data; it is
plain application data otherwise.

</div>
<!-- class="section" -->

<div class="section">
Steps to Follow

1.  Read the
    [`SaslTestServer.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__SASLTESTSERVER.JAVA-338B69BC)
    sample code.

    This code fragment defines the action to execute after the service
    principal has authenticated to the KDC. It replaces the
    `MyAction`{.codeph} in [Exercise 1: Using the JAAS
    API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
    The server specifies the quality of protections (QOP) that it will
    support and then creates an instance of
    <span class="apiname">SaslServer</span> to perform the
    authentication. The challenge-response protocol of SASL is performed
    in the while loop, with the server sending challenges to the client
    and processing the responses from the client. After authentication,
    the identity of the authenticated client can be obtained via a call
    to the <span class="apiname">getAuthorizedID()</span> method. If a
    security layer was negotiated, the server can exchange data securely
    with the client.

2.  Compile the sample code.

3.  Read the
    [`SaslTestClient.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__SASLTESTCLIENT.JAVA-338B6D11)
    sample code.

    This code fragment defines the action to execute after the client
    principal has authenticated to the KDC. It replaces the MyAction in
    [Exercise 1: Using the JAAS
    API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
    The program first specifies the quality of protections that it wants
    (in this case, confidentiality) and then creates an instance of
    `SaslClient`{.codeph} to use for authentication. It then checks
    whether the mechanism has an initial response and if so, gets the
    response by invoking the `evaluateChallenge()`{.codeph} method with
    an empty byte array. It then sends the response to the server to
    begin the authentication. The challenge-response protocol of SASL is
    performed in the while loop, with the client evaluating the
    challenges that it gets from the server and sending the server the
    corresponding responses to the challenges. After authentication, the
    client can proceed to communicate with the server using the
    negotiated security layer.

4.  Compile the sample code.

5.  Launch a new window and start the server. `SaslTestServer`{.codeph}
    takes two parameters: the service name and the name of the server
    that the service is running on. For example, if the service is host
    running on the machine j1hol-001, you would enter the following:

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf SaslTestServer host j1hol-001
    ```

6.  Run the client application. `SaslTestClient`{.codeph} takes two
    parameters: the service name and the name of the server that the
    service is running on. For example, if the service is host running
    on the machine j1hol-001, you would enter the following:

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf SaslTestClient host j1hol-001
    ```

    Provide a secure password.

7.  Observe the following output in the respective client and server
    applications\' windows.

    Output for running the `SaslTestServer`{.codeph} example:

    ``` {.oac_no_warn dir="ltr"}
    Authenticated principal: [host/j1hol-001@J1LABS.EXAMPLE.COM]
    Waiting for incoming connections...
    Got connection from client /192.0.2.102
    Client authenticated; authorized client is: test@J1LABS.EXAMPLE.COM
    Negotiated QOP: auth-conf
    Received: Hello There!
    Sending: Hello There! Fri May 07 15:32:37 PDT 2005
    Received data "Hello There!" of length 12
    ```

    Output for running the `SaslTestClient`{.codeph} example
    (<span class="italic">password</span> will be replaced by the
    password that you provided):

    ``` {.oac_no_warn dir="ltr"}
    Kerberos password for test: password
    Authenticated principal: [test@J1LABS.EXAMPLE.COM]
    Connected to address j1hol-001/192.0.2.102
    Client authenticated.
    Negotiated QOP: auth-conf
    Sending: Hello There!
    Received: Hello There! Fri May 07 15:32:37 PDT 2005
    ```

</div>
<!-- class="section" -->

<div class="section">
Summary

In this exercise, you learned how to write a client-server application
that uses the Java SASL API to authenticate and communicate securely
with each other.

</div>
<!-- class="section" -->

<div class="section">
Next Steps

1.  Proceed to [Exercise 5: Using the Java Secure Socket Extension with
    Kerberos](part-ii-secure-communications-using-java-se-security-api.htm#GUID-9AAFC7BB-8562-4E3E-B5EF-E33F30E779D1)
    to learn how to write a client/server application that uses the JSSE
    to authenticate and communicate securely with each other.

2.  Proceed to [Exercise 6: Deploying for Single
    Sign-On](part-iii-deploying-single-sign-kerberos-environment.htm#GUID-5D0B8FD9-FF12-44E7-B7E9-7620E95E784C)
    to learn how to configure the sample programs that you have just
    used to achieve single sign-on in a Kerberos environment.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-9AAFC7BB-8562-4E3E-B5EF-E33F30E779D1}

Exercise 5: Using the Java Secure Socket Extension with Kerberos {#JSSEC-GUID-9AAFC7BB-8562-4E3E-B5EF-E33F30E779D1 .sect2}
----------------------------------------------------------------

<div>
<div class="section">
Goal of This Exercise

The goal of this exercise is to learn how to use the JSSE API to perform
secure authentication and communication using Kerberos cipher suites.

</div>
<!-- class="section" -->

<div class="section">
Background for This Exercise

Secure Socket Layer (SSL) and Transport Layer Security (TLS) are the
most widely used protocols for implementing cryptography on the
Internet. TLS is the Internet standard evolved from SSL. SSL/TLS
provides application-level protocols (such as HTTP and LDAP) with secure
authentication and communication. For example, HTTPS is the resulting
protocol of using HTTP over SSL/TLS. SSL/TLS is used not only for
standard protocols such as HTTP, it is also widely used when building
custom applications using custom protocols that need to communicate
securely.

SSL/TLS traditionally used certificate-based authentication and is
commonly used for server-authentication. For example, when a Web client
such as a browser accesses a secure Web site (server) on behalf of a
user, the server sends its certificate to the browser so that the
browser can verify the identity of the server. This ensures that the
user does not divulge confidential information (such as credit card
information) to a bogus server. Recently, a new standard allows the use
of Kerberos with TLS. This means instead of using certificate-based
authentication, an application can use Kerberos credentials and take
advantage of the Kerberos infrastructure in the deployment environment.
Using Kerberos cipher suites also provides automatic support for mutual
authentication in which the client is also authenticated in addition to
the server.

The decision of whether to use Java GSS, Java SASL, or JSSE for a
particular application often depends upon several factors, including
(the protocols being used by) the services with which the application
interacts, the deployment environment (PKI or Kerberos-based), and the
application\'s security requirements. JSSE provides a secure end-to-end
channel that takes care of the I/O and transport, while Java GSS and
Java SASL provide encryption and integrity-protection on the data, but
the application is responsible for transporting the secured data to its
peer. Some details about factors for deciding when to use JSSE versus
Java GSS are presented in the document, [When to Use Java GSS-API Versus
JSSE](when-use-java-gss-api-vs-jsse.htm#GUID-51EAFD1C-7203-40C7-A295-61062D322E8C).

</div>
<!-- class="section" -->

<div class="section">
Resources for This Exercise

-   [Java Secure Socket Extension (JSSE) Reference
    Guide](java-secure-socket-extension-jsse-reference-guide.htm#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345 "The Java Secure Socket Extension (JSSE) enables secure Internet communications. It provides a framework and an implementation for a Java version of the SSL, TLS, and DTLS protocols and includes functionality for data encryption, server authentication, message integrity, and optional client authentication.")
-   The JSSE Javadoc API:
    [<span class="apiname">javax.net</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/package-summary.html)
    and
    [<span class="apiname">javax.net.ssl</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/package-summary.html)
-   [The SSL Protocol version 3.0](https://www.ietf.org/rfc/rfc6101.txt)
-   [The TLS Protocol Version 1.0
    (RFC 2246)](http://www.ietf.org/rfc/rfc2246.txt)
-   [Addition of Kerberos Cipher Suites to Transport Layer Security TLS
    (RFC 2712)](http://www.ietf.org/rfc/rfc2712.txt)
-   [When to Use Java GSS-API Versus
    JSSE](when-use-java-gss-api-vs-jsse.htm#GUID-51EAFD1C-7203-40C7-A295-61062D322E8C)

</div>
<!-- class="section" -->

<div class="section">
Overview of This Exercise

This exercise is a client-server application that demonstrates how to
communicate securely using the JSSE and Kerberos cipher suites. The
client and server parts first authenticate to Kerberos using [Exercise
1: Using the JAAS
API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
This stores the credentials in the subject. The application then
executes an action that performs JSSE operations (using a Kerberos
cipher suite) inside of a <span class="apiname">Subject.doAs</span>
using the subject. The Kerberos cipher suite implementation, because it
is executing inside the <span class="apiname">doAs</span>, obtains the
Kerberos credentials from the subject, and uses them to authenticate
with the peer and to exchange messages securely. This example sends
newline-terminated messages, encrypted using the negotiated cipher suite
and integrity-protected, back and forth between client and server.

According to the standard (RFC 2712) all Kerberos-enabled TLS
applications use the same service name
(<span class="italic">host</span>). That is why in this exercise, you do
not need to explicitly supply the Kerberos service name.

</div>
<!-- class="section" -->

<div class="section">
Steps to Follow

1.  Read the
    [`JsseServer.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JSSESERVER.JAVA-338B733A)
    sample code.

    This code fragment defines the action to execute after the service
    principal has authenticated to the KDC. It replaces the
    `MyAction`{.codeph} in [Exercise 1: Using the JAAS
    API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
    The server first creates an
    <span class="apiname">SSLServerSocket</span>. This is analogous to
    an application creating a plain
    <span class="apiname">ServerSocket</span> except an
    <span class="apiname">SSLServerSocket</span> will provide automatic
    authentication, encryption and decryption, as needed. The server
    then sets the cipher suites that it wants to use. The server then
    runs in a loop, accepting connections from SSL clients, and reads
    and writes from the SSL socket. The server can find out the
    identities of the owners of socket by invoking the
    <span class="apiname">getLocalPrincipal()</span> and
    <span class="apiname">getPeerPrincipal()</span> methods.

2.  Compile the sample code.

3.  Read the
    [`JsseClient.java`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JSSECLIENT.JAVA-338B7667)
    sample code.

    This code fragment defines the action to execute after the client
    principal has authenticated to the KDC. It replaces the
    `MyAction`{.codeph} in [Exercise 1: Using the JAAS
    API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.htm#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8).
    The client first creates an <span class="apiname">SSLSocket</span>.
    The client then sets the cipher suites that it wants to use. The
    client then exchanges messages with the server using the
    <span class="apiname">SSLSocket</span> by reading and writing to the
    socket\'s input/output streams. The client can find out the
    identities of the owners of socket by invoking the
    <span class="apiname">getLocalPrincipal()</span> and
    <span class="apiname">getPeerPrincipal()</span> methods.

4.  Compile the sample code.

5.  Launch a new window and start the server. `JsseServer`{.codeph}
    takes one parameter: the name of the server that the JSSE service is
    running on. For example, if it is running on the machine j1hol-001,
    you would enter the following:

    ``` {.oac_no_warn dir="ltr"}
    % xterm &
    % java -Djava.security.auth.login.config=jaas-krb5.conf JsseServer j1hol-001
    ```

6.  Run the client application. `JsseClient`{.codeph} takes one
    parameter: the name of the server that the JSSE service is running
    on. For example, if the service is running on the machine j1hol-001,
    you would enter the following.

    ``` {.oac_no_warn dir="ltr"}
    % java -Djava.security.auth.login.config=jaas-krb5.conf JsseClient j1hol-001
    ```

    Provide a secure password.

7.  Observe the following output in the respective client and server
    applications\' windows.

    Output for running the `JsseServer`{.codeph} example:

    ``` {.oac_no_warn dir="ltr"}
    Authenticated principal: [host/j1hol-001@J1LABS.EXAMPLE.COM]
    Waiting for incoming connections...
    Got connection from client /192.0.2.102
    Received: Hello There!
    Sending: Hello There! Fri May 07 15:32:37 PDT 2005
    Cipher suite in use: TLS_KRB5_WITH_3DES_EDE_CBC_SHA
    I am: host/j1hol-001@J1LABS.EXAMPLE.COM
    Client is: test@J1LABS.EXAMPLE.COM
    ```

    Output for running the `JsseClient`{.codeph} example
    (<span class="italic">password</span> will be replaced by the
    password that you provided):

    ``` {.oac_no_warn dir="ltr"}
    Kerberos password for test: password
    Authenticated principal: [test@J1LABS.EXAMPLE.COM]
    Sending: Hello There!
    Received: Hello There! Fri May 07 15:32:37 PDT 2005
    Cipher suite in use: TLS_KRB5_WITH_3DES_EDE_CBC_SHA
    I am: test@J1LABS.EXAMPLE.COM
    Server is: host/j1hol-001@J1LABS.EXAMPLE.COM
    ```

</div>
<!-- class="section" -->

<div class="section">
Summary

In this exercise, you learned how to write a client-server application
that uses JSSE to authenticate and communicate securely with each other,
using Kerberos as the underlying authentication system.

</div>
<!-- class="section" -->

<div class="section">
Next Steps

Proceed to [Exercise 6: Deploying for Single
Sign-On](part-iii-deploying-single-sign-kerberos-environment.htm#GUID-5D0B8FD9-FF12-44E7-B7E9-7620E95E784C)
to learn how to configure the sample programs in Exercises 3, 4, and 5
to achieve single sign-on in a Kerberos environment.

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
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| ---------- --------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| -------------------- | o | ass="icon">Contents< |
| -------------------- | g | /span>](toc.htm)     |
| - --                 | o |   -- --------------- |
|                      | ] | -------------------- |
|                      | ( | -------------------- |
|    [![Previous](../. | . | ---                  |
| ./dcommon/gifs/leftn | . |                      |
| av.gif)\             | / |                      |
|                      | . |                      |
|                      | . |                      |
|                [![Ne | / |                      |
| xt](../../dcommon/gi | d |                      |
| fs/rightnav.gif)\    | c |                      |
|                      | o |                      |
|                      | m |                      |
|    <span class="icon | m |                      |
| ">Previous</span>](p | o |                      |
| art-i-secure-authent | n |                      |
| ication-using-java-a | / |                      |
| uthentication-and-au | g |                      |
| thorization-service- | i |                      |
| jaas.htm)   <span cl | f |                      |
| ass="icon">Next</spa | s |                      |
| n>](part-iii-deployi | / |                      |
| ng-single-sign-kerbe | o |                      |
| ros-environment.htm) | r |                      |
|                      | a |                      |
|   ------------------ | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| -------------------- | . |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| ---------- --------- | f |                      |
| -------------------- | ) |                      |
| -------------------- | { |                      |
| -------------------- | . |                      |
| -------------------- | c |                      |
| - --                 | o |                      |
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
