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

  ----------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------- --
               [![Previous](../../dcommon/gifs/leftnav.gif)\                                                    [![Next](../../dcommon/gifs/rightnav.gif)\                                        
   <span class="icon">Previous</span>](jaas-authentication-tutorial.htm)   <span class="icon">Next</span>](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm)  
  ----------------------------------------------------------------------- ----------------------------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-D43CF965-8A5F-4A23-A2AF-F41DD5F8B411}<!-- End Header -->

JAAS Authorization Tutorial {#JSSEC-GUID-D43CF965-8A5F-4A23-A2AF-F41DD5F8B411 .sect1}
===========================

<div>
This tutorial expands the program and policy file developed in the [JAAS
Authentication
Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
tutorial to demonstrate the JAAS authorization component, which ensures
the authenticated caller has the access control rights (permissions)
required to do subsequent security-sensitive operations. Since the
authorization component requires that the user authentication first be
completed, please read the [JAAS Authentication
Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
tutorial first if you have not already done so.

The rest of this tutorial consists of the following sections:

-   [What is JAAS
    Authorization?](jaas-authorization-tutorial.html#GUID-AA85EDBD-7866-41CF-925F-6AA329C2E161)
-   [How is JAAS Authorization
    Performed?](jaas-authorization-tutorial.html#GUID-0420D2C8-DF99-43FF-929E-D44564C64F57)
    -   [How Do You Make Principal-Based Policy File
        Statements?](jaas-authorization-tutorial.html#GUID-8BB38DE7-73AA-4560-AA28-D9CCE265AA78)
    -   [How Do You Associate a Subject with an Access Control
        Context?](jaas-authorization-tutorial.html#GUID-BB640CDE-3EA5-4980-94F8-C821B98101FA)
-   [The Authorization Tutorial
    Code](jaas-authorization-tutorial.html#GUID-C1549AAE-E32F-449C-9A05-B175A5181EF8)
-   [The Login Configuration File for the JAAS Authorization
    Tutorial](jaas-authorization-tutorial.html#GUID-247D6204-446B-4B48-B376-5CD76CAFE3E7)
-   [The Policy
    File](jaas-authorization-tutorial.html#GUID-8462E46D-FF67-4630-9A87-D24EE60D100C)
-   [Running the Authorization Tutorial
    Code](jaas-authorization-tutorial.html#GUID-04A78ED2-B68C-4C89-849D-F9BF4F17BBD1)

If you want to first see the tutorial code in action, you can skip
directly to [Running the Authorization Tutorial
Code](jaas-authorization-tutorial.html#GUID-04A78ED2-B68C-4C89-849D-F9BF4F17BBD1)
and then go back to the other sections to learn more.

</div>
<div class="sect2">
[]{#GUID-AA85EDBD-7866-41CF-925F-6AA329C2E161}

What is JAAS Authorization? {#JSSEC-GUID-AA85EDBD-7866-41CF-925F-6AA329C2E161 .sect2}
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
an example of this in the `sampleacn.policy`{.codeph} file used in the
[JAAS Authentication
Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
tutorial. That file contains the following:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./SampleAcn.jar" {

   permission javax.security.auth.AuthPermission 
                    "createLoginContext.Sample";
};
```

This grants the code in the `SampleAcn.jar`{.codeph} file, located in
the current directory, the specified permission. (No signer is
specified, so it doesn\'t matter whether the code is signed or not.)

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
a Social Security Number <span class="apiname">Principal</span>
(\"987-65-4321\"), thereby distinguishing this
<span class="apiname">Subject</span> from other
<span class="apiname">Subject</span>s.

Permissions can be granted in the policy to specific
<span class="apiname">Principal</span>s. After the user has been
authenticated, the application can associate the
<span class="apiname">Subject</span> with the current access control
context. For each subsequent security-checked operation (a local file
access, for example), the Java runtime will automatically determine
whether the policy grants the required permission only to a specific
<span class="apiname">Principal</span> and if so, the operation will be
allowed only if the <span class="apiname">Subject</span> associated with
the access control context contains the designated
<span class="apiname">Principal</span>.

</div>
</div>
<div class="sect2">
[]{#GUID-0420D2C8-DF99-43FF-929E-D44564C64F57}

How is JAAS Authorization Performed? {#JSSEC-GUID-0420D2C8-DF99-43FF-929E-D44564C64F57 .sect2}
------------------------------------

<div>
To make JAAS authorization take place, the following is required:

-   The user must be authenticated, as described in the [JAAS
    Authentication
    Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
    tutorial.
-   <span class="apiname">Principal</span>-based entries must be
    configured in the security policy; see [How Do You Make
    Principal-Based Policy File
    Statements?](jaas-authorization-tutorial.html#GUID-8BB38DE7-73AA-4560-AA28-D9CCE265AA78)
-   The <span class="apiname">Subject</span> that is the result of
    authentication must be associated with the current access control
    context; see [How Do You Associate a Subject with an Access Control
    Context?](jaas-authorization-tutorial.html#GUID-BB640CDE-3EA5-4980-94F8-C821B98101FA).

</div>
<div class="sect3">
[]{#GUID-8BB38DE7-73AA-4560-AA28-D9CCE265AA78}

### How Do You Make Principal-Based Policy File Statements? {#JSSEC-GUID-8BB38DE7-73AA-4560-AA28-D9CCE265AA78 .sect3}

<div>
Policy file `grant`{.codeph} statements (see [Default Policy
Implementation and Policy File
Syntax](permissions-jdk1.html#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D)
can now optionally include one or more `Principal`{.codeph} fields.
Inclusion of a `Principal`{.codeph} field indicates that the user or
other entity represented by the specified `Principal`{.codeph},
executing the specified code, has the designated permissions.

Thus, the basic format of a `grant`{.codeph} statement is now

``` {.oac_no_warn dir="ltr"}
grant <signer(s) field>, <codeBase URL> 
  <Principal field(s)> {
    permission perm_class_name "target_name", "action";
    ....
    permission perm_class_name "target_name", "action";
  };
```

where each of the `signer`{.codeph}, `codeBase`{.codeph} and
`Principal`{.codeph} fields is optional and the order between the fields
doesn\'t matter.

A `Principal`{.codeph} field looks like the following:

``` {.oac_no_warn dir="ltr"}
Principal Principal_class "principal_name"
```

That is, it is the word `Principal`{.codeph} (where case doesn\'t
matter) followed by the (fully qualified) name of a `Principal`{.codeph}
class and a principal name.

A `Principal`{.codeph} class is a class that implements the
[<span class="apiname">java.security.Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
interface. All `Principal`{.codeph} objects have an associated name that
can be obtained by calling their `getName`{.codeph} method. The format
used for the name is dependent on each `Principal`{.codeph}
implementation.

The type of `Principal`{.codeph} placed in the `Subject`{.codeph}
created by the basic authentication mechanism used by this tutorial is
`SamplePrincipal`{.codeph}, so that is what should be used as the
`Principal_class`{.codeph} part of our `grant`{.codeph} statement\'s
`Principal`{.codeph} designation. User names for
`SamplePrincipal`{.codeph}s are of the form
<span class="variable">name</span>, and the only user name accepted for
this tutorial is `testUser`{.codeph}, so the `principal_name`{.codeph}
designation to use in the `grant`{.codeph} statement is
`testUser`{.codeph}.

It is possible to include more than one `Principal`{.codeph} field in a
`grant`{.codeph} statement. If multiple `Principal`{.codeph} fields are
specified, then the permissions in that `grant`{.codeph} statement are
granted only if the `Subject`{.codeph} associated with the current
access control context contains <span class="variable">all</span> of
those `Principal`{.codeph}s.

To grant the same set of permissions to different `Principal`{.codeph}s,
create multiple `grant`{.codeph} statements where each lists the
permissions and contains a single `Principal`{.codeph} field designating
one of the `Principal`{.codeph}s.

The policy file for this tutorial includes one `grant`{.codeph}
statement with a `Principal`{.codeph} field:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./SampleAction.jar",
        Principal sample.principal.SamplePrincipal "testUser" {

   permission java.util.PropertyPermission "java.home", "read";
   permission java.util.PropertyPermission "user.home", "read";
   permission java.io.FilePermission "foo.txt", "read";
};
```

This specifies that the indicated permissions are granted to the
specified `Principal`{.codeph} executing the code in
`SampleAction.jar`{.codeph}. (Note: the `SamplePrincipal`{.codeph} class
is in the `sample.principal`{.codeph} package.)

</div>
</div>
<div class="sect3">
[]{#GUID-BB640CDE-3EA5-4980-94F8-C821B98101FA}

### How Do You Associate a Subject with an Access Control Context? {#JSSEC-GUID-BB640CDE-3EA5-4980-94F8-C821B98101FA .sect3}

<div>
To create and associate a Subject with the current access control
context, you need the following:

-   The user must first be authenticated, as described in [JAAS
    Authentication
    Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4).
-   The static `doAs`{.codeph} method from the
    <span class="apiname">Subject</span> class must be called, passing
    it an authenticated <span class="apiname">Subject</span> and a
    [<span class="apiname">java.security.PrivilegedAction</span>](https://docs.oracle.com/javase/10/docs/api/java/security/PrivilegedAction.html)
    or
    [<span class="apiname">java.security.PrivilegedExceptionAction</span>](https://docs.oracle.com/javase/10/docs/api/java/security/PrivilegedExceptionAction.html).
    (See [Appendix A: API for Privileged
    Blocks](java-se-platform-security-architecture.html#GUID-BB3C8FB3-1A1A-47F3-8536-3952B84F46F2 "This section explains what privileged code is and what it is used for. It also shows you how to use the doPrivileged API.")
    in [Permissions in the
    JDK](permissions-jdk1.html#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.")
    for a comparison of PrivilegedAction and PrivilegedExceptionAction.)
    The `doAs`{.codeph} method associates the provided Subject with the
    current access control context and then invokes the `run`{.codeph}
    method from the action. The `run`{.codeph} method implementation
    contains all the code to be executed as the specified Subject. The
    action thus executes as the specified Subject.

    The static `doAsPrivileged`{.codeph} method from the Subject class
    may be called instead of the `doAs`{.codeph} method, as will be done
    for this tutorial. In addition to the parameters passed to
    `doAs`{.codeph}, `doAsPrivileged`{.codeph} requires a third
    parameter: an AccessControlContext. Unlike `doAs`{.codeph}, which
    associates the provided Subject with the current access control
    context, `doAsPrivileged`{.codeph} associates the Subject with the
    provided access control context or with an empty access control
    context if the parameter passed in is `null`{.codeph}, as is the
    case for this tutorial. See [doAs vs.
    doAsPrivileged](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-2A935F5E-0803-411D-B6BC-F8C64D01A25C)
    in the JAAS Reference Guide for a comparison of those methods.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-C1549AAE-E32F-449C-9A05-B175A5181EF8}

The Authorization Tutorial Code {#JSSEC-GUID-C1549AAE-E32F-449C-9A05-B175A5181EF8 .sect2}
-------------------------------

<div>
The code for this tutorial consists of four files:

-   [`SampleAzn.java`](jaas-authorization-tutorial.html#GUID-07EAB926-63EA-48F4-8DF0-4CC4526FA545__GUID-9AE66C05-0850-4AAF-8DD9-7D940069844F)
    is exactly the same as the `SampleAcn.java`{.codeph} application
    file from the [JAAS Authentication
    Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
    tutorial except for the additional code needed to call
    `Subject.doAsPrivileged`{.codeph}.
-   [`SampleAction.java`](jaas-authorization-tutorial.html#GUID-6ECF7E31-E49D-4DF7-B9C9-1EB62EA32510__GUID-49785CE0-3D88-480B-8F76-F87E8AB890E1)
    contains the `SampleAction`{.codeph} class. This class implements
    <span class="apiname">PrivilegedAction</span> and has a
    `run`{.codeph} method that contains all the code we want to be
    executed with <span class="apiname">Principal</span>-based
    authorization checks.
-   [`SampleLoginModule.java`](jaas-authentication-tutorial.html#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-F9A208EC-3247-4320-8158-82B0E84C6A04)
    is the class specified by the tutorial\'s login configuration file
    (see [The Login Configuration File for the JAAS Authorization
    Tutorial](jaas-authorization-tutorial.html#GUID-247D6204-446B-4B48-B376-5CD76CAFE3E7))
    as the class implementing the desired underlying authentication.
    `SampleLoginModule`{.codeph}\'s user authentication consists of
    simply verifying that the name and password specified by the user
    have specific values. This class was also used by the [JAAS
    Authentication
    Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
    tutorial and will not be discussed further here.
-   [`SamplePrincipal.java`](jaas-authentication-tutorial.html#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-3EA5533B-1284-481E-A35F-C82B17837F2E)
    is a sample class implementing the
    [<span class="apiname">java.security.Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
    interface. It is used by `SampleLoginModule`{.codeph}. This class
    was also used by the JAAS Authentication tutorial and will not be
    discussed further here.

The `SampleLoginModule.java`{.codeph} and
`SamplePrincipal.java`{.codeph} files were also used in the [JAAS
Authentication
Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
tutorial, so they are not described further here. The other source files
are described below.

</div>
<div class="sect3">
[]{#GUID-07EAB926-63EA-48F4-8DF0-4CC4526FA545}

### SampleAzn.java {#JSSEC-GUID-07EAB926-63EA-48F4-8DF0-4CC4526FA545 .sect3}

<div>
Like `SampleAcn`{.codeph}, the `SampleAzn`{.codeph} class instantiates a
<span class="apiname">LoginContext</span> `lc`{.codeph} and calls its
`login`{.codeph} method to perform the authentication. If successful,
the authenticated <span class="apiname">Subject</span> (which includes a
<span class="apiname">SamplePrincipal</span> representing the user) is
obtained by calling the <span class="apiname">LoginContext</span>\'s
`getSubject`{.codeph} method:

``` {.oac_no_warn dir="ltr"}
Subject mySubject = lc.getSubject();
```

After providing the user some information about the
<span class="apiname">Subject</span>, such as which
<span class="apiname">Principal</span>s it has, the `main`{.codeph}
method then calls `Subject.doAsPrivileged`{.codeph}, passing it the
authenticated <span class="apiname">Subject</span> `mySubject`{.codeph},
a <span class="apiname">PrivilegedAction</span>
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
which is considered to be executed on behalf of the
<span class="apiname">Subject</span> `mySubject`{.codeph}.

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

<div class="section" id="GUID-07EAB926-63EA-48F4-8DF0-4CC4526FA545__GUID-9AE66C05-0850-4AAF-8DD9-7D940069844F">
SampleAzn.java

``` {.oac_no_warn dir="ltr"}
package sample;

import java.io.*;
import java.util.*;
import java.security.Principal;
import java.security.PrivilegedAction;
import javax.security.auth.*;
import javax.security.auth.callback.*;
import javax.security.auth.login.*;
import javax.security.auth.spi.*;
import com.sun.security.auth.*;

/**
 * This Sample application attempts to authenticate a user
 * and executes a SampleAction as that user.
 *
 * If the user successfully authenticates itself,
 * the username and number of Credentials is displayed.
 */
public class SampleAzn {

    /**
     * Attempt to authenticate the user.
     *
     * @param args input arguments for this application.  These are ignored.
     */
     public static void main(String[] args) {

        // Obtain a LoginContext, needed for authentication. Tell it
        // to use the LoginModule implementation specified by the
        // entry named "Sample" in the JAAS login configuration
        // file and to also use the specified CallbackHandler.
        LoginContext lc = null;
        try {
            lc = new LoginContext("Sample", new MyCallbackHandler());
        } catch (LoginException le) {
            System.err.println("Cannot create LoginContext. "
                + le.getMessage());
            System.exit(-1);
        } catch (SecurityException se) {
            System.err.println("Cannot create LoginContext. "
                + se.getMessage());
            System.exit(-1);
        }

        // the user has 3 attempts to authenticate successfully
        int i;
        for (i = 0; i < 3; i++) {
            try {

                // attempt authentication
                lc.login();

                // if we return with no exception, authentication succeeded
                break;

            } catch (LoginException le) {

                  System.err.println("Authentication failed:");
                  System.err.println("  " + le.getMessage());
                  try {
                      Thread.currentThread().sleep(3000);
                  } catch (Exception e) {
                      // ignore
                  }

            }
        }

        // did they fail three times?
        if (i == 3) {
            System.out.println("Sorry");
            System.exit(-1);
        }

        System.out.println("Authentication succeeded!");

        Subject mySubject = lc.getSubject();

        // let's see what Principals we have
        Iterator principalIterator = mySubject.getPrincipals().iterator();
        System.out.println("Authenticated user has the following Principals:");
        while (principalIterator.hasNext()) {
            Principal p = (Principal)principalIterator.next();
            System.out.println("\t" + p.toString());
        }

        System.out.println("User has " +
                        mySubject.getPublicCredentials().size() +
                        " Public Credential(s)");

        // now try to execute the SampleAction as the authenticated Subject
        PrivilegedAction action = new SampleAction();
        Subject.doAsPrivileged(mySubject, action, null);

        System.exit(0);
    }
}

/**
 * A CallbackHandler implemented by the application.
 *
 * This application is text-based.  Therefore it displays information
 * to the user using the OutputStreams System.out and System.err,
 * and gathers input from the user using the InputStream System.in.
 */
class MyCallbackHandler implements CallbackHandler {

    /**
     * Invoke an array of Callbacks.
     *
     * @param callbacks an array of <code>Callback</code> objects which contain
     *                  the information requested by an underlying security
     *                  service to be retrieved or displayed.
     *
     * @exception java.io.IOException if an input or output error occurs. <p>
     *
     * @exception UnsupportedCallbackException if the implementation of this
     *                  method does not support one or more of the Callbacks
     *                  specified in the <code>callbacks</code> parameter.
     */
    public void handle(Callback[] callbacks)
    throws IOException, UnsupportedCallbackException {

        for (int i = 0; i < callbacks.length; i++) {
            if (callbacks[i] instanceof TextOutputCallback) {

                // display the message according to the specified type
                TextOutputCallback toc = (TextOutputCallback)callbacks[i];
                switch (toc.getMessageType()) {
                case TextOutputCallback.INFORMATION:
                    System.out.println(toc.getMessage());
                    break;
                case TextOutputCallback.ERROR:
                    System.out.println("ERROR: " + toc.getMessage());
                    break;
                case TextOutputCallback.WARNING:
                    System.out.println("WARNING: " + toc.getMessage());
                    break;
                default:
                    throw new IOException("Unsupported message type: " +
                                        toc.getMessageType());
                }

            } else if (callbacks[i] instanceof NameCallback) {

                // prompt the user for a username
                NameCallback nc = (NameCallback)callbacks[i];

                System.err.print(nc.getPrompt());
                System.err.flush();
                nc.setName((new BufferedReader
                        (new InputStreamReader(System.in))).readLine());

            } else if (callbacks[i] instanceof PasswordCallback) {

                // prompt the user for sensitive information
                PasswordCallback pc = (PasswordCallback)callbacks[i];
                System.err.print(pc.getPrompt());
                System.err.flush();
                pc.setPassword(System.console().readPassword());

            } else {
                throw new UnsupportedCallbackException
                        (callbacks[i], "Unrecognized Callback");
            }
        }
    }
}
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-6ECF7E31-E49D-4DF7-B9C9-1EB62EA32510}

### SampleAction.java {#JSSEC-GUID-6ECF7E31-E49D-4DF7-B9C9-1EB62EA32510 .sect3}

<div>
`SampleAction.java` contains the `SampleAction`{.codeph} class. This
class implements `java.security.PrivilegedAction`{.codeph} and has a
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

Here is the code:

<div class="section" id="GUID-6ECF7E31-E49D-4DF7-B9C9-1EB62EA32510__GUID-49785CE0-3D88-480B-8F76-F87E8AB890E1">
SampleAction.java

``` {.oac_no_warn dir="ltr"}
package sample;

import java.io.File;
import java.security.PrivilegedAction;

/**
 * This is a Sample PrivilegedAction implementation, designed to be
 * used with the Sample application.
 *
 */
public class SampleAction implements PrivilegedAction {

    /**
     * This Sample PrivilegedAction performs the following operations:
     * <ul>
     *   <li>Access the System property, <i>java.home</i></li>
     *   <li> Access the System property, <i>user.home</i></li>
     *   <li> Access the file, <i>foo.txt</i></li>
     * </ul>
     *
     * @return <code>null</code> in all cases.
     *
     * @exception SecurityException if the caller does not have permission
     *          to perform the operations listed above.
     */
    public Object run() {
        System.out.println("\nYour java.home property: "
                            +System.getProperty("java.home"));

        System.out.println("\nYour user.home property: "
                            +System.getProperty("user.home"));

        File f = new File("foo.txt");
        System.out.print("\nfoo.txt does ");
        if (!f.exists())
            System.out.print("not ");
        System.out.println("exist in the current working directory.");
        return null;
    }
}
```

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-247D6204-446B-4B48-B376-5CD76CAFE3E7}

The Login Configuration File for the JAAS Authorization Tutorial {#JSSEC-GUID-247D6204-446B-4B48-B376-5CD76CAFE3E7 .sect2}
----------------------------------------------------------------

<div>
The login configuration file used for this tutorial can be exactly the
same as that used by the [JAAS Authentication
Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
tutorial. Thus we can use the `sample_jaas.config` file, which contains
just one entry:

``` {.oac_no_warn dir="ltr"}
Sample {
  sample.module.SampleLoginModule required debug=true;
};
```

This entry is named `Sample`{.codeph} and that is the name that both our
tutorial applications `SampleAcn`{.codeph} and `SampleAzn`{.codeph} use
to refer to it. The entry specifies that the
<span class="apiname">LoginModule</span> to be used to do the user
authentication is the `SampleLoginModule`{.codeph} in the
`sample.module`{.codeph} package and that this
`SampleLoginModule`{.codeph} is required to \"succeed\" in order for
authentication to be considered successful. The
`SampleLoginModule`{.codeph} succeeds only if the name and password
supplied by the user are the one it expects (`testUser`{.codeph} and
`testPassword`{.codeph}, respectively).

The <span class="apiname">SampleLoginModule</span> also defines a
`debug`{.codeph} option that can be set to `true`{.codeph} as shown. If
this option is set to `true,`{.codeph}
<span class="apiname">SampleLoginModule</span> outputs extra information
about the progress of authentication.

</div>
</div>
<div class="sect2">
[]{#GUID-8462E46D-FF67-4630-9A87-D24EE60D100C}

The Policy File {#JSSEC-GUID-8462E46D-FF67-4630-9A87-D24EE60D100C .sect2}
---------------

<div>
The application for this authorization tutorial consists of two classes,
`SampleAzn`{.codeph} and `SampleAction`{.codeph}. The code in each class
contains some security-sensitive operations and thus relevant
permissions are required in a policy file in order for the operations to
be executed.

The <span class="apiname">LoginModule</span> used by this tutorial,
`SampleLoginModule`{.codeph}, also contains an operation requiring a
permission.

The permissions required by each of these classes are described below,
followed by the full policy file.

</div>
<div class="sect3">
[]{#GUID-B048635B-ACC3-4049-BFAA-16F047ABA415}

### Permissions Required by SampleAzn {#JSSEC-GUID-B048635B-ACC3-4049-BFAA-16F047ABA415 .sect3}

<div>
The main method of the `SampleAzn`{.codeph} class does two operations
for which permissions are required. It

-   creates a <span class="apiname">LoginContext</span>, and
-   calls the `doAsPrivileged`{.codeph} static method of the Subject
    class.

The <span class="apiname">LoginContext</span> creation is exactly the
same as was done in the authentication tutorial, and it thus needs the
same `javax.security.auth.AuthPermission`{.codeph} permission with
target \"`createLoginContext.Sample`{.codeph}\".

In order to call the `doAsPrivileged`{.codeph} method of the
<span class="apiname">Subject</span> class, you need to have a
`javax.security.auth.AuthPermission`{.codeph} with target
\"`doAsPrivileged`{.codeph}\".

Assuming the `SampleAzn`{.codeph} class is placed in a JAR file named
`SampleAzn.jar`{.codeph}, these permissions can be granted to the
`SampleAzn`{.codeph} code via the following `grant`{.codeph} statement
in the policy file:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./SampleAzn.jar" {
   permission javax.security.auth.AuthPermission 
                    "createLoginContext.Sample";
   permission javax.security.auth.AuthPermission "doAsPrivileged";
};
```

</div>
</div>
<div class="sect3">
[]{#GUID-1C4609F2-96F3-4B8B-BFF4-1496301EA4B0}

### Permissions Required by SampleAction {#JSSEC-GUID-1C4609F2-96F3-4B8B-BFF4-1496301EA4B0 .sect3}

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
Statements?](jaas-authorization-tutorial.html#GUID-8BB38DE7-73AA-4560-AA28-D9CCE265AA78),
our `grant`{.codeph} statement looks like the following:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./SampleAction.jar", Principal sample.principal.SamplePrincipal "testUser" {
    permission java.util.PropertyPermission "java.home", "read";
    permission java.util.PropertyPermission "user.home", "read";
    permission java.io.FilePermission "foo.txt", "read";
};
```

</div>
</div>
<div class="sect3">
[]{#GUID-C7890B53-2A4B-4024-8A67-23CAFC81C496}

### Permissions Required by SampleLoginModule {#JSSEC-GUID-C7890B53-2A4B-4024-8A67-23CAFC81C496 .sect3}

<div>
The `SampleLoginModule`{.codeph} code does one operation for which
permissions are required. It needs a
`javax.security.auth.AuthPermission`{.codeph} with target
\"`modifyPrincipals`{.codeph}\" in order to populate a
`Subject`{.codeph} with a `Principal`{.codeph}. The grant statement is
the following:

``` {.oac_no_warn dir="ltr"}
grant codebase "file:./SampleLM.jar" {
    permission javax.security.auth.AuthPermission "modifyPrincipals";
};
```

</div>
</div>
<div class="sect3">
[]{#GUID-3A2FF6CF-3124-4402-B550-D0F4E76B3D4D}

### The Full Policy File {#JSSEC-GUID-3A2FF6CF-3124-4402-B550-D0F4E76B3D4D .sect3}

<div>
The full policy file is `sampleazn.policy`:

<div class="section" id="GUID-3A2FF6CF-3124-4402-B550-D0F4E76B3D4D__GUID-6CA8F774-5E38-437D-8549-9604DEC5C317">
sampleazn.policy

``` {.oac_no_warn dir="ltr"}
/* grant the sample LoginModule permissions */

grant codebase "file:./SampleAction.jar", Principal sample.principal.SamplePrincipal "testUser" {
    permission java.util.PropertyPermission "java.home", "read";
    permission java.util.PropertyPermission "user.home", "read";
    permission java.io.FilePermission "foo.txt", "read";
};

grant codebase "file:./SampleLM.jar" {
    permission javax.security.auth.AuthPermission "modifyPrincipals";
};

grant codebase "file:./SampleAcn.jar" {
   permission javax.security.auth.AuthPermission "createLoginContext.Sample";
};
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-04A78ED2-B68C-4C89-849D-F9BF4F17BBD1}

### Running the Authorization Tutorial Code {#JSSEC-GUID-04A78ED2-B68C-4C89-849D-F9BF4F17BBD1 .sect3}

<div>
To execute our JAAS authorization tutorial code, all you have to do is

1.  Place the following files into a directory:

    -   `sample_jaas.config` login configuration file (see [The Login
        Configuration File for the JAAS Authorization
        Tutorial](jaas-authorization-tutorial.html#GUID-247D6204-446B-4B48-B376-5CD76CAFE3E7))
    -   [`sampleazn.policy`](jaas-authorization-tutorial.html#GUID-3A2FF6CF-3124-4402-B550-D0F4E76B3D4D__GUID-6CA8F774-5E38-437D-8549-9604DEC5C317)
        policy file

2.  Create a subdirectory named `sample` of that top-level directory,
    and place the following into it (note the `SampleAzn`{.codeph} and
    `SampleAction`{.codeph} classes are in a package named
    `sample`{.codeph}):

    -   [`SampleAzn.java`](jaas-authorization-tutorial.html#GUID-07EAB926-63EA-48F4-8DF0-4CC4526FA545__GUID-9AE66C05-0850-4AAF-8DD9-7D940069844F)
        source file
    -   [`SampleAction.java`](jaas-authorization-tutorial.html#GUID-6ECF7E31-E49D-4DF7-B9C9-1EB62EA32510__GUID-49785CE0-3D88-480B-8F76-F87E8AB890E1)
        source file

3.  Create a subdirectory of the `sample` directory and name it
    `module`. Place the following into it (note the
    `SampleLoginModule`{.codeph} class is in a package named
    `sample.module`{.codeph}):

    -   [`SampleLoginModule.java`](jaas-authentication-tutorial.html#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-F9A208EC-3247-4320-8158-82B0E84C6A04)
        source file

4.  Create another subdirectory of the `sample` directory and name it
    `principal`. Place the following into it (note the
    `SamplePrincipal`{.codeph} class is in a package named
    `sample.principal`{.codeph}):

    -   [`SamplePrincipal.java`](jaas-authentication-tutorial.html#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-3EA5533B-1284-481E-A35F-C82B17837F2E)
        source file

5.  While in the top-level directory, compile all the source files:

    `javac sample/SampleAction.java sample/SampleAzn.java sample/module/SampleLoginModule.java sample/principal/SamplePrincipal.java`{.codeph}

    (Type all that on one line.)

6.  Create a JAR file named `SampleAzn.jar`{.codeph} containing
    `SampleAzn.class`{.codeph} and `MyCallbackHandler.class`{.codeph}
    (Note the sources for both these classes are in
    `SampleAzn.java`{.codeph}):

    `jar -cvf SampleAzn.jar sample/SampleAzn.class sample/MyCallbackHandler.class `{.codeph}

    (Type all that on one line.)

7.  Create a JAR file named `SampleAction.jar`{.codeph} containing
    `SampleAction.class`{.codeph}:

    `jar -cvf SampleAction.jar sample/SampleAction.class `{.codeph}

8.  Create a JAR file containing `SampleLoginModule.class`{.codeph} and
    `SamplePrincipal.class`{.codeph}:

    `jar -cvf SampleLM.jar sample/module/SampleLoginModule.class  sample/principal/SamplePrincipal.class `{.codeph}

9.  Execute the `SampleAzn`{.codeph} application, specifying

    a.  by an appropriate `-classpath`{.codeph} clause that classes
        should be searched for in the `SampleAzn.jar`{.codeph},
        `SampleAction.jar`{.codeph}, and `SampleLM.jar`{.codeph} JAR
        files,
    b.  by `-Djava.security.manager`{.codeph} that a security manager
        should be installed,
    c.  by `-Djava.security.policy==sampleazn.policy`{.codeph} that the
        policy file to be used is `sampleazn.policy`{.codeph}, and
    d.  by
        `-Djava.security.auth.login.config==sample_jaas.config`{.codeph}
        that the login configuration file to be used is
        `sample_jaas.config`{.codeph}.

    Below are the full commands to use for both Windows and Solaris,
    Linux, and macOS systems. The only difference is that on Windows
    systems you use semicolons to separate class path items, while you
    use colons for that purpose on Solaris, Linux, and macOS systems.

    Here is the full command for Windows systems:

    ``` {.oac_no_warn dir="ltr"}
    java -classpath SampleAzn.jar;SampleAction.jar;SampleLM.jar 
     -Djava.security.manager 
     -Djava.security.policy==sampleazn.policy 
     -Djava.security.auth.login.config==sample_jaas.config sample.SampleAzn
    ```

    Here is the full command for Solaris, Linux, and macOS systems:

    ``` {.oac_no_warn dir="ltr"}
    java -classpath SampleAzn.jar:SampleAction.jar:SampleLM.jar 
     -Djava.security.manager 
     -Djava.security.policy==sampleazn.policy 
     -Djava.security.auth.login.config==sample_jaas.config sample.SampleAzn
    ```

    Type the full command on one line. Multiple lines are used here for
    legibility. If the command is too long for your system, you may need
    to place it in a `.bat` file (for Windows) or a `.sh` file (for
    Solaris, Linux, and macOS) and then run that file to execute the
    command.

    You will be prompted for a user name and password (use
    `testUser`{.codeph} and `testPassword`{.codeph}), and the
    `SampleLoginModule`{.codeph} specified in the login configuration
    file will check the name and password. If your login is successful,
    you will see the message `Authentication succeeded!`{.codeph} and if
    not, you will see `Authentication failed:`{.codeph} followed by a
    reason for the failure.

    Once authentication is successfully completed, the rest of the
    program (in `SampleAction`{.codeph}) will be executed on behalf of
    you, the user, requiring you to have been granted appropriate
    permissions. The `sampleazn.policy`{.codeph} policy file grants you
    the required permissions, so you will see a display of the values of
    your `java.home`{.codeph} and `user.home`{.codeph} system properties
    and a statement as to whether or not you have a file named
    `foo.txt`{.codeph} in the current directory.

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
| ------------- ------ | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| ------------- --     | o | ass="icon">Contents< |
|                [![Pr | g | /span>](toc.htm)     |
| evious](../../dcommo | o |   -- --------------- |
| n/gifs/leftnav.gif)\ | ] | -------------------- |
|                      | ( | -------------------- |
|                      | . | ---                  |
|             [![Next] | . |                      |
| (../../dcommon/gifs/ | / |                      |
| rightnav.gif)\       | . |                      |
|                      | . |                      |
|                      | / |                      |
|    <span class="icon | d |                      |
| ">Previous</span>](j | c |                      |
| aas-authentication-t | o |                      |
| utorial.htm)   <span | m |                      |
|  class="icon">Next</ | m |                      |
| span>](java-authenti | o |                      |
| cation-and-authoriza | n |                      |
| tion-service-jaas-lo | / |                      |
| ginmodule-developers | g |                      |
| -guide1.htm)         | i |                      |
|   ------------------ | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| ------------- ------ | o |                      |
| -------------------- | r |                      |
| -------------------- | a |                      |
| -------------------- | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| ------------- --     | . |                      |
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
