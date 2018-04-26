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

  ----------------------------------------------------------------------------------------------------------- ------------------------------------------------------------- --
                                 [![Previous](../../dcommon/gifs/leftnav.gif)\                                         [![Next](../../dcommon/gifs/rightnav.gif)\           
   <span class="icon">Previous</span>](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm)   <span class="icon">Next</span>](kerberos-requirements1.htm)  
  ----------------------------------------------------------------------------------------------------------- ------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-B69758E7-D7B9-4860-BFA2-0429618374E8}<!-- End Header -->

More Things You Can Do with Java GSS-API and JAAS {#JSSEC-GUID-B69758E7-D7B9-4860-BFA2-0429618374E8 .sect1}
=================================================

<div>
The previous tutorial, [Use of JAAS Login Utility and Java GSS-API for
Secure Message
Exchanges](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8),
demonstrated how two applications, in particular a client and a server,
could use the Java GSS-API to establish a secure context between them
and then securely exchange messages.

There are additional operations the context acceptor (the server in our
client/server example) can perform once the context has been established
with the context initiator (the client). Basically, the server can
\"impersonate\" the client. The level of impersonation depends upon
whether or not the client has delegated credentials to the server.

-   [Executing Code on Behalf of the Client
    User](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-7836E843-A8F1-4C59-A5FD-BFEE3B307508)
-   [Using Credentials Delegated from the
    Client](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-23E84B31-CEAD-4FAC-A3EB-AD807587A502)

</div>
<div class="sect2">
[]{#GUID-7836E843-A8F1-4C59-A5FD-BFEE3B307508}

Executing Code on Behalf of the Client User {#JSSEC-GUID-7836E843-A8F1-4C59-A5FD-BFEE3B307508 .sect2}
-------------------------------------------

<div>
One possible type of client impersonation the server can do is causing
code to be executed on behalf of the same entity (user) the client code
is executed on behalf of. Normally, a method executed by a thread uses
the access control settings for that thread itself. However, when
impersonating a client in this tutorial, the server uses the client\'s
access control settings so that the server has access to exactly those
resources that the client itself has when it runs.

One major benefit of the approach used in this tutorial is that the JAAS
authorization component can be used for access control. Without the JAAS
authorization component, the server principal would need access to any
resources accessed by the code executed on behalf of the client user,
and the server code would need to include access control logic to
determine whether the user was authorized to access such resources. By
utilizing JAAS authorization, providing principal-based access control,
the access control is handled automatically. Permissions for the
security-sensitive operations in such code only need to be granted to
that user and not also to the server code. See the [JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F)
tutorial for more information on JAAS authorization.

-   [Basic
    Approach](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-08F32421-A49E-4DB8-9FD9-CC25D398CF2D)
-   [Sample Code and Policy
    File](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-B04626E5-C67D-4116-A7D4-4D58270BE4CB)
-   [Running the Sample
    Code](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-4CD5A92F-DDD9-4464-9F42-4105B583A08B)

</div>
<div class="sect3">
[]{#GUID-08F32421-A49E-4DB8-9FD9-CC25D398CF2D}

### Basic Approach {#JSSEC-GUID-08F32421-A49E-4DB8-9FD9-CC25D398CF2D .sect3}

<div>
How does the server \"impersonate\" the client to execute code on behalf
of the user running the client code? Essentially the same way the client
code is set up to be run on behalf of that user. All the server code
needs to know is the user\'s principal name, which it can obtain from
the context established with the client.

Recall that JAAS authentication of the user executing the client code
results in creation of a <span class="apiname">Subject</span> containing
a <span class="apiname">Principal</span> with the user (principal) name.
The Subject is subsequently associated with a new access control context
(via a `Subject.doAsPrivileged`{.codeph} call from the Login utility)
and the client code is considered to be executed on behalf of the user;
subsequent access control decisions are based on whether or not that
particular user, executing the client code, is granted the required
permissions.

The server code is similarly handled, except in that case the Principal
specified for authentication is typically a \"service principal\", not a
user principal. Again, a <span class="apiname">Subject</span> containing
a <span class="apiname">Principal</span> with the specified principal
name is created, `Subject.doAsPrivileged`{.codeph} is called, and the
server code is considered to be executed on behalf of the specified
principal; subsequent access control decisions are based on whether or
not that particular principal, executing the server code, is granted the
required permissions.

Once the client and server have established a mutual context, the
context initiator\'s name (the client\'s principal name) can be
determined by the following:

``` {.oac_no_warn dir="ltr"}
GSSName clientGSSName = context.getSrcName();
```

The context acceptor (the server) can use this name to construct a
<span class="apiname">Subject</span> containing a
<span class="apiname">Principal</span> that represents the same entity.
For example, you can construct such a
<span class="apiname">Subject</span> with Oracle\'s JDK via the
following:

``` {.oac_no_warn dir="ltr"}
Subject client = 
  com.sun.security.jgss.GSSUtil.createSubject(clientGSSName, null);
```

The
[<span class="apiname">createSubject</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/jgss/GSSUtil.html#createSubject-org.ietf.jgss.GSSName-org.ietf.jgss.GSSCredential-)
method creates a new Subject from the GSSName and GSSCredential
specified as arguments. If the server code is just going to execute code
on behalf of the user in the local JVM, the user\'s credentials are not
required -- and in fact cannot even be obtained unless the client has
delegated credentials to the server, as discussed in [Using Credentials
Delegated from the
Client](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-23E84B31-CEAD-4FAC-A3EB-AD807587A502).
Since the credentials are not needed here, we pass a `null`{.codeph} for
the GSSCredential argument.

<div class="infoboxnote" id="GUID-08F32421-A49E-4DB8-9FD9-CC25D398CF2D__GUID-CCD1A8B1-8E91-418D-93DA-869E28C603FF">
Note:

Note: If you are not using Oracle\'s JDK, an alternative way to do this
is to construct a <span class="apiname">KerberosPrincipal</span>
instance as follows:

``` {.oac_no_warn dir="ltr"}
KerberosPrincipal principal = 
  new KerberosPrincipal(clientGSSName.toString());
```

Then use this principal to construct a new
<span class="apiname">Subject</span> or populate this principal in the
principal set of an existing <span class="apiname">Subject</span>.

The code that the server would like to execute on behalf of the user
should be initiated from the `run`{.codeph} method of a class that
implements `java.security.PrivilegedAction`{.codeph} (or
`java.security.PrivilegedExceptionAction`{.codeph}). That is, the code
can either be in such a `run`{.codeph} method or invoked from such a
`run`{.codeph} method.

The server code can pass the <span class="apiname">Subject</span>, along
with an instance of the <span class="apiname">PrivilegedAction</span>
(or <span class="apiname">PrivilegedExceptionAction</span>), to
`Subject.doAsPrivileged`{.codeph} to execute the subsequent code,
starting with the `run`{.codeph} method in the
<span class="apiname">PrivilegedAction</span>, on behalf of the
principal (user) in the specified Subject.

For example, suppose the <span class="apiname">PrivilegedAction</span>
class is called <span class="apiname">ReadFileAction</span> and it takes
as an argument a <span class="apiname">String</span> with the principal
name. You can create an instance of this class by

``` {.oac_no_warn dir="ltr"}
String clientName = clientGSSName.toString();
PrivilegedAction readFile = 
    new ReadFileAction(clientName);
```

The call to `doAsPrivileged`{.codeph} is then

``` {.oac_no_warn dir="ltr"}
Subject.doAsPrivileged(client, readFile, null);
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-B04626E5-C67D-4116-A7D4-4D58270BE4CB}

### Sample Code and Policy File {#JSSEC-GUID-B04626E5-C67D-4116-A7D4-4D58270BE4CB .sect3}

<div>
The following sample code and policy file illustrate the server
impersonating the client in order to execute code whose
security-sensitive operations are only permitted to be done by the
specific user executing the client.

-   [`SampleServerImp.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLESERVERIMP.JAVA-33894617)
-   [`ReadFileAction.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__READFILEACTION.JAVA-33894842)
-   [`serverimp.policy`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SERVERIMP.POLICY-33894A6C)

</div>
<div class="sect4">
[]{#GUID-78C0C551-4A03-4094-8BEB-DA3D5212E509}

#### SampleServerImp.java {#JSSEC-GUID-78C0C551-4A03-4094-8BEB-DA3D5212E509 .sect4}

<div>
The
[`SampleServerImp.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLESERVERIMP.JAVA-33894617)
file is exactly the same as the `SampleServer.java` file from the
previous ([Use of JAAS Login Utility and Java GSS-API for Secure Message
Exchanges](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8))
tutorial, except that after exchanging messages with the client, it has
the following code to perform a `ReadFileAction`{.codeph} as the client
user:

``` {.oac_no_warn dir="ltr"}
System.out.println("Impersonating client.");

/*
 * Extract the KerberosPrincipal from the client GSSName and 
 * populate it in the principal set of a new Subject. Pass in a 
 * null for credentials since credentials will not be needed.
 */
GSSName clientGSSName = context.getSrcName();
System.out.println("clientGSSName: " + clientGSSName);
Subject client =
   com.sun.security.jgss.GSSUtil.createSubject(clientGSSName,
        null);

/*
* Construct an action that will read a file meant only for the
* client
*/
String clientName = clientGSSName.toString();
PrivilegedAction readFile = 
   new ReadFileAction(clientName);

/*
* Invoke the action via a doAsPrivileged. This allows the
* action to be executed as the client subject, and it also 
* runs that code as privileged. This means that any permission 
* checking that happens beyond this point applies only to 
* the code being run as the client.
*/
Subject.doAsPrivileged(client, readFile, null);
```

</div>
</div>
<div class="sect4">
[]{#GUID-2754F056-55C4-4844-ABA5-7535B541A538}

#### ReadFileAction.java {#JSSEC-GUID-2754F056-55C4-4844-ABA5-7535B541A538 .sect4}

<div>
The
[`ReadFileAction.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__READFILEACTION.JAVA-33894842)
file contains the `ReadFileAction`{.codeph} class. Its constructor takes
as an argument a <span class="apiname">String</span> for the name of the
client user. The client user name is used to construct a file name for a
file from which `ReadFileAction`{.codeph} will attempt to read. The file
name will be:

``` {.oac_no_warn dir="ltr"}
./data/<name>_info.txt
```

where `<name>`{.codeph} is the client user name without its
corresponding realm. For example, if the full user name is
`mjones@KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}, then the file name is

``` {.oac_no_warn dir="ltr"}
./data/mjones_info.txt
```

<div class="infoboxnote" id="GUID-2754F056-55C4-4844-ABA5-7535B541A538__GUID-09828A7D-C3B7-40BF-9A22-8C3194F7EA76">
Note:

On Window, the forward slashes will be backward slashes.

</div>
The `ReadFileAction`{.codeph} `run`{.codeph} method reads the specified
file and prints its contents.

</div>
</div>
<div class="sect4">
[]{#GUID-53271ED8-797E-4BCB-8AAB-2D8ABAAE3991}

#### serverimp.policy {#JSSEC-GUID-53271ED8-797E-4BCB-8AAB-2D8ABAAE3991 .sect4}

<div>
<span class="apiname">ReadFileAction</span> attempts to read a file,
which is a security-checked operation. Since
<span class="apiname">ReadFileAction</span> is considered to be executed
as the client user (<span class="apiname">Principal</span>), the
appropriate permission must be granted not only to the
<span class="apiname">ReadFileAction</span> code itself, but to the
client <span class="apiname">Principal</span> as well.

Assuming the `ReadFileAction`{.codeph} class is placed in a JAR file
named `ReadFileAction.jar`{.codeph}, and the user principal name is
`mjones@KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}, this permission can be
granted via the following in a policy file:

``` {.oac_no_warn dir="ltr"}
grant CodeBase "file:./ReadFileAction.jar" 
    Principal javax.security.auth.kerberos.KerberosPrincipal 
        "mjones@KRBNT-OPERATIONS.EXAMPLE.COM" {

    permission java.io.FilePermission "data/mjones_info.txt", 
        "read";
};
```

The
[`serverimp.policy`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SERVERIMP.POLICY-33894A6C)
file is exactly the same as the `server.policy`{.codeph} file from the
previous ([Use of JAAS Login Utility and Java GSS-API for Secure Message
Exchanges](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8))
tutorial, except that it grants the
<span class="apiname">SampleServer</span> code the
`javax.security.auth.AuthPermission "doAsPrivileged"`{.codeph}
permission it needs in order to call the `doAsPrivileged`{.codeph}
method, and it has the following placeholder for granting the
<span class="apiname">FilePermission</span> shown above:

``` {.oac_no_warn dir="ltr"}
grant CodeBase "file:./ReadFileAction.jar" 
    Principal javax.security.auth.kerberos.KerberosPrincipal 
        "your_user_name@your_realm" {

    permission java.io.FilePermission "data/your_user_name_info.txt", 
        "read";
};
```

You must substitute your Kerberos realm for `your_realm`{.codeph}, and
your user name for `your_user_name`{.codeph} in both
`your_user_name@your_realm`{.codeph} and
`data/your_user_name_info.txt`{.codeph}. If you are working on Windows,
you also replace the \"/\" in `data/your_user_name_info.txt`{.codeph}
with a \"\\\".

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-4CD5A92F-DDD9-4464-9F42-4105B583A08B}

### Running the Sample Code {#JSSEC-GUID-4CD5A92F-DDD9-4464-9F42-4105B583A08B .sect3}

<div>
To run the sample code illustrating the server impersonating the client,
do everything listed in [Running the SampleClient and SampleServer
Programs](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-07D0C8CC-0922-4B0F-B14D-9A644CB13783)
in the previous tutorial, except for the following:

-   In the \"Prepare `SampleServer`{.codeph} for Execution\" step:
    -   Use
        [`SampleServerImp.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLESERVERIMP.JAVA-33894617)
        instead of `SampleServer.java`{.codeph}. Compile it and create a
        JAR file named `SampleServerImp.jar`{.codeph} containing
        `SampleServerImp.class`{.codeph} via the following:

        ``` {.oac_no_warn dir="ltr"}
        javac SampleServerImp.java
        jar -cvf SampleServerImp.jar SampleServerImp.class
        ```

    -   Use the
        [`serverimp.policy`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SERVERIMP.POLICY-33894A6C)
        policy file instead of `server.policy`{.codeph}.
    -   Use the
        [`csImpLogin.conf`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__CSIMPLOGIN.CONF-37761B67)
        login configuration file instead of `cs.conf`{.codeph}.
    -   Copy
        [`ReadFileAction.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__READFILEACTION.JAVA-33894842)
        to the same directory as the other files. Compile it and place
        it in a JAR file via the following:

        ``` {.oac_no_warn dir="ltr"}
        javac ReadFileAction.java
        jar -cvf ReadFileAction.jar ReadFileAction.class
        ```

    -   In `csImpLogin.conf`{.codeph}, replace
        `service_principal@your_realm`{.codeph} with the Kerberos name
        of the service principal that represents
        <span class="apiname">SampleServer</span> (see [Kerberos User
        and Service Principal
        Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80)).
    -   In `serverimp.policy`{.codeph}, replace
        `service_principal@your_realm`{.codeph} in both places it
        appears with the Kerberos name of the service principal that
        represents `SampleServer`{.codeph}. (The same name as that used
        in the login configuration file.) In addition, substitute your
        Kerberos realm for `your_realm`{.codeph}, and your user name for
        `your_user_name`{.codeph} in both
        `your_user_name@your_realm`{.codeph} and
        `data/your_user_name_info.txt`{.codeph}. If you are running on
        Windows, then replace the \"/\" in
        `data/your_user_name_info.txt`{.codeph} with a \"\\\".
    -   Create a `data`{.codeph} subdirectory of your current directory
        and create a short text file of the specified name in that
        directory. For example, if your user name is `mjones`{.codeph},
        the file to be placed in the data subdirectory should be named
        `mjones_info.txt`{.codeph}.

-   In the \"Execute `SampleServer`{.codeph}\" step:
    -   Use the following commands instead of those specified in that
        section so that `SampleServerImp`{.codeph} is executed,
        `serverimp.policy`{.codeph} and `csImpLogin.conf`{.codeph} are
        used, and `ReadFileAction.jar`{.codeph} is included.

        <div class="infoboxnote" id="GUID-4CD5A92F-DDD9-4464-9F42-4105B583A08B__GUID-EE702120-44BD-426F-817C-18158F6D293D">
        Note:

        <span class="bold">Important: In these commands, you must
        replace `<port_number>`{.codeph} with an appropriate port number
        (a high port number such as 4444), `<your_realm>`{.codeph} with
        your Kerberos realm, and `<your_kdc>`{.codeph} with your
        Kerberos KDC.</span>

        </div>
        Here is the command for Windows:

        ``` {.oac_no_warn dir="ltr"}
          java -classpath Login.jar;SampleServerImp.jar;ReadFileAction.jar 
            -Djava.security.manager 
            -Djava.security.krb5.realm=<your_realm> 
            -Djava.security.krb5.kdc=<your_kdc> 
            -Djava.security.policy=serverimp.policy 
            -Djava.security.auth.login.config=csImpLogin.conf 
            Login SampleServerImp <port_number> 
        ```

        Here is the command for Solaris, Linux, and macOS:

        ``` {.oac_no_warn dir="ltr"}
          java -classpath Login.jar:SampleServerImp.jar:ReadFileAction.jar 
            -Djava.security.manager 
            -Djava.security.krb5.realm=<your_realm> 
            -Djava.security.krb5.kdc=<your_kdc> 
            -Djava.security.policy=serverimp.policy 
            -Djava.security.auth.login.config=csImpLogin.conf 
            Login SampleServerImp <port_number> 
        ```

        As usual, type the full command on one line. Multiple lines are
        used here for legibility. If the command is too long for your
        system, you may need to place it in a .bat file (for Windows) or
        a .sh file (for Solaris, Linux, and macOS) and then run that
        file to execute the command.

        As when running `SampleServer`{.codeph}, you will be prompted
        for the Kerberos password for the service principal under which
        `SampleServerImp`{.codeph} is expected to be run. The Kerberos
        login module specified in the login configuration file will log
        the service principal into Kerberos. Once authentication is
        successfully completed, the `SampleServerImp`{.codeph} code will
        be executed on behalf of the service principal. It will listen
        for socket connections on the specified port.

        After you follow the \"Prepare `SampleClient`{.codeph} for
        Execution\" and \"Execute `SampleClient`{.codeph}\" instructions
        as usual and perform the user login, the client code will
        request a socket connection with `SampleServerImp`{.codeph}.
        Once `SampleServerImp`{.codeph} accepts the connection,
        `SampleClient`{.codeph} and `SampleServerImp`{.codeph} establish
        a shared context and then exchange messages as described in the
        previous tutorial.

        After the message exchange, `SampleServerImp`{.codeph}
        determines the principal name of the user executing the client
        code, creates a new <span class="apiname">Subject</span>
        containing a <span class="apiname">Principal</span> with that
        name, and calls `Subject.doAsPrivileged`{.codeph} to execute the
        code in `ReadFileAction`{.codeph} on behalf of the specified
        user. `ReadFileAction`{.codeph} reads the file named
        `your_user_name_info.txt`{.codeph} (where
        `your_user_name`{.codeph} represents the actual user name) in
        the `data`{.codeph} subdirectory of the current directory, and
        prints out its contents.

        For login troubleshooting suggestions, see
        [Troubleshooting](troubleshooting.html#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-23E84B31-CEAD-4FAC-A3EB-AD807587A502}

Using Credentials Delegated from the Client {#JSSEC-GUID-23E84B31-CEAD-4FAC-A3EB-AD807587A502 .sect2}
-------------------------------------------

<div>
The most complete type of client impersonation is possible if the client
delegates its credentials to the server.

Recall that prior to context establishment with the context acceptor
(the server in our previous tutorial), the context initiator (the
client) sets various context options. If the initiator calls the
`requestCredDeleg`{.codeph} method on the `context`{.codeph} object with
a `true`{.codeph} argument, as in

``` {.oac_no_warn dir="ltr"}
context.requestCredDeleg(true);
```

then this requests that the initiator\'s credentials be delegated to the
acceptor during context establishment.

Delegation of credentials from the initiator to the acceptor enables the
acceptor to authenticate itself as an agent or delegate of the
initiator.

First, after context establishment, the acceptor must determine whether
or not credential delegation actually took place. It does so by calling
the `getCredDelegState`{.codeph} method:

``` {.oac_no_warn dir="ltr"}
boolean delegated = context.getCredDelegState();
```

If credentials were delegated, the acceptor can obtain those credentials
by calling the `getDelegCr`{.codeph} method:

``` {.oac_no_warn dir="ltr"}
GSSCredential clientCr = context.getDelegCred();
```

The resulting <span class="apiname">GSSCredential</span> object can then
be used to initiate subsequent GSS-API contexts as a \"delegate\" of the
initiator. For example, the server could authenticate as the client to a
backend server that cares more about who the original client was than
who the intermediate server is.

Acting as the client, the server can establish a connection with the
backend server, establish a joint security context, and exchange
messages in basically the same manner that the client and server did.

One way it could be done is that when the server calls the
`createContext`{.codeph} method of a
<span class="apiname">GSSManager</span>, it could pass
`createContext`{.codeph} the delegated credentials instead of passing a
`null`{.codeph}.

Alternatively, the server code could first call the
`com.sun.security.jgss.GSSUtil createSubject`{.codeph} method and pass
it the delegated credentials. That method returns a
<span class="apiname">Subject</span> containing those credentials as the
default credentials. The server could then associate this
`Subject`{.codeph} with the current
<span class="apiname">AccessControlContext</span>, as described in [How
Do You Associate a Subject with an Access Control
Context?](jaas-authorization.html#GUID-86CC2E0C-58B9-4E35-91E1-EC130EE2E4FC)
in the JAAS Authorization tutorial. Then, when the server code calls the
<span class="apiname">GSSManager</span> `createContext`{.codeph} method,
it can pass a null (indicating the credentials for the \"current\"
Subject should be used). In other words, the server would effectively
become the client. Subsequent connections to backend servers using GSS
could be made exactly as described in the previous tutorials. This
approach is useful if you want the code that will use the delegated
credentials to be identical to the code that uses the default local
credentials.

<div class="section">
Constrained Delegation

If constrained delegation is configured in a KDC server, then, on the
server side, the <span class="apiname">getCredDelegState()</span> call
might still return true and <span class="apiname">getDelegCred()</span>
would return delegated credentials, depending on the KDC settings, even
if the client has not called
<span class="apiname">requestCredDeleg(true)</span>.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-46E411CE-A04B-4489-AEC6-9AF4D569B371}

Permission Required In Order to Delegate Credentials {#JSSEC-GUID-46E411CE-A04B-4489-AEC6-9AF4D569B371 .sect2}
----------------------------------------------------

<div>
In order to delegate credentials, the context initiator
(`SampleClient`{.codeph} in our previous tutorial) must have a
`javax.security.auth.kerberos.DelegationPermission`{.codeph}. An example
using placeholders in italics for actual values is the following:

``` {.oac_no_warn dir="ltr"}
permission javax.security.auth.kerberos.DelegationPermission
  "\"service_principal@your_realm\"  
     \"krbtgt/your_realm@your_realm\"";
```

Note that <span class="apiname">DelegationPermission</span> has a single
target in quotes that contains two items, both of which are quoted. Each
inner quote is escaped by a \"\\\". Thus the first item is

``` {.oac_no_warn dir="ltr"}
"service_principal@your_realm"
```

and the second is

``` {.oac_no_warn dir="ltr"}
"krbtgt/your_realm@your_realm"
```

This basically gives the code executing on behalf of the client the
permission to forward a Kerberos ticket to the specified peer
(`service_principal`{.codeph}), where the Kerberos ticket is meant to
avail service from `krbtgt/your_realm@your_realm`{.codeph}.

Substitute your realm for all places `your_realm`{.codeph} appears. Also
substitute the service principal name for the service principal
representing the server for `service_principal@your_realm`{.codeph}.
(See [Kerberos User and Service Principal
Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80)
in the previous tutorial.) Suppose your realm is
`KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph} and the service principal is
`sample/raven.example.com@KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}. Then
the permission could appear in a policy file as

``` {.oac_no_warn dir="ltr"}
permission javax.security.auth.kerberos.DelegationPermission
  "\"sample/raven.example.com@KRBNT-OPERATIONS.EXAMPLE.COM\"  
     \"krbtgt/KRBNT-OPERATIONS.EXAMPLE.COM@KRBNT-OPERATIONS.EXAMPLE.COM\"";
```

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
| --------- ---------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| ----------- --       | L |             <span cl |
|                      | o | ass="icon">Contents< |
|              [![Prev | g | /span>](toc.htm)     |
| ious](../../dcommon/ | o |   -- --------------- |
| gifs/leftnav.gif)\   | ] | -------------------- |
|                      | ( | -------------------- |
|                    [ | . | ---                  |
| ![Next](../../dcommo | . |                      |
| n/gifs/rightnav.gif) | / |                      |
| \                    | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](u | / |                      |
| se-jaas-login-utilit | d |                      |
| y-and-java-gss-api-s | c |                      |
| ecure-message-exchan | o |                      |
| ges.htm)   <span cla | m |                      |
| ss="icon">Next</span | m |                      |
| >](kerberos-requirem | o |                      |
| ents1.htm)           | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| -------------------- | s |                      |
| --------- ---------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| ----------- --       | a |                      |
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
