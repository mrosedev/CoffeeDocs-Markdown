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

  ------------------------------------------------------------- ------------------------------------------------------------------------------------------------------- --
          [![Previous](../../dcommon/gifs/leftnav.gif)\                                       [![Next](../../dcommon/gifs/rightnav.gif)\                                
   <span class="icon">Previous</span>](jaas-authorization.htm)   <span class="icon">Next</span>](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.htm)  
  ------------------------------------------------------------- ------------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-F41E74DF-EE54-4EB1-8609-49C6D324ADF5}<!-- End Header -->

Use of JAAS Login Utility {#JSSEC-GUID-F41E74DF-EE54-4EB1-8609-49C6D324ADF5 .sect1}
=========================

<div>
<span></span>

The previous two tutorials, [JAAS
Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
and [JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F),
show how you can use the <span class="apiname">LoginContext</span> and
<span class="apiname">Subject</span> classes to write a program to

-   authenticate the user to verify his or her identity and
-   associate an instance of a particular class representing the user (a
    <span class="apiname">Subject</span> instance) with an access
    control context in such a way that subsequent security-sensitive
    operations will be allowed if the current policy grants the user the
    required permissions.

This tutorial describes a Login utility that performs the above
operations and then executes any specified application as the
authenticated user.

Use of the Login utility with a sample application is demonstrated in
this tutorial. The next tutorial, [Use of JAAS Login Utility and Java
GSS-API for Secure Message
Exchanges](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8),
a client/server application using the Java GSS-API, also uses the Login
utility.

It is not necessary to read the previous two tutorials on JAAS
authentication and authorization prior to reading this one. However, you
may want to refer to some sections in those tutorials to obtain further
details regarding certain topics, such as [JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F).
You should also read [Appendix B: JAAS Login Configuration
File](appendix-b-jaas-login-configuration-file.html#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)
for information as to what a login configuration file is, since one is
needed for this and all other tutorials in this series.

As with all tutorials in this series of tutorials, the underlying
technology used to support authentication is Kerberos. See [Kerberos
Requirements](kerberos-requirements1.html#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998).

-   [What You Need to Know About the Login
    Utility](use-jaas-login-utility.html#GUID-F92EBF93-2E18-4006-86CC-3D4C0DC6174E)
-   [Application and Other File
    Requirements](use-jaas-login-utility.html#GUID-A988A760-1F2E-4665-AC8B-BACDEBAED5B5)
-   [The Sample Application
    Program](use-jaas-login-utility.html#GUID-78D65FB0-34DC-4DEE-95A4-0C0BD1AE6330)
-   [The Login Configuration
    File](use-jaas-login-utility.html#GUID-DFC52892-6206-4D1F-96B3-B8F11C2536E1)
-   [The Policy
    File](use-jaas-login-utility.html#GUID-FF7EBCB2-F3B9-4483-86A1-7EDA7ECA1689)
-   [Running the Sample Program with the Login
    Utility](use-jaas-login-utility.html#GUID-B3F1D0B9-D58A-469B-AF56-9636FE86FF0F)

If you want to first see the tutorial code in action, you can skip
directly to [Running the Sample Program with the Login
Utility](use-jaas-login-utility.html#GUID-B3F1D0B9-D58A-469B-AF56-9636FE86FF0F)
and then go back to the other sections to learn more.

</div>
<div class="sect2">
[]{#GUID-F92EBF93-2E18-4006-86CC-3D4C0DC6174E}

What You Need to Know About the Login Utility {#JSSEC-GUID-F92EBF93-2E18-4006-86CC-3D4C0DC6174E .sect2}
---------------------------------------------

<div>
You do not need to understand the code contained in
[`Login.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__LOGIN.JAVA-338935D0);
you can just use it as is. However, you need to understand some facts
about what it does so that your program, policy file, and login
configuration file will properly work with it. Below is a summary of
these facts, followed by sections with further information and examples.

The `Login`{.codeph} class does the following:

-   Assumes it is passed, as arguments, your application\'s top-level
    class name, followed by any arguments your application may require.
-   Assumes that the class name of your top-level application class is
    also used as the name of the entry to be looked up in your login
    configuration file.
-   Specifies the <span class="apiname">TextCallbackHandler</span> class
    (from the `com.sun.security.auth.callback`{.codeph} package) as the
    class to be used when communicating with the user. This class can
    prompt the user for a user name and password.
-   Uses a <span class="apiname">LoginContext</span> to authenticate the
    user. The <span class="apiname">LoginContext</span> invokes the
    appropriate authentication technology, or
    <span class="apiname">LoginModule</span>, to perform the
    authentication. <span class="apiname">LoginModules</span> use a
    <span class="apiname">CallbackHandler</span> (in our case,
    <span class="apiname">TextCallbackHandler</span>) as needed to
    communicate with the user.
-   Allows the user three attempts to successfully log in.
-   Creates an instance of the `MyAction`{.codeph} class (also in
    `Login.java`{.codeph}), passing it the application arguments, if
    any.
-   Invokes `Subject.doAsPrivileged`{.codeph}, passing it a
    <span class="apiname">Subject</span> representing the user, the
    `MyAction`{.codeph} instance, and a null
    <span class="apiname">AccessControlContext</span>. The result is
    that the public static main method from your application is invoked
    and your application code is considered to be executed on behalf of
    the user.

</div>
</div>
<div class="sect2">
[]{#GUID-A988A760-1F2E-4665-AC8B-BACDEBAED5B5}

Application and Other File Requirements {#JSSEC-GUID-A988A760-1F2E-4665-AC8B-BACDEBAED5B5 .sect2}
---------------------------------------

<div>
To utilize the Login utility to authenticate the user and execute your
application, you may need a small number of additions or modifications
to your login configuration file and policy file, as described in the
following.

-   [Application
    Requirements](use-jaas-login-utility.html#GUID-2DA66897-B872-4DB3-B580-2A884321B52E)
-   [Login Configuration File
    Requirements](use-jaas-login-utility.html#GUID-1475ADA8-4B71-4022-8295-209AFCEB89D9)
-   [Policy File
    Requirements](use-jaas-login-utility.html#GUID-6F2F1165-FF1F-46BB-B18B-1D13E1A51BAF)

</div>
<div class="sect3">
[]{#GUID-2DA66897-B872-4DB3-B580-2A884321B52E}

### Application Requirements {#JSSEC-GUID-2DA66897-B872-4DB3-B580-2A884321B52E .sect3}

<div>
In order to utilize the Login utility, your application code does not
need anything special. All you need is for the entry point of your
application to be the `main`{.codeph} method of a class you write, as
usual.

The way to invoke Login such that it will authenticate the user and then
instantiate `MyAction`{.codeph} to invoke your application is the
following:

``` {.oac_no_warn dir="ltr"}
java <options> Login <AppName> <app arguments> 
```

where `<AppName>`{.codeph} is your application\'s top-level class name
and `<app arguments>`{.codeph} are any arguments required by your
application. See [Running the Sample Program with the Login
Utility](use-jaas-login-utility.html#GUID-B3F1D0B9-D58A-469B-AF56-9636FE86FF0F)
for the full command used for this tutorial.

</div>
</div>
<div class="sect3">
[]{#GUID-1475ADA8-4B71-4022-8295-209AFCEB89D9}

### Login Configuration File Requirements {#JSSEC-GUID-1475ADA8-4B71-4022-8295-209AFCEB89D9 .sect3}

<div>
Whenever a LoginContext is used to authenticate the user, you need a
login configuration file to specify the desired login module. See the
[The Login
Configuration](jaas-authentication.html#GUID-C595253D-3817-4CA6-9336-D7D5159C9680)
section in the JAAS authentication tutorial for more information as to
what a login configuration file is and what it contains.

When you use the Login utility, the name for the login configuration
file entry must be exactly the same as your top-level application class
name. See [The Login Configuration
File](use-jaas-login-utility.html#GUID-DFC52892-6206-4D1F-96B3-B8F11C2536E1)
in this tutorial for an example.

</div>
</div>
<div class="sect3">
[]{#GUID-6F2F1165-FF1F-46BB-B18B-1D13E1A51BAF}

### Policy File Requirements {#JSSEC-GUID-6F2F1165-FF1F-46BB-B18B-1D13E1A51BAF .sect3}

<div>
Whenever you run an application with a security manager, you need a
policy indicating the permissions granted to specific code, or to
specific code being executed by a specific user (or users). One way of
specifying the policy is by `grant`{.codeph} statements in a policy
file. See [The Policy
File](use-jaas-login-utility.html#GUID-FF7EBCB2-F3B9-4483-86A1-7EDA7ECA1689)
for more information.

If you use the Login utility to invoke your application, then you will
need to grant it various permissions, as described in [Permissions
Required by the Login and MyAction
Classes](use-jaas-login-utility.html#GUID-9E9CAD3D-5F80-424E-AE19-B102064054E4).

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-78D65FB0-34DC-4DEE-95A4-0C0BD1AE6330}

The Sample Application Program {#JSSEC-GUID-78D65FB0-34DC-4DEE-95A4-0C0BD1AE6330 .sect2}
------------------------------

<div>
The
[`Sample.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLE.JAVA-3389388B)
application used for this tutorial performs the same actions as the
`SampleAction.java`{.codeph} application did in the previous ([JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F))
tutorial. It does the following:

-   Reads and prints the value of the `java.home`{.codeph} system
    property,
-   Reads and prints the value of the `user.home`{.codeph} system
    property, and
-   Determines whether or not a file named `foo.txt`{.codeph} exists in
    the current directory.

</div>
</div>
<div class="sect2">
[]{#GUID-DFC52892-6206-4D1F-96B3-B8F11C2536E1}

The Login Configuration File {#JSSEC-GUID-DFC52892-6206-4D1F-96B3-B8F11C2536E1 .sect2}
----------------------------

<div>
The
[`sample.conf`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLE.CONF-33893A5C)
login configuration file for this tutorial contains a single entry, just
like the login configuration file for the previous ([JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F))
tutorial. The entry contents are the same since the class implementing
the desired authentication technology in both cases is the
<span class="apiname">Krb5LoginModule</span> in the
`com.sun.security.auth.module`{.codeph} package.

The only difference is the name used for the entry. In the previous
tutorial we used the name \"JaasSample\", since that is the name used by
the <span class="apiname">JaasAzn</span> class to look up the entry.
When you use the Login utility with your application, it expects the
name for your login configuration file entry to be the same as the name
of your top-level application class. That application class for this
tutorial is named \"Sample\" so that must also be the name of the login
configuration file entry. Thus the login configuration file looks like
the following:

``` {.oac_no_warn dir="ltr"}
Sample {
   com.sun.security.auth.module.Krb5LoginModule required;
};
```

The \"required\" indicates that login using the
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
<div class="sect2">
[]{#GUID-FF7EBCB2-F3B9-4483-86A1-7EDA7ECA1689}

The Policy File {#JSSEC-GUID-FF7EBCB2-F3B9-4483-86A1-7EDA7ECA1689 .sect2}
---------------

<div>
The <span class="apiname">Login</span>,
<span class="apiname">MyAction</span>, and
<span class="apiname">Sample</span> classes all perform some
security-sensitive operations and thus relevant permissions are required
in a policy file,
[`sample.policy`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLE.POLICY-33893EE3),
in order for the operations to be executed.

</div>
<div class="sect3">
[]{#GUID-9E9CAD3D-5F80-424E-AE19-B102064054E4}

### Permissions Required by the Login and MyAction Classes {#JSSEC-GUID-9E9CAD3D-5F80-424E-AE19-B102064054E4 .sect3}

<div>
For this tutorial, you will create a `Login.jar`{.codeph} JAR file
containing the `Login.class`{.codeph} and `MyAction.class`{.codeph}
files. You need to grant `Login.jar`{.codeph} various permissions,
specifically the ones required for invoking the security-sensitive
methods the `Login.jar`{.codeph} classes call, as well as all the
permissions required by your application. Otherwise, access control
checks will fail.

The simplest thing to do, and what we recommend, is to grant
`Login.jar AllPermission`{.codeph}. For this tutorial, the
`Login.jar`{.codeph} file is assumed to be in the current directory and
the policy file includes the following:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./Login.jar" {
   permission java.security.AllPermission;
};
```

</div>
</div>
<div class="sect3">
[]{#GUID-25C2E3C5-F329-40F3-A701-878526AFEEB2}

### Permissions Required by Sample {#JSSEC-GUID-25C2E3C5-F329-40F3-A701-878526AFEEB2 .sect3}

<div>
(Note: This section is essentially a modified copy of the [Permissions
Required by
SampleAction](jaas-authorization.html#GUID-9ADEB874-E415-4ABC-BB20-70FBBFF87F84)
section from the previous ([JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F))
tutorial, since `Sample`{.codeph} and `SampleAction`{.codeph} perform
the same operations and thus require the same permissions.)

The `Sample`{.codeph} code does three operations for which permissions
are required. It

-   reads the value of the `java.home`{.codeph} system property.
-   reads the value of the `user.home`{.codeph} system property.
-   checks to see whether or not a file named `foo.txt`{.codeph} exists
    in the current directory.

The permissions required for these operations are the following:

``` {.oac_no_warn dir="ltr"}
permission java.util.PropertyPermission "java.home", "read";
permission java.util.PropertyPermission "user.home", "read";
permission java.io.FilePermission "foo.txt", "read";
```

We need to grant these permissions to the code in
`Sample.class`{.codeph}, which we will place in a JAR file named
`Sample.jar`{.codeph}. However, our `grant`{.codeph} statement will
grant the permissions not just to the <span class="variable">code</span>
but to a specific authenticated user executing the code. This
illustrates how you can use a Principal designation in a
`grant`{.codeph} statement to restrict execution of security-sensitive
operations in code to a specific user rather than allowing the
permissions to all users executing the code.

Thus, as explained in [JAAS
Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F),
our `grant`{.codeph} statement looks like the following:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./Sample.jar",
    Principal javax.security.auth.kerberos.KerberosPrincipal 
        "your_user_name@your_realm"  {

   permission java.util.PropertyPermission "java.home", "read";
   permission java.util.PropertyPermission "user.home", "read";
   permission java.io.FilePermission "foo.txt", "read";
};
```

<div class="infoboxnote" id="GUID-25C2E3C5-F329-40F3-A701-878526AFEEB2__GUID-E1C8CE5D-F8A4-4328-A22E-F91FAF17858C">
Note:

<span class="bold">Important: You must substitute your Kerberos user
name (complete with \"@\" and realm) for
`your_user_name@your_realm`{.codeph}.</span>

For example, if your user name is `mjones`{.codeph} and your realm is
`KRBNT-OPERATIONS.ABC.COM`{.codeph}, you would use
`mjones@KRBNT-OPERATIONS.ABC.COM`{.codeph}.

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-B3F1D0B9-D58A-469B-AF56-9636FE86FF0F}

Running the Sample Program with the Login Utility {#JSSEC-GUID-B3F1D0B9-D58A-469B-AF56-9636FE86FF0F .sect2}
-------------------------------------------------

<div>
To execute the `Sample`{.codeph} application with the Login utility, do
the following:

1.  Place the following files into a directory:
    -   The
        [`Login.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__LOGIN.JAVA-338935D0)
        source file.
    -   The
        [`Sample.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLE.JAVA-3389388B)
        source file.
    -   The
        [`sample.conf`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLE.CONF-33893A5C)
        login configuration file.
    -   The
        [`sample.policy`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLE.POLICY-33893EE3)
        policy file.
2.  Replace `your_user_name@your_realm`{.codeph} in
    `sample.policy`{.codeph} with your user name and realm.
3.  Compile `Login.java`{.codeph} and `Sample.java`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    javac Login.java Sample.java
    ```

    Note that `Login.java`{.codeph} contains two classes and thus
    compiling `Login.java`{.codeph} creates `Login.class`{.codeph} and
    `MyAction.class`{.codeph}.

4.  Create a JAR file named `Login.jar`{.codeph} containing
    `Login.class and MyAction.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf Login.jar Login.class MyAction.class
    ```

5.  Create a JAR file named `Sample.jar`{.codeph} containing
    `Sample.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf Sample.jar Sample.class
    ```

6.  Execute the `Login`{.codeph} class, specifying

    -   by an appropriate `-classpath`{.codeph} clause that classes
        should be searched for in the `Login.jar`{.codeph} and
        `Sample.jar`{.codeph} JAR files,
    -   by `-Djava.security.manager`{.codeph} that a security manager
        should be installed,
    -   by `-Djava.security.krb5.realm=<your_realm>`{.codeph} that your
        Kerberos realm is the one specified.
    -   by `-Djava.security.krb5.kdc=<your_kdc>`{.codeph} that your
        Kerberos KDC is the one specified.
    -   by `-Djava.security.policy=sample.policy`{.codeph} that the
        policy file to be used is `sample.policy`{.codeph}, and
    -   by `-Djava.security.auth.login.config=sample.conf`{.codeph} that
        the login configuration file to be used is
        `sample.conf`{.codeph}.

    You pass the name of your application (in this case,
    `Sample`{.codeph}) as an argument to `Login`{.codeph}. You would
    then add as arguments any arguments required by your application,
    but in our case `Sample`{.codeph} does not require any.

    Below are the full commands to use for Windows, Solaris, Linux, and
    macOS. The only difference is that on Windows you use semicolons to
    separate classpath items, while you use colons for that purpose on
    Solaris, Linux, and macOS. <span class="bold">Be sure to replace
    `<your_realm>`{.codeph} with your Kerberos realm, and
    `<your_kdc>`{.codeph} with your Kerberos KDC.</span>

    Here is the full command for Windows:

    ``` {.oac_no_warn dir="ltr"}
    java -classpath Login.jar;Sample.jar 
     -Djava.security.manager 
     -Djava.security.krb5.realm=<your_realm> 
     -Djava.security.krb5.kdc=<your_kdc> 
     -Djava.security.policy=sample.policy 
     -Djava.security.auth.login.config=sample.conf Login Sample
    ```

    Here is the full command for Solaris, Linux, and macOS:

    ``` {.oac_no_warn dir="ltr"}
    java -classpath Login.jar:Sample.jar 
     -Djava.security.manager 
     -Djava.security.krb5.realm=<your_realm> 
     -Djava.security.krb5.kdc=<your_kdc> 
     -Djava.security.policy=sample.policy 
     -Djava.security.auth.login.config=sample.conf Login Sample
    ```

    Type the full command on one line. Multiple lines are used here for
    legibility. If the command is too long for your system, you may need
    to place it in a .bat file (for Windows) or a .sh file (for Solaris,
    Linux, and macOS) and then run that file to execute the command.

    You will be prompted for your Kerberos user name and password, and
    the underlying Kerberos login module specified in the login
    configuration file will log you into Kerberos. Once authentication
    is successfully completed, the `Sample`{.codeph} code will be
    executed on behalf of you, the user. The `sample.policy`{.codeph}
    policy file grants you the required permissions, so you will see a
    display of the values of your `java.home`{.codeph} and
    `user.home`{.codeph} system properties and a statement as to whether
    or not you have a file named `foo.txt`{.codeph} in the current
    directory.

    For login troubleshooting suggestions, see
    [Troubleshooting](troubleshooting.html#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

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
| --- ---------------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| ------- --           | L |             <span cl |
|           [![Previou | o | ass="icon">Contents< |
| s](../../dcommon/gif | g | /span>](toc.htm)     |
| s/leftnav.gif)\      | o |   -- --------------- |
|                      | ] | -------------------- |
|               [![Nex | ( | -------------------- |
| t](../../dcommon/gif | . | ---                  |
| s/rightnav.gif)\     | . |                      |
|                      | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](j | / |                      |
| aas-authorization.ht | d |                      |
| m)   <span class="ic | c |                      |
| on">Next</span>](use | o |                      |
| -jaas-login-utility- | m |                      |
| and-java-gss-api-sec | m |                      |
| ure-message-exchange | o |                      |
| s.htm)               | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| --- ---------------- | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| ------- --           | a |                      |
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
