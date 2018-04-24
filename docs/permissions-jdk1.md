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

  --------------------------------------------------------------------------------- --------------------------------------------------------------- --
                    [![Previous](../../dcommon/gifs/leftnav.gif)\                             [![Next](../../dcommon/gifs/rightnav.gif)\            
   <span class="icon">Previous</span>](java-security-standard-algorithm-names.htm)   <span class="icon">Next</span>](troubleshooting-security.htm)  
  --------------------------------------------------------------------------------- --------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95}<!-- End Header -->

Permissions in the JDK {#JSSEC-GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 .sect1}
======================

<div>
A permission represents access to a system resource. In order for a
resource access to be allowed for an applet (or an application running
with a security manager), the corresponding permission must be
explicitly granted to the code attempting the access.

A permission typically has a name (often referred to as a \"target
name\") and, in some cases, a comma-separated list of one or more
actions. For example, the following code creates a
`FilePermission`{.codeph} object representing read access to the file
named `abc`{.codeph} in the `/tmp`{.codeph} directory:

``` {.codeblock dir="ltr"}
perm = new java.io.FilePermission("/tmp/abc", "read");
```

Here, the target name is \"`/tmp/abc`{.codeph}\" and the action string
is \"`read`{.codeph}\".

<div class="infoboxnote" id="GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95__GUID-832B417C-6149-414D-AB1A-4424471E317F">
Important:

The above statement creates a permission object. A permission object
represents, but does not grant access to, a system resource. Permission
objects are constructed and assigned (\"granted\") to code based on the
policy in effect. When a permission object is assigned to some code,
that code is granted the permission to access the system resource
specified in the permission object, in the specified manner. A
permission object may also be constructed by the current security
manager when making access decisions. In this case, the (target)
permission object is created based on the requested access, and checked
against the permission objects granted to and held by the code making
the request.

</div>
The policy for a Java application environment is represented by a Policy
object. In the `"JavaPolicy"`{.codeph} Policy implementation, the policy
can be specified within one or more policy configuration files. The
policy file(s) specify what permissions are allowed for code from
specified code sources. The following is a sample policy file entry that
grants code from the `/home/sysadmin`{.codeph} directory read access to
the file `/tmp/abc`{.codeph}:

``` {.codeblock dir="ltr"}
grant codeBase "file:/home/sysadmin/" {
    permission java.io.FilePermission "/tmp/abc", "read";
};
```

To know more about policy file locations and granting permissions in
policy files, see [Default Policy Implementation and Policy File
Syntax](permissions-jdk1.htm#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D).

Technically, whenever a resource access is attempted,
<span class="variable">all</span> code traversed by the execution thread
up to that point must have permission for that resource access, unless
some code on the thread has been marked as \"privileged.\" See [Appendix
A: API for Privileged
Blocks](java-se-platform-security-architecture.htm#GUID-BB3C8FB3-1A1A-47F3-8536-3952B84F46F2 "This section explains what privileged code is and what it is used for. It also shows you how to use the doPrivileged API.").

</div>
<div class="sect2">
[]{#GUID-8D0E8306-0DD8-4802-A71E-CFEE9BF8A287}

Permission Descriptions and Risks {#JSSEC-GUID-8D0E8306-0DD8-4802-A71E-CFEE9BF8A287 .sect2}
---------------------------------

<div>
The following is a list of all built-in JDK permission types. The class
summary for each permission type discusses the risks of granting each
permission.

-   [<span class="apiname">java.awt.AWTPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/awt/AWTPermission.html)
-   [<span class="apiname">java.io.FilePermission</span>](https://docs.oracle.com/javase/10/docs/api/java/io/FilePermission.html)
-   [<span class="apiname">java.io.SerializablePermission</span>](https://docs.oracle.com/javase/10/docs/api/java/io/SerializablePermission.html)
-   [<span class="apiname">java.lang.RuntimePermission</span>](https://docs.oracle.com/javase/10/docs/api/java/lang/RuntimePermission.html)
-   [<span class="apiname">java.lang.management.ManagementPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/lang/management/ManagementPermission.html)
-   [<span class="apiname">java.lang.reflect.ReflectPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/lang/reflect/ReflectPermission.html)
-   [<span class="apiname">java.net.NetPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/net/NetPermission.html)
-   [<span class="apiname">java.net.URLPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/net/URLPermission.html)
-   [<span class="apiname">java.net.SocketPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/net/SocketPermission.html)
-   [<span class="apiname">java.nio.file.LinkPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/nio/file/LinkPermission.html)
-   [<span class="apiname">java.security.AllPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/security/AllPermission.html)
-   [<span class="apiname">java.security.SecurityPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/security/SecurityPermission.html)
-   [<span class="apiname">java.security.UnresolvedPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/security/UnresolvedPermission.html)
-   [<span class="apiname">java.sql.SQLPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/sql/SQLPermission.html)
-   [<span class="apiname">java.util.logging.LoggingPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/util/logging/LoggingPermission.html)
-   [<span class="apiname">java.util.PropertyPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/util/PropertyPermission.html)
-   [<span class="apiname">javax.management.MBeanPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/management/MBeanPermission.html)
-   [<span class="apiname">javax.management.MBeanServerPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/management/MBeanServerPermission.html)
-   [<span class="apiname">javax.management.MBeanTrustPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/management/MBeanTrustPermission.html)
-   [<span class="apiname">javax.management.remote.SubjectDelegationPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/management/remote/SubjectDelegationPermission.html)
-   [<span class="apiname">javax.net.ssl.SSLPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/SSLPermission.html)
-   [<span class="apiname">javax.security.auth.AuthPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/AuthPermission.html)
-   [<span class="apiname">javax.security.auth.PrivateCredentialPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/PrivateCredentialPermission.html)
-   [<span class="apiname">javax.security.auth.kerberos.DelegationPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/kerberos/DelegationPermission.html)
-   [<span class="apiname">javax.security.auth.kerberos.ServicePermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/security/auth/kerberos/ServicePermission.html)
-   [<span class="apiname">javax.sound.sampled.AudioPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/sound/sampled/AudioPermission.html)
-   [<span class="apiname">javax.xml.bind.JAXBPermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/bind/JAXBPermission.html)
-   [<span class="apiname">javax.xml.ws.WebServicePermission</span>](https://docs.oracle.com/javase/10/docs/api/javax/xml/ws/WebServicePermission.html)

<div class="infoboxnote" id="GUID-8D0E8306-0DD8-4802-A71E-CFEE9BF8A287__GUID-B42850C7-683D-464E-B3B3-CCAEF05070B1">
Note:

See [Appendix A: FilePermission Path Name Canonicalization Disabled By
Default](permissions-jdk1.htm#GUID-83063225-0ACB-4909-9BAB-7F7D4E3749E2 "A canonical path is a path that doesn't contain any links or shortcuts. Performing path name canonicalization in a FilePermission object can negatively affect performance.")
for important information about a change in how
<span class="apiname">FilePermission</span> path names are
canonicalized.

</div>
</div>
<div class="sect3">
[]{#GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5}

### Methods and the Permissions They Require {#JSSEC-GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5 .sect3}

<div>
The following table is a list of methods that require permissions, which
<span class="apiname">SecurityManager</span> method they call, and which
permission is checked by the default implementation of that
<span class="apiname">SecurityManager</span> method.

<div class="section">
<div class="infoboxnote" id="GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5__GUID-68B0A7D8-17F4-4073-B38F-59C784F0ACC9">
Note:

This list is not complete; other methods exist that require permissions.
See the [Java SE and JDK API
Specification](https://docs.oracle.com/javase/10/docs/api/overview-summary.html)
for additional information on methods that throw
`SecurityException`{.codeph} and the permissions that are required.

</div>
In the default `SecurityManager`{.codeph} method implementations, a call
to a method in the <span class="bold">Method</span> column can only be
successful if the permission specified in the corresponding entry in the
<span class="bold">SecurityManager Method</span> column is allowed by
the policy currently in effect. For example, consider the following
table row:

<div class="tblformalwide" id="GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5__GUID-B478774A-9BA6-4CE5-BD73-C20B438139BC">
+-----------------------+-----------------------+-----------------------+
| Method                | SecurityManager       | Permission            |
|                       | Method Called         |                       |
+:======================+:======================+:======================+
| ``` {.oac_no_warn dir | <span class="apiname" | `java.awt.AWTPermissi |
| ="ltr"}               | >checkPermission</spa | on "accessEventQueue" |
| java.awt.Toolkit      | n>                    | ;`{.codeph}           |
|   public final EventQ |                       |                       |
| ueue                  |                       |                       |
|     getSystemEventQue |                       |                       |
| ue()                  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

This table row specifies that a call to the
<span class="apiname">getSystemEventQueue</span> method in the
<span class="apiname">java.awt.Toolkit</span> class results in a call to
the <span class="apiname">checkPermission</span>
<span class="apiname">SecurityManager</span> method, which can only be
successful if the following permission is granted to code on the call
stack:

``` {.oac_no_warn dir="ltr"}
java.awt.AWTPermission "accessEventQueue";
```

The table rows have the following format, where the runtime value of
`foo`{.codeph} replaces the string `{foo}`{.codeph} in the permission
name.

<div class="tblformalwide" id="GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5__GUID-6621EF67-3A46-40DE-96FA-50E97BEF78B5">
+-----------------------+-----------------------+-----------------------+
| Method                | SecurityManager       | Permission            |
|                       | Method Called         |                       |
+:======================+:======================+:======================+
| ``` {.oac_no_warn dir | <span class="apiname" | `SomePermission "{foo |
| ="ltr"}               | >checkXXX</span>      | }";`{.codeph}         |
| some.package.class    |                       |                       |
|   public static void  |                       |                       |
| someMethod(String foo |                       |                       |
| );                    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

As an example, here is one table entry:

<div class="tblformal" id="GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5__GUID-C1CA14D5-9BC1-48E5-BCE9-F2B09F4728B1">
+-----------------------+-----------------------+-----------------------+
| Method                | SecurityManager       | Permission            |
|                       | Method Called         |                       |
+:======================+:======================+:======================+
| ``` {.oac_no_warn dir | <span class="apiname" | `java.io.FilePermissi |
| ="ltr"}               | >checkRead(String)</s | on "{name}", "read";` |
| java.io.FileInputStre | pan>                  | {.codeph}             |
| am                    |                       |                       |
|   FileInputStream(Str |                       |                       |
| ing name)             |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

If the `FileInputStream`{.codeph} method (in this case, a constructor)
is called with `"/test/MyTestFile"` as the `name`{.codeph} argument, as
in

``` {.codeblock dir="ltr"}
FileInputStream("/test/MyTestFile");
```

then in order for the call to succeed, the following permission must be
set in the current policy, allowing read access to the file
`"/test/MyTestFile"`:

``` {.codeblock dir="ltr"}
java.io.FilePermission "/test/MyTestFile", "read";
```

More specifically, the permission must either be explicitly set, as
above, or implied by another permission, such as the following:

``` {.codeblock dir="ltr"}
java.io.FilePermission "/test/*", "read";
```

which allows read access to any files in the `"/test"`{.codeph}
directory.

In some cases, a term in braces is not exactly the same as the name of a
specific method argument but is meant to represent the relevant value.
Here is an example:

<div class="tblformalwide" id="GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5__GUID-3464ACE0-73BF-4DB7-86C4-C4DB82BAE603">
  Method                                                                                           SecurityManager Method Called                              Permission
  ------------------------------------------------------------------------------------------------ ---------------------------------------------------------- -----------------------------------------------------------------
  `java.net.DatagramSocket   public synchronized void       receive(DatagramPacket p);`{.codeph}   <span class="apiname">checkAccept({host}, {port})</span>   `java.net.SocketPermission "{host}:{port}", "accept";`{.codeph}

</div>
<!-- class="inftblhruleinformal" -->

Here, the appropriate host and port values are calculated by the
`receive`{.codeph} method and passed to `checkAccept`{.codeph}.

In most cases, just the name of the SecurityManager method called is
listed. Where the method is one of multiple methods of the same name,
the argument types are also listed, for example for
`checkRead(String)`{.codeph} and `checkRead(FileDescriptor)`{.codeph}.
In other cases where arguments may be relevant, they are also listed.

The following table is ordered by package name; the methods in classes
in the `java.awt`{.codeph} package are listed first, followed by methods
in classes in the `java.beans`{.codeph} package, and so on:

<div class="tblformalwide" id="GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5__GUID-8F3D87EA-CF98-4725-95DB-5AFD77C58FE6">
Table 1-6 Methods and the Permissions

+-----------------------+-----------------------+-----------------------+
| Method                | SecurityManager       | Permission            |
|                       | Method                |                       |
+:======================+:======================+:======================+
| ``` {.codeblock dir=" | <span class="apiname" | `java.awt.AWTPermissi |
| ltr"}                 | >checkPermission</spa | on "readDisplayPixels |
| java.awt.Graphics2d   | n>                    | "`{.codeph}           |
|   public abstract voi |                       | if this               |
| d                     |                       | <span class="apiname" |
|     setComposite(Comp |                       | >Graphics2D</span>    |
| osite comp)           |                       | context is drawing to |
| ```                   |                       | a                     |
|                       |                       | <span class="apiname" |
|                       |                       | >Component</span>     |
|                       |                       | on the display screen |
|                       |                       | and the               |
|                       |                       | <span class="apiname" |
|                       |                       | >Composite</span>     |
|                       |                       | is a custom object    |
|                       |                       | rather than an        |
|                       |                       | instance of the       |
|                       |                       | <span class="apiname" |
|                       |                       | >AlphaComposite</span |
|                       |                       | >                     |
|                       |                       | class. Note: The      |
|                       |                       | <span class="apiname" |
|                       |                       | >setComposite</span>  |
|                       |                       | method is actually    |
|                       |                       | abstract and thus     |
|                       |                       | can\'t invoke         |
|                       |                       | security checks. Each |
|                       |                       | actual implementation |
|                       |                       | of the method should  |
|                       |                       | call the              |
|                       |                       | <span class="apiname" |
|                       |                       | >java.lang.SecurityMa |
|                       |                       | nager                 |
|                       |                       | checkPermission</span |
|                       |                       | >                     |
|                       |                       | method with a         |
|                       |                       | <span class="apiname" |
|                       |                       | >java.awt.AWTPermissi |
|                       |                       | on(\"readDisplayPixel |
|                       |                       | s\")                  |
|                       |                       | </span>permission     |
|                       |                       | under the conditions  |
|                       |                       | noted.                |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.awt.AWTPermissi |
| ltr"}                 | >checkPermission</spa | on "createRobot"`{.co |
| java.awt.Robot        | n>                    | deph}                 |
|   public Robot()      |                       |                       |
|   public Robot(Graphi |                       |                       |
| csDevice screen)      |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.awt.AWTPermissi |
| ltr"}                 | >checkPermission</spa | on "listenToAllAWTEve |
| java.awt.Toolkit      | n>                    | nts"`{.codeph}        |
|   public void addAWTE |                       |                       |
| ventListener(         |                       |                       |
|     AWTEventListener  |                       |                       |
| listener,             |                       |                       |
|     long eventMask)   |                       |                       |
|   public void removeA |                       |                       |
| WTEventListener(      |                       |                       |
|     AWTEventListener  |                       |                       |
| listener)             |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkPrintJobAccess< | mission "queuePrintJo |
| java.awt.Toolkit      | /span>                | b"`{.codeph}          |
|   public abstract Pri |                       |                       |
| ntJob getPrintJob(    |                       | Note: The             |
|     Frame frame, Stri |                       | <span class="apiname" |
| ng jobtitle,          |                       | >getPrintJob</span>   |
|     Properties props) |                       | method is actually    |
| ```                   |                       | abstract and thus     |
|                       |                       | can\'t invoke         |
|                       |                       | security checks. Each |
|                       |                       | actual implementation |
|                       |                       | of the method should  |
|                       |                       | call the              |
|                       |                       | <span class="apiname" |
|                       |                       | >java.lang.SecurityMa |
|                       |                       | nager                 |
|                       |                       | checkPrintJobAccess</ |
|                       |                       | span>                 |
|                       |                       | method, which is      |
|                       |                       | successful only if    |
|                       |                       | the                   |
|                       |                       | `java.lang.RuntimePer |
|                       |                       | mission "queuePrintJo |
|                       |                       | b"`{.codeph}          |
|                       |                       | permission is         |
|                       |                       | currently allowed.    |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.awt.AWTPermissi |
| ltr"}                 | >checkPermission</spa | on "accessClipboard"` |
| java.awt.Toolkit      | n>                    | {.codeph}             |
|   public abstract Cli |                       |                       |
| pboard                |                       | Note: The             |
|     getSystemClipboar |                       | <span class="apiname" |
| d()                   |                       | >getSystemClipboard</ |
| ```                   |                       | span>                 |
|                       |                       | method is actually    |
|                       |                       | abstract and thus     |
|                       |                       | can\'t invoke         |
|                       |                       | security checks. Each |
|                       |                       | actual implementation |
|                       |                       | of the method should  |
|                       |                       | call the              |
|                       |                       | <span class="apiname" |
|                       |                       | >checkPermission</spa |
|                       |                       | n>                    |
|                       |                       | method, which is      |
|                       |                       | successful only if    |
|                       |                       | the                   |
|                       |                       | `java.awt.AWTPermissi |
|                       |                       | on "accessClipboard"  |
|                       |                       | `{.codeph}permission  |
|                       |                       | is currently allowed. |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.awt.AWTPermissi |
| ltr"}                 | >checkPermission</spa | on "accessEventQueue" |
| java.awt.Toolkit      | n>                    | `{.codeph}            |
|   public final EventQ |                       |                       |
| ueue                  |                       |                       |
|     getSystemEventQue |                       |                       |
| ue()                  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | If                    |
| ltr"}                 | >checkPermission</spa | `java.awt.AWTPermissi |
| java.awt.Window Windo | n>                    | on "showWindowWithout |
| w()                   |                       | WarningBanner"`{.code |
| ```                   |                       | ph}                   |
|                       |                       | is set, the window    |
|                       |                       | will be displayed     |
|                       |                       | without a banner      |
|                       |                       | warning that the      |
|                       |                       | window was created by |
|                       |                       | an applet. It it\'s   |
|                       |                       | not set, such a       |
|                       |                       | banner will be        |
|                       |                       | displayed.            |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.util.PropertyPe |
| ltr"}                 | >checkPropertiesAcces | rmission "*", "read,w |
| java.beans.Beans      | s</span>              | rite"`{.codeph}       |
|   public static void  |                       |                       |
| setDesignTime(        |                       |                       |
|     boolean isDesignT |                       |                       |
| ime)                  |                       |                       |
|   public static void  |                       |                       |
| setGuiAvailable(      |                       |                       |
|     boolean isGuiAvai |                       |                       |
| lable)                |                       |                       |
|                       |                       |                       |
| java.beans.Introspect |                       |                       |
| or                    |                       |                       |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setBeanInfoSearch |                       |                       |
| Path(String path[])   |                       |                       |
|                       |                       |                       |
| java.beans.PropertyEd |                       |                       |
| itorManager           |                       |                       |
|   public static void  |                       |                       |
| registerEditor(       |                       |                       |
|     Class targetType, |                       |                       |
|     Class editorClass |                       |                       |
| )                     |                       |                       |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setEditorSearchPa |                       |                       |
| th(String path[])     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.io.FilePermissi |
| ltr"}                 | >checkDelete(String)< | on "{name}", "delete" |
| java.io.File          | /span>                | `{.codeph}            |
|   public boolean dele |                       |                       |
| te()                  |                       |                       |
|   public void deleteO |                       |                       |
| nExit()               |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkRead(FileDescri | mission "readFileDesc |
| java.io.FileInputStre | ptor)</span>          | riptor"`{.codeph}     |
| am                    |                       |                       |
|   FileInputStream(Fil |                       |                       |
| eDescriptor fdObj)    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.io.FilePermissi |
| ltr"}                 | >checkRead(String)</s | on "{name}", "read"`{ |
| java.io.FileInputStre | pan>                  | .codeph}              |
| am                    |                       |                       |
|   FileInputStream(Str |                       |                       |
| ing name)             |                       |                       |
|   FileInputStream(Fil |                       |                       |
| e file)               |                       |                       |
|                       |                       |                       |
| java.io.File          |                       |                       |
|   public boolean exis |                       |                       |
| ts()                  |                       |                       |
|   public boolean canR |                       |                       |
| ead()                 |                       |                       |
|   public boolean isFi |                       |                       |
| le()                  |                       |                       |
|   public boolean isDi |                       |                       |
| rectory()             |                       |                       |
|   public boolean isHi |                       |                       |
| dden()                |                       |                       |
|   public long lastMod |                       |                       |
| ified()               |                       |                       |
|   public long length( |                       |                       |
| )                     |                       |                       |
|   public String[] lis |                       |                       |
| t()                   |                       |                       |
|   public String[] lis |                       |                       |
| t(                    |                       |                       |
|     FilenameFilter fi |                       |                       |
| lter)                 |                       |                       |
|   public File[] listF |                       |                       |
| iles()                |                       |                       |
|   public File[] listF |                       |                       |
| iles(                 |                       |                       |
|     FilenameFilter fi |                       |                       |
| lter)                 |                       |                       |
|   public File[] listF |                       |                       |
| iles(                 |                       |                       |
|     FileFilter filter |                       |                       |
| )                     |                       |                       |
|                       |                       |                       |
| java.io.RandomAccessF |                       |                       |
| ile                   |                       |                       |
|   RandomAccessFile(St |                       |                       |
| ring name, String mod |                       |                       |
| e)                    |                       |                       |
|   RandomAccessFile(Fi |                       |                       |
| le file, String mode) |                       |                       |
| ```                   |                       |                       |
|                       |                       |                       |
| (where mode is \"r\"  |                       |                       |
| in both               |                       |                       |
| <span class="apiname" |                       |                       |
| >RandomAccessFile</sp |                       |                       |
| an>                   |                       |                       |
| constructurs)         |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkWrite(FileDescr | mission "writeFileDes |
| java.io.FileOutputStr | iptor)</span>         | criptor"`{.codeph}    |
| eam                   |                       |                       |
|   FileOutputStream(Fi |                       |                       |
| leDescriptor fdObj)   |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.io.FilePermissi |
| ltr"}                 | >checkWrite(String)</ | on "{name}", "write"` |
| java.io.FileOutputStr | span>                 | {.codeph}             |
| eam                   |                       |                       |
|   FileOutputStream(Fi |                       |                       |
| le file)              |                       |                       |
|   FileOutputStream(St |                       |                       |
| ring name)            |                       |                       |
|   FileOutputStream(   |                       |                       |
|     String name,      |                       |                       |
|     boolean append)   |                       |                       |
|                       |                       |                       |
| java.io.File          |                       |                       |
|   public boolean canW |                       |                       |
| rite()                |                       |                       |
|   public boolean crea |                       |                       |
| teNewFile()           |                       |                       |
|   public static File  |                       |                       |
| createTempFile(       |                       |                       |
|     String prefix, St |                       |                       |
| ring suffix)          |                       |                       |
|   public static File  |                       |                       |
| createTempFile(       |                       |                       |
|     String prefix,    |                       |                       |
|     String suffix,    |                       |                       |
|     File directory)   |                       |                       |
|   public boolean mkdi |                       |                       |
| r()                   |                       |                       |
|   public boolean mkdi |                       |                       |
| rs()                  |                       |                       |
|   public boolean rena |                       |                       |
| meTo(File dest)       |                       |                       |
|   public boolean setL |                       |                       |
| astModified(long time |                       |                       |
| )                     |                       |                       |
|   public boolean setR |                       |                       |
| eadOnly()             |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.io.Serializable |
| ltr"}                 | >checkPermission</spa | Permission "enableSub |
| java.io.ObjectInputSt | n>                    | stitution"`{.codeph}  |
| ream                  |                       |                       |
|   protected final boo |                       |                       |
| lean                  |                       |                       |
|     enableResolveObje |                       |                       |
| ct(boolean enable);   |                       |                       |
|                       |                       |                       |
| java.io.ObjectOutputS |                       |                       |
| tream                 |                       |                       |
|   protected final boo |                       |                       |
| lean                  |                       |                       |
|     enableReplaceObje |                       |                       |
| ct(boolean enable)    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.io.Serializable |
| ltr"}                 | >checkPermission</spa | Permission "enableSub |
| java.io.ObjectInputSt | n>                    | classImplementation"` |
| ream                  |                       | {.codeph}             |
|   protected ObjectInp |                       |                       |
| utStream()            |                       |                       |
|                       |                       |                       |
| java.io.ObjectOutputS |                       |                       |
| tream                 |                       |                       |
|   protected ObjectOut |                       |                       |
| putStream()           |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.io.FilePermissi |
| ltr"}                 | >checkRead(String)</s | on "{name}", "read,wr |
| java.io.RandomAccessF | pan>                  | ite"`{.codeph}        |
| ile                   | and                   |                       |
|   RandomAccessFile(St | <span class="apiname" |                       |
| ring name, String mod | >checkWrite(String)</ |                       |
| e)                    | span>                 |                       |
| ```                   |                       |                       |
|                       |                       |                       |
| (where mode is        |                       |                       |
| \"rw\")               |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | If `loader`{.codeph}  |
| ltr"}                 | >checkPermission</spa | is null, and the      |
| java.lang.Class       | n>                    | caller\'s class       |
|   public static Class |                       | loader is not null,   |
|  forName(             |                       | then                  |
|     String name,      |                       | <span class="apiname" |
|     boolean initializ |                       | >java.lang.RuntimePer |
| e,                    |                       | mission(\"getClassLoa |
|     ClassLoader loade |                       | der\")</span>         |
| r)                    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | If the caller\'s      |
| ltr"}                 | >checkPermission</spa | class loader is null, |
| java.lang.Class       | n>                    | or is the same as or  |
|   public ClassLoader  |                       | an ancestor of the    |
| getClassLoader()      |                       | class loader for the  |
| ```                   |                       | class whose class     |
|                       |                       | loader is being       |
|                       |                       | requested, no         |
|                       |                       | permission is needed. |
|                       |                       | Otherwise,            |
|                       |                       | `java.lang.RuntimePer |
|                       |                       | mission "getClassLoad |
|                       |                       | er"`{.codeph}         |
|                       |                       | is required.          |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | Default               |
| ltr"}                 | >checkMemberAccess(th | <span class="apiname" |
| java.lang.Class       | is,                   | >checkMemberAccess</s |
|   public Class[] getD | Member.DECLARED)</spa | pan>                  |
| eclaredClasses()      | n>                    | does not require any  |
|   public Field[] getD | and, if this class is | permissions if        |
| eclaredFields()       | in a package,         | \"this\" class\'s     |
|   public Method[] get | <span class="apiname" | class loader is the   |
| DeclaredMethods()     | >checkPackageAccess({ | same as that of the   |
|   public Constructor[ | pkgName})</span>      | caller. Otherwise, it |
| ]                     |                       | requires              |
|     getDeclaredConstr |                       | `java.lang.RuntimePer |
| uctors()              |                       | mission "accessDeclar |
|   public Field getDec |                       | edMembers"`{.codeph}. |
| laredField(           |                       | If this class is in a |
|     String name)      |                       | package,              |
|   public Method getDe |                       | `java.lang.RuntimePer |
| claredMethod(...)     |                       | mission "accessClassI |
|   public Constructor  |                       | nPackage.{pkgName}"`{ |
|     getDeclaredConstr |                       | .codeph}              |
| uctor(...)            |                       | is also required.     |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | Default               |
| ltr"}                 | >checkMemberAccess(th | <span class="apiname" |
| java.lang.Class       | is,                   | >checkMemberAccess</s |
|   public Class[] getC | Member.PUBLIC)</span> | pan>                  |
| lasses()              | and, if class is in a | does not require any  |
|   public Field[] getF | package,              | permissions when the  |
| ields()               | <span class="apiname" | access type is        |
|   public Method[] get | >checkPackageAccess({ | <span class="apiname" |
| Methods()             | pkgName})</span>      | >Member.PUBLIC</span> |
|   public Constructor[ |                       | .                     |
| ] getConstructors()   |                       | If this class is in a |
|   public Field getFie |                       | package,              |
| ld(String name)       |                       | `java.lang.RuntimePer |
|   public Method getMe |                       | mission "accessClassI |
| thod(...)             |                       | nPackage.{pkgName}"`{ |
|   public Constructor  |                       | .codeph}              |
| getConstructor(...)   |                       | is required.          |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkPermission</spa | mission "getProtectio |
| java.lang.Class       | n>                    | nDomain"`{.codeph}    |
|   public ProtectionDo |                       |                       |
| main                  |                       |                       |
|     getProtectionDoma |                       |                       |
| in()                  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkCreateClassLoad | mission "createClassL |
| java.lang.ClassLoader | er</span>             | oader"`{.codeph}      |
|   ClassLoader()       |                       |                       |
|   ClassLoader(ClassLo |                       |                       |
| ader parent)          |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | If the caller\'s      |
| ltr"}                 | >checkPermission</spa | class loader is null, |
| java.lang.ClassLoader | n>                    | or is the same as or  |
|   public static Class |                       | an ancestor of the    |
| Loader                |                       | class loader for the  |
|     getSystemClassLoa |                       | class whose class     |
| der()                 |                       | loader is being       |
|   public ClassLoader  |                       | requested, no         |
| getParent()           |                       | permission is needed. |
| ```                   |                       | Otherwise,            |
|                       |                       | `java.lang.RuntimePer |
|                       |                       | mission "getClassLoad |
|                       |                       | er"`{.codeph}         |
|                       |                       | is required.          |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.io.FilePermissi |
| ltr"}                 | >checkExec</span>     | on "{command}", "exec |
| java.lang.Runtime     |                       | ute"`                 |
|   public Process exec |                       |                       |
| (String command)      |                       |                       |
|   public Process exec |                       |                       |
| (                     |                       |                       |
|     String command,   |                       |                       |
|     String envp[])    |                       |                       |
|   public Process exec |                       |                       |
| (String cmdarray[])   |                       |                       |
|   public Process exec |                       |                       |
| (                     |                       |                       |
|     String cmdarray[] |                       |                       |
| ,                     |                       |                       |
|     String envp[])    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkExit(status)</s | mission "exitVM.{stat |
| java.lang.Runtime     | pan>                  | us}"`{.codeph}        |
|   public void exit(in | where status is 0 for |                       |
| t status)             | <span class="apiname" |                       |
|   public static void  | >runFinalizersOnExit< |                       |
|     runFinalizersOnEx | /span>                |                       |
| it(boolean value)     |                       |                       |
|                       |                       |                       |
| java.lang.System      |                       |                       |
|   public static void  |                       |                       |
| exit(int status)      |                       |                       |
|   public static void  |                       |                       |
|     runFinalizersOnEx |                       |                       |
| it(boolean value)     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkPermission</spa | mission "shutdownHook |
| java.lang.Runtime     | n>                    | s"`{.codeph}          |
|   public void addShut |                       |                       |
| downHook(Thread hook) |                       |                       |
|   public boolean remo |                       |                       |
| veShutdownHook(Thread |                       |                       |
|  hook)                |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkLink({libName}) | mission "loadLibrary. |
| java.lang.Runtime     | </span>               | {libName}"`{.codeph}  |
|   public void load(St | where                 |                       |
| ring lib)             | <span class="apiname" |                       |
|   public void loadLib | >{libName}</span>     |                       |
| rary(String lib)      | is the lib, filename  |                       |
|                       | or libname argument   |                       |
| java.lang.System      |                       |                       |
|   public static void  |                       |                       |
| load(String filename) |                       |                       |
|   public static void  |                       |                       |
| loadLibrary(          |                       |                       |
|     String libname)   |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| <span class="apiname" | <span class="apiname" | See [Table            |
| >java.lang.SecurityMa | >checkPermission</spa | 1-7](permissions-jdk1 |
| nager</span>          | n>                    | .htm#GUID-7423481B-52 |
| methods               |                       | 7F-4F15-AF01-992D6352 |
|                       |                       | 1D2E__JAVA.LANG.SECUR |
|                       |                       | ITYMANAGERMETHODSAND- |
|                       |                       | 54E8CA5F "This table  |
|                       |                       | shows which permissio |
|                       |                       | ns are checked for by |
|                       |                       |  the default implemen |
|                       |                       | tations of the java.l |
|                       |                       | ang.SecurityManager m |
|                       |                       | ethods.").            |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.util.PropertyPe |
| ltr"}                 | >checkPropertiesAcces | rmission "*", "read,w |
| java.lang.System      | s</span>              | rite"`{.codeph}       |
|   public static Prope |                       |                       |
| rties                 |                       |                       |
|     getProperties()   |                       |                       |
|   public static void  |                       |                       |
|     setProperties(Pro |                       |                       |
| perties props)        |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.util.PropertyPe |
| ltr"}                 | >checkPropertyAccess< | rmission "{key}", "re |
| java.lang.System      | /span>                | ad"`{.codeph}         |
|   public static Strin |                       |                       |
| g                     |                       |                       |
|     getProperty(Strin |                       |                       |
| g key)                |                       |                       |
|   public static Strin |                       |                       |
| g                     |                       |                       |
|     getProperty(Strin |                       |                       |
| g key, String def)    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkPermission</spa | mission "setIO"`{.cod |
| java.lang.System      | n>                    | eph}                  |
|   public static void  |                       |                       |
| setIn(InputStream in) |                       |                       |
|   public static void  |                       |                       |
| setOut(PrintStream ou |                       |                       |
| t)                    |                       |                       |
|   public static void  |                       |                       |
| setErr(PrintStream er |                       |                       |
| r)                    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.util.PropertyPe |
| ltr"}                 | >checkPermission</spa | rmission "{key}", "wr |
| java.lang.System      | n>                    | ite"`{.codeph}        |
|   public static Strin |                       |                       |
| g                     |                       |                       |
|     setProperty(Strin |                       |                       |
| g key, String value)  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkPermission</spa | mission "setSecurityM |
| java.lang.System      | n>                    | anager"`{.codeph}     |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setSecurityManage |                       |                       |
| r(SecurityManager s)  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | If the caller\'s      |
| ltr"}                 | >checkPermission</spa | class loader is null, |
| java.lang.Thread      | n>                    | or is the same as or  |
|   public ClassLoader  |                       | an ancestor of the    |
| getContextClassLoader |                       | context class loader  |
| ()                    |                       | for the thread whose  |
| ```                   |                       | context class loader  |
|                       |                       | is being requested,   |
|                       |                       | no permission is      |
|                       |                       | needed. Otherwise,    |
|                       |                       | `java.lang.RuntimePer |
|                       |                       | mission "getClassLoad |
|                       |                       | er"`{.codeph}         |
|                       |                       | is required.          |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkPermission</spa | mission "setContextCl |
| java.lang.Thread      | n>                    | assLoader"`{.codeph}  |
|   public void setCont |                       |                       |
| extClassLoader(       |                       |                       |
|     ClassLoader cl)   |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkAccess(this)</s | mission "modifyThread |
| java.lang.Thread      | pan>                  | "`{.codeph}           |
|   public final void c |                       |                       |
| heckAccess()          |                       |                       |
|   public void interru |                       |                       |
| pt()                  |                       |                       |
|   public final void s |                       |                       |
| uspend()              |                       |                       |
|   public final void r |                       |                       |
| esume()               |                       |                       |
|   public final void s |                       |                       |
| etPriority(           |                       |                       |
|     int newPriority)  |                       |                       |
|   public final void s |                       |                       |
| etName(               |                       |                       |
|     String name)      |                       |                       |
|   public final void s |                       |                       |
| etDaemon(             |                       |                       |
|     boolean on)       |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkAccess({threadG | mission "modifyThread |
| java.lang.Thread      | roup})</span>         | Group"`{.codeph}      |
|   public static int   |                       |                       |
|     enumerate(Thread  |                       |                       |
| tarray[])             |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkAccess(this)</s | mission "modifyThread |
| java.lang.Thread      | pan>.                 | ". `{.codeph}.        |
|   public final void s | Also                  |                       |
| top()                 | <span class="apiname" | Also                  |
| ```                   | >checkPermission</spa | `java.lang.RuntimePer |
|                       | n>                    | mission "stopThread"` |
|                       | if the current thread | {.codeph}             |
|                       | is trying to stop a   | if the current thread |
|                       | thread other than     | is trying to stop a   |
|                       | itself.               | thread other than     |
|                       |                       | itself.               |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkAccess(this)</s | mission "modifyThread |
| java.lang.Thread      | pan>.                 | ".`{.codeph}          |
|   public final synchr | Also                  |                       |
| onized void           | <span class="apiname" | Also                  |
|     stop(Throwable ob | >checkPermission</spa | `java.lang.RuntimePer |
| j)                    | n>                    | mission "stopThread"` |
| ```                   | if the current thread | {.codeph}             |
|                       | is trying to stop a   | if the current thread |
|                       | thread other than     | is trying to stop a   |
|                       | itself or             | thread other than     |
|                       | <span class="apiname" | itself or             |
|                       | >obj</span>           | <span class="apiname" |
|                       | is not an instance of | >obj</span>           |
|                       | <span class="apiname" | is not an instance of |
|                       | >ThreadDeath</span>.  | <span class="apiname" |
|                       |                       | >ThreadDeath</span>.  |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkAccess({parentT | mission "modifyThread |
| java.lang.Thread      | hreadGroup})</span>   | Group"`{.codeph}      |
|   Thread()            |                       |                       |
|   Thread(Runnable tar |                       |                       |
| get)                  |                       |                       |
|   Thread(String name) |                       |                       |
|   Thread(Runnable tar |                       |                       |
| get, String name)     |                       |                       |
|                       |                       |                       |
| java.lang.ThreadGroup |                       |                       |
|   ThreadGroup(String  |                       |                       |
| name)                 |                       |                       |
|   ThreadGroup(        |                       |                       |
|     ThreadGroup paren |                       |                       |
| t,                    |                       |                       |
|     String name)      |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkAccess(this)</s | mission "modifyThread |
| java.lang.Thread      | pan>                  | Group"`{.codeph}      |
|   Thread(ThreadGroup  | for                   |                       |
| group, ...)           | <span class="apiname" |                       |
|                       | >ThreadGroup</span>   |                       |
| java.lang.ThreadGroup | methods, or           |                       |
|   public final void c | <span class="apiname" |                       |
| heckAccess()          | >checkAccess(group)</ |                       |
|   public int enumerat | span>                 |                       |
| e(Thread list[])      | for                   |                       |
|   public int enumerat | <span class="apiname" |                       |
| e(                    | >Thread</span>        |                       |
|     Thread list[],    | methods               |                       |
|     boolean recurse)  |                       |                       |
|   public int enumerat |                       |                       |
| e(ThreadGroup list[]) |                       |                       |
|   public int enumerat |                       |                       |
| e(                    |                       |                       |
|     ThreadGroup list[ |                       |                       |
| ],                    |                       |                       |
|     boolean recurse)  |                       |                       |
|   public final Thread |                       |                       |
| Group getParent()     |                       |                       |
|   public final void s |                       |                       |
| etDaemon(             |                       |                       |
|     boolean daemon)   |                       |                       |
|   public final void s |                       |                       |
| etMaxPriority(int pri |                       |                       |
| )                     |                       |                       |
|   public final void s |                       |                       |
| uspend()              |                       |                       |
|   public final void r |                       |                       |
| esume()               |                       |                       |
|   public final void d |                       |                       |
| estroy()              |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | Requires              |
| ltr"}                 | >checkAccess(this)</s | `java.lang.RuntimePer |
| java.lang.ThreadGroup | pan>                  | mission "modifyThread |
|   public final void i |                       | Group"`{.codeph}.     |
| nterrupt()            |                       | Also requires         |
| ```                   |                       | `java.lang.RuntimePer |
|                       |                       | mission "modifyThread |
|                       |                       | "`{.codeph},          |
|                       |                       | since the             |
|                       |                       | <span class="apiname" |
|                       |                       | >java.lang.Thread     |
|                       |                       | interrupt()</span>    |
|                       |                       | method is called for  |
|                       |                       | each thread in the    |
|                       |                       | thread group and in   |
|                       |                       | all of its subgroups. |
|                       |                       | See the               |
|                       |                       | [<span class="apiname |
|                       |                       | ">Thread              |
|                       |                       | interrupt()</span>](h |
|                       |                       | ttps://docs.oracle.co |
|                       |                       | m/javase/10/docs/api/ |
|                       |                       | java/lang/Thread.html |
|                       |                       | #interrupt--)         |
|                       |                       | method.               |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | Requires              |
| ltr"}                 | >checkAccess(this)</s | `java.lang.RuntimePer |
| java.lang.ThreadGroup | pan>                  | mission "modifyThread |
|   public final void s |                       | Group"`{.codeph}.     |
| top()                 |                       | Also requires         |
| ```                   |                       | `java.lang.RuntimePer |
|                       |                       | mission "modifyThread |
|                       |                       | "`{.codeph}           |
|                       |                       | and possibly          |
|                       |                       | `java.lang.RuntimePer |
|                       |                       | mission "stopThread"` |
|                       |                       | {.codeph},            |
|                       |                       | since the             |
|                       |                       | <span class="apiname" |
|                       |                       | >java.lang.Thread     |
|                       |                       | stop()</span> method  |
|                       |                       | is called for each    |
|                       |                       | thread in the thread  |
|                       |                       | group and in all of   |
|                       |                       | its subgroups. See    |
|                       |                       | the                   |
|                       |                       | [<span class="apiname |
|                       |                       | ">Thread              |
|                       |                       | stop()</span>](https: |
|                       |                       | //docs.oracle.com/jav |
|                       |                       | ase/10/docs/api/java/ |
|                       |                       | lang/Thread.html#stop |
|                       |                       | --)                   |
|                       |                       | method.               |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.reflect.Re |
| ltr"}                 | >checkPermission</spa | flectPermission "supp |
| java.lang.reflect.Acc | n>                    | ressAccessChecks"`{.c |
| essibleObject         |                       | odeph}                |
|   public static void  |                       |                       |
| setAccessible(...)    |                       |                       |
|   public void setAcce |                       |                       |
| ssible(...)           |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.NetPermissi |
| ltr"}                 | >checkPermission</spa | on "requestPasswordAu |
| java.net.Authenticato | n>                    | thentication"`{.codep |
| r                     |                       | h}                    |
|   public static Passw |                       |                       |
| ordAuthentication     |                       |                       |
|     requestPasswordAu |                       |                       |
| thentication(         |                       |                       |
|       InetAddress add |                       |                       |
| r,                    |                       |                       |
|       int port,       |                       |                       |
|       String protocol |                       |                       |
| ,                     |                       |                       |
|       String prompt,  |                       |                       |
|       String scheme)  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.NetPermissi |
| ltr"}                 | >checkPermission</spa | on "setDefaultAuthent |
| java.net.Authenticato | n>                    | icator"`{.codeph}     |
| r                     |                       |                       |
|   public static void  |                       |                       |
|     setDefault(Authen |                       |                       |
| ticator a)            |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.SocketPermi |
| ltr"}                 | >checkMulticast(InetA | ssion( mcastaddr.getH |
| java.net.MulticastSoc | ddress)</span>        | ostAddress(), "accept |
| ket                   |                       | ,connect")`{.codeph}  |
|   public void         |                       |                       |
|     joinGroup(InetAdd |                       |                       |
| ress mcastaddr)       |                       |                       |
|   public void         |                       |                       |
|     leaveGroup(InetAd |                       |                       |
| dress mcastaddr)      |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | ``` {.oac_no_warn dir |
| ltr"}                 | >checkMulticast(p.get | ="ltr"}               |
| java.net.DatagramSock | Address())</span>     | if (p.getAddress().is |
| et                    | or                    | MulticastAddress()) { |
|   public void send(Da | <span class="apiname" |   java.net.SocketPerm |
| tagramPacket p)       | >checkConnect(        | ission(               |
| ```                   | p.getAddress().getHos |     (p.getAddress()). |
|                       | tAddress(),           | getHostAddress(),     |
|                       | p.getPort())</span>   |     "accept,connect") |
|                       |                       | } else {              |
|                       |                       |   port = p.getPort(); |
|                       |                       |   host = p.getAddress |
|                       |                       | ().getHostAddress();  |
|                       |                       |   if (port == -1)     |
|                       |                       |     java.net.SocketPe |
|                       |                       | rmission "{host}","re |
|                       |                       | solve";               |
|                       |                       |   else                |
|                       |                       |     java.net.SocketPe |
|                       |                       | rmission "{host}:{por |
|                       |                       | t}","connect";        |
|                       |                       | }                     |
|                       |                       | ```                   |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | ``` {.oac_no_warn dir |
| ltr"}                 | >checkMulticast(p.get | ="ltr"}               |
| java.net.MulticastSoc | Address(),            | if (p.getAddress().is |
| ket                   | ttl)</span> or        | MulticastAddress()) { |
|   public synchronized | <span class="apiname" |   java.net.SocketPerm |
|  void                 | >checkConnect(        | ission(               |
|     send(DatagramPack | p.getAddress().getHos |     (p.getAddress()). |
| et p, byte ttl)       | tAddress(),           | getHostAddress(),     |
| ```                   | p.getPort())</span>   |     "accept,connect") |
|                       |                       | } else {              |
|                       |                       |   port = p.getPort(); |
|                       |                       |   host = p.getAddress |
|                       |                       | ().getHostAddress();  |
|                       |                       |   if (port == -1)     |
|                       |                       |     java.net.SocketPe |
|                       |                       | rmission "{host}","re |
|                       |                       | solve";               |
|                       |                       |   else                |
|                       |                       |     java.net.SocketPe |
|                       |                       | rmission "{host}:{por |
|                       |                       | t}","connect"         |
|                       |                       | }                     |
|                       |                       | ```                   |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.SocketPermi |
| ltr"}                 | >checkConnect({host}, | ssion "{host}", "reso |
| java.net.InetAddress  | -1)</span>            | lve"`{.codeph}        |
|   public String getHo |                       |                       |
| stName()              |                       |                       |
|   public static InetA |                       |                       |
| ddress[]              |                       |                       |
|     getAllByName(Stri |                       |                       |
| ng host)              |                       |                       |
|   public static InetA |                       |                       |
| ddress getLocalHost() |                       |                       |
|                       |                       |                       |
| java.net.DatagramSock |                       |                       |
| et                    |                       |                       |
|   public InetAddress  |                       |                       |
| getLocalAddress()     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.SocketPermi |
| ltr"}                 | >checkListen({port})< | ssion "localhost:{por |
| java.net.ServerSocket | /span>                | t}","listen"; `{.code |
|   ServerSocket(...)   |                       | ph}                   |
|                       |                       |                       |
| java.net.DatagramSock |                       |                       |
| et                    |                       |                       |
|   DatagramSocket(...) |                       |                       |
|                       |                       |                       |
| java.net.MulticastSoc |                       |                       |
| ket                   |                       |                       |
|   MulticastSocket(... |                       |                       |
| )                     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.SocketPermi |
| ltr"}                 | >checkAccept({host},  | ssion "{host}:{port}" |
| java.net.ServerSocket | {port})</span>        | , "accept"`{.codeph}  |
|   public Socket accep |                       |                       |
| t()                   |                       |                       |
|   protected final voi |                       |                       |
| d implAccept(Socket s |                       |                       |
| )                     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkSetFactory</spa | mission "setFactory"` |
| java.net.ServerSocket | n>                    | {.codeph}             |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setSocketFactory( |                       |                       |
| ...)                  |                       |                       |
|                       |                       |                       |
| java.net.Socket       |                       |                       |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setSocketImplFact |                       |                       |
| ory(...)              |                       |                       |
|                       |                       |                       |
| java.net.URL          |                       |                       |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setURLStreamHandl |                       |                       |
| erFactory(...)        |                       |                       |
|                       |                       |                       |
| java.net.URLConnectio |                       |                       |
| n                     |                       |                       |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setContentHandler |                       |                       |
| Factory(...)          |                       |                       |
|   public static void  |                       |                       |
|     setFileNameMap(Fi |                       |                       |
| leNameMap map)        |                       |                       |
|                       |                       |                       |
| java.net.HttpURLConne |                       |                       |
| ction                 |                       |                       |
|   public static void  |                       |                       |
|     setFollowRedirect |                       |                       |
| s(boolean set)        |                       |                       |
|                       |                       |                       |
| java.rmi.activation.A |                       |                       |
| ctivationGroup        |                       |                       |
|   public static synch |                       |                       |
| ronized               |                       |                       |
|     ActivationGroup c |                       |                       |
| reateGroup(...)       |                       |                       |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setSystem(Activat |                       |                       |
| ionSystem system)     |                       |                       |
|                       |                       |                       |
| java.rmi.server.RMISo |                       |                       |
| cketFactory           |                       |                       |
|   public synchronized |                       |                       |
|  static void          |                       |                       |
|     setSocketFactory( |                       |                       |
| ...)                  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.SocketPermi |
| ltr"}                 | >checkConnect({host}, | ssion "{host}:{port}" |
| java.net.Socket       | {port})</span>        | , "connect"`{.codeph} |
|   Socket(...)         |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.SocketPermi |
| ltr"}                 | >checkAccept({host},  | ssion "{host}:{port}" |
| java.net.DatagramSock | {port})</span>        | , "accept"`{.codeph}  |
| et                    |                       |                       |
|   public synchronized |                       |                       |
|  void                 |                       |                       |
|     receive(DatagramP |                       |                       |
| acket p)              |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.net.NetPermissi |
| ltr"}                 | >checkPermission</spa | on "specifyStreamHand |
| java.net.URL URL(...) | n>                    | ler"`{.codeph}        |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkCreateClassLoad | mission "createClassL |
| java.net.URLClassLoad | er</span>             | oader"`{.codeph}      |
| er                    |                       |                       |
|   URLClassLoader(...) |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkPermission</spa | tyPermission "createA |
| java.security.AccessC | n>                    | ccessControlContext"` |
| ontrolContext         |                       | {.codeph}             |
|   public AccessContro |                       |                       |
| lContext(             |                       |                       |
|     AccessControlCont |                       |                       |
| ext acc,              |                       |                       |
|     DomainCombiner co |                       |                       |
| mbiner)               |                       |                       |
|   public DomainCombin |                       |                       |
| er getDomainCombiner( |                       |                       |
| )                     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "addIden |
| java.security.Identit | \"addIdentityCertific | tityCertificate"`{.co |
| y                     | ate\")</span>         | deph}                 |
|   public void addCert |                       |                       |
| ificate(...)          |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "removeI |
| java.security.Identit | \"removeIdentityCerti | dentityCertificate"`{ |
| y                     | ficate\")</span>      | .codeph}              |
|   public void removeC |                       |                       |
| ertificate(...)       |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "setIden |
| java.security.Identit | \"setIdentityInfo\")< | tityInfo"`{.codeph}   |
| y                     | /span>                |                       |
|   public void setInfo |                       |                       |
| (String info)         |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "setIden |
| java.security.Identit | \"setIdentityPublicKe | tityPublicKey"`{.code |
| y                     | y\")</span>           | ph}                   |
|   public void setPubl |                       |                       |
| icKey(PublicKey key)  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "printId |
| java.security.Identit | \"printIdentity\")</s | entity"`{.codeph}     |
| y                     | pan>                  |                       |
|   public String toStr |                       |                       |
| ing(...)              |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "setSyst |
| java.security.Identit | \"setSystemScope\")</ | emScope"`{.codeph}    |
| yScope                | span>                 |                       |
|   protected static vo |                       |                       |
| id setSystemScope()   |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | This                  |
| ltr"}                 | >checkPermission(this | <span class="apiname" |
| java.security.Permiss | )</span>              | >Permission</span>    |
| ion                   |                       | object is the         |
|   public void checkGu |                       | permission checked.   |
| ard(Object object)    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkPermission</spa | tyPermission "getPoli |
| java.security.Policy  | n>                    | cy"`{.codeph}         |
|   public static Polic |                       |                       |
| y getPolicy()         |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkPermission</spa | tyPermission "setPoli |
| java.security.Policy  | n>                    | cy"`{.codeph}         |
|   public static void  |                       |                       |
|     setPolicy(Policy  |                       |                       |
| policy)               |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkPermission</spa | tyPermission "createP |
| java.security.Policy  | n>                    | olicy.{type}"`{.codep |
|   public static Polic |                       | h}                    |
| y                     |                       |                       |
|     getInstance(      |                       |                       |
|       String type,    |                       |                       |
|       SpiParameter pa |                       |                       |
| rams)                 |                       |                       |
|     getInstance(      |                       |                       |
|       String type,    |                       |                       |
|       SpiParameter pa |                       |                       |
| rams,                 |                       |                       |
|       String provider |                       |                       |
| )                     |                       |                       |
|     getInstance(      |                       |                       |
|       String type,    |                       |                       |
|       SpiParameter pa |                       |                       |
| rams,                 |                       |                       |
|       Provider provid |                       |                       |
| er)                   |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "clearPr |
| java.security.Provide | \"clearProviderProper | oviderProperties.{nam |
| r                     | ties.\"+{name})</span | e}"`{.codeph}         |
|   public synchronized | >                     | where `name`{.codeph} |
|  void clear()         |                       | is the provider name. |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "putProv |
| java.security.Provide | \"putProviderProperty | iderProperty.{name}"` |
| r                     | .\"+{name})</span>    | {.codeph}             |
|   public synchronized |                       | where `name`{.codeph} |
|  Object               |                       | is the provider name. |
|     put(Object key, O |                       |                       |
| bject value)          |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "removeP |
| java.security.Provide | \"removeProviderPrope | roviderProperty.{name |
| r                     | rty.\"+{name})</span> | }"`{.codeph}          |
|   public synchronized |                       | where `name`{.codeph} |
|  Object               |                       | is the provider name. |
|     remove(Object key |                       |                       |
| )                     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.lang.RuntimePer |
| ltr"}                 | >checkCreateClassLoad | mission "createClassL |
| java.security.SecureC | er</span>             | oader"`{.codeph}      |
| lassLoader            |                       |                       |
|   SecureClassLoader(. |                       |                       |
| ..)                   |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkPermission</spa | tyPermission "getProp |
| java.security.Securit | n>                    | erty.{key}"`{.codeph} |
| y                     |                       |                       |
|   public static void  |                       |                       |
| getProperty(String ke |                       |                       |
| y)                    |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "insertP |
| java.security.Securit | \"insertProvider.\"+p | rovider.{name}"`{.cod |
| y                     | rovider.getName())</s | eph}                  |
|   public static int   | pan>                  |                       |
|     addProvider(Provi |                       |                       |
| der provider)         |                       |                       |
|   public static int   |                       |                       |
|     insertProviderAt( |                       |                       |
|       Provider provid |                       |                       |
| er,                   |                       |                       |
|       int position);  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "removeP |
| java.security.Securit | \"removeProvider.\"+n | rovider.{name}"`{.cod |
| y                     | ame)</span>           | eph}                  |
|   public static void  |                       |                       |
|     removeProvider(St |                       |                       |
| ring name)            |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "setProp |
| java.security.Securit | \"setProperty.\"+key) | erty.{key}"`{.codeph} |
| y                     | </span>               |                       |
|   public static void  |                       |                       |
|     setProperty(Strin |                       |                       |
| g key, String datum)  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "getSign |
| java.security.Signer  | \"getSignerPrivateKey | erPrivateKey"`{.codep |
|   public PrivateKey g | \")</span>            | h}                    |
| etPrivateKey()        |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.security.Securi |
| ltr"}                 | >checkSecurityAccess( | tyPermission "setSign |
| java.security.Signer  | \"setSignerKeypair\") | erKeypair"`{.codeph}  |
|   public final void   | </span>               |                       |
|     setKeyPair(KeyPai |                       |                       |
| r pair)               |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.sql.SQLPermissi |
| ltr"}                 | >checkPermission</spa | on "setLog"`{.codeph} |
| java.sql.DriverManage | n>                    |                       |
| r                     |                       |                       |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setLogWriter(Prin |                       |                       |
| tWriter out)          |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.sql.SQLPermissi |
| ltr"}                 | >checkPermission</spa | on "setLog"`{.codeph} |
| java.sql.DriverManage | n>                    |                       |
| r                     |                       |                       |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setLogStream(Prin |                       |                       |
| tWriter out)          |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.util.PropertyPe |
| ltr"}                 | >checkPermission</spa | rmission "user.langua |
| java.util.Locale      | n>                    | ge","write"`{.codeph} |
|   public static synch |                       |                       |
| ronized void          |                       |                       |
|     setDefault(Locale |                       |                       |
|  newLocale)           |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `java.io.FilePermissi |
| ltr"}                 | >checkRead</span>     | on "{name}","read"`{. |
| java.util.zip.ZipFile |                       | codeph}               |
|   ZipFile(String name |                       |                       |
| )                     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "getSu |
| javax.security.auth.S | n>                    | bject"`{.codeph}      |
| ubject                |                       |                       |
|   public static Subje |                       |                       |
| ct getSubject(        |                       |                       |
|     final AccessContr |                       |                       |
| olContext acc)        |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "setRe |
| javax.security.auth.S | n>                    | adOnly"`{.codeph}     |
| ubject                |                       |                       |
|   public void setRead |                       |                       |
| Only()                |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "doAs" |
| javax.security.auth.S | n>                    | `{.codeph}            |
| ubject                |                       |                       |
|   public static Objec |                       |                       |
| t doAs(               |                       |                       |
|     final Subject sub |                       |                       |
| ject,                 |                       |                       |
|     final PrivilegedA |                       |                       |
| ction action)         |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "doAs" |
| javax.security.auth.S | n>                    | `{.codeph}            |
| ubject                |                       |                       |
|   public static Objec |                       |                       |
| t doAs(               |                       |                       |
|     final Subject sub |                       |                       |
| ject,                 |                       |                       |
|     final PrivilegedE |                       |                       |
| xceptionAction action |                       |                       |
| )                     |                       |                       |
|     throws            |                       |                       |
|       java.security.P |                       |                       |
| rivilegedActionExcept |                       |                       |
| ion                   |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "doAsP |
| javax.security.auth.S | n>                    | rivileged"`{.codeph}  |
| ubject                |                       |                       |
|   public static Objec |                       |                       |
| t doAsPrivileged(     |                       |                       |
|     final Subject sub |                       |                       |
| ject,                 |                       |                       |
|     final PrivilegedA |                       |                       |
| ction action,         |                       |                       |
|     final AccessContr |                       |                       |
| olContext acc)        |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "doAsP |
| javax.security.auth.S | n>                    | rivileged"`{.codeph}  |
| ubject                |                       |                       |
|   public static Objec |                       |                       |
| t doAsPrivileged(     |                       |                       |
|     final Subject sub |                       |                       |
| ject,                 |                       |                       |
|     final PrivilegedE |                       |                       |
| xceptionAction action |                       |                       |
| ,                     |                       |                       |
|     final AccessContr |                       |                       |
| olContext acc)        |                       |                       |
|       throws          |                       |                       |
|         java.security |                       |                       |
| .PrivilegedActionExce |                       |                       |
| ption                 |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "getSu |
| javax.security.auth.S | n>                    | bjectFromDomainCombin |
| ubjectDomainCombiner  |                       | er"`{.codeph}         |
|   public Subject getS |                       |                       |
| ubject()              |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "getSu |
| javax.security.auth.S | n>                    | bjectFromDomainCombin |
| ubjectDomainCombiner  |                       | er"`{.codeph}         |
|   public Subject getS |                       |                       |
| ubject()              |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "creat |
| javax.security.auth.l | n>                    | eLoginContext.{name}" |
| ogin.LoginContext     |                       | `{.codeph}            |
|   public LoginContext |                       |                       |
| (String name)         |                       |                       |
|     throws LoginExcep |                       |                       |
| tion                  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "creat |
| javax.security.auth.l | n>                    | eLoginContext.{name}" |
| ogin.LoginContext     |                       | `{.codeph}            |
|   public LoginContext |                       |                       |
| (                     |                       |                       |
|     String name,      |                       |                       |
|     Subject subject)  |                       |                       |
|     throws LoginExcep |                       |                       |
| tion                  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "creat |
| javax.security.auth.l | n>                    | eLoginContext.{name}" |
| ogin.LoginContext     |                       | `{.codeph}            |
|   public LoginContext |                       |                       |
| (                     |                       |                       |
|     String name,      |                       |                       |
|     CallbackHandler c |                       |                       |
| allbackHandler)       |                       |                       |
|     throws LoginExcep |                       |                       |
| tion                  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "creat |
| javax.security.auth.l | n>                    | eLoginContext.{name}" |
| ogin.LoginContext     |                       | `{.codeph}            |
|   public LoginContext |                       |                       |
| (                     |                       |                       |
|     String name,      |                       |                       |
|     Subject subject,  |                       |                       |
|     CallbackHandler c |                       |                       |
| allbackHandler)       |                       |                       |
|     throws LoginExcep |                       |                       |
| tion                  |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "getLo |
| javax.security.auth.l | n>                    | ginConfiguration"`{.c |
| ogin.Configuration    |                       | odeph}                |
|   public static Confi |                       |                       |
| guration              |                       |                       |
|     getConfiguration( |                       |                       |
| )                     |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "setLo |
| javax.security.auth.l | n>                    | ginConfiguration"`{.c |
| ogin.Configuration    |                       | odeph}                |
|   public static void  |                       |                       |
| setConfiguration(     |                       |                       |
|     Configuration con |                       |                       |
| figuration)           |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "refre |
| javax.security.auth.l | n>                    | shLoginConfiguration" |
| ogin.Configuration    |                       | `{.codeph}            |
|     public static voi |                       |                       |
| d refresh()           |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+
| ``` {.codeblock dir=" | <span class="apiname" | `javax.security.auth. |
| ltr"}                 | >checkPermission</spa | AuthPermission "creat |
| javax.security.auth.l | n>                    | eLoginConfiguration.{ |
| ogin.Configuration    |                       | type}"`{.codeph}      |
|   public static Confi |                       |                       |
| guration              |                       |                       |
|     getInstance(      |                       |                       |
|       String type,    |                       |                       |
|       SpiParameter pa |                       |                       |
| rams)                 |                       |                       |
|     getInstance(      |                       |                       |
|       String type,    |                       |                       |
|       SpiParameter pa |                       |                       |
| rams,                 |                       |                       |
|       String provider |                       |                       |
| )                     |                       |                       |
|     getInstance(Strin |                       |                       |
| g type,               |                       |                       |
|       SpiParameter pa |                       |                       |
| rams,                 |                       |                       |
|       Provider provid |                       |                       |
| er)                   |                       |                       |
| ```                   |                       |                       |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-7423481B-527F-4F15-AF01-992D63521D2E}

### java.lang.SecurityManager Method Permission Checks {#JSSEC-GUID-7423481B-527F-4F15-AF01-992D63521D2E .sect3}

<div>
The following table shows which permissions are checked by the default
implementations of the
<span class="apiname">java.lang.SecurityManager</span> methods.

<div class="section">
Each of the specified `check`{.codeph} methods calls the
`SecurityManager`{.codeph} `checkPermission`{.codeph} method with the
specified permission, except for the `checkConnect`{.codeph} and
`checkRead`{.codeph} methods that take a context argument. Those methods
expect the context to be an `AccessControlContext`{.codeph} and they
call the context\'s `checkPermission`{.codeph} method with the specified
permission.

<div class="tblformalwide" id="GUID-7423481B-527F-4F15-AF01-992D63521D2E__JAVA.LANG.SECURITYMANAGERMETHODSAND-54E8CA5F">
Table 1-7 java.lang.SecurityManager Methods and Permissions

+-----------------------------------+-----------------------------------+
| Method                            | Permission                        |
+:==================================+:==================================+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkAccept(String ho | java.net.SocketPermission "{host} |
| st, int port);                    | :{port}", "accept";               |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkAccess(Thread t) | java.lang.RuntimePermission "modi |
| ;                                 | fyThread";                        |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkAccess(ThreadGro | java.lang.RuntimePermission "modi |
| up g);                            | fyThreadGroup";                   |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkAwtEventQueueAcc | java.awt.AWTPermission "accessEve |
| ess();                            | ntQueue";                         |
| ```                               | ```                               |
|                                   |                                   |
| <div class="infoboxnote" id="GUID |                                   |
| -7423481B-527F-4F15-AF01-992D6352 |                                   |
| 1D2E__GUID-341E78C2-61D6-4F73-9FD |                                   |
| E-A4B190A7A675">                  |                                   |
| Note:                             |                                   |
|                                   |                                   |
| This method is deprecated; use    |                                   |
| instead                           |                                   |
| <span class="apiname">public void |                                   |
| checkPermission(Permission        |                                   |
| perm);</span>                     |                                   |
| </div>                            |                                   |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkConnect(String h | if (port == -1)                   |
| ost, int port);                   |   java.net.SocketPermission "{hos |
| ```                               | t}","resolve";                    |
|                                   | else                              |
|                                   |   java.net.SocketPermission "{hos |
|                                   | t}:{port}","connect";             |
|                                   | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkConnect(         | if (port == -1)                   |
|   String host,                    |   java.net.SocketPermission "{hos |
|   int port,                       | t}","resolve";                    |
|   Object context);                | else                              |
| ```                               |   java.net.SocketPermission "{hos |
|                                   | t}:{port}","connect";             |
|                                   | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkCreateClassLoade | java.lang.RuntimePermission "crea |
| r();                              | teClassLoader";                   |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkDelete(String fi | java.io.FilePermission "{file}",  |
| le);                              | "delete";                         |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | if cmd is an absolute path:       |
| public void checkExec(String cmd) |                                   |
| ;                                 | ``` {.oac_no_warn dir="ltr"}      |
| ```                               |   java.io.FilePermission "{cmd}", |
|                                   |  "execute";                       |
|                                   | ```                               |
|                                   |                                   |
|                                   | else                              |
|                                   |                                   |
|                                   | ``` {.oac_no_warn dir="ltr"}      |
|                                   |   java.io.FilePermission "<<ALL_F |
|                                   | ILES>>", "execute";               |
|                                   | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkExit(int status) | java.lang.RuntimePermission "exit |
| ;                                 | VM.{status}";                     |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkLink(String lib) | java.lang.RuntimePermission "load |
| ;                                 | Library.{lib}";                   |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkListen(int port) | java.net.SocketPermission "localh |
| ;                                 | ost:{port}","listen";             |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.codeblock dir="ltr"}        |
| public void checkMemberAccess(Cla | if (which != Member.PUBLIC) {     |
| ss clazz, int which);             |   if (currentClassLoader() != cla |
| ```                               | zz.getClassLoader()) {            |
|                                   |     checkPermission(              |
| <div class="infoboxnote" id="GUID |       new java.lang.RuntimePermis |
| -7423481B-527F-4F15-AF01-992D6352 | sion(                             |
| 1D2E__GUID-DBC85F63-49B5-4D97-8D5 |         "accessDeclaredMembers")) |
| 5-44DEDA9E85A8">                  | ;                                 |
| Note:                             |   }                               |
|                                   | }                                 |
| This method is deprecated; use    | ```                               |
| instead                           |                                   |
| <span class="apiname">public void |                                   |
| checkPermission(Permission perm); |                                   |
| </span>                           |                                   |
| </div>                            |                                   |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkMulticast(InetAd | java.net.SocketPermission(        |
| dress maddr);                     |   maddr.getHostAddress(),"accept, |
| ```                               | connect");                        |
|                                   | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkMulticast(InetAd | java.net.SocketPermission(        |
| dress maddr, byte ttl);           |   maddr.getHostAddress(),"accept, |
| ```                               | connect");                        |
|                                   | ```                               |
| <div class="infoboxnote" id="GUID |                                   |
| -7423481B-527F-4F15-AF01-992D6352 |                                   |
| 1D2E__GUID-F5833522-623D-4DDC-898 |                                   |
| 2-E850310DB54B">                  |                                   |
| Note:                             |                                   |
|                                   |                                   |
| This method is deprecated; use    |                                   |
| instead                           |                                   |
| <span class="apiname">public void |                                   |
| checkPermission(Permission perm); |                                   |
| </span>                           |                                   |
| </div>                            |                                   |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkPackageAccess(St | java.lang.RuntimePermission "acce |
| ring pkg);                        | ssClassInPackage.{pkg}";          |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkPackageDefinitio | java.lang.RuntimePermission "defi |
| n(String pkg);                    | neClassInPackage.{pkg}";          |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkPrintJobAccess() | java.lang.RuntimePermission "queu |
| ;                                 | ePrintJob";                       |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkPropertiesAccess | java.util.PropertyPermission "*", |
| ();                               |  "read,write";                    |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkPropertyAccess(S | java.util.PropertyPermission "{ke |
| tring key);                       | y}", "read,write";                |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkRead(FileDescrip | java.lang.RuntimePermission "read |
| tor fd);                          | FileDescriptor";                  |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkRead(String file | java.io.FilePermission "{file}",  |
| );                                | "read";                           |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkRead(String file | java.io.FilePermission "{file}",  |
| , Object context);                | "read";                           |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkSecurityAccess(S | java.security.SecurityPermission  |
| tring target);                    | "{target}";                       |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkSetFactory();    | java.lang.RuntimePermission "setF |
| ```                               | actory";                          |
|                                   | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkSystemClipboardA | java.awt.AWTPermission "accessCli |
| ccess();                          | pboard";                          |
| ```                               | ```                               |
|                                   |                                   |
| <div class="infoboxnote" id="GUID |                                   |
| -7423481B-527F-4F15-AF01-992D6352 |                                   |
| 1D2E__GUID-71A2C528-CA6C-4E44-847 |                                   |
| 7-07986428B883">                  |                                   |
| Note:                             |                                   |
|                                   |                                   |
| This method is deprecated; use    |                                   |
| instead                           |                                   |
| <span class="apiname">public void |                                   |
| checkPermission(Permission        |                                   |
| perm);</span>                     |                                   |
| </div>                            |                                   |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public boolean checkTopLevelWindo | java.awt.AWTPermission "showWindo |
| w(Object window);                 | wWithoutWarningBanner";           |
| ```                               | ```                               |
|                                   |                                   |
| <div class="infoboxnote" id="GUID |                                   |
| -7423481B-527F-4F15-AF01-992D6352 |                                   |
| 1D2E__GUID-233879A0-8AD7-4324-803 |                                   |
| 2-452BEC294AE0">                  |                                   |
| Note:                             |                                   |
|                                   |                                   |
| This method is deprecated; use    |                                   |
| instead                           |                                   |
| <span class="apiname">public void |                                   |
| checkPermission(Permission        |                                   |
| perm);</span>                     |                                   |
| </div>                            |                                   |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkWrite(FileDescri | java.lang.RuntimePermission "writ |
| ptor fd);                         | eFileDescriptor";                 |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public void checkWrite(String fil | java.io.FilePermission "{file}",  |
| e);                               | "write";                          |
| ```                               | ```                               |
+-----------------------------------+-----------------------------------+
| ``` {.oac_no_warn dir="ltr"}      | ``` {.oac_no_warn dir="ltr"}      |
| public SecurityManager();         | java.lang.RuntimePermission "crea |
| ```                               | teSecurityManager";               |
|                                   | ```                               |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D}

Default Policy Implementation and Policy File Syntax {#JSSEC-GUID-789089CA-8557-4017-B8B0-6899AD3BA18D .sect2}
----------------------------------------------------

<div>
The policy for a Java programming language application environment
(specifying which permissions are available for code from various
sources, and executing as various principals) is represented by a Policy
object. More specifically, it is represented by a `Policy`{.codeph}
subclass providing an implementation of the abstract methods in the
`Policy`{.codeph} class (which is in the `java.security`{.codeph}
package).

The source location for the policy information utilized by the Policy
object is up to the Policy implementation. The Policy reference
implementation obtains its information from static policy configuration
files.

The rest of this document pertains to the Policy reference
implementation and the syntax that must be used in policy files it
reads:

-   [Default Policy
    Implementation](permissions-jdk1.htm#GUID-233A73E2-33C6-4DD0-9EA9-8921ADF40358 "In the Policy reference implementation, the policy can be specified within one or more policy configuration files. The configuration file(s) specify what permissions are allowed for code from a specified code source, and executed by a specified principal. Each configuration file must be encoded in UTF-8.")
-   [Default Policy File
    Locations](permissions-jdk1.htm#GUID-BFF84712-05CF-4C1E-926F-411FDF83AE32 "There is by default a single system-wide policy file, and a single (optional) user policy file. When the Policy is initialized, the system policy is loaded in first, and then the user policy is added to it. If neither policy is present, a built-in policy is used. This built-in policy is the same as the java.policy file installed with the JRE.")
-   [Modifying the Policy
    Implementation](permissions-jdk1.htm#GUID-75C71299-8B56-4AC9-A83F-41BC14535545 "The Policy reference implementation can be modified by editing the security properties file, which is the java.security file in the conf/security directory of the JDK.")
-   [Policy File
    Syntax](permissions-jdk1.htm#GUID-7942E6F8-8AAB-4404-9FE9-E08DD6FFCFFA "The policy configuration file(s) for a JDK installation specifies what permissions (which types of system resource accesses) are granted to code from a specified code source, and executed as a specified principal.")
-   [Policy File
    Examples](permissions-jdk1.htm#GUID-CE19E4A6-897A-47E1-B6AB-3E49327F7364)
-   [Property Expansion in Policy
    Files](permissions-jdk1.htm#GUID-B614FBFF-0C3C-42F3-B766-DE709CA4D73A "Property expansion is possible in policy files and in the security properties file.")
-   [Windows Systems, File Paths, and Property
    Expansion](permissions-jdk1.htm#GUID-6DB03078-DAD5-4A2C-9DF9-58A8F2FA802C "The file path specifications on Windows systems should include two backslashes for each actual single backslash.")
-   [General Expansion in Policy
    Files](permissions-jdk1.htm#GUID-6ACBD24A-F4B8-4B32-BAA4-949199273BE5)

</div>
<div class="sect3">
[]{#GUID-233A73E2-33C6-4DD0-9EA9-8921ADF40358}

### Default Policy Implementation {#JSSEC-GUID-233A73E2-33C6-4DD0-9EA9-8921ADF40358 .sect3}

<div>
In the Policy reference implementation, the policy can be specified
within one or more policy configuration files. The configuration file(s)
specify what permissions are allowed for code from a specified code
source, and executed by a specified principal. Each configuration file
must be encoded in UTF-8.

There is by default a single system-wide policy file, and a single
(optional) user policy file. By default, permissions required by JDK
modules that are loaded by the platform class loader or its ancestors
are always granted.

The Policy reference implementation is initialized the first time its
<span class="apiname">getPermissions</span> method is called, or
whenever its <span class="apiname">refresh</span> method is called.
Initialization involves parsing the policy configuration file(s) (see
[Policy File
Syntax](permissions-jdk1.htm#GUID-7942E6F8-8AAB-4404-9FE9-E08DD6FFCFFA "The policy configuration file(s) for a JDK installation specifies what permissions (which types of system resource accesses) are granted to code from a specified code source, and executed as a specified principal.")),
and then populating the <span class="apiname">Policy</span> object.

</div>
</div>
<div class="sect3">
[]{#GUID-BFF84712-05CF-4C1E-926F-411FDF83AE32}

### Default Policy File Locations {#JSSEC-GUID-BFF84712-05CF-4C1E-926F-411FDF83AE32 .sect3}

<div>
There is by default a single system-wide policy file, and a single
(optional) user policy file. When the Policy is initialized, the system
policy is loaded in first, and then the user policy is added to it. If
neither policy is present, a built-in policy is used. This built-in
policy is the same as the `java.policy`{.codeph} file installed with the
JRE.

<div class="section">
System Policy File Locations

By default, the system policy file is
`<java-home>/conf/security/java.policy`.

The system policy file is meant to grant system-wide code permissions.
The `java.policy`{.codeph} file installed with the JDK allows anyone to
listen on dynamic ports, and allows any code to read certain
\"standard\" properties that are not security-sensitive, such as the
`os.name`{.codeph} and `file.separator`{.codeph} properties.

</div>
<!-- class="section" -->

<div class="section">
User Policy File Location

By default, the user policy file is `<user-home>/.java.policy`.

</div>
<!-- class="section" -->

<div class="section">
Policy File Location and Format

Policy file locations are specified in the security properties file
`<java-home>/conf/security/java.security`.

The policy file locations are specified as the values of properties
whose names are of the following form:

``` {.codeblock dir="ltr"}
policy.url.n
```

Here, `n`{.codeph} is a number. You specify each such property value in
a line of the following form:

``` {.oac_no_warn dir="ltr"}
policy.url.n=URL
```

Here, `URL`{.codeph} is a URL specification. For example, the default
system and user policy files are defined in the security properties file
as:

``` {.codeblock dir="ltr"}
policy.url.1=file:${java.home}/conf/security/java.policy
policy.url.2=file:${user.home}/.java.policy
```

(See [Property Expansion in Policy
Files](permissions-jdk1.htm#GUID-B614FBFF-0C3C-42F3-B766-DE709CA4D73A "Property expansion is possible in policy files and in the security properties file.")
for information about specifying property values via a special syntax,
such as specifying the `java.home`{.codeph} property value via
`${java.home}`{.codeph}.)

You can actually specify a number of URLs (including ones of the form
\"`http://`{.codeph}\"), and all the designated policy files will get
loaded. You can also comment out or change the second one to disable
reading the default user policy file.

The algorithm starts at `policy.url.1`{.codeph}, and keeps incrementing
until it does not find a URL. Thus if you have `policy.url.1`{.codeph}
and `policy.url.3`{.codeph}, and `policy.url.3`{.codeph} will never be
read.

</div>
<!-- class="section" -->

<div class="section">
Specifying an Additional Policy File at Runtime

It is also possible to specify an additional or a different policy file
when invoking execution of an application. This can be done via the
`-Djava.security.policy`{.codeph}</code> command line argument, which
sets the value of the `java.security.policy`{.codeph} property. For
example, if you use following command, where `someURL`{.codeph} is a URL
specifying the location of a policy file, then the specified policy file
will be loaded in addition to all the policy files that are specified in
the security properties file.

``` {.codeblock dir="ltr"}
java -Djava.security.manager -Djava.security.policy=someURL SomeApp
```

The URL can be any regular URL or simply the name of a policy file in
the current directory, as in:

``` {.oac_no_warn dir="ltr"}
java -Djava.security.manager -Djava.security.policy=mypolicy SomeApp
```

The `-Djava.security.manager`{.codeph} option ensures that the default
security manager is installed, and thus the application is subject to
policy checks. It is not required if the application
<span class="apiname">SomeApp</span> installs a security manager.

If you use the following command (note the double equals) then
<span class="italic">just</span> the specified policy file will be used;
all the ones indicated in the security properties file will be ignored.

``` {.codeblock dir="ltr"}
java -Djava.security.manager -Djava.security.policy==someURL SomeApp
```

<div class="infoboxnote" id="GUID-BFF84712-05CF-4C1E-926F-411FDF83AE32__GUID-0823E8DD-1B7F-4ACF-A012-5CB995B6F184">
Note:

The policy file value of the `-Djava.security.policy`{.codeph} option is
ignored if the `policy.allowSystemProperty`{.codeph}property in the
security properties file is set to false. The default is true.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-75C71299-8B56-4AC9-A83F-41BC14535545}

### Modifying the Policy Implementation {#JSSEC-GUID-75C71299-8B56-4AC9-A83F-41BC14535545 .sect3}

<div>
The Policy reference implementation can be modified by editing the
security properties file, which is the `java.security`{.codeph} file in
the `conf/security` directory of the JDK.

An alternative policy class can be given to replace the Policy reference
implementation class, as long as the former is a subclass of the
abstract Policy class and implements the
<span class="apiname">getPermissions</span> method (and other methods as
necessary).

One of the types of properties you can set in `java.security`{.codeph}
is of the following form:

``` {.codeblock dir="ltr"}
    policy.provider=PolicyClassName
```

<span class="variable">PolicyClassName</span> must specify the fully
qualified name of the desired `Policy`{.codeph} implementation class.

The default security properties file entry for this property is the
following:

``` {.codeblock dir="ltr"}
    policy.provider=sun.security.provider.PolicyFile
```

To customize, you can change the property value to specify another
class, as in

``` {.codeblock dir="ltr"}
    policy.provider=com.mycom.MyPolicy
```

</div>
</div>
<div class="sect3">
[]{#GUID-7942E6F8-8AAB-4404-9FE9-E08DD6FFCFFA}

### Policy File Syntax {#JSSEC-GUID-7942E6F8-8AAB-4404-9FE9-E08DD6FFCFFA .sect3}

<div>
The policy configuration file(s) for a JDK installation specifies what
permissions (which types of system resource accesses) are granted to
code from a specified code source, and executed as a specified
principal.

For an applet (or an application running under a security manager) to be
allowed to perform secured actions (such as reading or writing a file),
the applet (or application) must be granted permission for that
particular action. In the Policy reference implementation, that
permission must be granted by a grant entry in a policy configuration
file. See below and the [Java Security Architecture
Specification](https://docs.oracle.com/javase/8/docs/technotes/guides/security/spec/security-spec.doc.html)
for more information. (The only exception is that code always
automatically has permission to read files from its same (URL) location,
and subdirectories of that location; it does not need explicit
permission to do so.)

A policy configuration file essentially contains a list of entries. It
may contain a \"keystore\" entry, and contains zero or more \"grant\"
entries.

</div>
<div class="sect4">
[]{#GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83}

#### Keystore Entry {#JSSEC-GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83 .sect4}

<div>
A <span class="variable">keystore</span> is a database of private keys
and their associated digital certificates such as X.509 certificate
chains authenticating the corresponding public keys. The
[keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) utility
is used to create and administer keystores. The keystore specified in a
policy configuration file is used to look up the public keys of the
signers specified in the grant entries of the file. A keystore entry
must appear in a policy configuration file if any grant entries specify
signer aliases, or if any grant entries specify principal aliases.

At this time, there can be only one
`keystore`{.codeph}/`keystorePasswordURL`{.codeph} entry in the policy
file (other entries following the first one are ignored). This entry can
appear anywhere outside the file\'s grant entries. It has the following
syntax:

``` {.codeblock dir="ltr"}
keystore "some_keystore_url", "keystore_type", "keystore_provider";
keystorePasswordURL "some_password_url";
```

Here,

[<!-- -->]{#GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83__GUID-FA48724B-29BB-4C7C-A743-CC61DFD564A3}some\_keystore\_url
:   Specifies the URL location of the keystore.

[<!-- -->]{#GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83__GUID-B2EE8EF8-E6D6-477E-9B9F-2FC39C56A2B5}some\_password\_url
:   Specifies the URL location of the keystore password.

[<!-- -->]{#GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83__GUID-8F0D4F20-7003-4BE8-9D1B-40A9C65DF0ED}keystore\_type
:   Specifies the keystore type.

[<!-- -->]{#GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83__GUID-03504CED-F2F0-43FE-8C89-3AC56AD7F31F}keystore\_provider
:   Specifies the keystore provider.

<div class="p">
<div class="infoboxnote" id="GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83__GUID-13F2C15E-2BE1-4472-A851-140FC0A69AF5">
Note:

-   The input stream from `some_keystore_url`{.codeph} is passed to the
    <span class="apiname">KeyStore.load</span> method.

-   If NONE is specified as the URL, then a null stream is passed to the
    <span class="apiname">KeyStore.load</span> method. NONE should be
    specified in the URL if the KeyStore is not file-based. For example,
    if it resides on a hardware token device.

-   The URL is relative to the policy file location. If the policy file
    is specified in the security properties file as:

    ``` {.codeblock dir="ltr"}
        policy.url.1=http://foo.example.com/fum/some.policy
    ```

    and that policy file has an entry:

    ``` {.codeblock dir="ltr"}
        keystore ".keystore";
    ```

    then the keystore will be loaded from:

    ``` {.codeblock dir="ltr"}
        http://foo.example.com/fum/.keystore
    ```

-   The URL can also be absolute.

</div>
</div>
A <span class="bold">keystore type</span> defines the storage and data
format of the keystore information, and the algorithms used to protect
private keys in the keystore and the integrity of the keystore itself.
The default type is \"PKCS12\". Thus, if the keystore type is
\"PKCS12\", it does not need to be specified in the keystore entry.

</div>
</div>
<div class="sect4">
[]{#GUID-6E1C0535-58D9-443E-9361-6C9BABB0DCD0}

#### Grant Entries {#JSSEC-GUID-6E1C0535-58D9-443E-9361-6C9BABB0DCD0 .sect4}

<div>
Code being executed is always considered to come from a particular
\"code source\" (represented by an object of type
`CodeSource`{.codeph}). The code source includes not only the location
(URL) where the code originated from, but also a reference to the
certificate(s) containing the public key(s) corresponding to the private
key(s) used to sign the code. Certificates in a code source are
referenced by symbolic alias names from the user\'s keystore. Code is
also considered to be executed as a particular principal (represented by
an object of type `Principal`{.codeph}), or group of principals.

Each <span class="bold">grant entry</span> includes one or more
\"permission entries\" preceded by optional `codeBase`{.codeph},
`signedBy`{.codeph}, and principal name/value pairs that specify which
code you want to grant the permissions. The basic format of a grant
entry is the following:

``` {.codeblock dir="ltr"}
  grant signedBy "signer_names", codeBase "URL",
        principal principal_class_name "principal_name",
        principal principal_class_name "principal_name",
        ... {

      permission permission_class_name "target_name", "action", 
          signedBy "signer_names";
      permission permission_class_name "target_name", "action", 
          signedBy "signer_names";
      ...
  };
        
```

All non-italicized items above must appear as is (although case doesn\'t
matter and some are optional, as noted below). Italicized items
represent variable values.

A grant entry must begin with the word `grant`{.codeph}.

</div>
</div>
<div class="sect4">
[]{#GUID-7450CEFD-8EDC-495E-A7A3-6C2561FA4999}

#### The SignedBy, Principal, and CodeBase Fields {#JSSEC-GUID-7450CEFD-8EDC-495E-A7A3-6C2561FA4999 .sect4}

<div>
The `signedBy`{.codeph}, `codeBase`{.codeph}, and `principal`{.codeph}
values are optional, and the order of these fields does not matter.

A `signedBy`{.codeph} value indicates the alias for a certificate stored
in the keystore. The public key within that certificate is used to
verify the digital signature on the code; you grant the permission(s) to
code signed by the private key corresponding to the public key in the
keystore entry specified by the alias.

The `signedBy`{.codeph} value can be a comma-separated list of multiple
aliases. An example is \"Adam,Eve,Charles\", which means \"signed by
Adam and Eve and Charles\"; the relationship is AND, not OR. To be more
exact, a statement like \"Code signed by Adam\" means \"Code in a class
file contained in a JAR which is signed using the private key
corresponding to the public key certificate in the keystore whose entry
is aliased by Adam\".

The `signedBy`{.codeph} field is optional in that, if it is omitted, it
signifies \"any signer\". It doesn\'t matter whether the code is signed
or not or by whom.

A principal value specifies a
`class_name`{.codeph}/`principal_name`{.codeph} pair which must be
present within the executing thread\'s principal set. The principal set
is associated with the executing code by way of a Subject.

The `principal_class_name`{.codeph} may be set to the wildcard value,
\*, which allows it to match any `Principal`{.codeph} class. In
addition, the `principal_name`{.codeph} may also be set to the wildcard
value, \*, allowing it to match any `Principal`{.codeph} name. When
setting the `principal_class_name`{.codeph} or `principal_name`{.codeph}
to \*, do not surround the \* with quotes. Also, if you specify a
wildcard principal class, you must also specify a wildcard principal
name.

The principal field is optional in that, if it is omitted, it signifies
\"any principals\".

</div>
</div>
<div class="sect4">
[]{#GUID-2636C14A-A783-447A-BE7F-3BF031076117}

#### KeyStore Alias Replacement {#JSSEC-GUID-2636C14A-A783-447A-BE7F-3BF031076117 .sect4}

<div>
If the principal `class_name`{.codeph}/`principal_name`{.codeph} pair is
specified as a single quoted string, then it is treated as a keystore
alias. The keystore is consulted and queried (via the alias) for an X509
Certificate. If one is found, the principal class\_name is automatically
treated as `javax.security.auth.x500.X500Principal`{.codeph}, and the
`principal_name`{.codeph} is automatically treated as the subject
distinguished name from the certificate. If an X509 Certificate mapping
is not found, the entire grant entry is ignored.

A `codeBase`{.codeph} value indicates the code source location; you
grant the permission(s) to code from that location. An empty
`codeBase`{.codeph} entry signifies \"any code\"; it doesn\'t matter
where the code originates from.

<div class="p">
<div class="infoboxnote" id="GUID-2636C14A-A783-447A-BE7F-3BF031076117__GUID-797C0C75-D6F7-479D-A274-5836E058C003">
Note:

A `codeBase`{.codeph} value is a URL and thus should always utilize
slashes (never backslashes) as the directory separator, even when the
code source is actually on a Windows system. Thus, if the source
location for code on a Windows system is actually `C:\somepath\api\`,
then the policy `codeBase`{.codeph} entry should look like:

``` {.codeblock dir="ltr"}
    grant codeBase "file:/C:/somepath/api/" {
        ...
    };
```

</div>
</div>
The exact meaning of a `codeBase`{.codeph} value depends on the
characters at the end. A `codeBase`{.codeph} with a trailing
`"/"`{.codeph} matches all class files (not JAR files) in the specified
directory. A `codeBase`{.codeph} with a trailing `"/*"`{.codeph} matches
all files (both class and JAR files) contained in that directory. A
`codeBase`{.codeph} with a trailing `"/-"`{.codeph} matches all files
(both class and JAR files) in the directory and recursively all files in
subdirectories contained in that directory. The following table
illustrates the different cases:

<div class="tblformalwide" id="GUID-2636C14A-A783-447A-BE7F-3BF031076117__GUID-5FFCB962-D29F-444C-955E-7FD6F5F06472">
Table 1-8 KeyStore Alias

  Codebase URL of Downloaded Code        Codebase URL in Policy           Match?
  -------------------------------------- -------------------------------- --------
  www.example.com/people/gong/           www.example.com/people/gong      Yes
  www.example.com/people/gong/           www.example.com/people/gong/     Yes
  www.example.com/people/gong/           www.example.com/people/gong/\*   Yes
  www.example.com/people/gong/           www.example.com/people/gong/-    Yes
  www.example.com/people/gong/appl.jar   www.example.com/people/gong/     No
  www.example.com/people/gong/appl.jar   www.example.com/people/gong/-    Yes
  www.example.com/people/gong/appl.jar   www.example.com/people/gong/\*   Yes
  www.example.com/people/gong/appl.jar   www.example.com/people/-         Yes
  www.example.com/people/gong/appl.jar   www.example.com/people/\*        No
  www.example.com/people/gong/           www.example.com/people/-         Yes
  www.example.com/people/gong/           www.example.com/people/\*        No

</div>
<!-- class="inftblhruleinformal" -->

</div>
</div>
<div class="sect4">
[]{#GUID-696D4901-33DD-434E-9C25-09EC5AB4D3AB}

#### The Permission Entries {#JSSEC-GUID-696D4901-33DD-434E-9C25-09EC5AB4D3AB .sect4}

<div>
A <span class="bold">permission entry</span> must begin with the word
`permission`{.codeph}. The word `permission_class_name`{.codeph} in the
template above would actually be a specific permission type, such as
`java.io.FilePermission`{.codeph} or
`java.lang.RuntimePermission`{.codeph}.

The \"<span class="variable">action</span>\" is required for many
permission types, such as `java.io.FilePermission`{.codeph} (where it
specifies what type of file access is permitted). It is not required for
categories such as `java.lang.RuntimePermission`{.codeph} where it is
not necessary, you either have the permission specified by the
\"`target_name`{.codeph}\" value following the
<span class="variable">permission\_class\_name</span> or you don\'t.

The `signedBy`{.codeph} name/value pair for a permission entry is
optional. If present, it indicates a signed permission. That is, the
permission class itself must be signed by the given alias(es) in order
for the permission to be granted. For example, suppose you have the
following grant entry:

``` {.codeblock dir="ltr"}
  grant {
      permission Foo "foobar", signedBy "FooSoft";
  };
```

Then this permission of type <span class="variable">Foo</span> is
granted if the `Foo.class`{.codeph} permission was placed in a JAR file
and the JAR file was signed by the private key corresponding to the
public key in the certificate specified by the \"FooSoft\" alias, or if
`Foo.class`{.codeph} is a system class, since system classes are not
subject to policy restrictions.

Items that appear in a permission entry must appear in the specified
order (`permission`{.codeph},
<span class="variable">permission\_class\_name</span>,
\"<span class="variable">target\_name</span>\",
\"<span class="variable">action</span>\", and `signedBy`{.codeph}
\"<span class="variable">signer\_names</span>\"). An entry is terminated
with a semicolon.

Case is unimportant for the identifiers (`permission`{.codeph},
`signedBy`{.codeph}, `codeBase`{.codeph}, etc.) but is significant for
the <span class="variable">permission\_class\_name</span> or for any
string that is passed in as a value.

<div class="infoboxnote" id="GUID-696D4901-33DD-434E-9C25-09EC5AB4D3AB__GUID-E18CACDE-E866-4B47-95A0-4DF104B3B717">
Note:

See [Appendix A: FilePermission Path Name Canonicalization Disabled By
Default](permissions-jdk1.htm#GUID-83063225-0ACB-4909-9BAB-7F7D4E3749E2 "A canonical path is a path that doesn't contain any links or shortcuts. Performing path name canonicalization in a FilePermission object can negatively affect performance.")
for important information about a change in how
<span class="apiname">FilePermission</span> path names are
canonicalized.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-9A8CEB0F-E717-4DAB-91B6-726A79BE4EEB}

#### File Path Specifications on Windows Systems {#JSSEC-GUID-9A8CEB0F-E717-4DAB-91B6-726A79BE4EEB .sect4}

<div>
When you are specifying a `java.io.FilePermission`{.codeph}, the
\"<span class="variable">target\_name</span>\" is a file path. On
Windows systems, whenever you directly specify a file path in a string
(but not in a codebase URL), you need to include two backslashes for
each actual single backslash in the path, as in

``` {.codeblock dir="ltr"}
    grant {
        permission java.io.FilePermission "C:\\users\\cathy\\foo.bat", "read";
    };
```

The reason this is necessary is because the strings are processed by a
tokenizer (`java.io.StreamTokenizer`{.codeph}), which allows \"\\\" to
be used as an escape string (for example, \"\\n\" to indicate a new
line) and which thus requires two backslashes to indicate a single
backslash. After the tokenizer has processed the above file path string,
converting double backslashes to single backslashes, the end result is

``` {.codeblock dir="ltr"}
    "C:\users\cathy\foo.bat"
```

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-CE19E4A6-897A-47E1-B6AB-3E49327F7364}

### Policy File Examples {#JSSEC-GUID-CE19E4A6-897A-47E1-B6AB-3E49327F7364 .sect3}

<div>
<div class="section">
The following policy configuration file contains two entries:

``` {.codeblock dir="ltr"}
  // If the code is signed by "Duke", grant it read/write access to all 
  // files in /tmp:
  grant signedBy "Duke" {
      permission java.io.FilePermission "/tmp/*", "read,write";
  };

  // Grant everyone the following permission:
  grant { 
      permission java.util.PropertyPermission "java.vendor", "read";
  }; 
```

The following policy configuration file specifies that
<span class="italic">only</span> code that satisfies the following
conditions can call methods in the <span class="apiname">Security</span>
class to add or remove providers or to set Security Properties:

-   The code was loaded from a signed JAR file that is in the
    \"`/home/sysadmin/`{.codeph}\" directory on the local file system.
-   The signature can be verified using the public key referenced by the
    alias name \"`sysadmin`{.codeph}\" in the keystore.

``` {.codeblock dir="ltr"}
  grant signedBy "sysadmin", codeBase "file:/home/sysadmin/*" {
      permission java.security.SecurityPermission "Security.insertProvider.*";
      permission java.security.SecurityPermission "Security.removeProvider.*";
      permission java.security.SecurityPermission "Security.setProperty.*";
  };
```

Either component of the policy entry (or both) may be missing.

The following is a policy configuration file where `codeBase`{.codeph}
is missing:

``` {.codeblock dir="ltr"}
  grant signedBy "sysadmin" {
      permission java.security.SecurityPermission "Security.insertProvider.*";
      permission java.security.SecurityPermission "Security.removeProvider.*";
  };
```

If this policy is in effect, then code that comes in a JAR file signed
by \"`sysadmin`{.codeph}\" can add/remove providers, regardless of where
the JAR file originated from.

The following is a policy configuration file without a signer:

``` {.codeblock dir="ltr"}
  grant codeBase "file:/home/sysadmin/-" {
      permission java.security.SecurityPermission "Security.insertProvider.*";
      permission java.security.SecurityPermission "Security.removeProvider.*";
  };
```

In this case, code that comes from anywhere in the
`"home/sysadmin/"`{.codeph} directory on the local file system can
add/remove providers. The code does not need to be signed.

The following is a policy configuration file where neither
`codeBase`{.codeph} nor `signedBy`{.codeph} is included:

``` {.codeblock dir="ltr"}
  grant {
      permission java.security.SecurityPermission "Security.insertProvider.*";
      permission java.security.SecurityPermission "Security.removeProvider.*";
  };
```

Here, with both code source components missing, any code (regardless of
where it originated from, or whether or not it is signed, or who signed
it) can add/remove providers.

The following represents a principal-based entry:

``` {.codeblock dir="ltr"}
  grant principal javax.security.auth.x500.X500Principal "cn=Alice" {
      permission java.io.FilePermission "/home/Alice", "read, write";
  };
```

This permits any code executing as the X500Principal,
\"`cn=Alice`{.codeph}\", permission to read and write to
\"`/home/Alice`{.codeph}".

The following represents a principal-based entry with a wildcard value:

``` {.codeblock dir="ltr"}
  grant principal javax.security.auth.x500.X500Principal * {
      permission java.io.FilePermission "/tmp", "read, write";
  };
```

This permits any code executing as an X500Principal (regardless of the
distinguished name), permission to read and write to \"`/tmp`{.codeph}".

The following example shows a grant statement with both codesource and
principal information:

``` {.codeblock dir="ltr"}
  grant codebase "http://www.games.example.com",
        signedBy "Duke",
        principal javax.security.auth.x500.X500Principal "cn=Alice" {
      permission java.io.FilePermission "/tmp/games", "read, write";
  };
```

This allows code downloaded from \"`www.games.example.com`{.codeph}\",
signed by \"`Duke`{.codeph}\", and executed by \"`cn=Alice`{.codeph}\",
permission to read and write into the \"`/tmp/games`{.codeph}\"
directory.

The following example shows a grant statement with KeyStore alias
replacement:

``` {.codeblock dir="ltr"}
  keystore "http://foo.example.com/blah/.keystore";

  grant principal "alice" {
      permission java.io.FilePermission "/tmp/games", "read, write";
  };
```

\"`alice`{.codeph}\" will be replaced by the following:

``` {.codeblock dir="ltr"}
    javax.security.auth.x500.X500Principal "cn=Alice"
```

This assumes that X.509 certificate associated with the keystore alias,
`alice`{.codeph}, has a subject distinguished name of
\"`cn=Alice`{.codeph}\". This allows code executed by the X500Principal
\"`cn=Alice`{.codeph}\" permission to read and write into the
\"`/tmp/games`{.codeph}\" directory.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-B614FBFF-0C3C-42F3-B766-DE709CA4D73A}

### Property Expansion in Policy Files {#JSSEC-GUID-B614FBFF-0C3C-42F3-B766-DE709CA4D73A .sect3}

<div>
Property expansion is possible in policy files and in the security
properties file.

<div class="section">
Property expansion is similar to expanding variables in a shell. That
is, when a string like

``` {.codeblock dir="ltr"}
    ${some.property}
```

appears in a policy file, or in the security properties file, it will be
expanded to the value of the system property. For example,

``` {.codeblock dir="ltr"}
    permission java.io.FilePermission "${user.home}", "read";
```

will expand \"`${user.home}`{.codeph}\" to use the value of the
\"user.home\" system property. If that property\'s value is
\"`/home/cathy`{.codeph}\", then the above is equivalent to

``` {.codeblock dir="ltr"}
    permission java.io.FilePermission "/home/cathy", "read";
```

In order to assist in platform-independent policy files, you can also
use the special notation of \"`${/}`{.codeph}\", which is a shortcut for
`${file.separator}`{.codeph}\". This allows things like

``` {.codeblock dir="ltr"}
    permission java.io.FilePermission "${user.home}${/}*", "read";
```

If the value of the \"`user.home`{.codeph} \" property is
`/home/cathy`{.codeph}, and you are on Solaris, Linux, or macOS, the
above gets converted to:

``` {.codeblock dir="ltr"}
    permission java.io.FilePermission "/home/cathy/*", "read";
```

If on the other hand the \"`user.home`{.codeph}\" value is
`C:\users\cathy`{.codeph} and you are on a Windows system, the above
gets converted to:

``` {.codeblock dir="ltr"}
    permission java.io.FilePermission "C:\users\cathy\*", "read";
```

Also, as a special case, if you expand a property in a codebase, such as

``` {.codeblock dir="ltr"}
    grant codeBase "file:${my.libraries}/api/"
```

then any file separator characters will be automatically converted to
`/`{.codeph} characters. For example, suppose the value of
`my.libraries`{.codeph} is `C:\Users\me\lib`. Thus on a Windows system,
the above would get converted to

``` {.codeblock dir="ltr"}
    grant codeBase "file:C:/Users/me/lib/api/"
```

Thus you don\'t need to use `${/}`{.codeph} in codebase strings (and you
shouldn\'t). Property expansion takes place anywhere a double quoted
string is allowed in the policy file. This includes the
<span class="variable">\"signer\_names\"</span>,
<span class="variable">\"URL\"</span>,
<span class="variable">\"target\_name\"</span>, and
<span class="variable">\"action\"</span> fields. Whether or not property
expansion is allowed is controlled by the value of the
\"`policy.expandProperties`{.codeph}\" property in the security
properties file. If the value of this property is true (the default),
expansion is allowed.

<div class="infoboxnote" id="GUID-B614FBFF-0C3C-42F3-B766-DE709CA4D73A__GUID-EA7920CD-C466-4CDA-A721-50FC4DE60EAA">
Note:

You can\'t use nested properties; they will not work. For example,

``` {.codeblock dir="ltr"}
    "${user.${foo}}"
```

doesn\'t work, even if the \"`foo`{.codeph}\" property is set to
\"`home`{.codeph}\". The reason is the property parser doesn\'t
recognize nested properties; it simply looks for the first
\"`${`{.codeph}\", and then keeps looking until it finds the first
\"`}`{.codeph}\" and tries to interpret the result (in this case,
\"`${user.$foo}`{.codeph}\") as a property, but fails if there is no
such property.

</div>
<div class="infoboxnote" id="GUID-B614FBFF-0C3C-42F3-B766-DE709CA4D73A__GUID-F7E9BDFF-52F9-40A9-AD58-D924458266D5">
Note:

If a property can\'t be expanded in a grant entry, permission entry, or
keystore entry, that entry is ignored. For example, if the system
property \"`foo`{.codeph}\" is not defined and you have:

``` {.codeblock dir="ltr"}
    grant codeBase "${foo}" {
        permission ...;
        permission ...;
    };
```

then all the permissions in this grant entry are ignored. If you have

``` {.codeblock dir="ltr"}
    grant {
        permission Foo "${foo}";
        permission Bar "barTarget";
    };
```

then only the \"`permission Foo...`{.codeph}\" entry is ignored. And
finally, if you have

``` {.codeblock dir="ltr"}
    keystore "${foo}";
```

then the keystore entry is ignored.

</div>
</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-6DB03078-DAD5-4A2C-9DF9-58A8F2FA802C}

### Windows Systems, File Paths, and Property Expansion {#JSSEC-GUID-6DB03078-DAD5-4A2C-9DF9-58A8F2FA802C .sect3}

<div>
The file path specifications on Windows systems should include two
backslashes for each actual single backslash.

<div class="section">
As mentioned in [File Path Specifications on Windows
Systems](permissions-jdk1.htm#GUID-9A8CEB0F-E717-4DAB-91B6-726A79BE4EEB),
on Windows systems, when you directly specify a file path in a string
(but not in a codebase URL), you need to include two backslashes for
each actual single backslash in the path, as in

``` {.codeblock dir="ltr"}
    grant {
        permission java.io.FilePermission "C:\\users\\cathy\\foo.bat", "read";
    };
```

This is because the strings are processed by a tokenizer
(`java.io.StreamTokenizer`{.codeph}), which allows \"`\`{.codeph}\" to
be used as an escape string (e.g., \"`\n`{.codeph}\" to indicate a new
line) and which thus requires two backslashes to indicate a single
backslash. After the tokenizer has processed the above file path string,
converting double backslashes to single backslashes, the end result is

<div class="p">
``` {.codeblock dir="ltr"}
    "C:\users\cathy\foo.bat"
```

</div>
Expansion of a property in a string takes place after the tokenizer has
processed the string. Thus if you have the string

``` {.codeblock dir="ltr"}
    "${user.home}\\foo.bat"
```

then first the tokenizer processes the string, converting the double
backslashes to a single backslash, and the result is

``` {.codeblock dir="ltr"}
    "${user.home}\foo.bat"
```

Then the `${user.home}`{.codeph} property is expanded and the end result
is

``` {.codeblock dir="ltr"}
    "C:\users\cathy\foo.bat"
```

assuming the \"`user.home`{.codeph}\" value is
`C:\users\cathy`{.codeph}. Of course, for platform independence, it
would be better if the string was initially specified without any
explicit slashes, i.e., using the `${/}`{.codeph} property instead, as
in

``` {.codeblock dir="ltr"}
    "${user.home}${/}foo.bat"
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect3">
[]{#GUID-6ACBD24A-F4B8-4B32-BAA4-949199273BE5}

### General Expansion in Policy Files {#JSSEC-GUID-6ACBD24A-F4B8-4B32-BAA4-949199273BE5 .sect3}

<div>
<div class="section">
Generalized forms of expansion are also supported in policy files. For
example, permission names may contain a string of the following form:

``` {.oac_no_warn dir="ltr"}
${{protocol:protocol_data}}
```

If such a string occurs in a permission name, then the value in
<span class="italic">protocol</span> determines the exact type of
expansion that should occur, and
<span class="italic">protocol\_data</span> is used to help perform the
expansion. <span class="italic">protocol\_data</span> may be empty, in
which case the above string should simply take the form:

``` {.oac_no_warn dir="ltr"}
${{protocol}}
```

There are two protocols supported in the default policy file
implementation:

1.  `${{self}}`{.codeph}

    The protocol, <span class="bold">`self`{.codeph}</span>, denotes a
    replacement of the entire string, `${{self}}`{.codeph}, with one or
    more principal class/name pairs. The exact replacement performed
    depends upon the contents of the grant clause to which the
    permission belongs.

    If the grant clause does not contain any principal information, the
    permission will be ignored (permissions containing
    `${{self}}`{.codeph} in their target names are only valid in the
    context of a principal-based grant clause). For example,
    `BarPermission`{.codeph} will always be ignored in the following
    grant clause:

    ``` {.codeblock dir="ltr"}
    grant codebase "www.example.com", signedby "duke" {
        permission BarPermission "... ${{self}} ...";
    };
    ```

    If the grant clause contains principal information,
    `${{self}}`{.codeph} will be replaced with that same principal
    information. For example, `${{self}}`{.codeph} in
    `BarPermission`{.codeph} will be replaced with
    <span class="bold">`javax.security.auth.x500.X500Principal "cn=Duke"`{.codeph}</span>
    in the following grant clause:

    ``` {.codeblock dir="ltr"}
    grant principal javax.security.auth.x500.X500Principal "cn=Duke" {
        permission BarPermission "... ${{self}} ...";
    };
    ```

    If there is a comma-separated list of principals in the grant
    clause, then `${{self}}`{.codeph} will be replaced by the same
    comma-separated list or principals. In the case where both the
    principal class and name are wildcarded in the grant clause,
    `${{self}}`{.codeph} is replaced with all the principals associated
    with the `Subject`{.codeph} in the current
    `AccessControlContext`{.codeph}.

    The following example describes a scenario involving both
    <span class="bold">`self`{.codeph}</span> and [KeyStore Alias
    Replacement](permissions-jdk1.htm#GUID-2636C14A-A783-447A-BE7F-3BF031076117)
    together:

    ``` {.codeblock dir="ltr"}
    keystore "http://foo.example.com/blah/.keystore";

    grant principal "duke" {
        permission BarPermission "... ${{self}} ...";
    };
    ```

    In the above example, \"`duke`{.codeph}\" will first be expanded
    into `javax.security.auth.x500.X500Principal "cn=Duke"`{.codeph}
    assuming the X.509 certificate associated with the
    `KeyStore`{.codeph} alias, \"`duke`{.codeph}\", has a subject
    distinguished name of \"`cn=Duke`{.codeph}\". Next,
    `${{self}}`{.codeph} will be replaced with the same principal
    information that was just expanded in the grant clause:
    <span class="bold">`javax.security.auth.x500.X500Principal "cn=Duke"`{.codeph}</span>.

2.  `${{alias:alias_name}}`{.codeph}

    The protocol, <span class="bold">`alias`{.codeph}</span>, denotes a
    <span class="apiname">java.security.KeyStore</span> alias
    substitution. The `KeyStore`{.codeph} used is the one specified in
    the [Keystore
    Entry](permissions-jdk1.htm#GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83).
    <span class="variable">alias\_name</span> represents an alias into
    the `KeyStore`{.codeph}. `${{alias:alias_name}}`{.codeph} is
    replaced with
    <span class="bold">`javax.security.auth.x500.X500Principal "DN"`{.codeph}</span>,
    where <span class="variable">DN</span> represents the subject
    distinguished name of the certificate belonging to
    <span class="variable">alias\_name</span>. For example:

    ``` {.codeblock dir="ltr"}
    keystore "http://foo.example.com/blah/.keystore";

    grant codebase "www.example.com" {
        permission BarPermission "... ${{alias:duke}} ...";
    };
    ```

    In the above example the X.509 certificate associated with the
    alias, <span class="variable">duke</span>, is retrieved from the
    `KeyStore`{.codeph},
    <span class="variable">foo.example.com/blah/.keystore</span>.
    Assuming duke\'s certificate specifies
    \"`o=dukeOrg, cn=duke`{.codeph}\" as the subject distinguished name,
    then `${{alias:duke}}`{.codeph} is replaced with
    <span class="bold">`javax.security.auth.x500.X500Principal "o=dukeOrg, cn=duke"`{.codeph}</span>.

    The permission entry is ignored under the following error
    conditions:

    -   The keystore entry is unspecified
    -   The <span class="variable">alias\_name</span> is not provided
    -   The certificate for <span class="variable">alias\_name</span>
        can not be retrieved
    -   The certificate retrieved is not an X.509 certificate

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-83063225-0ACB-4909-9BAB-7F7D4E3749E2}

Appendix A: FilePermission Path Name Canonicalization Disabled By Default {#JSSEC-GUID-83063225-0ACB-4909-9BAB-7F7D4E3749E2 .sect2}
-------------------------------------------------------------------------

<div>
A canonical path is a path that doesn\'t contain any links or shortcuts.
Performing path name canonicalization in a `FilePermission`{.codeph}
object can negatively affect performance.

Before JDK 9, path names were canonicalized when two
`FilePermission`{.codeph} objects were compared. This allowed a program
to access a file using a different name than the name that was granted
to a `FilePermission`{.codeph} object in a policy file, as long as the
object pointed to the same file. Because the canonicalization had to
access the underlying file system, it could be quite slow.

In JDK 9, path name canonicalization is disabled by default. This means
two `FilePermission`{.codeph} objects aren't equal to each other if one
uses an absolute path and the other uses a relative path, or one uses a
symbolic link and the other uses a target, or one uses a Windows long
name and the other uses a DOS-style 8.3 name. This is true even if they
all point to the same file in the file system.

Therefore, if a path name is granted to a `FilePermission`{.codeph}
object in a policy file, then the program should also access that file
using the same path name style. For example, if the path name in the
policy file is using a symbolic link, then the program should also use
that symbolic link. Accessing the file with the target path name will
fail the permission check.

<div class="section">
Compatibility Layer

A compatibility layer has been added to ensure that granting a
`FilePermission`{.codeph} object for a relative path will permit
applications to access the file with an absolute path (and conversely).
This works for the default Policy provider and the [Limited
<span class="apiname">doPrivileged</span>](https://docs.oracle.com/javase/10/docs/api/java/security/AccessController.html#doPrivileged-java.security.PrivilegedExceptionAction-java.security.AccessControlContext-java.security.Permission...-)
calls.

For example, a `FilePermission`{.codeph} object on a file with a
relative path name of `"a"`{.codeph} no longer implies a
`FilePermission`{.codeph} object on the same file with an absolute path
name as `"/pwd/a"` (`"pwd"`{.codeph} is the current working directory).
Granting code a `FilePermission`{.codeph} object to read `"a"`{.codeph}
allows that code to also read `"/pwd/a"`{.codeph} when a Security
Manager is enabled.

The compatibility layer doesn't cover translations between symbolic
links and targets, or Windows long names and DOS-style 8.3 names, or any
other different name forms that can be canonicalized to the same name.

</div>
<!-- class="section" -->

<div class="section">
Customizing Path Name Canonicalization

The system properties in [Table
1-9](permissions-jdk1.htm#GUID-83063225-0ACB-4909-9BAB-7F7D4E3749E2__LISTOFSYSTEMPROPERTIESTOCUSTOMIZEPA-C3268ADF "List of system properties to customize path name canonicalization.")
can be used to customize the `FilePermission`{.codeph} path name
canonicalization. See [How to Specify a java.lang.System
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363).

<div class="tblformalwide" id="GUID-83063225-0ACB-4909-9BAB-7F7D4E3749E2__LISTOFSYSTEMPROPERTIESTOCUSTOMIZEPA-C3268ADF">
Table 1-9 System Properties to Customize Path Name Canonicalization

+-----------------------+-----------------------+-----------------------+
| System Property       | Default Value         | Description           |
+:======================+:======================+:======================+
| `jdk.io.permissionsUs | false                 | The system property   |
| eCanonicalPath`{.code |                       | can be used to enable |
| ph}                   |                       | or disable path name  |
|                       |                       | canonicalization in   |
|                       |                       | the                   |
|                       |                       | `FilePermission`{.cod |
|                       |                       | eph}                  |
|                       |                       | object.               |
|                       |                       |                       |
|                       |                       | -   To disable        |
|                       |                       |     `FilePermission`{ |
|                       |                       | .codeph}              |
|                       |                       |     path name         |
|                       |                       |     canonicalization, |
|                       |                       |     set               |
|                       |                       |     `jdk.io.permissio |
|                       |                       | nsUseCanonicalPath=fa |
|                       |                       | lse`{.codeph}.        |
|                       |                       |                       |
|                       |                       | -   To enable         |
|                       |                       |     `FilePermission`{ |
|                       |                       | .codeph}              |
|                       |                       |     path name         |
|                       |                       |     canonicalization, |
|                       |                       |     set               |
|                       |                       |     `jdk.io.permissio |
|                       |                       | nsUseCanonicalPath=tr |
|                       |                       | ue`{.codeph}.         |
+-----------------------+-----------------------+-----------------------+
| `jdk.security.filePer | false                 | The system property   |
| mCompat`{.codeph}     |                       | can be used to extend |
|                       |                       | the compatibility     |
|                       |                       | layer to support      |
|                       |                       | third-party Policy    |
|                       |                       | implementations.      |
|                       |                       |                       |
|                       |                       | -   To disable the    |
|                       |                       |     system property,  |
|                       |                       |     set               |
|                       |                       |     `jdk.security.fil |
|                       |                       | ePermCompat=false`{.c |
|                       |                       | odeph}.               |
|                       |                       |                       |
|                       |                       |     The               |
|                       |                       |     `FilePermission`{ |
|                       |                       | .codeph}              |
|                       |                       |     for a relative    |
|                       |                       |     path will permit  |
|                       |                       |     applications to   |
|                       |                       |     access the file   |
|                       |                       |     with an absolute  |
|                       |                       |     path for the      |
|                       |                       |     default Policy    |
|                       |                       |     provider and the  |
|                       |                       |     [Limited          |
|                       |                       |     <span class="apin |
|                       |                       | ame">doPrivileged</sp |
|                       |                       | an>](https://docs.ora |
|                       |                       | cle.com/javase/10/doc |
|                       |                       | s/api/java/security/A |
|                       |                       | ccessController.html# |
|                       |                       | doPrivileged-java.sec |
|                       |                       | urity.PrivilegedExcep |
|                       |                       | tionAction-java.secur |
|                       |                       | ity.AccessControlCont |
|                       |                       | ext-java.security.Per |
|                       |                       | mission...-)          |
|                       |                       |     method.           |
|                       |                       |                       |
|                       |                       | -   To extend the     |
|                       |                       |     compatibility     |
|                       |                       |     layer to support  |
|                       |                       |     third-party       |
|                       |                       |     Policy            |
|                       |                       |     implementations,  |
|                       |                       |     set               |
|                       |                       |     `jdk.security.fil |
|                       |                       | ePermCompat=true`{.co |
|                       |                       | deph}.                |
|                       |                       |                       |
|                       |                       |     The               |
|                       |                       |     `FilePermission`{ |
|                       |                       | .codeph}              |
|                       |                       |     for a relative    |
|                       |                       |     path will permit  |
|                       |                       |     applications to   |
|                       |                       |     access the file   |
|                       |                       |     with an absolute  |
|                       |                       |     path for the      |
|                       |                       |     default Policy    |
|                       |                       |     provider, the     |
|                       |                       |     [Limited          |
|                       |                       |     <span class="apin |
|                       |                       | ame">doPrivileged</sp |
|                       |                       | an>](https://docs.ora |
|                       |                       | cle.com/javase/10/doc |
|                       |                       | s/api/java/security/A |
|                       |                       | ccessController.html# |
|                       |                       | doPrivileged-java.sec |
|                       |                       | urity.PrivilegedExcep |
|                       |                       | tionAction-java.secur |
|                       |                       | ity.AccessControlCont |
|                       |                       | ext-java.security.Per |
|                       |                       | mission...-)          |
|                       |                       |     method, and for   |
|                       |                       |     third-party       |
|                       |                       |     Policy            |
|                       |                       |     implementations.  |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

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
| -------------------- | O | -------------------- |
| -------------------- | r | ---                  |
| --- ---------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ------- --           | e | )\                   |
|                      | L |             <span cl |
| [![Previous](../../d | o | ass="icon">Contents< |
| common/gifs/leftnav. | g | /span>](toc.htm)     |
| gif)\                | o |   -- --------------- |
|               [![Nex | ] | -------------------- |
| t](../../dcommon/gif | ( | -------------------- |
| s/rightnav.gif)\     | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](j | . |                      |
| ava-security-standar | . |                      |
| d-algorithm-names.ht | / |                      |
| m)   <span class="ic | d |                      |
| on">Next</span>](tro | c |                      |
| ubleshooting-securit | o |                      |
| y.htm)               | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| -------------------- | / |                      |
| --- ---------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ------- --           | s |                      |
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
