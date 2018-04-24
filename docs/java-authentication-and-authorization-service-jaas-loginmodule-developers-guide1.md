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

  ---------------------------------------------------------------------- ----------------------------------------------------------------------------------- --
              [![Previous](../../dcommon/gifs/leftnav.gif)\                                  [![Next](../../dcommon/gifs/rightnav.gif)\                      
   <span class="icon">Previous</span>](jaas-authorization-tutorial.htm)   <span class="icon">Next</span>](java-generic-security-services-java-gss-api1.htm)  
  ---------------------------------------------------------------------- ----------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A}<!-- End Header -->

Java Authentication and Authorization Service (JAAS): LoginModule Developer\'s Guide {#JSSEC-GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A .sect1}
====================================================================================

<div>
JAAS provides subject-based authorization on authenticated identities.
This document focuses on the authentication aspect of JAAS, specifically
the
[<span class="apiname">LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html)
interface.

<div class="section">
Who Should Read This Document

This document is intended for experienced programmers who require the
ability to write a
[<span class="apiname">LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html)
implementing an authentication technology.

</div>
<!-- class="section" -->

<div class="section">
Related Documentation

This document assumes you have already read the following:

-   [Java Authentication and Authorization Service (JAAS) Reference
    Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html)

It also discusses various classes and interfaces in the JAAS API. See
the Javadoc API documentation for the JAAS API specification for more
detailed information:

-   [<span class="apiname">javax.security.auth
    </span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/package-summary.html)
-   [<span class="apiname">javax.security.auth.callback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/package-summary.html)
-   [<span class="apiname">javax.security.auth.kerberos</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/kerberos/package-summary.html)
-   [<span class="apiname">javax.security.auth.login
    </span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/package-summary.html)
-   [<span class="apiname">javax.security.auth.spi
    </span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/package-summary.html)
-   [<span class="apiname">javax.security.auth.x500
    </span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/x500/package-summary.html)

The following packages contain supported
<span class="apiname">LoginModule</span> examples:

-   [<span class="apiname">com.sun.security.auth</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/package-summary.html)
-   [<span class="apiname">com.sun.security.auth.callback</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/callback/package-summary.html)
-   [<span class="apiname">com.sun.security.auth.login</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/login/package-summary.html)
-   [<span class="apiname">com.sun.security.auth.module</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/package-summary.html)

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
    Authentication](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/AcnOnly.html)
-   [JAAS
    Authorization](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/AcnAndAzn.html)

These two tutorials are a part of [Introduction to JAAS and Java GSS-API
Tutorials](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/index.html)
that utilize Kerberos as the underlying technology for authentication
and secure communication.

</div>
<!-- class="section" -->

</div>
<div class="sect2">
[]{#GUID-3F7CF22D-A207-49EE-B1CC-575FBF3789DE}

Introduction to LoginModule {#JSSEC-GUID-3F7CF22D-A207-49EE-B1CC-575FBF3789DE .sect2}
---------------------------

<div>
Authentication technology providers must implement the
[<span class="apiname">LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html)
interface. `LoginModule`{.codeph}s are plugged in under applications to
provide a particular type of authentication.

While applications write to the
[<span class="apiname">LoginContext</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/LoginContext.html)
Application Programming Interface (API), authentication technology
providers implement the `LoginModule`{.codeph} interface. A
[<span class="apiname">Configuration</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
specifies the `LoginModule`{.codeph}(s) to be used with a particular
login application. Different `LoginModule`{.codeph}s can be plugged in
under the application without requiring any modifications to the
application itself.

The `LoginContext`{.codeph} is responsible for reading the
`Configuration`{.codeph} and instantiating the specified
`LoginModule`{.codeph}s. Each `LoginModule`{.codeph} is initialized with
a
[<span class="apiname">Subject</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/Subject.html),
a
[<span class="apiname">CallbackHandler</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/CallbackHandler.html),
shared `LoginModule`{.codeph} state, and `LoginModule`{.codeph}-specific
options.

The <span class="bold">`Subject`{.codeph}</span> represents the user or
service currently being authenticated and is updated by a
`LoginModule`{.codeph} with relevant
[<span class="apiname">Principal</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Principal.html)s
and credentials if authentication succeeds. `LoginModule`{.codeph}s use
the <span class="bold">`CallbackHandler`{.codeph}</span> to communicate
with users (to prompt for user names and passwords, for example), as
described in the login method description. Note that the
`CallbackHandler`{.codeph} may be null. A `LoginModule`{.codeph} that
requires a `CallbackHandler`{.codeph} to authenticate the
`Subject`{.codeph} may throw a
[<span class="apiname">LoginException</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/LoginException.html)
if it was initialized with a `null`{.codeph} `CallbackHandler`{.codeph}.
`LoginModule`{.codeph}s optionally use the <span class="bold">shared
state</span> to share information or data among themselves.

The <span class="bold">`LoginModule`{.codeph}-specific options</span>
represent the options configured for this `LoginModule`{.codeph} in the
login `Configuration`{.codeph}. The options are defined by the
`LoginModule`{.codeph} itself and control the behavior within it. For
example, a `LoginModule`{.codeph} may define options to support
debugging/testing capabilities. Options are defined using a key-value
syntax, such as <span class="variable">debug=true</span>. The
`LoginModule`{.codeph} stores the options as a `Map`{.codeph} so that
the values may be retrieved using the key. Note that there is no limit
to the number of options a `LoginModule`{.codeph} chooses to define.

The calling application sees the authentication process as a single
operation invoked via a call to the `LoginContext`{.codeph}\'s
`login`{.codeph} method. However, the authentication process within each
`LoginModule`{.codeph} proceeds in two distinct phases. In the first
phase of authentication, the `LoginContext`{.codeph}\'s `login`{.codeph}
method invokes the `login`{.codeph} method of each
`LoginModule`{.codeph} specified in the `Configuration`{.codeph}. The
`login`{.codeph} method for a `LoginModule`{.codeph} performs the actual
authentication (prompting for and verifying a password for example) and
saves its authentication status as private state information. Once
finished, the `LoginModule`{.codeph}\'s `login`{.codeph} method returns
`true`{.codeph} (if it succeeded) or `false`{.codeph} (if it should be
ignored), or it throws a `LoginException`{.codeph} to specify a failure.
In the failure case, the `LoginModule`{.codeph} must not retry the
authentication or introduce delays. The responsibility of such tasks
belongs to the application. If the application attempts to retry the
authentication, each `LoginModule`{.codeph}\'s `login`{.codeph} method
will be called again.

In the second phase, if the `LoginContext`{.codeph}\'s overall
authentication succeeded (calls to the relevant
<span class="variable">required</span>,
<span class="variable">requisite</span>,
<span class="variable">sufficient</span> and
<span class="variable">optional</span> `LoginModule`{.codeph}s\'
`login`{.codeph} methods succeeded), then the `commit`{.codeph} method
for each `LoginModule`{.codeph} gets invoked. (For an explanation of the
`LoginModule`{.codeph} flags <span class="variable">required</span>,
<span class="variable">requisite</span>,
<span class="variable">sufficient</span> and
<span class="variable">optional</span>, please consult the
[<span class="apiname">Configuration</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
documentation and [Appendix B: Example Login
Configurations](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html#AppendixB)
in the JAAS Reference Guide.) The `commit`{.codeph} method for a
`LoginModule`{.codeph} checks its privately saved state to see if its
own authentication succeeded. If the overall `LoginContext`{.codeph}
authentication succeeded and the `LoginModule`{.codeph}\'s own
authentication succeeded, then the `commit`{.codeph} method associates
the relevant `Principal`{.codeph}s (authenticated identities) and
credentials (authentication data such as cryptographic keys) with the
`Subject`{.codeph}.

If the `LoginContext`{.codeph}\'s overall authentication failed (the
relevant REQUIRED, REQUISITE, SUFFICIENT and OPTIONAL
`LoginModule`{.codeph}s\' `login`{.codeph} methods did not succeed),
then the `abort`{.codeph} method for each `LoginModule`{.codeph} gets
invoked. In this case, the `LoginModule`{.codeph} removes/destroys any
authentication state originally saved.

Logging out a `Subject`{.codeph} involves only one phase. The
`LoginContext`{.codeph} invokes the `LoginModule`{.codeph}\'s
`logout`{.codeph} method. The `logout`{.codeph} method for the
`LoginModule`{.codeph} then performs the logout procedures, such as
removing `Principal`{.codeph}s or credentials from the
`Subject`{.codeph}, or logging session information.

</div>
</div>
<div class="sect2">
[]{#GUID-EE1C4BBE-289F-4419-A233-43F2D897765B}

Steps to Implement a LoginModule {#JSSEC-GUID-EE1C4BBE-289F-4419-A233-43F2D897765B .sect2}
--------------------------------

<div>
The following are the steps required to implement and test a
`LoginModule`{.codeph}:

</div>
<div class="sect3">
[]{#GUID-A4140569-4124-4AE7-81CC-145537BE0F42}

### Step 1: Understand the Authentication Technology {#JSSEC-GUID-A4140569-4124-4AE7-81CC-145537BE0F42 .sect3}

<div>
First, understand the authentication technology to be implemented by
your new `LoginModule`{.codeph} provider and determine its requirements.

1.  <span>Determine whether or not your `LoginModule`{.codeph} will
    require some form of user interaction (retrieving a user name and
    password, for example). If so, you will need to become familiar with
    the
    [<span class="apiname">CallbackHandler</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/CallbackHandler.html)
    interface and the
    [<span class="apiname">javax.security.auth.callback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/package-summary.html)
    package.</span>

    <div>
    In that package you will find several possible `Callback`{.codeph}
    implementations to use. (Alternatively, you can create your own
    `Callback`{.codeph} implementations.) The `LoginModule`{.codeph}
    will invoke the `CallbackHandler`{.codeph} specified by the
    application itself and passed to the `LoginModule`{.codeph}\'s
    `initialize`{.codeph} method. The `LoginModule`{.codeph} passes the
    `CallbackHandler`{.codeph} an array of appropriate
    `Callback`{.codeph}s. See [LoginModule.login
    Method](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__LOGINMODULE.LOGINMETHOD-21144491)
    in [Step 3: Implement the Abstract LoginModule
    Methods](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F "The LoginModule interface specifies five abstract methods that require implementations.").

    <div class="p">
    <div class="infoboxnote" id="GUID-A4140569-4124-4AE7-81CC-145537BE0F42__GUID-E00E32FE-7328-4E56-B91F-04095BA3A9D6">
    Note:

    It is possible for `LoginModule`{.codeph} implementations not to
    have any end-user interactions. Such `LoginModule`{.codeph}s would
    not need to access the `callback`{.codeph} package.

    </div>
    </div>
    </div>
2.  <span>Determine what configuration options you want to make
    available to the user, who specifies configuration information in
    whatever form the current Configuration implementation expects (for
    example, in files). For each option, decide the option name and
    possible values.</span>
    <div>
    For example, if a `LoginModule`{.codeph} may be configured to
    consult a particular authentication server host, decide on the
    option\'s key name (\"auth\_server\", for example), as well as the
    possible server hostnames valid for that option
    (\"server\_one.example.com\" and \"server\_two.example.com\", for
    example).
    </div>

</div>
</div>
<div class="sect3">
[]{#GUID-A6BAE987-54F4-4634-9D03-7EB986C7F484}

### Step 2: Name the LoginModule Implementation {#JSSEC-GUID-A6BAE987-54F4-4634-9D03-7EB986C7F484 .sect3}

<div>
Decide on the proper package and class name for your
`LoginModule`{.codeph}.

<div class="example" id="GUID-A6BAE987-54F4-4634-9D03-7EB986C7F484__GUID-61466AE4-79E1-4B1F-9BFA-6DD64DEB781C">
For example, a `LoginModule`{.codeph} developed by IBM might be called
`com.ibm.auth.Module`{.codeph} where `com.ibm.auth`{.codeph} is the
package name and `Module`{.codeph} is the name of the
`LoginModule`{.codeph} class implementation.

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect3">
[]{#GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F}

### Step 3: Implement the Abstract LoginModule Methods {#JSSEC-GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F .sect3}

<div>
The `LoginModule`{.codeph} interface specifies five abstract methods
that require implementations.

<div class="section">
-   [<span class="apiname">initialize</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html#initialize-javax.security.auth.Subject-javax.security.auth.callback.CallbackHandler-java.util.Map-java.util.Map-)

-   [<span class="apiname">login</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html#login--)

-   [<span class="apiname">commit</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html#commit--)

-   [<span class="apiname">abort</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html#abort--)

-   [<span class="apiname">logout</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/spi/LoginModule.html#logout--)

In addition to these methods, a <span class="apiname">LoginModule</span>
implementation must provide a public constructor with no arguments. This
allows for its proper instantiation by a
<span class="apiname">LoginContext</span>. Note that if no constructor
is provided in your <span class="apiname">LoginModule</span>
implementation, a default no-argument constructor is automatically
inherited from the <span class="apiname">Object</span> class.

</div>
<!-- class="section" -->

<div class="section" id="GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__LOGINMODULE.INITIALIZEMETHOD-2114401D">
LoginModule.initialize Method

``` {.oac_no_warn dir="ltr"}
    public void initialize(
        Subject subject,
        CallbackHandler handler,
        Map<java.lang.String, ?> sharedState,
        Map<java.lang.String, ?> options);
```

The `initialize`{.codeph} method is called to initialize the
`LoginModule`{.codeph} with the relevant authentication and state
information.

This method is called by a `LoginContext`{.codeph} immediately after
this `LoginModule`{.codeph} has been instantiated, and prior to any
calls to its other public methods. The method implementation should
store away the provided arguments for future use.

The `initialize`{.codeph} method may additionally peruse the provided
<span class="variable">sharedState</span> to determine what additional
authentication state it was provided by other `LoginModule`{.codeph}s,
and may also traverse through the provided
<span class="variable">options</span> to determine what configuration
options were specified to affect the `LoginModule`{.codeph}\'s behavior.
It may save option values in variables for future use.

Below is a list of options commonly supported by
<span class="apiname">LoginModule</span>s. Note that the following is
simply a guideline. Modules are free to support a subset (or none) of
the following options.

-   `tryFirstPass`{.codeph} - If `true`{.codeph}, the first
    <span class="apiname">LoginModule</span> in the stack saves the
    password entered, and subsequent
    <span class="apiname">LoginModules</span> also try to use it. If
    authentication fails, the <span class="apiname">LoginModule</span>s
    prompt for a new password and retry the authentication.
-   `useFirstPass`{.codeph} - If `true`{.codeph}, the first
    <span class="apiname">LoginModule</span> in the stack saves the
    password entered, and subsequent
    <span class="apiname">LoginModules</span> also try to use it.
    <span class="apiname">LoginModule</span>s do not prompt for a new
    password if authentication fails (authentication simply fails).
-   `tryMappedPass`{.codeph} - If `true`{.codeph}, the first
    <span class="apiname">LoginModule</span> in the stack saves the
    password entered, and subsequent
    <span class="apiname">LoginModules</span> attempt to map it into
    their service-specific password. If authentication fails, the
    <span class="apiname">LoginModule</span>s prompt for a new password
    and retry the authentication.
-   `useMappedPass`{.codeph} - If `true`{.codeph}, the first
    <span class="apiname">LoginModule</span> in the stack saves the
    password entered, and subsequent
    <span class="apiname">LoginModules</span> attempt to map it into
    their service-specific password.
    <span class="apiname">LoginModule</span>s do not prompt for a new
    password if authentication fails (authentication simply fails).
-   `moduleBanner`{.codeph} - If `true`{.codeph}, then when invoking the
    <span class="apiname">CallbackHandler</span>, the
    <span class="apiname">LoginModule</span> provides a
    <span class="apiname">TextOutputCallback</span> as the first
    <span class="apiname">Callback</span>, which describes the
    <span class="apiname">LoginModule</span> performing the
    authentication.
-   `debug`{.codeph} - If `true`{.codeph}, instructs a
    <span class="apiname">LoginModule</span> to output debugging
    information.

The `initialize`{.codeph} method may freely ignore state or options it
does not understand, although it would be wise to log such an event if
it does occur.

Note that the `LoginContext`{.codeph} invoking this
`LoginModule`{.codeph} (and the other configured
`LoginModule`{.codeph}s, as well), all share the same references to the
provided `Subject`{.codeph} and `sharedState`{.codeph}. Modifications to
the `Subject`{.codeph} and `sharedState`{.codeph} will, therefore, be
seen by all.

</div>
<!-- class="section" -->

<div class="section" id="GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__LOGINMODULE.LOGINMETHOD-21144491">
LoginModule.login Method

``` {.oac_no_warn dir="ltr"}
    boolean login() throws LoginException;
```

The `login`{.codeph} method is called to authenticate a
`Subject`{.codeph}. This is phase 1 of authentication.

This method implementation should perform the actual authentication. For
example, it may cause prompting for a user name and password, and then
attempt to verify the password against a password database. Another
example implementation may inform the user to insert their finger into a
fingerprint reader, and then match the input fingerprint against a
fingerprint database.

If your `LoginModule`{.codeph} requires some form of user interaction
(retrieving a user name and password, for example), it should not do so
directly. That is because there are various ways of communicating with a
user, and it is desirable for `LoginModule`{.codeph}s to remain
independent of the different types of user interaction. Rather, the
`LoginModule`{.codeph}\'s `login`{.codeph} method should invoke the
`handle`{.codeph} method of the
[<span class="apiname">CallbackHandler</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/CallbackHandler.html)
interface passed to the `initialize`{.codeph} method to perform the user
interaction and set appropriate results, such as the user name and
password. The `LoginModule`{.codeph} passes the
`CallbackHandler`{.codeph} an array of appropriate `Callback`{.codeph}s,
for example a
[<span class="apiname">NameCallback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/NameCallback.html)
for the user name and a
[<span class="apiname">PasswordCallback</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/callback/PasswordCallback.html)
for the password, and the `CallbackHandler`{.codeph} performs the
requested user interaction and sets appropriate values in the
`Callback`{.codeph}s. For example, to process a `NameCallback`{.codeph},
the `CallbackHandler`{.codeph} may prompt for a name, retrieve the value
from the user, and call the `NameCallback`{.codeph}\'s
`setName`{.codeph} method to store the name.

The authentication process may also involve communication over a
network. For example, if this method implementation performs the
equivalent of a <span class="variable">kinit</span> in Kerberos, then it
would need to contact the KDC. If a password database entry itself
resides in a remote naming service, then that naming service needs to be
contacted, perhaps via the Java Naming and Directory Interface (JNDI).
Implementations might also interact with an underlying operating system.
For example, if a user has already logged into an operating system like
Solaris, Linux, macOS, or Windows, this method might simply import the
underlying operating system\'s identity information.

The `login`{.codeph} method should

1.  Determine whether or not this `LoginModule`{.codeph} should be
    ignored. One example of when it should be ignored is when a user
    attempts to authenticate under an identity irrelevant to this
    `LoginModule`{.codeph} (if a user attempts to authenticate as
    <span class="variable">root</span> using NIS, for example). If this
    `LoginModule`{.codeph} should be ignored, `login`{.codeph} should
    return `false`{.codeph}. Otherwise, it should do the following:
2.  Call the `CallbackHandler`{.codeph} `handle`{.codeph} method if user
    interaction is required.
3.  Perform the authentication.
4.  Store the authentication result (success or failure).
5.  If authentication succeeded, save any relevant state information
    that may be needed by the `commit`{.codeph} method.
6.  Return `true`{.codeph} if authentication succeeds, or throw a
    [<span class="apiname">LoginException</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/LoginException.html)
    such as
    [<span class="apiname">FailedLoginException</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/FailedLoginException.html)
    if authentication fails.

Note that the `login`{.codeph} method implementation should not
associate any new `Principal`{.codeph} or credential information with
the saved `Subject`{.codeph} object. This method merely performs the
authentication, and then stores away the authentication result and
corresponding authentication state. This result and state will later be
accessed by the `commit`{.codeph} or `abort`{.codeph} method. Note that
the result and state should typically not be saved in the
<span class="variable">sharedState</span> `Map`{.codeph}, as they are
not intended to be shared with other `LoginModule`{.codeph}s.

An example of where this method might find it useful to store state
information in the <span class="variable">sharedState</span>
`Map`{.codeph} is when `LoginModule`{.codeph}s are configured to share
passwords. In this case, the entered password would be saved as shared
state. By sharing passwords, the user only enters the password once, and
can still be authenticated to multiple `LoginModule`{.codeph}s. The
standard conventions for saving and retrieving names and passwords from
the <span class="variable">sharedState</span> `Map`{.codeph} are the
following:

-   `javax.security.auth.login.name`{.codeph} - Use this as the shared
    state map key for saving/retrieving a name. The value should be a
    <span class="apiname">String</span>.
-   `javax.security.auth.login.password`{.codeph} - Use this as the
    shared state map key for saving/retrieving a password. The value
    should be a <span class="apiname">char</span> array.

If authentication fails, the `login`{.codeph} method should not retry
the authentication. This is the responsibility of the application.
Multiple `LoginContext`{.codeph} `login`{.codeph} method calls by an
application are preferred over multiple login attempts from within
`LoginModule.login()`{.codeph}.

</div>
<!-- class="section" -->

<div class="section" id="GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__LOGINMODULE.COMMITMETHOD-21144844">
LoginModule.commit Method

``` {.oac_no_warn dir="ltr"}
    boolean commit() throws LoginException;
```

The `commit`{.codeph} method is called to commit the authentication
process. This is phase 2 of authentication when phase 1 succeeds. It is
called if the `LoginContext`{.codeph}\'s overall authentication
succeeded (that is, if the relevant REQUIRED, REQUISITE, SUFFICIENT and
OPTIONAL `LoginModule`{.codeph}s succeeded.)

This method should access the authentication result and corresponding
authentication state saved by the `login`{.codeph} method.

If the authentication result denotes that the `login`{.codeph} method
failed, then this `commit`{.codeph} method should remove/destroy any
corresponding state that was originally saved.

If the saved result instead denotes that this `LoginModule`{.codeph}\'s
`login`{.codeph} method succeeded, then the corresponding state
information should be accessed to build any relevant
`Principal`{.codeph} and credential information. Such
`Principal`{.codeph}s and credentials should then be added to the
`Subject`{.codeph} stored away by the `initialize`{.codeph} method.

After adding `Principal`{.codeph}s and credentials, dispensable state
fields should be destroyed expeditiously. Likely fields to destroy would
be user names and passwords stored during the authentication process.

The `commit`{.codeph} method should save private state indicating
whether the commit succeeded or failed.

The following chart depicts what a `LoginModule`{.codeph}\'s
`commit`{.codeph} method should return. The different boxes represent
the different situations that may occur. For example, the top-left
corner box depicts what the `commit`{.codeph} method should return if
both the previous call to `login`{.codeph} succeeded and the
`commit`{.codeph} method itself succeeded.

<div class="tblformalwide" id="GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__GUID-80D5A33A-9B15-45EA-87FD-1C17A26F795C">
Table 6-2 LoginModule.commit Method Return Values

   Login Status    COMMIT: SUCCESS   COMMIT: FAILURE
  ---------------- ----------------- -----------------
  LOGIN: SUCCESS   return TRUE       throw EXCEPTION
  LOGIN: FAILURE   return FALSE      return FALSE

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

<div class="section" id="GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__LOGINMODULE.ABORTMETHOD-21144BEF">
LoginModule.abort Method

``` {.oac_no_warn dir="ltr"}
    boolean abort() throws LoginException;
```

The `abort`{.codeph} method is called to abort the authentication
process. This is phase 2 of authentication when phase 1 fails. It is
called if the `LoginContext`{.codeph}\'s overall authentication failed.

This method first accesses this `LoginModule`{.codeph}\'s authentication
result and corresponding authentication state saved by the
`login`{.codeph} (and possibly `commit`{.codeph}) methods, and then
clears out and destroys the information. Sample state to destroy would
be user names and passwords.

If this `LoginModule`{.codeph}\'s authentication attempt failed, then
there shouldn\'t be any private state to clean up.

The following charts depict what a `LoginModule`{.codeph}\'s
`abort`{.codeph} method should return. This first chart assumes that the
previous call to `login`{.codeph} succeeded. For instance, the
`abort`{.codeph} method should return TRUE if both the previous call to
`login`{.codeph} and `commit`{.codeph} succeeded, and the
`abort`{.codeph} method itself also succeeded.

<div class="tblformalwide" id="GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__GUID-BBDD2DC0-2F02-45A3-86D5-05E37240DC3A">
Table 6-3 LoginModule.abort Method Return Values: Login Succeeded

   Login Status     ABORT: SUCCESS   ABORT: FAILURE
  ----------------- ---------------- -----------------
  COMMIT: SUCCESS   return TRUE      throw EXCEPTION
  COMMIT: FAILURE   return TRUE      throw EXCEPTION

</div>
<!-- class="inftblhruleinformal" -->

The second chart depicts what a
<span class="apiname">LoginModule</span>\'s abort method should return,
assuming that the previous call to login failed. For instance, the
<span class="apiname">abort</span> method should return FALSE if the
previous call to <span class="apiname">login</span> failed, the previous
call to <span class="apiname">commit</span> succeeded, and the
<span class="apiname">abort</span> method itself also succeeded.

</div>
<!-- class="section" -->

<div class="tblformalwide" id="GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__LOGINMODULE.ABORTMETHODRETURNVALUES-2119026E">
Table 6-4 LoginModule.abort Method Return Values: Login Failed

   Login Status     ABORT: SUCCESS   ABORT: FAILURE
  ----------------- ---------------- ----------------
  COMMIT: SUCCESS   return FALSE     return FALSE
  COMMIT: FAILURE   return FALSE     return FALSE

</div>
<!-- class="inftblhruleinformal" -->

<div class="section" id="GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F__LOGINMODULE.LOGOUTMETHOD-21144F6A">
LoginModule.logout Method

``` {.oac_no_warn dir="ltr"}
    boolean logout() throws LoginException;
```

The `logout`{.codeph} method is called to log out a `Subject`{.codeph}.

This method removes `Principal`{.codeph}s, and removes/destroys
credentials associated with the `Subject`{.codeph} during the
`commit`{.codeph} operation. This method should not touch those
`Principal`{.codeph}s or credentials previously existing in the
`Subject`{.codeph}, or those added by other `LoginModule`{.codeph}s.

If the `Subject`{.codeph} has been marked
<span class="variable">read-only</span> (the `Subject`{.codeph}\'s
`isReadOnly`{.codeph} method returns
<span class="variable">true</span>), then this method should only
destroy credentials associated with the `Subject`{.codeph} during the
`commit`{.codeph} operation (removing the credentials is not possible).
If the `Subject`{.codeph} has been marked as
<span class="variable">read-only</span> and the credentials associated
with the `Subject`{.codeph} during the `commit`{.codeph} operation are
not destroyable (they do not implement the `Destroyable`{.codeph}
interface), then this method may throw a `LoginException`{.codeph}.

The `logout`{.codeph} method should return `true`{.codeph} if logout
succeeds, or otherwise throw a `LoginException`{.codeph}.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-4A0BD9DC-B45F-4606-A6BD-8BAC22952C52}

### Step 4: Choose or Write a Sample Application {#JSSEC-GUID-4A0BD9DC-B45F-4606-A6BD-8BAC22952C52 .sect3}

<div>
Either choose an existing sample application for your testing, or write
a new one.

See [Java Authentication and Authorization Service (JAAS) Reference
Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html)
for information about application requirements and a sample application
you can use for your testing.

</div>
</div>
<div class="sect3">
[]{#GUID-6DEAB2A4-2ADE-4CC8-B188-F0A58A38F61C}

### Step 5: Compile the LoginModule and Application {#JSSEC-GUID-6DEAB2A4-2ADE-4CC8-B188-F0A58A38F61C .sect3}

<div>
Compile your new `LoginModule`{.codeph} and the application you will use
for testing.

</div>
</div>
<div class="sect3">
[]{#GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979}

### Step 6: Prepare for Testing {#JSSEC-GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979 .sect3}

<div>
<div class="section" id="GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__STEP6APLACEYOURLOGINMODULEANDAPPLIC-83D213BF">
Step 6a: Place Your `LoginModule`{.codeph} and Application Code in JAR
Files

Place your `LoginModule`{.codeph} and application code in separate JAR
files, in preparation for referencing the JAR files in the policy in
[Step 6b: Set LoginModule and Application JAR File
Permissions](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__STEP6CSETLOGINMODULEANDAPPLICATIONJ-83D21A8B).
Here is a sample command for creating a JAR file:

``` {.oac_no_warn dir="ltr"}
jar cvf <JAR file name> <list of classes, separated by spaces>
```

This command creates a JAR file with the specified name containing the
specified classes.

For more information on the <span class="bold">jar</span> tool, see
[jar](olink:JSWOR614).

</div>
<!-- class="section" -->

<div class="section" id="GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__STEP6CSETLOGINMODULEANDAPPLICATIONJ-83D21A8B">
Step 6b: Set `LoginModule`{.codeph} and Application JAR File Permissions

If your `LoginModule`{.codeph} and/or application performs
security-sensitive tasks that will trigger security checks (making
network connections, reading or writing files on a local disk, etc.), it
will need to be granted the required permissions if it is run while a
security manager is installed; see [Permissions in the
JDK](permissions-jdk1.htm#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.").

Since `LoginModule`{.codeph}s usually associate `Principal`{.codeph}s
and credentials with an authenticated Subject, some types of permissions
a `LoginModule`{.codeph} will typically require are
[<span class="apiname">AuthPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/AuthPermission.html)s
with target names \"modifyPrincipals\", \"modifyPublicCredentials\", and
\"modifyPrivateCredentials\".

A sample statement granting permissions to a `LoginModule`{.codeph}
whose code is in `MyLM.jar`{.codeph} appears below. Such a statement
could appear in a policy file. In this example, the `MyLM.jar`{.codeph}
file is assumed to be in the `/localWork`{.codeph} directory.

``` {.oac_no_warn dir="ltr"}
grant codeBase "file:/localWork/MyLM.jar" {
    permission javax.security.auth.AuthPermission "modifyPrincipals";
    permission javax.security.auth.AuthPermission "modifyPublicCredentials";
    permission javax.security.auth.AuthPermission "modifyPrivateCredentials";
};
```

<div class="infoboxnote" id="GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__GUID-AF562355-EB12-48C5-A4A3-686DB9A8DA32">
Note:

Since a `LoginModule`{.codeph} is always invoked within an
`AccessController.doPrivileged`{.codeph} call, it should not have to
call `doPrivileged`{.codeph} itself. If it does, it may inadvertently
open up a security hole. For example, a `LoginModule`{.codeph} that
invokes the application-provided `CallbackHandler`{.codeph} inside a
`doPrivileged`{.codeph} call opens up a security hole by permitting the
application\'s `CallbackHandler`{.codeph} to gain access to resources it
would otherwise not have been able to access.

</div>
</div>
<!-- class="section" -->

<div class="section" id="GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__STEP6DCREATEACONFIGURATIONREFERENCI-83D21DD1">
Step 6c: Create a Configuration Referencing the LoginModule

Because JAAS supports a pluggable authentication architecture, your new
`LoginModule`{.codeph} can be used without requiring modifications to
existing applications. Only the login `Configuration`{.codeph} needs to
be updated in order to indicate use of a new `LoginModule`{.codeph}.

The default `Configuration`{.codeph} implementation from Oracle reads
configuration information from configuration files, as described in
[<span class="apiname">ConfigFile</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/login/ConfigFile.html).

Create a configuration file to be used for testing. For example, to
configure the previously-mentioned hypothetical IBM
`LoginModule`{.codeph} for an application, the configuration file might
look like this:

``` {.oac_no_warn dir="ltr"}
    AppName {
        com.ibm.auth.Module REQUIRED debug=true;
    };
```

where `AppName`{.codeph} should be whatever name the application uses to
refer to this entry in the login configuration file. The application
specifies this name as the first argument to the `LoginContext`{.codeph}
constructor.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-D8079E42-9E73-4378-9D34-E528BE727857}

### Step 7: Test Use of the LoginModule {#JSSEC-GUID-D8079E42-9E73-4378-9D34-E528BE727857 .sect3}

<div>
Test your application and its use of the `LoginModule`{.codeph}. When
you run the application, specify the login configuration file to be
used. For example, suppose your application is named `MyApp`{.codeph},
it is located in `MyApp.jar`{.codeph}, and your configuration file is
`test.conf`{.codeph}.

<div class="section">
You could run the application and specify the configuration file via the
following:

``` {.oac_no_warn dir="ltr"}
java -classpath MyApp.jar
 -Djava.security.auth.login.config=test.conf MyApp
```

Type all that on one line. Multiple lines are used here for legibility.

To specify a policy file named `my.policy`{.codeph} and run the
application with a security manager installed, do the following:

``` {.oac_no_warn dir="ltr"}
java -classpath MyApp.jar -Djava.security.manager
 -Djava.security.policy=my.policy
 -Djava.security.auth.login.config=test.conf MyApp
```

Again, type all that on one line.

You may want to configure the `LoginModule`{.codeph} with a
<span class="variable">debug</span> option to help ensure that it is
working correctly.

Debug your code and continue testing as needed. If you have problems,
review the steps above and ensure they are all completed.

Be sure to vary user input and the `LoginModule`{.codeph} options
specified in the configuration file.

Be sure to also include testing using different installation options
(e.g., placing the `LoginModule`{.codeph} on the class path or module
path) and execution environments (with or without a security manager
running). In particular, in order to ensure your `LoginModule`{.codeph}
works when a security manager is installed and the
`LoginModule`{.codeph}, you need to test such an installation and
execution environment, after granting required permissions, as described
in [Step 6b: Set LoginModule and Application JAR File
Permissions](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__STEP6CSETLOGINMODULEANDAPPLICATIONJ-83D21A8B).

</div>
<!-- class="section" -->

1.  <span>If you find during testing that your `LoginModule`{.codeph} or
    application needs modifications, make the modifications, recompile
    ([Step 5: Compile the LoginModule and
    Application](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-6DEAB2A4-2ADE-4CC8-B188-F0A58A38F61C "Compile your new LoginModule and the application you will use for testing.")).</span>
2.  <span>Place the updated code in a JAR file ([Step 6a: Place Your
    LoginModule and Application Code in JAR
    Files](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__STEP6APLACEYOURLOGINMODULEANDAPPLIC-83D213BF)).</span>
3.  <span>If needed fix or add to the permissions ([Step 6b: Set
    LoginModule and Application JAR File
    Permissions](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__STEP6CSETLOGINMODULEANDAPPLICATIONJ-83D21A8B)).</span>
4.  <span>If needed modify the login configuration file ([Step 6c:
    Create a Configuration Referencing the
    LoginModule](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979__STEP6DCREATEACONFIGURATIONREFERENCI-83D21DD1)).</span>
5.  <span>Re-run the application and repeat these steps as
    needed.</span>

</div>
</div>
<div class="sect3">
[]{#GUID-F799DF94-AD31-47CC-8760-863492F506EF}

### Step 8: Document Your LoginModule Implementation {#JSSEC-GUID-F799DF94-AD31-47CC-8760-863492F506EF .sect3}

<div>
Write documentation for clients of your `LoginModule`{.codeph}.

<div class="section">
Example documentation you may want to include is:

</div>
<!-- class="section" -->

-   <span>A README or User Guide describing</span>
    1.  <span>The authentication process employed by your
        `LoginModule`{.codeph} implementation.</span>
    2.  <span>Information on how to install the
        `LoginModule`{.codeph}.</span>
    3.  <span>Configuration options accepted by the
        `LoginModule`{.codeph}. For each option, specify the option name
        and possible values (or types of values), as well as the
        behavior the option controls.</span>
    4.  <span>The permissions required by your `LoginModule`{.codeph}
        when it is run with a security manager.</span>
-   <span>An example `Configuration`{.codeph} file that references your
    new `LoginModule`{.codeph}.</span>
-   <span>An example policy file granting your `LoginModule`{.codeph}
    the required permissions.</span>
-   <span>API documentation. Putting Javadoc comments into your source
    code as you write it will make the Javadoc API documentation easy to
    generate.</span>

</div>
</div>
<div class="sect3">
[]{#GUID-0A07484F-050E-4162-AE90-3A975AB26055}

### Step 9: Make LoginModule JAR File and Documents Available {#JSSEC-GUID-0A07484F-050E-4162-AE90-3A975AB26055 .sect3}

<div>
Make your `LoginModule`{.codeph} JAR file and documentation available to
clients.

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
| ------------ ------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ---------------- --  | e | )\                   |
|               [![Pre | L |             <span cl |
| vious](../../dcommon | o | ass="icon">Contents< |
| /gifs/leftnav.gif)\  | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|              [![Next | ] | -------------------- |
| ](../../dcommon/gifs | ( | -------------------- |
| /rightnav.gif)\      | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](j | . |                      |
| aas-authorization-tu | . |                      |
| torial.htm)   <span  | / |                      |
| class="icon">Next</s | d |                      |
| pan>](java-generic-s | c |                      |
| ecurity-services-jav | o |                      |
| a-gss-api1.htm)      | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| ------------ ------- | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ---------------- --  | s |                      |
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
