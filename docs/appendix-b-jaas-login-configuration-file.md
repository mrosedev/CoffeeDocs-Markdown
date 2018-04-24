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

  ------------------------------------------------------------------------------------------------------------- ----------------------------------------------------- --
                                  [![Previous](../../dcommon/gifs/leftnav.gif)\                                      [![Next](../../dcommon/gifs/rightnav.gif)\       
   <span class="icon">Previous</span>](java-authentication-and-authorization-service-jaas-reference-guide.htm)   <span class="icon">Next</span>](jaas-tutorials.htm)  
  ------------------------------------------------------------------------------------------------------------- ----------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E}<!-- End Header -->

Appendix B: JAAS Login Configuration File {#JSSEC-GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E .sect1}
=========================================

<div>
JAAS authentication is performed in a pluggable fashion, so Java
applications can remain independent from underlying authentication
technologies. Configuration information such as the desired
authentication technology is specified at runtime. The source of the
configuration information (for example, a file or a database) is up to
the current
[<span class="apiname">javax.security.auth.login.Configuration</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
implementation. The default `Configuration`{.codeph} implementation,
`ConfigFile`{.codeph}, gets its configuration information from login
configuration files. For details about the default login
`Configuration`{.codeph} implementation provided with JAAS, see the
[`com.sun.security.auth.login.ConfigFile`{.codeph}](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/login/ConfigFile.html)
class.

</div>
<div class="sect2">
[]{#GUID-9713B697-EFED-49A1-9E15-8039AD04458B}

Login Configuration File Structure and Contents {#JSSEC-GUID-9713B697-EFED-49A1-9E15-8039AD04458B .sect2}
-----------------------------------------------

<div>
A login configuration file consists of one or more entries, each
specifying which underlying authentication technology should be used for
a particular application or applications. The structure of each entry is
the following:

``` {.oac_no_warn dir="ltr"}
<name used by application to refer to this entry> { 
    <LoginModule> <flag> <LoginModule options>;
    <optional additional LoginModules, flags and options>;
};
```

Thus, each login configuration file entry consists of a name followed by
one or more <span class="apiname">LoginModule</span>-specific entries,
where each <span class="apiname">LoginModule</span>-specific entry is
terminated by a semicolon and the entire group of
<span class="apiname">LoginModule</span>-specific entries is enclosed in
braces. Each configuration file entry is terminated by a semicolon.

<div class="example" id="GUID-9713B697-EFED-49A1-9E15-8039AD04458B__GUID-8B49A958-1B17-4713-AB56-42F99D6B8247">
Example 6-1 Login Configuration File for JAAS Authentication Tutorial

As an example, the login configuration file used for the [JAAS
Authentication
Tutorial](jaas-authentication-tutorial.htm#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
tutorial contains just one entry, which is

``` {.oac_no_warn dir="ltr"}
Sample {
   sample.module.SampleLoginModule required debug=true;
};
```

Here, the entry is named `Sample`{.codeph} and that is the name that the
JAAS Authentication tutorial application (`SampleAcn.java`{.codeph})
uses to refer to this entry. The entry specifies that the
<span class="apiname">LoginModule</span> to be used to do the user
authentication is the `SampleLoginModule`{.codeph} in the
`sample.module`{.codeph} package and that this
`SampleLoginModule`{.codeph} is required to \"succeed\" in order for
authentication to be considered successful. The
`SampleLoginModule`{.codeph} succeeds only if the name and password
supplied by the user are the ones it expects (`testUser`{.codeph} and
`testPassword`{.codeph}, respectively).

The <span class="bold">name</span> for an entry in a login configuration
file is the name that applications use to refer to the entry when they
instantiate a <span class="apiname">LoginContext</span>, as described in
[JAAS Authentication
Tutorial](jaas-authentication-tutorial.htm#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
in the JAAS authentication tutorial. The name can be whatever name the
application developer wishes to use. Here, the term \"application\"
refers to whatever code does the JAAS login.

The specified <span class="apiname">LoginModules</span> (described
below) are used to control the authentication process. Authentication
proceeds down the list in the exact order specified, as described in the
[<span class="apiname">Configuration</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
class.

The subparts of each <span class="apiname">LoginModule</span>-specific
entry are the following:

-   <span class="bold">LoginModule</span>: This specifies a class
    implementing the desired authentication technology. Specifically,
    the class must be a subclass of the
    <span class="apiname">LoginModule</span> class, which is in the
    `javax.security.auth.spi`{.codeph} package. A typical
    <span class="apiname">LoginModule</span> may prompt for and verify a
    user name and password, as is done by the
    `SampleLoginModule`{.codeph} (in the `sample.module`{.codeph}
    package) used for these tutorials. Any vendor can provide a
    LoginModule implementation that you can use. Some implementations
    are supplied with the JRE from Oracle. You can view the reference
    documentation for the various
    <span class="apiname">LoginModule</span>s, all in the
    `com.sun.security.auth`{.codeph} package:

    -   [<span class="apiname">JndiLoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/JndiLoginModule.html)
    -   [<span class="apiname">KeyStoreLoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/KeyStoreLoginModule.html)
    -   [<span class="apiname">Krb5LoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/Krb5LoginModule.html)
    -   [<span class="apiname">NTLoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/NTLoginModule.html)
    -   [<span class="apiname">UnixLoginModule</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/UnixLoginModule.html)

-   <span class="bold">flag</span>: The flag value indicates whether
    success of the preceding <span class="apiname">LoginModule</span> is
    `required`{.codeph}, `requisite`{.codeph}, `sufficient`{.codeph}, or
    `optional`{.codeph}. If there is just one
    <span class="apiname">LoginModule</span>-specific entry, as there is
    in our tutorials, then the flag for it should be \"required\". The
    options are described in more detail in the
    [<span class="apiname">Configuration</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
    class.

-   <span class="bold">LoginModule options</span>: If the specified
    <span class="apiname">LoginModule</span> implementation has options
    that can be set, you specify any desired option values here. This is
    a space-separated list of values which are passed directly to the
    underlying <span class="apiname">LoginModule</span>. Options are
    defined by the <span class="apiname">LoginModule</span> itself, and
    control the behavior within it. For example, a
    <span class="apiname">LoginModule</span> may define options to
    support debugging/testing capabilities.

    The correct way to specify options in the configuration file is by
    using a name-value pairing, for example `debug=true`{.codeph}, where
    the option name (in this case, `debug`{.codeph}) and value (in this
    case, `true`{.codeph}) should be separated by an equals symbol.

</div>
<!-- class="example" -->

<div class="example" id="GUID-9713B697-EFED-49A1-9E15-8039AD04458B__GUID-B4E5B990-335D-4505-984C-23EA6B12E626">
Example 6-2 Login Configuration File Demonstrating required, sufficient,
requisite, and optional Flags

The following is a sample login configuration file that demonstrates the
`required`{.codeph}, `sufficient`{.codeph}, `requisite`{.codeph}, and
`optional`{.codeph} flags. See the
[`Configuration`{.codeph}](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/login/Configuration.html)
class for more information about these flags.

``` {.oac_no_warn dir="ltr"}
Login1 {
       sample.SampleLoginModule required debug=true;
    };

    Login2 {
       sample.SampleLoginModule required;
       com.sun.security.auth.module.NTLoginModule sufficient;
       com.foo.SmartCard requisite debug=true;
       com.foo.Kerberos optional debug=true;
    };
```

The application <span class="bold">Login1</span> only has one configured
`LoginModule`{.codeph}, `SampleLoginModule`{.codeph}. Therefore, an
attempt by <span class="bold">Login1</span> to authenticate a subject
(user or service) will be successful if and only if the
`SampleLoginModule`{.codeph} succeeds.

The authentication logic for the application
<span class="bold">Login2</span> is easier to explain with the following
table:

<div class="tblformalwide" id="GUID-9713B697-EFED-49A1-9E15-8039AD04458B__GUID-08C8B04B-2735-4218-AA3B-DDE4F7514A5F">
Table 6-1 Login2 Authentication Status

<table style="width:100%;">
<colgroup>
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
<col style="width: 10%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Module Class</th>
<th style="text-align: left;">Flag</th>
<th style="text-align: left;">Authentication Attempt 1</th>
<th style="text-align: left;">Authentication Attempt 2</th>
<th style="text-align: left;">Authentication Attempt 3</th>
<th style="text-align: left;">Authentication Attempt 4</th>
<th style="text-align: left;">Authentication Attempt 5</th>
<th style="text-align: left;">Authentication Attempt 6</th>
<th style="text-align: left;">Authentication Attempt 7</th>
<th style="text-align: left;">Authentication Attempt 8</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><p><code class="codeph">SampleLoginModule</code></p></td>
<td style="text-align: left;"><p>required</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p><code class="codeph">NTLoginModule</code></p></td>
<td style="text-align: left;"><p>sufficient</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>SmartCard</p></td>
<td style="text-align: left;"><p>requisite</p></td>
<td style="text-align: left;"><p>*</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>*</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>fail</p></td>
</tr>
<tr class="even">
<td style="text-align: left;"><p>Kerberos</p></td>
<td style="text-align: left;"><p>optional</p></td>
<td style="text-align: left;"><p>*</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>*</p></td>
<td style="text-align: left;"><p>*</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>*</p></td>
</tr>
<tr class="odd">
<td style="text-align: left;"><p>Overall Authentication</p></td>
<td style="text-align: left;"><p>not applicable</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>pass</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
<td style="text-align: left;"><p>fail</p></td>
</tr>
</tbody>
</table>

</div>
<!-- class="inftblhruleinformal" -->

\* = trivial value due to control returning to the application because a
previous <span class="italic">requisite</span> module failed or a
previous <span class="italic">sufficient</span> module succeeded.

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect2">
[]{#GUID-1D5D78E1-4771-43B7-AEED-1D427A7044F0}

Where to Specify Which Login Configuration File Should Be Used {#JSSEC-GUID-1D5D78E1-4771-43B7-AEED-1D427A7044F0 .sect2}
--------------------------------------------------------------

<div>
The configuration file to be used can be specified in one of two ways:

1.  On the command line.

    You can use a `-Djava.security.auth.login.config`{.codeph}
    interpreter command line argument to specify the login configuration
    file that should be used. We use this approach for all the
    tutorials. For example, we run our `SampleAcn`{.codeph} application
    in the [JAAS Authentication
    Tutorial](jaas-authentication-tutorial.htm#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
    using the following command, which specifies that the configuration
    file is the `sample_jaas.config`{.codeph} file in the current
    directory:

    ``` {.oac_no_warn dir="ltr"}
    java -Djava.security.auth.login.config==sample_jaas.config sample.SampleAcn
    ```

    <div class="infoboxnote" id="GUID-1D5D78E1-4771-43B7-AEED-1D427A7044F0__GUID-2DD19A7E-59D7-40A6-AC26-ACD6E8AD9583">
    Note:

    If you use a single equals sign (`=`{.codeph}) with the
    `java.security.auth.login.config`{.codeph} system property, then the
    configurations specified by both this system property and the
    `java.security` file are used.

    </div>
2.  In the Java Security Properties file.

    An alternate approach to specifying the location of the login
    configuration file is to indicate its URL as the value of a
    `login.config.url.n`{.codeph} property in the security properties
    file. The Security Properties file is the `java.security`{.codeph}
    file located in the `conf/security`{.codeph} directory of the JDK.

    Here, `n`{.codeph} indicates a consecutively-numbered integer
    starting with 1. Thus, if desired, you can specify more than one
    login configuration file by indicating one file\'s URL for the
    `login.config.url.1`{.codeph} property, a second file\'s URL for the
    `login.config.url.2`{.codeph} property, and so on. If more than one
    login configuration file is specified (that is, if `n`{.codeph} \>
    1), then the files are read and concatenated into a single
    configuration.

    Here is an example of what would need to be added to the security
    properties file in order to indicate the
    `sample_jaas.config`{.codeph} login configuration file used by this
    tutorial. This example assumes the file is in the
    `C:\AcnTest`{.codeph} directory on Windows:

    ``` {.oac_no_warn dir="ltr"}
    login.config.url.1=file:C:/AcnTest/sample_jaas.config
    ```

    (Note that URLs always use forward slashes, regardless of what
    operating system the user is running.)

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
| ----------- -------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| ----- --             | L |             <span cl |
|                      | o | ass="icon">Contents< |
|               [![Pre | g | /span>](toc.htm)     |
| vious](../../dcommon | o |   -- --------------- |
| /gifs/leftnav.gif)\  | ] | -------------------- |
|                      | ( | -------------------- |
|                  [![ | . | ---                  |
| Next](../../dcommon/ | . |                      |
| gifs/rightnav.gif)\  | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](j | / |                      |
| ava-authentication-a | d |                      |
| nd-authorization-ser | c |                      |
| vice-jaas-reference- | o |                      |
| guide.htm)   <span c | m |                      |
| lass="icon">Next</sp | m |                      |
| an>](jaas-tutorials. | o |                      |
| htm)                 | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| -------------------- | s |                      |
| ----------- -------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| ----- --             | a |                      |
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
