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

  -------------------------------------------------------------------------------------- ----------------------------------------------------------------------- --
                      [![Previous](../../dcommon/gifs/leftnav.gif)\                                    [![Next](../../dcommon/gifs/rightnav.gif)\                
   <span class="icon">Previous</span>](source-code-jaas-and-java-gss-api-tutorials.htm)   <span class="icon">Next</span>](single-sign-using-kerberos-java1.htm)  
  -------------------------------------------------------------------------------------- ----------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-DFC5108C-A999-4F95-942F-21C0DD83F48B}<!-- End Header -->

Related Documentation {#JSSEC-GUID-DFC5108C-A999-4F95-942F-21C0DD83F48B .sect1}
=====================

<div>
-   API specifications

    -   [<span class="apiname">com.sun.security.jgss</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/jgss/package-summary.html)
        package
    -   [<span class="apiname">com.sun.security.auth</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/package-summary.html)
        package
    -   [<span class="apiname">com.sun.security.auth.callback</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/callback/package-summary.html)
        package
    -   [<span class="apiname">com.sun.security.auth.login</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/login/package-summary.html)
        package
    -   [<span class="apiname">com.sun.security.auth.module</span>](https://docs.oracle.com/javase/10/docs/api/com/sun/security/auth/module/package-summary.html)
        package

-   User guides and tutorials

    -   [Java Authentication and Authorization Service (JAAS) Reference
        Guide](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-2A935F5E-0803-411D-B6BC-F8C64D01A25C)
    -   [Java Security
        Tutorial](https://docs.oracle.com/javase/tutorial/security/index.html)

-   Other Java Security Documentation

    -   [Default Policy Implementation and Policy File
        Syntax](permissions-jdk1.htm#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D)
    -   [Permissions in the
        JDK](permissions-jdk1.htm#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.")
    -   [Single Sign-on Using Kerberos in
        Java](single-sign-using-kerberos-java1.htm#GUID-D4230975-A28B-4532-B1DD-3C7219A4867F)
    -   [Java SE Platform Security
        Architecture](java-se-platform-security-architecture.htm#GUID-D6C53B30-01F9-49F1-9F61-35815558422B "This section explains what privileged code is and what it is used for. It also shows you how to use the doPrivileged API.This section describes the doPrivileged API and the use of the privileged feature.If you are using a lambda expression or anonymous inner class, then any local variables you access must be final or effectively final.If the action performed in your run method could throw a checked exception (one that must be listed in the throws clause of a method), then you need to use the PrivilegedExceptionAction interface instead of the PrivilegedAction interface.The typical use case of the doPrivileged method is to enable the method that invokes it to perform one or more actions that require permission checks without requiring the callers of the current method to have all the necessary permissions.When coding the current method, you want to temporarily extend the permission of the calling method to perform an action.Marking code as privileged enables a piece of trusted code to temporarily enable access to more resources than are available directly to the code that called it.The doPrivileged method can be invoked reflectively using the java.lang.reflect.Method.invoke method.")

-   Reference document

    -   [Generic Security Service API Version 2: Java Bindings
        Update](https://tools.ietf.org/html/rfc5653)

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
| -------- ----------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
|  --                  | L |             <span cl |
|                      | o | ass="icon">Contents< |
|   [![Previous](../.. | g | /span>](toc.htm)     |
| /dcommon/gifs/leftna | o |   -- --------------- |
| v.gif)\              | ] | -------------------- |
|                      | ( | -------------------- |
|    [![Next](../../dc | . | ---                  |
| ommon/gifs/rightnav. | . |                      |
| gif)\                | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](s | / |                      |
| ource-code-jaas-and- | d |                      |
| java-gss-api-tutoria | c |                      |
| ls.htm)   <span clas | o |                      |
| s="icon">Next</span> | m |                      |
| ](single-sign-using- | m |                      |
| kerberos-java1.htm)  | o |                      |
|                      | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| -------- ----------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
|  --                  | a |                      |
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
