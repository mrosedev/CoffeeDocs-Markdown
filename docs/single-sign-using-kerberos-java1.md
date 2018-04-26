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

  ----------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------- --
            [![Previous](../../dcommon/gifs/leftnav.gif)\                                                      [![Next](../../dcommon/gifs/rightnav.gif)\                                             
   <span class="icon">Previous</span>](related-documentation1.htm)   <span class="icon">Next</span>](advanced-security-programming-java-se-authentication-secure-communication-and-single-sign1.htm)  
  ----------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-D4230975-A28B-4532-B1DD-3C7219A4867F}<!-- End Header -->

<script type="text/javascript">
window.name='single-sign-using-kerberos-java1'
</script>
<script type="text/javascript">
    function footdisplay(footnum,footnote) {
    var msg = window.open('about:blank', 'NewWindow' + footnum,
        'directories=no,height=100,location=no,menubar=no,resizable=yes,' +
        'scrollbars=yes,status=no,toolbar=no,width=598');
    msg.document.open('text/html');
    msg.document.write('<!DOCTYPE html ');
    msg.document.write('PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" ');
    msg.document.write('"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">'); 
    msg.document.write('<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en-us" lang="en-us" dir="ltr"><head><title>');
   
    msg.document.write('Footnote&amp;nbsp; ' + footnum);
    msg.document.write('<\/title><meta http-equiv="Content-Type" ');
    msg.document.write('content="text/html; charset=utf-8" />');
    msg.document.write('<meta http-equiv="Content-Script-Type" ');
    msg.document.write('content="text/javascript" />');
    msg.document.write('<style type="text/css"> <![CDATA[ ');
    msg.document.write('h1 {text-align: center; font-size: 14pt;}');
    msg.document.write('fieldset {border: none;}');
    msg.document.write('form {text-align: center;}');
    msg.document.write(' ]]\u003e <\/style>');
    msg.document.write('<\/head><body><div id="footnote"><h1>Footnote&nbsp; ' + footnum + '<\/h1><p>');
    msg.document.write(footnote);
    msg.document.write('<\/p><form action="" method="post"><fieldset>');
    msg.document.write('<input type="button" value="OK" ');
    msg.document.write('onclick="window.close();" />');
    msg.document.write('<\/fieldset><\/form><\/div><\/body><\/html>');
    msg.document.close();
    setTimeout(function() {
        var height = msg.document.getElementById('footnote').offsetHeight;
        msg.resizeTo(598, height + 100);
    }
    , 100);
    msg.focus();
}
            </script>
<noscript>
The script content on this page is for navigation purposes only and does
not alter the content in any way.

</noscript>
Single Sign-on Using Kerberos in Java {#JSSEC-GUID-D4230975-A28B-4532-B1DD-3C7219A4867F .sect1}
=====================================

<div>
</div>
<div class="sect2">
[]{#GUID-E8171823-258A-45DF-A420-661EAC84CCDD}

Abstract {#JSSEC-GUID-E8171823-258A-45DF-A420-661EAC84CCDD .sect2}
--------

<div>
A significant enhancement to the Java SE security architecture is the
capability to achieve single sign-on using Kerberos Version 5. A single
sign-on solution lets users authenticate themselves just once to access
information on any of several systems. This is done using JAAS for
authentication and authorization and Java GSS-API to establish a secure
context for communication with a peer application. Our focus is on
Kerberos V5 as the underlying security mechanism for single sign-on,
although other security mechanisms may be added in the future.

</div>
</div>
<div class="sect2">
[]{#GUID-7147244C-E7D5-4D70-92C6-069EB7C651A3}

Introduction {#JSSEC-GUID-7147244C-E7D5-4D70-92C6-069EB7C651A3 .sect2}
------------

<div>
With the increasing use of distributed systems users need to access
resources that are often remote. Traditionally users have had to sign-on
to multiple systems, each of which may involve different user names and
authentication techniques. In contrast, with single sign-on, the user
needs to authenticate only once and the authenticated identity is
securely carried across the network to access resources on behalf of the
user.

In this paper we discuss how to use single sign-on based on the Kerberos
V5 protocol. We use the Java Authentication and Authorization Service
(JAAS) to authenticate a principal to Kerberos and obtain credentials
that prove its identity. We show how Oracle\'s implementation of a
Kerberos login module can be made to read credentials from an existing
cache on platforms that contain native Kerberos support. We then use the
Java Generic Security Service API (Java GSS-API) to authenticate to a
remote peer using the previously obtained Kerberos credentials. We also
show how to delegate Kerberos credentials for single sign-on in a
multi-tier environment.

</div>
</div>
<div class="sect2">
[]{#GUID-6F8CAB6F-7DA8-4DED-8369-92BBB95C8A9E}

Kerberos V5 {#JSSEC-GUID-6F8CAB6F-7DA8-4DED-8369-92BBB95C8A9E .sect2}
-----------

<div>
Kerberos V5 is a trusted third party network authentication protocol
designed to provide strong authentication using secret key cryptography.
When using Kerberos V5, the user\'s password is never sent across the
network, not even in encrypted form, except during Kerberos V5
administration. Kerberos was developed in the mid-1980\'s as part of
MIT\'s Project Athena. A full description of the Kerberos V5 protocol is
beyond the scope of this paper. For more information on the Kerberos V5
protocol please refer to
[\[1\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-01)
and
[\[2\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-02).

Kerberos V5 is a mature protocol and has been widely deployed. A free
reference implementation in C is available from MIT. For these reasons
we have selected Kerberos V5 as the underlying technology for single
sign-on in Java SE.

</div>
</div>
<div class="sect2">
[]{#GUID-38C14739-0A86-46EA-B0E9-44A7CD6AA9E4}

Java Authentication and Authorization Service (JAAS) {#JSSEC-GUID-38C14739-0A86-46EA-B0E9-44A7CD6AA9E4 .sect2}
----------------------------------------------------

<div>
The Java SE security architecture used to solely determine privileges by
the origin of the code and the public key certificates matching the code
signers. However, in a multi-user environment it is desirable to further
specify privileges based on the authenticated identity of the user
running the code.

JAAS supplies such a capability. JAAS is a pluggable framework and
programming interface specifically targeted for authentication and
access control based on the authenticated identities.

</div>
<div class="sect3">
[]{#GUID-B4D7E22E-459E-4909-ABF7-647733847E75}

### Pluggable and Stackable Framework {#JSSEC-GUID-B4D7E22E-459E-4909-ABF7-647733847E75 .sect3}

<div>
JAAS authentication framework is based on Pluggable Authentication
Module (PAM); see
[\[3\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-03)
and
[\[4\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-04).
JAAS authentication is performed in a pluggable fashion allowing system
administrators to add appropriate authentication modules. This permits
Java applications to remain independent of underlying authentication
technologies, and new or updated authentication technologies can be
seamlessly configured without requiring modifications to the application
itself.

JAAS authentication framework also supports the stacking of
authentication modules. Multiple modules can be specified and they are
invoked by the JAAS framework in the order they were specified. The
success of the overall authentication depends on the results of the
individual authentication modules.

</div>
</div>
<div class="sect3">
[]{#GUID-2FFC7B8E-C8FC-492B-8D57-0BC14EA4D033}

### Authentication and Authorization {#JSSEC-GUID-2FFC7B8E-C8FC-492B-8D57-0BC14EA4D033 .sect3}

<div>
The JAAS framework can be divided into two components: an authentication
component and an authorization component.

The JAAS authentication component provides the ability to reliably and
securely determine who is currently executing Java code, regardless of
whether the code is running as an application, an applet, a bean, or a
servlet.

The JAAS authorization component supplements the existing Java security
framework by providing the means to restrict the executing Java code
from performing sensitive tasks, depending on its codesource and
depending on who is executing the code.

</div>
</div>
<div class="sect3">
[]{#GUID-AA7F81DA-583A-4275-8D2E-0C1FD2919ED2}

### Subject {#JSSEC-GUID-AA7F81DA-583A-4275-8D2E-0C1FD2919ED2 .sect3}

<div>
JAAS uses the term Subject to refer to any entity that is the source of
a request to access resources. A Subject may be a user or a service.
Since an entity may have many names or principals JAAS uses Subject as
an extra layer of abstraction that handles multiple names per entity.
Thus a Subject is comprised of a set of principals. There are no
restrictions on principal names.

A Subject is only populated with authenticated principals.
Authentication typically involves the user providing proof of identity,
such as a password.

A Subject may also have security related attributes, which are referred
to as credentials. The credentials can be public or private. Sensitive
credentials such as private cryptographic keys are stored in the private
credentials set of the Subject.

The <span class="apiname">Subject</span> class has methods to retrieve
the principals, public credentials and private credentials associated
with it.

Please note that different permissions may be required for operations on
these classes. For example
<span class="apiname">AuthPermission(\"modifyPrincipals\")</span> may be
required to modify the principal set of the Subject. Similar permissions
are required to modify the public credentials, private credentials and
to get the current Subject.

</div>
</div>
<div class="sect3">
[]{#GUID-6F5671ED-C6FC-4842-A1FA-DB08E61C369A}

### doAs and doAsPrivileged {#JSSEC-GUID-6F5671ED-C6FC-4842-A1FA-DB08E61C369A .sect3}

<div>
Java SE enforces runtime access controls via
<span class="apiname">java.lang.SecurityManager</span>. The
<span class="apiname">SecurityManager</span> is consulted anytime
sensitive operations are attempted. The
<span class="apiname">SecurityManager</span> delegates this
responsibility to
<span class="apiname">java.security.AccessController</span>. The
<span class="apiname">AccessController</span> obtains a current image of
the <span class="apiname">AccessControlContext</span> and verifies that
it has sufficient permission to do the operation requested.

JAAS provides two methods, <span class="apiname">doAs</span> and
<span class="apiname">doAsPrivileged</span>, that can be used to
associate an authenticated Subject with the
<span class="apiname">AccessControlContext</span> dynamically.

The <span class="apiname">doAs</span> method associates the Subject with
the current thread\'s access control context and subsequent access
control checks are made on the basis of the code being executed and the
Subject executing it.

``` {.oac_no_warn dir="ltr"}
public static Object doAs(final Subject subject,
                          final PrivilegedAction action)

public static Object doAs(final Subject subject,
                          final PrivilegedExceptionAction action)
    throws  PrivilegedActionException;
```

Both forms of the <span class="apiname">doAs</span> method first
associate the specified subject with the current Thread\'s
<span class="apiname">AccessControlContext</span>, and then execute the
action. This achieves the effect of having the action run as the
Subject. The first method can throw runtime exceptions but normal
execution has it returning an <span class="apiname">Object</span> from
the <span class="apiname">run()</span> method of its action argument.
The second method behaves similarly except that it can throw a checked
<span class="apiname">PrivilegedActionException</span> from its
<span class="apiname">run()</span> method. An
<span class="apiname">AuthPermission(\"doAs\")</span> is required to
call the <span class="apiname">doAs</span> methods.

The following methods also execute code as a particular Subject:

``` {.oac_no_warn dir="ltr"}
public static Object doAsPrivileged(final Subject subject,
                                    final PrivilegedAction action,
                                    final AccessControlContext  acc);

public static Object doAsPrivileged(final Subject subject,
                                    final PrivilegedExceptionAction action,
                                    final AccessControlContext acc)
    throws PrivilegedActionException;
```

The <span class="apiname">doAsPrivileged</span> method behaves exactly
as <span class="apiname">doAs</span>, except that it allows the caller
to specify an access control context. Thus it effectively throws away
the current <span class="apiname">AccessControlContext</span> and
authorization decisions will be based on the
<span class="apiname">AccessControlContext</span> passed in.

Since the <span class="apiname">AccessControlContext</span> is set on a
per thread basis, different threads within the JVM can assume different
identities. The Subject associated with a specific
<span class="apiname">AccessControlContext</span> can be retrieved by
using the following method:

``` {.oac_no_warn dir="ltr"}
public static Subject getSubject(final AccessControlContext acc);
```

</div>
</div>
<div class="sect3">
[]{#GUID-DBF4F859-01ED-4E47-B842-EE128B146E8D}

### LoginContext {#JSSEC-GUID-DBF4F859-01ED-4E47-B842-EE128B146E8D .sect3}

<div>
The <span class="apiname">LoginContext</span> class provides the basic
methods used to authenticate Subjects. It also allows an application to
be independent of the underlying authentication technologies. The
<span class="apiname">LoginContext</span> consults a configuration that
determines the authentication services or
<span class="apiname">LoginModules</span> configured for a particular
application. If the application does not have a specific entry, it
defaults to the entry identified as \"other\".

To support the stackable nature of
<span class="apiname">LoginModules</span>,
<span class="apiname">LoginContext</span> performs authentication in two
phases. In the first phase or login phase, it invokes each configured
LoginModule to attempt the authentication. If all the necessary
<span class="apiname">LoginModules</span> succeed, then
<span class="apiname">LoginContext</span> enters the second phase where
it invokes each LoginModule again to formally commit the authentication
process. During this phase the Subject is populated with the
authenticated principals and their credentials. If either of the phase
fails, then the <span class="apiname">LoginContext</span> invokes each
configured module to abort the entire authentication attempt. Each
<span class="apiname">LoginModule</span> then cleans up any relevant
state associated with the authentication attempt.

<span class="apiname">LoginContext</span> has four constructors that can
be used to instantiate it. All of them require the configuration entry
name to be passed. In addition the Subject and/or a
<span class="apiname">CallbackHandler</span> can also be passed to the
constructors.

</div>
</div>
<div class="sect3">
[]{#GUID-20572EC0-B790-4C69-B168-6129F9B42C26}

### Callbacks {#JSSEC-GUID-20572EC0-B790-4C69-B168-6129F9B42C26 .sect3}

<div>
The login modules invoked by JAAS must be able to garner information
from the caller for authentication. For example the Kerberos login
module may require users to enter their Kerberos password for
authentication.

The <span class="apiname">LoginContext</span> allows the application to
specify a callback handler that the underlying login modules use to
interact with users. There are two callback handlers - one based on the
command line and another based on a GUI.

</div>
</div>
<div class="sect3">
[]{#GUID-8AFBA819-AE63-4879-B83F-0E64FB880939}

### LoginModules {#JSSEC-GUID-8AFBA819-AE63-4879-B83F-0E64FB880939 .sect3}

<div>
Oracle provides an implementation of the
<span class="apiname">UnixLoginModule</span>,
<span class="apiname">NTLoginModule</span>,
<span class="apiname">JNDILoginModule</span>,
<span class="apiname">KeyStoreLoginModule</span> and
<span class="apiname">Krb5LoginModule</span>.

</div>
</div>
<div class="sect3">
[]{#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E}

### The Kerberos Login Module {#JSSEC-GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E .sect3}

<div>
The class
<span class="apiname">com.sun.security.auth.module.Krb5LoginModule</span>
is Oracle\'s implementation of a login module for the Kerberos version 5
protocol. Upon successful authentication the Ticket Granting Ticket
(TGT) is stored in the Subject\'s private credentials set and the
Kerberos principal is stored in the Subject\'s principal set.

Based on certain configurable options,
<span class="apiname">Krb5LoginModule</span> can also use an existing
credentials cache, such as a native cache in the operating system, to
acquire the TGT and/or use a `keytab` file containing the secret key to
implicitly authenticate a principal. Both Solaris and Windows contain a
credentials cache that <span class="apiname">Krb5LoginModule</span> can
use for fetching the TGT. Solaris also contains a system-wide `keytab`
file that <span class="apiname">Krb5LoginModule</span> can use for
fetching the secret key. On all platforms,
<span class="apiname">Krb5LoginModule</span> supports options to set the
file path to a ticket cache or `keytab` file of choice. This is useful
when third-party Kerberos support is installed and Java integration is
desired. Please consult the documentation for
<span class="apiname">Krb5LoginModule</span> to learn about these
options. In the absence of a native cache or `keytab`, the user will be
prompted for the password and the TGT obtained from the key distribution
center (KDC).

The following is a sample JAAS login configuration entry for a client
application. In this example,
<span class="apiname">Krb5LoginModule</span> will use the native ticket
cache to get the TGT available in it. The authenticated identity will be
the identity of the Kerberos principal that the TGT belongs to.

``` {#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E__SAMPLECLIENTCOM.SUN.SECURITY.AUTH.M-37F332E5 .oac_no_warn dir="ltr"}
// Sample client configuration entry

SampleClient {
    com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true
};
```

The following is a sample login configuration entry for a server
application. With this configuration, the secret key from the keytab is
used to authenticate the principal `nfs/bar.example.com`{.codeph} and
both the TGT obtained from the Kerberos KDC and the secret key are
stored in the Subject\'s private credentials set. The stored key may be
used later to validate a service ticket sent by a client (See the
section on Java GSS-API.)

``` {#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E__SAMPLESERVERCONFIGURATIONENTRYSAMPL-37F37F85 .oac_no_warn dir="ltr"}
// Sample server configuration entry

SampleServer {
     com.sun.security.auth.module.Krb5LoginModule
         required useKeyTab=true storeKey=true principal="nfs/bar.example.com"
};
```

In the following client code example, the configuration entry
`SampleClient`{.codeph} will be used by the
<span class="apiname">LoginContext</span>. The
<span class="apiname">TextCallbackHandler</span> class will be used to
prompt the user for the Kerberos password. Once the user has logged in,
the Subject will be populated with the Kerberos Principal name and the
TGT. Thereafter the user can execute code using
<span class="apiname">Subject.doAs</span> passing in the Subject
obtained from the <span class="apiname">LoginContext</span>.

``` {#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E__SAMPLECLIENTCODELOGINCONTEXTLCNULLT-37F389A2 .oac_no_warn dir="ltr"}
// Sample client code

LoginContext lc = null;

try {
        lc = new LoginContext("SampleClient", new TextCallbackHandler());
        // attempt authentication
        lc.login();
} catch (LoginException le) {
    ...
}

// Now try to execute ClientAction as the authenticated Subject

Subject mySubject = lc.getSubject();
PrivilegedAction action = new ClientAction();
Subject.doAs(mySubject, action);
```

<span class="apiname">ClientAction</span> could be an action that is
allowed only for authenticated Kerberos client Principals with a
specific value.

The following shows server side sample code. It is similar to the
[sample client
code](single-sign-using-kerberos-java1.html#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E__SAMPLECLIENTCODELOGINCONTEXTLCNULLT-37F389A2)
except for the application entry name and the
<span class="apiname">PrivilegedAction</span>.

``` {#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E__SAMPLESERVERCODELOGINCONTEXTLCNULLT-37F4D999 .oac_no_warn dir="ltr"}
// Sample server code

LoginContext lc = null;

try {
        lc = new LoginContext("SampleServer", new TextCallbackHandler());
        // attempt authentication
        lc.login();
} catch (LoginException le) {
   ...
}

// Now try to execute ServerAction as the authenticated Subject

Subject mySubject = lc.getSubject();
PrivilegedAction action = new ServerAction();
Subject.doAs(mySubject, action);
```

</div>
</div>
<div class="sect3">
[]{#GUID-A82CE65B-0730-42EC-973B-51D1CDA7D382}

### Kerberos Classes {#JSSEC-GUID-A82CE65B-0730-42EC-973B-51D1CDA7D382 .sect3}

<div>
To enable other vendors to provide their own Kerberos login module
implementation that can be used with Java GSS-API, three standard
Kerberos classes have been introduced in the
<span class="apiname">javax.security.auth.kerberos</span> package. These
are <span class="apiname">KerberosPrincipal</span> for Kerberos
principals, <span class="apiname">KerberosKey</span> for the long-term
Kerberos secret key and <span class="apiname">KerberosTicket</span> for
Kerberos tickets. All implementations of the Kerberos login module must
use these classes to store principals, keys and tickets in the Subject.

</div>
</div>
<div class="sect3">
[]{#GUID-BB48DD97-7BC5-487D-AE9C-E469917DFE73}

### Authorization {#JSSEC-GUID-BB48DD97-7BC5-487D-AE9C-E469917DFE73 .sect3}

<div>
Upon successful authentication of a Subject, access controls can be
enforced based upon the principals associated with the authenticated
Subject. The JAAS principal based access controls augment the
<span class="apiname">CodeSource</span> access controls of Java SE.
Permissions granted to a Subject are configured in
<span class="apiname">Policy</span>, which is an abstract class for
representing the system wide access control policy. Oracle provides a
file based implementation of the <span class="apiname">Policy</span>
class. The <span class="apiname">Policy</span> class is provider based
so that others can provide their own policy implementation.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-3336BC5D-90CA-4646-B96A-FE79EA2D1AD6}

Java Generic Security Service Application Program Interface (Java GSS-API) {#JSSEC-GUID-3336BC5D-90CA-4646-B96A-FE79EA2D1AD6 .sect2}
--------------------------------------------------------------------------

<div>
</div>
<div class="sect3">
[]{#GUID-A92F4222-4C58-49AA-AF94-E7BB12D3C3C5}

### Generic Security Service API (GSS-API) {#JSSEC-GUID-A92F4222-4C58-49AA-AF94-E7BB12D3C3C5 .sect3}

<div>
Enterprise applications often have varying security requirements and
deploy a range of underlying technologies to achieve this. In such a
scenario how do we develop a client-server application so that it can
easily migrate from one technology to another? The GSS-API was designed
in the Common Authentication Technology working group of the IETF to
solve this problem by providing a uniform application programming
interface for peer to peer authentication and secure communication that
insulates the caller from the details of the underlying technology.

The API, described in a language independent form in RFC 2743
[\[6\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-06),
accommodates the following security services: authentication, message
confidentiality and integrity, sequencing of protected messages, replay
detection, and credential delegation. The underlying security technology
or \"security mechanism\" being used, has a choice of supporting one or
more of these features beyond the essential one way
authentication.[^Foot 1^](#fn_1){#fn_1}

There are mainly two standard security mechanisms that the IETF has
defined: Kerberos V5
[\[6\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-06)
and the Simple Public Key Mechanism (SPKM)
[\[8\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-08).

The API is designed such that an implementation may support multiple
mechanisms simultaneously, giving the application the ability to choose
one at runtime. However, a client application and a server application
that communicate with each other must use the same security mechanism.
[Figure
7-1](single-sign-using-kerberos-java1.html#GUID-A92F4222-4C58-49AA-AF94-E7BB12D3C3C5__AMULTI-MECHANISMGSS-APIIMPLEMENTATI-37F451B6)
illustrates this. It shows a client-server application that uses the
GSS-API for secure communication. The GSS framework enables this
application to support multiple security mechanisms (in this example,
Kerberos V5 and SPKM). Once the GSS-API negotiates a security mechanism
for the client or server application (in this example, Kerberos V5) the
other must use the same.

<div class="figure" id="GUID-A92F4222-4C58-49AA-AF94-E7BB12D3C3C5__AMULTI-MECHANISMGSS-APIIMPLEMENTATI-37F451B6">
Figure 7-1 A Multi-Mechanism GSS-API Implementation

![The surrounding text describes this
figure.](img/jgss_pb_001b.png "The surrounding text describes this figure.")

</div>
<!-- class="figure" -->

Mechanisms are identified by means of unique object identifier\'s
(OID\'s) that are registered with the IANA. For instance, the Kerberos
V5 mechanism is identified by the OID
`{iso(1) member-body(2) United States(840) mit(113554) infosys(1) gssapi(2) krb5(2)}`{.codeph}

Another important feature of the API is that it is token based. i.e.,
Calls to the API generate opaque octets that the application must
transport to its peer. This enables the API to be transport independent.

</div>
</div>
<div class="sect3">
[]{#GUID-D73F1DE2-D003-429F-B918-2CDC6897E9C7}

### Java GSS-API {#JSSEC-GUID-D73F1DE2-D003-429F-B918-2CDC6897E9C7 .sect3}

<div>
The Java API for the Generic Security Service was also defined at the
IETF and is documented in RFC 2853
[\[10\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-10).
Oracle is pursuing the standardization of this API under the Java
Community Process (JCP)
[\[11\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-11)
and plans to deliver a reference implementation with Merlin. Because the
JCP is merely endorsing this externally defined API, the IETF assigned
package namespace `org.ietf.jgss`{.codeph} will be retained in Merlin.

Oracle\'s implementation of Java GSS-API, will initially ship with
support for the Kerberos V5 mechanism only. Kerberos V5 mechanism
support is mandatory for all Java GSS-API implementations in Java SE,
although they are free to support additional mechanisms. In a future
release, a Service Provider Interface (SPI) will be added so that new
mechanisms can be configured statically or even at runtime. Even now the
reference implementation in Merlin will be modular and support a private
provider SPI that will be converted to public when standardized.

The Java GSS-API framework itself is quite thin, and all security
related functionality is delegated to components obtained from the
underlying mechanisms. The <span class="apiname">GSSManager</span> class
is aware of all mechanism providers installed and is responsible for
invoking them to obtain these components.

The implementation of the default
<span class="apiname">GSSManager</span> that will ship with Java SE is
obtained as follows:

``` {.oac_no_warn dir="ltr"}
GSSManager manager = GSSManager.getInstance();
```

The <span class="apiname">GSSManager</span> can be used to configure new
providers and to list all mechanisms already present. The
<span class="apiname">GSSManager</span> also serves as a factory class
for three important interfaces: <span class="apiname">GSSName</span>,
<span class="apiname">GSSCredential</span>, and
<span class="apiname">GSSContext</span>. These interfaces are described
below with the methods to instantiate their implementations. For a
complete API specification, readers are referred to
[\[9\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-09)
and
[\[11\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-11).

Most calls to Java GSS-API throw a
<span class="apiname">GSSException</span> that encapsulate problems that
occur both within the GSS-API framework, and within the mechanism
providers.

</div>
</div>
<div class="sect3">
[]{#GUID-AB5BB523-052A-4ACA-B0D5-BF5A3C220093}

### The GSSName Interface {#JSSEC-GUID-AB5BB523-052A-4ACA-B0D5-BF5A3C220093 .sect3}

<div>
This interface represents an entity for the purposes of Java GSS-API. An
implementation of this interface is instantiated as follows:

``` {.oac_no_warn dir="ltr"}
GSSName GSSManager.createName(String name, Oid nameType)
    throws GSSException
```

For example:

``` {.oac_no_warn dir="ltr"}
GSSName clientName = manager.createName("duke", GSSName.NT_USER_NAME);
```

This call returns a <span class="apiname">GSSName</span> that represents
the user principal `duke`{.codeph} at a mechanism independent level.
Internally, it is assumed that each supported mechanism will map the
generic representation of the user to a more mechanism specific form.
For instance a Kerberos V5 mechanism provider might map this name to
`duke@EXAMPLE.COM`{.codeph} where `EXAMPLE.COM`{.codeph} is the local
Kerberos realm. Similarly, a public key based mechanism provider might
map this name to an X.509 Distinguished Name.

If we were referring to a principal that was not a user, but some sort
of service, we would indicate that to the Java GSS-API call so that the
mechanism knows to interpret it differently.

Example:

``` {.oac_no_warn dir="ltr"}
GSSName serverName = manager.createName("nfs@bar.example.com",
                                         GSSName.NT_HOSTBASED_SERVICE);
```

The Kerberos V5 mechanism would map this name to the Kerberos specific
form `nfs/bar.example.com@EXAMPLE.COM`{.codeph} where
`EXAMPLE.COM`{.codeph} is the realm of the principal. This principal
represents the service `nfs`{.codeph} running on the host machine
`bar.example.com`{.codeph}.

Oracle\'s implementation of the `GSSName`{.codeph} interface is a
container class. The container class lazily asks the individual
providers to perform their mapping when their mechanism is used and then
stores each mapped element in a set of principals. In this respect an
implementation of `GSSName`{.codeph} is similar to the principal set
stored in a Subject. It may even contain the same elements that are in a
Subject\'s principal set, but its use is restricted to the context of
Java GSS-API.

The name element stored by the Oracle Kerberos V5 provider is an
instance of a subclass of
`javax.security.auth.kerberos.KerberosPrincipal`{.codeph}.

</div>
</div>
<div class="sect3">
[]{#GUID-01637F56-125B-469E-8C4A-D642417DE870}

### The GSSCredential Interface {#JSSEC-GUID-01637F56-125B-469E-8C4A-D642417DE870 .sect3}

<div>
This interface encapsulates the credentials owned by one entity. Like
the <span class="apiname">GSSName</span>, this interface too is a
multi-mechanism container.

Its implementation is instantiated as follows:

``` {.oac_no_warn dir="ltr"}
GSSCredential createCredential(GSSName name,
                               int lifetime,
                               Oid[] desiredMechs,
                               int usage)
    throws GSSException
```

Here is an example of this call on the client side:

``` {.oac_no_warn dir="ltr"}
GSSCredential clientCreds =
    manager.createCredential(clientName,
                             8*3600,
                             desiredMechs,
                             GSSCredential.INITIATE_ONLY);
```

The <span class="apiname">GSSManager</span> invokes the providers of the
mechanisms listed in the <span class="apiname">desiredMechs</span> for
credentials that belong to the <span class="apiname">GSSName</span>
<span class="apiname">clientName</span>. Additionally, it imposes the
restriction that the credential must be the kind that can initiate
outbound requests (i.e., a client credential), and requests a lifetime
of 8 hours for it. The returned object contains elements from a subset
of <span class="apiname">desiredMechs</span> that had some credential
available to satisfy this criteria. The element stored by the Kerberos
V5 mechanism is an instance of a subclass of
<span class="apiname">javax.security.auth.kerberos.KerberosTicket</span>
containing a TGT that belongs to the user.

Credential acquisition on the server side occurs as follows:

``` {.oac_no_warn dir="ltr"}
GSSCredential serverCreds =
    manager.createCredential(serverName,
                             GSSCredential.INDEFINITE_LIFETIME,
                             desiredMechs,
                             GSSCredential.ACCEPT_ONLY);
```

The behavior is similar to the client case, except that the kind of
credential requested is one that can accept incoming requests (i.e., a
server credential). Moreover, servers are typically long lived and like
to request a longer lifetime for the credentials such as the
<span class="apiname">INDEFINITE\_LIFETIME</span> shown here. The
Kerberos V5 mechanism element stored is an instance of a subclass of
<span class="apiname">javax.security.auth.kerberos.KerberosKey</span>
containing the secret key of the server.

This step can be an expensive one, and applications generally acquire a
reference at initialization time to all the credentials they expect to
use during their lifetime.

</div>
</div>
<div class="sect3">
[]{#GUID-D552C782-1820-444B-85EA-A4AED3DE3757}

### The GSSContext Interface {#JSSEC-GUID-D552C782-1820-444B-85EA-A4AED3DE3757 .sect3}

<div>
The <span class="apiname">GSSContext</span> is an interface whose
implementation provides security services to the two peers.

On the client side a <span class="apiname">GSSContext</span>
implementation is obtained with the following API call:

``` {.oac_no_warn dir="ltr"}
GSSContext GSSManager.createContext(GSSName peer,
                                    Oid mech,
                                    GSSCredential clientCreds,
                                    int lifetime)
    throws GSSException
```

This returns an initialized security context that is aware of the peer
that it must communicate with and the mechanism that it must use to do
so. The client\'s credentials are necessary to authenticate to the peer.

On the server side the <span class="apiname">GSSContext</span> is
obtained as follows:

``` {.oac_no_warn dir="ltr"}
GSSContext GSSManager.createContext(GSSCredential serverCreds)
    throws GSSException
```

This returns an initialized security context on the acceptor\'s side. At
this point it does not know the name of the peer (client) that will send
a context establishment request or even the underlying mechanism that
will be used. However, if the incoming request is not for service
principal represented by the credentials
<span class="apiname">serverCreds</span>, or the underlying mechanism
requested by the client side does not have a credential element in
<span class="apiname">serverCreds</span>, then the request will fail.

Before the <span class="apiname">GSSContext</span> can be used for its
security services it has to be established with an exchange of tokens
between the two peers. Each call to the context establishment methods
will generate an opaque token that the application must somehow send to
its peer using a communication channel of its choice.

The client uses the following API call to establish the context:

``` {.oac_no_warn dir="ltr"}
byte[] GSSContext.initSecContext(byte[] inToken,
                                 int offset,
                                 int len)

   throws GSSException
```

The server uses the following call:

``` {.oac_no_warn dir="ltr"}
byte[] acceptSecContext(byte[] inToken,
                        int offset,
                        int len)

   throws GSSException
```

These two methods are complementary and the input accepted by one is the
output generated by the other. The first token is generated when the
client calls <span class="apiname">initSecContext</span> for the first
time. The arguments to this method are ignored during that call. The
last token generated depends on the particulars of the security
mechanism being used and the properties of the context being
established.

The number of round trips of GSS-API tokens required to authenticate the
peers varies from mechanism to mechanism and also varies with
characteristics such as whether mutual authentication or one-way
authentication is desired. Thus each side of the application must
continue to call the context establishment methods in a loop until the
process is complete.

In the case of the Kerberos V5 mechanism, there is no more than one
round trip of tokens during context establishment. The client first
sends a token generated by its
<span class="apiname">initSecContext()</span> containing the Kerberos
AP-REQ message
[\[2\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-02).
In order to generate the AP-REQ message, the Kerberos provider obtains a
service ticket for the target server using the client\'s TGT. The
service ticket is encrypted with the server\'s long-term secret key and
is encapsulated as part of the AP-REQ message. After the server receives
this token, it is passed to the
<span class="apiname">acceptSecContext()</span> method which decrypts
the service ticket and authenticates the client. If mutual
authentication was not requested, both the client and server side
contexts would be established, and the server side
<span class="apiname">acceptSecContext()</span> would generate no
output.

However, if mutual authentication were enabled, then the server\'s
<span class="apiname">acceptSecContext()</span> would generate an output
token containing the Kerberos AP-REP
[\[2\]](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-02)
message. This token would need to be sent back to the client for
processing by its <span class="apiname">initSecContext()</span>, before
the client side context is established.

Note that when a <span class="apiname">GSSContext</span> is initialized
on the client side, it is clear what underlying mechanism needs to be
used. The Java GSS-API framework can obtain a context implementation
from the appropriate mechanism provider. Thereafter, all calls made to
the <span class="apiname">GSSContext</span> object are delegated to the
mechanism\'s context implementation. On the server side, the mechanism
to use is not decided until the first token from the client side
arrives.

Here is a class showing how the client side of an application would be
coded. This is the `ClientAction`{.codeph} class that was executed using
the <span class="apiname">doAs</span> method in the [sample client
code](single-sign-using-kerberos-java1.html#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E__SAMPLECLIENTCODELOGINCONTEXTLCNULLT-37F389A2)
in the section [The Kerberos Login
Module](single-sign-using-kerberos-java1.html#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E):

``` {.oac_no_warn dir="ltr"}
// Sample client using Java GSS-API

class ClientAction implements PrivilegedAction {

    public Object run() {
        ...
        ...
        try {
            GSSManager manager = GSSManager.getInstance();
            GSSName clientName =
                manager.createName("duke", GSSName.NT_USER_NAME);
            GSSCredential clientCreds =
                manager.createCredential(clientName,
                                          8*3600,
                                          desiredMechs,
                                          GSSCredential.INITIATE_ONLY);
            GSSName peerName =
                manager.createName("nfs@bar.example.com",
                                    GSSName.NT_HOSTBASED_SERVICE);
            GSSContext secContext =
                manager.createContext(peerName,
                                      krb5Oid,
                                      clientCreds,
                                      GSSContext.DEFAULT_LIFETIME);
            secContext.requestMutualAuth(true);

            // The first input token is ignored
            byte[] inToken = new byte[0];

            byte[] outToken = null;

            boolean established = false;

           // Loop while the context is still not established
           while (!established) {
               outToken =
                   secContext.initSecContext(inToken, 0, inToken.length);

               // Send a token to the peer if one was generated
               if (outToken != null)
                  sendToken(outToken);

               if (!secContext.isEstablished()) {
                  inToken = readToken();
               else
                  established = true;
            }
        } catch (GSSException e) {
             ....
        }
        ...
        ...
    }
}
```

The corresponding section of code on the server side running the
`ServerAction`{.codeph} class from the [sample server
code](single-sign-using-kerberos-java1.html#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E__SAMPLESERVERCODELOGINCONTEXTLCNULLT-37F4D999)
in the section [The Kerberos Login
Module](single-sign-using-kerberos-java1.html#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E):

``` {.oac_no_warn dir="ltr"}
// Sample server using Java GSS-API

class ServerAction implelemts PrivilegedAction {

    public Object run() {
        ...
        ...
        try {
            GSSManager manager = GSSManager.getInstance();
            GSSName serverName =
                manager.createName("nfs@bar.example.com",
                                    GSSName.NT_HOSTBASED_SERVICE);
            GSSCredential serverCreds =
             manager.createCredential(serverName,
                                       GSSCredential.INDEFINITE_LIFETIME,
                                       desiredMechs,
                                       GSSCredential.ACCEPT_ONLY);
            GSSContext secContext = manager.createContext(serverCreds);

            byte[] inToken = null;
            byte[] outToken = null;

            // Loop while the context is still not established
            while (!secContext.isEstablished()) {
                 inToken = readToken();
                 outToken =
                     secContext.acceptSecContext(inToken, 0, inToken.length);

                  // Send a token to the peer if one was generated
                  if (outToken != null)
                      sendToken(outToken);
            }
        } catch (GSSException e) {
          ...
        }
        ...
        ...
   }
}
```

</div>
</div>
<div class="sect3">
[]{#GUID-627867F1-0787-4D20-A971-01F2B5EA3FF3}

### Message Protection {#JSSEC-GUID-627867F1-0787-4D20-A971-01F2B5EA3FF3 .sect3}

<div>
Once the security context is established, it can be used for message
protection. Java GSS-API provides both message integrity and message
confidentiality. The two calls that enable this are as follows:

``` {.oac_no_warn dir="ltr"}
byte[] GSSContext.wrap(byte[] clearText,
                       int offset,
                       int len,
                       MessageProp properties)
    throws GSSException
```

and

``` {.oac_no_warn dir="ltr"}
byte[] unwrap(byte[] inToken,
              int offset,
              int len,
              MessageProp properties)
    throws GSSException
```

The <span class="apiname">wrap</span> method is used to encapsulate a
cleartext message in a token such that it is integrity protected.
Optionally, the message can also be encrypted by requesting this through
a <span class="apiname">MessageProp</span> object. The
<span class="apiname">wrap</span> method returns an opaque token that
the caller sends to its peer. The original cleartext is returned by the
peer\'s <span class="apiname">unwrap</span> method when the token is
passed to it. The <span class="apiname">MessageProp</span> object on the
<span class="apiname">unwrap</span> side returns information about
whether the message was simply integrity protected or whether it was
encrypted as well. It also contains sequencing and duplicate token
warnings.

</div>
</div>
<div class="sect3">
[]{#GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B}

### Credential Delegation {#JSSEC-GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B .sect3}

<div>
Java GSS-API allows the client to securely delegate its credentials to
the server, such that the server can initiate other security contexts on
behalf of the client. This feature is useful for single sign-on in a
multi-tier environment. [Figure
7-2](single-sign-using-kerberos-java1.html#GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B__GUID-BDE6C438-A115-4935-BF04-A06CAC888B99)
illustrates this.

<div class="figure" id="GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B__GUID-BDE6C438-A115-4935-BF04-A06CAC888B99">
Figure 7-2 Traditional Credential Delegation

![Description of Figure 7-2
follows](img/jgss_pb_002c.png "Description of Figure 7-2 follows")\
[Description of \"Figure 7-2 Traditional Credential
Delegation\"](img_text/jgss_pb_002c.htm)

</div>
<!-- class="figure" -->

The client requests credential delegation prior to making the first call
to <span class="apiname">initSecContext()</span>:

``` {.oac_no_warn dir="ltr"}
void GSSContext.requestCredDeleg(boolean state)
    throws GSSException
```

by setting state to true.

The server receives the delegated credential after context
establishment:

``` {.oac_no_warn dir="ltr"}
GSSCredential GSSContext.getDelegCred() throws GSSException
```

The server can then pass this <span class="apiname">GSSCredential</span>
to <span class="apiname">GSSManager.createContext()</span> pretending to
be the client.

In the case of the Kerberos V5 mechanism, the delegated credential is a
forwarded TGT that is encapsulated as part of the first token sent from
the client to the server. Using this TGT, the server can obtain a
service ticket on behalf of the client for any other service.

<div class="section">
MS-SFU Kerberos Extensions

[MS-SFU](http://msdn.microsoft.com/en-us/library/cc246071.aspx) refers
to Microsoft Kerberos 5 extensions that allow a service to obtain a
Kerberos service ticket on behalf of a client. Microsoft calls this
feature constrained delegation. This is useful when the authentication
between the client and this service is not established through Kerberos
(thus the standard Kerberos delegation cannot be used) but the service
needs to access a Kerberos-secured back-end server in the name of the
client.

MS-SFU adds two extensions to that protocol: Service for User to Self
(S4U2self), which allows a front-end service to obtain a Kerberos
service ticket to itself on behalf of a user, and Service for User to
Proxy (S4U2proxy), which enables it to obtain a service ticket on behalf
of the user to a second, back-end service. Together, these two
extensions enable the front-end service to obtain a Kerberos service
ticket on behalf of a user. The resulting service ticket can be used to
access other services on the local or remote machines. The public method
[<span class="apiname">ExtendedGSSCredential::impersonate</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/jgss/ExtendedGSSCredential.html#impersonate-org.ietf.jgss.GSSName-)
in the <span class="apiname">com.sun.security.jgss</span> package
implements these extensions.

This feature is very useful in secure enterprise deployments. For
example, in a typical network service, the front end (such as a web
server) often needs to access the back end (such as a database server)
on behalf of a client. Normal Kerberos 5 supports delegation, but
demands that all layers in this chain explicitly use Kerberos
authentication at each step, which is not always possible or desirable.

For example, if a client logs in to a web server using digest
authentication, then there are no Kerberos credentials to be delegated,
and normal step-by-step Kerberos 5 authentication cannot occur. However,
because MS-SFU defines the Service for User (S4U2self) extension so that
the front end can access the back end on behalf of the client without
presenting the client\'s Kerberos credentials, MS-SFU could provide
authentication in this situation. [Figure
7-3](single-sign-using-kerberos-java1.html#GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B__CONSTRAINEDDELEGATIONWITHS4U2SELF-47300961)
illustrates this.

<div class="figure" id="GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B__CONSTRAINEDDELEGATIONWITHS4U2SELF-47300961">
Figure 7-3 Constrained Delegation with S4U2self

![Description of Figure 7-3
follows](img/jgss_pb_004c.png "Description of Figure 7-3 follows")\
[Description of \"Figure 7-3 Constrained Delegation with
S4U2self\"](img_text/jgss_pb_004c.htm)

</div>
<!-- class="figure" -->

In addition, there are potential security gaps in the standard Kerberos
5 delegation mechanism (which Microsoft calls open delegation). In this
mechanism, once the service account has the client\'s delegated
credentials, it has access to any service. Thus, great care is needed
with open delegation.

In contrast, with MS-SFU delegation (implemented in S4U2proxy), the
administrator can precisely control the services to which a particular
service can access on behalf a client.[Figure
7-4](single-sign-using-kerberos-java1.html#GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B__CONSTRAINEDDELEGATIONWITHS4U2PROXY-47300C1F)
illustrates this.

<div class="figure" id="GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B__CONSTRAINEDDELEGATIONWITHS4U2PROXY-47300C1F">
Figure 7-4 Constrained Delegation with S4U2proxy

![Description of Figure 7-4
follows](img/jgss_pb_003c.png "Description of Figure 7-4 follows")\
[Description of \"Figure 7-4 Constrained Delegation with
S4U2proxy\"](img_text/jgss_pb_003c.htm)

</div>
<!-- class="figure" -->

<div class="infoboxnote" id="GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B__GUID-E3BFE2DB-1022-4C40-A5E6-9A7CA8223CD0">
Note:

To delegate credentials as specified in the RFCs in this document, you
must use traditional delegation. With constrained delegation, the client
is unable to determine if its own credentials can be delegated because
this is determined by the KDC.

</div>
</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-B54B88B4-087F-4B0D-A28B-C0980D762D5C}

Default Credential Acquisition Model {#JSSEC-GUID-B54B88B4-087F-4B0D-A28B-C0980D762D5C .sect2}
------------------------------------

<div>
Previously we discussed how an application uses the
<span class="apiname">GSSManager.createCredential()</span> method to
populate a <span class="apiname">GSSCredential</span> object with
mechanism specific credentials. The next two sub-sections will focus on
how Java GSS-API mechanisms obtain these credentials. The mechanisms do
not themselves perform a user login. Instead, the login is performed
prior to using Java GSS-API and the credentials are assumed to be stored
in some cache that the mechanism provider is aware of. The
<span class="apiname">GSSManager.createCredential()</span> method merely
obtains references to those credentials and returns them in a
GSS-centric container, the <span class="apiname">GSSCredential</span>.

In Java SE, we impose the restriction that the credentials cache that
Java GSS-API mechanism providers use to obtain these elements must
exclusively be the public and private credential sets in the Subject
that is on the current access control context.

This model has the advantage that credential management is simple and
predictable from the application\'s point of view. An application, given
the right permissions, can purge the credentials in the Subject or renew
them using standard Java API\'s. If it purged the credentials, it would
be sure that the Java GSS-API mechanism would fail, or if it renewed a
time based credential it would be sure that the mechanism would succeed.

Here is the sequence of events relevant to credential acquisition when
the Kerberos V5 mechanism is used by the client application in Figures 3
and 6:

1.  The application invokes a JAAS login, which in turn invokes the
    configured <span class="apiname">Krb5LoginModule</span>
2.  <span class="apiname">Krb5LoginModule</span> obtains a TGT
    (<span class="apiname">KerberosTicket</span>) for the user either
    from the KDC or from an existing ticket cache, and stores this TGT
    in the private credentials set of a Subject
3.  The application retrieves the populated Subject, then calls
    <span class="apiname">Subject.doAs</span>/<span class="apiname">doAsPrivileged</span>
    which places this Subject on the access control context of the
    thread executing <span class="apiname">ClientAction</span>
4.  <span class="apiname">ClientAction</span> calls the
    <span class="apiname">GSSManager.createCredential</span> method,
    passing it the Kerberos V5 OID in
    <span class="apiname">desiredMechs</span>.
5.  GSSManager.createCredential invokes the Kerberos V5 GSS-API
    provider, asking for a Kerberos credential for initiating security
    contexts.
6.  The Kerberos provider obtains the Subject from the current access
    control context, and searches through its private credential set for
    a valid KerberosTicket that represents the TGT for the user.
7.  The KerberosTicket is returned to the GSSManager which stores it in
    a GSSCredential container instance to be returned to the caller.

On the server side, when the Kerberos login is successful in step 2,
Krb5LoginModule stores the KerberosKey for the server in the Subject in
addition to the KerberosTicket. Later on the KerberosKey is retrieved in
steps 5 through 7 and used to decrypt the service ticket that the client
sends.

</div>
</div>
<div class="sect2">
[]{#GUID-7F63948A-0FF3-4818-89E8-B39A1CF4DBB3}

Exceptions to the Model {#JSSEC-GUID-7F63948A-0FF3-4818-89E8-B39A1CF4DBB3 .sect2}
-----------------------

<div>
The default credential acquisition model for Java GSS-API requires
credentials to be present in the current Subject. Typically, the
credentials are placed there after a JAAS login by the application.

There might be cases where an application wishes to use Kerberos
credentials from outside the Subject. It is recommended that such
credentials be read as part of the initial JAAS login, either by
configuring <span class="apiname">Krb5LoginModule</span> to read them,
or by writing a custom login module that reads them. However, some
applications might have constrains that either prevent them from using
JAAS prior to calling Java GSS-API, or force them to use some Kerberos
mechanism provider that does not retrieve credentials from the current
Subject.

The system property `javax.security.auth.useSubjectCredsOnly`{.codeph}
accommodates such cases while still retaining the standard model for
others. This system property serves as a boolean where a value of true
requires that the standard credential acquisition model be followed, and
a value of false permits the provider to use any cache of it choice. The
default value of this property (when it is not set) will be assumed to
be true.

If there is no valid Kerberos credential in the current Subject, and
this property is true, then the Kerberos mechanism throws a
<span class="apiname">GSSException</span>. Setting this property to
false does not necessarily mean that the provider has to use a cache
other than the current Subject, it only gives the provider the latitude
to do so if it wishes.

The Oracle provider for the Kerberos V5 GSS-API mechanism always obtains
credentials from a Subject. If there are no valid credentials in the
current Subject, and this property is set to false, then the provider
attempts to obtain new credentials from a temporary Subject by invoking
a JAAS login itself. It uses the text callback handler for input/output
with the user, and the JAAS configuration entry identified by \"other\"
for the list of modules and options to use.[^Foot 2^](#fn_2){#fn_2}

The Oracle provider for the Kerberos V5 GSS-API mechanism assumes that
one of these modules will be a Kerberos login module. It is possible to
configure the modules listed under \"other\" to read a pre-existing
cache so that the user is not unexpectedly prompted for a password in
the middle of a Java GSS-API call. The new Subject that is populated by
this login is discarded by the Kerberos GSS-API mechanism just as soon
as the required credentials are retrieved from it.

</div>
</div>
<div class="sect2">
[]{#GUID-E478197F-C0D8-4D35-82D8-E52E2B307B9B}

Web Browser Integration {#JSSEC-GUID-E478197F-C0D8-4D35-82D8-E52E2B307B9B .sect2}
-----------------------

<div>
An important class of applications that should be able to capitalize on
Java Single Sign-on are applets. For this discussion we assume that the
browser JRE has all the required packages.

One complication in using applets arises mostly out of the fact that
before an applet can use Java GSS-API, it must perform a JAAS login. The
main problems with this are (a) an increase in the effort required on
the part of the applet developer and (b) unnecessary repeated login by
the same user each time he or she starts an applet.

A good model to solve this problem would be to have the browser (or the
Java Plug-in) perform a JAAS login once at startup. This would provide a
Subject that could always be associated with the access control context
whenever any Java code was run. As a result, the applet code would not
need to perform a JAAS login prior to using Java GSS-API, and the user
login would occur just once.

In the absence of this login functionality in the browser (or Java
Plug-in), applets can still avoid having to perform a JAAS login
themselves. To do so, the applets would have to set the
`javax.security.auth.useSubjectCredsOnly`{.codeph} system property to
false and use a GSS-API mechanism provider that is capable of obtaining
credentials from sources other than current Subject. When using an
Oracle JRE with an Oracle Kerberos GSS-API provider, expect the
mechanism to perform a JAAS login to obtain new credentials as explained
in the previous section. The applet deployer would only need to ensure
that the appropriate modules and options are listed in the entry
\"other\" in the JAAS configuration used by the JRE. This saves the
applet developer from calling into JAAS API\'s directly, but it does not
stop the repeated JAAS login that might happen with each applet the user
runs. However, by configuring the login modules to read a pre-existing
native cache, the deployer can both hide the login from the user, and
minimize the overhead in the multiple logins. (See how this is done for
the JAAS configuration entry `SampleClient`{.codeph} in the [sample
client configuration
entry](single-sign-using-kerberos-java1.html#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E__SAMPLECLIENTCOM.SUN.SECURITY.AUTH.M-37F332E5)
in the section [The Kerberos Login
Module](single-sign-using-kerberos-java1.html#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E).)

</div>
</div>
<div class="sect2">
[]{#GUID-1793ADE8-8B78-4680-A871-063ED761CFF5}

Security Risks {#JSSEC-GUID-1793ADE8-8B78-4680-A871-063ED761CFF5 .sect2}
--------------

<div>
The convenience of single sign-on also introduces new risks. What
happens if a malicious user gains access to your unattended desktop from
where he or she can start applets as you? What happens if malicious
applets sign on as you to services that they are not supposed to?

For the former, we have no solution but to caution you against leaving
your workstation unlocked! For the latter, we have many authorizations
checks in place.

To illustrate some details of the permissions model consider an example
where your browser has performed a JAAS login at startup time and
associated a Subject with all applets that run in it.

The Subject is protected from rogue applets by means of the
<span class="apiname">javax.security.auth.AuthPermission</span> class.
This permission is checked whenever code tries to obtain a reference to
the Subject associated with any access control context.

Even if an applet were given access to a Subject, it needs a
<span class="apiname">javax.security.auth.PrivateCredentialPermission</span>
to actually read the sensitive private credentials stored in it.

Other kinds of checks are to be done by Java GSS-API mechanism providers
as they read credentials and establish security contexts on behalf of
the credential\'s owner. In order to support the Kerberos V5 mechanism,
two new permission classes have been added with the package
<span class="apiname">javax.security.auth.kerberos</span>:

``` {.oac_no_warn dir="ltr"}
ServicePermission(String servicePrinicipal, String action)
DelegationPermission(String principals)
```

As new GSS-API mechanisms are standardized for Java SE, more packages
will be added that contain relevant permission classes for providers of
those mechanisms.

The Kerberos GSS-API mechanism permission checks take place at the
following points in the program\'s execution:

</div>
<div class="sect3">
[]{#GUID-23E25BFC-E77A-495C-8406-897E9D124395}

### Credential Acquisition {#JSSEC-GUID-23E25BFC-E77A-495C-8406-897E9D124395 .sect3}

<div>
The <span class="apiname">GSSManager.createCredential()</span> method
obtains mechanism specific credential elements from a cache such as the
current Subject and stores them in a
<span class="apiname">GSSCredential</span> container. Allowing applets
to acquire <span class="apiname">GSSCredential</span> freely, even if
they cannot use them to do much, is undesirable. Doing so leaks
information about the existence of user and service principals. Thus,
before an application can acquire a
<span class="apiname">GSSCredential</span> with any Kerberos credential
elements in it, a <span class="apiname">ServicePermission</span> check
is made.

On the client side, a successful
<span class="apiname">GSSCredential</span> acquisition implies that a
TGT has been accessed from a cache. Thus the following
<span class="apiname">ServicePermission</span> is checked:

``` {.oac_no_warn dir="ltr"}
ServicePermission("krbtgt/EXAMPLE.COM@EXAMPLE.COM", "initiate");
```

The service principal `krbtgt/EXAMPLE.COM@EXAMPLE.COM`{.codeph}
represents the ticket granting service (TGS) in the Kerberos realm
`EXAMPLE.COM`{.codeph}, and the action \"initiate\" suggests that a
ticket to this service is being accessed. The TGS service principal will
always be used in this permission check at the time of client side
credential acquisition.

On the server side, a successful
<span class="apiname">GSSCredential</span> acquisition implies that a
secret key has been accessed from a cache. Thus the following
<span class="apiname">ServicePermission</span> is checked:

``` {.oac_no_warn dir="ltr"}
ServicePermission("nfs/bar.example.com@EXAMPLE.COM", "accept");
```

Here the service principal `nfs/bar.example.com`{.codeph} represents the
Kerberos service principal and the action \"accept\" suggests that the
secret key for this service is being requested.

</div>
</div>
<div class="sect3">
[]{#GUID-5BB1D535-B4A3-403A-91CF-8A5B98B6DB0E}

### Context Establishment {#JSSEC-GUID-5BB1D535-B4A3-403A-91CF-8A5B98B6DB0E .sect3}

<div>
An applet that has permissions to contact a particular server, say the
LDAP server, must not instead contact a different server such as the FTP
server. Of course, the applet might be restricted from doing so with the
help of <span class="apiname">SocketPermission</span>. However, it is
possible to use <span class="apiname">ServicePermission</span> to
restrict it from authenticating using your identity, even if the network
connection was permitted.

When the Kerberos mechanism provider is about to initiate context
establishment it checks the
<span class="apiname">ServicePermission</span>:

``` {.oac_no_warn dir="ltr"}
ServicePermission("ftp@EXAMPLE.COM", "initiate");
```

This check prevents unauthorized code from obtaining and using a
Kerberos service ticket for the principal `ftp@EXAMPLE.COM`{.codeph}.

Providing limited access to specific service principals using this
permission is still dangerous. Downloaded code is allowed to communicate
back with the host it originated from. A malicious applet could send
back the initial GSS-API output token that contains a
<span class="apiname">KerberosTicket</span> encrypted in the target
service principal\'s long-term secret key, thus exposing it to an
offline dictionary attack. For this reason it is not advisable to grant
any \"initiate\" <span class="apiname">ServicePermission</span> to code
downloaded from untrusted sites.

On the server side, the permission to use the secret key to accept
incoming security context establishment requests is already checked
during credential acquisition. Hence, no checks are made in the context
establishment stage.

</div>
</div>
<div class="sect3">
[]{#GUID-3D1AFF31-323B-4DD6-829A-B7205FA11161}

### Credential Delegation {#JSSEC-GUID-3D1AFF31-323B-4DD6-829A-B7205FA11161 .sect3}

<div>
An applet that has permission to establish a security context with a
server on your behalf also has the ability to request that your
credentials be delegated to that server. But not all servers are trusted
to the extent that your credentials can be delegated to them. Thus,
before a Kerberos provider obtains a delegated credential to send to the
peer, it checks the following permission:

``` {.oac_no_warn dir="ltr"}
DelegationPermission(" \"ftp@EXAMPLE.COM\" \"krbtgt/EXAMPLE.COM@EXAMPLE.COM\" ");
```

This permission allows the Kerberos service principal ftp@EXAMPLE.COM to
receive a forwarded TGT (represented by the ticket granting service
krbtgt/EXAMPLE.COM@EXAMPLE.COM).[^Foot 3^](#fn_3){#fn_3}

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-4A2151A0-B23A-4B2E-BFEE-A17545262B48}

Conclusions {#JSSEC-GUID-4A2151A0-B23A-4B2E-BFEE-A17545262B48 .sect2}
-----------

<div>
In this paper we have presented a framework to enable single sign-on in
Java. This requires sharing of credentials between JAAS which does the
initial authentication to obtain credentials, and Java GSS-API which
uses those credentials to communicate securely over the wire. We have
focused on Kerberos V5 as the underlying security mechanism, but JAAS\'s
stackable architecture and Java GSS-API\'s multi-mechanism nature allow
us to use any number of different mechanisms simultaneously.

The Kerberos login module for JAAS is capable of reading native caches
so that users do not have to authenticate themselves beyond desktop
login on platforms that support Kerberos. Moreover, the Kerberos V5
mechanism for Java GSS-API allows credentials to be delegated which
enables single sign-on in multi-tier environments.

Finally, a number of permissions checks are shown to prevent the
unauthorized use of the single-sign on features provided by Kerberos.

</div>
</div>
<div class="sect2">
[]{#GUID-D65B3B0F-2689-4B4E-BAAD-A9E0D3571A84}

Acknowledgements {#JSSEC-GUID-D65B3B0F-2689-4B4E-BAAD-A9E0D3571A84 .sect2}
----------------

<div>
We thank Gary Ellison, Charlie Lai, and Jeff Nisewanger for their
contribution at each stage of the Kerberos single sign-on project. JAAS
1.0 was implemented by Charlie as an optional package for Kestrel (J2SE
1.3). Gary has been instrumental in designing the permissions model for
the Kerberos Java GSS-API mechanism. We are grateful to Bob Scheifler
for his feedback on integrating JAAS 1.0 into Merlin and to Tim Blackman
for the KeyStoreLoginModule and CallbackHandler implementations. We also
thank Bruce Rich, Tony Nadalin, Thomas Owusu and Yanni Zhang for their
comments and suggestions. We thank Mary Dageforde for the documentation
and tutorials. Sriramulu Lakkaraju, Stuart Ke and Shital Shisode
contributed tests for the projects. Maxine Erlund provided management
support for the project.

</div>
</div>
<div class="sect2">
[]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B}

References {#JSSEC-GUID-67712665-922E-4947-8103-0AAE9C2AAC2B .sect2}
----------

<div>
1.  [Neuman, Clifford and Tso, Theodore (1994). Kerberos: An
    Authentication Service for Computer Networks, IEEE Communications,
    volume 39 pages
    33-38]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-01}
2.  [J.Kohl and C.Neuman. The Kerberos Network Authentication Service
    (V5) Internet Engineering Task Force, September 1993 [Request for
    Comments
    1510](http://www.ietf.org/rfc/rfc1510.txt)]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-02}
3.  [V. Samar and C. Lai. Making Login Services Independent from
    Authentication Technologies. In Proceedings of the SunSoft
    Developer\'s Conference,
    March 1996.]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-03}
4.  [X/Open Single Sign-On Service (XSSO) - Pluggable Authentication.
    Preliminary Specification P702, The Open Group, June 1997.
    [http://www.opengroup.org](http://www3.opengroup.org/)]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-04}
5.  [A Smart Card Login Module for Java Authentication and Authorization
    Service.
    [http://www.gemplus.com/techno/smartjaas/index.html](http://www.gemalto.com/gemplus/index.html)]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-05}
6.  [J. Linn. Generic Security Service Application Program
    Interface,Version 2. Internet Engineering Task Force, January 2000
    [Request for Comments
    2743](http://www.ietf.org/rfc/rfc2743.txt)]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-06}
7.  [J. Linn. The Kerberos Version 5 GSS-API Mechanism. Internet
    Engineering Task Force, June 1996 [Request for Comments
    1964](http://www.ietf.org/rfc/rfc1964.txt)]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-07}
8.  [C.Adams. The Simple Public-Key GSS-API Mechanism (SPKM). Internet
    Engineering Task Force, October 1996 [Request for Comments
    2025](http://www.ietf.org/rfc/rfc2025.txt)]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-08}
9.  [J. Kabat and M.Upadhyay. Generic Security Service API Version 2:
    Java Bindings. Internet Engineering Task Force, January 1997
    [Request for Comments
    2853](http://www.ietf.org/rfc/rfc2853.txt)]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-09}
10. [JSR 000072 Generic Security Services
    API]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-10}
11. [[Java Platform, Standard Edition API
    Specification](https://docs.oracle.com/javase/10/docs/api/overview-summary.html)]{#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B__SSO-KERBEROS-11}

</div>
</div>

------------------------------------------------------------------------

\

Footnote Legend

Footnote 1: The GSS-API Kerberos mechanism performs client
authentication at the minimum.\
Footnote 2: Actually it first tries to use the JAAS configuration entry
`com.sun.security.jgss.initiate`{.codeph} for the client and
`com.sun.security.jgss.accept`{.codeph} for the server and falls back on
the entry for \"other\", if these entries are missing. This gives system
administrators some additional control over its behavior.\
Footnote 3: The use of two principal names in this permission allows for
finer grained delegation such as proxy tickets for specific services
unlike a carte blanche forwarded TGT. Even though the GSS-API does not
allow for proxy tickets, another API such as JSSE might support this
idea at some point in the future.\

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
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| ----------------- -- | o | ass="icon">Contents< |
|             [![Previ | g | /span>](toc.htm)     |
| ous](../../dcommon/g | o |   -- --------------- |
| ifs/leftnav.gif)\    | ] | -------------------- |
|                      | ( | -------------------- |
|                      | . | ---                  |
|            [![Next]( | . |                      |
| ../../dcommon/gifs/r | / |                      |
| ightnav.gif)\        | . |                      |
|                      | . |                      |
|                      | / |                      |
|    <span class="icon | d |                      |
| ">Previous</span>](r | c |                      |
| elated-documentation | o |                      |
| 1.htm)   <span class | m |                      |
| ="icon">Next</span>] | m |                      |
| (advanced-security-p | o |                      |
| rogramming-java-se-a | n |                      |
| uthentication-secure | / |                      |
| -communication-and-s | g |                      |
| ingle-sign1.htm)     | i |                      |
|   ------------------ | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| ------- ------------ | o |                      |
| -------------------- | r |                      |
| -------------------- | a |                      |
| -------------------- | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| ----------------- -- | . |                      |
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
