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

  ----------------------------------------------------------------------------------------------------- --------------------------------------------------------- --
                              [![Previous](../../dcommon/gifs/leftnav.gif)\                                    [![Next](../../dcommon/gifs/rightnav.gif)\         
   <span class="icon">Previous</span>](use-java-gss-api-secure-message-exchanges-jaas-programming.htm)   <span class="icon">Next</span>](jaas-authorization.htm)  
  ----------------------------------------------------------------------------------------------------- --------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623}<!-- End Header -->

JAAS Authentication {#JSSEC-GUID-0C6EB04B-D203-4688-A3E2-A7D442334623 .sect1}
===================

<div>
JAAS can be used for two purposes:

-   for <span class="variable">authentication</span> of users, to
    reliably and securely determine who is currently executing Java
    code, regardless of whether the code is running as an application,
    an applet, a bean, or a servlet; and
-   for <span class="variable">authorization</span> of users to ensure
    they have the access control rights (permissions) required to do the
    actions performed.

This section provides a basic tutorial for the authentication component.
The authorization component will be described in the [JAAS
Authorization](jaas-authorization.htm#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F)
tutorial.

JAAS authentication is performed in a
<span class="variable">pluggable</span> fashion. This permits Java
applications to remain independent from underlying authentication
technologies. New or updated technologies can be plugged in without
requiring modifications to the application itself. An implementation for
a particular authentication technology to be used is determined at
runtime. The implementation is specified in a login configuration file.
The authentication technology used for this tutorial is Kerberos. (See
[Kerberos
Requirements](kerberos-requirements1.htm#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998).)

The rest of this tutorial consists of the following sections:

1.  [The Authentication Tutorial
    Code](jaas-authentication.htm#GUID-F12A6645-5A3E-41F7-94E6-57694DFFF2D3)
2.  [The Login
    Configuration](jaas-authentication.htm#GUID-C595253D-3817-4CA6-9336-D7D5159C9680)
3.  [Running the
    Code](jaas-authentication.htm#GUID-A76E9155-E82F-48C0-9382-C365C157EEBF)
4.  [Running the Code with a Security
    Manager](jaas-authentication.htm#GUID-EF86E769-AFAF-4341-B9B0-4E122A0BFCEC)

If you want to first see the tutorial code in action, you can skip
directly to [Running the
Code](jaas-authentication.htm#GUID-A76E9155-E82F-48C0-9382-C365C157EEBF)
and then go back to the other sections to learn about coding and
configuration file details.

</div>
<div class="sect2">
[]{#GUID-F12A6645-5A3E-41F7-94E6-57694DFFF2D3}

The Authentication Tutorial Code {#JSSEC-GUID-F12A6645-5A3E-41F7-94E6-57694DFFF2D3 .sect2}
--------------------------------

<div>
Our authentication tutorial code is contained in a single source file,
[`JaasAcn.java`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JAASACN.JAVA-338927FE).
This file\'s `main`{.codeph} method performs the authentication and then
reports whether or not authentication succeeded.

The code for authenticating the user is very simple, consisting of just
two steps:

1.  [Instantiating a
    LoginContext](jaas-authentication.htm#GUID-080F384C-0FF3-4443-B4A7-21B6F03371F0)
2.  [Calling the LoginContext\'s login
    Method](jaas-authentication.htm#GUID-98A3DD32-C417-449B-9C55-1C9509364612)

</div>
<div class="sect3">
[]{#GUID-080F384C-0FF3-4443-B4A7-21B6F03371F0}

### Instantiating a LoginContext {#JSSEC-GUID-080F384C-0FF3-4443-B4A7-21B6F03371F0 .sect3}

<div>
In order to authenticate a user, you first need a
`javax.security.auth.login.LoginContext`{.codeph}. Here is the basic way
to instantiate a <span class="apiname">LoginContext</span>:

``` {.oac_no_warn dir="ltr"}
import javax.security.auth.login.*;
. . .
LoginContext lc = 
    new LoginContext(<config file entry name>,
           <CallbackHandler to be used for user interaction>); 
```

and here is the specific way our tutorial code does the instantiation:

``` {.oac_no_warn dir="ltr"}
import javax.security.auth.login.*;
import com.sun.security.auth.callback.TextCallbackHandler;
. . .
LoginContext lc = 
    new LoginContext("JaasSample", 
          new TextCallbackHandler());
```

The arguments are the following:

1.  <span class="bold">The name of an entry in the JAAS login
    configuration file</span>

    This is the name for the <span class="apiname">LoginContext</span>
    to use to look up an entry for this application in the JAAS login
    configuration file, described in [The Login
    Configuration](jaas-authentication.htm#GUID-C595253D-3817-4CA6-9336-D7D5159C9680).
    Such an entry specifies the class(es) that implement the desired
    underlying authentication technology(ies). The class(es) must
    implement the <span class="apiname">LoginModule</span> interface,
    which is in the `javax.security.auth.spi`{.codeph} package.

    In our sample code, we use the `Krb5LoginModule`{.codeph} in the
    `com.sun.security.auth.module`{.codeph} package, which performs
    Kerberos authentication.

    The entry in the login configuration file we use for this tutorial
    (see
    [`jaas.conf`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JASS.CONF-33892AE7))
    has the name \"JaasSample\", so that is the name we specify as the
    first argument to the <span class="apiname">LoginContext</span>
    constructor.

2.  <span class="bold">A <span class="apiname">CallbackHandler</span>
    instance.</span>

    When a <span class="apiname">LoginModule</span> needs to communicate
    with the user, for example to ask for a user name and password, it
    does not do so directly. That is because there are various ways of
    communicating with a user, and it is desirable for
    <span class="apiname">LoginModules</span> to remain independent of
    the different types of user interaction. Rather, the
    <span class="apiname">LoginModule</span> invokes a
    <span class="apiname">CallbackHandler</span> to perform the user
    interaction and obtain the requested information, such as the user
    name and password. (<span class="apiname">CallbackHandler</span> is
    an interface in the `javax.security.auth.callback`{.codeph}
    package.)

    An instance of the particular
    <span class="apiname">CallbackHandler</span> to be used is specified
    as the second argument to the
    <span class="apiname">LoginContext</span> constructor. The
    <span class="apiname">LoginContext</span> forwards that instance to
    the underlying <span class="apiname">LoginModule</span> (in our case
    <span class="apiname">Krb5LoginModule</span>). An application
    typically provides its own
    <span class="apiname">CallbackHandler</span> implementation. A
    simple <span class="apiname">CallbackHandler</span>,
    <span class="apiname">TextCallbackHandler</span>, is provided in the
    `com.sun.security.auth.callback`{.codeph} package to output
    information to and read input from the command line.

</div>
</div>
<div class="sect3">
[]{#GUID-98A3DD32-C417-449B-9C55-1C9509364612}

### Calling the LoginContext\'s login Method {#JSSEC-GUID-98A3DD32-C417-449B-9C55-1C9509364612 .sect3}

<div>
Once we have a <span class="apiname">LoginContext</span> `lc`{.codeph},
we can call its `login`{.codeph} method to carry out the authentication
process:

``` {.oac_no_warn dir="ltr"}
lc.login();
```

The LoginContext instantiates a new empty
[`javax.security.auth.Subject`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Subject.html)
object (which represents the user or service being authenticated; see
[Subject](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3)).
The <span class="apiname">LoginContext</span> constructs the configured
<span class="apiname">LoginModule</span> (in our case
<span class="apiname">Krb5LoginModule</span>) and initializes it with
this new <span class="apiname">Subject</span> and
<span class="apiname">TextCallbackHandler</span>.

The <span class="apiname">LoginContext</span>\'s `login`{.codeph} method
then calls methods in the <span class="apiname">Krb5LoginModule</span>
to perform the login and authentication. The
<span class="apiname">Krb5LoginModule</span> will utilize the
<span class="apiname">TextCallbackHandler</span> to obtain the user name
and password. Then the <span class="apiname">Krb5LoginModule</span> will
use this information to get the user credentials from the Kerberos KDC.
See the [Kerberos reference
documentation](http://web.MIT.edu/kerberos/www/index.html).

If authentication is successful, the
<span class="apiname">Krb5LoginModule</span> populates the
<span class="apiname">Subject</span> with (1) a Kerberos
<span class="apiname">Principal</span> representing the user and (2) the
user\'s credentials (TGT).

The calling application can subsequently retrieve the authenticated
<span class="apiname">Subject</span> by calling the
<span class="apiname">LoginContext</span>\'s `getSubject`{.codeph}
method, although doing so is not necessary for this tutorial.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-C595253D-3817-4CA6-9336-D7D5159C9680}

The Login Configuration {#JSSEC-GUID-C595253D-3817-4CA6-9336-D7D5159C9680 .sect2}
-----------------------

<div>
JAAS authentication is performed in a pluggable fashion, so applications
can remain independent from underlying authentication technologies. A
system administrator determines the authentication technologies, or
<span class="apiname">LoginModule</span>s, to be used for each
application and configures them in a login
<span class="apiname">Configuration</span>. The source of the
configuration information (for example, a file or a database) is up to
the current
[<span class="apiname">javax.security.auth.login.Configuration</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
implementation. The default `Configuration`{.codeph} implementation from
Oracle reads configuration information from configuration files, as
described in
[<span class="apiname">com.sun.security.auth.login.ConfigFile</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/login/ConfigFile.html).

See [Appendix B: JAAS Login Configuration
File](appendix-b-jaas-login-configuration-file.htm#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)
for information as to what a login configuration file is, what it
contains, and how to specify which login configuration file should be
used.

</div>
<div class="sect3">
[]{#GUID-D6F986DD-2046-4025-A65F-AC8855C85984}

### The Login Configuration File for This Tutorial {#JSSEC-GUID-D6F986DD-2046-4025-A65F-AC8855C85984 .sect3}

<div>
As noted, the login configuration file we use for this tutorial,
[jass.conf](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JASS.CONF-33892AE7),
contains just one entry, which is

``` {.oac_no_warn dir="ltr"}
JaasSample {
  com.sun.security.auth.module.Krb5LoginModule required;
};
```

This entry is named `JaasSample`{.codeph} and that is the name that our
tutorial application, `JaasAcn`{.codeph}, uses to refer to this entry.
The entry specifies that the <span class="apiname">LoginModule</span> to
be used to do the user authentication is the
<span class="apiname">Krb5LoginModule</span> in the
`com.sun.security.auth.module`{.codeph} package and that this
<span class="apiname">Krb5LoginModule</span> is required to \"succeed\"
in order for authentication to be considered successful. The
<span class="apiname">Krb5LoginModule</span> succeeds only if the name
and password supplied by the user are successfully used to log the user
into the Kerberos KDC.

See the
[<span class="apiname">Krb5LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/Krb5LoginModule.html)
Javadoc API documentation for information about all the possible options
that can be passed to <span class="apiname">Krb5LoginModule</span>.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-A76E9155-E82F-48C0-9382-C365C157EEBF}

Running the Code {#JSSEC-GUID-A76E9155-E82F-48C0-9382-C365C157EEBF .sect2}
----------------

<div>
To execute our JAAS authentication tutorial code, all you have to do is

1.  Place the
    [`JaasAcn.java`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JAASACN.JAVA-338927FE)
    application source file and the
    [`jaas.conf`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JASS.CONF-33892AE7)
    login configuration file into a directory.
2.  Compile `JaasAcn.java`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    javac JaasAcn.java
    ```

3.  Execute the `JaasAcn`{.codeph} application, specifying
    -   by `-Djava.security.krb5.realm=<your_realm>`{.codeph} that your
        Kerberos realm is the one specified.

        For example, if your realm is
        `KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph} you\'d put
        `-Djava.security.krb5.realm=KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}.

    -   by `-Djava.security.krb5.kdc=<your_kdc>`{.codeph} that your
        Kerberos KDC is the one specified.

        For example, if your KDC is `samplekdc.example.com`{.codeph}
        you\'d put
        `-Djava.security.krb5.kdc=samplekdc.example.com`{.codeph}.

    -   by `-Djava.security.auth.login.config=jaas.conf`{.codeph} that
        the login configuration file to be used is `jaas.conf`{.codeph}.

The full command is below.

<div class="infoboxnote" id="GUID-A76E9155-E82F-48C0-9382-C365C157EEBF__GUID-5651F673-F501-42BB-AF33-C11B7DCC5F73">
Note:

<span class="bold">Be sure to replace `<your_realm>`{.codeph} with your
Kerberos realm, and `<your_kdc>`{.codeph} with your Kerberos KDC.</span>

</div>
``` {.oac_no_warn dir="ltr"}
java -Djava.security.krb5.realm=<your_realm> 
 -Djava.security.krb5.kdc=<your_kdc> 
 -Djava.security.auth.login.config=jaas.conf JaasAcn
```

Type all that on one line. Multiple lines are used here for legibility.

You will be prompted for your Kerberos user name and password, and the
underlying Kerberos authentication mechanism specified in the login
configuration file will log you into Kerberos. If your login is
successful, you will see the following message:

``` {.oac_no_warn dir="ltr"}
Authentication succeeded!
```

If the login is not successful (for example, if you misspell your
password), you will see

``` {.oac_no_warn dir="ltr"}
Authentication failed:
```

followed by a reason for the failure. For example, if you mistype your
user name, you may see a message like the following (where the
formatting is slightly modified here to increase legibility):

``` {.oac_no_warn dir="ltr"}
Authentication failed:
  Kerberos Authentication Failed:
    javax.security.auth.login.LoginException: 
      KrbException: Client not found in Kerberos database
```

For login troubleshooting suggestions, see
[Troubleshooting](troubleshooting.htm#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

After fixing any problems, re-run the program to try again.

</div>
</div>
<div class="sect2">
[]{#GUID-EF86E769-AFAF-4341-B9B0-4E122A0BFCEC}

Running the Code with a Security Manager {#JSSEC-GUID-EF86E769-AFAF-4341-B9B0-4E122A0BFCEC .sect2}
----------------------------------------

<div>
When a Java program is run with a security manager installed, the
program is not allowed to access resources or otherwise perform
security-sensitive operations unless it is explicitly granted permission
(see [Permissions in the
JDK](permissions-jdk1.htm#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.")
to do so by the security policy in effect. The permission must be
granted by an entry in a policy file (see [Default Policy Implementation
and Policy File
Syntax](permissions-jdk1.htm#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D)).

Most browsers install a security manager, so
<span class="variable">applets</span> typically run under the scrutiny
of a security manager. <span class="variable">Applications</span>, on
the other hand, do not, since a security manager is not automatically
installed when an application is running. Thus an application, like our
`JaasAcn`{.codeph} application, by default has full access to resources.

<span class="bold">To run an application with a security manager</span>,
simply invoke the interpreter with a `-Djava.security.manager`{.codeph}
argument included on the command line.

If you try invoking `JaasAcn`{.codeph} with a security manager but
without specifying any policy file, you will get the following (unless
you have a default policy setup elsewhere that grants the required
permissions or grants `AllPermission`{.codeph}):

``` {.oac_no_warn dir="ltr"}
% java -Djava.security.manager \
 -Djava.security.krb5.realm=<your_realm> \
 -Djava.security.krb5.kdc=<your_kdc> \
 -Djava.security.auth.login.config=jaas.conf JaasAcn
Exception in thread "main" java.security.AccessControlException: 
  access denied (
  javax.security.auth.AuthPermission createLoginContext.JaasSample)
```

As you can see, you get an
<span class="apiname">AccessControlException</span>, because we haven\'t
created and used a policy file granting our code the permission that is
required in order to be allowed to create a
<span class="apiname">LoginContext</span>.

Here are the complete steps required in order to be able to run our
`JaasAcn`{.codeph} application with a security manager installed. You
can skip the first two steps if you have already done them, as described
in [Running the
Code](jaas-authentication.htm#GUID-A76E9155-E82F-48C0-9382-C365C157EEBF).

1.  Place the
    [`JaasAcn.java`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JAASACN.JAVA-338927FE)
    application source file and the
    [`jaas.conf`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JASS.CONF-33892AE7)
    login configuration file into a directory.
2.  Compile `JaasAcn.java`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    javac JaasAcn.java
    ```

3.  Create a JAR file containing `JaasAcn.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf JaasAcn.jar JaasAcn.class
    ```

    This command creates a JAR file, `JaasAcn.jar`{.codeph}, and places
    the `JaasAcn.class`{.codeph} file inside it.

4.  Create a policy file granting the code in the JAR file the required
    permission.

    The permission that is needed by code attempting to instantiate a
    <span class="apiname">LoginContext</span> is a
    `javax.security.auth.AuthPermission`{.codeph} with target
    `createLoginContext.<entry name>`{.codeph}. Here,
    `<entry name>`{.codeph} refers to the name of the login
    configuration file entry that the application references in its
    instantiation of <span class="apiname">LoginContext</span>. The name
    used by our `JaasAcn`{.codeph} application\'s
    <span class="apiname">LoginContext</span> instantiation is
    `JaasSample`{.codeph}, as you can see in the code:

    ``` {.oac_no_warn dir="ltr"}
    LoginContext lc = 
        new LoginContext("JaasSample", 
              new TextCallbackHandler());
    ```

    Thus, the permission that needs to be granted to
    `JaasAcn.jar`{.codeph} is

    ``` {.oac_no_warn dir="ltr"}
    permission javax.security.auth.AuthPermission 
      "createLoginContext.JaasSample";
    ```

    Copy the policy file
    [`jaasacn.policy`](source-code-jaas-and-java-gss-api-tutorials.htm#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JASSACN.POLICY-33892D36)
    to the same directory as that in which you stored
    `JaasAcn.java`{.codeph}, etc. This is a text file containing the
    following `grant`{.codeph} statement to grant `JaasAcn.jar`{.codeph}
    (in the current directory) the required permission:

    ``` {.oac_no_warn dir="ltr"}
    grant codebase "file:./JaasAcn.jar" {
       permission javax.security.auth.AuthPermission 
                        "createLoginContext.JaasSample";
    };
    ```

    Note: Policy files and the structure of entries within them are
    described in [Default Policy Implementation and Policy File
    Syntax](permissions-jdk1.htm#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D).
    Permissions are described in [Permissions in the
    JDK](permissions-jdk1.htm#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.").

5.  Execute the `JaasAcn`{.codeph} application, specifying

    a.  by an appropriate `-classpath`{.codeph} clause that classes
        should be searched for in the `JaasAcn.jar`{.codeph} JAR file,
    b.  by `-Djava.security.manager`{.codeph} that a security manager
        should be installed,
    c.  by `-Djava.security.krb5.realm=<your_realm>`{.codeph} that your
        Kerberos realm is the one specified. For example, if your realm
        is `KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}you\'d put
        `-Djava.security.krb5.realm=KRBNT-OPERATIONS.EXAMPLE.COM`{.codeph}.
    d.  by `-Djava.security.krb5.kdc=<your_kdc>`{.codeph} that your
        Kerberos KDC is the one specified. For example, if your KDC is
        `samplekdc.example.com`{.codeph}you\'d put
        `-Djava.security.krb5.kdc=samplekdc.example.com`{.codeph}.
    e.  by `-Djava.security.policy=jaasacn.policy`{.codeph} that the
        policy file to be used is `jaasacn.policy`{.codeph}, and
    f.  by `-Djava.security.auth.login.config=jaas.conf`{.codeph} that
        the login configuration file to be used is `jaas.conf`{.codeph}.

    The full command is below.

    <div class="infoboxnote" id="GUID-EF86E769-AFAF-4341-B9B0-4E122A0BFCEC__GUID-38015C89-C0E8-4C45-934F-7AF0A69D677B">
    Note:

    <span class="bold">Be sure to replace `<your_realm>`{.codeph} with
    your Kerberos realm, and `<your_kdc>`{.codeph} with your Kerberos
    KDC.</span>

    </div>
    ``` {.oac_no_warn dir="ltr"}
    java -classpath JaasAcn.jar -Djava.security.manager 
     -Djava.security.krb5.realm=<your_realm> 
     -Djava.security.krb5.kdc=<your_kdc> 
     -Djava.security.policy=jaasacn.policy 
     -Djava.security.auth.login.config=jaas.conf JaasAcn
    ```

    Type all that on one line. Multiple lines are used here for
    legibility. If the command is too long for your system, you may need
    to place it in a .bat file (for Windows) or a .sh file (for Solaris,
    Linux, and macOS) then run that file to execute the command.

    Since the specified policy file contains an entry granting the code
    the required permission, `JaasAcn`{.codeph} will be allowed to
    instantiate a <span class="apiname">LoginContext</span> and continue
    execution. You will be prompted for your Kerberos user name and
    password, and the underlying Kerberos authentication mechanism
    specified in the login configuration file will log you into
    Kerberos. If your login is successful, you will see the message
    \"Authentication succeeded!\" and if not, you will see
    \"Authentication failed:\" followed by a reason for the failure.

    For login troubleshooting suggestions, see
    [Troubleshooting](troubleshooting.htm#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

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
| --- ---------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| - --                 | L |             <span cl |
|                      | o | ass="icon">Contents< |
|           [![Previou | g | /span>](toc.htm)     |
| s](../../dcommon/gif | o |   -- --------------- |
| s/leftnav.gif)\      | ] | -------------------- |
|                      | ( | -------------------- |
|            [![Next]( | . | ---                  |
| ../../dcommon/gifs/r | . |                      |
| ightnav.gif)\        | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](u | / |                      |
| se-java-gss-api-secu | d |                      |
| re-message-exchanges | c |                      |
| -jaas-programming.ht | o |                      |
| m)   <span class="ic | m |                      |
| on">Next</span>](jaa | m |                      |
| s-authorization.htm) | o |                      |
|                      | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| -------------------- | s |                      |
| --- ---------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| - --                 | a |                      |
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
