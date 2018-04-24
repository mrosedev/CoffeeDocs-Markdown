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

  --------------------------------------------------------- ------------------------------------------------------------------ --
        [![Previous](../../dcommon/gifs/leftnav.gif)\                   [![Next](../../dcommon/gifs/rightnav.gif)\             
   <span class="icon">Previous</span>](jaas-tutorials.htm)   <span class="icon">Next</span>](jaas-authorization-tutorial.htm)  
  --------------------------------------------------------- ------------------------------------------------------------------ --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4}<!-- End Header -->

JAAS Authentication Tutorial {#JSSEC-GUID-BFEBDB00-9826-499C-A20F-E9463883DED4 .sect1}
============================

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
The authorization component will be described in the [JAAS Authorization
Tutorial](jaas-authorization-tutorial.htm#GUID-D43CF965-8A5F-4A23-A2AF-F41DD5F8B411).

JAAS authentication is performed in a
<span class="variable">pluggable</span> fashion. This permits Java
applications to remain independent from underlying authentication
technologies. New or updated technologies can be plugged in without
requiring modifications to the application itself. An implementation for
a particular authentication technology to be used is determined at
runtime. The implementation is specified in a login configuration file.
The authentication technology used for this tutorial is very basic, just
ensuring that the user specifies a particular name and password.

The rest of this tutorial consists of the following sections:

1.  [The Authentication Tutorial
    Code](jaas-authentication-tutorial.htm#GUID-EF77AA97-CB87-4D1D-A3BF-8541FF41BA4A)
2.  [The Login
    Configuration](jaas-authentication-tutorial.htm#GUID-987700C5-AE03-4EB1-B16A-66A1404B9604)
3.  [Running the
    Code](jaas-authentication-tutorial.htm#GUID-743703A2-7EC1-4391-A816-4A883FB6A017)
4.  [Running the Code with a Security
    Manager](jaas-authentication-tutorial.htm#GUID-44F2BF3A-F51D-4F21-8F40-96CB1120396D)

If you want to first see the tutorial code in action, you can skip
directly to [Running the
Code](jaas-authentication-tutorial.htm#GUID-743703A2-7EC1-4391-A816-4A883FB6A017)
and then go back to the other sections to learn about coding and
configuration file details.

</div>
<div class="sect2">
[]{#GUID-EF77AA97-CB87-4D1D-A3BF-8541FF41BA4A}

The Authentication Tutorial Code {#JSSEC-GUID-EF77AA97-CB87-4D1D-A3BF-8541FF41BA4A .sect2}
--------------------------------

<div>
The code for this tutorial consists of three files:

-   [`SampleAcn.java`](jaas-authentication-tutorial.htm#GUID-E007D5F4-3FA5-417A-B85F-E669839F0101__GUID-1270A0AC-EA51-4A47-B9BC-BDB42F96F5FE)
    contains the sample application class (`SampleAcn`{.codeph}) and
    another class used to handle user input
    (`MyCallbackHandler`{.codeph}). <span class="bold">The code in this
    file is the only code you need to understand for this tutorial. Your
    application will only indirectly use the other source files.</span>
-   [`SampleLoginModule.java`](jaas-authentication-tutorial.htm#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-F9A208EC-3247-4320-8158-82B0E84C6A04)
    is the class specified by the tutorial\'s login configuration file,
    `sample_jass.config`, described in [The Login Configuration File for
    the JAAS Authentication
    Tutorial](jaas-authentication-tutorial.htm#GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F)
    as the class implementing the desired underlying authentication.
    `SampleLoginModule`{.codeph}\'s user authentication consists of
    simply verifying that the name and password specified by the user
    have specific values.
-   [`SamplePrincipal.java`](jaas-authentication-tutorial.htm#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-3EA5533B-1284-481E-A35F-C82B17837F2E)
    is a sample class implementing the
    [<span class="apiname">java.security.Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
    interface. It is used by `SampleLoginModule`{.codeph}.

</div>
<div class="sect3">
[]{#GUID-01DE56D2-3A45-4C38-83EB-257783975372}

### SampleAcn.java {#JSSEC-GUID-01DE56D2-3A45-4C38-83EB-257783975372 .sect3}

<div>
Our authentication tutorial application code is contained in a single
source file, `SampleAcn.java`. That file contains two classes:

-   [The SampleAcn
    Class](jaas-authentication-tutorial.htm#GUID-8DE2AB48-46DC-4EDC-B6E1-93EE0E35D801)
-   [The MyCallbackHandler
    Class](jaas-authentication-tutorial.htm#GUID-3D19984B-76FE-4BD6-8B21-44512936DAEE)

</div>
<div class="sect4">
[]{#GUID-8DE2AB48-46DC-4EDC-B6E1-93EE0E35D801}

#### The SampleAcn Class {#JSSEC-GUID-8DE2AB48-46DC-4EDC-B6E1-93EE0E35D801 .sect4}

<div>
The `main`{.codeph} method of the `SampleAcn`{.codeph} class performs
the authentication and then reports whether or not authentication
succeeded.

The code for authenticating the user is very simple, consisting of just
two steps:

1.  [Instantiating a
    LoginContext](jaas-authentication-tutorial.htm#GUID-C6F31AF5-24D6-48FD-B92C-930BFC312FDE)
2.  [Calling the LoginContext\'s login
    Method](jaas-authentication-tutorial.htm#GUID-A2D1F3BA-3CFF-498A-A1F0-9E728C5C5C51)

First the basic code is shown, followed by [The Complete SampleAcn Class
Code](jaas-authentication-tutorial.htm#GUID-E007D5F4-3FA5-417A-B85F-E669839F0101),
complete with the import statement it requires and error handling.

</div>
<div class="sect5">
[]{#GUID-C6F31AF5-24D6-48FD-B92C-930BFC312FDE}

##### Instantiating a LoginContext {#JSSEC-GUID-C6F31AF5-24D6-48FD-B92C-930BFC312FDE .sect5}

<div>
In order to authenticate a user, you first need a
`javax.security.auth.login.LoginContext`{.codeph}. Here is the basic way
to instantiate a LoginContext:

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
. . .
LoginContext lc =
    new LoginContext("Sample",
          new MyCallbackHandler());
```

The arguments are the following:

1.  <span class="bold">The name of an entry in the JAAS login
    configuration file</span>

    This is the name for the <span class="apiname">LoginContext</span>
    to use to look up an entry for this application in the JAAS login
    configuration file, described in [The Login
    Configuration](jaas-authentication-tutorial.htm#GUID-987700C5-AE03-4EB1-B16A-66A1404B9604).
    Such an entry specifies the class(es) that implement the desired
    underlying authentication technology(ies). The class(es) must
    implement the <span class="apiname">LoginModule</span> interface,
    which is in the `javax.security.auth.spi`{.codeph} package.

    In our sample code, we use the `SampleLoginModule`{.codeph} supplied
    with this tutorial. The `SampleLoginModule`{.codeph} performs
    authentication by ensuring that the user types a particular name and
    password.

    The entry in the login configuration file we use for this tutorial,
    `sample_jass.config` (see [The Login Configuration File for the JAAS
    Authentication
    Tutorial](jaas-authentication-tutorial.htm#GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F)),
    has the name \"Sample\", so that is the name we specify as the first
    argument to the LoginContext constructor.

2.  <span class="bold">A CallbackHandler instance</span>

    When a <span class="apiname">LoginModule</span> needs to communicate
    with the user, for example to ask for a user name and password, it
    does not do so directly. That is because there are various ways of
    communicating with a user, and it is desirable for
    <span class="apiname">LoginModule</span>s to remain independent of
    the different types of user interaction. Rather, the
    <span class="apiname">LoginModule</span> invokes a
    [<span class="apiname">javax.security.auth.callback.CallbackHandler</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/CallbackHandler.html)
    to perform the user interaction and obtain the requested
    information, such as the user name and password.

    An instance of the particular
    <span class="apiname">CallbackHandler</span> to be used is specified
    as the second argument to the
    <span class="apiname">LoginContext</span> constructor. The
    <span class="apiname">LoginContext</span> forwards that instance to
    the underlying <span class="apiname">LoginModule</span> (in our case
    `SampleLoginModule`{.codeph}). An application typically provides its
    own <span class="apiname">CallbackHandler</span> implementation. A
    simple <span class="apiname">CallbackHandler</span>,
    <span class="apiname">TextCallbackHandler</span>, is provided in the
    `com.sun.security.auth.callback`{.codeph} package to output
    information to and read input from the command line. However, we
    instead demonstrate the more typical case of an application
    providing its own <span class="apiname">CallbackHandler</span>
    implementation, described in [The MyCallbackHandler
    Class](jaas-authentication-tutorial.htm#GUID-3D19984B-76FE-4BD6-8B21-44512936DAEE).

</div>
</div>
<div class="sect5">
[]{#GUID-A2D1F3BA-3CFF-498A-A1F0-9E728C5C5C51}

##### Calling the LoginContext\'s login Method {#JSSEC-GUID-A2D1F3BA-3CFF-498A-A1F0-9E728C5C5C51 .sect5}

<div>
Once we have a <span class="apiname">LoginContext</span> `lc`{.codeph},
we can call its `login`{.codeph} method to carry out the authentication
process:

``` {.oac_no_warn dir="ltr"}
lc.login();
```

The <span class="apiname">LoginContext</span> instantiates a new empty
[<span class="apiname">javax.security.auth.Subject</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Subject.html)
object (which represents the user or service being authenticated; see
[Subject](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3)).
The <span class="apiname">LoginContext</span> constructs the configured
<span class="apiname">LoginModule</span> (in our case
`SampleLoginModule`{.codeph}) and initializes it with this new
<span class="apiname">Subject</span> and `MyCallbackHandler`{.codeph}.

The <span class="apiname">LoginContext</span>\'s `login`{.codeph} method
then calls methods in the `SampleLoginModule`{.codeph} to perform the
login and authentication. The `SampleLoginModule`{.codeph} will utilize
the `MyCallbackHandler`{.codeph} to obtain the user name and password.
Then the `SampleLoginModule`{.codeph} will check that the name and
password are the ones it expects.

If authentication is successful, the `SampleLoginModule`{.codeph}
populates the <span class="apiname">Subject</span> with a
<span class="apiname">Principal</span> representing the user. The
<span class="apiname">Principal</span> the `SampleLoginModule`{.codeph}
places in the <span class="apiname">Subject</span> is an instance of
`SamplePrincipal`{.codeph}, which is a sample class implementing the
[<span class="apiname">java.security.Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
interface.

The calling application can subsequently retrieve the authenticated
<span class="apiname">Subject</span> by calling the
<span class="apiname">LoginContext</span>\'s `getSubject`{.codeph}
method, although doing so is not necessary for this tutorial.

</div>
</div>
<div class="sect5">
[]{#GUID-E007D5F4-3FA5-417A-B85F-E669839F0101}

##### The Complete SampleAcn Class Code {#JSSEC-GUID-E007D5F4-3FA5-417A-B85F-E669839F0101 .sect5}

<div>
Now that you have seen the basic code required to authenticate the user,
we can put it all together into the full class in `SampleAcn.java`,
which includes relevant import statements and error handling:

<div class="section" id="GUID-E007D5F4-3FA5-417A-B85F-E669839F0101__GUID-1270A0AC-EA51-4A47-B9BC-BDB42F96F5FE">
SampleAcn.java

``` {.oac_no_warn dir="ltr"}
package sample;

import java.io.*;
import java.util.*;
import javax.security.auth.login.*;
import javax.security.auth.*;
import javax.security.auth.callback.*;

/**
 * This Sample application attempts to authenticate a user
 * and reports whether or not the authentication was successful.
 */
public class SampleAcn {

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

    }
}


/**
 * The application implements the CallbackHandler.
 *
 * <p> This application is text-based.  Therefore it displays information
 * to the user using the OutputStreams System.out and System.err,
 * and gathers input from the user using the InputStream System.in.
 */
class MyCallbackHandler implements CallbackHandler {

    /**
     * Invoke an array of Callbacks.
     *
     * <p>
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
</div>
<div class="sect4">
[]{#GUID-3D19984B-76FE-4BD6-8B21-44512936DAEE}

#### The MyCallbackHandler Class {#JSSEC-GUID-3D19984B-76FE-4BD6-8B21-44512936DAEE .sect4}

<div>
In some cases a <span class="apiname">LoginModule</span> must
communicate with the user to obtain authentication information.
<span class="apiname">LoginModule</span>s use a
[`javax.security.auth.callback.CallbackHandler`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/CallbackHandler.html)
for this purpose. An application can either use one of the sample
implementations provided in the
`com.sun.security.auth.callback`{.codeph} package or, more typically,
write a <span class="apiname">CallbackHandler</span> implementation. The
application passes the <span class="apiname">CallbackHandler</span> as
an argument to the <span class="apiname">LoginContext</span>
instantiation. The <span class="apiname">LoginContext</span> forwards
the <span class="apiname">CallbackHandler</span> directly to the
underlying <span class="apiname">LoginModule</span>s.

The tutorial sample code supplies its own
<span class="apiname">CallbackHandler</span> implementation, the
`MyCallbackHandler`{.codeph} class in
[``](jaas-authentication-tutorial.htm#GUID-01DE56D2-3A45-4C38-83EB-257783975372).

<span class="apiname">CallbackHandler</span> is an interface with one
method to implement:

``` {.oac_no_warn dir="ltr"}
     void handle(Callback[] callbacks)
         throws java.io.IOException, UnsupportedCallbackException;
```

The <span class="apiname">LoginModule</span> passes the
<span class="apiname">CallbackHandler</span> handle method an array of
appropriate
[<span class="apiname">javax.security.auth.callback.Callback</span>s](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/Callback.html),
for example a
[<span class="apiname">NameCallback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/NameCallback.html)
for the user name and a
[<span class="apiname">PasswordCallback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/PasswordCallback.html)
for the password, and the <span class="apiname">CallbackHandler</span>
performs the requested user interaction and sets appropriate values in
the <span class="apiname">Callback</span>s.

The `MyCallbackHandler`{.codeph} `handle`{.codeph} method is structured
as follows:

``` {.oac_no_warn dir="ltr"}
public void handle(Callback[] callbacks)
  throws IOException, UnsupportedCallbackException {

  for (int i = 0; i < callbacks.length; i++) {
    if (callbacks[i] instanceof TextOutputCallback) {

      // display a message according to a specified type
      . . .

    } else if (callbacks[i] instanceof NameCallback) {

      // prompt the user for a username
      . . .

    } else if (callbacks[i] instanceof PasswordCallback) {

      // prompt the user for a password
      . . .

    } else {
        throw new UnsupportedCallbackException
         (callbacks[i], "Unrecognized Callback");
    }
  }
}
```

A <span class="apiname">CallbackHandler</span>
<span class="apiname">handle</span> method is passed an array of
<span class="apiname">Callback</span> instances, each of a particular
type (<span class="apiname">NameCallback</span>,
<span class="apiname">PasswordCallback</span>, etc.). It must handle
each Callback, performing user interaction in a way that is appropriate
for the executing application.

`MyCallbackHandler`{.codeph} handles three types of Callbacks:
<span class="bold"><span class="apiname">NameCallback</span></span> to
prompt the user for a user name,
<span class="bold"><span class="apiname">PasswordCallback</span></span>
to prompt for a password, and
<span class="bold"><span class="apiname">TextOutputCallback</span></span>
to report any error, warning, or other messages the
<span class="apiname">SampleLoginModule</span> wishes to send to the
user.

The <span class="apiname">handle</span> method handles a
<span class="bold"><span class="apiname">TextOutputCallback</span></span>
by extracting the message to be reported and then printing it to
`System.out`{.codeph}, optionally preceded by additional wording that
depends on the message type. The message to be reported is determined by
calling the <span class="apiname">TextOutputCallback</span>\'s
<span class="apiname">getMessage</span> method and the type by calling
its <span class="apiname">getMessageType</span> method. Here is the code
for handling a <span class="apiname">TextOutputCallback</span>:

``` {.oac_no_warn dir="ltr"}
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
```

The `handle`{.codeph} method handles a
<span class="bold"><span class="apiname">NameCallback</span></span> by
prompting the user for a user name. It does this by printing the prompt
to `System.err`{.codeph}. It then sets the name for use by the
`SampleLoginModule`{.codeph} by calling the
<span class="apiname">NameCallback</span>\'s `setName`{.codeph} method,
passing it the name typed by the user:

``` {.oac_no_warn dir="ltr"}
} else if (callbacks[i] instanceof NameCallback) {

    // prompt the user for a username
    NameCallback nc = (NameCallback)callbacks[i];

    System.err.print(nc.getPrompt());
    System.err.flush();
    nc.setName((new BufferedReader
        (new InputStreamReader(System.in))).readLine());
```

Similarly, the `handle`{.codeph} method handles a
<span class="bold"><span class="apiname">PasswordCallback</span></span>
by printing a prompt to `System.err`{.codeph} to prompt the user for a
password. It then sets the password for use by the
`SampleLoginModule`{.codeph} by calling the
<span class="apiname">PasswordCallback</span>\'s `setPassword`{.codeph}
method, passing it the password typed by the user:

``` {.oac_no_warn dir="ltr"}
} else if (callbacks[i] instanceof PasswordCallback) {

    // prompt the user for sensitive information
    PasswordCallback pc = (PasswordCallback)callbacks[i];

    System.err.print(pc.getPrompt());
    System.err.flush();
    pc.setPassword(System.console().readPassword());
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075}

### SampleLoginModule.java and SamplePrincipal.java {#JSSEC-GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075 .sect3}

<div>
`SampleLoginModule.java` implements the
[`LoginModule`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html)
interface. `SampleLoginModule`{.codeph} is the class specified by the
tutorial\'s login configuration file (see [The Login Configuration File
for the JAAS Authentication
Tutorial](jaas-authentication-tutorial.htm#GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F))
as the class implementing the desired underlying authentication.
`SampleLoginModule`{.codeph}\'s user authentication consists of simply
verifying that the name and password specified by the user have specific
values. This `SampleLoginModule`{.codeph} is specified by the
tutorial\'s login configuration file as the
<span class="apiname">LoginModule</span> to use because (1) It performs
a basic type of authentication suitable for any environment and thus is
appropriate for a tutorial for all users, and (2) It provides an example
<span class="apiname">LoginModule</span> implementation for experienced
programmers who require the ability to write a
<span class="apiname">LoginModule</span> implementing an authentication
technology.

`SamplePrincipal.java` is a sample class implementing the
[<span class="apiname">java.security.Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)
interface. If authentication is successful, the
`SampleLoginModule`{.codeph} populates a
[<span class="apiname">Subject</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Subject.html)
with a `SamplePrincipal`{.codeph} representing the user.

<span class="bold">Important: If you are an application writer, you do
not need to know how to write a <span class="apiname">LoginModule</span>
or a <span class="apiname">Principal</span> implementation. You do not
need to examine the `SampleLoginModule`{.codeph} or
`SamplePrincipal`{.codeph} code.</span> All you have to know is how to
write your application and specify configuration information (such as in
a login configuration file) such that the application will be able to
utilize the <span class="apiname">LoginModule</span> specified by the
configuration to authenticate the user. You need to determine which
<span class="apiname">LoginModule</span>(s) you want to use and read the
<span class="apiname">LoginModule</span>\'s documentation to learn about
what options you can specify values for (in the configuration) to
control the <span class="apiname">LoginModule</span>\'s behavior.

Any vendor can provide a LoginModule implementation that you can use.
Some implementations are supplied with the JRE from Oracle, as listed in
[Appendix B: JAAS Login Configuration
File](appendix-b-jaas-login-configuration-file.htm#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E).

Information for programmers who want to write a
<span class="apiname">LoginModule</span> can be found in [Java
Authentication and Authorization Service (JAAS): LoginModule
Developer\'s
Guide](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A).

<div class="section" id="GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-F9A208EC-3247-4320-8158-82B0E84C6A04">
SampleLoginModule.java

``` {.oac_no_warn dir="ltr"}
package sample.module;

import java.util.*;
import java.io.IOException;
import javax.security.auth.*;
import javax.security.auth.callback.*;
import javax.security.auth.login.*;
import javax.security.auth.spi.*;
import sample.principal.SamplePrincipal;

/**
 * <p> This sample LoginModule authenticates users with a password.
 *
 * <p> This LoginModule only recognizes one user:       testUser
 * <p> testUser's password is:  testPassword
 *
 * <p> If testUser successfully authenticates itself,
 * a <code>SamplePrincipal</code> with the testUser's user name
 * is added to the Subject.
 *
 * <p> This LoginModule recognizes the debug option.
 * If set to true in the login Configuration,
 * debug messages will be output to the output stream, System.out.
 *
 */
public class SampleLoginModule implements LoginModule {

    // initial state
    private Subject subject;
    private CallbackHandler callbackHandler;
    private Map sharedState;
    private Map options;

    // configurable option
    private boolean debug = false;

    // the authentication status
    private boolean succeeded = false;
    private boolean commitSucceeded = false;

    // username and password
    private String username;
    private char[] password;

    // testUser's SamplePrincipal
    private SamplePrincipal userPrincipal;

    /**
     * Initialize this <code>LoginModule</code>.
     *
     * @param subject the <code>Subject</code> to be authenticated. <p>
     *
     * @param callbackHandler a <code>CallbackHandler</code> for communicating
     *                  with the end user (prompting for user names and
     *                  passwords, for example). <p>
     *
     * @param sharedState shared <code>LoginModule</code> state. <p>
     *
     * @param options options specified in the login
     *                  <code>Configuration</code> for this particular
     *                  <code>LoginModule</code>.
     */
    public void initialize(Subject subject,
                   CallbackHandler callbackHandler,
                         Map<java.lang.String, ?> sharedState,
                         Map<java.lang.String, ?> options) {

        this.subject = subject;
        this.callbackHandler = callbackHandler;
        this.sharedState = sharedState;
        this.options = options;

        // initialize any configured options
        debug = "true".equalsIgnoreCase((String)options.get("debug"));
    }

    /**
     * Authenticate the user by prompting for a user name and password.
     *
     * @return true in all cases since this <code>LoginModule</code>
     *          should not be ignored.
     *
     * @exception FailedLoginException if the authentication fails. <p>
     *
     * @exception LoginException if this <code>LoginModule</code>
     *          is unable to perform the authentication.
     */
    public boolean login() throws LoginException {

        // prompt for a user name and password
        if (callbackHandler == null)
            throw new LoginException("Error: no CallbackHandler available " +
                        "to garner authentication information from the user");

        Callback[] callbacks = new Callback[2];
        callbacks[0] = new NameCallback("user name: ");
        callbacks[1] = new PasswordCallback("password: ", false);

        try {
            callbackHandler.handle(callbacks);
            username = ((NameCallback)callbacks[0]).getName();
            char[] tmpPassword = ((PasswordCallback)callbacks[1]).getPassword();
            if (tmpPassword == null) {
                // treat a NULL password as an empty password
                tmpPassword = new char[0];
            }
            password = new char[tmpPassword.length];
            System.arraycopy(tmpPassword, 0,
                        password, 0, tmpPassword.length);
            ((PasswordCallback)callbacks[1]).clearPassword();

        } catch (java.io.IOException ioe) {
            throw new LoginException(ioe.toString());
        } catch (UnsupportedCallbackException uce) {
            throw new LoginException("Error: " + uce.getCallback().toString() +
                " not available to garner authentication information " +
                "from the user");
        }

        // print debugging information
        if (debug) {
            System.out.println("\t\t[SampleLoginModule] " +
                                "user entered user name: " +
                                username);
            System.out.print("\t\t[SampleLoginModule] " +
                                "user entered password: ");
            for (int i = 0; i < password.length; i++)
                System.out.print(password[i]);
            System.out.println();
        }

        // verify the username/password
        boolean usernameCorrect = false;
        boolean passwordCorrect = false;
        if (username.equals("testUser"))
            usernameCorrect = true;
        if (usernameCorrect &&
            password.length == 12 &&
            password[0] == 't' &&
            password[1] == 'e' &&
            password[2] == 's' &&
            password[3] == 't' &&
            password[4] == 'P' &&
            password[5] == 'a' &&
            password[6] == 's' &&
            password[7] == 's' &&
            password[8] == 'w' &&
            password[9] == 'o' &&
            password[10] == 'r' &&
            password[11] == 'd') {

            // authentication succeeded!!!
            passwordCorrect = true;
            if (debug)
                System.out.println("\t\t[SampleLoginModule] " +
                                "authentication succeeded");
            succeeded = true;
            return true;
        } else {

            // authentication failed -- clean out state
            if (debug)
                System.out.println("\t\t[SampleLoginModule] " +
                                "authentication failed");
            succeeded = false;
            username = null;
            for (int i = 0; i < password.length; i++)
                password[i] = ' ';
            password = null;
            if (!usernameCorrect) {
                throw new FailedLoginException("User Name Incorrect");
            } else {
                throw new FailedLoginException("Password Incorrect");
            }
        }
    }

    /**
     * This method is called if the LoginContext's
     * overall authentication succeeded
     * (the relevant REQUIRED, REQUISITE, SUFFICIENT and OPTIONAL LoginModules
     * succeeded).
     *
     * If this LoginModule's own authentication attempt
     * succeeded (checked by retrieving the private state saved by the
     * <code>login</code> method), then this method associates a
     * <code>SamplePrincipal</code>
     * with the <code>Subject</code> located in the
     * <code>LoginModule</code>.  If this LoginModule's own
     * authentication attempted failed, then this method removes
     * any state that was originally saved.
     *
     * @exception LoginException if the commit fails.
     *
     * @return true if this LoginModule's own login and commit
     *          attempts succeeded, or false otherwise.
     */
    public boolean commit() throws LoginException {
        if (succeeded == false) {
            return false;
        } else {
            // add a Principal (authenticated identity)
            // to the Subject

            // assume the user we authenticated is the SamplePrincipal
            userPrincipal = new SamplePrincipal(username);
            if (!subject.getPrincipals().contains(userPrincipal))
                subject.getPrincipals().add(userPrincipal);

            if (debug) {
                System.out.println("\t\t[SampleLoginModule] " +
                                "added SamplePrincipal to Subject");
            }

            // in any case, clean out state
            username = null;
            for (int i = 0; i < password.length; i++)
                password[i] = ' ';
            password = null;

            commitSucceeded = true;
            return true;
        }
    }

    /**
     * This method is called if the LoginContext's
     * overall authentication failed.
     * (the relevant REQUIRED, REQUISITE, SUFFICIENT and OPTIONAL LoginModules
     * did not succeed).
     *
     * If this LoginModule's own authentication attempt
     * succeeded (checked by retrieving the private state saved by the
     * <code>login</code> and <code>commit</code> methods),
     * then this method cleans up any state that was originally saved.
     *
     * @exception LoginException if the abort fails.
     *
     * @return false if this LoginModule's own login and/or commit attempts
     *          failed, and true otherwise.
     */
    public boolean abort() throws LoginException {
        if (succeeded == false) {
            return false;
        } else if (succeeded == true && commitSucceeded == false) {
            // login succeeded but overall authentication failed
            succeeded = false;
            username = null;
            if (password != null) {
                for (int i = 0; i < password.length; i++)
                    password[i] = ' ';
                password = null;
            }
            userPrincipal = null;
        } else {
            // overall authentication succeeded and commit succeeded,
            // but someone else's commit failed
            logout();
        }
        return true;
    }

    /**
     * Logout the user.
     *
     * This method removes the <code>SamplePrincipal</code>
     * that was added by the <code>commit</code> method.
     *
     * @exception LoginException if the logout fails.
     *
     * @return true in all cases since this <code>LoginModule</code>
     *          should not be ignored.
     */
    public boolean logout() throws LoginException {

        subject.getPrincipals().remove(userPrincipal);
        succeeded = false;
        succeeded = commitSucceeded;
        username = null;
        if (password != null) {
            for (int i = 0; i < password.length; i++)
                password[i] = ' ';
            password = null;
        }
        userPrincipal = null;
        return true;
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-3EA5533B-1284-481E-A35F-C82B17837F2E">
SamplePrincipal.java

``` {.oac_no_warn dir="ltr"}
package sample.principal;

import java.security.Principal;

/**
 * This class implements the <code>Principal</code> interface
 * and represents a Sample user.
 *
 * Principals such as this <code>SamplePrincipal</code>
 * may be associated with a particular <code>Subject</code>
 * to augment that <code>Subject</code> with an additional
 * identity.  Refer to the <code>Subject</code> class for more information
 * on how to achieve this.  Authorization decisions can then be based upon
 * the Principals associated with a <code>Subject</code>.
 *
 * @see java.security.Principal
 * @see javax.security.auth.Subject
 */
public class SamplePrincipal implements Principal, java.io.Serializable {

    /**
     * @serial
     */
    private String name;

    /**
     * Create a SamplePrincipal with a Sample username.
     *
     * @param name the Sample username for this user.
     *
     * @exception NullPointerException if the <code>name</code>
     *                  is <code>null</code>.
     */
    public SamplePrincipal(String name) {
        if (name == null)
            throw new NullPointerException("illegal null input");

        this.name = name;
    }

    /**
     * Return the Sample username for this <code>SamplePrincipal</code>.
     *
     * @return the Sample username for this <code>SamplePrincipal</code>
     */
    public String getName() {
        return name;
    }

    /**
     * Return a string representation of this <code>SamplePrincipal</code>.
     *
     * @return a string representation of this <code>SamplePrincipal</code>.
     */
    public String toString() {
        return("SamplePrincipal:  " + name);
    }

    /**
     * Compares the specified Object with this <code>SamplePrincipal</code>
     * for equality.  Returns true if the given object is also a
     * <code>SamplePrincipal</code> and the two SamplePrincipals
     * have the same username.
     *
     * @param o Object to be compared for equality with this
     *          <code>SamplePrincipal</code>.
     *
     * @return true if the specified Object is equal equal to this
     *          <code>SamplePrincipal</code>.
     */
    public boolean equals(Object o) {
        if (o == null)
            return false;

        if (this == o)
            return true;

        if (!(o instanceof SamplePrincipal))
            return false;
        SamplePrincipal that = (SamplePrincipal)o;

        if (this.getName().equals(that.getName()))
            return true;
        return false;
    }

    /**
     * Return a hash code for this <code>SamplePrincipal</code>.
     *
     * @return a hash code for this <code>SamplePrincipal</code>.
     */
    public int hashCode() {
        return name.hashCode();
    }
}
```

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-987700C5-AE03-4EB1-B16A-66A1404B9604}

The Login Configuration {#JSSEC-GUID-987700C5-AE03-4EB1-B16A-66A1404B9604 .sect2}
-----------------------

<div>
JAAS authentication is performed in a pluggable fashion, so applications
can remain independent from underlying authentication technologies. A
system administrator determines the authentication technologies, or
<span class="apiname">LoginModules</span>, to be used for each
application and configures them in a login
<span class="apiname">Configuration</span>. The source of the
configuration information (for example, a file or a database) is up to
the current
[<span class="apiname">javax.security.auth.login.Configuration</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
implementation. The default `Configuration`{.codeph} implementation from
Oracle reads configuration information from configuration files, as
described in the
[<span class="apiname">ConfigFile</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/login/ConfigFile.html)
class.

See [Appendix B: JAAS Login Configuration
File](appendix-b-jaas-login-configuration-file.htm#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)
for information as to what a login configuration file is, what it
contains, and how to specify which login configuration file should be
used.

</div>
<div class="sect3">
[]{#GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F}

### The Login Configuration File for the JAAS Authentication Tutorial {#JSSEC-GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F .sect3}

<div>
As noted, the login configuration file we use for this tutorial,
`sample_jass.config`, contains just one entry, which is

``` {.oac_no_warn dir="ltr"}
Sample {
  sample.module.SampleLoginModule required debug=true;
};
```

This entry is named \"Sample\" and that is the name that our tutorial
application, `SampleAcn`{.codeph}, uses to refer to this entry. The
entry specifies that the <span class="apiname">LoginModule</span> to be
used to do the user authentication is the `SampleLoginModule`{.codeph}
in the `sample.module`{.codeph} package and that this
`SampleLoginModule`{.codeph} is required to \"succeed\" in order for
authentication to be considered successful. The
`SampleLoginModule`{.codeph} succeeds only if the name and password
supplied by the user are the one it expects (\"testUser\" and
\"testPassword\", respectively).

The `SampleLoginModule`{.codeph} also defines a \"debug\" option that
can be set to `true`{.codeph} as shown. If this option is set to
`true,`{.codeph} `SampleLoginModule`{.codeph} outputs extra information
about the progress of authentication. A
<span class="apiname">LoginModule</span> can define as many options as
it wants. The <span class="apiname">LoginModule</span> documentation
should specify the possible option names and values you can set in your
configuration file.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-743703A2-7EC1-4391-A816-4A883FB6A017}

Running the Code {#JSSEC-GUID-743703A2-7EC1-4391-A816-4A883FB6A017 .sect2}
----------------

<div>
To execute our JAAS authentication tutorial code, all you have to do is

1.  Place the following file into a directory:

    -   <span class="apiname">sample\_jass.config</span> login
        configuration file (see [The Login Configuration File for the
        JAAS Authentication
        Tutorial](jaas-authentication-tutorial.htm#GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F))

2.  Create a subdirectory named <span class="apiname">sample</span> of
    that top-level directory, and place the following into it (note the
    `SampleAcn`{.codeph} and
    <span class="apiname">MyCallbackHandler</span> classes, both in
    `SampleAcn.java`{.codeph}, are in a package named
    `sample`{.codeph}):

    -   [`SampleAcn.java`](jaas-authentication-tutorial.htm#GUID-E007D5F4-3FA5-417A-B85F-E669839F0101__GUID-1270A0AC-EA51-4A47-B9BC-BDB42F96F5FE)
        application source file

3.  Create a subdirectory of the `sample` directory and name it
    `module`. Place the following into it (note the `SampleLoginModule`
    class is in a package named `sample.module`{.codeph}):

    -   [`SampleLoginModule.java`](jaas-authentication-tutorial.htm#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-F9A208EC-3247-4320-8158-82B0E84C6A04)
        source file

4.  Create another subdirectory of the `sample` directory and name it
    `principal`. Place the following into it (note the
    `SamplePrincipal`{.codeph} class is in a package named
    `sample.principal`{.codeph}):
    -   [`SamplePrincipal.java`](jaas-authentication-tutorial.htm#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-3EA5533B-1284-481E-A35F-C82B17837F2E)
        source file
5.  While in the top-level directory, compile `SampleAcn.java`{.codeph},
    `SampleLoginModule.java`{.codeph}, and
    `SamplePrincipal.java`{.codeph}:

    `javac sample/SampleAcn.java sample/module/SampleLoginModule.java sample/principal/SamplePrincipal.java`{.codeph}

    (Type all that on one line.)

6.  Execute the `SampleAcn`{.codeph} application, specifying
    -   by
        `-Djava.security.auth.login.config==sample_jaas.config`{.codeph}
        that the login configuration file to be used is
        `sample_jaas.config`{.codeph}.

The full command is below.

``` {.oac_no_warn dir="ltr"}
java -Djava.security.auth.login.config==sample_jaas.config sample.SampleAcn
```

You will be prompted for your user name and password, and the
`SampleLoginModule`{.codeph} specified in the login configuration file
will check to ensure these are correct. The `SampleLoginModule`{.codeph}
expects `testUser`{.codeph} for the user name and
`testPassword`{.codeph} for the password.

You will see some messages output by `SampleLoginModule`{.codeph} as a
result of the `debug`{.codeph} option being set to `true`{.codeph} in
the login configuration file. Then, if your login is successful, you
will see the following message output by
<span class="apiname">SampleAcn</span>:

``` {.oac_no_warn dir="ltr"}
Authentication succeeded!
```

If the login is not successful (for example, if you misspell the
password), you will see

``` {.oac_no_warn dir="ltr"}
Authentication failed:
```

followed by a reason for the failure. For example, if you mistype the
password, you may see a message like the following:

``` {.oac_no_warn dir="ltr"}
Authentication failed:
  Password Incorrect
```

<span class="apiname">SampleAcn</span> gives you three chances to
successfully log in.

</div>
</div>
<div class="sect2">
[]{#GUID-44F2BF3A-F51D-4F21-8F40-96CB1120396D}

Running the Code with a Security Manager {#JSSEC-GUID-44F2BF3A-F51D-4F21-8F40-96CB1120396D .sect2}
----------------------------------------

<div>
When a Java program is run with a security manager installed, the
program is not allowed to access resources or otherwise perform
security-sensitive operations unless it is explicitly granted permission
to do so by the security policy in effect. (See [Permissions in the
JDK](permissions-jdk1.htm#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.").)
The permission must be granted by an entry in a policy file (see
[Default Policy Implementation and Policy File
Syntax](permissions-jdk1.htm#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D).)

Most browsers install a security manager, so
<span class="variable">applets</span> typically run under the scrutiny
of a security manager. <span class="variable">Applications</span>, on
the other hand, do not, since a security manager is not automatically
installed when an application is running. Thus an application, like our
`SampleAcn`{.codeph} application, by default has full access to
resources.

<span class="bold">To run an application with a security manager</span>,
simply invoke the interpreter with a `-Djava.security.manager`{.codeph}
argument included on the command line.

If you try invoking `SampleAcn`{.codeph} with a security manager but
without specifying any policy file, you will get the following (unless
you have a default policy setup elsewhere that grants the required
permissions or grants `AllPermission`{.codeph}):

``` {.oac_no_warn dir="ltr"}
% java -Djava.security.manager \
 -Djava.security.auth.login.config==sample_jaas.config sample.SampleAcn
Exception in thread "main" java.security.AccessControlException:
  access denied (
  javax.security.auth.AuthPermission createLoginContext.Sample)
```

As you can see, you get an
<span class="apiname">AccessControlException</span>, because we haven\'t
created and used a policy file granting our code the permission that is
required in order to be allowed to create a
<span class="apiname">LoginContext</span>.

Here are the complete steps required in order to be able to run our
`SampleAcn`{.codeph} application with a security manager installed. You
can skip the first five steps if you have already done them, as
described in [Running the
Code](jaas-authentication-tutorial.htm#GUID-743703A2-7EC1-4391-A816-4A883FB6A017).

1.  Place the following file into a directory:

    -   `sample_jass.config` login configuration file (see [The Login
        Configuration File for the JAAS Authentication
        Tutorial](jaas-authentication-tutorial.htm#GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F))

2.  Create a subdirectory named <span class="apiname">sample</span> of
    that top-level directory, and place the following into it (note the
    `SampleAcn`{.codeph} and
    <span class="apiname">MyCallbackHandler</span> classes, both in
    `SampleAcn.java`{.codeph}, are in a package named
    `sample`{.codeph}):

    -   [`SampleAcn.java`](jaas-authentication-tutorial.htm#GUID-E007D5F4-3FA5-417A-B85F-E669839F0101__GUID-1270A0AC-EA51-4A47-B9BC-BDB42F96F5FE)
        application source file

3.  Create a subdirectory of the `sample` directory and name it
    `module`. Place the following into it (note the `SampleLoginModule`
    class is in a package named `sample.module`{.codeph}):

    -   [`SampleLoginModule.java`](jaas-authentication-tutorial.htm#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-F9A208EC-3247-4320-8158-82B0E84C6A04)
        source file

4.  Create another subdirectory of the `sample` directory and name it
    `principal`. Place the following into it (note the
    `SamplePrincipal`{.codeph} class is in a package named
    `sample.principal`{.codeph}):

    -   [`SamplePrincipal.java`](jaas-authentication-tutorial.htm#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075__GUID-3EA5533B-1284-481E-A35F-C82B17837F2E)
        source file

5.  While in the top-level directory, compile `SampleAcn.java`{.codeph},
    `SampleLoginModule.java`{.codeph}, and
    `SamplePrincipal.java`{.codeph}:

    `javac sample/SampleAcn.java sample/module/SampleLoginModule.java sample/principal/SamplePrincipal.java`{.codeph}

    (Type all that on one line.)

6.  Create a JAR file containing `SampleAcn.class`{.codeph} and
    `MyCallbackHandler.class`{.codeph}:

    `jar -cvf SampleAcn.jar sample/SampleAcn.class sample/MyCallbackHandler.class`{.codeph}

    (Type all that on one line.) This command creates a JAR file,
    `SampleAcn.jar`{.codeph}, and places the `SampleAcn.class`{.codeph}
    and `MyCallbackHandler.class`{.codeph} files inside it.

7.  Create a JAR file containing `SampleLoginModule.class`{.codeph} and
    `SamplePrincipal.class`{.codeph}:

    `jar -cvf SampleLM.jar sample/module/SampleLoginModule.class sample/principal/SamplePrincipal.class`{.codeph}

8.  Create a policy file granting the required permissions.

    The permission that is needed by code attempting to instantiate a
    <span class="apiname">LoginContext</span> is a
    `javax.security.auth.AuthPermission`{.codeph} with target
    `createLoginContext.<entry name>`{.codeph}. Here,
    `<entry name>`{.codeph} refers to the name of the login
    configuration file entry that the application references in its
    instantiation of <span class="apiname">LoginContext</span>. The name
    used by our `SampleAcn`{.codeph} application\'s
    <span class="apiname">LoginContext</span> instantiation is
    `Sample`{.codeph}, as you can see in the code:

    ``` {.oac_no_warn dir="ltr"}
    LoginContext lc =
        new LoginContext("Sample",
              new MyCallbackHandler());
    ```

    Thus, the permission that needs to be granted to
    `SampleAcn.jar`{.codeph} is

    ``` {.oac_no_warn dir="ltr"}
    permission javax.security.auth.AuthPermission
      "createLoginContext.Sample";
    ```

    The `SampleLM.jar`{.codeph} file also needs to be granted a
    permission. The documentation for a
    <span class="apiname">LoginModule</span> should tell you what
    permissions it needs to be granted. In the case of
    `SampleLoginModule`{.codeph}, it needs a
    `javax.security.auth.AuthPermission`{.codeph} with target
    `modifyPrincipals`{.codeph} in order to populate a
    <span class="apiname">Subject</span> with a
    <span class="apiname">Principal</span>:

    ``` {.oac_no_warn dir="ltr"}
    permission javax.security.auth.AuthPermission
      "modifyPrincipals";
    ```

    Copy the policy file
    [`sampleacn.policy`](jaas-authentication-tutorial.htm#GUID-44F2BF3A-F51D-4F21-8F40-96CB1120396D__SAMPLEACN.POLICY-2FEDE143)
    to the same directory as that in which you stored
    `SampleAcn.java`{.codeph}, etc. The policy file contains the
    following `grant`{.codeph} statement to grant
    `SampleAcn.jar`{.codeph} (in the current directory) its required
    permission:

    ``` {.oac_no_warn dir="ltr"}
    grant codebase "file:./SampleAcn.jar" {
       permission javax.security.auth.AuthPermission "createLoginContext.Sample";
    };
    ```

    The policy file also contains the following `grant`{.codeph}
    statement to grant `SampleLM.jar`{.codeph} (also in the current
    directory) its required permission:

    ``` {.oac_no_warn dir="ltr"}
    grant codebase "file:./SampleLM.jar" {
       permission javax.security.auth.AuthPermission "modifyPrincipals";
    };
    ```

    Note: Policy files and the structure of entries within them are
    described in [Default Policy Implementation and Policy File
    Syntax](permissions-jdk1.htm#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D).
    Permissions are described in [Permissions in the
    JDK](permissions-jdk1.htm#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.").

    Execute the `SampleAcn`{.codeph} application, specifying

    a.  by an appropriate `-classpath`{.codeph} clause that classes
        should be searched for in the `SampleAcn.jar`{.codeph} and
        `SampleLM.jar`{.codeph} JAR files,
    b.  by `-Djava.security.manager`{.codeph} that a security manager
        should be installed,
    c.  by `-Djava.security.policy==sampleacn.policy`{.codeph} that the
        policy file to be used is `sampleacn.policy`{.codeph}, and
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
    java -classpath SampleAcn.jar;SampleLM.jar
     -Djava.security.manager
     -Djava.security.policy==sampleacn.policy
     -Djava.security.auth.login.config==sample_jaas.config
     sample.SampleAcn
    ```

    Here is the full command for Solaris, Linux, and macOS systems:

    ``` {.oac_no_warn dir="ltr"}
    java -classpath SampleAcn.jar:SampleLM.jar
     -Djava.security.manager
     -Djava.security.policy==sampleacn.policy
     -Djava.security.auth.login.config==sample_jaas.config
     sample.SampleAcn
    ```

    Type all that on one line. Multiple lines are used here for
    legibility. If the command is too long for your system, you may need
    to place it in a `.bat`{.codeph} file (for Microsoft Windows) or a
    `.sh`{.codeph} file (for Solaris, Linux, and macOS) and then run
    that file to execute the command.

    Since the specified policy file contains an entry granting the code
    the required permissions, execution should proceed without any
    exceptions indicating a required permission was not granted. You
    will be prompted for a user name and password (use
    `testUser`{.codeph} and `testPassword`{.codeph}), and the
    `SampleLoginModule`{.codeph} specified in the login configuration
    file will check the name and password. If your login is successful,
    you will see the message `Authentication succeeded!`{.codeph} and if
    not, you will see `Authentication failed:`{.codeph} followed by a
    reason for the failure.

<div class="section" id="GUID-44F2BF3A-F51D-4F21-8F40-96CB1120396D__SAMPLEACN.POLICY-2FEDE143">
sampleacn.policy

``` {.oac_no_warn dir="ltr"}
/* grant the sample LoginModule permissions */
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
</div>
<!-- class="ind" --><!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   -- --------------- |
| -------------------- | [ | -------------------- |
| -------------------  | O | -------------------- |
| -------------------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| ------ --            | l | dcommon/gifs/toc.gif |
|         [![Previous] | e | )\                   |
| (../../dcommon/gifs/ | L |             <span cl |
| leftnav.gif)\        | o | ass="icon">Contents< |
|             [![Next] | g | /span>](toc.htm)     |
| (../../dcommon/gifs/ | o |   -- --------------- |
| rightnav.gif)\       | ] | -------------------- |
|                      | ( | -------------------- |
|    <span class="icon | . | ---                  |
| ">Previous</span>](j | . |                      |
| aas-tutorials.htm)   | / |                      |
|  <span class="icon"> | . |                      |
| Next</span>](jaas-au | . |                      |
| thorization-tutorial | / |                      |
| .htm)                | d |                      |
|   ------------------ | c |                      |
| -------------------- | o |                      |
| -------------------  | m |                      |
| -------------------- | m |                      |
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
