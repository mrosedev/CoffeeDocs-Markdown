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

  ------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------- --
                               [![Previous](../../dcommon/gifs/leftnav.gif)\                                                                              [![Next](../../dcommon/gifs/rightnav.gif)\                                                  
   <span class="icon">Previous</span>](part-v-secure-authentication-using-spnego-java-gss-mechanism.htm)   <span class="icon">Next</span>](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm)  
  ------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-996F729E-5FEA-4E29-A32A-78FB510B2D80}<!-- End Header -->

Part VI: HTTP/SPNEGO Authentication {#JSSEC-GUID-996F729E-5FEA-4E29-A32A-78FB510B2D80 .sect1}
===================================

<div>
</div>
<div class="sect2">
[]{#GUID-2978DB58-6217-4E29-95EF-2C1F25F7C37F}

Exercise 9: Using HTTP/SPNEGO Authentication {#JSSEC-GUID-2978DB58-6217-4E29-95EF-2C1F25F7C37F .sect2}
--------------------------------------------

<div>
</div>
<div class="sect3">
[]{#GUID-89457AC9-89FE-4934-A6F3-B03D72D95AA7}

### What is HTTP SPNEGO {#JSSEC-GUID-89457AC9-89FE-4934-A6F3-B03D72D95AA7 .sect3}

<div>
HTTP SPNEGO supports the Negotiate authentication scheme in an HTTP
communication. SPNEGO supports types of authentication:

<div class="section">
Web Authentication

The Web Server responds with

</div>
<!-- class="section" -->

``` {.oac_no_warn dir="ltr"}
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Negotiate
```

the client will need to send a header like

``` {.oac_no_warn dir="ltr"}
Authorization: Negotiate YY.....
```

to authenticate itself to the server

<div class="section">
Proxy Authentication

The Web Server responses with

</div>
<!-- class="section" -->

``` {.oac_no_warn dir="ltr"}
HTTP/1.1 407 Proxy Authentication Required
Proxy-Authenticate: Negotiate
```

the client will need to send a header like

``` {.oac_no_warn dir="ltr"}
Proxy-Authorization: Negotiate YY.....
```

to authenticate itself to the proxy server.

This feature supports both types of authentication.

</div>
</div>
<div class="sect3">
[]{#GUID-1101592C-854C-4CB2-B46C-CE3EE8652FB0}

### How to use HTTP/SPNEGO Authentication {#JSSEC-GUID-1101592C-854C-4CB2-B46C-CE3EE8652FB0 .sect3}

<div>
There is no new public API function involved in the new feature, but
several configurations are needed to perform a success communication:

<div class="section">
Kerberos 5 Configuration

Since the SPNEGO mechanism will call JGSS, which in turns calls the
Kerberos V5 login module to do real works. Kerberos 5 configurations are
needed. This includes the following:

-   Some way to provide Kerberos configurations. This can be achieved
    with the Java system property `java.security.krb5.conf`{.codeph}.
    For example:

    ``` {.oac_no_warn dir="ltr"}
    java -Djava.security.krb5.conf=krb5.conf \
         -Djavax.security.auth.useSubjectCredsOnly=false \
         ClassName
    ```

    A JAAS config file denoting what login module to use. HTTP SPNEGO
    codes will look for the standard entry named
    `com.sun.security.jgss.krb5.initiate`{.codeph}.

    For example, you can provide a file `spnegoLogin.conf`{.codeph}:

    ``` {.oac_no_warn dir="ltr"}
    com.sun.security.jgss.krb5.initiate {
        com.sun.security.auth.module.Krb5LoginModule
            required useTicketCache=true;
    };
    ```

    and run java with:

    ``` {.oac_no_warn dir="ltr"}
    java -Djava.security.krb5.conf=krb5.conf \
         -Djava.security.auth.login.config=spnegoLogin.conf \
         -Djavax.security.auth.useSubjectCredsOnly=false \
         ClassName
    ```

</div>
<!-- class="section" -->

<div class="section">
User Name and Password Retrieval

Just like any other HTTP authentication scheme, the client can provide a
customized <span class="apiname">java.net.Authenticator</span> to feed
user name and password to the HTTP SPNEGO module
<span class="bold">if</span> they are needed (i.e. there is no
credential cache available). The only authentication information needed
to be checked in your <span class="apiname">Authenticator</span> is the
scheme which can be retrieved with
<span class="apiname">getRequestingScheme()</span>. The value should be
\"Negotiate\".

This means your <span class="apiname">Authenticator</span>
implementation will look like:

``` {.oac_no_warn dir="ltr"}
class MyAuthenticator extends Authenticator {

        public PasswordAuthentication getPasswordAuthentication () {
            if (getRequestingScheme().equalsIgnoreCase("negotiate")) {
                String krb5user;
                char[] krb5pass;
                // get krb5user and krb5pass in your own way
                ....
                return (new PasswordAuthentication (krb5user,
                            krb5pass));
            } else {
                ....
            }
        }
    }
```

<div class="infoboxnote" id="GUID-1101592C-854C-4CB2-B46C-CE3EE8652FB0__GUID-EE01F3DE-A2B0-4137-8EBD-EADFE95AB71E">
Note:

According to the specification of
<span class="apiname">java.net.Authenticator</span>, it\'s designed to
get the user name and password at the same time, so do not specify
`principal=xxx`{.codeph} in the JAAS config file.

</div>
</div>
<!-- class="section" -->

<div class="section">
Scheme Preference

The client can still provide system property
<span class="apiname">http.auth.preference</span> to denote that a
certain scheme should always be used as long as the server request for
it. You can use \"SPNEGO\" or \"Kerberos\" for this system property.
\"SPNEGO\" means you prefer to response the Negotiate scheme using the
GSS/SPNEGO mechanism; \"Kerberos\" means you prefer to response the
Negotiate scheme using the GSS/Kerberos mechanism. Normally, when
authenticating against a Microsoft product, you can use \"SPNEGO\". The
value \"Kerberos\" also works for Microsoft servers. It\'s only needed
when you encounter a server which knows Negotiate but doesn\'t know
about SPNEGO.

If `http.auth.preference`{.codeph} is not set, the internal order chosen
is:

-   GSS/SPNEGO -\> Digest -\> NTLM -\> Basic

Notice that Kerberos does not appear in this list, since whenever
Negotiate is supported, GSS/SPNEGO is always chosen.

</div>
<!-- class="section" -->

<div class="section">
Fallback

If the server has provided more than one authentication scheme
(including Negotiate), according to the processing order mentioned in
the last section, Java will try to challenge the Negotiate scheme.
However, if the protocol cannot be established successfully (for
example, the Kerberos configuration is not correct, or the server\'s
hostname is not recorded in the KDC principal DB, or the user name and
password provided by <span class="apiname">Authenticator</span> is
wrong), then the second strongest scheme will be automatically used.

<div class="infoboxnote" id="GUID-1101592C-854C-4CB2-B46C-CE3EE8652FB0__GUID-2FE4CFC7-2814-49D2-AE82-53932203725E">
Note:

If `http.auth.preference`{.codeph} is set to SPNEGO or Kerberos, then
SPNEGO assumes you only want to try the Negotiate scheme even if it
fails. SPNEGO will not fallback to any other scheme and your program
will throw an <span class="apiname">IOException</span> saying it
received a 401 or 407 error from the HTTP response.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-05B34286-D0B6-4C35-B0BF-C98CD9F7E1D2}

### HTTP/SPNEGO Authentication Example {#JSSEC-GUID-05B34286-D0B6-4C35-B0BF-C98CD9F7E1D2 .sect3}

<div>
Assume that you have an IIS Server running on a Windows Server within an
Active Directory. A web page on this server is configured to be
protected by Integrated Windows Authentication. This means the server
will prompt for both Negotiate and NTLM authentication.

You need to prepare these files to get the protected file:

<div class="section">
RunHttpSpnego.java

``` {.oac_no_warn dir="ltr"}
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.Authenticator;
import java.net.PasswordAuthentication;
import java.net.URL;

public class RunHttpSpnego {

    static final String kuser = "username"; // your account name
    static final String kpass = "password"; // your password for the account

    static class MyAuthenticator extends Authenticator {
        public PasswordAuthentication getPasswordAuthentication() {
            // I haven't checked getRequestingScheme() here, since for NTLM
            // and Negotiate, the usrname and password are all the same.
            System.err.println("Feeding username and password for " + getRequestingScheme());
            return (new PasswordAuthentication(kuser, kpass.toCharArray()));
        }
    }

    public static void main(String[] args) throws Exception {
        Authenticator.setDefault(new MyAuthenticator());
        URL url = new URL(args[0]);
        InputStream ins = url.openConnection().getInputStream();
        BufferedReader reader = new BufferedReader(new InputStreamReader(ins));
        String str;
        while((str = reader.readLine()) != null)
            System.out.println(str);
    }
}
```

</div>
<!-- class="section" -->

<div class="section">
krb.conf

``` {.oac_no_warn dir="ltr"}
[libdefaults]
    default_realm = AD.LOCAL
[realms]
    AD.LOCAL = {
        kdc = kdc.ad.local
    }
```

</div>
<!-- class="section" -->

<div class="section">
login.conf

``` {.oac_no_warn dir="ltr"}
com.sun.security.jgss.krb5.initiate {
  com.sun.security.auth.module.Krb5LoginModule required  doNotPrompt=false useTicketCache=true;
};
```

</div>
<!-- class="section" -->

<div class="section">
Compiling and Running the Example

1.  Compile `RunHttpSpnego.java`.

2.  Run `RunHttpSpnego.java`:

    ``` {.oac_no_warn dir="ltr"}
    java -Djava.security.krb5.conf=krb5.conf \
        -Djava.security.auth.login.config=login.conf \
        -Djavax.security.auth.useSubjectCredsOnly=false \
        RunHttpSpnego \
        http://www.ad.local/hello/hello.html
    ```

    You will see the following:

    ``` {.oac_no_warn dir="ltr"}
    Feeding username and password for Negotiate 
    <h1>Hello, You got me!</h1>
    ```

    In fact, if you are running on a Windows machine as a domain user,
    or, you are running on a Linux or Solaris machine that has already
    issued the kinit command and got the credential cache. The class
    `MyAuthenticator`{.codeph} will be completely ignored, and the
    output will be simply:

    ``` {.oac_no_warn dir="ltr"}
    <h1>Hello, You got me!</h1>
    ```

    which shows the user name and password are not consulted. This is
    the so-called Single Sign-On.

    Also, you can just run

    ``` {.oac_no_warn dir="ltr"}
    java RunHttpSpnego http://www.ad.local/hello/hello.html
    ```

    to see how the fallback is done, in which case you will see

    ``` {.oac_no_warn dir="ltr"}
    Feeding username and password for ntlm
    <h1>Hello, You got me!</h1>
    ```

</div>
<!-- class="section" -->

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
| -------------------- | a |       [![Go To Table |
| ----- -------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| -------------------- | o | ass="icon">Contents< |
| -------------------- | g | /span>](toc.htm)     |
| -------------------- | o |   -- --------------- |
| ----- --             | ] | -------------------- |
|                      | ( | -------------------- |
|            [![Previo | . | ---                  |
| us](../../dcommon/gi | . |                      |
| fs/leftnav.gif)\     | / |                      |
|                      | . |                      |
|                      | . |                      |
|                      | / |                      |
|               [![Nex | d |                      |
| t](../../dcommon/gif | c |                      |
| s/rightnav.gif)\     | o |                      |
|                      | m |                      |
|                      | m |                      |
|                      | o |                      |
|    <span class="icon | n |                      |
| ">Previous</span>](p | / |                      |
| art-v-secure-authent | g |                      |
| ication-using-spnego | i |                      |
| -java-gss-mechanism. | f |                      |
| htm)   <span class=" | s |                      |
| icon">Next</span>](s | / |                      |
| ource-code-advanced- | o |                      |
| security-programming | r |                      |
| -java-se-authenticat | a |                      |
| ion-secure-communica | c |                      |
| tion-and-single-sig. | l |                      |
| htm)                 | e |                      |
|   ------------------ | . |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| -------------------- | ) |                      |
| ----- -------------- | { |                      |
| -------------------- | . |                      |
| -------------------- | c |                      |
| -------------------- | o |                      |
| -------------------- | p |                      |
| -------------------- | y |                      |
| -------------------- | r |                      |
| ----- --             | i |                      |
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
