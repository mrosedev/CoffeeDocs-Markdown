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

  ------------------------------------------------------------------------ ---------------------------------------------------------- --
               [![Previous](../../dcommon/gifs/leftnav.gif)\                       [![Next](../../dcommon/gifs/rightnav.gif)\         
   <span class="icon">Previous</span>](when-use-java-gss-api-vs-jsse.htm)   <span class="icon">Next</span>](jaas-authentication.htm)  
  ------------------------------------------------------------------------ ---------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-42A2B80C-90CD-4C7A-8EED-8BFFE83CAF56}<!-- End Header -->

Use of Java GSS-API for Secure Message Exchanges Without JAAS Programming {#JSSEC-GUID-42A2B80C-90CD-4C7A-8EED-8BFFE83CAF56 .sect1}
=========================================================================

<div>
This tutorial presents two sample applications demonstrating the use of
the Java GSS-API for secure exchanges of messages between communicating
applications, in this case a client application and a server
application.

Java GSS-API uses what is called a \"security mechanism\" to provide
these services. The GSS-API implementation contains support for the
Kerberos V5 mechanism in addition to any other vendor-specific choices.
The Kerberos V5 mechanism is used for this tutorial.

In order to perform authentication between the client and server and to
establish cryptographic keys for secure communication, a GSS-API
mechanism needs access to certain credentials for the local entity on
each side of the connection. In our case, the credential used on the
client side consists of a Kerberos ticket, and on the server side, it
consists of a long-term Kerberos secret key. Kerberos tickets can
optionally include the host address and IPv4 and IPv6 host addresses are
both supported. Java GSS-API requires that the mechanism obtain these
credentials from the Subject associated with the thread\'s access
control context.

To populate a Subject with such credentials, client and server
applications typically will first perform JAAS authentication using a
Kerberos <span class="apiname">LoginModule</span>. The [JAAS
Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
tutorial demonstrates how to do this. The [JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F)
tutorial then demonstrates how to associate the authenticated Subject
with the thread\'s access control context. A utility has also been
written as a convenience to automatically perform those operations on
your behalf. The [Use of JAAS Login
Utility](use-jaas-login-utility.html#GUID-F41E74DF-EE54-4EB1-8609-49C6D324ADF5)
tutorial demonstrates how to use the Login utility.

For this tutorial, we will not have the client and server perform JAAS
authentication, nor will we have them use the Login utility. Instead, we
will rely on setting the system property
`javax.security.auth.useSubjectCredsOnly`{.codeph} to `false`{.codeph},
which allows us to relax the restriction of requiring a GSS mechanism to
obtain necessary credentials from an existing
[Subject](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3),
set up by JAAS. See [The useSubjectCredsOnly System
Property](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-841EB74E-3B52-4421-BC10-FE3C8511E007).

<div class="infoboxnote" id="GUID-42A2B80C-90CD-4C7A-8EED-8BFFE83CAF56__GUID-C1D390A1-E212-48D7-BB3D-B117D67BD365">
Note:

This is a simplified introductory tutorial. For example, we do not
include any policy files or run the sample code using a security
manager. In real life, code using Java GSS-API should be run with a
security manager, so that security-sensitive operations would not be
allowed unless the required permissions were explicitly granted.

</div>
There is another tutorial, [Use of JAAS Login Utility and Java GSS-API
for Secure Message
Exchanges](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8),
that is just like the tutorial you are reading except that it utilizes
the Login utility, policy files, and a more complex login configuration
file. A login configuration file (see [Appendix B: JAAS Login
Configuration
File](appendix-b-jaas-login-configuration-file.html#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)),
required whenever JAAS authentication is done, specifies the desired
authentication module.

As with all tutorials in this series, the underlying technology used to
support authentication and secure communication for the applications in
this tutorial is Kerberos V5. See [Kerberos
Requirements](kerberos-requirements1.html#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998).

-   [Overview of the Client and Server
    Applications](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-BEDCBE80-87A3-4124-B891-DF15C55301A5)
-   [The SampleClient and SampleServer
    Code](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-0DDC8ACE-7398-41C6-B061-CF3DEAB7AC86)
-   [Kerberos User and Service Principal
    Names](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-6D82A7D2-C406-40F4-838A-42ED61194182)
-   [The Login Configuration
    File](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-2ED6C724-87F1-49EB-9015-32E6E74E3C6A)
-   [The useSubjectCredsOnly System
    Property](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-841EB74E-3B52-4421-BC10-FE3C8511E007)
-   [Running the SampleClient and SampleServer
    Programs](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-DC1FCD2D-101C-4EF2-8034-387CBE66FA3E)

If you want to first see the tutorial code in action, you can skip
directly to [Running the SampleClient and SampleServer
Programs](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-DC1FCD2D-101C-4EF2-8034-387CBE66FA3E)
and then go back to the other sections to learn more.

</div>
<div class="sect2">
[]{#GUID-BEDCBE80-87A3-4124-B891-DF15C55301A5}

Overview of the Client and Server Applications {#JSSEC-GUID-BEDCBE80-87A3-4124-B891-DF15C55301A5 .sect2}
----------------------------------------------

<div>
The applications for this tutorial are named `SampleClient`{.codeph} and
`SampleServer`{.codeph}.

Here is a summary of execution of the `SampleClient`{.codeph} and
`SampleServer`{.codeph} applications:

1.  Run the `SampleServer`{.codeph} application. `SampleServer`{.codeph}
    a.  Reads its argument, the port number that it should listen on for
        client connections.
    b.  Creates a <span class="apiname">ServerSocket</span> for
        listening for client connections on that port.
    c.  Listens for a connection.
2.  Run the `SampleClient`{.codeph} application (possibly on a different
    machine). `SampleClient`{.codeph}
    a.  Reads its arguments: (1) The name of the Kerberos principal that
        represents `SampleServer`{.codeph} (see [Kerberos User and
        Service Principal
        Names](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-6D82A7D2-C406-40F4-838A-42ED61194182)), (2)
        the name of the host (machine) on which `SampleServer`{.codeph}
        is running, and (3) the port number on which
        `SampleServer`{.codeph} listens for client connections.
    b.  Attempts a socket connection with the `SampleServer`{.codeph},
        using the host and port it was passed as arguments.
3.  The socket connection is accepted by `SampleServer`{.codeph} and
    both applications initialize a
    <span class="apiname">DataInputStream</span> and a
    <span class="apiname">DataOutputStream</span> from the socket input
    and output streams, to be used for future data exchanges.
4.  `SampleClient`{.codeph} and `SampleServer`{.codeph} each instantiate
    a <span class="apiname">GSSContext</span> and follow a protocol for
    establishing a shared context that will enable subsequent secure
    data exchanges.
5.  `SampleClient`{.codeph} and `SampleServer`{.codeph} can now securely
    exchange messages.
6.  When `SampleClient`{.codeph} and `SampleServer`{.codeph} are done
    exchanging messages, they perform clean-up operations.

The actual code and further details are presented in the following
sections.

</div>
</div>
<div class="sect2">
[]{#GUID-0DDC8ACE-7398-41C6-B061-CF3DEAB7AC86}

The SampleClient and SampleServer Code {#JSSEC-GUID-0DDC8ACE-7398-41C6-B061-CF3DEAB7AC86 .sect2}
--------------------------------------

<div>
The entire code for both the
[` SampleClient.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLECLIENT.JAVA-338923E1)
and
[`SampleServer.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLESERVER.JAVA-33891DED)
programs resides in their `main`{.codeph} methods and can be broken down
into the following subparts:

1.  [Obtaining the Command-Line
    Arguments](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-50F25F90-A350-4A21-A06E-44E33209D542)
2.  [Establishing a Socket Connection for Message
    Exchanges](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-04BC81DE-98D3-42CA-9AC0-45CB4ECEC0BB)
3.  [Establishing a Security
    Context](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-3619B5FA-76CA-4445-8770-8D56CEBA967B)
4.  [Exchanging Messages
    Securely](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-39585A77-5CF3-4122-B4EC-3D778392370D)
5.  [Clean
    Up](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-DA54B317-30B2-4666-86B6-B1AD4D627002)

<div class="infoboxnote" id="GUID-0DDC8ACE-7398-41C6-B061-CF3DEAB7AC86__GUID-39A47901-8887-47B3-BDCC-CDA90803FABF">
Note:

The Java GSS-API classes utilized by these programs
(<span class="apiname">GSSManager</span>,
<span class="apiname">GSSContext</span>,
<span class="apiname">GSSName</span>,
<span class="apiname">GSSCredential</span>,
<span class="apiname">MessageProp</span>, and
<span class="apiname">Oid</span>) are found in the
[<span class="apiname">org.ietf.jgss</span>](https://docs.oracle.com/javase/10/docs/api/org/ietf/jgss/package-summary.html)
package.

</div>
</div>
<div class="sect3">
[]{#GUID-50F25F90-A350-4A21-A06E-44E33209D542}

### Obtaining the Command-Line Arguments {#JSSEC-GUID-50F25F90-A350-4A21-A06E-44E33209D542 .sect3}

<div>
The first thing both our client and server `main`{.codeph} methods do is
read the command-line arguments.

</div>
<div class="sect4">
[]{#GUID-E4E494AB-4273-4C46-B172-D0DBBF010903}

#### Arguments Read by SampleClient {#JSSEC-GUID-E4E494AB-4273-4C46-B172-D0DBBF010903 .sect4}

<div>
`SampleClient`{.codeph} expects three arguments:

1.  A service principal name -- The name of the Kerberos principal that
    represents `SampleServer`{.codeph} (see [Kerberos User and Service
    Principal
    Names](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-6D82A7D2-C406-40F4-838A-42ED61194182)).
2.  A host name -- The machine on which `SampleServer`{.codeph} is
    running.
3.  A port number -- The port number of the port on which
    `SampleServer`{.codeph} listens for connections.

Here is the code for reading the command-line arguments:

``` {.oac_no_warn dir="ltr"}
if (args.length < 3) {
    System.out.println("Usage: java <options> Login SampleClient "
       + " <servicePrincipal> <hostName> <port>");
    System.exit(-1);
}

String server = args[0];
String hostName = args[1];
int port = Integer.parseInt(args[2]);
```

</div>
</div>
<div class="sect4">
[]{#GUID-3E0915A3-9B41-4CA4-90D6-1A039A8B54C0}

#### Argument Read by SampleServer {#JSSEC-GUID-3E0915A3-9B41-4CA4-90D6-1A039A8B54C0 .sect4}

<div>
`SampleServer`{.codeph} expects just one argument:

-   A local port number -- The port number used by
    `SampleServer`{.codeph} for listening for connections with clients.
    This number should be the same as the port number specified when
    running the `SampleClient`{.codeph} program.

Here is the code for reading the command-line argument:

``` {.oac_no_warn dir="ltr"}
if (args.length != 1) {
    System.out.println(
        "Usage: java <options> Login SampleServer <localPort>");
    System.exit(-1);
}

int localPort = Integer.parseInt(args[0]);
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-04BC81DE-98D3-42CA-9AC0-45CB4ECEC0BB}

### Establishing a Socket Connection for Message Exchanges {#JSSEC-GUID-04BC81DE-98D3-42CA-9AC0-45CB4ECEC0BB .sect3}

<div>
Java GSS-API provides methods for creating and interpreting tokens
(opaque byte data). The tokens contain messages to be securely exchanged
between two peers, but the method of actual token transfer is up to the
peers. For our `SampleClient`{.codeph} and `SampleServer`{.codeph}
applications, we establish a socket connection between the client and
server and exchange data using the socket input and output streams.

</div>
<div class="sect4">
[]{#GUID-17E54F39-2231-4271-BBDB-AF72D3D75FF3}

#### SampleClient Code for Socket Connection {#JSSEC-GUID-17E54F39-2231-4271-BBDB-AF72D3D75FF3 .sect4}

<div>
`SampleClient`{.codeph} was passed as arguments the name of the host
machine `SampleServer`{.codeph} is running on, as well as the port
number on which `SampleServer`{.codeph} will be listening for
connections, so `SampleClient`{.codeph} has all it needs to establish a
socket connection with `SampleServer`{.codeph}. It uses the following
code to set up the connection and initialize a
<span class="apiname">DataInputStream</span> and a
<span class="apiname">DataOutputStream</span> for future data exchanges:

``` {.oac_no_warn dir="ltr"}
Socket socket = new Socket(hostName, port);

DataInputStream inStream = 
  new DataInputStream(socket.getInputStream());
DataOutputStream outStream = 
  new DataOutputStream(socket.getOutputStream());

System.out.println("Connected to server " 
   + socket.getInetAddress());
```

</div>
</div>
<div class="sect4">
[]{#GUID-6E59BA99-675F-4937-88BB-89268949B356}

#### SampleServer Code for Socket Connection {#JSSEC-GUID-6E59BA99-675F-4937-88BB-89268949B356 .sect4}

<div>
The `SampleServer`{.codeph} application was passed as an argument the
port number to be used for listening for connections from clients. It
creates a `ServerSocket`{.codeph} for listening on that port:

``` {.oac_no_warn dir="ltr"}
ServerSocket ss = new ServerSocket(localPort);
```

The `ServerSocket`{.codeph} can then wait for and accept a connection
from a client, and then initialize a
<span class="apiname">DataInputStream</span> and a
<span class="apiname">DataOutputStream</span> for future data exchanges
with the client :

``` {.oac_no_warn dir="ltr"}
Socket socket = ss.accept();

DataInputStream inStream =
    new DataInputStream(socket.getInputStream());
DataOutputStream outStream = 
    new DataOutputStream(socket.getOutputStream());

System.out.println("Got connection from client "
    + socket.getInetAddress());
```

The `accept`{.codeph} method waits until a client (in our case,
`SampleClient`{.codeph}) requests a connection on the host and port of
the `SampleServer`{.codeph}, which `SampleClient`{.codeph} does via

``` {.oac_no_warn dir="ltr"}
Socket socket = new Socket(hostName, port);
```

When the connection is requested and established, the `accept`{.codeph}
method returns a new <span class="apiname">Socket</span> object bound to
a new port. The server can communicate with the client over this new
socket and continue to listen for other client connection requests on
the `ServerSocket`{.codeph} bound to the original port. Thus, a server
program typically has a loop which can handle multiple connection
requests.

The basic loop structure for our `SampleServer`{.codeph} is the
following:

``` {.oac_no_warn dir="ltr"}
while (true) {

    Socket socket = ss.accept();

    <Establish input and output streams for the connection>; 
    <Establish a context with the client>; 
    <Exchange messages with the client>;
    <Clean up>;
}
```

Client connections are queued at the original port, so with this program
structure used by `SampleServer`{.codeph}, the interaction with the
first client making a connection has to complete before the next
connection can be accepted. The server could actually service multiple
clients simultaneously through the use of threads -- one thread per
client connection, as in

``` {.oac_no_warn dir="ltr"}
while (true) {
    <accept a connection>;
    <create a thread to handle the client>;
}
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-3619B5FA-76CA-4445-8770-8D56CEBA967B}

### Establishing a Security Context {#JSSEC-GUID-3619B5FA-76CA-4445-8770-8D56CEBA967B .sect3}

<div>
Before two applications can use Java GSS-API to securely exchange
messages between them, they must establish a joint security context
using their credentials. (Note: In the case of `SampleClient`{.codeph},
the credentials were established when the Login utility authenticated
the user on whose behalf the `SampleClient`{.codeph} was run, and
similarly for `SampleServer`{.codeph}.) The security context
encapsulates shared state information that might include, for example,
cryptographic keys. One use of such keys might be to encrypt messages to
be exchanged, if encryption is requested.

As part of the security context establishment, the context initiator (in
our case, `SampleClient`{.codeph}) is authenticated to the acceptor
(`SampleServer`{.codeph}), and may require that the acceptor also be
authenticated back to the initiator, in which case we say that \"mutual
authentication\" took place.

Both applications create and use a
<span class="apiname">GSSContext</span> object to establish and maintain
the shared information that makes up the security context.

The instantiation of the context object is done differently by the
context initiator and the context acceptor. After the initiator
instantiates a <span class="apiname">GSSContext</span>, it may choose to
set various context options that will determine the characteristics of
the desired security context, for example, specifying whether or not
mutual authentication should take place. After all the desired
characteristics have been set, the initiator calls the
`initSecContext`{.codeph} method, which produces a token required by the
acceptor\'s `acceptSecContext`{.codeph} method.

While Java GSS-API methods exist for preparing tokens to be exchanged
between applications, <span class="variable">it is the responsibility of
the applications to actually transfer the tokens between them.</span> So
after the initiator has received a token from its call to
`initSecContext`{.codeph}, it sends that token to the acceptor. The
acceptor calls `acceptSecContext`{.codeph}, passing it the token. The
`acceptSecContext`{.codeph} method may in turn return a token. If it
does, the acceptor should send that token to the initiator, which should
then call `initSecContext`{.codeph} again and pass it this token. Each
time `initSecContext`{.codeph} or `acceptSecContext`{.codeph} returns a
token, the application that called the method should send the token to
its peer and that peer should pass the token to its appropriate method
(`acceptSecContext`{.codeph} or `initSecContext`{.codeph}). This
continues until the context is fully established (which is the case when
the context\'s `isEstablished`{.codeph} method returns `true`{.codeph}).

The context establishment code for our sample applications is described
in the following:

-   [Context Establishment by
    SampleClient](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-3C5C1A0A-83D7-4AF8-94EC-EEA8112DEBAC)
-   [Context Establishment by
    SampleServer](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-7466BDBC-CB41-4287-802A-C3426B14304A)

</div>
<div class="sect4">
[]{#GUID-3C5C1A0A-83D7-4AF8-94EC-EEA8112DEBAC}

#### Context Establishment by SampleClient {#JSSEC-GUID-3C5C1A0A-83D7-4AF8-94EC-EEA8112DEBAC .sect4}

<div>
In our client/server scenario, SampleClient is the context initiator.
Here are the basic steps it takes to establish a security context:

1.  [SampleClient GSSContext
    Instantiation](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-5E314B25-F3EF-4F40-BB32-678F9DD71D3B)
2.  [SampleClient Setting of Desired
    Options](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-4D05D762-CD29-4A82-B773-5652A4754BF5)
3.  [SampleClient Context Establishment
    Loop](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-AB3C68A2-4E5E-42B2-96C1-C8BDAB5058A7):
    Loops while the context is not yet established, each time calling
    `initSecContext`{.codeph}, sending any returned token to
    `SampleServer`{.codeph}, and receiving a token (if any) from
    `SampleServer`{.codeph}.

</div>
<div class="sect5">
[]{#GUID-5E314B25-F3EF-4F40-BB32-678F9DD71D3B}

##### SampleClient GSSContext Instantiation {#JSSEC-GUID-5E314B25-F3EF-4F40-BB32-678F9DD71D3B .sect5}

<div>
A <span class="apiname">GSSContext</span> is created by instantiating a
<span class="apiname">GSSContext</span> and then calling one of its
`createContext`{.codeph} methods. The
<span class="apiname">GSSManager</span> class serves as a factory for
other important GSS API classes. It can create instances of classes
implementing the <span class="apiname">GSSContext</span>,
<span class="apiname">GSSCredential</span>, and
<span class="apiname">GSSName</span> interfaces.

`SampleClient`{.codeph} obtains an instance of the default
<span class="apiname">GSSManager</span> subclass by calling the
<span class="apiname">GSSManager</span> static method
`getInstance`{.codeph}:

``` {.oac_no_warn dir="ltr"}
GSSManager manager = GSSManager.getInstance();
```

The default <span class="apiname">GSSManager</span> subclass is one
whose `create*`{.codeph} methods (`createContext`{.codeph}, etc.) return
classes whose implementations support Kerberos as the underlying
technology.

The <span class="apiname">GSSManager</span> factory method for creating
a context on the initiator\'s side has the following signature:

``` {.oac_no_warn dir="ltr"}
GSSContext createContext(GSSName peer, Oid mech, 
            GSSCredential myCred, int lifetime);
```

The arguments are described below, followed by the complete call to
`createContext`{.codeph}.

</div>
<div class="sect6">
[]{#GUID-4C2BEA87-066F-4910-B09B-CB9C9B65D896}

###### The GSSName peer Argument {#JSSEC-GUID-4C2BEA87-066F-4910-B09B-CB9C9B65D896 .sect6}

<div>
The peer in our client/server paradigm is the server. For the
`peer`{.codeph} argument, we need a <span class="apiname">GSSName</span>
for the service principal representing the server. (See [Kerberos User
and Service Principal
Names](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-6D82A7D2-C406-40F4-838A-42ED61194182).)
A <span class="apiname">String</span> for the service principal name is
passed as the first argument to `SampleClient`{.codeph}, which places
the argument into its local <span class="apiname">String</span> variable
named `server`{.codeph}. The <span class="apiname">GSSManager</span>
`manager`{.codeph} is used to instantiate a
<span class="apiname">GSSName</span> by calling one of its
`createName`{.codeph} methods. `SampleClient`{.codeph} calls the
`createName`{.codeph} method with the following signature:

``` {.oac_no_warn dir="ltr"}
GSSName createName(String nameStr, Oid nameType);
```

`SampleClient`{.codeph} passes the `server`{.codeph}
<span class="apiname">String</span> for the `nameStr`{.codeph} argument.

The second argument is an <span class="apiname">Oid</span>. An
<span class="apiname">Oid</span> represents a Universal Object
Identifier. Oids are hierarchically globally-interpretable identifiers
used within the GSS-API framework to identify mechanisms and name types.
The structure and encoding of Oids is defined in the ISOIEC-8824 and
ISOIEC-8825 standards. The <span class="apiname">Oid</span> passed to
the `createName`{.codeph} method is specifically a name type
<span class="apiname">Oid</span> (not a mechanism Oid).

In GSS-API, string names are often mapped from a mechanism-independent
format into a mechanism-specific format. Usually, an Oid specifies what
name format the string is in so that the mechanism knows how to do this
mapping. Passing in a `null`{.codeph} <span class="apiname">Oid</span>
indicates that the name is already in a native format that the mechanism
uses. This is the case for the `server`{.codeph} String; it is in the
appropriate format for a Kerberos Version 5 name. Thus,
`SampleClient`{.codeph} passes a `null`{.codeph} for the
<span class="apiname">Oid</span>. Here is the call:

``` {.oac_no_warn dir="ltr"}
GSSName serverName = manager.createName(server, null);
```

</div>
</div>
<div class="sect6">
[]{#GUID-25214B28-5B08-4173-874B-7A2CEDDE55FB}

###### The Oid mech Argument {#JSSEC-GUID-25214B28-5B08-4173-874B-7A2CEDDE55FB .sect6}

<div>
The second argument to the <span class="apiname">GSSManager</span>
`createContext`{.codeph} method is an Oid representing the mechanism to
be used for the authentication between the client and the server during
context establishment and for subsequent secure communication between
them.

Our tutorial will use Kerberos V5 as the security mechanism. The Oid for
the Kerberos V5 mechanism is defined in [RFC
1964](http://www.ietf.org/rfc/rfc1964.txt) as \"1.2.840.113554.1.2.2\"
so we create such an <span class="apiname">Oid</span>:

``` {.oac_no_warn dir="ltr"}
Oid krb5Oid = new Oid("1.2.840.113554.1.2.2");
```

`SampleClient`{.codeph} passes `krb5Oid`{.codeph} as the second argument
to `createContext`{.codeph}.

</div>
</div>
<div class="sect6">
[]{#GUID-AA193F7A-9EAB-4A3B-88DC-104EA28DB05D}

###### The GSSCredential myCred Argument {#JSSEC-GUID-AA193F7A-9EAB-4A3B-88DC-104EA28DB05D .sect6}

<div>
The third argument to the <span class="apiname">GSSManager</span>
`createContext`{.codeph} method is a
<span class="apiname">GSSCredential</span> representing the caller\'s
credentials. If you pass `null`{.codeph} for this argument, as
<span class="apiname">SampleClient</span> does, the default credentials
are used.

</div>
</div>
<div class="sect6">
[]{#GUID-8728175F-7265-40E3-A10B-82EC27FDEA84}

###### The int lifetime Argument {#JSSEC-GUID-8728175F-7265-40E3-A10B-82EC27FDEA84 .sect6}

<div>
The final argument to the <span class="apiname">GSSManager</span>
`createContext`{.codeph} method is an `int`{.codeph} specifying the
desired lifetime, in seconds, for the context that is created.
`SampleClient`{.codeph} passes `GSSContext.DEFAULT_LIFETIME`{.codeph} to
request a default lifetime.

</div>
</div>
<div class="sect6">
[]{#GUID-6DA100F6-33D3-479F-AFB2-1DC61EE2F127}

###### The Complete createContext Call {#JSSEC-GUID-6DA100F6-33D3-479F-AFB2-1DC61EE2F127 .sect6}

<div>
Now that we have all the required arguments, here is the call
`SampleClient`{.codeph} makes to create a
<span class="apiname">GSSContext</span>:

``` {.oac_no_warn dir="ltr"}
GSSContext context = 
    manager.createContext(serverName,
                          krb5Oid,
                          null,
                          GSSContext.DEFAULT_LIFETIME);
```

</div>
</div>
</div>
<div class="sect5">
[]{#GUID-4D05D762-CD29-4A82-B773-5652A4754BF5}

##### SampleClient Setting of Desired Options {#JSSEC-GUID-4D05D762-CD29-4A82-B773-5652A4754BF5 .sect5}

<div>
After instantiating a context, and prior to actually establishing the
context with the context acceptor, the context initiator may choose to
set various options that determine the desired security context
characteristics. Each such option is set by calling a `request`{.codeph}
method on the instantiated context. Most `request`{.codeph} methods take
a `boolean`{.codeph} argument for indicating whether or not the feature
is requested. It is not always possible for a request to be satisfied,
so whether or not it was can be determined after context establishment
by calling one of the `get`{.codeph} methods.

`SampleClient`{.codeph} requests the following:

1.  <span class="bold">Mutual authentication</span>. The context
    initiator is always authenticated to the acceptor. If the initiator
    requests mutual authentication, then the acceptor is also
    authenticated to the initiator.
2.  <span class="bold">Confidentiality</span>. Requesting
    confidentiality means that you request the
    <span class="variable">enabling</span> of encryption for the context
    method named `wrap`{.codeph}. Encryption is actually used only if
    the <span class="apiname">MessageProp</span> object passed to the
    `wrap`{.codeph} method requests privacy.
3.  <span class="bold">Integrity</span>. This requests integrity for the
    `wrap`{.codeph} and `getMIC`{.codeph} methods. When integrity is
    requested, a cryptographic tag known as a Message Integrity Code
    (MIC) will be generated when calling those methods. When
    `getMIC`{.codeph} is called, the generated MIC appears in the
    returned token. When `wrap`{.codeph} is called, the MIC is packaged
    together with the message (the original message or the result of
    encrypting the message, depending on whether confidentiality was
    applied) all as part of one token. You can subsequently verify the
    MIC against the message to ensure that the message has not been
    modified in transit.

The `SampleClient`{.codeph} code for making these requests on the
`GSSException`{.codeph} `context`{.codeph} is the following:

``` {.oac_no_warn dir="ltr"}
context.requestMutualAuth(true);  // Mutual authentication
context.requestConf(true);  // Will use encryption later
context.requestInteg(true); // Will use integrity later
```

After the context is established, the client must explicitly check the
context states by calling the accesor methods, like
<span class="apiname">getMutualAuthState</span>,
<span class="apiname">getConfState</span>, or
<span class="apiname">getIntegState</span>, and destroy the security
context if any of them do not match the desired state.

<div class="infoboxnote" id="GUID-4D05D762-CD29-4A82-B773-5652A4754BF5__GUID-5D58F826-9EF4-432F-8A87-EA1B00074217">
Note:

When using the default <span class="apiname">GSSManager</span>
implementation and the Kerberos mechanism, these requests will always be
granted.

</div>
</div>
</div>
<div class="sect5">
[]{#GUID-AB3C68A2-4E5E-42B2-96C1-C8BDAB5058A7}

##### SampleClient Context Establishment Loop {#JSSEC-GUID-AB3C68A2-4E5E-42B2-96C1-C8BDAB5058A7 .sect5}

<div>
After `SampleClient`{.codeph} has instantiated a
<span class="apiname">GSSContext</span> and specified the desired
context options, it can actually establish the security context with
`SampleServer`{.codeph}. To do so, `SampleClient`{.codeph} has a loop.
Each loop iteration

1.  Calls the context\'s `initSecContext`{.codeph} method. If this is
    the first call, the method is passed a `null`{.codeph} token.
    Otherwise, it is passed the token most recently sent to
    `SampleClient`{.codeph} by `SampleServer`{.codeph} (a token
    generated by a `SampleServer`{.codeph} call to
    `acceptSecContext`{.codeph}).
2.  Sends the token returned by `initSecContext`{.codeph} (if any) to
    `SampleServer`{.codeph}. The first call to `initSecContext`{.codeph}
    always produces a token. The last call might not return a token.
3.  Checks to see if the context is established. If not,
    `SampleClient`{.codeph} receives another token from
    `SampleServer`{.codeph} and then starts the next loop iteration.

The tokens returned by `initSecContext`{.codeph} or received from
`SampleServer`{.codeph} are placed in a byte array. Tokens should be
treated by `SampleClient`{.codeph} and `SampleServer`{.codeph} as opaque
data to be passed between them and interpreted by Java GSS-API methods.

The `initSecContext`{.codeph} arguments are a byte array containing a
token, the starting offset into that array of where the token begins,
and the token length. For the first call, `SampleClient`{.codeph} passes
a null token, since no token has yet been received from
`SampleServer`{.codeph}.

To exchange tokens with `SampleServer`{.codeph}, `SampleClient`{.codeph}
uses the <span class="apiname">DataInputStream</span>
`inStream`{.codeph} and <span class="apiname">DataOutputStream</span>
`outStream`{.codeph} it previously set up using the input and output
streams for the socket connection made with `SampleServer`{.codeph}.
Note that whenever a token is written, the number of bytes in the token
is written first, followed by the token itself. The reasons are
discussed in the introduction to the [The SampleClient and SampleServer
Message
Exchanges](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-D929F2E0-8AD5-46A3-8A1F-7C30ACE5675B)
section.

Here is the `SampleClient`{.codeph} context establishment loop, followed
by code displaying information about who the client and server are and
whether or not mutual authentication actually took place:

``` {.oac_no_warn dir="ltr"}
byte[] token = new byte[0];

while (!context.isEstablished()) {

    // token is ignored on the first call
    token = context.initSecContext(token, 0, token.length);

    // Send a token to the server if one was generated by
    // initSecContext
    if (token != null) {
        System.out.println("Will send token of size "
                   + token.length + " from initSecContext.");
        outStream.writeInt(token.length);
        outStream.write(token);
        outStream.flush();
    }

    // If the client is done with context establishment
    // then there will be no more tokens to read in this loop
    if (!context.isEstablished()) {
        token = new byte[inStream.readInt()];
        System.out.println("Will read input token of size "
                   + token.length
                   + " for processing by initSecContext");
        inStream.readFully(token);
    }
}

System.out.println("Context Established! ");
System.out.println("Client is " + context.getSrcName());
System.out.println("Server is " + context.getTargName());
if (context.getMutualAuthState())
    System.out.println("Mutual authentication took place!");
```

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-7466BDBC-CB41-4287-802A-C3426B14304A}

#### Context Establishment by SampleServer {#JSSEC-GUID-7466BDBC-CB41-4287-802A-C3426B14304A .sect4}

<div>
In our client/server scenario, `SampleServer`{.codeph} is the context
acceptor. Here are the basic steps it takes to establish a security
context:

1.  [SampleServer GSSContext
    Instantiation](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-528478D5-A436-4539-9994-F6F338B02910)
2.  [SampleClient Context Establishment
    Loop](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-AB3C68A2-4E5E-42B2-96C1-C8BDAB5058A7):
    Loops while the context is not yet established, each time receiving
    a token from `SampleClient`{.codeph}, calling
    `acceptSecContext`{.codeph} and passing it the token, and sending
    any returned token to `SampleClient`{.codeph}.

</div>
<div class="sect5">
[]{#GUID-528478D5-A436-4539-9994-F6F338B02910}

##### SampleServer GSSContext Instantiation {#JSSEC-GUID-528478D5-A436-4539-9994-F6F338B02910 .sect5}

<div>
As described in [SampleClient GSSContext
Instantiation](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-5E314B25-F3EF-4F40-BB32-678F9DD71D3B),
a <span class="apiname">GSSContext</span> is created by instantiating a
<span class="apiname">GSSManager</span> and then calling one of its
`createContext`{.codeph} methods.

Like `SampleClient`{.codeph}, `SampleServer`{.codeph} obtains an
instance of the default <span class="apiname">GSSManager</span> subclass
by calling the <span class="apiname">GSSManager</span> static method
`getInstance`{.codeph}:

``` {.oac_no_warn dir="ltr"}
GSSManager manager = GSSManager.getInstance();
```

The <span class="apiname">GSSManager</span> factory method for creating
a context on the acceptor\'s side has the following signature:

``` {.oac_no_warn dir="ltr"}
GSSContext createContext(GSSCredential myCred);
```

If you pass `null`{.codeph} for the
<span class="apiname">GSSCredential</span> argument, as
`SampleServer`{.codeph} does, the default credentials are used. The
context is instantiated via the following:

``` {.oac_no_warn dir="ltr"}
GSSContext context = manager.createContext((GSSCredential)null);
```

</div>
</div>
<div class="sect5">
[]{#GUID-0DCD04B3-6461-4F0E-B160-2560909F22CA}

##### SampleServer Context Establishment Loop {#JSSEC-GUID-0DCD04B3-6461-4F0E-B160-2560909F22CA .sect5}

<div>
After SampleServer has instantiated a GSSContext, it can establish the
security context with SampleClient. To do so, SampleServer has a loop
that continues until the context is established. Each loop iteration
does the following:

1.  Receives a token from SampleClient. This token is the result of a
    SampleClient `initSecContext`{.codeph} call.
2.  Calls the context\'s `acceptSecContext`{.codeph} method, passing it
    the token just received.
3.  If `acceptSecContext`{.codeph} returns a token, then SampleServer
    sends this token to SampleClient and then starts the next loop
    iteration if the context is not yet established.

The tokens returned by `acceptSecContext`{.codeph} or received from
SampleClient are placed in a byte array.

The `acceptSecContext`{.codeph} arguments are a byte array containing a
token, the starting offset into that array of where the token begins,
and the token length.

To exchange tokens with SampleClient, SampleServer uses the
DataInputStream `inStream`{.codeph} and DataOutputStream
`outStream`{.codeph} it previously set up using the input and output
streams for the socket connection made with SampleClient.

Here is the SampleServer context establishment loop:

``` {.oac_no_warn dir="ltr"}
byte[] token = null;

while (!context.isEstablished()) {

    token = new byte[inStream.readInt()];
    System.out.println("Will read input token of size "
       + token.length
       + " for processing by acceptSecContext");
    inStream.readFully(token);
    
    token = context.acceptSecContext(token, 0, token.length);
    
    // Send a token to the peer if one was generated by
    // acceptSecContext
    if (token != null) {
        System.out.println("Will send token of size "
           + token.length
           + " from acceptSecContext.");
        outStream.writeInt(token.length);
        outStream.write(token);
        outStream.flush();
    }
}

System.out.print("Context Established! ");
System.out.println("Client is " + context.getSrcName());
System.out.println("Server is " + context.getTargName());
if (context.getMutualAuthState())
    System.out.println("Mutual authentication took place!");
```

</div>
</div>
</div>
</div>
<div class="sect3">
[]{#GUID-39585A77-5CF3-4122-B4EC-3D778392370D}

### Exchanging Messages Securely {#JSSEC-GUID-39585A77-5CF3-4122-B4EC-3D778392370D .sect3}

<div>
Once a security context has been established between
`SampleClient`{.codeph} and `SampleServer`{.codeph}, they can use the
context to securely exchange messages.

-   [GSSContext Methods for Message
    Exchange](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-683071BD-5FAB-4392-BABD-A5A68C145120)
-   [The SampleClient and SampleServer Message
    Exchanges](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-D929F2E0-8AD5-46A3-8A1F-7C30ACE5675B)

</div>
<div class="sect4">
[]{#GUID-683071BD-5FAB-4392-BABD-A5A68C145120}

#### GSSContext Methods for Message Exchange {#JSSEC-GUID-683071BD-5FAB-4392-BABD-A5A68C145120 .sect4}

<div>
Two types of methods exist for preparing messages for secure exchange:
`wrap`{.codeph} and `getMIC`{.codeph}. There are actually two
`wrap`{.codeph} methods (and two `getMIC`{.codeph} methods), where the
differences between the two are the indication of where the input
message is (a byte array or an input stream) and where the output should
go (to a byte array return value or to an output stream).

These methods for preparing messages for exchange, and the corresponding
methods for interpretation by the peer of the resulting tokens, are
described below.

</div>
<div class="sect5">
[]{#GUID-F034E83C-1CA8-49E5-8BA7-AD25EFC6A8CD}

##### wrap {#JSSEC-GUID-F034E83C-1CA8-49E5-8BA7-AD25EFC6A8CD .sect5}

<div>
The `wrap`{.codeph} method is the primary method for message exchanges.

The signature for the `wrap`{.codeph} method called by
`SampleClient`{.codeph} is the following:

``` {.oac_no_warn dir="ltr"}
byte[] wrap (byte[] inBuf, int offset, interface len, 
                MessageProp msgProp)
```

You pass `wrap`{.codeph} a message (in `inBuf`{.codeph}), the offset
into `inBuf`{.codeph} where the message begins (`offset`{.codeph}), and
the length of the message (`len`{.codeph}). You also pass a
<span class="apiname">MessageProp</span>, which is used to indicate the
desired QOP (Quality-of-Protection) and to specify whether or not
privacy (encryption) is desired. A QOP value selects the cryptographic
integrity and encryption (if requested) algorithm(s) to be used. The
algorithms corresponding to various QOP values are specified by the
provider of the underlying mechanism. For example, the values for
Kerberos V5 are defined in [RFC
1964](http://www.ietf.org/rfc/rfc1964.txt) in section 4.2. It is common
to specify 0 as the QOP value to request the default QOP.

The `wrap`{.codeph} method returns a token containing the message and a
cryptographic Message Integrity Code (MIC) over it. The message placed
in the token will be encrypted if the
<span class="apiname">MessageProp</span> indicates privacy is desired.
You do not need to know the format of the returned token; it should be
treated as opaque data. You send the returned token to your peer
application, which calls the `unwrap`{.codeph} method to \"unwrap\" the
token to get the original message and to verify its integrity.

</div>
</div>
<div class="sect5">
[]{#GUID-A722F5F0-0B1D-43DE-A65B-0830999C89D0}

##### getMIC {#JSSEC-GUID-A722F5F0-0B1D-43DE-A65B-0830999C89D0 .sect5}

<div>
If you simply want to get a token containing a cryptographic Message
Integrity Code (MIC) for a supplied message, you call `getMIC`{.codeph}.
A sample reason you might want to do this is to confirm with your peer
that you both have the same data, by just transporting a MIC for that
data without incurring the cost of transporting the data itself to each
other.

The signature for the `getMIC`{.codeph} method called by
`SampleServer`{.codeph} is the following:

``` {.oac_no_warn dir="ltr"}
byte[] getMIC (byte[] inMsg, int offset, int len,
            MessageProp msgProp)
```

You pass `getMIC`{.codeph} a message (in `inMsg`{.codeph}), the offset
into `inMsg`{.codeph} where the message begins (`offset`{.codeph}), and
the length of the message (`len`{.codeph}). You also pass a
<span class="apiname">MessageProp</span>, which is used to indicate the
desired QOP (Quality-of-Protection). It is common to specify 0 as the
QOP value to request the default QOP.

If you have a token created by `getMIC`{.codeph} and the message used to
calculate the MIC (or a message purported to be the message on which the
MIC was calculated), you can call the `verifyMIC`{.codeph} method to
verify the MIC for the message. If the verification is successful (that
is, if a <span class="apiname">GSSException</span> is not thrown), it
proves that the message is exactly the same as it was when the MIC was
calculated. A peer receiving a message from an application typically
expects a MIC as well, so that they can verify the MIC and be assured
the message has not been modified or corrupted in transit. Note: If you
know ahead of time that you will want the MIC as well as the message
then it is more convenient to use the `wrap`{.codeph} and
`unwrap`{.codeph} methods. But there could be situations where the
message and the MIC are received separately.

The signature for the `verifyMIC`{.codeph} corresponding to the
`getMIC`{.codeph} shown above is the following:

``` {.oac_no_warn dir="ltr"}
void verifyMIC (byte[] inToken, int tokOffset, int tokLen,
        byte[] inMsg, int msgOffset, int msgLen,
        MessageProp msgProp);
```

This verifies the MIC contained in the `inToken`{.codeph} (of length
`tokLen`{.codeph}, starting at offset `tokOffset`{.codeph}) over the
message contained in `inMsg`{.codeph} (of length `msgLen`{.codeph},
starting at offset `msgOffset`{.codeph}). The
<span class="apiname">MessageProp</span> is used by the underlying
mechanism to return information to the caller, such as the QOP
indicating the strength of protection that was applied to the message.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-D929F2E0-8AD5-46A3-8A1F-7C30ACE5675B}

#### The SampleClient and SampleServer Message Exchanges {#JSSEC-GUID-D929F2E0-8AD5-46A3-8A1F-7C30ACE5675B .sect4}

<div>
The message exchanges between SampleClient and SampleServer are
summarized below, followed by the coding details.

These steps are the \"standard\" steps used for verifying a GSS-API
client and server. A group at MIT has written a GSS-API client and a
GSS-API server that have become fairly popular test programs for
checking interoperability between different implementations of the
GSS-API library. (These GSS-API sample applications can be downloaded as
a part of the Kerberos distribution available from MIT at
[http://web.mit.edu/kerberos](http://web.mit.edu/kerberos/).) This
client and server from MIT follow the protocol that once the context is
established, the client sends a message across and it expects back the
MIC on that message. If you implement a GSS-API library, it is common
practice to test it by running either the client or server using your
library implementation against a corresponding peer server or client
that uses another GSS-API library implementation. If both library
implementations conform to the standards, then the two peers will be
able to communicate successfully.

One implication of testing your client or server against ones written in
C (like the MIT ones) is the way tokens must be exchanged. C
implementations of GSS-API do not include stream-based methods. In the
absence of stream-based methods on your peer, when you write a token you
must first write the number of bytes and then write the token.
Similarly, when you are reading a token, you first read the number of
bytes and then read the token. This is what `SampleClient`{.codeph} and
`SampleServer`{.codeph} do.

Here is the summary of the `SampleClient`{.codeph} and
`SampleServer`{.codeph} message exchanges:

1.  `SampleClient`{.codeph} calls `wrap`{.codeph} to encrypt and
    calculate a MIC for a message.
2.  `SampleClient`{.codeph} sends the token returned from
    `wrap`{.codeph} to `SampleServer`{.codeph}.
3.  `SampleServer`{.codeph} calls `unwrap`{.codeph} to obtain the
    original message and verify its integrity.
4.  `SampleServer`{.codeph} calls `getMIC`{.codeph} to calculate a MIC
    on the decrypted message.
5.  `SampleServer`{.codeph} sends the token returned by
    `getMIC`{.codeph} (which contains the MIC) to
    `SampleClient`{.codeph}.
6.  `SampleClient`{.codeph} calls `verifyMIC`{.codeph} to verify that
    the MIC sent by `SampleServer`{.codeph} is a valid MIC for the
    original message.

</div>
<div class="sect5">
[]{#GUID-BDB7693C-A999-4CDC-BEF1-9D3A207085F9}

##### SampleClient Code to Encrypt the Message and Send It {#JSSEC-GUID-BDB7693C-A999-4CDC-BEF1-9D3A207085F9 .sect5}

<div>
The `SampleClient`{.codeph} code for encrypting a message, calculating a
MIC for it, and sending the result to `SampleServer`{.codeph} is the
following:

``` {.oac_no_warn dir="ltr"}
byte[] messageBytes = "Hello There!\0".getBytes();

/*
 * The first MessageProp argument is 0 to request
 * the default Quality-of-Protection.
 * The second argument is true to request
 * privacy (encryption of the message).
 */
MessageProp prop =  new MessageProp(0, true);

/*
 * Encrypt the data and send it across. Integrity protection
 * is always applied, irrespective of encryption.
 */
token = context.wrap(messageBytes, 0, messageBytes.length, 
    prop);
System.out.println("Will send wrap token of size " 
    + token.length);
outStream.writeInt(token.length);
outStream.write(token);
outStream.flush();
```

</div>
</div>
<div class="sect5">
[]{#GUID-39C5FDB4-97B8-4132-9197-9C58F838F4C9}

##### SampleServer Code to Unwrap Token, Calculate MIC, and Send It {#JSSEC-GUID-39C5FDB4-97B8-4132-9197-9C58F838F4C9 .sect5}

<div>
The following `SampleServer`{.codeph} code reads the wrapped token sent
by `SampleClient`{.codeph} and \"unwraps\" it to obtain the original
message and have its integrity verified. The unwrapping in this case
includes decryption since the message was encrypted.

<div class="infoboxnote" id="GUID-39C5FDB4-97B8-4132-9197-9C58F838F4C9__GUID-B372F294-8EDD-481C-A627-E64C7D79147F">
Note:

Here, the integrity check is expected to succeed. But note that in
general if an integrity check fails, it signifies that the message was
changed in transit. If the `unwrap`{.codeph} method encounters an
integrity check failure, it throws a
<span class="apiname">GSSException</span> with major error code
<span class="apiname">GSSException.BAD\_MIC</span>.

</div>
``` {.oac_no_warn dir="ltr"}
/*
 * Create a MessageProp which unwrap will use to return 
 * information such as the Quality-of-Protection that was 
 * applied to the wrapped token, whether or not it was 
 * encrypted, etc. Since the initial MessageProp values
 * are ignored, it doesn't matter what they are set to.
 */
MessageProp prop = new MessageProp(0, false);

/* 
 * Read the token. This uses the same token byte array 
 * as that used during context establishment.
 */
token = new byte[inStream.readInt()];
System.out.println("Will read token of size " 
    + token.length);
inStream.readFully(token);

byte[] bytes = context.unwrap(token, 0, token.length, prop);
String str = new String(bytes);
System.out.println("Received data \""
    + str + "\" of length " + str.length());
System.out.println("Encryption applied: "
    + prop.getPrivacy());
```

Next, `SampleServer`{.codeph} generates a MIC for the decrypted message
and sends it to `SampleClient`{.codeph}. This is not really necessary
but simply illustrates generating a MIC on the decrypted message, which
should be exactly the same as the original message
`SampleClient`{.codeph} wrapped and sent to `SampleServer`{.codeph}.
When `SampleServer`{.codeph} generates this and sends it to
`SampleClient`{.codeph}, and `SampleClient`{.codeph} verifies it, this
proves to `SampleClient`{.codeph} that the decrypted message
`SampleServer`{.codeph} has is in fact exactly the same as the original
message from `SampleClient`{.codeph}.

``` {.oac_no_warn dir="ltr"}
/*
 * First reset the QOP of the MessageProp to 0
 * to ensure the default Quality-of-Protection
 * is applied.
 */
prop.setQOP(0);

token = context.getMIC(bytes, 0, bytes.length, prop);

System.out.println("Will send MIC token of size " 
                   + token.length);
outStream.writeInt(token.length);
outStream.write(token);
outStream.flush();
```

</div>
</div>
<div class="sect5">
[]{#GUID-FF93FB73-B91B-489A-807F-577939ACE8A6}

##### SampleClient Code to Verify the MIC {#JSSEC-GUID-FF93FB73-B91B-489A-807F-577939ACE8A6 .sect5}

<div>
The following `SampleClient`{.codeph} code reads the MIC calculated by
`SampleServer`{.codeph} on the decrypted message and then verifies that
the MIC is a MIC for the original message, proving that the decrypted
message `SampleServer`{.codeph} has is the same as the original message:

``` {.oac_no_warn dir="ltr"}
token = new byte[inStream.readInt()];
System.out.println("Will read token of size " + token.length);
inStream.readFully(token);

/* 
 * Recall messageBytes is the byte array containing
 * the original message and prop is the MessageProp 
 * already instantiated by SampleClient.
 */
context.verifyMIC(token, 0, token.length, 
          messageBytes, 0, messageBytes.length,
          prop);

System.out.println("Verified received MIC for message.");
```

</div>
</div>
</div>
</div>
<div class="sect3">
[]{#GUID-DA54B317-30B2-4666-86B6-B1AD4D627002}

### Clean Up {#JSSEC-GUID-DA54B317-30B2-4666-86B6-B1AD4D627002 .sect3}

<div>
When `SampleClient`{.codeph} and `SampleServer`{.codeph} have finished
exchanging messages, they need to perform cleanup operations. Both
contain the following code to

-   close the socket connection and

-   release system resources and cryptographic information stored in the
    context object and then invalidate the context.

    ``` {.oac_no_warn dir="ltr"}
    socket.close();
    context.dispose();
    ```

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-6D82A7D2-C406-40F4-838A-42ED61194182}

Kerberos User and Service Principal Names {#JSSEC-GUID-6D82A7D2-C406-40F4-838A-42ED61194182 .sect2}
-----------------------------------------

<div>
Since the underlying authentication and secure communication technology
used by this tutorial is Kerberos V5, we use Kerberos-style principal
names wherever a user or service is called for (see
[Principals](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-8FAF9739-CD62-4A47-9582-884DBF3081F0)).

For example, when you run `SampleClient`{.codeph} you are asked to
provide your <span class="bold">user name</span>. Your Kerberos-style
user name is simply the user name you were assigned for Kerberos
authentication. It consists of a base user name (like `mjones`{.codeph})
followed by an \"`@`{.codeph}\" and your realm (like
`mjones@KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}).

A server program like `SampleServer`{.codeph} is typically considered to
offer a \"service\" and to be run on behalf of a particular
\"<span class="bold">service principal</span>.\" A service principal
name for `SampleServer`{.codeph} is needed in several places:

-   When you run `SampleServer`{.codeph}, and `SampleClient`{.codeph}
    attempts a connection to it, the underlying Kerberos mechanism will
    attempt to authenticate to the Kerberos KDC. It prompts you to log
    in. You should log in as the appropriate service principal.
-   When you run `SampleClient`{.codeph}, one of the arguments is the
    service principal name. This is needed so `SampleClient`{.codeph}
    can initiate establishment of a security context with the
    appropriate service.
-   If the `SampleClient`{.codeph} and `SampleServer`{.codeph} programs
    were run with a security manager (they\'re not for this tutorial),
    the client and server policy files would each require a
    <span class="apiname">ServicePermission</span> with name equal to
    the service principal name and action equal to \"initiate\" or
    \"accept\" (for initiating or accepting establishment of a security
    context).

Throughout this document, and in the accompanying login configuration
file, `service_principal@your_realm`{.codeph}, is used as a placeholder
to be replaced by the actual name to be used in your environment.
<span class="italic">Any</span> Kerberos principal can actually be used
for the service principal name. So <span class="bold">for the purposes
of trying out this tutorial, you could use your user name as both the
client user name and the service principal name.</span>

In a production environment, system administrators typically like
servers to be run as specific principals only and may assign a
particular name to be used. Often the Kerberos-style service principal
name assigned is of the form

``` {.oac_no_warn dir="ltr"}
service_name/machine_name@realm;
```

For example, an nfs service run on a machine named `raven`{.codeph} in
the realm named `KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph} could have the
service principal name

``` {.oac_no_warn dir="ltr"}
nfs/raven@KRBNT-OPERATIONS.EXAMPLE.COM
```

Such multi-component names are not required, however. Single-component
names, just like those of user principals, can be used. For example, an
installation might use the same ftp service principal
`ftp@realm`{.codeph} for all ftp servers in that realm, while another
installation might have different ftp principals for different ftp
servers, such as `ftp/host1@realm`{.codeph} and
`ftp/host2@realm`{.codeph} on machines `host1`{.codeph} and
`host2`{.codeph}, respectively.

</div>
<div class="sect3">
[]{#GUID-B2F0BDD6-C35F-4B99-8AC3-60F0FCD351DF}

### When the Realm Is Required in Principal Names {#JSSEC-GUID-B2F0BDD6-C35F-4B99-8AC3-60F0FCD351DF .sect3}

<div>
If the realm of a user or service principal name is the default realm
(see [Kerberos
Requirements](kerberos-requirements1.html#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998)),
you can leave off the realm when you are logging into Kerberos (that is,
when you are prompted for your user name). Thus, for example, if your
user name is `mjones@KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}, and you run
`SampleClient`{.codeph}, when it requests your user name you could just
specify `mjones`{.codeph}, leaving off the realm. The name is
interpreted in the context of being a Kerberos principal name and the
default realm is appended, as needed.

You can also leave off the realm if a principal name will be converted
to a <span class="apiname">GSSName</span> by a
<span class="apiname">GSSManager</span> `createName`{.codeph} method.
For example, when you run `SampleClient`{.codeph}, one of the arguments
is the server service principal name. You can specify the name without
including the realm, because `SampleClient`{.codeph} passes the name to
such a `createName`{.codeph} method, which appends the default realm as
needed.

It is recommended that you always include realms when principal names
are used in login configuration files and policy files, because the
behavior of the parsers for such files may be implementation-dependent;
they may or may not append the default realm before such names are
utilized and subsequent actions may fail if there is no realm in the
name.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-2ED6C724-87F1-49EB-9015-32E6E74E3C6A}

The Login Configuration File {#JSSEC-GUID-2ED6C724-87F1-49EB-9015-32E6E74E3C6A .sect2}
----------------------------

<div>
For this tutorial, we are letting the underlying Kerberos mechanism
obtain credentials of the users running `SampleClient`{.codeph} and
`SampleServer`{.codeph}, rather than invoking JAAS methods directly (as
in the [JAAS
Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
and [JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F)
tutorials) or indirectly (for example, via the Login utility described
in the [Use of JAAS Login
Utility](use-jaas-login-utility.html#GUID-F41E74DF-EE54-4EB1-8609-49C6D324ADF5)
tutorial and in the [Use of JAAS Login Utility and Java GSS-API for
Secure Message
Exchanges](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8)
tutorial).

The default Kerberos mechanism implementation supplied by Oracle
actually prompts for a Kerberos name and password and authenticates the
specified user (or service) to the Kerberos KDC. The mechanism relies on
JAAS to perform this authentication.

JAAS supports a pluggable authentication framework, meaning that any
type of authentication module can be plugged under a calling
application. A login configuration specifies the login module to be used
for a particular application. The default JAAS implementation from
Oracle requires that the login configuration information be specified in
a file. (Note: Some other vendors might not have file-based
implementations.) See [Appendix B: JAAS Login Configuration
File](appendix-b-jaas-login-configuration-file.html#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)
for information as to what a login configuration file is, what it
contains, and how to specify which login configuration file should be
used.

For this tutorial, the Kerberos login module
`com.sun.security.auth.module.Krb5LoginModule`{.codeph} is specified in
the configuration file. This login module prompts for a Kerberos name
and password and attempts to authenticate to the Kerberos KDC.

Both `SampleClient`{.codeph} and `SampleServer`{.codeph} can use the
same login configuration file, if that file contains two entries, one
entry for the client side and one for the server side.

The
[`bcsLogin.conf`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__BCSLOGIN.CONF-3389212B)
login configuration file used for this tutorial is the following:

``` {.oac_no_warn dir="ltr"}
com.sun.security.jgss.initiate  {
  com.sun.security.auth.module.Krb5LoginModule required;
};

com.sun.security.jgss.accept  {
  com.sun.security.auth.module.Krb5LoginModule required storeKey=true 
};
```

Entries with these two names (`com.sun.security.jgss.initiate`{.codeph}
and `com.sun.security.jgss.accept`{.codeph}) are used by Oracle
implementations of GSS-API mechanisms when they need new credentials.
Since the mechanism used in this tutorial is the Kerberos V5 mechanism,
a Kerberos login module will need to be invoked in order to obtain these
credentials. Thus we list
[<span class="apiname">Krb5LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/Krb5LoginModule.html)
as a required module in these entries. The
`com.sun.security.jgss.initiate`{.codeph} entry specifies the
configuration for the client side and the
`com.sun.security.jgss.accept`{.codeph} entry for the server side.

The <span class="apiname">Krb5LoginModule</span> succeeds only if the
attempt to log in to the Kerberos KDC as a specified entity is
successful. When running `SampleClient`{.codeph} or
`SampleServer`{.codeph}, the user will be prompted for a name and
password.

The `SampleServer`{.codeph} entry
<span class="bold">`storeKey=true`{.codeph}</span> indicates that a
secret key should be calculated from the password provided during login
and it should be stored in the private credentials of the
<span class="apiname">Subject</span> created as a result of login. This
key is subsequently utilized during mutual authentication when
establishing a security context between `SampleClient`{.codeph} and
`SampleServer`{.codeph}.

The
[<span class="apiname">Krb5LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/Krb5LoginModule.html)
Javadoc API documentation describes the configuration options that the
<span class="apiname">Krb5LoginModule</span> class supports.

</div>
</div>
<div class="sect2">
[]{#GUID-841EB74E-3B52-4421-BC10-FE3C8511E007}

The useSubjectCredsOnly System Property {#JSSEC-GUID-841EB74E-3B52-4421-BC10-FE3C8511E007 .sect2}
---------------------------------------

<div>
For this tutorial, we set the system property
`javax.security.auth.useSubjectCredsOnly`{.codeph} to `false`{.codeph},
which allows us to relax the usual restriction of requiring a GSS
mechanism to obtain necessary credentials from an existing
[Subject](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3),
set up by JAAS. When this restriction is relaxed, it allows the
mechanism to obtain credentials from some vendor-specific location. For
example, some vendors might choose to use the operating system\'s cache
if one exists, while others might choose to read from a protected file
on disk.

When this restriction is relaxed, Oracle\'s Kerberos mechanism still
looks for the credentials in the Subject associated with the thread\'s
access control context, but if it doesn\'t find any there, it performs
JAAS authentication using a Kerberos module to obtain new ones. The
Kerberos module prompts you for a Kerberos principal name and password.
Note that Kerberos mechanism implementations from other vendors may
behave differently when this property is set to `false`{.codeph}.
Consult their documentation to determine their implementation\'s
behavior.

</div>
</div>
<div class="sect2">
[]{#GUID-DC1FCD2D-101C-4EF2-8034-387CBE66FA3E}

Running the SampleClient and SampleServer Programs {#JSSEC-GUID-DC1FCD2D-101C-4EF2-8034-387CBE66FA3E .sect2}
--------------------------------------------------

<div>
To execute the `SampleClient`{.codeph} and `SampleServer`{.codeph}
programs, do the following:

-   [Prepare SampleServer for
    Execution](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-758C5F29-2F6A-420B-9BFA-FA741149F3B6)
-   [Prepare SampleClient for
    Execution](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-2D1E8C81-221C-44CC-9B86-7A41C7DCA44B)
-   [Execute
    SampleServer](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-9D61C2A9-1E0D-4701-8FBF-F5D31AA4BB2C)
-   [Execute
    SampleClient](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-9AF3C84A-CB43-4F4B-A09D-445D8741FE59)

</div>
<div class="sect3">
[]{#GUID-758C5F29-2F6A-420B-9BFA-FA741149F3B6}

### Prepare SampleServer for Execution {#JSSEC-GUID-758C5F29-2F6A-420B-9BFA-FA741149F3B6 .sect3}

<div>
To prepare `SampleServer`{.codeph} for execution, do the following:

1.  Copy the following files into a directory accessible by the machine
    on which you will run `SampleServer`{.codeph}:
    -   The
        [`SampleServer.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLESERVER.JAVA-33891DED)
        source file.
    -   The
        [`bcsLogin.conf`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__BCSLOGIN.CONF-3389212B)
        login configuration file.
2.  Compile `SampleServer.java`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    javac SampleServer.java
    ```

</div>
</div>
<div class="sect3">
[]{#GUID-2D1E8C81-221C-44CC-9B86-7A41C7DCA44B}

### Prepare SampleClient for Execution {#JSSEC-GUID-2D1E8C81-221C-44CC-9B86-7A41C7DCA44B .sect3}

<div>
To prepare `SampleClient`{.codeph} for execution, do the following:

1.  Copy the following files into a directory accessible by the machine
    on which you will run `SampleClient`{.codeph}:
    -   The
        [`SampleClient.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLECLIENT.JAVA-338923E1)
        source file.
    -   The
        [`bcsLogin.conf`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__BCSLOGIN.CONF-3389212B)
        login configuration file.
2.  Compile `SampleClient.java`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    javac SampleClient.java
    ```

</div>
</div>
<div class="sect3">
[]{#GUID-9D61C2A9-1E0D-4701-8FBF-F5D31AA4BB2C}

### Execute SampleServer {#JSSEC-GUID-9D61C2A9-1E0D-4701-8FBF-F5D31AA4BB2C .sect3}

<div>
It is important to execute `SampleServer`{.codeph} before
`SampleClient`{.codeph} because `SampleClient`{.codeph} will try to make
a socket connection to `SampleServer`{.codeph} and that will fail if
`SampleServer`{.codeph} is not yet running and accepting socket
connections.

To execute `SampleServer`{.codeph}, be sure to run it on the machine it
is expected to be run on. This machine name (host name) is specified as
an argument to `SampleClient`{.codeph}. The service principal name
appears in several places, including the login configuration file and
the policy files.

Go to the directory in which you have prepared `SampleServer`{.codeph}
for execution. Execute `SampleServer`{.codeph}, specifying

-   by `-Djava.security.krb5.realm=<your_realm>`{.codeph} that your
    Kerberos realm is the one specified.

    For example, if your realm is
    `KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph} you\'d put
    `-Djava.security.krb5.realm=KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}.

-   by `-Djava.security.krb5.kdc=<your_kdc>`{.codeph} that your Kerberos
    KDC is the one specified.

    For example, if your KDC is `samplekdc.example.com`{.codeph}you\'d
    put `-Djava.security.krb5.kdc=samplekdc.example.com`{.codeph}.

-   by `-Djavax.security.auth.useSubjectCredsOnly=false`{.codeph} that
    the underlying mechanism can decide how to get credentials. See [The
    useSubjectCredsOnly System
    Property](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-841EB74E-3B52-4421-BC10-FE3C8511E007).

-   by `-Djava.security.auth.login.config=bcsLogin.conf`{.codeph} that
    the login configuration file to be used is `bcsLogin.conf`{.codeph}.

The only argument required by `SampleServer`{.codeph} is one specifying
the port number to be used for listening for client connections. Choose
a high port number unlikely to be used for anything else. An example
would be something like 4444.

Below is the full command to use for both Microsoft Windows and Solaris,
Linux, and macOS systems.

<div class="infoboxnote" id="GUID-9D61C2A9-1E0D-4701-8FBF-F5D31AA4BB2C__GUID-ADC9E59B-57DF-47DA-890F-4DCC371D84D1">
Note:

<span class="bold">Important: In this command, you must replace
`<port_number>`{.codeph} with an appropriate port number,
`<your_realm>`{.codeph} with your Kerberos realm, and
`<your_kdc>`{.codeph} with your Kerberos KDC.</span>

The `java.security.krb5.kdc`{.codeph} system property interprets the
\":\" symbol as a separation character for multiple KDCs. If the KDC is
not listening on the default port (88), you must provide the default
realm and its KDC(s) in a `krb5.conf` file, then set the system property
`java.security.krb5.kdc.conf`{.codeph} with the name of this file:

``` {.oac_no_warn dir="ltr"}
-Djava.security.krb5.conf=<your_krb5.conf_file>
```

</div>
Here is the command:

``` {.oac_no_warn dir="ltr"}
java -Djava.security.krb5.realm=<your_realm> 
 -Djava.security.krb5.kdc=<your_kdc> 
 -Djavax.security.auth.useSubjectCredsOnly=false
 -Djava.security.auth.login.config=bcsLogin.conf 
 SampleServer <port_number>
```

The full command should appear on one line (or, on Solaris, Linux, or
macOS, on multiple lines where each line but the last is terminated with
\" \\\" indicating that there is more to come). Multiple lines are used
here just for legibility. Since this command is very long, you may need
to place it in a .bat file (for Windows) or a .sh file (for Solaris,
Linux, or macOS) and then run that file to execute the command.

The `SampleServer`{.codeph}</code> code will listen for socket
connections on the specified port. When prompted, type the Kerberos name
and password for the service principal. The underlying Kerberos
authentication mechanism specified in the login configuration file will
log the service principal into Kerberos.

For login troubleshooting suggestions, see
[Troubleshooting](troubleshooting.html#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

</div>
</div>
<div class="sect3">
[]{#GUID-9AF3C84A-CB43-4F4B-A09D-445D8741FE59}

### Execute SampleClient {#JSSEC-GUID-9AF3C84A-CB43-4F4B-A09D-445D8741FE59 .sect3}

<div>
To execute `SampleClient`{.codeph}, first go to the directory in which
you have prepared `SampleClient`{.codeph} for execution. Execute
`SampleClient`{.codeph}, specifying

-   by `-Djava.security.krb5.realm=<your_realm>`{.codeph} that your
    Kerberos realm is the one specified.
-   by `-Djava.security.krb5.kdc=<your_kdc>`{.codeph} that your Kerberos
    KDC is the one specified.
-   by `-Djavax.security.auth.useSubjectCredsOnly=false`{.codeph} that
    the underlying mechanism can decide how to get credentials.
-   by `-Djava.security.auth.login.config=bcsLogin.conf`{.codeph} that
    the login configuration file to be used is `bcsLogin.conf`{.codeph}.

The `SampleClient`{.codeph} arguments are (1) the Kerberos name of the
service principal that represents `SampleServer`{.codeph} (see [Kerberos
User and Service Principal
Names](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-6D82A7D2-C406-40F4-838A-42ED61194182),
(2) the name of the host (machine) on which `SampleServer`{.codeph} is
running, and (3) the port number on which `SampleServer`{.codeph} is
listening for client connections.

Below is the full command to use for both Windows and Solaris, Linux,
and macOS systems.

<div class="infoboxnote" id="GUID-9AF3C84A-CB43-4F4B-A09D-445D8741FE59__GUID-AC5953E8-06A3-4527-97BA-108C746A6B98">
Note:

<span class="bold">Important: In this command, you must replace
`<service_principal>`{.codeph}, `<host>`{.codeph},
`<port_number>`{.codeph}, `<your_realm>`{.codeph}, and
`<your_kdc>`{.codeph} with appropriate values</span> (and note that the
port number must be the same as the port number passed as an argument to
`SampleServer`{.codeph}). These values need not be placed in quotes.

</div>
Here is the command:

``` {.oac_no_warn dir="ltr"}
java -Djava.security.krb5.realm=<your_realm> 
 -Djava.security.krb5.kdc=<your_kdc> 
 -Djavax.security.auth.useSubjectCredsOnly=false
 -Djava.security.auth.login.config=bcsLogin.conf 
 SampleClient <service_principal> <host> <port_number>
```

Type the full command on one line. Multiple lines are used here for
legibility. As with the command for executing `SampleServer`{.codeph},
if the command is too long to type directly into your command window,
place it in a .bat file (Windows) or a .sh file (Solaris, Linux, and
macOS) and then execute that file.

When prompted, type your Kerberos user name and password. The underlying
Kerberos authentication mechanism specified in the login configuration
file will log you into Kerberos. The `SampleClient`{.codeph} code
requests a socket connection with `SampleServer`{.codeph}. Once
`SampleServer`{.codeph} accepts the connection, `SampleClient`{.codeph}
and `SampleServer`{.codeph} establish a shared context and then exchange
messages as described in this tutorial.

For login troubleshooting suggestions, see
[Troubleshooting](troubleshooting.html#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

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
| -------------- ----- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| ------------- --     | l | dcommon/gifs/toc.gif |
|                [![Pr | e | )\                   |
| evious](../../dcommo | L |             <span cl |
| n/gifs/leftnav.gif)\ | o | ass="icon">Contents< |
|                      | g | /span>](toc.htm)     |
|    [![Next](../../dc | o |   -- --------------- |
| ommon/gifs/rightnav. | ] | -------------------- |
| gif)\                | ( | -------------------- |
|    <span class="icon | . | ---                  |
| ">Previous</span>](w | . |                      |
| hen-use-java-gss-api | / |                      |
| -vs-jsse.htm)   <spa | . |                      |
| n class="icon">Next< | . |                      |
| /span>](jaas-authent | / |                      |
| ication.htm)         | d |                      |
|   ------------------ | c |                      |
| -------------------- | o |                      |
| -------------------- | m |                      |
| -------------- ----- | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| ------------- --     | / |                      |
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
