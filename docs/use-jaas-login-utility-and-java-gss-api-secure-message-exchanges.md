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

  ----------------------------------------------------------------- ----------------------------------------------------------------------------------- --
            [![Previous](../../dcommon/gifs/leftnav.gif)\                               [![Next](../../dcommon/gifs/rightnav.gif)\                      
   <span class="icon">Previous</span>](use-jaas-login-utility.htm)   <span class="icon">Next</span>](more-things-you-can-do-java-gss-api-and-jaas.htm)  
  ----------------------------------------------------------------- ----------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8}<!-- End Header -->

Use of JAAS Login Utility and Java GSS-API for Secure Message Exchanges {#JSSEC-GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8 .sect1}
=======================================================================

<div>
This tutorial presents two sample applications to demonstrate the use of
the Java GSS-API. This API permits secure exchanges of messages between
communicating applications. Here are the sample client and server
applications you\'ll need for this tutorial:

-   [`SampleClient.java`{.codeph}](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLECLIENT.JAVA-338923E1)
-   [`SampleServer.java`{.codeph}](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLESERVER.JAVA-33891DED)

<div class="infoboxnote" id="GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8__GUID-14947E17-44D9-4CE2-8A0F-922A12CFEC92">
Note:

This tutorial uses the same client and server applications as the [Use
of Java GSS-API for Secure Message Exchanges Without JAAS
Programming](use-java-gss-api-secure-message-exchanges-jaas-programming.htm#GUID-42A2B80C-90CD-4C7A-8EED-8BFFE83CAF56)
tutorial. In that tutorial, JAAS (Java Authentication and Authorization
Service) programming is not required. Instead, you let the underlying
mechanism decide how to get credentials.

</div>
This tutorial uses policy files and a more complex login configuration
file. The programs are run with a security manager; as a result,
security-sensitive operations are not allowed unless the required
permissions were explicitly granted. This tutorial also demonstrates how
JAAS authorization adds <span class="italic">user-centric</span> access
control that applies control based on <span class="italic">who</span> is
running the code -- not just on what code is running.

-   [Before You Start: Recommended
    Reading](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-A742F77E-9D77-42E1-BFB8-2DE9C6FB3051)
-   [Overview of the Client and Server
    Applications](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-1C2B6E45-2E2F-421C-B0D3-F034156DDAE7)
-   [Kerberos User and Service Principal
    Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80)
-   [The Login Configuration
    File](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-3B582CD5-135F-4516-843E-1831DB25CCC4)
-   [The Policy
    Files](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-2BA7F0B7-D3E3-4B81-8E98-0A39F9763B59)
-   [Running the SampleClient and SampleServer
    Programs](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-07D0C8CC-0922-4B0F-B14D-9A644CB13783)

</div>
<div class="sect2">
[]{#GUID-A742F77E-9D77-42E1-BFB8-2DE9C6FB3051}

Before You Start: Recommended Reading {#JSSEC-GUID-A742F77E-9D77-42E1-BFB8-2DE9C6FB3051 .sect2}
-------------------------------------

<div>
In this Java GSS-API tutorial, the first step is JAAS authentication.
Previous tutorials demonstrated the use of JAAS for user authentication
and authorization, and presented examples of policy files and of login
configuration files (specifying the underlying authentication technology
to be used) that JAAS requires. Applications in the JAAS introductory
tutorials, [JAAS
Authentication](jaas-authentication.htm#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
and [JAAS
Authorization](jaas-authorization.htm#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F),
made direct calls to JAAS methods. The [Use of JAAS Login
Utility](use-jaas-login-utility.htm#GUID-F41E74DF-EE54-4EB1-8609-49C6D324ADF5)
tutorial showed the use of a utility program that frees the application
from having to do this. The client and server applications in the
current tutorial also use the same utility program, so we recommend you
<span class="bold">read the login utility tutorial first</span>.

As with all tutorials in this series, the underlying technology used to
support authentication and secure communication for the applications in
this tutorial is Kerberos. See [Kerberos
Requirements](kerberos-requirements1.htm#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998).

</div>
</div>
<div class="sect2">
[]{#GUID-1C2B6E45-2E2F-421C-B0D3-F034156DDAE7}

Overview of the Client and Server Applications {#JSSEC-GUID-1C2B6E45-2E2F-421C-B0D3-F034156DDAE7 .sect2}
----------------------------------------------

<div>
The applications for this tutorial are named `SampleClient`{.codeph} and
`SampleServer`{.codeph}.

Each is invoked by executing the Login utility supplied with this
tutorial and passing it as arguments the name of the application
(`SampleClient`{.codeph} or `SampleServer`{.codeph}), followed by the
arguments needed by the application. The Login utility uses a JAAS
<span class="apiname">LoginContext</span> to authenticate the user using
Kerberos. Finally, the Login utility invokes the `main`{.codeph} method
of the application class, in our case either `SampleClient`{.codeph} or
`SampleServer`{.codeph}, and passes the application its arguments.

Here is a summary of execution of the `SampleClient`{.codeph} and
`SampleServer`{.codeph} applications:

1.  Run the `SampleServer`{.codeph} application by running the Login
    utility and passing it as arguments the name
    \"`SampleServer`{.codeph}\" followed by the arguments for the
    `SampleServer`{.codeph} program. The Login utility prompts you for
    the password for the principal that `SampleServer`{.codeph} should
    run as. (See [Kerberos User and Service Principal
    Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80).)
    After authentication is complete, `SampleServer`{.codeph} is run it:
    a.  Reads its argument, the port number that it should listen on for
        client connections.
    b.  Creates a <span class="apiname">ServerSocket</span> for
        listening for client connections on that port.
    c.  Listens for a connection.
2.  Run the `SampleClient`{.codeph} application (possibly on a different
    machine), by running the Login utility and passing it as arguments
    the name \"`SampleClient`{.codeph}\" followed by the arguments for
    the `SampleClient`{.codeph} program. The Login utility prompts you
    for your Kerberos name and password. After authentication is
    complete, `SampleClient`{.codeph} is run. It
    a.  Reads its arguments: (1) The name of the Kerberos principal that
        represents `SampleServer`{.codeph}. (See [Kerberos User and
        Service Principal
        Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80).), (2)
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
    a <span class="apiname">GSSContext</span> and establish a shared
    context that will enable subsequent secure data exchanges.
5.  `SampleClient`{.codeph} and `SampleServer`{.codeph} can now securely
    exchange messages.
6.  When `SampleClient`{.codeph} and `SampleServer`{.codeph} are done
    exchanging messages, they perform clean-up operations.

<div class="infoboxnote" id="GUID-1C2B6E45-2E2F-421C-B0D3-F034156DDAE7__GUID-FF74737A-36D0-4B2D-8625-D720121B8CE2">
Note:

</div>
Refer to the [The SampleClient and SampleServer
Code](use-java-gss-api-secure-message-exchanges-jaas-programming.htm#GUID-0DDC8ACE-7398-41C6-B061-CF3DEAB7AC86)
section of the [Use of Java GSS-API for Secure Message Exchanges Without
JAAS
Programming](use-java-gss-api-secure-message-exchanges-jaas-programming.htm#GUID-42A2B80C-90CD-4C7A-8EED-8BFFE83CAF56)
tutorial for a full discussion of the code used in this tutorial.

</div>
</div>
<div class="sect2">
[]{#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80}

Kerberos User and Service Principal Names {#JSSEC-GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80 .sect2}
-----------------------------------------

<div>
Since the underlying authentication and secure communication technology
used by this tutorial is Kerberos V5, we use Kerberos-style principal
names wherever a user or service is called for (see
[Principals](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-8FAF9739-CD62-4A47-9582-884DBF3081F0)).

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

-   When you run `SampleServer`{.codeph} you must log in as the
    appropriate service principal. The login configuration file for this
    tutorial actually specifies the service principal name (as an option
    to the <span class="apiname">Krb5LoginModule</span>), so the JAAS
    authentication (done by the <span class="apiname">Login</span>
    utility) just asks you to specify the password for that service
    principal. If you specify the correct password, the authentication
    is successful, a <span class="apiname">Subject</span> is created
    containing a <span class="apiname">Principal</span> with the service
    principal name, and that <span class="apiname">Subject</span> is
    associated with a new access control context. The
    subsequently-executed code (the `SampleServer`{.codeph} code) is
    considered to be executed on behalf of the specified principal.
-   When you run `SampleClient`{.codeph}, one of the arguments is the
    service principal name. This is needed so `SampleClient`{.codeph}
    can initiate establishment of a security context with the
    appropriate service.
-   The client and server policy files each require a
    <span class="apiname">ServicePermission</span> with name equal to
    the service principal name and action equal to \"initiate\" or
    \"accept\" (for initiating or accepting establishment of a security
    context).

Throughout this document, and in the accompanying login configuration
file and policy files, `service_principal@your_realm`{.codeph} is used
as a placeholder to be replaced by the actual name to be used in your
environment. <span class="italic">Any</span> Kerberos principal can
actually be used for the service principal name. So
<span class="bold">for the purposes of trying out this tutorial, you
could use your user name as both the client user name and the service
principal name.</span>

In a production environment, system administrators typically like
servers to be run as specific principals only and may assign a
particular name to be used. Often the Kerberos-style service principal
name assigned is of the form

``` {.oac_no_warn dir="ltr"}
service_name/machine_name@realm; 
```

For example, an nfs service run on a machine named \"raven\" in the
realm named `KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph} could have the
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
[]{#GUID-E863F99A-77AC-4BE8-BAC1-A7B2E77FE775}

### When the Realm is Required in Principal Names {#JSSEC-GUID-E863F99A-77AC-4BE8-BAC1-A7B2E77FE775 .sect3}

<div>
If the realm of a user or service principal name is the default realm
(see [Kerberos
Requirements](kerberos-requirements1.htm#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998)),
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
[]{#GUID-3B582CD5-135F-4516-843E-1831DB25CCC4}

The Login Configuration File {#JSSEC-GUID-3B582CD5-135F-4516-843E-1831DB25CCC4 .sect2}
----------------------------

<div>
Whenever JAAS is used, a login configuration is required to specify the
desired authentication technology. (See [Appendix B: JAAS Login
Configuration
File](appendix-b-jaas-login-configuration-file.htm#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)
for more information about what a login configuration file is.) Both
`SampleClient`{.codeph} and `SampleServer`{.codeph} can use the same
login configuration file, if that file contains two entries, one entry
for the client side and one for the server side.

The
[`csLogin.conf`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__CSLOGIN.CONF-33894173)
login configuration file used for this tutorial is the following:

``` {.oac_no_warn dir="ltr"}
SampleClient {
  com.sun.security.auth.module.Krb5LoginModule required;
};

SampleServer {
  com.sun.security.auth.module.Krb5LoginModule required storeKey=true 
    principal="service_principal@your_realm";
};
```

Note that the name for each entry matches the respective class names for
our two top-level applications, `SampleClient`{.codeph} and
`SampleServer`{.codeph}. Recall that this is also the name that is
passed to the Login utility that performs JAAS operations for the
application. That utility expects the name of the entry to be looked up
in your login configuration file to be the same as the name it is
passed.

Both entries specify that Oracle\'s Kerberos V5 LoginModule must be used
to successfully authenticate the user. The Krb5LoginModule succeeds only
if the attempt to log in to the Kerberos KDC as a specified entity is
successful. In the case of `SampleClient`{.codeph}, the user will be
prompted for their name and password. In the case of
`SampleServer`{.codeph}, a name is already supplied in this login
configuration file (the specified principal, as described below) and the
user running `SampleServer`{.codeph} is just asked for the password for
the entity specified by that name. They must specify the correct
password in order for authentication to succeed.

The `SampleServer`{.codeph} entry
<span class="bold">`storeKey=true`{.codeph}</span> indicates that a
secret key should be calculated from the password provided during login
and it should be stored in the private credentials of the
<span class="apiname">Subject</span> created as a result of login. This
key is subsequently utilized during mutual authentication when
establishing a security context between `SampleClient`{.codeph} and
`SampleServer`{.codeph}.

The <span class="apiname">Krb5LoginModule</span> has a
<span class="bold">`principal`{.codeph}</span> option that can be used
to specify that only the specified principal (entity/user) should be
logged in for the given program. Here, the `SampleClient`{.codeph} entry
does not specify a principal (although it could, if desired), so the
user is prompted for a user name and password and anyone with a valid
user name and password can run `SampleClient`{.codeph}.
`SampleServer`{.codeph}, on the other hand, indicates a particular
principal because system administrators usually like servers to be run
as specific principals only. In this case, the user running
`SampleServer`{.codeph} is prompted for that principal\'s password and
must supply the correct one in order for authentication to succeed.

Note that you must replace `service_principal@your_realm`{.codeph} with
the name of the service principal that represents
`SampleServer`{.codeph}. (See [Kerberos User and Service Principal
Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80).)

If the server has a keytab file containing secret keys, then use the
following JAAS login entry:

``` {.oac_no_warn dir="ltr"}
SampleServer {
  com.sun.security.auth.module.Krb5LoginModule required
  principal="service_principal@your_realm"
  storeKey=true useKeyTab=true keyTab=keytab.file.name
  isInitiator=false;
};
```

Because the keytab file already provides the keys, you will not be
prompted for a password. If the keytab file contains keys for more than
one service principal and the server is designed to act as all these
service principals, then you can set the principal entry to the
following:

``` {.oac_no_warn dir="ltr"}
  principal=*
```

See the
[<span class="apiname">Krb5LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/Krb5LoginModule.html)
Javadoc API documentation for information about all the possible options
that can be passed to <span class="apiname">Krb5LoginModule</span>.

</div>
</div>
<div class="sect2">
[]{#GUID-2BA7F0B7-D3E3-4B81-8E98-0A39F9763B59}

The Policy Files {#JSSEC-GUID-2BA7F0B7-D3E3-4B81-8E98-0A39F9763B59 .sect2}
----------------

<div>
The policy file used when running `SampleClient`{.codeph} is
[`client.policy`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__CLIENT.POLICY-33894283),
and the policy file used when running `SampleServer`{.codeph} is
[`server.policy`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SERVER.POLICY-33894513).
Their contents are described below.

</div>
<div class="sect3">
[]{#GUID-6C3F477A-6245-48F1-B83F-3CCE8581197C}

### The Client Policy File {#JSSEC-GUID-6C3F477A-6245-48F1-B83F-3CCE8581197C .sect3}

<div>
</div>
<div class="sect4">
[]{#GUID-F5030E1B-C83F-4464-BD5C-D0D04051FF12}

#### Permissions Required by the Login Utility Classes {#JSSEC-GUID-F5030E1B-C83F-4464-BD5C-D0D04051FF12 .sect4}

<div>
A number of permissions are required by the classes in
`Login.java`{.codeph} (`Login`{.codeph} and `MyAction`{.codeph}). As
recommended in [Use of JAAS Login
Utility](use-jaas-login-utility.htm#GUID-F41E74DF-EE54-4EB1-8609-49C6D324ADF5)
on the use of the Login utility, we create a `Login.jar`{.codeph} JAR
file containing the `Login.class`{.codeph} and `MyAction.class`{.codeph}
files and in the `client.policy`{.codeph} policy file we grant
`Login.jar AllPermission`{.codeph}:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./Login.jar" {
   permission java.security.AllPermission;
};
```

</div>
</div>
<div class="sect4">
[]{#GUID-92A55C57-DA1F-492E-95F3-7FDCF84FCB34}

#### Permissions Required by SampleClient {#JSSEC-GUID-92A55C57-DA1F-492E-95F3-7FDCF84FCB34 .sect4}

<div>
The `SampleClient`{.codeph} code does two types of operations for which
permissions are required. It

-   opens a socket connection with the host machine running the
    `SampleServer`{.codeph} application.
-   initiates establishment of a security context with
    `SampleServer`{.codeph}.

The permission required to open a socket connection is

``` {.oac_no_warn dir="ltr"}
permission java.net.SocketPermission "*", "connect";
```

You may replace the \"\*\" with the hostname or IP address of the
machine that `SampleServer`{.codeph} will be running on.

The permission(s) required to initiate establishment of a security
context will depend on the underlying mechanism. This tutorial uses
Kerberos as the underlying mechanism, and for that two
`javax.security.auth.kerberos.ServicePermission`{.codeph}s are required.
A <span class="apiname">ServicePermission</span> contains a service
principal name and an action (or list of actions). To initiate
establishment of a security context, you need two
<span class="apiname">ServicePermissions</span> with action
\"initiate\", whose names specify:

-   the service principal name for the ticket granting service for your
    realm. Granting this permission essentially allows the use of
    Kerberos as a client.
-   the service principal name representing `SampleServer`{.codeph}.
    (See [Kerberos User and Service Principal
    Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80).)
    Granting this permission allows you to interact with the service,
    `SampleServer`{.codeph}, using Kerberos.

We want to grant the permissions to a specific authenticated user
executing `SampleClient`{.codeph}, so we specify both the
`SampleClient`{.codeph} code location (in `SampleClient.jar`{.codeph})
and a Principal designation indicating the user name and realm for the
user (you, the person who will run `SampleClient`{.codeph}). (See [How
Do You Make Principal-Based Policy File
Statements?](jaas-authorization.htm#GUID-80F0B546-1E95-457B-8EF7-5BB1519E20A4)
in [JAAS
Authorization](jaas-authorization.htm#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F)
for information on policy file `grant`{.codeph} statements that include
<span class="apiname">Principal</span> designations.)

Here is the basic form for the `grant`{.codeph} statement:

``` {.oac_no_warn dir="ltr"}
  grant CodeBase "file:./SampleClient.jar", 
    Principal javax.security.auth.kerberos.KerberosPrincipal 
        "your_user_name@your_realm" {

    permission java.net.SocketPermission "*", "connect";

    permission javax.security.auth.kerberos.ServicePermission
        "krbtgt/your_realm@your_realm", 
        "initiate";

    permission javax.security.auth.kerberos.ServicePermission
        "service_principal@your_realm", 
        "initiate";
};
```

You must substitute your Kerberos user name (complete with \"@\" and
realm) for `your_user_name@your_realm`{.codeph}. For example, if your
user name is <span class="apiname">mjones</span> and your realm is
<span class="apiname">KRBNT-OPERATIONS.EXAMPLE.COM</span>, you would use
<span class="apiname">mjones@KRBNT-OPERATIONS.EXAMPLE.COM</span>.

You must also substitute your realm in
<span class="apiname">krbtgt/your\_realm@your\_realm</span> and the
service principal name for the service principal representing the server
(see [Kerberos User and Service Principal
Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80)
for the service principal name for the service principal representing
the server for `service_principal@your_realm`{.codeph}. Suppose the
former is
<span class="apiname">krbtgt/KRBNT-OPERATIONS.EXAMPLE.COM@KRBNT-OPERATIONS.EXAMPLE.COM</span>
and the latter is
<span class="apiname">sample/raven.example.com@KRBNT-OPERATIONS.EXAMPLE.COM</span>,
and your user name is as specified in the previous paragraph. Then the
`grant`{.codeph} statement would be

``` {.oac_no_warn dir="ltr"}
grant CodeBase "file:./SampleClient.jar", 
    Principal javax.security.auth.kerberos.KerberosPrincipal 
        "mjones@KRBNT-OPERATIONS.EXAMPLE.COM" {

    permission java.net.SocketPermission "*", "connect";

    permission javax.security.auth.kerberos.ServicePermission
        "krbtgt/KRBNT-OPERATIONS.EXAMPLE.COM@KRBNT-OPERATIONS.EXAMPLE.COM", 
        "initiate";

    permission javax.security.auth.kerberos.ServicePermission
        "sample/raven.example.com@KRBNT-OPERATIONS.EXAMPLE.COM", 
        "initiate";
};
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-9126BE63-55A5-45C0-8EDC-89A65A83271D}

### The Server Policy File {#JSSEC-GUID-9126BE63-55A5-45C0-8EDC-89A65A83271D .sect3}

<div>
</div>
<div class="sect4">
[]{#GUID-D84DE593-D18A-49A6-BE6D-DD7F787527C9}

#### Permissions Required by the Login Utility Classes {#JSSEC-GUID-D84DE593-D18A-49A6-BE6D-DD7F787527C9 .sect4}

<div>
The `grant`{.codeph} statement in the server policy file for the Login
classes is exactly the same as the one in the client policy file, as
described in [Permissions Required by the Login Utility
Classes](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-F5030E1B-C83F-4464-BD5C-D0D04051FF12):

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./Login.jar" {
   permission java.security.AllPermission;
};
```

</div>
</div>
<div class="sect4">
[]{#GUID-D4D40063-566E-489E-AB13-C5B7ADA112B9}

#### Permissions Required by SampleServer {#JSSEC-GUID-D4D40063-566E-489E-AB13-C5B7ADA112B9 .sect4}

<div>
The `SampleServer`{.codeph} code does two types of operations for which
permissions are required. It

-   accepts socket connections.
-   accepts establishment of a security context, that is, it is the
    \"acceptor\" for security context establishment.

The permission required to accept socket connections is

``` {.oac_no_warn dir="ltr"}
permission java.net.SocketPermission "*", "accept";
```

You may replace the \"\*\" with the hostname or IP address of the
machine that `SampleClient`{.codeph} will be running on.

The permission required to accept establishment of a security context is

``` {.oac_no_warn dir="ltr"}
permission javax.security.auth.kerberos.ServicePermission
    "service_principal@your_realm", 
    "accept";
```

where `service_principal@your_realm`{.codeph} is the Kerberos name of
the service principal that represents `SampleServer`{.codeph} (see
[Kerberos User and Service Principal
Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80)).

We want to grant the permissions to a specific authenticated user
executing `SampleServer`{.codeph} (the service principal considered to
represent `SampleServer`{.codeph}), so we specify both the
`SampleServer`{.codeph} code location (in `SampleServer.jar`{.codeph})
and a Principal designation indicating the service principal. Suppose
this name is
`sample/raven.example.com@KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}. Then
the `grant`{.codeph} statement would be

``` {.oac_no_warn dir="ltr"}
  grant CodeBase "file:./SampleServer.jar" 
    Principal javax.security.auth.kerberos.KerberosPrincipal 
        "sample/raven.example.com@KRBNT-OPERATIONS.EXAMPLE.COM" {

    permission java.net.SocketPermission "*", "accept";

    permission javax.security.auth.kerberos.ServicePermission
        "sample/raven.example.com@KRBNT-OPERATIONS.EXAMPLE.COM", "accept";
};
```

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-07D0C8CC-0922-4B0F-B14D-9A644CB13783}

Running the SampleClient and SampleServer Programs {#JSSEC-GUID-07D0C8CC-0922-4B0F-B14D-9A644CB13783 .sect2}
--------------------------------------------------

<div>
To execute the `SampleClient`{.codeph} and `SampleServer`{.codeph}
programs, do the following:

-   [Prepare SampleServer for
    Execution](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-901B5429-D25C-4DAA-90BB-7665E3682D52)
-   [Prepare SampleClient for
    Execution](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-F72FA916-2507-479C-A2E3-89FCB25D0FE8)
-   [Execute
    SampleServer](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-70ADB0E1-E036-4E40-8289-66545AD90C2F)
-   [Execute
    SampleClient](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-19CC950B-FFCA-471A-918E-92559F556356)

</div>
<div class="sect3">
[]{#GUID-901B5429-D25C-4DAA-90BB-7665E3682D52}

### Prepare SampleServer for Execution {#JSSEC-GUID-901B5429-D25C-4DAA-90BB-7665E3682D52 .sect3}

<div>
To prepare `SampleServer`{.codeph} for execution, do the following:

1.  Copy the following files into a directory accessible by the machine
    on which you will run `SampleServer`{.codeph}:
    -   The
        [`Login.java`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__LOGIN.JAVA-338935D0)
        source file.
    -   The
        [`SampleServer.java`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLESERVER.JAVA-33891DED)
        source file.
    -   The
        [`csLogin.conf`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__CSLOGIN.CONF-33894173)
        login configuration file.
    -   The
        [`server.policy`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SERVER.POLICY-33894513)
        policy file.
2.  Replace `service_principal@your_realm`{.codeph} in
    `csLogin.conf`{.codeph} with the name of the service principal
    representing `SampleServer`{.codeph} (see [Kerberos User and Service
    Principal
    Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80)).
3.  In both places it appears, replace
    `service_principal@your_realm`{.codeph} in `server.policy`{.codeph}
    with the Kerberos name of the service principal that represents
    `SampleServer`{.codeph}. (The same name as that used in the login
    configuration file.)
4.  Compile `Login.java`{.codeph} and `SampleServer.java`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    javac Login.java SampleServer.java
    ```

    Note that `Login.java`{.codeph} contains two classes and thus
    compiling `Login.java`{.codeph} creates `Login.class`{.codeph} and
    `MyAction.class`{.codeph}.

5.  Create a JAR file named `Login.jar`{.codeph} containing
    `Login.class and MyAction.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf Login.jar Login.class MyAction.class
    ```

6.  Create a JAR file named `SampleServer.jar`{.codeph} containing
    `SampleServer.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf SampleServer.jar SampleServer.class
    ```

</div>
</div>
<div class="sect3">
[]{#GUID-F72FA916-2507-479C-A2E3-89FCB25D0FE8}

### Prepare SampleClient for Execution {#JSSEC-GUID-F72FA916-2507-479C-A2E3-89FCB25D0FE8 .sect3}

<div>
To prepare `SampleClient`{.codeph} for execution, do the following:

1.  Copy the following files into a directory accessible by the machine
    on which you will run `SampleClient`{.codeph}:
    -   The
        [`Login.java`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__LOGIN.JAVA-338935D0)
        source file.
    -   The
        [`SampleClient.java`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLECLIENT.JAVA-338923E1)
        source file.
    -   The
        [`csLogin.conf`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__CSLOGIN.CONF-33894173)
        login configuration file.
    -   The
        [`client.policy`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__CLIENT.POLICY-33894283)
        policy file.
2.  Replace parts of `client.policy`{.codeph}:
    -   replace `your_user_name@your_realm`{.codeph} with your user name
        and realm.
    -   replace `your_realm`{.codeph} in
        `krbtgt/your_realm@your_realm`{.codeph} with your realm.
    -   replace `service_principal@your_realm`{.codeph} with the
        Kerberos name of the service principal that represents
        `SampleServer`{.codeph} (see [Kerberos User and Service
        Principal
        Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80)).
3.  Compile `Login.java`{.codeph} and `SampleClient.java`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    javac Login.java SampleClient.java
    ```

4.  Create a JAR file named `Login.jar`{.codeph} containing
    `Login.class and MyAction.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf Login.jar Login.class MyAction.class
    ```

5.  Create a JAR file named `SampleClient.jar`{.codeph} containing
    `SampleClient.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf SampleClient.jar SampleClient.class
    ```

</div>
</div>
<div class="sect3">
[]{#GUID-70ADB0E1-E036-4E40-8289-66545AD90C2F}

### Execute SampleServer {#JSSEC-GUID-70ADB0E1-E036-4E40-8289-66545AD90C2F .sect3}

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
for execution. Execute the `Login`{.codeph} class, specifying

-   by an appropriate `-classpath`{.codeph} clause that classes should
    be searched for in the `Login.jar`{.codeph} and
    `SampleServer.jar`{.codeph} JAR files,
-   by `-Djava.security.manager`{.codeph} that a security manager should
    be installed,
-   by `-Djava.security.krb5.realm=<your_realm>`{.codeph} that your
    Kerberos realm is the one specified. For example, if your realm is
    `KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph} you\'d put
    `-Djava.security.krb5.realm=KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}.
-   by `-Djava.security.krb5.kdc=<your_kdc>`{.codeph} that your Kerberos
    KDC is the one specified. For example, if your KDC is
    `samplekdc.example.com`{.codeph} you\'d put
    `-Djava.security.krb5.kdc=samplekdc.example.com`{.codeph}.
-   by `-Djava.security.policy=server.policy`{.codeph} that the policy
    file to be used is `server.policy`{.codeph}, and
-   by `-Djava.security.auth.login.config=csLogin.conf`{.codeph} that
    the login configuration file to be used is `csLogin.conf`{.codeph}.

You pass the name of your application (in this case,
`SampleServer`{.codeph}) as an argument to Login. You then add as
arguments any arguments required by your application, which in the case
of `SampleServer`{.codeph} is a single argument specifying the port
number to be used for listening for client connections. Choose a high
port number unlikely to be used for anything else. An example would be
something like 4444.

Below are the full commands to use for Windows and Solaris, Linux, and
macOS. The only difference is that Windows you use semicolons to
separate class path items, while you use colons for that purpose on
Solaris, Linux, and macOS.

<div class="infoboxnote" id="GUID-70ADB0E1-E036-4E40-8289-66545AD90C2F__GUID-B539751A-F513-41FA-A623-134F1ABEEBD4">
Note:

<span class="bold">Important: In these commands, you must replace
`<port_number>`{.codeph} with an appropriate port number,
`<your_realm>`{.codeph} with your Kerberos realm, and
`<your_kdc>`{.codeph} with your Kerberos KDC.</span>

</div>
Here is the command for Windows:

``` {.oac_no_warn dir="ltr"}
java -classpath Login.jar;SampleServer.jar 
 -Djava.security.manager 
 -Djava.security.krb5.realm=<your_realm> 
 -Djava.security.krb5.kdc=<your_kdc> 
 -Djava.security.policy=server.policy 
 -Djava.security.auth.login.config=csLogin.conf 
 Login SampleServer <port_number>
```

Here is the command for Solaris, Linux, and macOS:

``` {.oac_no_warn dir="ltr"}
java -classpath Login.jar:SampleServer.jar 
 -Djava.security.manager 
 -Djava.security.krb5.realm=<your_realm>
 -Djava.security.krb5.kdc=<your_kdc> 
 -Djava.security.policy=server.policy 
 -Djava.security.auth.login.config=csLogin.conf 
 Login SampleServer <port_number>
```

Type the full command on one line. Multiple lines are used here for
legibility. If the command is too long for your system, you may need to
place it in a .bat file (for Windows) or a .sh file (for Solaris, Linux,
and macOS) and then run that file to execute the command.

You will be prompted for the Kerberos password for the service
principal. The underlying Kerberos authentication mechanism specified in
the login configuration file will log the service principal into
Kerberos. Once authentication is successfully completed, the
`SampleServer`{.codeph} code will be executed on behalf of the service
principal. It will listen for socket connections on the specified port.

For login troubleshooting suggestions, see
[Troubleshooting](troubleshooting.htm#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

</div>
</div>
<div class="sect3">
[]{#GUID-19CC950B-FFCA-471A-918E-92559F556356}

### Execute SampleClient {#JSSEC-GUID-19CC950B-FFCA-471A-918E-92559F556356 .sect3}

<div>
To execute `SampleClient`{.codeph}, go to the directory in which you
have prepared `SampleClient`{.codeph} for execution. Then execute the
`Login`{.codeph} class, specifying

-   by an appropriate `-classpath`{.codeph} clause that classes should
    be searched for in the `Login.jar`{.codeph} and
    `SampleClient.jar`{.codeph} JAR files,
-   by `-Djava.security.manager`{.codeph} that a security manager should
    be installed,
-   by `-Djava.security.krb5.realm=<your_realm>`{.codeph} that your
    Kerberos realm is the one specified.
-   by `-Djava.security.krb5.kdc=<your_kdc>`{.codeph} that your Kerberos
    KDC is the one specified.
-   by `-Djava.security.policy=client.policy`{.codeph} that the policy
    file to be used is `client.policy`{.codeph}, and
-   by `-Djava.security.auth.login.config=csLogin.conf`{.codeph} that
    the login configuration file to be used is `csLogin.conf`{.codeph}.

Pass to Login the name of your application (`SampleClient`{.codeph})
followed by the arguments required by `SampleClient`{.codeph}. The
`SampleClient`{.codeph} arguments are (1) the Kerberos name of the
service principal that represents `SampleServer`{.codeph} (see [Kerberos
User and Service Principal
Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80),
(2) the name of the host (machine) on which `SampleServer`{.codeph} is
running, and (3) the port number on which `SampleServer`{.codeph} is
listening for client connections.

Below are the full commands to use for Windows, Solaris, Linux, and
macOS.

<div class="infoboxnote" id="GUID-19CC950B-FFCA-471A-918E-92559F556356__GUID-8F54E144-67DF-418F-B273-76815F39CF91">
Note:

</div>
<span class="bold">Important: In these commands, you must replace
`<service_principal>`{.codeph}, `<host>`{.codeph},
`<port_number>`{.codeph}, `<your_realm>`{.codeph}, and
`<your_kdc>`{.codeph} with appropriate values</span> (and note that the
port number must be the same as the port number passed as an argument to
`SampleServer`{.codeph}). These values need not be placed in quotes.

Here is the command for Windows:

``` {.oac_no_warn dir="ltr"}
java -classpath Login.jar;SampleClient.jar 
 -Djava.security.manager 
 -Djava.security.krb5.realm=<your_realm> 
 -Djava.security.krb5.kdc=<your_kdc> 
 -Djava.security.policy=client.policy 
 -Djava.security.auth.login.config=csLogin.conf 
 Login SampleClient <service_principal> <host> <port_number>
```

Here is the command for Solaris, Linux, and macOS:

``` {.oac_no_warn dir="ltr"}
java -classpath Login.jar:SampleClient.jar 
 -Djava.security.manager 
 -Djava.security.krb5.realm=<your_realm> 
 -Djava.security.krb5.kdc=<your_realm> 
 -Djava.security.policy=client.policy 
 -Djava.security.auth.login.config=csLogin.conf 
 Login SampleClient <service_principal> <host> <port_number>
```

Type the full command on one line. Multiple lines are used here for
legibility. As with the command for executing `SampleServer`{.codeph},
if the command is too long to type directly into your command window,
place it in a .bat file (Microsoft Windows) or a .sh file (Solaris,
Linux, and macOS) and then execute that file.

When prompted, type your Kerberos user name and password. The underlying
Kerberos authentication mechanism specified in the login configuration
file will log you into Kerberos. Once authentication is successfully
completed, the `SampleClient`{.codeph} code will be executed on behalf
of you. It will request a socket connection with
`SampleServer`{.codeph}. Once `SampleServer`{.codeph} accepts the
connection, `SampleClient`{.codeph} and `SampleServer`{.codeph}
establish a shared context and then exchange messages as described in
this tutorial.

For login troubleshooting suggestions, see
[Troubleshooting](troubleshooting.htm#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

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
| ------- ------------ | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ----------- --       | e | )\                   |
|             [![Previ | L |             <span cl |
| ous](../../dcommon/g | o | ass="icon">Contents< |
| ifs/leftnav.gif)\    | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|         [![Next](../ | ] | -------------------- |
| ../dcommon/gifs/righ | ( | -------------------- |
| tnav.gif)\           | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](u | . |                      |
| se-jaas-login-utilit | . |                      |
| y.htm)   <span class | / |                      |
| ="icon">Next</span>] | d |                      |
| (more-things-you-can | c |                      |
| -do-java-gss-api-and | o |                      |
| -jaas.htm)           | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| ------- ------------ | / |                      |
| -------------------- | g |                      |
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
