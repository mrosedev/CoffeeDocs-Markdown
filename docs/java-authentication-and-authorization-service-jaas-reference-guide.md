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

  ---------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------- --
                          [![Previous](../../dcommon/gifs/leftnav.gif)\                                            [![Next](../../dcommon/gifs/rightnav.gif)\                    
   <span class="icon">Previous</span>](java-authentication-and-authorization-service-jaas1.htm)   <span class="icon">Next</span>](appendix-b-jaas-login-configuration-file.htm)  
  ---------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-2A935F5E-0803-411D-B6BC-F8C64D01A25C}<!-- End Header -->

Java Authentication and Authorization Service (JAAS) Reference Guide {#JSSEC-GUID-2A935F5E-0803-411D-B6BC-F8C64D01A25C .sect1}
====================================================================

<div>
JAAS can be used for two purposes:

-   for <span class="variable">authentication</span> of users, to
    reliably and securely determine who is currently executing Java
    code, regardless of whether the code is running as an application,
    an applet, a bean, or a servlet; and
-   for <span class="variable">authorization</span> of users to ensure
    they have the access control rights (permissions) required to do the
    actions performed.

JAAS implements a Java version of the standard Pluggable Authentication
Module (PAM) framework.

Traditionally Java has provided codesource-based access controls (access
controls based on <span class="variable">where</span> the code
originated from and <span class="variable">who signed</span> the code).
It lacked, however, the ability to additionally enforce access controls
based on <span class="variable">who runs</span> the code. JAAS provides
a framework that augments the Java security architecture with such
support.

JAAS authentication is performed in a
<span class="variable">pluggable</span> fashion. This permits
applications to remain independent from underlying authentication
technologies. New or updated authentication technologies can be plugged
under an application without requiring modifications to the application
itself. Applications enable the authentication process by instantiating
a
[`LoginContext`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/LoginContext.html)
object, which in turn references a
[`Configuration`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
to determine the authentication technology or technologies, or
[`LoginModule`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html)(s),
to be used in performing the authentication. Typical
`LoginModule`{.codeph}s may prompt for and verify a user name and
password. Others may read and verify a voice or fingerprint sample.

Once the user or service executing the code has been authenticated, the
JAAS authorization component works in conjunction with the core Java SE
access control model to protect access to sensitive resources. Access
control decisions are based both on the executing code\'s
`CodeSource`{.codeph} <span class="variable">and</span> on the user or
service running the code, who is represented by a
[`Subject`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Subject.html)
object. The `Subject`{.codeph} is updated by a `LoginModule`{.codeph}
with relevant
[`Principal`{.codeph}s](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
and credentials if authentication succeeds.

</div>
<div class="sect2">
[]{#GUID-31AC2288-E4E8-42D9-821E-85385F1F2FE8}

Who Should Read This Document {#JSSEC-GUID-31AC2288-E4E8-42D9-821E-85385F1F2FE8 .sect2}
-----------------------------

<div>
This document is intended for experienced developers who require the
ability to design applications constrained by a
`CodeSource`{.codeph}-based and `Subject`{.codeph}-based security model.
It is also intended to be read by
<span class="apiname">LoginModule</span> developers (developers
implementing an authentication technology) prior to reading the [Java
Authentication and Authorization Service (JAAS): LoginModule
Developer\'s
Guide](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A).

You may wish to first read [JAAS Authentication
Tutorial](jaas-authentication-tutorial.htm#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
and [JAAS Authorization
Tutorial](jaas-authorization-tutorial.htm#GUID-D43CF965-8A5F-4A23-A2AF-F41DD5F8B411)
to get an overview of how to use JAAS and to see sample code in action,
and then return to this document for further information.

</div>
</div>
<div class="sect2">
[]{#GUID-11885DA7-0D17-4756-B193-3CC9376B1225}

Related Documentation {#JSSEC-GUID-11885DA7-0D17-4756-B193-3CC9376B1225 .sect2}
---------------------

<div>
This document assumes you have already read the following:

-   [Java SE Platform Security
    Architecture](java-se-platform-security-architecture.htm#GUID-D6C53B30-01F9-49F1-9F61-35815558422B "This section explains what privileged code is and what it is used for. It also shows you how to use the doPrivileged API.This section describes the doPrivileged API and the use of the privileged feature.If you are using a lambda expression or anonymous inner class, then any local variables you access must be final or effectively final.If the action performed in your run method could throw a checked exception (one that must be listed in the throws clause of a method), then you need to use the PrivilegedExceptionAction interface instead of the PrivilegedAction interface.The typical use case of the doPrivileged method is to enable the method that invokes it to perform one or more actions that require permission checks without requiring the callers of the current method to have all the necessary permissions.When coding the current method, you want to temporarily extend the permission of the calling method to perform an action.Marking code as privileged enables a piece of trusted code to temporarily enable access to more resources than are available directly to the code that called it.The doPrivileged method can be invoked reflectively using the java.lang.reflect.Method.invoke method.")
-   [Java SE Security
    Tutorial](https://docs.oracle.com/javase/tutorial/security/index.html)

A supplement to this guide is the [JAAS LoginModule Developer\'s
Guide](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A),
intended for experienced programmers who require the ability to write a
[`LoginModule`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html)
implementing an authentication technology.

The following <span class="bold">tutorials</span> for JAAS
authentication and authorization can be run by everyone:

-   [JAAS Authentication
    Tutorial](jaas-authentication-tutorial.htm#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
-   [JAAS Authorization
    Tutorial](jaas-authorization-tutorial.htm#GUID-D43CF965-8A5F-4A23-A2AF-F41DD5F8B411)

Similar tutorials for JAAS authentication and authorization, but which
demonstrate the use of a Kerberos LoginModule and thus which require a
Kerberos installation, can be found at

-   [JAAS
    Authentication](jaas-authentication.htm#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
-   [JAAS
    Authorization](jaas-authorization.htm#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F)

These two tutorials are a part of [Introduction to JAAS and Java GSS-API
Tutorials](introduction-jaas-and-java-gss-api-tutorials1.htm) that
utilize Kerberos as the underlying technology for authentication and
secure communication.

</div>
</div>
<div class="sect2">
[]{#GUID-D679A98F-C706-4FE2-9027-39A520BA0FCB}

Core Classes and Interfaces {#JSSEC-GUID-D679A98F-C706-4FE2-9027-39A520BA0FCB .sect2}
---------------------------

<div>
The JAAS-related core classes and interfaces can be broken into three
categories: Common, Authentication, and Authorization.

</div>
<div class="sect3">
[]{#GUID-2CDC988F-D462-4CEA-9243-CC74B000327F}

### Common Classes {#JSSEC-GUID-2CDC988F-D462-4CEA-9243-CC74B000327F .sect3}

<div>
Common classes are those shared by both the JAAS authentication and
authorization components.

The key JAAS class is
[`javax.security.auth.Subject`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Subject.html),
which represents a grouping of related information for a single entity
such as a person. It encompasses the entity\'s
[Principals](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-8FAF9739-CD62-4A47-9582-884DBF3081F0),
public credentials, and private credentials.

Note that the `java.security.Principal`{.codeph} interface is used to
represent a Principal. Also note that a credential, as defined by JAAS,
may be any Object.

</div>
<div class="sect4">
[]{#GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3}

#### Subject {#JSSEC-GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3 .sect4}

<div>
To authorize access to resources, applications first need to
authenticate the source of the request. The JAAS framework defines the
term <span class="italic">subject</span> to represent the source of a
request. A subject may be any entity, such as a person or a service.
Once the subject is authenticated, a
[`javax.security.auth.Subject`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Subject.html)
is populated with associated identities, or
[Principals](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-8FAF9739-CD62-4A47-9582-884DBF3081F0).
A `Subject`{.codeph} may have many `Principal`{.codeph}s. For example, a
person may have a name `Principal`{.codeph} (\"John Doe\") and a SSN
`Principal`{.codeph} (\"123-45-6789\"), which distinguish it from other
subjects.

A `Subject`{.codeph} may also own security-related attributes, which are
referred to as <span class="variable">credentials</span>; see the
section
[Credentials](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-9381520E-7A13-4087-BA26-C6CB8BE4A437).
Sensitive credentials that require special protection, such as private
cryptographic keys, are stored within a private credential
`Set`{.codeph}. Credentials intended to be shared, such as public key
certificates, are stored within a public credential `Set`{.codeph}.
Different permissions (described below) are required to access and
modify the different credential `Set`{.codeph}s.

Subjects are created using these constructors:

``` {.oac_no_warn dir="ltr"}
    public Subject();

    public Subject(boolean readOnly, Set principals,
                   Set pubCredentials, Set privCredentials);
```

The first constructor creates a `Subject`{.codeph} with empty (non-null)
`Set`{.codeph}s of `Principal`{.codeph}s and credentials. The second
constructor creates a `Subject`{.codeph} with the specified
`Set`{.codeph}s of `Principal`{.codeph}s and credentials. It also has a
boolean argument which can be used to make the `Subject`{.codeph}
read-only. In a read-only `Subject`{.codeph}, the `Principal`{.codeph}
and credential `Set`{.codeph}s are immutable.

An application writer does not have to instantiate a `Subject`{.codeph}.
If the application instantiates a `LoginContext`{.codeph} and does not
pass a `Subject`{.codeph} to the `LoginContext`{.codeph} constructor,
the `LoginContext`{.codeph} instantiates a new empty `Subject`{.codeph}.
See the
[LoginContext](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-164692CF-6790-488C-BF86-39F7C5CF0F5A)
section.

If a `Subject`{.codeph} was not instantiated to be in a read-only state,
it can be set read-only by calling the following method:

``` {.oac_no_warn dir="ltr"}
    public void setReadOnly();
```

A `javax.security.auth.AuthPermission`{.codeph} with target
\"setReadOnly\" is required to invoke this method. Once in a read-only
state, any attempt to add or remove `Principal`{.codeph}s or credentials
will result in an `IllegalStateException`{.codeph} being thrown. The
following method may be called to test a `Subject`{.codeph}\'s read-only
state:

``` {.oac_no_warn dir="ltr"}
    public boolean isReadOnly();
```

To retrieve the `Principal`{.codeph}s associated with a Subject, two
methods are available:

``` {.oac_no_warn dir="ltr"}
    public Set getPrincipals();
    public Set getPrincipals(Class c);
```

The first method returns all `Principal`{.codeph}s contained in the
`Subject`{.codeph}, while the second method only returns those
`Principal`{.codeph}s that are an instance of the specified Class
`c`{.codeph}, or an instance of a subclass of Class `c`{.codeph}. An
empty set will be returned if the `Subject`{.codeph} does not have any
associated `Principal`{.codeph}s.

To retrieve the public credentials associated with a `Subject`{.codeph},
these methods are available:

``` {.oac_no_warn dir="ltr"}
    public Set getPublicCredentials();
    public Set getPublicCredentials(Class c);
```

The behavior of these methods is similar to that for the
`getPrincipals`{.codeph} methods, except in this case the public
credentials are being obtained.

To access private credentials associated with a `Subject`{.codeph}, the
following methods are available:

``` {.oac_no_warn dir="ltr"}
    public Set getPrivateCredentials();
    public Set getPrivateCredentials(Class c);
```

The behavior of these methods is similar to that for the
`getPrincipals`{.codeph} and `getPublicCredentials`{.codeph} methods.

To modify or operate upon a `Subject`{.codeph}\'s
`Principal`{.codeph}`Set`{.codeph}, public credential `Set`{.codeph}, or
private credential `Set`{.codeph}, callers use the methods defined in
the
[`java.util.Set`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/util/Set.html)
class. The following example demonstrates this:

``` {.oac_no_warn dir="ltr"}
    Subject subject;
    Principal principal;
    Object credential;

    . . .

    // add a Principal and credential to the Subject
    subject.getPrincipals().add(principal);
    subject.getPublicCredentials().add(credential);
```

Note: An `AuthPermission`{.codeph} with target \"modifyPrincipals\",
\"modifyPublicCredentials\", or \"modifyPrivateCredentials\" is required
to modify the respective `Set`{.codeph}s. Also note that only the sets
returned via the `getPrincipals()`{.codeph},
`getPublicCredentials()`{.codeph}, and
`getPrivateCredentials()`{.codeph} methods with no arguments are backed
by the `Subject`{.codeph}\'s respective internal sets. Therefore any
modification to the returned set affects the internal sets as well. The
sets returned via the `getPrincipals(Class c)`{.codeph},
`getPublicCredentials(Class c)`{.codeph}, and
`getPrivateCredentials(Class c)`{.codeph} methods are not backed by the
`Subject`{.codeph}\'s respective internal sets. A new set is created and
returned for each such method invocation. Modifications to these sets
will not affect the `Subject`{.codeph}\'s internal sets.

In order to iterate through a Set of private credentials, you need a
`javax.security.auth.PrivateCredentialPermission`{.codeph} to access
each credential. See the
[`PrivateCredentialPermission`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/PrivateCredentialPermission.html)
API documentation for further information.

A `Subject`{.codeph} may be associated with an
`AccessControlContext`{.codeph} (see the `doAs`{.codeph} and
`doAsPrivileged`{.codeph} method descriptions below). The following
method returns the `Subject`{.codeph} associated with the specified
`AccessControlContext`{.codeph}, or `null`{.codeph} if no
`Subject`{.codeph} is associated with the specified
`AccessControlContext`{.codeph}.

``` {.oac_no_warn dir="ltr"}
    public static Subject getSubject(final AccessControlContext acc);
```

An `AuthPermission`{.codeph} with target \"getSubject\" is required to
call `Subject.getSubject`{.codeph}.

The `Subject`{.codeph} class also includes the following methods
inherited from `java.lang.Object`{.codeph}.

``` {.oac_no_warn dir="ltr"}
    public boolean equals(Object o);
    public String toString();
    public int hashCode();
```

</div>
<div class="sect5">
[]{#GUID-FA47090A-D270-4E4E-A5F6-752E1A48DC4C}

##### The doAs methods for performing an action as a particular Subject {#JSSEC-GUID-FA47090A-D270-4E4E-A5F6-752E1A48DC4C .sect5}

<div>
The following static methods may be called to perform an action as a
particular `Subject`{.codeph}:

``` {.oac_no_warn dir="ltr"}
    public static Object
        doAs(final Subject subject,
             final java.security.PrivilegedAction action);

    public static Object
        doAs(final Subject subject,
             final java.security.PrivilegedExceptionAction action)
             throws java.security.PrivilegedActionException;
```

Both methods first associate the specified `subject`{.codeph} with the
current Thread\'s `AccessControlContext`{.codeph}, and then execute the
`action`{.codeph}. This achieves the effect of having the
`action`{.codeph} run as the `subject`{.codeph}. The first method can
throw runtime exceptions but normal execution has it returning an Object
from the `run`{.codeph} method of its `action`{.codeph} argument. The
second method behaves similarly except that it can throw a checked
exception from its `PrivilegedExceptionAction run`{.codeph} method. An
`AuthPermission`{.codeph} with target \"doAs\" is required to call the
`doAs`{.codeph} methods.

</div>
</div>
<div class="sect5">
[]{#GUID-3BF4EEC2-3953-4331-955B-C34EF2514F36}

##### Subject.doAs Example {#JSSEC-GUID-3BF4EEC2-3953-4331-955B-C34EF2514F36 .sect5}

<div>
Here is an example utilizing the first `doAs`{.codeph} method. Assume
that someone named \"Bob\" has been authenticated by a
`LoginContext`{.codeph} (see the
[LoginContext](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-164692CF-6790-488C-BF86-39F7C5CF0F5A))
and as a result a `Subject`{.codeph} was populated with a
`Principal`{.codeph} of class `com.ibm.security.Principal`{.codeph}, and
that `Principal`{.codeph} has the name \"BOB\". Also assume that a
<span class="apiname">SecurityManager</span> has been installed, and
that the following exists in the access control policy (see
[Policy](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-66990EE6-1213-4BF7-AC43-A4C75AE6746D)
for more details on the policy file).

``` {.oac_no_warn dir="ltr"}
    // grant "BOB" permission to read the file "foo.txt"
    grant Principal com.ibm.security.Principal "BOB" {
        permission java.io.FilePermission "foo.txt", "read";
    };
```

Here is the sample application code:

``` {.oac_no_warn dir="ltr"}
    class ExampleAction implements java.security.PrivilegedAction {
        public Object run() {
            java.io.File f = new java.io.File("foo.txt");

            // the following call invokes a security check
            if (f.exists()) {
                System.out.println("File foo.txt exists");
            }
            return null;
        }
    }

    public class Example1 {
        public static void main(String[] args) {

            // Authenticate the subject, "BOB".
            // This process is described in the
            // LoginContext class.

            Subject bob;
            // Set bob to the Subject created during the
            // authentication process

            // perform "ExampleAction" as "BOB"
            Subject.doAs(bob, new ExampleAction());
        }
    }
```

During execution, `ExampleAction`{.codeph} will encounter a security
check when it makes a call to `f.exists()`{.codeph}. However, since
`ExampleAction`{.codeph} is running as \"BOB\", and the policy (above)
grants the necessary `FilePermission`{.codeph} to \"BOB\", the
`ExampleAction`{.codeph} will pass the security check. If the
`grant`{.codeph} statement in the policy is altered (adding an incorrect
`CodeBase`{.codeph} or changing the `Principal`{.codeph} to \"MOE\", for
example), then a `SecurityException`{.codeph} will be thrown.

</div>
</div>
<div class="sect5">
[]{#GUID-7CBADEEE-D62F-4AA7-BD75-78F79C72067A}

##### The doAsPrivileged methods {#JSSEC-GUID-7CBADEEE-D62F-4AA7-BD75-78F79C72067A .sect5}

<div>
The following methods also perform an action as a particular
`Subject`{.codeph}.

``` {.oac_no_warn dir="ltr"}
    public static Object doAsPrivileged(
        final Subject subject,
        final java.security.PrivilegedAction action,
        final java.security.AccessControlContext acc);

    public static Object doAsPrivileged(
        final Subject subject,
        final java.security.PrivilegedExceptionAction action,
        final java.security.AccessControlContext acc)
        throws java.security.PrivilegedActionException;
```

An `AuthPermission`{.codeph} with target \"doAsPrivileged\" is required
to call the `doAsPrivileged`{.codeph} methods.

</div>
</div>
<div class="sect5">
[]{#GUID-97198A0C-B488-4D24-A242-CAFA8F70DFA5}

##### doAs versus doAsPrivileged {#JSSEC-GUID-97198A0C-B488-4D24-A242-CAFA8F70DFA5 .sect5}

<div>
The `doAsPrivileged`{.codeph} methods behave exactly the same as the
`doAs`{.codeph} methods, except that instead of associating the provided
`Subject`{.codeph} with the current Thread\'s
`AccessControlContext`{.codeph}, they use the provided
`AccessControlContext`{.codeph}. In this way, actions can be restricted
by `AccessControlContext`{.codeph}s different from the current one.

An `AccessControlContext`{.codeph} contains information about all the
code executed since the `AccessControlContext`{.codeph} was
instantiated, including the code location and the permissions the code
is granted by the policy. In order for an access control check to
succeed, the policy must grant each code item referenced by the
`AccessControlContext`{.codeph} the required permissions.

If the `AccessControlContext`{.codeph} provided to
`doAsPrivileged`{.codeph} is `null`{.codeph}, then the action is not
restricted by a separate `AccessControlContext`{.codeph}. One example
where this may be useful is in a server environment. A server may
authenticate multiple incoming requests and perform a separate
`doAs`{.codeph} operation for each request. To start each
`doAs`{.codeph} action \"fresh,\" and without the restrictions of the
current server `AccessControlContext`{.codeph}, the server can call
`doAsPrivileged`{.codeph} and pass in a
`null`{.codeph}`AccessControlContext`{.codeph}.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-8FAF9739-CD62-4A47-9582-884DBF3081F0}

#### Principals {#JSSEC-GUID-8FAF9739-CD62-4A47-9582-884DBF3081F0 .sect4}

<div>
As mentioned previously, once a <span class="apiname">Subject</span> is
authenticated, it is populated with associated identities, or
<span class="apiname">Principal</span>s. A
<span class="apiname">Subject</span> may have many
<span class="apiname">Principals</span>. For example, a person may have
a name <span class="apiname">Principal</span> (\"John Doe\") and an SSN
<span class="apiname">Principal</span> (\"123-45-6789\"), which
distinguish it from other <span class="apiname">Subject</span>s. A
<span class="apiname">Principal</span> must implement the
[<span class="apiname">java.security.Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
and
[<span class="apiname">java.io.Serializable</span>](https://docs.oracle.com/javase/10/docs/api/java/io/Serializable.html)
interfaces. See
[Subject](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3)
for information about ways to update the
<span class="apiname">Principal</span>s associated with a
<span class="apiname">Subject</span>.

</div>
</div>
<div class="sect4">
[]{#GUID-9381520E-7A13-4087-BA26-C6CB8BE4A437}

#### Credentials {#JSSEC-GUID-9381520E-7A13-4087-BA26-C6CB8BE4A437 .sect4}

<div>
In addition to associated Principals, a Subject may own security-related
attributes, which are referred to as credentials. A credential may
contain information used to authenticate the subject to new services.
Such credentials include passwords, Kerberos tickets, and public key
certificates. Credentials might also contain data that simply enables
the subject to perform certain activities. Cryptographic keys, for
example, represent credentials that enable the subject to sign or
encrypt data. Public and private credential classes are not part of the
core JAAS class library. Any class, therefore, can represent a
credential.

Public and private credential classes are not part of the core JAAS
class library. Developers, however, may elect to have their credential
classes implement two interfaces related to credentials:
`Refreshable`{.codeph} and `Destroyable`{.codeph}.

</div>
<div class="sect5">
[]{#GUID-9FA5AFF7-92A9-4F26-9266-71B8871C3A86}

##### Refreshable {#JSSEC-GUID-9FA5AFF7-92A9-4F26-9266-71B8871C3A86 .sect5}

<div>
The
[`javax.security.auth.Refreshable`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Refreshable.html)
<span class="bold">interface</span> provides the capability for a
credential to refresh itself. For example, a credential with a
particular time-restricted lifespan may implement this interface to
allow callers to refresh the time period for which it is valid. The
interface has two abstract methods:

``` {.oac_no_warn dir="ltr"}
    boolean isCurrent();
```

This method determines whether the credential is current or valid.

``` {.oac_no_warn dir="ltr"}
    void refresh() throws RefreshFailedException;
```

This method updates or extends the validity of the credential. The
method implementation should perform an

`AuthPermission("refreshCredential")`{.codeph}

security check to ensure the caller has permission to refresh the
credential.

</div>
</div>
<div class="sect5">
[]{#GUID-B5587785-F349-46FA-8D8C-AB7EA09AC98C}

##### Destroyable {#JSSEC-GUID-B5587785-F349-46FA-8D8C-AB7EA09AC98C .sect5}

<div>
The
[`javax.security.auth.Destroyable`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Destroyable.html)
<span class="bold">interface</span> provides the capability of
destroying the contents within a credential. The interface has two
abstract methods:

``` {.oac_no_warn dir="ltr"}
    boolean isDestroyed();
```

Determines whether the credential has been destroyed.

``` {.oac_no_warn dir="ltr"}
    void destroy() throws DestroyFailedException;
```

Destroys and clears the information associated with this credential.
Subsequent calls to certain methods on this credential will result in an
`IllegalStateException`{.codeph} being thrown. The method implementation
should perform an `AuthPermission("destroyCredential")`{.codeph}
security check to ensure the caller has permission to destroy the
credential.

</div>
</div>
</div>
</div>
<div class="sect3">
[]{#GUID-6A19B0FB-39F9-4917-A3B1-72E4387BA021}

### Authentication Classes and Interfaces {#JSSEC-GUID-6A19B0FB-39F9-4917-A3B1-72E4387BA021 .sect3}

<div>
Authentication represents the process by which the identity of a subject
is verified, and must be performed in a secure fashion; otherwise a
perpetrator may impersonate others to gain access to a system.
Authentication typically involves the subject demonstrating some form of
evidence to prove its identity. Such evidence may be information only
the subject would likely know or have (such as a password or
fingerprint), or it may be information only the subject could produce
(such as signed data using a private key).

To authenticate a subject (user or service), the following steps are
performed:

1.  An application instantiates a `LoginContext`{.codeph}.
2.  The `LoginContext`{.codeph} consults a
    [`Configuration`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
    to load all of the `LoginModule`{.codeph}s configured for that
    application.
3.  The application invokes the `LoginContext`{.codeph}\'s
    `login`{.codeph} method.
4.  The `login`{.codeph} method invokes all of the loaded
    `LoginModule`{.codeph}s. Each `LoginModule`{.codeph} attempts to
    authenticate the subject. Upon success, `LoginModule`{.codeph}s
    associate relevant `Principal`{.codeph}s and credentials with a
    `Subject`{.codeph} object that represents the subject being
    authenticated.
5.  The `LoginContext`{.codeph} returns the authentication status to the
    application.
6.  If authentication succeeded, the application retrieves the
    `Subject`{.codeph} from the `LoginContext`{.codeph}.

The authentication classes are described below.

</div>
<div class="sect4">
[]{#GUID-164692CF-6790-488C-BF86-39F7C5CF0F5A}

#### LoginContext {#JSSEC-GUID-164692CF-6790-488C-BF86-39F7C5CF0F5A .sect4}

<div>
The
[`javax.security.auth.login.LoginContext`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/LoginContext.html)
class provides the basic methods used to authenticate subjects, and
provides a way to develop an application independent of the underlying
authentication technology. The `LoginContext`{.codeph} consults a
[`Configuration`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
to determine the authentication services, or
[`LoginModule`{.codeph}(s)](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html),
configured for a particular application. Therefore, different
`LoginModule`{.codeph}s can be plugged in under an application without
requiring any modifications to the application itself.

`LoginContext`{.codeph} offers four constructors from which to choose:

``` {.oac_no_warn dir="ltr"}
    public LoginContext(String name) throws LoginException;

    public LoginContext(String name, Subject subject) throws LoginException;

    public LoginContext(String name, CallbackHandler callbackHandler)
           throws LoginException

    public LoginContext(String name, Subject subject,
           CallbackHandler callbackHandler) throws LoginException
```

All of the constructors share a common parameter: name. This argument is
used by the `LoginContext`{.codeph} as an index into the login
`Configuration`{.codeph} to determine which `LoginModule`{.codeph}s are
configured for the application instantiating the
`LoginContext`{.codeph}. Constructors that do not take a Subject as an
input parameter instantiate a new `Subject`{.codeph}. Null inputs are
disallowed for all constructors. Callers require an
`AuthPermission`{.codeph} with target
\"createLoginContext.<span class="variable">\<name\></span>\" to
instantiate a `LoginContext`{.codeph}. Here,
<span class="variable">\<name\></span> refers to the name of the login
configuration entry that the application references in the name
parameter for the `LoginContext`{.codeph} instantiation.

See
[CallbackHandler](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-1018AB86-8912-4C00-8717-2FA2B54A4866)
for information on what a `CallbackHandler`{.codeph} is and when you may
need one.

Actual authentication occurs with a call to the following method:

``` {.oac_no_warn dir="ltr"}
    public void login() throws LoginException;
```

When `login`{.codeph} is invoked, all of the configured
`LoginModule`{.codeph}s are invoked to perform the authentication. If
the authentication succeeded, the `Subject`{.codeph} (which may now hold
`Principal`{.codeph}s, public credentials, and private credentials) can
be retrieved by using the following method:

``` {.oac_no_warn dir="ltr"}
     public Subject getSubject();
```

To logout a `Subject`{.codeph} and remove its authenticated
`Principals`{.codeph} and credentials, the following method is provided:

``` {.oac_no_warn dir="ltr"}
    public void logout() throws LoginException;
```

The following code sample demonstrates the calls necessary to
authenticate and logout a Subject:

``` {.oac_no_warn dir="ltr"}
    // let the LoginContext instantiate a new Subject
    LoginContext lc = new LoginContext("entryFoo");
    try {
        // authenticate the Subject
        lc.login();
        System.out.println("authentication successful");

        // get the authenticated Subject
        Subject subject = lc.getSubject();

        ...

        // all finished -- logout
        lc.logout();
    } catch (LoginException le) {
        System.err.println("authentication unsuccessful: " +
            le.getMessage());
    }
```

</div>
</div>
<div class="sect4">
[]{#GUID-0FDBE77C-01C3-4A98-9925-4F8D2E260118}

#### LoginModule {#JSSEC-GUID-0FDBE77C-01C3-4A98-9925-4F8D2E260118 .sect4}

<div>
The
[`LoginModule`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html)
<span class="bold">interface</span> gives developers the ability to
implement different kinds of authentication technologies that can be
plugged in under an application. For example, one type of
`LoginModule`{.codeph} may perform a user name/password-based form of
authentication. Other `LoginModule`{.codeph}s may interface to hardware
devices such as smart cards or biometric devices.

Note: If you are an application writer, you do not need to understand
the workings of `LoginModule`{.codeph}s. All you have to know is how to
write your application and specify configuration information (such as in
a login configuration file) such that the application will be able to
utilize the LoginModule specified by the configuration to authenticate
the user.

If, on the other hand, you are a programmer who wishes to write a
LoginModule implementing an authentication technology, see the [Java
Authentication and Authorization Service (JAAS): LoginModule
Developer\'s
Guide](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A)
for detailed step-by-step instructions.

</div>
</div>
<div class="sect4">
[]{#GUID-1018AB86-8912-4C00-8717-2FA2B54A4866}

#### CallbackHandler {#JSSEC-GUID-1018AB86-8912-4C00-8717-2FA2B54A4866 .sect4}

<div>
In some cases a `LoginModule`{.codeph} must communicate with the user to
obtain authentication information. `LoginModule`{.codeph}s use a
[<span class="apiname">javax.security.auth.callback.CallbackHandler</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/CallbackHandler.html)
for this purpose. Applications implement the `CallbackHandler`{.codeph}
<span class="bold">interface</span> and pass it to the
`LoginContext`{.codeph}, which forwards it directly to the underlying
`LoginModule`{.codeph}s. A `LoginModule`{.codeph} uses the
`CallbackHandler`{.codeph} both to gather input from users (such as a
password or smart card pin number) or to supply information to users
(such as status information). By allowing the application to specify the
`CallbackHandler`{.codeph}, underlying `LoginModules`{.codeph} can
remain independent of the different ways applications interact with
users. For example, the implementation of a `CallbackHandler`{.codeph}
for a GUI application might display a window to solicit input from a
user. On the other hand, the implementation of a
`CallbackHandler`{.codeph} for a non-GUI tool might simply prompt the
user for input directly from the command line.

`CallbackHandler`{.codeph}

is an interface with one method to implement:

``` {.oac_no_warn dir="ltr"}
     void handle(Callback[] callbacks)
         throws java.io.IOException, UnsupportedCallbackException;
```

The `LoginModule`{.codeph} passes the `CallbackHandler handle`{.codeph}
method an array of appropriate `Callback`{.codeph}s, for example a
[<span class="apiname">NameCallback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/NameCallback.html)
for the user name and a
[<span class="apiname">PasswordCallback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/PasswordCallback.html)
for the password, and the `CallbackHandler`{.codeph} performs the
requested user interaction and sets appropriate values in the
`Callback`{.codeph}s. For example, to process a `NameCallback`{.codeph},
the `CallbackHandler`{.codeph} may prompt for a name, retrieve the value
from the user, and call the `NameCallback`{.codeph}\'s
`setName`{.codeph} method to store the name.

The
[`CallbackHandler`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/CallbackHandler.html)
documentation has a lengthy example not included in this document that
readers may want to examine.

</div>
</div>
<div class="sect4">
[]{#GUID-A6E64966-EDDC-4519-9E42-1114E5E3DEFC}

#### Callback {#JSSEC-GUID-A6E64966-EDDC-4519-9E42-1114E5E3DEFC .sect4}

<div>
The
[`javax.security.auth.callback`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/package-summary.html)
package contains the Callback <span class="bold">interface</span> as
well as several implementations. LoginModules may pass an array of
Callbacks directly to the handle method of a
[CallbackHandler](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-1018AB86-8912-4C00-8717-2FA2B54A4866).

Please consult the various Callback APIs for more information on their
use.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-B8891FFA-ACD2-4E42-9488-0551B28F31C8}

### Authorization Classes {#JSSEC-GUID-B8891FFA-ACD2-4E42-9488-0551B28F31C8 .sect3}

<div>
To make JAAS authorization take place, granting access control
permissions based not just on what code is running but also on who is
running it, the following is required:

-   The user must be authenticated, as described in the
    [LoginContext](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-164692CF-6790-488C-BF86-39F7C5CF0F5A)
    section.
-   The Subject that is the result of authentication must be associated
    with an access control context, as described in the
    [Subject](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3)
    section.
-   Principal-based entries must be configured in the security policy,
    as described below.

The `Policy`{.codeph} abstract class and the authorization-specific
classes `AuthPermission`{.codeph} and
`PrivateCredentialPermission`{.codeph} are described below.

</div>
<div class="sect4">
[]{#GUID-66990EE6-1213-4BF7-AC43-A4C75AE6746D}

#### Policy {#JSSEC-GUID-66990EE6-1213-4BF7-AC43-A4C75AE6746D .sect4}

<div>
The
[`java.security.Policy`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Policy.html)
class is an <span class="bold">abstract</span> class for representing
the system-wide access control policy. The `Policy`{.codeph} API
supports
[`Principal`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)-based
queries.

As a default, the JDK provides a file-based subclass implementation,
which was upgraded to support `Principal`{.codeph}-based
`grant`{.codeph} entries in policy files.

Policy files and the structure of entries within them are described in
[Default Policy Implementation and Policy File
Syntax](permissions-jdk1.htm#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D).

</div>
</div>
<div class="sect4">
[]{#GUID-B7D676A5-E9E6-4FDA-B0F3-8A51B3747138}

#### AuthPermission {#JSSEC-GUID-B7D676A5-E9E6-4FDA-B0F3-8A51B3747138 .sect4}

<div>
The
[`javax.security.auth.AuthPermission`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/AuthPermission.html)
class encapsulates the basic permissions required for JAAS. An
`AuthPermission`{.codeph} contains a name (also referred to as a
\"target name\") but no actions list; you either have the named
permission or you don\'t.

In addition to its inherited methods (from the
[`java.security.Permission`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Permission.html)
class), an `AuthPermission`{.codeph} has two public constructors:

``` {.oac_no_warn dir="ltr"}
    public AuthPermission(String name);
    public AuthPermission(String name, String actions);
```

The first constructor creates a new `AuthPermission`{.codeph} with the
specified name. The second constructor also creates a new
`AuthPermission`{.codeph} object with the specified name, but has an
additional actions argument which is currently unused and should be
null. This constructor exists solely for the `Policy`{.codeph} object to
instantiate new `Permission`{.codeph} objects. For most other code, the
first constructor is appropriate.

Currently the `AuthPermission`{.codeph} object is used to guard access
to the `Policy`{.codeph}, `Subject`{.codeph}, `LoginContext`{.codeph},
and `Configuration`{.codeph} objects. Refer to the
[`AuthPermission`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/AuthPermission.html)
Javadoc API documentation for the list of valid names that are
supported.

</div>
</div>
<div class="sect4">
[]{#GUID-D7D015EE-54C6-4D85-83C2-05742314847D}

#### PrivateCredentialPermission {#JSSEC-GUID-D7D015EE-54C6-4D85-83C2-05742314847D .sect4}

<div>
The
[`javax.security.auth.PrivateCredentialPermission`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/PrivateCredentialPermission.html)
class protects access to a `Subject`{.codeph}\'s private credentials and
provides one public constructor:

``` {.oac_no_warn dir="ltr"}
     public PrivateCredentialPermission(String name, String actions);
```

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-7B9C6511-A221-414A-8A4B-6BCF08172065}

JAAS Tutorials and Sample Programs {#JSSEC-GUID-7B9C6511-A221-414A-8A4B-6BCF08172065 .sect2}
----------------------------------

<div>
The [JAAS
Authentication](jaas-authentication-tutorial.htm#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
and [JAAS
Authorization](jaas-authorization-tutorial.htm#GUID-D43CF965-8A5F-4A23-A2AF-F41DD5F8B411)
tutorials contain the following samples:

-   [`SampleAcn.java`](jaas-authentication-tutorial.htm#GUID-E007D5F4-3FA5-417A-B85F-E669839F0101__GUID-1270A0AC-EA51-4A47-B9BC-BDB42F96F5FE)
    is a sample application demonstrating JAAS authentication.
-   [`SampleAzn.java`](jaas-authorization-tutorial.htm#GUID-07EAB926-63EA-48F4-8DF0-4CC4526FA545__GUID-9AE66C05-0850-4AAF-8DD9-7D940069844F)
    is a sample application used by the authorization tutorial. It
    demonstrates both authentication and authorization.
-   [The Login Configuration File for the JAAS Authentication
    Tutorial](jaas-authentication-tutorial.htm#GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F)
    describes `sample_jaas.config`, which is a sample login
    configuration file used by both tutorials.
-   [`sampleacn.policy`](jaas-authentication-tutorial.htm#GUID-44F2BF3A-F51D-4F21-8F40-96CB1120396D__SAMPLEACN.POLICY-2FEDE143)
    is a sample policy file granting permissions required by the code
    for the authentication tutorial.
-   [`sampleazn.policy`](jaas-authorization-tutorial.htm#GUID-3A2FF6CF-3124-4402-B550-D0F4E76B3D4D__GUID-6CA8F774-5E38-437D-8549-9604DEC5C317)
    is a sample policy file granting permissions required by the code
    for the authorization tutorial.
-   [`SampleLoginModule.java`](jaas-authentication-tutorial.htm#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-F9A208EC-3247-4320-8158-82B0E84C6A04)
    is the class specified by the tutorials\' login configuration file
    (`sample_jaas.config`{.codeph}) as the class implementing the
    desired underlying authentication.
    <span class="apiname">SampleLoginModule</span>\'s user
    authentication consists of simply verifying that the name and
    password specified by the user have specific values.
-   [`SamplePrincipal.java`](jaas-authentication-tutorial.htm#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-3EA5533B-1284-481E-A35F-C82B17837F2E)
    is a sample class implementing the
    [`Principal`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
    interface. It is used by
    <span class="apiname">SampleLoginModule</span>.

See the tutorials for detailed information about the applications, the
policy files, and the login configuration file.

Application writers do not need to understand the code for
`SampleLoginModule.java` or `SamplePrincipal.java`, as explained in the
tutorials. Programmers who wish to write LoginModules can learn how to
do so by reading the [Java Authentication and Authorization Service
(JAAS): LoginModule Developer\'s
Guide](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A).

</div>
</div>
<div class="sect2">
[]{#GUID-106F4B32-B9A3-4B75-BDBF-29B252BB3F53}

Appendix A: JAAS Settings in the java.security Security Properties File {#JSSEC-GUID-106F4B32-B9A3-4B75-BDBF-29B252BB3F53 .sect2}
-----------------------------------------------------------------------

<div>
A number of JAAS-related settings can be configured in the
`java.security`{.codeph} master Security Properties file, which is
located in the `conf/security` directory of the JDK.

JAAS adds two new security properties to `java.security`{.codeph}:

-   `login.configuration.provider`{.codeph}
-   `login.config.url.n`{.codeph}

The following pre-existing properties are also relevant for JAAS users:

-   `policy.provider`{.codeph}
-   `policy.url.n`{.codeph}

The following example demonstrates how to configure these properties. In
this example, we leave the values provided in the default
`java.security`{.codeph} file for the `policy.provider`{.codeph},
`policy.url.n`{.codeph}, and `login.configuration.provider`{.codeph}
Security Properties. The default `java.security`{.codeph} file also
lists a value for the `login.config.url.n`{.codeph} Security Property,
but it is commented out. In the example below, it is not commented.

``` {.oac_no_warn dir="ltr"}
...

#
# Class to instantiate as the javax.security.auth.login.Configuration
# provider.
#
login.configuration.provider=sun.security.provider.ConfigFile

#
# Default login configuration file
#
#login.config.url.1=file:${user.home}/.java.login.config

#
# Class to instantiate as the system Policy. This is the name of the class
# that will be used as the Policy object. The system class loader is used to
# locate this class.
#
policy.provider=sun.security.provider.PolicyFile

# The default is to have a single system-wide policy file,
# and a policy file in the user's home directory.
#
policy.url.1=file:${java.home}/conf/security/java.policy
policy.url.2=file:${user.home}/.java.policy

...
```

Note: Modifications made to this file may be overwritten by subsequent
JDK updates. However, an alternate `java.security`{.codeph} properties
file may be specified from the command line via the system property
`java.security.properties=<URL>`{.codeph}. This properties file appends
to the system properties file. If both properties files specify values
for the same key, the value from command-line properties file is
selected, as it is the last one loaded.

Also, specifying `java.security.properties==<URL>`{.codeph} (using two
equals signs), then that properties file will completely override the
system properties file.

To disable the ability to specify an additional properties file from the
command line, set the key `security.overridePropertiesFile`{.codeph} to
`false`{.codeph} in the system properties file. It is set to
`true`{.codeph} by default.

</div>
<div class="sect3">
[]{#GUID-75C5BF67-1530-4383-8A0D-6C2C6B378096}

### Login Configuration Provider {#JSSEC-GUID-75C5BF67-1530-4383-8A0D-6C2C6B378096 .sect3}

<div>
The default JAAS login configuration implementation provided by Oracle
gets its configuration information from files and expects the
information to be provided in a specific format shown in the tutorials.

The default JAAS login configuration implementation can be replaced by
specifying the alternative provider class implementation in the
`login.configuration.provider`{.codeph} property.

For example:

``` {.oac_no_warn dir="ltr"}
    login.configuration.provider=com.foo.Config
```

If the Security property `login.configuration.provider`{.codeph} is not
found, or is left unspecified, then it is set to the default value:

``` {.oac_no_warn dir="ltr"}
    login.configuration.provider=com.sun.security.auth.login.ConfigFile
```

Note that there is no means to dynamically set the login configuration
provider from the command line.

</div>
</div>
<div class="sect3">
[]{#GUID-F26A634E-7D9F-41FD-822A-59A2D33E79BB}

### Login Configuration URLs {#JSSEC-GUID-F26A634E-7D9F-41FD-822A-59A2D33E79BB .sect3}

<div>
If you are using a login configuration implementation that expects the
configuration information to be specified in files (as does the default
implementation from Oracle), the location of the login configuration
file(s) can be statically set by specifying their respective URLs in the
`login.config.url.n`{.codeph} property.
\'<span class="variable">n</span>\' is a consecutively numbered integer
starting with 1. If multiple configuration files are specified (if
<span class="variable">n</span> \>= 2), they will be read and unioned
into one single configuration.

For example:

``` {.oac_no_warn dir="ltr"}
  login.config.url.1=file:C:/config/.java.login.config
  login.config.url.2=file:C:/users/foo/.foo.login.config
```

If the location of the configuration files is not set in the
`java.security`{.codeph} properties file, and also is not specified
dynamically from the command line (via the
`-Djava.security.auth.login.config`{.codeph} option), JAAS attempts to
load a default configuration from

``` {.oac_no_warn dir="ltr"}
file:${user.home}/.java.login.config
```

</div>
</div>
<div class="sect3">
[]{#GUID-6396FFE2-3877-405C-B40C-8B838A2B69D5}

### Policy Provider {#JSSEC-GUID-6396FFE2-3877-405C-B40C-8B838A2B69D5 .sect3}

<div>
The default policy implementation can be replaced by specifying the
alternative provider class implementation in the
`policy.provider`{.codeph} property.

For example:

``` {.oac_no_warn dir="ltr"}
policy.provider=com.foo.Policy
```

If the Security property `policy.provider`{.codeph} is not found, or is
left unspecified, then the `Policy`{.codeph} is set to the default
value:

``` {.oac_no_warn dir="ltr"}
policy.provider=sun.security.provider.PolicyFile
```

Note that there is no means to dynamically set the policy provider from
the command line.

</div>
</div>
<div class="sect3">
[]{#GUID-D6502328-3C68-4E79-816B-599CC503DF73}

### Policy File URLs {#JSSEC-GUID-D6502328-3C68-4E79-816B-599CC503DF73 .sect3}

<div>
The location of the access control policy files can be statically set by
specifying their respective URLs in the `auth.policy.url.n`{.codeph}
property. `n`{.codeph} is a consecutively numbered integer starting with
1. If multiple policies are specified (if `n`{.codeph} \>= 2), they will
be read and unioned into one single policy.

For example:

``` {.oac_no_warn dir="ltr"}
policy.url.1=file:C:/policy/.java.policy
policy.url.2=file:C:/users/foo/.foo.policy
```

If the location of the policy file(s) is not set in the
`java.security`{.codeph} properties file, and is not specified
dynamically from the command line (via the
`-Djava.security.policy`{.codeph} option), the access control policy
defaults to the same policy as that of the system policy file installed
with the JDK. That policy file

-   grants all permissions to standard extensions
-   allows anyone to listen on un-privileged ports
-   allows any code to read certain \"standard\" properties that are not
    security-sensitive, such as the `os.name`{.codeph} and
    `file.separator`{.codeph} properties.

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
| ---------------- --- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| ---------------- --  | L |             <span cl |
|                      | o | ass="icon">Contents< |
|       [![Previous](. | g | /span>](toc.htm)     |
| ./../dcommon/gifs/le | o |   -- --------------- |
| ftnav.gif)\          | ] | -------------------- |
|                      | ( | -------------------- |
|                [![Ne | . | ---                  |
| xt](../../dcommon/gi | . |                      |
| fs/rightnav.gif)\    | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](j | / |                      |
| ava-authentication-a | d |                      |
| nd-authorization-ser | c |                      |
| vice-jaas1.htm)   <s | o |                      |
| pan class="icon">Nex | m |                      |
| t</span>](appendix-b | m |                      |
| -jaas-login-configur | o |                      |
| ation-file.htm)      | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ---------------- --- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| ---------------- --  | a |                      |
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
