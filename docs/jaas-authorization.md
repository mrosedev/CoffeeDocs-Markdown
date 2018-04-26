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

  -------------------------------------------------------------- ------------------------------------------------------------- --
          [![Previous](../../dcommon/gifs/leftnav.gif)\                   [![Next](../../dcommon/gifs/rightnav.gif)\           
   <span class="icon">Previous</span>](jaas-authentication.htm)   <span class="icon">Next</span>](use-jaas-login-utility.htm)  
  -------------------------------------------------------------- ------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F}<!-- End Header -->

JAAS Authorization {#JSSEC-GUID-69241059-CCD0-49F6-838F-DDC752F9F19F .sect1}
==================

<div>
<span></span>

This tutorial expands the program and policy file developed in the [JAAS
Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
tutorial to demonstrate the JAAS authorization component, which ensures
the authenticated caller has the access control rights (permissions)
required to do subsequent security-sensitive operations. Since the
authorization component requires that the user authentication first be
completed, please read the [JAAS
Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
tutorial first if you have not already done so.

The rest of this tutorial consists of the following sections:

-   [What is JAAS
    Authorization?](jaas-authorization.html#GUID-95EBDFAE-D531-45ED-BF48-4CC122E483E1)
-   [How Is JAAS Authorization
    Performed?](jaas-authorization.html#GUID-9B40B33D-3618-4F98-9DDE-9A639F751CA4)
    -   [How Do You Make Principal-Based Policy File
        Statements?](jaas-authorization.html#GUID-80F0B546-1E95-457B-8EF7-5BB1519E20A4)
    -   [How Do You Associate a Subject with an Access Control
        Context?](jaas-authorization.html#GUID-86CC2E0C-58B9-4E35-91E1-EC130EE2E4FC)
-   [The Authorization Tutorial
    Code](jaas-authorization.html#GUID-6C7F947A-E2F3-4C1A-BF58-8198E4E9B6D3)
-   [The Login Configuration
    File](jaas-authorization.html#GUID-C7E4B4C5-1541-4482-BA11-98A1D489CA76)
-   [The Policy
    File](jaas-authorization.html#GUID-19567566-CC1A-4440-AE33-D7C6AB305D3F)
-   [Running the Authorization Tutorial
    Code](jaas-authorization.html#GUID-F22DFBEC-7DF0-4CFB-B882-B5A58C2C76B1)

If you want to first see the tutorial code in action, you can skip
directly to [Running the Authorization Tutorial
Code](jaas-authorization.html#GUID-F22DFBEC-7DF0-4CFB-B882-B5A58C2C76B1)
and then go back to the other sections to learn more.

</div>
<div class="sect2">
[]{#GUID-95EBDFAE-D531-45ED-BF48-4CC122E483E1}

What is JAAS Authorization? {#JSSEC-GUID-95EBDFAE-D531-45ED-BF48-4CC122E483E1 .sect2}
---------------------------

<div>
JAAS authorization extends the existing Java security architecture that
uses a security policy (see [Default Policy Implementation and Policy
File
Syntax](permissions-jdk1.html#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D))
to specify what access rights are granted to executing code. That
architecture is <span class="variable">code-centric</span>. That is, the
permissions are granted based on code characteristics: where the code is
coming from and whether it is digitally signed and if so by whom. We saw
an example of this in the `jaasacn.policy`{.codeph} file used in the
[JAAS
Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
tutorial. That file contains the following:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./JaasAcn.jar" {
   permission javax.security.auth.AuthPermission 
                    "createLoginContext.JaasSample";
};
```

This grants the code in the `JaasAcn.jar`{.codeph} file, located in the
current directory, the specified permission. (No signer is specified, so
it doesn\'t matter whether the code is signed or not.)

JAAS authorization augments the existing code-centric access controls
with new <span class="variable">user-centric</span> access controls.
Permissions can be granted based not just on what code is running but
also on <span class="variable">who</span> is running it.

When an application uses JAAS authentication to authenticate the user
(or other entity such as a service), a
[<span class="apiname">Subject</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Subject.html)
is created as a result. The purpose of the
<span class="apiname">Subject</span> is to represent the authenticated
user. A <span class="apiname">Subject</span> is comprised of a set of
[<span class="apiname">Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)s,
where each <span class="apiname">Principal</span> represents an identity
for that user. For example, a <span class="apiname">Subject</span> could
have a name <span class="apiname">Principal</span> (\"Susan Smith\") and
a Social Security Number Principal (\"987-65-4321\"), thereby
distinguishing this <span class="apiname">Subject</span> from other
Subjects.

Permissions can be granted in the policy to specific
<span class="apiname">Principal</span>s. After the user has been
authenticated, the application can associate the
<span class="apiname">Subject</span> with the current access control
context. For each subsequent security-checked operation, (a local file
access, for example), the Java runtime will automatically determine
whether the policy grants the required permission only to a specific
<span class="apiname">Principal</span> and if so, the operation will be
allowed only if the <span class="apiname">Subject</span> associated with
the access control context contains the designated
<span class="apiname">Principal</span>.

</div>
</div>
<div class="sect2">
[]{#GUID-9B40B33D-3618-4F98-9DDE-9A639F751CA4}

How Is JAAS Authorization Performed? {#JSSEC-GUID-9B40B33D-3618-4F98-9DDE-9A639F751CA4 .sect2}
------------------------------------

<div>
To make JAAS authorization take place, the following is required:

-   The user must be authenticated, as described in the [JAAS
    Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
    tutorial.
-   Principal-based entries must be configured in the security policy.
    See [How Do You Make Principal-Based Policy File
    Statements?](jaas-authorization.html#GUID-80F0B546-1E95-457B-8EF7-5BB1519E20A4)
-   The Subject that is the result of authentication must be associated
    with the current access control context. See [How Do You Associate a
    Subject with an Access Control
    Context?](jaas-authorization.html#GUID-86CC2E0C-58B9-4E35-91E1-EC130EE2E4FC)

</div>
<div class="sect3">
[]{#GUID-80F0B546-1E95-457B-8EF7-5BB1519E20A4}

### How Do You Make Principal-Based Policy File Statements? {#JSSEC-GUID-80F0B546-1E95-457B-8EF7-5BB1519E20A4 .sect3}

<div>
Policy file `grant`{.codeph} statements can now optionally include one
or more Principal fields (see [Default Policy Implementation and Policy
File
Syntax](permissions-jdk1.html#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D)).
Inclusion of a Principal field indicates that the user or other entity
represented by the specified Principal, executing the specified code,
has the designated permissions.

Thus, the basic format of a `grant`{.codeph} statement is now

``` {.oac_no_warn dir="ltr"}
grant <signer(s) field>, <codeBase URL> 
  <Principal field(s)> {
    permission perm_class_name "target_name", "action";
    ....
    permission perm_class_name "target_name", "action";
  };
```

where each of the signer, codeBase and Principal fields is optional and
the order between the fields doesn\'t matter.

A Principal field looks like the following:

``` {.oac_no_warn dir="ltr"}
Principal Principal_class "principal_name"
```

That is, it is the word \"Principal\" (where case doesn\'t matter)
followed by the (fully qualified) name of a Principal class and a
principal name.

A <span class="apiname">Principal</span> class is a class that
implements the
[<span class="apiname">java.security.Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
interface. All Principal objects have an associated name that can be
obtained by calling their `getName`{.codeph} method. The format used for
the name is dependent on each <span class="apiname">Principal</span>
implementation.

The type of <span class="apiname">Principal</span> placed in the
<span class="apiname">Subject</span> created by the Kerberos
authentication mechanism used by this tutorial is
`javax.security.auth.kerberos.KerberosPrincipal`{.codeph}, so that is
what should be used as the `Principal_class`{.codeph} part of our
`grant`{.codeph} statement\'s <span class="apiname">Principal</span>
designation. User names for `KerberosPrincipal`{.codeph}s are of the
form `name@realm`{.codeph}. Thus, if the user name is `mjones`{.codeph}
and the realm is `KRBNT-OPS.ABC.COM`{.codeph}, the full
`principal_name`{.codeph} designation to use in the `grant`{.codeph}
statement is `mjones@KRBNT-OPS.ABC.COM`{.codeph}.

It is possible to include more than one Principal field in a
`grant`{.codeph} statement. If multiple Principal fields are specified,
then the permissions in that `grant`{.codeph} statement are granted only
if the Subject associated with the current access control context
contains <span class="variable">all</span> of those Principals.

To grant the same set of permissions to different Principals, create
multiple `grant`{.codeph} statements where each lists the permissions
and contains a single Principal field designating one of the Principals.

The policy file for this tutorial includes one `grant`{.codeph}
statement with a Principal field:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./SampleAction.jar",
    Principal javax.security.auth.kerberos.KerberosPrincipal 
        "your_user_name@your_realm"  {

   permission java.util.PropertyPermission "java.home", "read";
   permission java.util.PropertyPermission "user.home", "read";
   permission java.io.FilePermission "foo.txt", "read";
};
```

where you substitute your Kerberos user name (complete with \"@\" and
realm) for `your_user_name@your_realm`{.codeph}. This specifies that the
indicated permissions are granted to the specified principal executing
the code in `SampleAction.jar`{.codeph}.

</div>
</div>
<div class="sect3">
[]{#GUID-86CC2E0C-58B9-4E35-91E1-EC130EE2E4FC}

### How Do You Associate a Subject with an Access Control Context? {#JSSEC-GUID-86CC2E0C-58B9-4E35-91E1-EC130EE2E4FC .sect3}

<div>
To create and associate a Subject with an access control context, you
need the following:

-   The user must first be authenticated, as described in [JAAS
    Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623).
-   The static `doAs`{.codeph} method from the
    <span class="apiname">Subject</span> class must be called, passing
    it an authenticated <span class="apiname">Subject</span> and a
    [<span class="apiname">java.security.PrivilegedAction</span>](https://docs.oracle.com/javase/10/docs/api/java/security/PrivilegedAction.html)
    or
    [<span class="apiname">java.security.PrivilegedExceptionAction</span>](https://docs.oracle.com/javase/10/docs/api/java/security/PrivilegedExceptionAction.html).
    (See [Appendix A: API for Privileged
    Blocks](java-se-platform-security-architecture.html#GUID-BB3C8FB3-1A1A-47F3-8536-3952B84F46F2 "This section explains what privileged code is and what it is used for. It also shows you how to use the doPrivileged API.")
    for a comparison of <span class="apiname">PrivilegedAction</span>
    and <span class="apiname">PrivilegedExceptionAction</span>.) The
    `doAs`{.codeph} method associates the provided
    <span class="apiname">Subject</span> with the current access control
    context and then invokes the `run`{.codeph} method from the action.
    The `run`{.codeph} method implementation contains all the code to be
    executed as the specified <span class="apiname">Subject</span>. The
    action thus executes as the specified
    <span class="apiname">Subject</span>.

    The static `doAsPrivileged`{.codeph} method from the
    <span class="apiname">Subject</span> class may be called instead of
    the `doAs`{.codeph} method. In addition to the parameters passed to
    `doAs`{.codeph}, `doAsPrivileged`{.codeph} requires a third
    parameter: an <span class="apiname">AccessControlContext</span>.
    Unlike `doAs`{.codeph}, which associates the provided Subject with
    the current access control context, `doAsPrivileged`{.codeph}
    associates the <span class="apiname">Subject</span> with the
    provided access control context. See [doAs versus
    doAsPrivileged](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-97198A0C-B488-4D24-A242-CAFA8F70DFA5)
    in the JAAS Reference Guide for a comparison of those methods.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-6C7F947A-E2F3-4C1A-BF58-8198E4E9B6D3}

The Authorization Tutorial Code {#JSSEC-GUID-6C7F947A-E2F3-4C1A-BF58-8198E4E9B6D3 .sect2}
-------------------------------

<div>
The code for this tutorial consists of two files:

-   [`JaasAzn.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JAASAZN.JAVA-33892F00)
    is exactly the same as the `JaasAcn.java`{.codeph} from the [JAAS
    Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
    tutorial except for the additional code needed to call
    `Subject.doAsPrivileged`{.codeph}.
-   [`SampleAction.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLEACTION.JAVA-33893145)
    contains the <span class="apiname">SampleAction</span> class. This
    class implements <span class="apiname">PrivilegedAction</span> and
    has a `run`{.codeph} method that contains all the code we want to be
    executed with <span class="apiname">Principal</span>-based
    authorization checks.

</div>
<div class="sect3">
[]{#GUID-EEBB584B-80FA-4EDD-B57A-BED4CCFE4EB4}

### JaasAzn.java {#JSSEC-GUID-EEBB584B-80FA-4EDD-B57A-BED4CCFE4EB4 .sect3}

<div>
[`JaasAzn.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JAASAZN.JAVA-33892F00)
is exactly the same as the `JaasAcn.java`{.codeph} code used in the
previous tutorial except with three statements added at the end of the
`main`{.codeph} method, after the authentication is done. These
statements result in (1) association of a
<span class="apiname">Subject</span> representing the authenticated user
with the current access control context and (2) execution of the code in
the `run`{.codeph} method of `SampleAction`{.codeph}. Associating the
<span class="apiname">Subject</span> with the access control context
enables security-sensitive operations in the `SampleAction`{.codeph}
`run`{.codeph} method (and any code it invokes directly or indirectly)
to be executed if a <span class="apiname">Principal</span> representing
the authenticated user is granted the required permissions in the
current policy.

Like `JaasAcn.java`{.codeph}, `JaasAzn.java`{.codeph} instantiates a
<span class="apiname">LoginContext</span> `lc`{.codeph} and calls its
`login`{.codeph} method to perform the authentication. If successful,
the authenticated <span class="apiname">Subject</span> (which includes a
<span class="apiname">Principal</span> representing the user) is
obtained by calling the <span class="apiname">LoginContext</span>\'s
`getSubject`{.codeph} method:

``` {.oac_no_warn dir="ltr"}
Subject mySubject = lc.getSubject();
```

The `main`{.codeph} method then calls `Subject.doAsPrivileged`{.codeph},
passing it the authenticated <span class="apiname">Subject</span>
`mySubject`{.codeph}, a <span class="apiname">PrivilegedAction</span>
(`SampleAction`{.codeph}) and a `null`{.codeph}
<span class="apiname">AccessControlContext</span>, as described in the
following.

The `SampleAction`{.codeph} class is instantiated via the following:

``` {.oac_no_warn dir="ltr"}
PrivilegedAction action = new SampleAction();
```

The call to `Subject.doAsPrivileged`{.codeph} is performed via:

``` {.oac_no_warn dir="ltr"}
Subject.doAsPrivileged(mySubject, action, null);
```

The `doAsPrivileged`{.codeph} method invokes execution of the
`run`{.codeph} method in the
<span class="apiname">PrivilegedAction</span> `action`{.codeph}
(`SampleAction`{.codeph}) to initiate execution of the rest of the code,
which is considered to be executed on behalf of the Subject
`mySubject`{.codeph}.

Passing `null`{.codeph} as the
<span class="apiname">AccessControlContext</span> (third) argument to
`doAsPrivileged`{.codeph} indicates that `mySubject`{.codeph} should be
associated with a new empty
<span class="apiname">AccessControlContext</span>. The result is that
security checks occurring during execution of `SampleAction`{.codeph}
will only require permissions for the `SampleAction`{.codeph} code
itself (or other code it invokes), running as `mySubject`{.codeph}. Note
that the caller of `doAsPrivileged`{.codeph} (and the callers on the
execution stack at the time `doAsPrivileged`{.codeph} was called) do not
require any permissions while the action executes.

</div>
</div>
<div class="sect3">
[]{#GUID-994AEA05-292D-418A-8C2D-A32E3A9AC7D3}

### SampleAction.java {#JSSEC-GUID-994AEA05-292D-418A-8C2D-A32E3A9AC7D3 .sect3}

<div>
[`SampleAction.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLEACTION.JAVA-33893145)
contains the <span class="apiname">SampleAction</span> class. This class
implements `java.security.PrivilegedAction`{.codeph} and has a
`run`{.codeph} method that contains all the code we want to be executed
as the Subject `mySubject`{.codeph}. For this tutorial, we will perform
three operations, each of which cannot be done unless code has been
granted required permissions. We will:

-   Read and print the value of the `java.home`{.codeph} system
    property,
-   Read and print the value of the `user.home`{.codeph} system
    property, and
-   Determine whether or not a file named `foo.txt`{.codeph} exists in
    the current directory.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-C7E4B4C5-1541-4482-BA11-98A1D489CA76}

The Login Configuration File {#JSSEC-GUID-C7E4B4C5-1541-4482-BA11-98A1D489CA76 .sect2}
----------------------------

<div>
The login configuration file used for this tutorial can be exactly the
same as that used by the [JAAS
Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
tutorial. Thus we can use
[<span class="apiname">jaas.conf</span>](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JASS.CONF-33892AE7),
which contains just one entry:

``` {.oac_no_warn dir="ltr"}
JaasSample {
  com.sun.security.auth.module.Krb5LoginModule required;
};
```

This entry is named \"JaasSample\" and that is the name that both our
tutorial applications `JaasAcn`{.codeph} and `JaasAzn`{.codeph} use to
refer to it. The entry specifies that the
<span class="apiname">LoginModule</span> to be used to do the user
authentication is the <span class="apiname">Krb5LoginModule</span> in
the `com.sun.security.auth.module`{.codeph} package and that this
<span class="apiname">Krb5LoginModule</span> is required to \"succeed\"
in order for authentication to be considered successful. The
<span class="apiname">Krb5LoginModule</span> succeeds only if the name
and password supplied by the user are successfully used to log the user
into the Kerberos KDC.

</div>
</div>
<div class="sect2">
[]{#GUID-19567566-CC1A-4440-AE33-D7C6AB305D3F}

The Policy File {#JSSEC-GUID-19567566-CC1A-4440-AE33-D7C6AB305D3F .sect2}
---------------

<div>
This authorization tutorial contains two classes, `JaasAzn`{.codeph} and
`SampleAction`{.codeph}. The code in each class contains some
security-sensitive operations and thus relevant permissions are required
in a policy file in order for the operations to be executed.

</div>
<div class="sect3">
[]{#GUID-90DA29A4-6980-49EB-B4F0-21E6678AB7A2}

### Permissions Required by JaasAzn {#JSSEC-GUID-90DA29A4-6980-49EB-B4F0-21E6678AB7A2 .sect3}

<div>
The main method of the `JaasAzn`{.codeph} class does two operations for
which permissions are required. It

-   creates a <span class="apiname">LoginContext</span>, and
-   calls the `doAsPrivileged`{.codeph} static method of the
    <span class="apiname">Subject</span> class.

The <span class="apiname">LoginContext</span> creation is exactly the
same as was done in the authentication tutorial, and it thus needs the
same `javax.security.auth.AuthPermission`{.codeph} permission with
target `createLoginContext.JaasSample`{.codeph}.

In order to call the `doAsPrivileged`{.codeph} method of the Subject
class, you need to have a `javax.security.auth.AuthPermission`{.codeph}
with target `doAsPrivileged`{.codeph}.

Assuming the `JaasAzn`{.codeph} class is placed in a JAR file named
`JaasAzn.jar`{.codeph}, these permissions can be granted to the
`JaasAzn`{.codeph} code via the following `grant`{.codeph} statement in
the policy file:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./JaasAzn.jar" {
   permission javax.security.auth.AuthPermission 
                    "createLoginContext.JaasSample";
   permission javax.security.auth.AuthPermission "doAsPrivileged";
};
```

</div>
</div>
<div class="sect3">
[]{#GUID-9ADEB874-E415-4ABC-BB20-70FBBFF87F84}

### Permissions Required by SampleAction {#JSSEC-GUID-9ADEB874-E415-4ABC-BB20-70FBBFF87F84 .sect3}

<div>
The `SampleAction`{.codeph} code does three operations for which
permissions are required. It

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
`SampleAction.class`{.codeph}, which we will place in a JAR file named
`SampleAction.jar`{.codeph}. However, for this particular
`grant`{.codeph} statement we want to grant the permissions not just to
the <span class="variable">code</span> but to a specific user executing
the code, to demonstrate how to restrict access to a particular user.

Thus, as explained in [How Do You Make Principal-Based Policy File
Statements?](jaas-authorization.html#GUID-80F0B546-1E95-457B-8EF7-5BB1519E20A4),
our `grant`{.codeph} statement looks like the following:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./SampleAction.jar",
    Principal javax.security.auth.kerberos.KerberosPrincipal 
        "your_user_name@your_realm"  {

   permission java.util.PropertyPermission "java.home", "read";
   permission java.util.PropertyPermission "user.home", "read";
   permission java.io.FilePermission "foo.txt", "read";
};
```

You substitute your Kerberos user name (complete with \"@\" and realm)
for `your_user_name@your_realm`{.codeph}. For example, if your user name
is `mjones`{.codeph} and your realm is
`KRBNT-OPERATIONS.ABC.COM`{.codeph}, you would use
`mjones@KRBNT-OPERATIONS.ABC.COM`{.codeph}.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-F22DFBEC-7DF0-4CFB-B882-B5A58C2C76B1}

Running the Authorization Tutorial Code {#JSSEC-GUID-F22DFBEC-7DF0-4CFB-B882-B5A58C2C76B1 .sect2}
---------------------------------------

<div>
To execute our JAAS authorization tutorial code, all you have to do is

1.  Place the following files into a directory:
    -   The
        [`JaasAzn.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JAASAZN.JAVA-33892F00)
        source file.
    -   The
        [`SampleAction.java`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__SAMPLEACTION.JAVA-33893145)
        source file.
    -   The
        [`jaas.conf`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JASS.CONF-33892AE7)
        login configuration file.
    -   The
        [`jaasazn.policy`](source-code-jaas-and-java-gss-api-tutorials.html#GUID-09D4192C-D855-49D6-BC62-E08F49ADB4F8__JASSAZN.POLICY-3389344E)
        policy file.
2.  Replace `your_user_name@your_realm`{.codeph} in
    `jaasazn.policy`{.codeph} with your user name and realm.
3.  Compile `SampleAction.java`{.codeph} and `JaasAzn.java`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    javac SampleAction.java JaasAzn.java
    ```

4.  Create a JAR file named `JaasAzn.jar`{.codeph} containing
    `JaasAzn.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf JaasAzn.jar JaasAzn.class
    ```

5.  Create a JAR file named `SampleAction.jar`{.codeph} containing
    `SampleAction.class`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    jar -cvf SampleAction.jar SampleAction.class
    ```

6.  Execute the `JaasAzn`{.codeph} application, specifying

    a.  by an appropriate `-classpath`{.codeph} clause that classes
        should be searched for in the `JaasAzn.jar`{.codeph} and
        `SampleAction.jar`{.codeph} JAR files,
    b.  by `-Djava.security.manager`{.codeph} that a security manager
        should be installed,
    c.  by `-Djava.security.krb5.realm=<your_realm>`{.codeph} that your
        Kerberos realm is the one specified.
    d.  by `-Djava.security.krb5.kdc=<your_kdc>`{.codeph} that your
        Kerberos KDC is the one specified.
    e.  by `-Djava.security.policy=jaasazn.policy`{.codeph} that the
        policy file to be used is `jaasazn.policy`{.codeph}, and
    f.  by `-Djava.security.auth.login.config=jaas.conf`{.codeph} that
        the login configuration file to be used is `jaas.conf`{.codeph}.

    Below are the full commands to use for Windows, Solaris, Linux, and
    macOS. The only difference is that on Windows you use semicolons to
    separate classpath items, while you use colons for that purpose on
    Solaris, Linux, and macOS.

    <div class="infoboxnote" id="GUID-F22DFBEC-7DF0-4CFB-B882-B5A58C2C76B1__GUID-727C449C-ADA7-4370-8CA3-BF4DA171C9D7">
    Note:

    <span class="bold">Be sure to replace `<your_realm>`{.codeph} with
    your Kerberos realm, and `<your_kdc>`{.codeph} with your Kerberos
    KDC.</span>

    </div>
    Here is the full command for Windows:

    ``` {.oac_no_warn dir="ltr"}
    java -classpath JaasAzn.jar;SampleAction.jar 
     -Djava.security.manager 
     -Djava.security.krb5.realm=<your_realm> 
     -Djava.security.krb5.kdc=<your_kdc> 
     -Djava.security.policy=jaasazn.policy 
     -Djava.security.auth.login.config=jaas.conf JaasAzn
    ```

    Here is the full command for Solaris, Linux, and macOS:

    ``` {.oac_no_warn dir="ltr"}
    java -classpath JaasAzn.jar:SampleAction.jar 
     -Djava.security.manager 
     -Djava.security.krb5.realm=<your_realm> 
     -Djava.security.krb5.kdc=<your_kdc> 
     -Djava.security.policy=jaasazn.policy 
     -Djava.security.auth.login.config=jaas.conf JaasAzn
    ```

    Type the full command on one line. Multiple lines are used here for
    legibility. If the command is too long for your system, you may need
    to place it in a .bat file (for Windows) or a .sh file (for Solaris,
    Linux, and macOS) and then run that file to execute the command.

    You will be prompted for your Kerberos user name and password, and
    the underlying Kerberos authentication mechanism specified in the
    login configuration file will log you into Kerberos. If your login
    is successful, you will see the message \"Authentication
    succeeded!\" and if not, you will see \"Authentication Failed.\"

    For login troubleshooting suggestions, see
    [Troubleshooting](troubleshooting.html#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE).

    Once authentication is successfully completed, the rest of the
    program (in `SampleAction`{.codeph}) will be executed on behalf of
    you, the user, requiring you to have been granted appropriate
    permissions. The `jaasazn.policy`{.codeph} policy file grants you
    the required permissions, so you will see a display of the values of
    your `java.home`{.codeph} and `user.home`{.codeph} system properties
    and a statement as to whether or not you have a file named
    `foo.txt`{.codeph} in the current directory.

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
| ---- --------------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| ------ --            | l | dcommon/gifs/toc.gif |
|           [![Previou | e | )\                   |
| s](../../dcommon/gif | L |             <span cl |
| s/leftnav.gif)\      | o | ass="icon">Contents< |
|               [![Nex | g | /span>](toc.htm)     |
| t](../../dcommon/gif | o |   -- --------------- |
| s/rightnav.gif)\     | ] | -------------------- |
|                      | ( | -------------------- |
|    <span class="icon | . | ---                  |
| ">Previous</span>](j | . |                      |
| aas-authentication.h | / |                      |
| tm)   <span class="i | . |                      |
| con">Next</span>](us | . |                      |
| e-jaas-login-utility | / |                      |
| .htm)                | d |                      |
|   ------------------ | c |                      |
| -------------------- | o |                      |
| -------------------- | m |                      |
| ---- --------------- | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| ------ --            | / |                      |
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
