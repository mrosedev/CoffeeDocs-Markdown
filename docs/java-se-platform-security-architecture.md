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

  ------------------------------------------------------------------ ----------------------------------------------------------------------------- --
            [![Previous](../../dcommon/gifs/leftnav.gif)\                             [![Next](../../dcommon/gifs/rightnav.gif)\                   
   <span class="icon">Previous</span>](java-security-overview1.htm)   <span class="icon">Next</span>](java-security-standard-algorithm-names.htm)  
  ------------------------------------------------------------------ ----------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-D6C53B30-01F9-49F1-9F61-35815558422B}<!-- End Header -->

Java SE Platform Security Architecture {#JSSEC-GUID-D6C53B30-01F9-49F1-9F61-35815558422B .sect1}
======================================

<div>
This document gives an overview of the motivation of the major security
features implemented for the JDK, describes the classes that are part of
the Java security architecture, discusses the impact of this
architecture on existing code, and gives thoughts on writing
security-sensitive code.

</div>
<div class="sect2">
[]{#GUID-C203D80F-C730-45C3-AB95-D4E61FD6D89C}

Introduction {#JSSEC-GUID-C203D80F-C730-45C3-AB95-D4E61FD6D89C .sect2}
------------

<div>
Since the inception of Java technology, there has been strong and
growing interest around the security of the Java platform as well as new
security issues raised by the deployment of Java technology.

From a technology provider\'s point of view, Java security includes two
aspects:

-   Provide the Java platform as a secure, ready-built platform on which
    to run Java-enabled applications in a secure fashion.
-   Provide security tools and services implemented in the Java
    programming language that enable a wider range of security-sensitive
    applications, for example, in the enterprise world.

This document discusses issues related to the first aspect, where the
customers for such technologies include vendors that bundle or embed
Java technology in their products (such as browsers and operating
systems).

</div>
<div class="sect3">
[]{#GUID-CF079719-BCCD-44B5-B637-288D0D28D4F0}

### The Original Sandbox Model {#JSSEC-GUID-CF079719-BCCD-44B5-B637-288D0D28D4F0 .sect3}

<div>
The original security model provided by the Java platform is known as
the sandbox model, which existed in order to provide a very restricted
environment in which to run untrusted code obtained from the open
network. The essence of the sandbox model is that local code is trusted
to have full access to vital system resources (such as the file system)
while downloaded remote code (an applet) is not trusted and can access
only the limited resources provided inside the sandbox. This sandbox
model is illustrated in the figure below.

<span>![Description of jssec\_dt\_030\_anc4.eps
follows](img/jssec_dt_030_anc4.png "Description of jssec_dt_030_anc4.eps follows")\
[Description of the illustration
jssec\_dt\_030\_anc4.eps](img_text/jssec_dt_030_anc4.htm)</span>

The sandbox model was deployed through the Java Development Kit (JDK),
and was generally adopted by applications built with JDK 1.0, including
Java-enabled web browsers.

Overall security is enforced through a number of mechanisms. First of
all, the language is designed to be type-safe and easy to use. The hope
is that the burden on the programmer is such that the likelihood of
making subtle mistakes is lessened compared with using other programming
languages such as C or C++. Language features such as automatic memory
management, garbage collection, and range checking on strings and arrays
are examples of how the language helps the programmer to write safe
code.

Second, compilers and a bytecode verifier ensure that only legitimate
Java bytecodes are executed. The bytecode verifier, together with the
Java Virtual Machine, guarantees language safety at run time.

Moreover, a classloader defines a local name space, which can be used to
ensure that an untrusted applet cannot interfere with the running of
other programs.

Finally, access to crucial system resources is mediated by the Java
Virtual Machine and is checked in advance by a
<span class="apiname">SecurityManager</span> class that restricts the
actions of a piece of untrusted code to the bare minimum.

JDK 1.1 introduced the concept of a \"signed applet\", as illustrated by
the figure below. In that release, a correctly digitally signed applet
is treated as if it is trusted local code if the signature key is
recognized as trusted by the end system that receives the applet. Signed
applets, together with their signatures, are delivered in the JAR (Java
Archive) format. In JDK 1.1, unsigned applets still run in the sandbox.

<span>![Description of jssec\_dt\_029\_anc3.eps
follows](img/jssec_dt_029_anc3.png "Description of jssec_dt_029_anc3.eps follows")\
[Description of the illustration
jssec\_dt\_029\_anc3.eps](img_text/jssec_dt_029_anc3.htm)</span>

</div>
</div>
<div class="sect3">
[]{#GUID-C574845A-4D55-4EB1-8D73-326C8B755C2D}

### Evolving the Sandbox Model {#JSSEC-GUID-C574845A-4D55-4EB1-8D73-326C8B755C2D .sect3}

<div>
The new Java SE Platform Security Architecture, illustrated in the
figure below, is introduced primarily for the following purposes.

![Description of jssec\_dt\_032\_anc9.eps
follows](img/jssec_dt_032_anc9.png "Description of jssec_dt_032_anc9.eps follows")\
[Description of the illustration
jssec\_dt\_032\_anc9.eps](img_text/jssec_dt_032_anc9.htm)

-   Fine-grained access control.

    This capability existed in the JDK from the beginning, but to use
    it, the application writer had to do substantial programming (e.g.,
    by subclassing and customizing the
    <span class="apiname">SecurityManager</span> and
    <span class="apiname">ClassLoader</span> classes). The HotJava
    browser 1.0 is such an application, as it allows the browser user to
    choose from a small number of different security levels.

    However, such programming is extremely security-sensitive and
    requires sophisticated skills and in-depth knowledge of computer
    security. The new architecture will make this exercise simpler and
    safer.

-   Easily configurable security policy.

    Once again, this capability existed previously in the JDK but was
    not easy to use. Moreover, writing security code is not
    straightforward, so it is desirable to allow application builders
    and users to configure security policies without having to program.

-   Easily extensible access control structure.

    Up to JDK 1.1, in order to create a new access permission, you had
    to add a new `check`{.codeph} method to the
    <span class="apiname">SecurityManager</span> class. The new
    architecture allows typed permissions (each representing an access
    to a system resource) and automatic handling of all permissions
    (including yet-to-be-defined permissions) of the correct type. No
    new method in the <span class="apiname">SecurityManager</span> class
    needs to be created in most cases. (In fact, we have so far not
    encountered a situation where a new method must be created.)

-   Extension of security checks to all Java programs, including
    applications as well as applets.

    There is no longer a built-in concept that all local code is
    trusted. Instead, local code (e.g., non-system code, application
    packages installed on the local file system) is subjected to the
    same security control as applets, although it is possible, if
    desired, to declare that the policy on local code (or remote code)
    be the most liberal, thus enabling such code to effectively run as
    totally trusted. The same principle applies to signed applets and
    any Java application.

    Finally, an implicit goal is to make internal adjustment to the
    design of security classes (including the
    <span class="apiname">SecurityManager</span> and
    <span class="apiname">ClassLoader</span> classes) to reduce the
    risks of creating subtle security holes in future programming.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-2C2D6A1A-01CA-4C51-9BD4-33E5B1578E00}

Protection Mechanisms -- Overview of Basic Concepts {#JSSEC-GUID-2C2D6A1A-01CA-4C51-9BD4-33E5B1578E00 .sect2}
---------------------------------------------------

<div>
We now go over, in some detail, the new protection architecture and give
a brief explanation of its functionality. We start with an overview of
the basic concepts behind the new architecture. We then introduce the
major new classes in a natural order, starting with permission
specifications, going on to the policy and related features, followed by
access control and its usage, and then covering secure class loading and
resolution.

A fundamental concept and important building block of system security is
the protection domain \[Saltzer and Schroeder 75\]. A domain can be
scoped by the set of objects that are currently directly accessible by a
principal, where a principal is an entity in the computer system to
which permissions (and as a result, accountability) are granted. The
sandbox utilized in JDK 1.0 is one example of a protection domain with a
fixed boundary.

The protection domain concept serves as a convenient mechanism for
grouping and isolation between units of protection. For example, it is
possible (but not yet provided as a built-in feature) to separate
protection domains from interacting with each other so that any
permitted interaction must be either through trusted system code or
explicitly allowed by the domains concerned. Note that existing object
accessibility rules remain valid under the new security architecture.

Protection domains generally fall into two distinct categories: system
domain and application domain. It is important that all protected
external resources, such as the file system, the networking facility,
and the screen and keyboard, be accessible only via system domains. The
figure below illustrates the domain composition of a Java application
environment.

![Description of jssec\_dt\_028\_anc2.eps
follows](img/jssec_dt_028_anc2.png "Description of jssec_dt_028_anc2.eps follows")\
[Description of the illustration
jssec\_dt\_028\_anc2.eps](img_text/jssec_dt_028_anc2.htm)

A domain conceptually encloses a set of classes whose instances are
granted the same set of permissions. Protection domains are determined
by the policy currently in effect. The Java application environment
maintains a mapping from code (classes and instances) to their
protection domains and then to their permissions, as illustrated by the
figure below.

![Description of jssec\_dt\_026\_anc.eps
follows](img/jssec_dt_026_anc.png "Description of jssec_dt_026_anc.eps follows")\
[Description of the illustration
jssec\_dt\_026\_anc.eps](img_text/jssec_dt_026_anc.htm)

A thread of execution (which is often, but not necessarily tied to, a
single Java thread, which in turn is not necessarily tied to the thread
concept of the underlying operation system) may occur completely within
a single protection domain or may involve an application domain and also
the system domain. For example, an application that prints a message out
will have to interact with the system domain that is the only access
point to an output stream. In this case, it is crucial that at any time
the application domain does not gain additional permissions by calling
the system domain. Otherwise, there can be serious security
implications.

In the reverse situation where a system domain invokes a method from an
application domain, such as when the AWT system domain calls an
applet\'s paint method to display the applet, it is again crucial that
at any time the effective access rights are the same as current rights
enabled in the application domain.

In other words, a less \"powerful\" domain cannot gain additional
permissions as a result of calling or being called by a more powerful
domain.

This discussion of one thread involving two protection domains naturally
generalizes to a thread that traverses multiple protection domains. A
simple and prudent rule of thumb for calculating permissions is the
following:

-   The permission set of an execution thread is considered to be the
    intersection of the permissions of all protection domains traversed
    by the execution thread.
-   When a piece of code calls the
    <span class="apiname">doPrivileged</span> method (see below), the
    permission set of the execution thread is considered to include a
    permission if it is allowed by the said code\'s protection domain
    and by all protection domains that are called or entered directly or
    indirectly subsequently.

As you can see, the <span class="apiname">doPrivileged</span> method
enables a piece of trusted code to temporarily enable access to more
resources than are available directly to the application that called it.
This is necessary in some situations. For example, an application may
not be allowed direct access to files that contain fonts, but the system
utility to display a document must obtain those fonts, on behalf of the
user. We provide the <span class="apiname">doPrivileged</span> method
for the system domain to deal with this situation, and the method is in
fact available to all domains.

During execution, when access to a critical system resource (such as
file I/O and network I/O) is requested, the resource-handling code
directly or indirectly invokes a special
<span class="apiname">AccessController</span> class method that
evaluates the request and decides if the request should be granted or
denied.

Such an evaluation follows and generalizes the \"rule of thumb\" given
above. The actual way in which the evaluation is conducted can vary
between implementations. The basic principle is to examine the call
history and the permissions granted to the relevant protection domains,
and to return silently if the request is granted or throw a security
exception if the request is denied.

Finally, each domain (system or application) may also implement
additional protection of its internal resources within its own domain
boundary. For example, a banking application may need to support and
protect internal concepts such as checking accounts, deposits and
withdrawals. Because the semantics of such protection is unlikely to be
predictable or enforceable by the JDK, the protection system at this
level is best left to the system or application developers.
Nevertheless, whenever appropriate, we provide helpful primitives to
simplify developers\' tasks. One such primitive is the
<span class="apiname">SignedObject</span> class, whose detail we will
describe later.

</div>
</div>
<div class="sect2">
[]{#GUID-EDCA17D5-A2FD-472B-A156-32DD6AE87C42}

Permissions and Security Policy {#JSSEC-GUID-EDCA17D5-A2FD-472B-A156-32DD6AE87C42 .sect2}
-------------------------------

<div>
</div>
<div class="sect3">
[]{#GUID-DEA8EAB1-CF00-4658-AA6D-D2C9754C8B37}

### The Permission Classes {#JSSEC-GUID-DEA8EAB1-CF00-4658-AA6D-D2C9754C8B37 .sect3}

<div>
The permission classes represent access to system resources. The
<span class="apiname">java.security.Permission</span> class is an
abstract class and is subclassed, as appropriate, to represent specific
accesses.

As an example of a permission, the following code can be used to produce
a permission to read the file named `abc` in the `/tmp` directory:

``` {.oac_no_warn dir="ltr"}
    perm = new java.io.FilePermission("/tmp/abc", "read");
```

New permissions are subclassed either from the
<span class="apiname">Permission</span> class or one of its subclasses,
such as <span class="apiname">java.security.BasicPermission</span>.
Subclassed permissions (other than
<span class="apiname">BasicPermission</span>) generally belong to their
own packages. Thus, <span class="apiname">FilePermission</span> is found
in the <span class="apiname">java.io</span> package.

A crucial abstract method that needs to be implemented for each new
class of permission is the `implies`{.codeph} method. Basically, \"a
implies b\" means that if one is granted permission \"a\", one is
naturally granted permission \"b\". This is important when making access
control decisions.

Associated with the abstract class
<span class="apiname">java.security.Permission</span> are the abstract
class named
<span class="apiname">java.security.PermissionCollection</span> and the
final class <span class="apiname">java.security.Permissions</span>.

Class <span class="apiname">java.security.PermissionCollection</span>
represents a collection (i.e., a set that allows duplicates) of
<span class="apiname">Permission</span> objects for a single category
(such as file permissions), for ease of grouping. In cases where
permissions can be added to the
<span class="apiname">PermissionCollection</span> object in any order,
such as for file permissions, it is crucial that the
<span class="apiname">PermissionCollection</span> object ensure that the
correct semantics are followed when the `implies`{.codeph} function is
called.

Class <span class="apiname">java.security.Permissions</span> represents
a collection of collections of <span class="apiname">Permission</span>
objects, or in other words, a super collection of heterogeneous
permissions.

Applications are free to add new categories of permissions that the
system supports. How to add such application-specific permissions is
discussed later in this document.

Now we describe the syntax and semantics of all built-in permissions.

</div>
<div class="sect4">
[]{#GUID-1805A836-1DC0-4DBE-88CF-83BEAFD65C76}

#### java.security.Permission {#JSSEC-GUID-1805A836-1DC0-4DBE-88CF-83BEAFD65C76 .sect4}

<div>
This abstract class is the ancestor of all permissions. It defines the
essential functionalities required for all permissions.

Each permission instance is typically generated by passing one or more
string parameters to the constructor. In a common case with two
parameters, the first parameter is usually \"the name of the target\"
(such as the name of a file for which the permission is aimed), and the
second parameter is the action (such as \"read\" action on a file).
Generally, a set of actions can be specified together as a
comma-separated composite string.

</div>
</div>
<div class="sect4">
[]{#GUID-9EC8B31D-35F4-4414-AE50-64037057D62A}

#### java.security.PermissionCollection {#JSSEC-GUID-9EC8B31D-35F4-4414-AE50-64037057D62A .sect4}

<div>
This class holds a homogeneous collection of permissions. In other
words, each instance of the class holds only permissions of the same
type.

</div>
</div>
<div class="sect4">
[]{#GUID-F7F4DA3B-79E5-4306-88AC-791B64DCD350}

#### java.security.Permissions {#JSSEC-GUID-F7F4DA3B-79E5-4306-88AC-791B64DCD350 .sect4}

<div>
This class is designed to hold a heterogeneous collection of
permissions. Basically, it is a collection of
<span class="apiname">java.security.PermissionCollection</span> objects.

</div>
</div>
<div class="sect4">
[]{#GUID-05F504BC-6075-4CC2-A573-67F4B6AC96AC}

#### java.security.UnresolvedPermission {#JSSEC-GUID-05F504BC-6075-4CC2-A573-67F4B6AC96AC .sect4}

<div>
Recall that the internal state of a security policy is normally
expressed by the permission objects that are associated with each code
source. Given the dynamic nature of Java technology, however, it is
possible that when the policy is initialized the actual code that
implements a particular permission class has not yet been loaded and
defined in the Java application environment. For example, a referenced
permission class may be in a JAR file that will later be loaded.

The <span class="apiname">UnresolvedPermission</span> class is used to
hold such \"unresolved\" permissions. Similarly, the class
<span class="apiname">java.security.UnresolvedPermissionCollection</span>
stores a collection of <span class="apiname">UnresolvedPermission</span>
permissions.

During access control checking on a permission of a type that was
previously unresolved, but whose class has since been loaded, the
unresolved permission is \"resolved\" and the appropriate access control
decision is made. That is, a new object of the appropriate class type is
instantiated, if possible, based on the information in the
<span class="apiname">UnresolvedPermission</span>. This new object
replaces the <span class="apiname">UnresolvedPermission</span>, which is
removed. If the permission is still unresolvable at this time, the
permission is considered invalid, as if it is never granted in a
security policy.

</div>
</div>
<div class="sect4">
[]{#GUID-FDEB3FEC-9DA9-4524-8B3D-E3D559F5C504}

#### java.io.FilePermission {#JSSEC-GUID-FDEB3FEC-9DA9-4524-8B3D-E3D559F5C504 .sect4}

<div>
The targets for this class can be specified in the following ways, where
directory and file names are strings that cannot contain white spaces.

``` {.oac_no_warn dir="ltr"}
file
directory (same as directory/)
directory/file
directory/* (all files in this directory)
* (all files in the current directory)
directory/- (all files in the file system under this directory)
- (all files in the file system under the current directory)
"<<ALL FILES>>" (all files in the file system)
```

Note that `<<ALL FILES>>`{.codeph} is a special string denoting all
files in the system. On a Solaris, Linux, or macOS system, this includes
all files under the root directory. On a Windows system, this includes
all files on all drives.

The actions are: <span class="bold">read</span>,
<span class="bold">write</span>, <span class="bold">delete</span>, and
<span class="bold">execute</span>. Therefore, the following are valid
code samples for creating file permissions:

``` {.oac_no_warn dir="ltr"}
import java.io.FilePermission;

FilePermission p = new FilePermission("myfile", "read,write");
FilePermission p = new FilePermission("/home/gong/", "read");
FilePermission p = new FilePermission("/tmp/mytmp", "read,delete");
FilePermission p = new FilePermission("/bin/*", "execute");
FilePermission p = new FilePermission("*", "read");
FilePermission p = new FilePermission("/-", "read,execute");
FilePermission p = new FilePermission("-", "read,execute");
FilePermission p = new FilePermission("<<ALL FILES>>", "read");
```

The `implies`{.codeph} method in this class correctly interprets the
file system. For
example,` FilePermission("/-", "read,execute")`{.codeph} implies
`FilePermission("/home/gong/public_html/index.html", "read")`{.codeph},
and `FilePermission("bin/*", "execute")`{.codeph} implies
`FilePermission("bin/emacs19.31", "execute")`{.codeph}.

<div class="infoboxnote" id="GUID-FDEB3FEC-9DA9-4524-8B3D-E3D559F5C504__GUID-02987D36-8BCD-433E-8C57-303A464A5F62">
Note:

Most of these strings are given in platform-dependent format. For
example, to represent read access to the file named `foo` in the `temp`
directory on the `C` drive of a Windows system, you would use

``` {.oac_no_warn dir="ltr"}
FilePermission p = new FilePermission("c:\\temp\\foo", "read");
```

The double backslashes are necessary to represent a single backslash
because the strings are processed by a tokenizer
(<span class="apiname">java.io.StreamTokenizer</span>), which allows
`\`{.codeph} to be used as an escape string (e.g., `\n`{.codeph} to
indicate a new line) and which thus requires two backslashes to indicate
a single backslash. After the tokenizer has processed the above
<span class="apiname">FilePermission</span> target string, converting
double backslashes to single backslashes, the end result is the actual
path:

``` {.oac_no_warn dir="ltr"}
"c:\temp\foo"
```

It is necessary that the strings be given in platform-dependent format
until there is a universal file description language. Note also that the
use of meta symbols such as `*`{.codeph} and `-`{.codeph} prevents the
use of specific file names. We think this is a small limitation that can
be tolerated for the moment. Finally, note that `-/`{.codeph} and
`<<ALL FILES>>`{.codeph} are the same target on Solaris, Linux, and
macOS systems in that they both refer to the entire file system. (They
can refer to multiple file systems if they are all available). The two
targets are potentially different on other operating systems, such as
Windows and macOS.

Also note that a target name that specifies just a directory, with a
\"read\" action, as in

``` {.oac_no_warn dir="ltr"}
FilePermission p = new FilePermission("/home/gong/", "read");
```

means you are only giving permission to list the files in that
directory, not read any of them. To allow read access to files, you must
specify either an explicit file name, or an `*`{.codeph} or
`-`{.codeph}, as in

``` {.oac_no_warn dir="ltr"}
FilePermission p = new FilePermission("/home/gong/myfile", "read");
FilePermission p = new FilePermission("/home/gong/*", "read");
FilePermission p = new FilePermission("/home/gong/-", "read");
```

And finally, note that code always automatically has permission to read
files from its same (URL) location, and subdirectories of that location;
it does not need explicit permission to do so.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-1C00ACB3-88F6-4A8E-85D8-9AF7CB46D812}

#### java.net.SocketPermission {#JSSEC-GUID-1C00ACB3-88F6-4A8E-85D8-9AF7CB46D812 .sect4}

<div>
This class represents access to a network via sockets. The target for
this class can be given as `hostname:port_range`{.codeph}, where
`hostname`{.codeph} can be given in the following ways:

``` {.oac_no_warn dir="ltr"}
hostname (a single host)
IP address (a single host)
localhost (the local machine)
"" (equivalent to "localhost")
hostname.domain (a single host within the domain)
hostname.subdomain.domain
*.domain (all hosts in the domain)
*.subdomain.domain
* (all hosts)
```

That is, the host is expressed as a DNS name, as a numerical IP address,
as `"localhost"`{.codeph} (for the local machine) or as `""`{.codeph}
(which is equivalent to specifying `"localhost"`{.codeph}).

The wildcard `*`{.codeph} may be included once in a DNS name host
specification. If it is included, it must be in the leftmost position,
as in `*.sun.com`{.codeph}.

The `port_range`{.codeph} can be given as follows:

``` {.oac_no_warn dir="ltr"}
N (a single port)
N- (all ports numbered N and above)
-N (all ports numbered N and below)
N1-N2 (all ports between N1 and N2, inclusive)
```

Here `N`{.codeph}, `N1`{.codeph}, and `N2`{.codeph} are non-negative
integers ranging from 0 to 65535 (2^16-1^).

The actions on sockets are <span class="bold">accept</span>,
<span class="bold">connect</span>, <span class="bold">listen</span>, and
<span class="bold">resolve</span> (which is basically DNS lookup). Note
that implicitly, the action \"resolve\" is implied by \"accept\",
\"connect\", and \"listen\" -- i.e., those who can listen or accept
incoming connections from or initiate out-going connections to a host
should be able to look up the name of the remote host.

Below are some examples of socket permissions.

``` {.oac_no_warn dir="ltr"}
import java.net.SocketPermission;

SocketPermission p = new SocketPermission("java.example.com","accept");
p = new SocketPermission("192.0.2.99","accept");
p = new SocketPermission("*.com","connect");
p = new SocketPermission("*.example.com:80","accept");
p = new SocketPermission("*.example.com:-1023","accept");
p = new SocketPermission("*.example.com:1024-","connect");
p = new SocketPermission("java.example.com:8000-9000",
         "connect,accept");
p = new SocketPermission("localhost:1024-",
          "accept,connect,listen");
```

<div class="infoboxnote" id="GUID-1C00ACB3-88F6-4A8E-85D8-9AF7CB46D812__GUID-1CEB4B30-5722-4A7A-9E99-BDF281AA9CD9">
Note:

`SocketPermission("java.example.com:80,8080","accept")`{.codeph} and
`SocketPermission("java.example.com,javasun.example.com","accept"`{.codeph})
are not valid socket permissions.

Moreover, because <span class="bold">listen</span> is an action that
applies only to ports on the local host, whereas
<span class="bold">accept</span> is an action that applies to ports on
both the local and remote host, both actions are necessary.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-BCC9A9CD-AB9C-42C5-9294-E0A593770F4C}

#### java.security.BasicPermission {#JSSEC-GUID-BCC9A9CD-AB9C-42C5-9294-E0A593770F4C .sect4}

<div>
The <span class="apiname">BasicPermission</span> class extends the
<span class="apiname">Permission</span> class. It can be used as the
base class for permissions that want to follow the same naming
convention as <span class="apiname">BasicPermission</span> (see below).

The name for a <span class="apiname">BasicPermission</span> is the name
of the given permission (for example, \"exitVM\", \"setFactory\",
\"queuePrintJob\", etc). The naming convention follows the hierarchical
property naming convention. An asterisk may appear at the end of the
name, following a \".\", or by itself, to signify a wildcard match. For
example: \"java.\*\" or \"\*\" is valid, \"\*java\" or \"a\*b\" is not
valid.

The action string (inherited from
<span class="apiname">Permission</span>) is unused. Thus,
<span class="apiname">BasicPermission</span> is commonly used as the
base class for \"named\" permissions (ones that contain a name but no
actions list; you either have the named permission or you don\'t.)
Subclasses may implement actions on top of
<span class="apiname">BasicPermission</span>, if desired.

Some of the <span class="apiname">BasicPermission</span> subclasses are
<span class="apiname">java.lang.RuntimePermission</span>,
<span class="apiname">java.security.SecurityPermission</span>,
<span class="apiname">java.util.PropertyPermission</span>, and
<span class="apiname">java.net.NetPermission</span>.

</div>
</div>
<div class="sect4">
[]{#GUID-D10A4043-110B-4E92-BAC0-4654E20E01D0}

#### java.util.PropertyPermission {#JSSEC-GUID-D10A4043-110B-4E92-BAC0-4654E20E01D0 .sect4}

<div>
The targets for this class are basically the names of Java properties as
set in various property files. Examples are the `java.home`{.codeph} and
`os.name`{.codeph} properties. Targets can be specified as \"\*\" (any
property), \"a.\*\" (any property whose name has a prefix \"a.\"),
\"a.b.\*\", and so on. Note that the wildcard can occur only once and
can only be at the rightmost position.

This is one of the <span class="apiname">BasicPermission</span>
subclasses that implements actions on top of
<span class="apiname">BasicPermission</span>. The actions are read and
write. Their meaning is defined as follows: \"read\" permission allows
the `getProperty`{.codeph} method in
<span class="apiname">java.lang.System</span> to be called to get the
property value, and \"write\" permission allows the
`setProperty`{.codeph} method to be called to set the property value.

</div>
</div>
<div class="sect4">
[]{#GUID-744ACFDF-6ED1-473D-9D3A-5F34541A4377}

#### java.lang.RuntimePermission {#JSSEC-GUID-744ACFDF-6ED1-473D-9D3A-5F34541A4377 .sect4}

<div>
The target for a <span class="apiname">RuntimePermission</span> can be
represented by any string, and there is no action associated with the
targets. For example, `RuntimePermission("exitVM")`{.codeph} denotes the
permission to exit the Java Virtual Machine.

The target names are:

``` {.oac_no_warn dir="ltr"}
createClassLoader
getClassLoader
setContextClassLoader
setSecurityManager
createSecurityManager
exitVM
setFactory
setIO
modifyThread
stopThread
modifyThreadGroup
getProtectionDomain
readFileDescriptor
writeFileDescriptor
loadLibrary.{library name}
accessClassInPackage.{package name}
defineClassInPackage.{package name}
accessDeclaredMembers.{class name}
queuePrintJob
```

</div>
</div>
<div class="sect4">
[]{#GUID-D5BF900D-436B-4DB0-A855-FBAAF20D89FA}

#### java.awt.AWTPermission {#JSSEC-GUID-D5BF900D-436B-4DB0-A855-FBAAF20D89FA .sect4}

<div>
This is in the same spirit as the
<span class="apiname">RuntimePermission</span>; it\'s a permission
without actions. The targets for this class are:

``` {.oac_no_warn dir="ltr"}
accessClipboard
accessEventQueue
listenToAllAWTEvents
showWindowWithoutWarningBanner
```

</div>
</div>
<div class="sect4">
[]{#GUID-0DBB6926-DA1E-491F-8E23-D0712AC13CCB}

#### java.net.NetPermission {#JSSEC-GUID-0DBB6926-DA1E-491F-8E23-D0712AC13CCB .sect4}

<div>
This class contains the following targets and no actions:

``` {.oac_no_warn dir="ltr"}
requestPasswordAuthentication
setDefaultAuthenticator
specifyStreamHandler
```

</div>
</div>
<div class="sect4">
[]{#GUID-B5B444DD-0DED-4023-A0CB-BE2988CBA2DB}

#### java.lang.reflect.ReflectPermission {#JSSEC-GUID-B5B444DD-0DED-4023-A0CB-BE2988CBA2DB .sect4}

<div>
This is the <span class="apiname">Permission</span> class for reflective
operations. A <span class="apiname">ReflectPermission</span> is a named
permission (like <span class="apiname">RuntimePermission</span>) and has
no actions. The only name currently defined is
`suppressAccessChecks`{.codeph}, which allows suppressing the standard
Java programming language access checks -- for public, default (package)
access, protected, and private members -- performed by reflected objects
at their point of use.

</div>
</div>
<div class="sect4">
[]{#GUID-372E6279-A298-4399-BD86-CF094FCD7FC3}

#### java.io.SerializablePermission {#JSSEC-GUID-372E6279-A298-4399-BD86-CF094FCD7FC3 .sect4}

<div>
This class contains the following targets and no actions:

``` {.oac_no_warn dir="ltr"}
enableSubclassImplementation
enableSubstitution
```

</div>
</div>
<div class="sect4">
[]{#GUID-5F524238-B23D-4A58-8733-330EE6946AC4}

#### java.security.SecurityPermission {#JSSEC-GUID-5F524238-B23D-4A58-8733-330EE6946AC4 .sect4}

<div>
<span class="apiname">SecurityPermissions</span> control access to
security-related objects, such as <span class="apiname">Security</span>,
<span class="apiname">Policy</span>,
<span class="apiname">Provider</span>,
<span class="apiname">Signer</span>, and
<span class="apiname">Identity</span> objects. This class contains the
following targets and no actions:

``` {.oac_no_warn dir="ltr"}
getPolicy
setPolicy
getProperty.{key}
setProperty.{key}
insertProvider.{provider name}
removeProvider.{provider name}
setSystemScope
setIdentityPublicKey
setIdentityInfo
printIdentity
addIdentityCertificate
removeIdentityCertificate
clearProviderProperties.{provider name}
putProviderProperty.{provider name}
removeProviderProperty.{provider name}
getSignerPrivateKey
setSignerKeyPair
```

</div>
</div>
<div class="sect4">
[]{#GUID-51FC4F94-2A29-4B3A-88CB-7AF4C9A5BA59}

#### java.security.AllPermission {#JSSEC-GUID-51FC4F94-2A29-4B3A-88CB-7AF4C9A5BA59 .sect4}

<div>
This permission implies all permissions. It is introduced to simplify
the work of system administrators who might need to perform multiple
tasks that require all (or numerous) permissions. It would be
inconvenient to require the security policy to iterate through all
permissions. Note that <span class="apiname">AllPermission</span> also
implies new permissions that are defined in the future.

Clearly, much caution is necessary when considering granting this
permission.

</div>
</div>
<div class="sect4">
[]{#GUID-07D4DF51-7CFB-4DDA-BFC8-DF3B06BC5011}

#### javax.security.auth.AuthPermission {#JSSEC-GUID-07D4DF51-7CFB-4DDA-BFC8-DF3B06BC5011 .sect4}

<div>
<span class="apiname">AuthPermission</span> handles authentication
permissions and authentication-related object such as
<span class="apiname">Subject</span>,
<span class="apiname">SubjectDomainCombiner</span>,
<span class="apiname">LoginContext</span>, and
<span class="apiname">Configuration</span>. This class contains the
following targets and no actions:

``` {.oac_no_warn dir="ltr"}
doAs
doAsPrivileged
getSubject
getSubjectFromDomainCombiner
setReadOnly
modifyPrincipals
modifyPublicCredentials
modifyPrivateCredentials
refreshCredential
destroyCredential
createLoginContext.{name}
getLoginConfiguration
setLoginConfiguration
refreshLoginConfiguration
```

</div>
</div>
<div class="sect4">
[]{#GUID-693DDD12-F742-4C65-8578-04B4F4CB26A1}

#### Discussion of Permission Implications {#JSSEC-GUID-693DDD12-F742-4C65-8578-04B4F4CB26A1 .sect4}

<div>
Recall that permissions are often compared against each other, and to
facilitate such comparisons, we require that each permission class
defines an `implies`{.codeph} method that represents how the particular
permission class relates to other permission classes. For example,
`java.io.FilePermission("/tmp/*", "read")`{.codeph} implies
`java.io.FilePermission("/tmp/a.txt", "read")`{.codeph} but does not
imply any <span class="apiname">java.net.NetPermission</span>.

There is another layer of implication that may not be immediately
obvious to some readers. Suppose that one applet has been granted the
permission to write to the entire file system. This presumably allows
the applet to replace the system binary, including the JVM runtime
environment. This effectively means that the applet has been granted all
permissions.

Another example is that if an applet is granted the runtime permission
to create class loaders, it is effectively granted many more
permissions, as a class loader can perform sensitive operations.

Other permissions that are \"dangerous\" to give out include those that
allow the setting of system properties, runtime permissions for defining
packages and for loading native code libraries (because the Java
security architecture is not designed to and does not prevent malicious
behavior at the level of native code), and of course the
<span class="apiname">AllPermission</span>.

For more information about permissions, including tables enumerating the
risks of assigning specific permissions as well as a table of all the
JDK built-in methods that require permissions, see [Permissions in the
JDK](permissions-jdk1.html#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95 "A permission represents access to a system resource. In order for a resource access to be allowed for an applet (or an application running with a security manager), the corresponding permission must be explicitly granted to the code attempting the access.").

</div>
</div>
<div class="sect4">
[]{#GUID-F9498F7F-365E-46D5-8B39-2FDCEB7D9E8C}

#### How To Create New Types of Permissions {#JSSEC-GUID-F9498F7F-365E-46D5-8B39-2FDCEB7D9E8C .sect4}

<div>
It is essential that no one except Oracle should extend the permissions
that are built into the JDK, either by adding new functionality or by
introducing additional target keywords into a class such as
<span class="apiname">java.lang.RuntimePermission</span>. This maintains
consistency.

To create a new permission, the following steps are recommended, as
shown by an example. Suppose an application developer from company ABC
wants to create a customized permission to \"watch TV\".

First, create a new class `com.abc.Permission`{.codeph} that extends the
abstract class <span class="apiname">java.security.Permission</span> (or
one of its subclasses), and another new class
`com.abc.TVPermission`{.codeph} that extends the
<span class="apiname">com.abc.Permission</span>. Make sure that the
`implies`{.codeph} method, among others, is correctly implemented. (Of
course, `com.abc.TVPermission`{.codeph} can directly extend
<span class="apiname">java.security.Permission</span>; the intermediate
`com.abc.Permission`{.codeph} is not required.)

``` {.oac_no_warn dir="ltr"}
public class com.abc.Permission extends java.security.Permission

public class com.abc.TVPermission extends com.abc.Permission
```

The following figure shows the subclass relationship.

<span>![Description of jssec\_dt\_031\_anc8.eps
follows](img/jssec_dt_031_anc8.png "Description of jssec_dt_031_anc8.eps follows")\
[Description of the illustration
jssec\_dt\_031\_anc8.eps](img_text/jssec_dt_031_anc8.htm)</span>

Second, include these new classes with the application package.

Each user that wants to allow this new type of permission for specific
code does so by adding an entry in a policy file. (Details of the policy
file syntax are given in a later section.) An example of a policy file
entry granting code from `http://example.com/`{.codeph} permission to
watch channel 5 would be:

``` {.oac_no_warn dir="ltr"}
grant codeBase  "http://example.com/" {
    permission com.abc.TVPermission "channel-5", "watch";
}
```

In the application\'s resource management code, when checking to see if
a permission should be granted, call
<span class="apiname">AccessController</span>\'s
`checkPermission`{.codeph} method using a
`com.abc.TVPermission`{.codeph} object as the parameter.

``` {.oac_no_warn dir="ltr"}
   com.abc.TVPermission tvperm = new
        com.abc.TVPermission("channel-5", "watch");
   AccessController.checkPermission(tvperm);
```

Note that, when adding a new permission, one should create a new
(permission) class and not add a new method to the security manager. (In
the past, in order to enable checking of a new type of access, you had
to add a new method to the <span class="apiname">SecurityManager</span>
class.)

If more elaborate `TVPermissions`{.codeph} such as \"channel-1:13\" or
\"channel-\*\" are allowed, then it may be necessary to implement a
`TVPermissionCollection`{.codeph} object that knows how to deal with the
semantics of these pseudo names.

New code should always invoke a permission check by calling the
`checkPermission`{.codeph} method of the
<span class="apiname">AccessController</span> class in order to exercise
the built-in access control algorithm. There is no essential need to
examine whether there is a <span class="apiname">ClassLoader</span> or a
<span class="apiname">SecurityManager</span>. On the other hand, if the
algorithm should be left to the installed security manager class, then
the method `SecurityManager.checkPermission`{.codeph} should be invoked
instead.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-B1EE1A73-CF14-40CB-A524-F76600BC9DF0}

### java.security.CodeSource {#JSSEC-GUID-B1EE1A73-CF14-40CB-A524-F76600BC9DF0 .sect3}

<div>
This class extends the concept of a codebase within HTML to encapsulate
not only the code location (URL) but also the certificate(s) containing
public keys that should be used to verify signed code originating from
that location. Note that this is not the equivalent of the
`CodeBase`{.codeph} tag in HTML files. Each certificate is represented
as a <span class="apiname">java.security.cert.Certificate</span>, and
each URL as a <span class="apiname">java.net.URL</span>.

</div>
</div>
<div class="sect3">
[]{#GUID-93B94FD3-599F-4C9F-9479-7EDC34B05D65}

### java.security.Policy {#JSSEC-GUID-93B94FD3-599F-4C9F-9479-7EDC34B05D65 .sect3}

<div>
The system security policy for a Java application environment,
specifying which permissions are available for code from various
sources, is represented by a <span class="apiname">Policy</span> object.
More specifically, it is represented by a
<span class="apiname">Policy</span> subclass providing an implementation
of the abstract methods in the <span class="apiname">Policy</span>
class.

In order for an applet (or an application running under a
<span class="apiname">SecurityManager</span>) to be allowed to perform
secured actions, such as reading or writing a file, the applet (or
application) must be granted permission for that particular action. The
only exception is that code always automatically has permission to read
files from its same <span class="apiname">CodeSource</span>, and
subdirectories of that <span class="apiname">CodeSource</span>; it does
not need explicit permission to do so.

There could be multiple instances of the
<span class="apiname">Policy</span> object, although only one is \"in
effect\" at any time. The currently-installed
<span class="apiname">Policy</span> object can be obtained by calling
the `getPolicy`{.codeph} method, and it can be changed by a call to the
`setPolicy`{.codeph} method (by code with permission to reset the
Policy).

The source location for the policy information utilized by the
<span class="apiname">Policy</span> object is up to the Policy
implementation. The policy configuration may be stored, for example, as
a flat ASCII file, as a serialized binary file of the
<span class="apiname">Policy</span> class, or as a database. There is a
<span class="apiname">Policy</span> reference implementation that
obtains its information from static policy configuration files.

</div>
<div class="sect4">
[]{#GUID-F5270083-CCAC-49E0-ACAC-50176FBFDD97}

#### Policy File Format {#JSSEC-GUID-F5270083-CCAC-49E0-ACAC-50176FBFDD97 .sect4}

<div>
In the Policy reference implementation, the policy can be specified
within one or more policy configuration files. The configuration files
indicate what permissions are allowed for code from specified code
sources. Each configuration file must be encoded in UTF-8.

A policy configuration file essentially contains a list of entries. It
may contain a keystore entry, and contains zero or more grant entries.

A keystore is a database of private keys and their associated digital
certificates such as X.509 certificate chains authenticating the
corresponding public keys. The `keytool`{.codeph} utility is used to
create and administer keystores. The keystore specified in a policy
configuration file is used to look up the public keys of the signers
specified in the grant entries of the file. A keystore entry must appear
in a policy configuration file if any grant entries specify signer
aliases, or if any grant entries specify a principal alias (see below).

At this time, there can be only one keystore entry in the policy file
(others after the first one are ignored), and it can appear anywhere
outside the file\'s grant entries . It has the following syntax:

``` {.oac_no_warn dir="ltr"}
keystore "some_keystore_url", "keystore_type";
```

Here, `some_keystore_url`{.codeph} specifies the URL location of the
keystore, and `keystore_type`{.codeph} specifies the keystore type. The
latter is optional. If not specified, the type is assumed to be that
specified by the `keystore.type`{.codeph} property in the security
properties file.

The URL is relative to the policy file location. Thus if the policy file
is specified in the security properties file as:

``` {.oac_no_warn dir="ltr"}
policy.url.1=http://foo.bar.example.com/blah/some.policy
```

and that policy file has an entry:

``` {.oac_no_warn dir="ltr"}
keystore ".keystore";
```

then the keystore will be loaded from:

``` {.oac_no_warn dir="ltr"}
http://foo.bar.example.com/blah/.keystore
```

The URL can also be absolute.

A keystore type defines the storage and data format of the keystore
information, and the algorithms used to protect private keys in the
keystore and the integrity of the keystore itself. The Oracle JDK\'s
default keystore type is PKCS12.

Each grant entry in a policy file essentially consists of a
<span class="apiname">CodeSource</span> and its permissions. Actually, a
<span class="apiname">CodeSource</span> consists of a URL and a set of
certificates, while a policy file entry includes a URL and a list of
signer names. The system creates the corresponding
<span class="apiname">CodeSource</span> after consulting the keystore to
determine the certificate(s) of the specified signers.

Each grant entry in the policy file is of the following format, where
the leading `grant`{.codeph} is a reserved word that signifies the
beginning of a new entry and optional items appear in brackets. Within
each entry, a leading `permission`{.codeph} is another reserved word
that marks the beginning of a new permission in the entry. Each grant
entry grants a set of permissions to a specified code source and
principals.

``` {.oac_no_warn dir="ltr"}
grant [SignedBy "signer_names"] [, CodeBase "URL"]
      [, Principal [principal_class_name] "principal_name"]
      [, Principal [principal_class_name] "principal_name"] ... {
    permission permission_class_name [ "target_name" ] 
               [, "action"] [, SignedBy "signer_names"];
    permission ...
};
```

White spaces are allowed immediately before or after any comma. The name
of the permission class must be a fully qualified class name, such as
<span class="apiname">java.io.FilePermission</span>, and cannot be
abbreviated (for example, to
<span class="apiname">FilePermission</span>).

Note that the action field is optional in that it can be omitted if the
permission class does not require it. If it is present, then it must
come immediately after the target field.

The exact meaning of a CodeBase URL value depends on the characters at
the end. A CodeBase with a trailing \"/\" matches all class files (not
JAR files) in the specified directory. A CodeBase with a trailing
\"/\*\" matches all files (both class and JAR files) contained in that
directory. A CodeBase with a trailing \"/-\" matches all files (both
class and JAR files) in the directory and recursively all files in
subdirectories contained in that directory.

The CodeBase field (URL) is optional in that, if it is omitted, it
signifies \"any code base\".

The first signer name field is a string alias that is mapped, via a
separate mechanism, to a set of public keys (within certificates in the
keystore) that are associated with the signers. These keys are used to
verify that certain signed classes are really signed by these signers.

This signer field can be a comma-separated string containing names of
multiple signers, an example of which is `Adam,Eve,Charles`{.codeph},
which means signed by Adam and Eve and Charles (i.e., the relationship
is AND, not OR).

This field is optional in that, if it is omitted, it signifies \"any
signer\", or in other words, \"It doesn\'t matter whether the code is
signed or not\".

The second signer field, inside a permission entry, represents the alias
to the keystore entry containing the public key corresponding to the
private key used to sign the bytecodes that implemented the said
permission class. This permission entry is effective (i.e., access
control permission will be granted based on this entry) only if the
bytecode implementation is verified to be correctly signed by the said
alias.

A principal value specifies a class\_name/principal\_name pair which
must be present within the executing threads principal set. The
principal set is associated with the executing code by way of a Subject.
The principal field is optional in that, if it is omitted, it signifies
\"any principals\".

<div class="infoboxnote" id="GUID-F5270083-CCAC-49E0-ACAC-50176FBFDD97__GUID-0BB07966-22BF-44C7-9200-21C4B1700432">
Note:

Regarding keystore alias replacement: If the principal
class\_name/principal\_name pair is specified as a single quoted string,
it is treated as a keystore alias. The keystore is consulted and queried
(via the alias) for an X509 Certificate. If one is found, the
principal\_class is automatically treated as
<span class="apiname">javax.security.auth.x500.X500Principal</span>, and
the principal\_name is automatically treated as the subject
distinguished name from the certificate. If an X509 Certificate mapping
is not found, the entire grant entry is ignored.

</div>
The order between the CodeBase, SignedBy, and Principal fields does not
matter.

An informal BNF grammar for the policy file format is given below, where
non-capitalized terms are terminals:

``` {.oac_no_warn dir="ltr"}
PolicyFile -> PolicyEntry | PolicyEntry; PolicyFile
PolicyEntry -> grant {PermissionEntry}; |
           grant SignerEntry {PermissionEntry} |
           grant CodebaseEntry {PermissionEntry} |
           grant PrincipalEntry {PermissionEntry} |
           grant SignerEntry, CodebaseEntry {PermissionEntry} |
           grant CodebaseEntry, SignerEntry {PermissionEntry} |
           grant SignerEntry, PrincipalEntry {PermissionEntry} |
           grant PrincipalEntry, SignerEntry {PermissionEntry} |
           grant CodebaseEntry, PrincipalEntry {PermissionEntry} |
           grant PrincipalEntry, CodebaseEntry {PermissionEntry} |
           grant SignerEntry, CodebaseEntry, PrincipalEntry {PermissionEntry} |
           grant CodebaseEntry, SignerEntry, PrincipalEntry {PermissionEntry} |
           grant SignerEntry, PrincipalEntry, CodebaseEntry {PermissionEntry} |
           grant CodebaseEntry, PrincipalEntry, SignerEntry {PermissionEntry} |
           grant PrincipalEntry, CodebaseEntry, SignerEntry {PermissionEntry} |
           grant PrincipalEntry, SignerEntry, CodebaseEntry {PermissionEntry} |
           keystore "url"
SignerEntry -> signedby (a comma-separated list of strings)
CodebaseEntry -> codebase (a string representation of a URL)
PrincipalEntry -> OnePrincipal | OnePrincipal, PrincipalEntry
OnePrincipal -> principal [ principal_class_name ] "principal_name" (a principal)
PermissionEntry -> OnePermission | OnePermission PermissionEntry
OnePermission -> permission permission_class_name
                 [ "target_name" ] [, "action_list"]
                 [, SignerEntry];
```

Now we give some examples. The following policy grants permission
`a.b.Foo`{.codeph} to code signed by `Roland`{.codeph}:

``` {.oac_no_warn dir="ltr"}
grant signedBy "Roland" {
    permission a.b.Foo;
};
```

The following grants a <span class="apiname">FilePermission</span> to
all code (regardless of the signer and/or CodeBase):

``` {.oac_no_warn dir="ltr"}
grant {
   permission java.io.FilePermission ".tmp", "read";
};
```

The following grants two permissions to code that is signed by both
`Li`{.codeph} and `Roland`{.codeph}:

``` {.oac_no_warn dir="ltr"}
grant signedBy "Roland,Li" {
  permission java.io.FilePermission "/tmp/*", "read";
  permission java.util.PropertyPermission "user.*";
};
```

The following grants two permissions to code that is signed by
`Li`{.codeph} and that comes from `http://example.com`{.codeph}:

``` {.oac_no_warn dir="ltr"}
grant codeBase "http://example.com/*", signedBy "Li" {
    permission java.io.FilePermission "/tmp/*", "read";
    permission java.io.SocketPermission "*", "connect";
};
```

The following grants two permissions to code that is signed by both
`Li`{.codeph} and `Roland`{.codeph}, and only if the bytecodes
implementing `com.abc.TVPermission`{.codeph} are genuinely signed by
`Li`{.codeph}.

``` {.oac_no_warn dir="ltr"}
grant signedBy "Roland,Li" {
  permission java.io.FilePermission "/tmp/*", "read";
  permission com.abc.TVPermission "channel-5", "watch", 
     signedBy "Li";
};
```

The reason for including the second signer field is to prevent spoofing
when a permission class does not reside with the Java runtime
installation. For example, a copy of the `com.abc.TVPermission`{.codeph}
class can be downloaded as part of a remote JAR archive, and the user
policy might include an entry that refers to it. Because the archive is
not long-lived, the second time the `com.abc.TVPermission`{.codeph}
class is downloaded, possibly from a different web site, it is crucial
that the second copy is authentic, as the presence of the permission
entry in the user policy might reflect the user\'s confidence or belief
in the first copy of the class bytecode.

The reason we chose to use digital signatures to ensure authenticity,
rather than storing (a hash value of) the first copy of the bytecodes
and using it to compare with the second copy, is because the author of
the permission class can legitimately update the class file to reflect a
new design or implementation.

<div class="infoboxnote" id="GUID-F5270083-CCAC-49E0-ACAC-50176FBFDD97__GUID-141DB287-56F2-4917-B75B-5EF9E37B19EE">
Note:

The strings for a file path must be specified in a platform-dependent
format; this is necessary until there is a universal file description
language. The above examples have shown strings appropriate on Solaris.
On Windows, when you directly specify a file path in a string, you need
to include two backslashes for each actual single backslash in the path,
as in

``` {.oac_no_warn dir="ltr"}
grant signedBy "Roland" {
  permission java.io.FilePermission "C:\\users\\Cathy\\*", "read";
};
```

This is because the strings are processed by a tokenizer
(<span class="apiname">java.io.StreamTokenizer</span>), which allows
\"\\\" to be used as an escape string (e.g., \"\\n\" to indicate a new
line) and which thus requires two backslashes to indicate a single
backslash. After the tokenizer has processed the above
<span class="apiname">FilePermission</span> target string, converting
double backslashes to single backslashes, the end result is the actual
path:

``` {.oac_no_warn dir="ltr"}
"C:\users\Cathy\*"
```

</div>
Finally, here are some principal-based grant entries:

``` {.oac_no_warn dir="ltr"}
grant principal javax.security.auth.x500.X500Principal "cn=Alice" {
  permission java.io.FilePermission "/home/Alice", "read, write";
};
```

This permits any code executing as the
<span class="apiname">X500Principal</span>, `cn=Alice`{.codeph},
permission to read and write to `/home/Alice`.

The following example shows a grant statement with both codesource and
principal information.

``` {.oac_no_warn dir="ltr"}
  grant codebase "http://www.games.example.com",
        signedBy "Duke",
        principal javax.security.auth.x500.X500Principal "cn=Alice" {
    permission java.io.FilePermission "/tmp/games", "read, write";
  };
```

This allows code downloaded from `www.games.example.com`{.codeph},
signed by `Duke`{.codeph}, and executed by `cn=Alice`{.codeph},
permission to read and write into the `/tmp/games` directory.

he following example shows a grant statement with KeyStore alias
replacement:

``` {.oac_no_warn dir="ltr"}
  keystore "http://foo.bar.example.com/blah/.keystore";

  grant principal "alice" {
    permission java.io.FilePermission "/tmp/games", "read, write";
  };
```

`alice`{.codeph} will be replaced by
<span class="apiname">javax.security.auth.x500.X500Principal</span>
`cn=Alice`{.codeph} assuming the X.509 certificate associated with the
keystore alias, <span class="italic">alice</span>, has a subject
distinguished name of `cn=Alice`{.codeph}. This allows code executed by
the <span class="apiname">X500Principal</span> `cn=Alice`{.codeph}
permission to read and write into the `/tmp/games` directory.

</div>
</div>
<div class="sect4">
[]{#GUID-D21747DB-EA50-420E-9D8F-C72F34F5FCA5}

#### Property Expansion in Policy Files {#JSSEC-GUID-D21747DB-EA50-420E-9D8F-C72F34F5FCA5 .sect4}

<div>
Property expansion is possible in policy files and in the security
properties file. Property expansion is similar to expanding variables in
a shell. That is, when a string like `${some.property}`{.codeph} appears
in a policy file, or in the security properties file, it will be
expanded to the value of the specified system property. For example,

``` {.oac_no_warn dir="ltr"}
permission java.io.FilePermission "${user.home}", "read";
```

will expand `${user.home}`{.codeph} to use the value of the
`user.home`{.codeph} system property. If that property\'s value is
`/home/cathy`, then the above is equivalent to

``` {.oac_no_warn dir="ltr"}
permission java.io.FilePermission "/home/cathy", "read";
```

In order to assist in platform-independent policy files, you can also
use the special notation of `${/}`{.codeph}, which is a shortcut for
`${file.separator}`{.codeph}. This allows permission designations such
as

``` {.oac_no_warn dir="ltr"}
permission java.io.FilePermission "${user.home}${/}*", "read";
```

If `user.home`{.codeph} is `/home/cathy`, and you are on Solaris, the
above gets converted to:

``` {.oac_no_warn dir="ltr"}
permission java.io.FilePermission "/home/cathy/*", "read";
```

If on the other hand `user.home`{.codeph} is `C:\users\cathy` and you
are on a Windows system, the above gets converted to:

``` {.oac_no_warn dir="ltr"}
permission java.io.FilePermission "C:\users\cathy\*", "read";
```

Also, as a special case, if you expand a property in a codebase, such as

``` {.oac_no_warn dir="ltr"}
grant codeBase "file:/${java.home}/lib/ext/"
```

then any `file.separator`{.codeph} characters will be automatically
converted to slashes (`/`{.codeph}), which is desirable since codebases
are URLs. Thus on a Windows system, even if `java.home`{.codeph} is set
to `C:\j2sdk1.2`, the above would get converted to

``` {.oac_no_warn dir="ltr"}
grant codeBase "file:/C:/j2sdk1.2/lib/ext/"
```

Thus you don\'t need to use `${/}`{.codeph} in codebase strings (and you
shouldn\'t).

Property expansion takes place anywhere a double quoted string is
allowed in the policy file. This includes the `signedby`{.codeph},
`codebase`{.codeph}, target names, and action fields.

Whether or not property expansion is allowed is controlled by the value
of the `policy.expandProperties`{.codeph} property in the Security
Properties file. If the value of this Security Property is true (the
default), expansion is allowed.

Please note: You can\'t use nested properties; they will not work. For
example,

``` {.oac_no_warn dir="ltr"}
"${user.${foo}}"
```

doesn\'t work, even if the `foo`{.codeph} property is set to
`home`{.codeph}. The reason is the property parser doesn\'t recognize
nested properties; it simply looks for the first `${`{.codeph}, and then
keeps looking until it finds the first `}`{.codeph} and tries to
interpret the result `${user.$foo}`{.codeph} as a property, but fails if
there is no such property.

Also note: If a property can\'t be expanded in a grant entry, permission
entry, or keystore entry, that entry is ignored. For example, if the
system property `foo`{.codeph} is not defined and you have:

``` {.oac_no_warn dir="ltr"}
grant codeBase "${foo}" {
  permission ...;
  permission ...;
};
```

then all the permissions in this grant entry are ignored. If you have

``` {.oac_no_warn dir="ltr"}
grant {
  permission Foo "${foo}";
  permission Bar;
};
```

then only the `permission Foo "${foo}";`{.codeph} entry is ignored. And
finally, if you have

``` {.oac_no_warn dir="ltr"}
keystore "${foo}";
```

then the keystore entry is ignored.

One final note: On Windows systems, when you directly specify a file
path in a string, you need to include two backslashes for each actual
single backslash in the path, as in

``` {.oac_no_warn dir="ltr"}
"C:\\users\\cathy\\foo.bat"
```

This is because the strings are processed by a tokenizer
(<span class="apiname">java.io.StreamTokenizer</span>), which allows the
backslash (`\`{.codeph}) to be used as an escape string (e.g.,
`\n`{.codeph} to indicate a new line) and which thus requires two
backslashes to indicate a single backslash. After the tokenizer has
processed the above string, converting double backslashes to single
backslashes, the end result is

``` {.oac_no_warn dir="ltr"}
"C:\users\cathy\foo.bat"
```

Expansion of a property in a string takes place
<span class="bold">after</span> the tokenizer has processed the string.
Thus if you have the string

``` {.oac_no_warn dir="ltr"}
"${user.home}\\foo.bat"
```

then first the tokenizer processes the string, converting the double
backslashes to a single backslash, and the result is

``` {.oac_no_warn dir="ltr"}
"${user.home}\foo.bat"
```

Then the `${user.home}`{.codeph} property is expanded and the end result
is

``` {.oac_no_warn dir="ltr"}
"C:\users\cathy\foo.bat"
```

assuming the `user.home`{.codeph} value is `C:\users\cathy`. Of course,
for platform independence, it would be better if the string was
initially specified without any explicit slashes, i.e., using the
`${/}`{.codeph} property instead, as in

``` {.oac_no_warn dir="ltr"}
"${user.home}${/}foo.bat"
```

</div>
</div>
<div class="sect4">
[]{#GUID-17F2CE51-A2C7-48DF-98B9-3C7F4970A084}

#### General Expansion in Policy Files {#JSSEC-GUID-17F2CE51-A2C7-48DF-98B9-3C7F4970A084 .sect4}

<div>
Generalized forms of expansion are also supported in policy files. For
example, permission names may contain a string of the form:
`${{protocol:protocol_data}}`{.codeph} If such a string occurs in a
permission name, then the value in `protocol`{.codeph} determines the
exact type of expansion that should occur, and `protocol_data`{.codeph}
is used to help perform the expansion. `protocol_data`{.codeph} may be
empty, in which case the above string should simply take the form:

`${{protocol}}`{.codeph}

There are two protocols supported in the default policy file
implementation:

1.  `${{self}}`{.codeph}

    The protocol, `self`{.codeph}, denotes a replacement of the entire
    string, `${{self}}`{.codeph}, with one or more principal class/name
    pairs. The exact replacement performed depends upon the contents of
    the grant clause to which the permission belongs.

    If the grant clause does not contain any principal information, the
    permission will be ignored (permissions containing
    `${{self}}`{.codeph} in their target names are only valid in the
    context of a principal-based grant clause). For example,
    `BarPermission`{.codeph} will always be ignored in the following
    grant clause:

    ``` {.oac_no_warn dir="ltr"}
    grant codebase "www.foo.example.com", signedby "duke" {
        permission BarPermission "... ${{self}} ...";
    };
    ```

    If the grant clause contains principal information,
    `${{self}}`{.codeph} will be replaced with that same principal
    information. For example, `${{self}}`{.codeph} in
    `BarPermission`{.codeph} will be replaced by
    `javax.security.auth.x500.X500Principal "cn=Duke"`{.codeph} in the
    following grant clause:

    ``` {.oac_no_warn dir="ltr"}
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
    `self`{.codeph} and [KeyStore alias
    replacement](java-se-platform-security-architecture.html#GUID-F5270083-CCAC-49E0-ACAC-50176FBFDD97__GUID-0BB07966-22BF-44C7-9200-21C4B1700432)
    together:

    ``` {.oac_no_warn dir="ltr"}
        keystore "http://foo.bar.example.com/blah/.keystore";

        grant principal "duke" {
            permission BarPermission "... ${{self}} ...";
        };       
    ```

    In the above example, \"duke\" will first be expanded into
    `javax.security.auth.x500.X500Principal "cn=Duke"`{.codeph} assuming
    the X.509 certificate associated with the KeyStore alias,
    `"duke"`{.codeph}, has a subject distinguished name of
    `"cn=Duke"`{.codeph}. Next, `${{self}}`{.codeph} will be replaced
    with the same principal information that just got expanded in the
    grant clause:
    `javax.security.auth.x500.X500Principal "cn=Duke"`{.codeph}.

2.  `${{alias:alias_name}}`{.codeph}

    The protocol, `alias`{.codeph}, denotes a
    <span class="apiname">java.security.KeyStore</span> alias
    substitution. The `KeyStore`{.codeph} used is the one specified in
    the KeyStore entry; see [Policy File
    Format](java-se-platform-security-architecture.html#GUID-F5270083-CCAC-49E0-ACAC-50176FBFDD97).
    `alias_name`{.codeph} represents an alias into the
    `KeyStore`{.codeph}. `${{alias:alias_name}}`{.codeph} is replaced
    with `javax.security.auth.x500.X500Principal "DN"`{.codeph}, where
    `DN`{.codeph} represents the subject distinguished name of the
    certificate belonging to `alias_name`{.codeph}. For example:

    ``` {.oac_no_warn dir="ltr"}
                keystore "http://foo.bar.example.com/blah/.keystore";

                grant codebase "www.foo.example.com" {
                    permission BarPermission "... ${{alias:duke}} ...";
                };
    ```

    In the above example the X.509 certificate associated with the
    alias, `duke`{.codeph}, is retrieved from the `KeyStore`{.codeph},
    `foo.bar.example.com/blah/.keystore`{.codeph}. Assuming duke\'s
    certificate specifies `"o=dukeOrg, cn=duke"`{.codeph} as the subject
    distinguished name, then `${{alias:duke}}`{.codeph} is replaced with
    `javax.security.auth.x500.X500Principal "o=dukeOrg, cn=duke"`{.codeph}.

    The permission entry is ignored under the following error
    conditions:

    -   The keystore entry is unspecified
    -   The `alias_name`{.codeph} is not provided
    -   The certificate for `alias_name`{.codeph} cannot be retrieved
    -   The certificate retrieved is not an X.509 certificate

</div>
</div>
<div class="sect4">
[]{#GUID-938D6987-F1B0-4894-8348-EED3AD4B55FE}

#### Assigning Permissions {#JSSEC-GUID-938D6987-F1B0-4894-8348-EED3AD4B55FE .sect4}

<div>
When a principal executes a class that originated from a particular
<span class="apiname">CodeSource</span>, the security mechanism consults
the policy object to determine what permissions to grant. This is done
by invoking the `getPermissions`{.codeph} or `implies`{.codeph} method
on the <span class="apiname">Policy</span> object that is installed in
the VM.

Clearly, a given code source in a
<span class="apiname">ProtectionDomain</span> can match the code source
given in multiple entries in the policy, for example because the
wildcard (`*`{.codeph}) is allowed.

The following algorithm is used to locate the appropriate set of
permissions in the policy.

1.  Match the public keys, if code is signed.

2.  If a key is not recognized in the policy, then ignore the key.

    If every key is ignored, then treat the code as unsigned.

3.  If the keys are matched or no signer was specified, then try to
    match all URLs in the policy for the keys.

4.  If the keys are matched (or no signer was specified) and the URLs
    are matched (or no codebase was specified), then try to match all
    principals in the policy with the principals associated with the
    current executing thread.

5.  If either key, URL, or principals are not matched, then use the
    built-in default permission, which is the original sandbox
    permission.

The exact meaning of a policy entry codeBase URL value depends on the
characters at the end. A codeBase with a trailing `"/"`{.codeph} matches
all class files (not JAR files) in the specified directory. A codeBase
with a trailing `"/*"`{.codeph} matches all files (both class and JAR
files) contained in that directory. A codeBase with a trailing
`"/-"`{.codeph} matches all files (both class and JAR files) in the
directory and recursively all files in subdirectories contained in that
directory.

As an example, given `"http://example.com/-"`{.codeph} in the policy,
then any code base that is on this web site matches the policy entry.
Matching code bases include `"http://example.com/j2se/sdk/"`{.codeph}
and `"http://example.com/people/gong/appl.jar"`{.codeph}.

If multiple entries are matched, then all the permissions given in those
entries are granted. In other words, permission assignment is additive.
For example, if code signed with key A gets permission X and code signed
by key B gets permission Y and no particular codebase is specified, then
code signed by both A and B gets permissions X and Y. Similarly, if code
with codeBase `"http://example.com/-"`{.codeph} is given permission X,
and `"http://example.com/people/*`{.codeph}\" is given permission Y, and
no particular signers are specified, then an applet from
\"http://example.com/people/applet.jar\" gets both X and Y.

Note that URL matching here is purely syntactic. For example, a policy
can give an entry that specifies a URL
`"ftp://ftp.example.com"`{.codeph}. Such an entry is useful only when
one can obtain Java code directly from ftp for execution.

To specify URLs for the local file system, a file URL can be used. For
example, to specify files in the `/home/cathy/temp` directory in a
Solaris system, you\'d use

``` {.oac_no_warn dir="ltr"}
"file:/home/cathy/temp/*"
```

To specify files in the `temp` directory on the C drive in a Windows
system, use

``` {.oac_no_warn dir="ltr"}
"file:/c:/temp/*"
```

Note: codeBase URLs always use slashes (no backlashes), regardless of
the platform they apply to.

You can also use an absolute path name such as

``` {.oac_no_warn dir="ltr"}
"/home/gong/bin/MyWonderfulJava"
```

</div>
</div>
<div class="sect4">
[]{#GUID-6A3C0484-51D2-4818-8488-AF7CA523EA4A}

#### Default System and User Policy Files {#JSSEC-GUID-6A3C0484-51D2-4818-8488-AF7CA523EA4A .sect4}

<div>
In the Policy reference implementation, the policy can be specified
within one or more policy configuration files. The configuration files
specify what permissions are allowed for code from specified code
sources. A policy file can be composed via a simple text editor. There
is by default a single system-wide policy file, and a single user policy
file. The system policy file is by default located at

-   `{java.home}/conf/security/java.policy` (UNIX-based systems)
-   `{java.home}\conf\security\java.policy` (Windows)

Here, `java.home`{.codeph} is a system property specifying the directory
into which the JDK was installed. The user policy file is by default
located at

-   `{user.home}/.java.policy` (UNIX-based systems)
-   `{user.home}\.java.policy` (Windows)

Here, `user.home`{.codeph} is a system property specifying the user\'s
home directory.

When the Policy is initialized, the system policy is loaded in first,
and then the user policy is added to it. If neither policy is present, a
built-in policy is used. This built-in policy is the same as the
original sandbox policy. Policy file locations are specified in the
security properties file, which is located at

-   `{java.home}/conf/security/java.security` (UNIX-based systems)
-   `{java.home}\conf\security\java.security` (Windows)

The policy file locations are specified as the values of properties
whose names are of the form

``` {.oac_no_warn dir="ltr"}
policy.url.n
```

Here, `n`{.codeph} is a number. You specify each such property value in
a line of the following form:

``` {.oac_no_warn dir="ltr"}
policy.url.n=URL
```

Here, `URL`{.codeph} is a URL specification. For example, the default
system and user policy files are defined in the security properties file
as

``` {.oac_no_warn dir="ltr"}
policy.url.1=file:${java.home}/conf/security/java.policy
policy.url.2=file:${user.home}/.java.policy
```

You can actually specify a number of URLs, including ones of the form
\"http://\", and all the designated policy files will get loaded. You
can also comment out or change the second one to disable reading the
default user policy file.

The algorithm starts at `policy.url.1`{.codeph}, and keeps incrementing
until it does not find a URL. Thus if you have `policy.url.1`{.codeph}
and `policy.url.3`{.codeph}, `policy.url.3`{.codeph} will never be read.

It is also possible to specify an additional or a different policy file
when invoking execution of an application. This can be done via the
`-Djava.security.policy`{.codeph} command-line argument, which sets the
value of the `java.security.policy`{.codeph} property. For example,
consider the following example:

``` {.oac_no_warn dir="ltr"}
java -Djava.security.manager -Djava.security.policy=pURL SomeApp
```

Here, `pURL`{.codeph} is a URL specifying the location of a policy file,
then the specified policy file will be loaded in addition to all the
policy files that are specified in the security properties file. (The
`-Djava.security.manager`{.codeph} argument ensures that the default
security manager is installed, and thus the application is subject to
policy checks, as described in [Managing Applets and
Applications](java-se-platform-security-architecture.html#GUID-DE9A9E41-E735-4624-A015-A22D6C7E75DA).
It is not required if the application `SomeApp`{.codeph} installs a
security manager.)

If you use the following, with a double equals sign, then just the
specified policy file will be used; all others will be ignored.

``` {.oac_no_warn dir="ltr"}
java -Djava.security.manager -Djava.security.policy==pURL SomeApp
```

<div class="infoboxnote" id="GUID-6A3C0484-51D2-4818-8488-AF7CA523EA4A__GUID-E15E92CF-001E-47DB-AA30-DAB2989887DD">
Note:

The `-Djava.security.policy`{.codeph} policy file value will be ignored
(for both `java`{.codeph} and `appletviewer`{.codeph} commands) if
the` policy.allowSystemProperty`{.codeph} property in the security
properties file is set to false. The default is true.

</div>
</div>
</div>
<div class="sect4">
[]{#GUID-DD5954DB-DE02-4121-971A-2AAF56D90F2B}

#### Customizing Policy Evaluation {#JSSEC-GUID-DD5954DB-DE02-4121-971A-2AAF56D90F2B .sect4}

<div>
The current design of the <span class="apiname">Policy</span> class is
not as comprehensive as it could be. We have given the issues much
thought and are progressing cautiously, partly to ensure that we define
method calls that are appropriate for the most common cases. For the
meantime, an alternative policy class can be given to replace the
default policy class, as long as the former is a subclass of the
abstract <span class="apiname">Policy</span> class and implements the
`getPermissions`{.codeph} method (and other methods as necessary).

The <span class="apiname">Policy</span> reference implementation can be
changed by resetting the value of the
<span class="apiname">policy.provider</span> Security Property (in the
Security Properties file, `<java-home>/conf/security/java.security`) to
the fully qualified name of the desired
<span class="apiname">Policy</span> implementation class.

The Security Property `policy.provider` specifies the name of the policy
class, and the default is the following:

``` {.oac_no_warn dir="ltr"}
policy.provider=sun.security.provider.PolicyFile
```

To customize, you can change the property value to specify another
class, as in

``` {.oac_no_warn dir="ltr"}
policy.provider=com.mycom.MyPolicy
```

Note that the <span class="apiname">MyPolicy</span> class must be a
subclass of <span class="apiname">java.security.Policy</span>. It is
perhaps worth emphasizing that such an override of the policy class is a
temporary solution and a more comprehensive policy API will probably
make this unnecessary.

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-6F218913-E967-40AA-A756-3D41FE0D12A2}

### java.security.GeneralSecurityException {#JSSEC-GUID-6F218913-E967-40AA-A756-3D41FE0D12A2 .sect3}

<div>
This is an exception class that is a subclass of
<span class="apiname">java.lang.Exception</span>. The intention is that
there should be two types of exceptions associated with security and the
security packages.

-   <span class="apiname">java.lang.SecurityException</span> and its
    subclasses should be runtime exceptions (unchecked, not declared)
    that are likely to cause the execution of a program to stop.

    Such an exception is thrown only when some sort of security
    violation is detected. For example, such an exception is thrown when
    some code attempts to access a file, but it does not have permission
    for the access. Application developers may catch these exceptions,
    if they want.

<!-- -->

-   <span class="apiname">java.security.GeneralSecurityException</span>,
    which is a subclass of
    <span class="apiname">java.lang.Exception</span> (must be declared
    or caught) that is thrown in all other cases from within the
    security packages.

    Such an exception is security related but non-vital. For example,
    passing in an invalid key is probably not a security violation and
    should be caught and dealt with by a developer.

There are currently still two exceptions within the
<span class="apiname">java.security</span> package that are subclasses
from <span class="apiname">RuntimeException</span>. We at this moment
cannot change these due to backward compatibility requirements. We will
revisit this issue in the future.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-3067791D-ABC6-480E-8E6F-6578F9FFC25D}

Access Control Mechanisms and Algorithms {#JSSEC-GUID-3067791D-ABC6-480E-8E6F-6578F9FFC25D .sect2}
----------------------------------------

<div>
</div>
<div class="sect3">
[]{#GUID-650F5B1E-287D-4DAD-B111-D26E012147C1}

### java.security.ProtectionDomain {#JSSEC-GUID-650F5B1E-287D-4DAD-B111-D26E012147C1 .sect3}

<div>
The <span class="apiname">ProtectionDomain</span> class encapsulates the
characteristics of a domain. Such a domain encloses a set of classes
whose instances are granted a set of permissions when being executed on
behalf of a given set of <span class="apiname">Principals</span>.

A <span class="apiname">ProtectionDomain</span> is constructed with a
<span class="apiname">CodeSource</span>, a
<span class="apiname">ClassLoader</span>, an array of Principals, and a
collection of <span class="apiname">Permissions</span>. The
<span class="apiname">CodeSource</span> encapsulates the codebase
(<span class="apiname">java.net.URL</span>) for all classes in this
domain, as well as a set of certificates (of type
<span class="apiname">java.security.cert.Certificate</span>) for public
keys that correspond to the private keys that signed all code in this
domain. The <span class="apiname">Principal</span>s represent the user
on whose behalf the code is running.

The permissions passed in at
<span class="apiname">ProtectionDomain</span> construction time
represent a static set of permissions bound to the domain regardless of
the <span class="apiname">Policy</span> in force. The
<span class="apiname">ProtectionDomain</span> subsequently consults the
current policy during each security check to retrieve dynamic
permissions granted to the domain.

Classes from different <span class="apiname">CodeSources</span>, or that
are being executed on behalf of different principals, belong to
different domains.

Today all code shipped as part of the JDK is considered system code and
run inside the unique system domain. Each applet or application runs in
its appropriate domain, determined by policy.

It is possible to ensure that objects in any non-system domain cannot
automatically discover objects in another non-system domain. This
partition can be achieved by careful class resolution and loading, for
example, using different classloaders for different domains. However,
<span class="apiname">SecureClassLoader</span> (or its subclasses) can,
at its choice, load classes from different domains, thus allowing these
classes to co-exist within the same name space (as partitioned by a
classloader).

</div>
</div>
<div class="sect3">
[]{#GUID-C3873E27-A5E4-4F6A-BB56-A0AB3EC5684F}

### java.security.AccessController {#JSSEC-GUID-C3873E27-A5E4-4F6A-BB56-A0AB3EC5684F .sect3}

<div>
The <span class="apiname">AccessController</span> class is used for
three purposes, each of which is described in further detail in sections
below:

-   to decide whether an access to a critical system resource is to be
    allowed or denied, based on the security policy currently in effect,
-   to mark code as being \"privileged\", thus affecting subsequent
    access determinations, and
-   to obtain a \"snapshot\" of the current calling context so
    access-control decisions from a different context can be made with
    respect to the saved context.

Any code that controls access to system resources should invoke
<span class="apiname">AccessController</span> methods if it wishes to
use the specific security model and access control algorithm utilized by
these methods. If, on the other hand, the application wishes to defer
the security model to that of the
<span class="apiname">SecurityManager</span> installed at runtime, then
it should instead invoke corresponding methods in the
<span class="apiname">SecurityManager</span> class.

For example, the typical way to invoke access control has been the
following code (taken from an earlier version of JDK):

``` {.oac_no_warn dir="ltr"}
ClassLoader loader = this.getClass().getClassLoader();
if (loader != null) {
    SecurityManager security = System.getSecurityManager();
    if (security != null) {
        security.checkRead("path/file");
    }
}
```

Under the current architecture, the check typically should be invoked
whether or not there is a classloader associated with a calling class.
It could be simply, for example:

``` {.oac_no_warn dir="ltr"}
FilePermission perm = new FilePermission("path/file", "read");
AccessController.checkPermission(perm);
```

The <span class="apiname">AccessController</span>
`checkPermission`{.codeph} method examines the current execution context
and makes the right decision as to whether or not the requested access
is allowed. If it is, this check returns quietly. Otherwise, an
<span class="apiname">AccessControlException</span> (a subclass of
<span class="apiname">java.lang.SecurityException</span>) is thrown.

Note that there are (legacy) cases, for example, in some browsers, where
whether there is a <span class="apiname">SecurityManager</span>
installed signifies one or the other security state that may result in
different actions being taken. For backward compatibility, the
`checkPermission`{.codeph} method on
<span class="apiname">SecurityManager</span> can be used.

``` {.oac_no_warn dir="ltr"}
SecurityManager security = System.getSecurityManager();
if (security != null) {
    FilePermission perm = new FilePermission("path/file", "read");
    security.checkPermission(perm);
}
```

We currently do not change this aspect of the
<span class="apiname">SecurityManager</span> usage, but would encourage
application developers to use new techniques introduced in the JDK in
their future programming when the built-in access control algorithm is
appropriate.

The default behavior of the <span class="apiname">SecurityManager</span>
`checkPermission`{.codeph} method is actually to call the
<span class="apiname">AccessController</span> `checkPermission`{.codeph}
method. A different <span class="apiname">SecurityManager</span>
implementation may implement its own security management approach,
possibly including the addition of further constraints used in
determining whether or not an access is permitted.

</div>
<div class="sect4">
[]{#GUID-9C3AC8FE-C4E6-41EC-A96C-827C5A23D51A}

#### Algorithm for Checking Permissions {#JSSEC-GUID-9C3AC8FE-C4E6-41EC-A96C-827C5A23D51A .sect4}

<div>
Suppose access control checking occurs in a thread of computation that
has a chain of multiple callers (think of this as multiple method calls
that cross the protection domain boundaries), as illustrated in the next
figure.

<span>![Description of jssec\_dt\_027\_anc1.eps
follows](img/jssec_dt_027_anc1.png "Description of jssec_dt_027_anc1.eps follows")\
[Description of the illustration
jssec\_dt\_027\_anc1.eps](img_text/jssec_dt_027_anc1.htm)</span>

When the `checkPermission`{.codeph} method of the
<span class="apiname">AccessController</span> is invoked by the most
recent caller (e.g., a method in the File class), the basic algorithm
for deciding whether to allow or deny the requested access is as
follows.

If any caller in the call chain does not have the requested permission,
<span class="apiname">AccessControlException</span> is thrown, unless
the following is true -- a caller whose domain is granted the said
permission has been marked as \"privileged\" (see the next section) and
all parties subsequently called by this caller (directly or indirectly)
all have the said permission.

There are obviously two implementation strategies:

-   In an \"eager evaluation\" implementation, whenever a thread enters
    a new protection domain or exits from one, the set of effective
    permissions is updated dynamically.

    The benefit is that checking whether a permission is allowed is
    simplified and can be faster in many cases. The disadvantage is
    that, because permission checking occurs much less frequently than
    cross-domain calls, a large percentage of permission updates are
    likely to be useless effort.

<!-- -->

-   In a \"lazy evaluation\" implementation, whenever permission
    checking is requested, the thread state (as reflected by the current
    state, including the current thread\'s call stack or its equivalent)
    is examined and a decision is reached to either deny or grant the
    particular access requested.

    One potential downside of this approach is performance penalty at
    permission checking time, although this penalty would have been
    incurred anyway in the \"eager evaluation\" approach (albeit at
    earlier times and spread out among each cross-domain call). Our
    implementation so far has yielded acceptable performance, so we feel
    that lazy evaluation is the most economical approach overall.

Therefore, the algorithm for checking permissions is currently
implemented as \"lazy evaluation\". Suppose the current thread traversed
m callers, in the order of caller 1 to caller 2 to caller `m`{.codeph}.
Then caller m invoked the `checkPermission`{.codeph} method. The basic
algorithm `checkPermission`{.codeph} uses to determine whether access is
granted or denied is the following (see subsequent sections for
refinements):

``` {.oac_no_warn dir="ltr"}
    for (int i = m; i > 0; i--) {

        if (caller i's domain does not have the permission)
            throw AccessControlException

        else if (caller i is marked as privileged) {
            if (a context was specified in the call to doPrivileged)
                context.checkPermission(permission)
            if (limited permissions were specified in the call to doPrivileged) {
                for (each limited permission) {
                    if (the limited permission implies the requested permission)
                        return;
                }
            } else
                return;
        }
    }

    // Next, check the context inherited when the thread was created.
    // Whenever a new thread is created, the AccessControlContext at
    // that time is stored and associated with the new thread, as the
    // "inherited" context.

    inheritedContext.checkPermission(permission);
```

</div>
</div>
<div class="sect4">
[]{#GUID-E8898CB5-65BB-4D1A-A574-8F7112FC353F}

#### Handling Privileges {#JSSEC-GUID-E8898CB5-65BB-4D1A-A574-8F7112FC353F .sect4}

<div>
A static method in the `AccessController`{.codeph} class allows code in
a class instance to inform the `AccessController`{.codeph} that a body
of its code is \"privileged\" in that it is solely responsible for
requesting access to its available resources, no matter what code caused
it to do so.

That is, a caller can be marked as being \"privileged\" when it calls
the `doPrivileged`{.codeph} method. When making access control
decisions, the `checkPermission`{.codeph} method stops checking if it
reaches a caller that was marked as \"privileged\" via a
`doPrivileged`{.codeph} call without a context argument (see a
subsequent section for information about a context argument). If that
caller\'s domain has the specified permission, no further checking is
done and `checkPermission`{.codeph} returns quietly, indicating that the
requested access is allowed. If that domain does not have the specified
permission, an exception is thrown, as usual.

The normal use of the \"privileged\" feature is as follows:

If you don\'t need to return a value from within the \"privileged\"
block, do the following:

``` {.oac_no_warn dir="ltr"}
  somemethod() {
       ...normal code here...
       AccessController.doPrivileged(new PrivilegedAction() {
           public Object run() {
               // privileged code goes here, for example:
               System.loadLibrary("awt");
               return null; // nothing to return
           }
       });
       ...normal code here...
  }
```

`PrivilegedAction`{.codeph} is an interface with a single method, named
`run`{.codeph}, that returns an Object. The above example shows creation
of an anonymous inner class implementing that interface; a concrete
implementation of the `run`{.codeph} method is supplied. When the call
to `doPrivileged`{.codeph} is made, an instance of the
`PrivilegedAction`{.codeph} implementation is passed to it. The
`doPrivileged`{.codeph} method calls the `run`{.codeph} method from the
`PrivilegedAction`{.codeph} implementation after enabling privileges,
and returns the `run`{.codeph} method\'s return value as the
`doPrivileged`{.codeph} return value, which is ignored in this example.
(For more information about inner classes, see [Nested
Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)
in the Java Tutorials.

If you need to return a value, you can do something like the following:

``` {.oac_no_warn dir="ltr"}
  somemethod() {
       ...normal code here...
       String user = (String) AccessController.doPrivileged(
         new PrivilegedAction() {
           public Object run() {
               return System.getProperty("user.name");
           }
         }
       );
       ...normal code here...
  }
```

If the action performed in your `run`{.codeph} method could throw a
\"checked\" exception (one listed in the `throws`{.codeph} clause of a
method), then you need to use the `PrivilegedExceptionAction`{.codeph}
interface instead of the `PrivilegedAction`{.codeph} interface:

``` {.oac_no_warn dir="ltr"}
  somemethod() throws FileNotFoundException {
       ...normal code here...
     try {
       FileInputStream fis = (FileInputStream)
        AccessController.doPrivileged(
         new PrivilegedExceptionAction() {
           public Object run() throws FileNotFoundException {
               return new FileInputStream("someFile");
           }
         }
       );
     } catch (PrivilegedActionException e) {
       // e.getException() should be an instance of
       // FileNotFoundException,
       // as only "checked" exceptions will be "wrapped" in a
       // <code>PrivilegedActionException</code>.
       throw (FileNotFoundException) e.getException();
     }
       ...normal code here...
 }
```

Some important points about being privileged: Firstly, this concept only
exists within a single thread. As soon as the privileged code completes,
the privilege is guaranteed to be erased or revoked.

Secondly, in this example, the body of code in the `run`{.codeph} method
is privileged. However, if it calls less trustworthy code that is less
privileged, that code will not gain any privileges as a result; a
permission is only granted if the privileged code has the permission
<span class="italic">and</span> so do all the subsequent callers in the
call chain up to the `checkPermission`{.codeph} call.

A variant of
[<span class="apiname">AccessController.doPrivileged</span>](https://docs.oracle.com/javase/10/docs/api/java/security/AccessController.html#doPrivileged-java.security.PrivilegedAction-java.security.AccessControlContext-java.security.Permission...-)
enables code to assert a subset of its privileges without preventing the
full traversal of the stack to check for other permissions. See
[Asserting a Subset of
Privileges](java-se-platform-security-architecture.html#GUID-35DBFA01-FEF4-4382-A5D1-4AD2CA441CDA).

For more information about marking code as \"privileged,\" see [Appendix
A: API for Privileged
Blocks](java-se-platform-security-architecture.html#GUID-BB3C8FB3-1A1A-47F3-8536-3952B84F46F2 "This section explains what privileged code is and what it is used for. It also shows you how to use the doPrivileged API.").

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-734D48E4-81FB-4EFF-9459-AEAD30DA3408}

### Inheritance of Access Control Context {#JSSEC-GUID-734D48E4-81FB-4EFF-9459-AEAD30DA3408 .sect3}

<div>
When a thread creates a new thread, a new stack is created. If the
current security context was not retained when this new thread was
created, then when `AccessController.checkPermission`{.codeph} was
called inside the new thread, a security decision would be made based
solely upon the new thread\'s context, not taking into consideration
that of the parent thread.

This clean stack issue would not be a security problem per se, but it
would make the writing of secure code, and especially system code, more
prone to subtle errors. For example, a non-expert developer might
assume, quite reasonably, that a child thread (e.g., one that does not
involve untrusted code) inherits the same security context from the
parent thread (e.g., one that involves untrusted code). This would cause
unintended security holes when accessing controlled resources from
inside the new thread (and then passing the resources along to less
trusted code), if the parent context was not in fact saved.

Thus, when a new thread is created, we actually ensure (via thread
creation and other code) that it automatically inherits the parent
thread\'s security context at the time of creation of the child thread,
in such a way that subsequent `checkPermission`{.codeph} calls in the
child thread will take into consideration the inherited parent context.

In other words, the logical thread context is expanded to include both
the parent context (in the form of an
<span class="apiname">AccessControlContext</span>, described in the next
section) and the current context, and the algorithm for checking
permissions is expanded to the following. (Recall there are m callers up
to the call to `checkPermission`{.codeph}, and see the next section for
information about the <span class="apiname">AccessControlContext</span>
`checkPermission`{.codeph} method.)

``` {.oac_no_warn dir="ltr"}
    for (int i = m; i > 0; i--) {

        if (caller i's domain does not have the permission)
            throw AccessControlException

        else if (caller i is marked as privileged) {
            if (a context was specified in the call to doPrivileged)
                context.checkPermission(permission)
            if (limited permissions were specified in the call to doPrivileged) {
                for (each limited permission) {
                    if (the limited permission implies the requested permission)
                        return;
                }
            } else
                return;
        }
    }

    // Next, check the context inherited when the thread was created.
    // Whenever a new thread is created, the AccessControlContext at
    // that time is stored and associated with the new thread, as the
    // "inherited" context.

    inheritedContext.checkPermission(permission);
```

Note that this inheritance is transitive so that, for example, a
grandchild inherits both from the parent and the grandparent. Also note
that the inherited context snapshot is taken when the new child is
created, and not when the child is first run. There is no public API
change for the inheritance feature.

</div>
</div>
<div class="sect3">
[]{#GUID-046F1EA2-133F-4D9B-9EF2-EB21FBB3C5E9}

### java.security.AccessControlContext {#JSSEC-GUID-046F1EA2-133F-4D9B-9EF2-EB21FBB3C5E9 .sect3}

<div>
Recall that the <span class="apiname">AccessController</span>
`checkPermission`{.codeph} method performs security checks within the
context of the current execution thread (including the inherited
context). A difficulty arises when such a security check can only be
done in a different context. That is, sometimes a security check that
should be made within a given context will actually need to be done from
within a different context. For example, when one thread posts an event
to another thread, the second thread serving the requesting event would
not have the proper context to complete access control, if the service
requests access to controller resources.

To address this issue, we provide the
<span class="apiname">AccessController</span> `getContext`{.codeph}
method and <span class="apiname">AccessControlContext</span> class. The
`getContext`{.codeph} method takes a \"snapshot\" of the current calling
context, and places it in an
<span class="apiname">AccessControlContext</span> object, which it
returns. A sample call is the following:

``` {.oac_no_warn dir="ltr"}
    AccessControlContext acc = AccessController.getContext();
```

This context captures relevant information so that an access control
decision can be made by checking, from within a different context,
against this context information. For example, one thread can post a
request event to a second thread, while also supplying this context
information. <span class="apiname">AccessControlContext</span> itself
has a `checkPermission`{.codeph} method that makes access decisions
based on the context it encapsulates, rather than that of the current
execution thread. Thus, the second thread can perform an appropriate
security check if necessary by invoking the following:

``` {.oac_no_warn dir="ltr"}
    acc.checkPermission(permission);
```

The above method call is equivalent to performing the same security
check in the context of the first thread, even though it is done in the
second thread.

There are also times where one or more permissions must be checked
against an access control context, but it is unclear a priori which
permissions are to be checked. In these cases you can use the
`doPrivileged`{.codeph} method that takes a context:

``` {.oac_no_warn dir="ltr"}
    somemethod() {
        AccessController.doPrivileged(new PrivilegedAction() {
            public Object run() {
                // Code goes here. Any permission checks from 
                // this point forward require both the current 
                // context and the snapshot's context to have 
                // the desired permission.
             }
        });
        ...normal code here...
```

Now the complete algorithm utilized by the
<span class="apiname">AccessController</span> `checkPermission`{.codeph}
method can be given. Suppose the current thread traversed `m`{.codeph}
callers, in the order of caller 1 to caller 2 to caller `m`{.codeph}.
Then caller `m`{.codeph} invoked the `checkPermission`{.codeph} method.
The algorithm `checkPermission`{.codeph} uses to determine whether
access is granted or denied is the following

``` {.oac_no_warn dir="ltr"}
    for (int i = m; i > 0; i--) {

        if (caller i's domain does not have the permission)
            throw AccessControlException

        else if (caller i is marked as privileged) {
            if (a context was specified in the call to doPrivileged)
                context.checkPermission(permission)
            if (limited permissions were specified in the call to doPrivileged) {
                for (each limited permission) {
                    if (the limited permission implies the requested permission)
                        return;
                }
            } else
                return;
        }
    }

    // Next, check the context inherited when the thread was created.
    // Whenever a new thread is created, the AccessControlContext at
    // that time is stored and associated with the new thread, as the
    // "inherited" context.

    inheritedContext.checkPermission(permission);
```

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-C4FA75FE-B65C-4D8E-B608-D21A8D769A7D}

Secure Class Loading {#JSSEC-GUID-C4FA75FE-B65C-4D8E-B608-D21A8D769A7D .sect2}
--------------------

<div>
Dynamic class loading is an important feature of the Java Virtual
Machine because it provides the Java platform with the ability to
install software components at run-time. It has a number of unique
characteristics. First of all, lazy loading means that classes are
loaded on demand and at the last moment possible. Second, dynamic class
loading maintains the type safety of the Java Virtual Machine by adding
link-time checks, which replace certain run-time checks and are
performed only once. Moreover, programmers can define their own class
loaders that, for example, specify the remote location from which
certain classes are loaded, or assign appropriate security attributes to
them. Finally, class loaders can be used to provide separate name spaces
for various software components. For example, a browser can load applets
from different web pages using separate class loaders, thus maintaining
a degree of isolation between those applet classes. In fact, these
applets can contain classes of the same name -- these classes are
treated as distinct types by the Java Virtual Machine.

The class loading mechanism is not only central to the dynamic nature of
the Java programming language. It also plays a critical role in
providing security because the class loader is responsible for locating
and fetching the class file, consulting the security policy, and
defining the class object with the appropriate permissions.

</div>
<div class="sect3">
[]{#GUID-221C1C24-AC48-45D4-B6BF-B31F8ACAFA04}

### Class Loader Class Hierarchies {#JSSEC-GUID-221C1C24-AC48-45D4-B6BF-B31F8ACAFA04 .sect3}

<div>
When loading a class, because there can be multiple instances of class
loader objects in one Java Virtual Machine, an important question is how
do we determine which class loader to use. The JDK has introduced
multiple class loader classes are introduced that have distinct
properties, so another important question is what type of class loader
we should use.

The root of the class loader class hierarchy is an abstract class called
<span class="apiname">java.lang.ClassLoader</span>. Class
<span class="apiname">java.security.SecureClassLoader</span> is a
subclass and a concrete implementation of the abstract
<span class="apiname">ClassLoader</span> class. Class
<span class="apiname">java.net.URLClassLoader</span> is a subclass of
<span class="apiname">SecureClassLoader</span>.

When creating a custom class loader class, one can subclass from any of
the above class loader classes, depending on the particular needs of the
custom class loader.

</div>
</div>
<div class="sect3">
[]{#GUID-24372B10-3942-4084-803F-8E5CD7F1B72C}

### The Primordial Class Loader {#JSSEC-GUID-24372B10-3942-4084-803F-8E5CD7F1B72C .sect3}

<div>
Because each class is loaded by its class loader, and each class loader
itself is a class and must be loaded by another class loader, we seem to
have the obvious chicken-and-egg problem, i.e., where does the first
class loader come from? There is a \"primordial\'\' class loader that
bootstraps the class loading process. The primordial class loader is
generally written in a native language, such as C, and does not manifest
itself within the Java context. The primordial class loader often loads
classes from the local file system in a platform-dependent manner.

Some classes, such as those defined in the
<span class="apiname">java.\*</span> package, are essential for the
correct functioning of the Java Virtual Machine and runtime system. They
are often referred to as base classes. Due to historical reasons, all
such classes have a class loader that is a null. This null class loader
is perhaps the only sign of the existence of a primordial class loader.
In fact, it is easier to simply view the null class loader as the
primordial class loader.

Given all classes in one Java application environment, we can easily
form a class loading tree to reflect the class loading relationship.
Each class that is not a class loader is a leaf node. Each class\'s
parent node is its class loader, with the null class loader being the
root class. Such a structure is a tree because there cannot be cycles --
a class loader cannot have loaded its own ancestor class loader.

</div>
</div>
<div class="sect3">
[]{#GUID-AEABE469-63AF-4041-B0F4-A283971DCFD6}

### Class Loader Delegation {#JSSEC-GUID-AEABE469-63AF-4041-B0F4-A283971DCFD6 .sect3}

<div>
When one class loader is asked to load a class, this class loader either
loads the class itself or it can ask another class loader to do so. In
other words, the first class loader can delegate to the second class
loader. The delegation relationship is virtual in the sense that it has
nothing to do with which class loader loads which other class loader.
Instead, the delegation relationship is formed when class loader objects
are created, and in the form of a parent-child relationship.
Nevertheless, the system class loader is the delegation root ancestor of
all class loaders. Care must be taken to ensure that the delegation
relationship does not contain cycles. Otherwise, the delegation process
may enter into an infinite loop.

</div>
</div>
<div class="sect3">
[]{#GUID-044B4753-FEC7-4B9F-AD73-EE8EBAC66D21}

### Class Resolution Algorithm {#JSSEC-GUID-044B4753-FEC7-4B9F-AD73-EE8EBAC66D21 .sect3}

<div>
The default implementation of the JDK
<span class="apiname">ClassLoader</span> method for loading a class
searches for classes in the following order:

-   Check if the class has already been loaded.
-   If the current class loader has a specified delegation parent,
    delegate to the parent to try to load this class. If there is no
    parent, delegate to the primordial class loader.
-   Call a customizable method to find the class elsewhere.

Here, the first step looks into the class loader\'s local cache (or its
functional equivalent, such as a global cache) to see if a loaded class
matches the target class. The last step provides a way to customize the
mechanism for looking for classes; thus a custom class loader can
override this method to specify how a class should be looked up. For
example, an applet class loader can override this method to go back to
the applet host and try to locate the class file and load it over the
network.

If at any step a class is located, it is returned. If the class is not
found using the above steps, a
<span class="apiname">ClassNotFound</span> exception is thrown.

Observe that it is critical for type safety that the same class not be
loaded more than once by the same class loader. If the class is not
among those already loaded, the current class loader attempts to
delegate the task to the parent class loader. This can occur
recursively. This ensures that the appropriate class loader is used. For
example, when locating a system class, the delegation process continues
until the system class loader is reached.

We have seen the delegation algorithm earlier. But, given the name of
any class, which class loader do we start with in trying to load the
class? The rules for determining the class loader are the following:

-   When loading the first class of an application, a new instance of
    the <span class="apiname">URLClassLoader</span> is used.
-   When loading the first class of an applet, a new instance of the
    <span class="apiname">AppletClassLoader</span> is used.
-   When <span class="apiname">java.lang.Class.ForName</span> is
    directly called, the primordial class loader is used.
-   If the request to load a class is triggered by a reference to it
    from an existing class, the class loader for the existing class is
    asked to load the class.

Note that rules about the use of
<span class="apiname">URLClassLoader</span> and
<span class="apiname">AppletClassLoader</span> instances have exceptions
and can vary depending on the particular system environment. For
example, a web browser may choose to reuse an existing
<span class="apiname">AppletClassLoader</span> to load applet classes
from the same web page.

Due to the power of class loaders, we severely restrict who can create
class loader instances. On the other hand, it is desirable to provide a
convenient mechanism for applications or applets to specify URL
locations and load classes from them. We provide static methods to allow
any program to create instances of the
<span class="apiname">URLClassLoader</span> class, although not other
types of class loaders.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-36A4FAF4-B31B-4BF1-A030-51E9555FE349}

Security Management {#JSSEC-GUID-36A4FAF4-B31B-4BF1-A030-51E9555FE349 .sect2}
-------------------

<div>
</div>
<div class="sect3">
[]{#GUID-DE9A9E41-E735-4624-A015-A22D6C7E75DA}

### Managing Applets and Applications {#JSSEC-GUID-DE9A9E41-E735-4624-A015-A22D6C7E75DA .sect3}

<div>
Currently, all JDK system code invokes
<span class="apiname">SecurityManager</span> methods to check the policy
currently in effect and perform access control checks. There is
typically a security manager
(<span class="apiname">SecurityManager</span> implementation) installed
whenever an applet is running; the
<span class="apiname">appletviewer</span> and most browsers install a
security manager.

A security manager is not automatically installed when an application is
running. To apply the same security policy to an application found on
the local file system as to downloaded applets, either the user running
the application must invoke the Java Virtual Machine with the
`-Djava.security.manager`{.codeph} command-line argument (which sets the
value of the `java.security.manager`{.codeph} property), as in

``` {.oac_no_warn dir="ltr"}
    java -Djava.security.manager SomeApp
```

or the application itself must call the `setSecurityManager`{.codeph}
method in the <span class="apiname">java.lang.System</span> class to
install a security manager.

It is possible to specify on the command line a particular security
manager to be utilized, by following `-Djava.security.manager`{.codeph}
with an equals and the name of the class to be used as the security
manager, as in

``` {.oac_no_warn dir="ltr"}
    java -Djava.security.manager=COM.abc.MySecMgr SomeApp
```

If no security manager is specified, the built-in default security
manager is utilized (unless the application installs a different
security manager). All of the following are equivalent and result in
usage of the default security manager:

``` {.oac_no_warn dir="ltr"}
    java -Djava.security.manager SomeApp
    java -Djava.security.manager="" SomeApp
    java -Djava.security.manager=default SomeApp
```

The JDK includes a property named `java.class.path`{.codeph}. Classes
that are stored on the local file system but should not be treated as
base classes (e.g., classes built into the SDK) should be on this path.
Classes on this path are loaded with a secure class loader and are thus
subjected to the security policy being enforced.

There is also a `-Djava.security.policy`{.codeph} command-line argument
whose usage determines what policy files are utilized. This command-line
argument is described in detail in [Default Policy Implementation and
Policy File
Syntax](permissions-jdk1.html#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D).
Basically, if you don\'t include `-Djava.security.policy`{.codeph} on
the command line, then the policy files specified in the security
properties file will be used.

You can use a `-Djava.security.policy`{.codeph} command-line argument to
specify an additional or a different policy file when invoking execution
of an application. For example, if you type the following, where
`pURL`{.codeph} is a URL specifying the location of a policy file, then
the specified policy file will be loaded in addition to all the policy
files specified in the security properties file:

``` {.oac_no_warn dir="ltr"}
    java -Djava.security.manager -Djava.security.policy=pURL SomeApp
```

If you instead type the following command, using a double equals, then
just the specified policy file will be used; all others will be ignored:

``` {.oac_no_warn dir="ltr"}
    java -Djava.security.manager -Djava.security.policy==pURL SomeApp
```

</div>
</div>
<div class="sect3">
[]{#GUID-B83ECC0C-02AB-497A-B07D-D74AB9572DC7}

### SecurityManager versus AccessController {#JSSEC-GUID-B83ECC0C-02AB-497A-B07D-D74AB9572DC7 .sect3}

<div>
The new access control mechanism is fully backward compatible. For
example, all `check`{.codeph} methods in
<span class="apiname">SecurityManager</span> are still supported,
although most of their implementations are changed to call the new
<span class="apiname">SecurityManager</span> `checkPermission`{.codeph}
method, whose default implementation calls the
<span class="apiname">AccessController</span> `checkPermission`{.codeph}
method. Note that certain internal security checks may stay in the
<span class="apiname">SecurityManager</span> class, unless it can be
parameterized.

We have not at this time revised any system code to call
<span class="apiname">AccessController</span> instead of calling
<span class="apiname">SecurityManager</span> (and checking for the
existence of a classloader), because of the potential of existing
third-party applications that subclass the
<span class="apiname">SecurityManager</span> and customize the
`check`{.codeph} methods. In fact, we added a new method
`SecurityManager.checkPermission`{.codeph} that by default simply
invokes `AccessController.checkPermission`{.codeph}.

To understand the relationship between
<span class="apiname">SecurityManager</span> and
<span class="apiname">AccessController</span>, it is sufficient to note
that <span class="apiname">SecurityManager</span> represents the concept
of a central point of access control, while
<span class="apiname">AccessController</span> implements a particular
access control algorithm, with special features such as the
`doPrivileged`{.codeph} method. By keeping
<span class="apiname">SecurityManager</span> up to date, we maintain
backward compatibility (e.g., for those applications that have written
their own security manager classes based on earlier versions of the JDK)
and flexibility (e.g., for someone wanting to customize the security
model to implement mandatory access control or multilevel security). By
providing <span class="apiname">AccessController</span>, we build in the
algorithm that we believe is the most restrictive and that relieves the
typical programmer from the burden of having to write extensive security
code in most scenarios.

We encourage the use of <span class="apiname">AccessController</span> in
application code, while customization of a security manager (via
subclassing) should be the last resort and should be done with extreme
care. Moreover, a customized security manager, such as one that always
checks the time of the day before invoking standard security checks,
could and should utilize the algorithm provided by
<span class="apiname">AccessController</span> whenever appropriate.

One thing to remember is that, when you implement your own
`SecurityManager`{.codeph}, you should install it as trusted software
and grant it `java.security.AllPermission`{.codeph}. You can do this by
adjusting the policy file to grant `AllPermission`{.codeph} to your
`SecurityManager`{.codeph}. For more information, see [Default Policy
Implementation and Policy File
Syntax](permissions-jdk1.html#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D).

</div>
</div>
<div class="sect3">
[]{#GUID-1EE99075-F7E3-4EF6-988F-C7C0817508B9}

### Auxiliary Tools {#JSSEC-GUID-1EE99075-F7E3-4EF6-988F-C7C0817508B9 .sect3}

<div>
This section briefly describes the usage of two tools that assist in the
deployment of security features.

</div>
<div class="sect4">
[]{#GUID-491B4412-CD5A-4D06-AB51-88AF8E30D42B}

#### The Key and Certificate Management Tool {#JSSEC-GUID-491B4412-CD5A-4D06-AB51-88AF8E30D42B .sect4}

<div>
<span class="bold">keytool</span> is a key and certificate management
utility. It enables users to administer their own public/private key
pairs and associated certificates for use in self-authentication (where
the user authenticates himself/herself to other users/services) or data
integrity and authentication services, using digital signatures. The
authentication information includes both a sequence (chain) of X.509
certificates, and an associated private key, which can be referenced by
a so-called \"alias\". This tool also manages certificates (that are
\"trusted\" by the user), which are stored in the same database as the
authentication information, and can be referenced by an \"alias\".

<span class="bold">keytool</span> stores the keys and certificates in a
so-called <span class="italic">keystore</span>. The default keystore
implementation implements the keystore as a file. It protects private
keys with a password.

The chains of X.509 certificates are provided by organizations called
Certification Authorities, or CAs. Identities (including CAs) use their
private keys to authenticate their association with objects (such as
with channels which are secured using SSL), with archives of code they
signed, or (for CAs) with X.509 certificates they have issued. As a
bootstrapping tool, certificates generated using the -genkey command may
be used until a Certification Authority returns a certificate chain.

The private keys in this database are always stored in encrypted form,
to make it difficult to disclose these private keys inappropriately. A
password is required to access or modify the database. These private
keys are encrypted using the \"password\", which should be several words
long. If the password is lost, those authentication keys cannot be
recovered.

In fact, each private key in the keystore can be protected using its own
individual password, which may or may not be the same as the password
that protects the keystore\'s overall integrity.

This tool is (currently) intended to be used from the command line,
where one simply types `keytool`{.codeph} as a shell prompt.
<span class="bold">keytool</span> is a script that executes the
appropriate Java classes and is built together with the SDK.

The command line options for each command may be provided in any order.
Typing an incorrect option or typing `keytool -help`{.codeph} will cause
the tool\'s usage to be summarized on the output device (such as a shell
window). See
[keytool](olink:JSWOR-GUID-5990A2E4-78E3-47B7-AE75-6D1826259549) in
<span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

</div>
</div>
<div class="sect4">
[]{#GUID-7D6D44B5-8BC7-48DB-B0D3-A9E824522AC6}

#### The JAR Signing and Verification Tool {#JSSEC-GUID-7D6D44B5-8BC7-48DB-B0D3-A9E824522AC6 .sect4}

<div>
The <span class="bold">jarsigner</span> tool can be used to digitally
sign Java archives (JAR files), and to verify such signatures. This tool
depends on the keystore that is managed by the
<span class="bold">keytool</span>. Its usage is quickly summarized
below. See
[jarsigner](olink:JSWOR-GUID-925E7A1B-B3F3-44D2-8B49-0B3FA2C54864) in
<span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

</div>
</div>
</div>
</div>
<div class="sect2">
[]{#GUID-032A4F7C-C654-45A7-8931-9E7385BEFCB1}

GuardedObject and SignedObject {#JSSEC-GUID-032A4F7C-C654-45A7-8931-9E7385BEFCB1 .sect2}
------------------------------

<div>
</div>
<div class="sect3">
[]{#GUID-2D31C55D-F676-4993-B159-CE27A336509C}

### java.security.GuardedObject and java.security.Guard {#JSSEC-GUID-2D31C55D-F676-4993-B159-CE27A336509C .sect3}

<div>
Recall that the class <span class="apiname">AccessControlContext</span>
is useful when an access control decision has to be made in a different
context. There is another such scenario, where the supplier of a
resource is not in the same thread as the consumer of that resource, and
the consumer thread cannot provide the supplier thread the access
control context information (because the context is security-sensitive,
or the context is too large to pass, or for other reasons). For this
case, we provide a class called
<span class="apiname">GuardedObject</span> to protect access to the
resource, illustrated in the figure below.

<span>![The following paragraph described this
figure.](img/jssec_dt_033_anca3.png "The following paragraph described this figure.")</span>

The basic idea is that the supplier of the resource can create an object
representing the resource, create a
<span class="apiname">GuardedObject</span> that embeds the resource
object inside, and then provide the
<span class="apiname">GuardedObject</span> to the consumer. In creating
the <span class="apiname">GuardedObject</span>, the supplier also
specifies a <span class="apiname">Guard</span> object such that anyone
(including the consumer) can only obtain the resource object if certain
(security) checks inside the <span class="apiname">Guard</span> are
satisfied.

<span class="apiname">Guard</span> is an interface, so any object can
choose to become a <span class="apiname">Guard</span>. The only method
in this interface is called `checkGuard`{.codeph}. It takes an
<span class="apiname">Object</span> argument and it performs certain
(security) checks. The <span class="apiname">Permission</span> class in
<span class="apiname">java.security</span> implements the
<span class="apiname">Guard</span> interface.

For example, suppose a system thread is asked to open a file
`/a/b/c.txt` for read access, but the system thread does not know who
the requestor is or under what circumstances the request is made.
Therefore, the correct access control decision cannot be made at the
server side. The system thread can use
<span class="apiname">GuardedObject</span> to delay the access control
checking, as follows.

``` {.oac_no_warn dir="ltr"}
    FileInputStream f = new FileInputStream("/a/b/c.txt");
    FilePermission p = new FilePermission("/a/b/c.txt", "read");
    GuardedObject g = new GuardedObject(f, p);
```

Now the system thread can pass g to the consumer thread. For that thread
to obtain the file input stream, it has to call

``` {.oac_no_warn dir="ltr"}
    FileInputStream fis = (FileInputStream) g.getObject();
```

This method in turn invokes the `checkGuard`{.codeph} method on the
<span class="apiname">Guard</span> object `p`{.codeph}, and because
`p`{.codeph} is a <span class="apiname">Permission</span>, its
`checkGuard`{.codeph} method is in fact:

``` {.oac_no_warn dir="ltr"}
    SecurityManager sm = System.getSecurityManager();
    if (sm != null) sm.checkPermission(this);
```

This ensures that a proper access control check takes place within the
consumer context. In fact, one can replace often-used hash tables and
access control lists in many cases and simply store a hash table of
<span class="apiname">GuardedObjects</span>.

This basic pattern of <span class="apiname">GuardedObject</span> and
<span class="apiname">Guard</span> is very general, and we expect that
by extending the basic <span class="apiname">Guard</span> and
<span class="apiname">GuardedObject</span> classes, developers can
easily obtain quite powerful access control tools. For example,
per-method invocation can be achieved with an appropriate
<span class="apiname">Guard</span> for each method, and a
<span class="apiname">Guard</span> can check the time of the day, the
signer or other identification of the caller, or any other relevant
information.

Note that certain typing information is lost because
<span class="apiname">GuardedObject</span> returns an
<span class="apiname">Object</span>.
<span class="apiname">GuardedObject</span> is intended to be used
between cooperating parties so that the receiving party should know what
type of object to expect (and to cast for). In fact, we envision that
most usage of <span class="apiname">GuardedObject</span> involves
<span class="apiname">subclassing</span> it (say to form a
<span class="apiname">GuardedFileInputStream</span> class), thus
encapsulating typing information, and casting can happen suitably in the
subclass.

</div>
</div>
<div class="sect3">
[]{#GUID-1BE94E77-1A54-4A0E-BCD1-6E395A576A78}

### java.security.SignedObject {#JSSEC-GUID-1BE94E77-1A54-4A0E-BCD1-6E395A576A78 .sect3}

<div>
This class is an essential building block for other security primitives.
<span class="apiname">SignedObject</span> contains another
<span class="apiname">Serializable</span> object, the (to-be-)signed
object and its signature. If the signature is not null, it contains a
valid digital signature of the signed object. This is illustrated in the
figure below.

<span>![The previous paragraph describes this
figure.](img/jssec_dt_034_anca9.png "The previous paragraph describes this figure.")</span>

The underlying signing algorithm is set through a Signature object as a
parameter to the `sign`{.codeph} method call, and the algorithm can be,
among others, the NIST standard DSA, using DSA and SHA-256. The
algorithm is specified using the same convention for signatures, such as
\"SHA/DSA\".

The signed object is a \"deep copy\" (in serialized form) of an original
object. Once the copy is made, further manipulation of the original
object has no side effect on the copy. A signed object is immutable.

A typical example of creating a signed object is the following:

``` {.oac_no_warn dir="ltr"}
    Signature signingEngine = Signature.getInstance(algorithm,provider);
    SignedObject so = new SignedObject(myobject, signingKey, signingEngine);
```

A typical example of verification is the following (having received
<span class="apiname">SignedObject</span> `so`{.codeph}), where the
first line is not needed if the name of the algorithm is known:

``` {.oac_no_warn dir="ltr"}
    String algorithm = so.getAlgorithm();
    Signature verificationEngine = Signature.getInstance(algorithm, provider);
    so.verify(verificationEngine);
```

Potential applications of <span class="apiname">SignedObject</span>
include:

-   It can be used internally to any Java application environment as an
    unforgeable authorization token -- one that can be passed around
    without the fear that the token can be maliciously modified without
    being detected.
-   It can be used to sign and serialize data/object for storage outside
    the Java runtime (e.g., storing critical access control data on
    disk).
-   Nested <span class="apiname">SignedObjects</span> can be used to
    construct a logical sequence of signatures, resembling a chain of
    authorization and delegation.

It is intended that this class can be subclassed in the future to allow
multiple signatures on the same signed object. In that case, existing
method calls in this base class will be fully compatible in semantics.
In particular, any `get`{.codeph} method will return the unique value if
there is only one signature, and will return an arbitrary one from the
set of signatures if there is more than one signature.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-2AB14B2B-AEDD-413D-B3AF-22F58BE10F34}

Discussion and Future Directions {#JSSEC-GUID-2AB14B2B-AEDD-413D-B3AF-22F58BE10F34 .sect2}
--------------------------------

<div>
</div>
<div class="sect3">
[]{#GUID-9B24696B-B2A9-428E-8017-BE4A1952DFBF}

### Resource Consumption Management {#JSSEC-GUID-9B24696B-B2A9-428E-8017-BE4A1952DFBF .sect3}

<div>
Resource consumption management is relatively easy to implement in some
cases (e.g., to limit the number of windows any application can pop up
at any one time), while it can be quite hard to implement efficiently in
other cases (e.g., to limit memory or file system usage). We plan to
coherently address such issues in the future.

</div>
</div>
<div class="sect3">
[]{#GUID-489C2508-06FA-420D-B7AF-5E993C263AE8}

### Arbitrary Grouping of Permissions {#JSSEC-GUID-489C2508-06FA-420D-B7AF-5E993C263AE8 .sect3}

<div>
Sometimes it is convenient to group a number of permissions together and
use a short-hand name to refer to them. For example, if we would like to
have a permission called `SuperPermission`{.codeph} to include (and
imply) both `FilePermission("-", "read,write")`{.codeph} and
`SocketPermission("*", "connect,accept")`{.codeph}, technically we can
use the class <span class="apiname">Permissions</span> or a similar
class to implement this super permission by using the `add`{.codeph}
methods to add the required permissions. And such grouping can be
arbitrarily complicated.

The more difficult issues are the following. First, to understand what
actual permissions one is granting when giving out such a super
permission, either a fixed and named permission class is created to
denote a statically specified group of permissions, or the member
permissions need to be spelled out in the policy file. Second,
processing the policy (file) can become more complicated because the
grouped permissions may need to be expanded. Moreover, nesting of
grouped permission increases complexity even more.

</div>
</div>
<div class="sect3">
[]{#GUID-9F0CA451-E717-400C-BC46-7CACD6640F97}

### Object-Level Protection {#JSSEC-GUID-9F0CA451-E717-400C-BC46-7CACD6640F97 .sect3}

<div>
Given the object-oriented nature of the Java programming language, it is
conceivable that developers will benefit from a set of appropriate
object-level protection mechanisms that (1) goes beyond the natural
protection provided by the Java programming language and that (2)
supplements the thread-based access control mechanism.

One such mechanism is <span class="apiname">SignedObject</span>. Another
is the <span class="apiname">SealedObject</span> class, which uses
encryption to hide the content of an object.

<span class="apiname">GuardedObject</span> is a general way to enforce
access control at a per class/object per method level. This method,
however, should be used only selectively, partly because this type of
control can be difficult to administer at a high level.

</div>
</div>
<div class="sect3">
[]{#GUID-212090BE-D62C-4E0E-8D61-5F4A05EDFE82}

### Subdividing Protection Domains {#JSSEC-GUID-212090BE-D62C-4E0E-8D61-5F4A05EDFE82 .sect3}

<div>
A potentially useful concept not currently implemented is that of
\"subdomains.\" A subdomain is one that is enclosed in another. A
subdomain would not have more permissions or privileges than the domain
of which it is a subpart. A domain could be created, for example, to
selectively further limit what a program can do.

Often a domain is thought of as supporting inheritance: a subdomain
would automatically inherit the parent domain\'s security attributes,
except in certain cases where the parent further restricts the subdomain
explicitly. Relaxing a subdomain by right amplification is a possibility
with the notion of trusted code.

For convenience, we can think of the system domain as a single, big
collection of all system code. For better protection, though, system
code should be run in multiple system domains, where each domain
protects a particular type of resource and is given a special set of
rights. For example, if file system code and network system code run in
separate domains, where the former has no rights to the networking
resources and the latter has no rights to the file system resources, the
risks and consequence of an error or security flaw in one system domain
is more likely to be confined within its boundary.

</div>
</div>
<div class="sect3">
[]{#GUID-4D698AAC-212D-40F6-A1EF-343598D550BB}

### Running Applets with Signed Content {#JSSEC-GUID-4D698AAC-212D-40F6-A1EF-343598D550BB .sect3}

<div>
The JAR and Manifest specifications on code signing allow a very
flexible format. Classes within the same archive can be signed with
different keys, and a class can be unsigned, signed with one key, or
signed with multiple keys. Other resources within the archive, such as
audio clips and graphic images, can also be signed or unsigned, just
like classes can.

This flexibility brings about the issue of interpretation. The following
questions need to be answered, especially when keys are treated
differently:

1.  Should images and audios be required to be signed with the same key
    if any class in the archive is signed?

2.  If images and audios are signed with different keys, can they be
    placed in the same `appletviewer`{.codeph} (or browser page), or
    should they be sent to different viewers for processing?

These questions are not easy to answer, and require consistency across
platforms and products to be the most effective. Our intermediate
approach is to provide a simple answer -- all images and audio clips are
forwarded to be processed within the same applet classloader, whether
they are signed or not. This temporary solution will be improved once a
consensus is reached.

Moreover, if a digital signature cannot be verified because the bytecode
content of a class file does not match the signed hash value in the JAR,
a security exception is thrown, as the original intention of the JAR
author is clearly altered. Previously, there was a suggestion to run
such code as untrusted. This idea is undesirable because the applet
classloader allows the loading of code signed by multiple parties. This
means that accepting a partially modified JAR file would allow an
untrusted piece of code to run together with and access other code
through the same classloader.

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-BB3C8FB3-1A1A-47F3-8536-3952B84F46F2}

Appendix A: API for Privileged Blocks {#JSSEC-GUID-BB3C8FB3-1A1A-47F3-8536-3952B84F46F2 .sect2}
-------------------------------------

<div>
This section explains what privileged code is and what it is used for.
It also shows you how to use the doPrivileged API.

-   [Using the doPrivileged
    API](java-se-platform-security-architecture.html#GUID-3747895F-0C78-45D7-9CA9-AEE9A1FDC217 "This section describes the doPrivileged API and the use of the privileged feature.")
-   [What It Means to Have Privileged
    Code](java-se-platform-security-architecture.html#GUID-73F600BE-8098-4613-AD4B-E2DEFB9118D8 "Marking code as privileged enables a piece of trusted code to temporarily enable access to more resources than are available directly to the code that called it.")
-   [Reflection](java-se-platform-security-architecture.html#GUID-0E000DED-C900-48BF-BBD0-8FD3599600E1 "The doPrivileged method can be invoked reflectively using the java.lang.reflect.Method.invoke method.")

</div>
<div class="sect3">
[]{#GUID-3747895F-0C78-45D7-9CA9-AEE9A1FDC217}

### Using the doPrivileged API {#JSSEC-GUID-3747895F-0C78-45D7-9CA9-AEE9A1FDC217 .sect3}

<div>
This section describes the doPrivileged API and the use of the
privileged feature.

-   [No Return Value, No Exception
    Thrown](java-se-platform-security-architecture.html#GUID-A8827156-5B0C-4CBD-85C5-4A73B10194B1)
-   [Accessing Local
    Variables](java-se-platform-security-architecture.html#GUID-8661C7DE-C5EE-4D9A-B4C4-257F3EDEFD61 "If you are using a lambda expression or anonymous inner class, then any local variables you access must be final or effectively final.")
-   [Handling
    Exceptions](java-se-platform-security-architecture.html#GUID-FE22FB75-A320-40F3-94D4-87B7E6A0784A "If the action performed in your run method could throw a checked exception (one that must be listed in the throws clause of a method), then you need to use the PrivilegedExceptionAction interface instead of the PrivilegedAction interface.")
-   [Asserting a Subset of
    Privileges](java-se-platform-security-architecture.html#GUID-35DBFA01-FEF4-4382-A5D1-4AD2CA441CDA)
-   [Least
    Privilege](java-se-platform-security-architecture.html#GUID-522F4040-3CDD-4063-8380-94A3B477AD21 "The typical use case of the doPrivileged method is to enable the method that invokes it to perform one or more actions that require permission checks without requiring the callers of the current method to have all the necessary permissions.")
-   [More
    Privilege](java-se-platform-security-architecture.html#GUID-05B5503A-E24A-4E27-A3DE-BFFF73D65D9B "When coding the current method, you want to temporarily extend the permission of the calling method to perform an action.")

</div>
<div class="sect4">
[]{#GUID-A8827156-5B0C-4CBD-85C5-4A73B10194B1}

#### No Return Value, No Exception Thrown {#JSSEC-GUID-A8827156-5B0C-4CBD-85C5-4A73B10194B1 .sect4}

<div>
<div class="section">
If you do not need to return a value from within the
<span class="italic">privileged</span> block, your call to
[`doPrivileged`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/AccessController.html#doPrivileged-java.security.PrivilegedAction-)
can look like [Example
1-1](java-se-platform-security-architecture.html#GUID-A8827156-5B0C-4CBD-85C5-4A73B10194B1__SAMPLECODEFORPRIVILEGEDBLOCK-754E162C).

Note that the invocation of `doPrivileged`{.codeph} with a lambda
expression explicitly casts the lambda expression as of type
`PrivilegedAction<Void>`{.codeph}. Another version of the method
`doPrivileged`{.codeph} exists that takes an object of type
[`PrivilegedExceptionAction`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/PrivilegedExceptionAction.html);
see [Handling
Exceptions](java-se-platform-security-architecture.html#GUID-FE22FB75-A320-40F3-94D4-87B7E6A0784A "If the action performed in your run method could throw a checked exception (one that must be listed in the throws clause of a method), then you need to use the PrivilegedExceptionAction interface instead of the PrivilegedAction interface.").

`PrivilegedAction`{.codeph} is a functional interface with a single
abstract method, named `run`{.codeph}, that returns a value of type
specified by its type parameter.

Note that this example ignores the return value of the `run`{.codeph}
method. Also, depending on what <span class="italic">privileged
code</span> actually consists of, you might have to make some changes
due to the way inner classes work. For example, if
<span class="italic">privileged code</span> throws an exception or
attempts to access local variables, then you will have to make some
changes, which is described later.

Be <span class="italic">very</span> careful in your use of the
<span class="italic">privileged</span> construct, and always remember to
make the privileged code section as small as possible. That is, try to
limit the code within the `run`{.codeph} method to only what needs to be
run with privileges, and do more general things outside the
`run`{.codeph} method. Also note that the call to
`doPrivileged`{.codeph} should be made in the code that wants to enable
its privileges. Do not be tempted to write a utility class that itself
calls `doPrivileged`{.codeph} as that could lead to security holes. You
can write utility classes for `PrivilegedAction`{.codeph} classes
though, as shown in the preceding example. See [Guideline 9-3: Safely
invoke
`java.security.AccessController.doPrivileged`{.codeph}](http://www.oracle.com/technetwork/java/seccodeguide-139067.html#9)
in [Secure Coding Guidelines for the Java Programming
Language](http://www.oracle.com/technetwork/java/seccodeguide-139067.html).

</div>
<!-- class="section" -->

<div class="example" id="GUID-A8827156-5B0C-4CBD-85C5-4A73B10194B1__SAMPLECODEFORPRIVILEGEDBLOCK-754E162C">
Example 1-1 Sample Code for Privileged Block

The following code specifies privileged code three ways:

-   In a class that implements the interface
    [`PrivilegedAction`{.codeph}](https://docs.oracle.com/javase/10/docs/api/java/security/PrivilegedAction.html).

-   In an anonymous class.

-   In a lambda expression.

``` {.codeblock dir="ltr"}
import java.security.*;

public class NoReturnNoException {
    
    class MyAction implements PrivilegedAction<Void> {
        public Void run() {
            // Privileged code goes here, for example:
            System.loadLibrary("awt");
            return null; // nothing to return
        }
    }
    
    public void somemethod() {
           
        MyAction mya = new MyAction();
        
        // Become privileged:
        AccessController.doPrivileged(mya);
       
        // Anonymous class
        AccessController.doPrivileged(new PrivilegedAction<Void>() {
            public Void run() {
                // Privileged code goes here, for example:
                System.loadLibrary("awt");
                return null; // nothing to return
            }
        });
        
        // Lambda expression
        AccessController.doPrivileged((PrivilegedAction<Void>)
            () -> {
                // Privileged code goes here, for example:
                System.loadLibrary("awt");
                return null; // nothing to return
            }
        );
    }
    
    public static void main(String... args) {
        NoReturnNoException myApplication = new NoReturnNoException();
        myApplication.somemethod();
    }
}
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-CDC779A5-567B-4A79-9AD9-6887CD66BA3A}

#### Returning Values {#JSSEC-GUID-CDC779A5-567B-4A79-9AD9-6887CD66BA3A .sect4}

<div>
<div class="section">
If you need to return a value, then you can do something like the
following:

``` {.codeblock dir="ltr"}
System.out.println(
    AccessController.doPrivileged((PrivilegedAction<String>)
        () -> System.getProperty("user.name")
    )
);
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-8661C7DE-C5EE-4D9A-B4C4-257F3EDEFD61}

#### Accessing Local Variables {#JSSEC-GUID-8661C7DE-C5EE-4D9A-B4C4-257F3EDEFD61 .sect4}

<div>
If you are using a lambda expression or anonymous inner class, then any
local variables you access must be `final`{.codeph} or effectively
final.

<div class="section">
For example:

``` {.codeblock dir="ltr"}
String lib = "awt";
AccessController.doPrivileged((PrivilegedAction<Void>)
    () -> {
        System.loadLibrary(lib);
        return null; // nothing to return
    }
); 
   
AccessController.doPrivileged(new PrivilegedAction<Void>() {
    public Object run() {
        System.loadLibrary(lib);
        return null; // nothing to return
    }        
});
```

The variable `lib`{.codeph} is effectively final because its value has
not been modified. For example, suppose you add the following assignment
statement after the declaration of the variable `lib`{.codeph}:

``` {.codeblock dir="ltr"}
lib = "swing";
```

The compiler generates the following errors when it encounters the
invocation `System.loadLibrary`{.codeph} both in the lambda expression
and the anonymous class:

-   `error: local variables referenced from a lambda expression must be final or effectively final`{.codeph}
-   `error: local variables referenced from an inner class must be final or effectively final`{.codeph}

See [Accessing Members of an Enclosing
Class](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html#accessing-members-of-an-enclosing-class)
in [Local
Classes](https://docs.oracle.com/javase/tutorial/java/javaOO/localclasses.html)
for more information.

If there are cases where you cannot make an existing variable
effectively final (because it gets set multiple times), then you can
create a new `final`{.codeph} variable right before invoking the
`doPrivileged`{.codeph} method, and set that variable equal to the other
variable. For example:

``` {.codeblock dir="ltr"}
String lib;
    
// The lib variable gets set multiple times so you can't make it
// effectively final.
  
// Create a final String that you can use inside of the run method
final String fLib = lib;
    
AccessController.doPrivileged((PrivilegedAction<Void>)
    () -> {
        System.loadLibrary(fLib);
        return null; // nothing to return
    }
);
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-FE22FB75-A320-40F3-94D4-87B7E6A0784A}

#### Handling Exceptions {#JSSEC-GUID-FE22FB75-A320-40F3-94D4-87B7E6A0784A .sect4}

<div>
If the action performed in your `run`{.codeph} method could throw a
<span class="italic">checked</span> exception (one that must be listed
in the `throws`{.codeph} clause of a method), then you need to use the
`PrivilegedExceptionAction`{.codeph} interface instead of the
`PrivilegedAction`{.codeph} interface.

<div class="example" id="GUID-FE22FB75-A320-40F3-94D4-87B7E6A0784A__PUBLICVOIDPROCESSSOMEFILETHROWSIOEX-755D68AB">
Example 1-2 Sample for Handling Exceptions

If a checked exception is thrown during execution of the `run`{.codeph}
method, then it is placed in a `PrivilegedActionException`{.codeph}
<span class="italic">wrapper</span> exception that is then thrown and
should be caught by your code, as illustrated in the following example:

``` {.codeblock dir="ltr"}
public void processSomefile() throws IOException {

    try {
        Path path = FileSystems.getDefault().getPath("somefile");
        BufferedReader br = AccessController.doPrivileged(
            (PrivilegedExceptionAction<BufferedReader>)
                () -> Files.newBufferedReader(path)
        );
        // ... read from file and do something
    } catch (PrivilegedActionException e) {
    
        // e.getException() should be an instance of IOException
        // as only checked exceptions will be wrapped in a
        // PrivilegedActionException.
        throw (IOException) e.getException();
    }
}
```

</div>
<!-- class="example" -->

</div>
</div>
<div class="sect4">
[]{#GUID-35DBFA01-FEF4-4382-A5D1-4AD2CA441CDA}

#### Asserting a Subset of Privileges {#JSSEC-GUID-35DBFA01-FEF4-4382-A5D1-4AD2CA441CDA .sect4}

<div>
<div class="section">
As of JDK 8, a variant of
[<span class="apiname">doPrivileged</span>](https://docs.oracle.com/javase/10/docs/api/java/security/AccessController.html#doPrivileged-java.security.PrivilegedAction-java.security.AccessControlContext-java.security.Permission...-)
is available that enables code to assert a subset of its privileges,
without preventing the full traversal of the stack to check for other
permissions. This variant of the `doPrivileged`{.codeph} variant has
three parameters, one of which you use to specify this subset of
privileges. For example, the following excerpt asserts a privilege to
retrieve system properties:

``` {.codeblock dir="ltr"}
// Returns the value of the specified property. All code
// is allowed to read the app.version and app.vendor
// properties.

public String getProperty(final String prop) {
    return AccessController.doPrivileged(
        (PrivilegedAction<String>) () -> System.getProperty(prop),
        null,
        new java.util.PropertyPermission("app.version", "read"),
        new java.util.PropertyPermission("app.vendor", "read")
    );
}
```

The first parameter of this version of `doPrivileged`{.codeph} is of
type `java.security.PrivilegedAction`{.codeph}. In this example, the
first parameter is a lambda expression that implements the functional
interface `PrivilegedAction`{.codeph} whose `run`{.codeph} method
returns the value of the system property specified by the parameter
`prop`{.codeph}.

The second parameter of this version of `doPrivileged`{.codeph} is of
type
[<span class="apiname">AccessControlContext</span>](https://docs.oracle.com/javase/10/docs/api/java/security/AccessControlContext.html).
Sometimes you need to perform an additional security check within a
different context, such as a worker thread. You can obtain an
`AccessControlContext`{.codeph} instance from a particular calling
context with the method `AccessControlContext.getContext`{.codeph}. If
you specify `null`{.codeph} for this parameter (as in this example),
then the invocation of `doPrivileged`{.codeph} does not perform any
additional security checks.

The third parameter of this version of `doPrivileged`{.codeph} is of
type
[<span class="apiname">Permission</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Permission.html)`...`{.codeph},
which is a varargs parameter. This means that you can specify one or
more `Permission`{.codeph} parameters or an array of
`Permission`{.codeph} objects, as in `Permission[]`{.codeph}. In this
example, the invocation of `doPrivileged`{.codeph} can retrieve the
properties `app.version`{.codeph} and `app.vendor`{.codeph}.

You can use this three parameter variant of `doPrivileged`{.codeph} in a
mode of least privilege or a mode of more privilege.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-522F4040-3CDD-4063-8380-94A3B477AD21}

#### Least Privilege {#JSSEC-GUID-522F4040-3CDD-4063-8380-94A3B477AD21 .sect4}

<div>
The typical use case of the `doPrivileged`{.codeph} method is to enable
the method that invokes it to perform one or more actions that require
permission checks without requiring the callers of the current method to
have all the necessary permissions.

<div class="section">
For example, the current method might need to open a file or make a
network request for its own internal implementation purposes.

Before JDK 8, calls to `doPrivileged`{.codeph} methods had only two
parameters. They worked by granting temporary privileges to the calling
method and stopping the normal full traversal of the stack for access
checking when it reached that class, rather than continuing up the call
stack where it might reach a method whose defining class does not have
the required permission. Typically, the class that is calling
`doPrivileged`{.codeph} might have additional permissions that are not
required in that code path and which might also be missing from some
caller classes.

Normally, these extra permissions are not exercised at runtime. Not
elevating them through use of `doPrivileged`{.codeph} helps to block
exploitation of any incorrect code that could perform unintended
actions. This is especially true when the `PrivilegedAction`{.codeph} is
more complex than usual, or when it calls code outside the class or
package boundary that might evolve independently over time.

The three-parameter variant of `doPrivileged`{.codeph} is generally
safer to use because it avoids unnecessarily elevating permissions that
are not intended to be required. However, it executes less efficiently
so simple or performance-critical code paths might choose not to use it.

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect4">
[]{#GUID-05B5503A-E24A-4E27-A3DE-BFFF73D65D9B}

#### More Privilege {#JSSEC-GUID-05B5503A-E24A-4E27-A3DE-BFFF73D65D9B .sect4}

<div>
When coding the current method, you want to temporarily extend the
permission of the calling method to perform an action.

<div class="section">
For example, a framework I/O API might have a general purpose method for
opening files of a particular data format. This API would take a normal
file path parameter and use it to open an underlying
`FileInputStream`{.codeph} using the calling code\'s permissions.
However, this might also allow any caller to open the data files in a
special directory that contains some standard demonstration samples.

The callers of this API could be directly granted a
`FilePermission`{.codeph} for <span class="italic">read</span> access.
However, it might not be convenient or possible for the security policy
of the calling code to be updated. For example, the calling code could
be a sandboxed applet.

One way to implement this is for the code to check the incoming path and
determine if it refers to a file in the special directory. If it does,
then it would call `doPrivileged`{.codeph}, enabling all permissions,
then open the file inside the `PrivilegedAction`{.codeph}. If the file
was not in the special directory, the code would open the file without
using `doPrivileged`{.codeph}.

This technique requires the implementation to carefully handle the
requested file path to determine if it refers to the special shared
directory. The file path must be canonicalized before calling
`doPrivileged`{.codeph} so that any relative path will be processed (and
permission to read the `user.dir`{.codeph} system property will be
checked) prior to determining if the path refers to a file in the
special directory. It must also prevent malicious \"../\" path elements
meant to escape out of the special directory.

A simpler and better implementation would use the variant of
`doPrivileged`{.codeph} with the third parameter. It would pass a
`FilePermission`{.codeph} with <span class="italic">read</span> access
to the special directory as the third parameter. Then any manipulation
of the file would be inside the `PrivilegedAction`{.codeph}. This
implementation is simpler and much less prone to contain a security
flaw.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect3">
[]{#GUID-73F600BE-8098-4613-AD4B-E2DEFB9118D8}

### What It Means to Have Privileged Code {#JSSEC-GUID-73F600BE-8098-4613-AD4B-E2DEFB9118D8 .sect3}

<div>
Marking code as <span class="italic">privileged</span> enables a piece
of trusted code to temporarily enable access to more resources than are
available directly to the code that called it.

The policy for a JDK installation specifies what permissions which types
of system resource accesses -- are allowed for code from specified code
sources. A <span class="italic">code source</span> (of type
[<span class="apiname">CodeSource</span>](https://docs.oracle.com/javase/10/docs/api/java/security/CodeSource.html))
essentially consists of the code location (URL) and a reference to the
certificates containing the public keys corresponding to the private
keys used to sign the code (if it was signed).

The policy is represented by a
[<span class="apiname">Policy</span>](https://docs.oracle.com/javase/10/docs/api/java/security/Policy.html)
object. More specifically, it is represented by a `Policy`{.codeph}
subclass providing an implementation of the abstract methods in the
`Policy`{.codeph} class (which is in the `java.security`{.codeph}
package).

The source location for the policy information used by the
`Policy`{.codeph} object depends on the `Policy`{.codeph}
implementation. The `Policy`{.codeph} reference implementation obtains
its information from policy configuration files. See [Default Policy
Implementation and Policy File
Syntax](permissions-jdk1.html#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D)
for information about the `Policy`{.codeph} reference implementation and
the syntax that must be used in policy files it reads.

A <span class="italic">protection domain</span> encompasses a
`CodeSource`{.codeph} instance and the permissions granted to code from
that `CodeSource`{.codeph}, as determined by the security policy
currently in effect. Thus, classes signed by the same keys and from the
same URL are typically placed in the same domain, and a class belongs to
one and only one protection domain. (However, classes signed by the same
keys and from the same URL but loaded by separate class loader instances
are typically placed in separate domains.) Classes that have the same
permissions but are from different code sources belong to different
domains.

Classes shipped with the JDK run-time image and loaded by the bootstrap
class loader are granted <span class="apiname">AllPermission</span>.
However, classes shipped with the JDK run-time image and loaded by the
platform class loader are granted permissions as specified by the
default policy of the JDK. Each module\'s classes are assigned a unique
protection domain using the <span class="apiname">jrt</span> URL scheme
and may only be granted the permissions necessary for them to function
correctly, and not necessarily
<span class="apiname">AllPermission</span>.

Each applet or application runs in its appropriate domain, determined by
its code source. For an applet (or an application running under a
security manager) to be allowed to perform a secured action (such as
reading or writing a file), the applet or application must be granted
permission for that particular action.

More specifically, whenever a resource access is attempted,
<span class="italic">all</span> code traversed by the execution thread
up to that point must have permission for that resource access,
<span class="italic">unless some code on the thread has been marked as
<span class="bold">privileged</span></span>. That is, suppose that
access control checking occurs in a thread of execution that has a chain
of multiple callers. (Think of this as multiple method calls that
potentially cross the protection domain boundaries.) When the
[<span class="apiname">AccessController.checkPermission</span>](https://docs.oracle.com/javase/10/docs/api/java/security/AccessController.html#checkPermission-java.security.Permission-)
method is invoked by the most recent caller, the basic algorithm for
deciding whether to allow or deny the requested access is as follows: If
the code for any caller in the call chain does not have the requested
permission, then an
[<span class="apiname">AccessControlException</span>](https://docs.oracle.com/javase/10/docs/api/java/security/AccessControlException.html)
is thrown, <span class="italic">unless</span> the following is true: a
caller whose code is granted the said permission has been marked as
<span class="italic">privileged</span>, and all parties subsequently
called by this caller (directly or indirectly) have the said permission.

<div class="infoboxnote" id="GUID-73F600BE-8098-4613-AD4B-E2DEFB9118D8__GUID-955EFB93-C9A2-4A0E-A8C1-BBD7DD42E24E">
Note:

The method `AccessController.checkPermission`{.codeph} is normally
invoked indirectly through invocations of specific
`SecurityManager`{.codeph} methods that begin with the word
`check`{.codeph} such as `checkConnect`{.codeph} or through the method
`SecurityManager.checkPermission`{.codeph}. Normally, these checks only
occur if a `SecurityManager`{.codeph} has been installed; code checked
by the `AccessController.checkPermission`{.codeph} method first checks
if the method `System.getSecurityManager`{.codeph} returns null.

</div>
Marking code as <span class="italic">privileged</span> enables a piece
of trusted code to temporarily enable access to more resources than are
available directly to the code that called it. This is necessary in some
situations. For example, an application might not be allowed direct
access to files that contain fonts, but the system utility to display a
document must obtain those fonts, on behalf of the user. The system
utility must become privileged in order to obtain the fonts.

</div>
</div>
<div class="sect3">
[]{#GUID-0E000DED-C900-48BF-BBD0-8FD3599600E1}

### Reflection {#JSSEC-GUID-0E000DED-C900-48BF-BBD0-8FD3599600E1 .sect3}

<div>
The <span class="apiname">doPrivileged</span> method can be invoked
reflectively using the
<span class="apiname">java.lang.reflect.Method.invoke</span> method.

<div class="section">
One subtlety that must be considered is the interaction of this API with
reflection. The `doPrivileged`{.codeph} method can be invoked
reflectively using the
[<span class="apiname">java.lang.reflect.Method.invoke</span>](https://docs.oracle.com/javase/10/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-)
method. In this case, the privileges granted in privileged mode are not
those of `Method.invoke`{.codeph} but of the non-reflective code that
invoked it. Otherwise, system privileges could erroneously (or
maliciously) be conferred on user code. Note that similar requirements
exist when using reflection in the existing API.

</div>
<!-- class="section" -->

</div>
</div>
</div>
<div class="sect2">
[]{#GUID-426CFCAD-6B98-4190-ADE5-E5A14C135CA2}

Appendix B: Acknowledgments {#JSSEC-GUID-426CFCAD-6B98-4190-ADE5-E5A14C135CA2 .sect2}
---------------------------

<div>
The design and implementation of new security features in Java 2 SDK is
the work of primarily members of the JavaSoft security group. Other
(past and present) members of the JavaSoft community provided invaluable
insight, detailed reviews, and much needed technical assistance.
Significant contributors, in alphabetical order, include but are not
limited to: Gigi Ankeny, Josh Bloch, Satya Dodda, Charlie Lai, Sheng
Liang, Jan Luehe, Marianne Mueller, Jeff Nisewanger, Hemma
Prafullchandra, Roger Riggs, Nakul Saraiya, Bill Shannon, Roland
Schemers, and Vijay Srinivasan.

This work is not possible without strong support from JavaSoft
management (our thanks go to Dick Neiss, Jon Kannegaard, and Alan
Baratz), and the testing and documentation groups (especially Mary
Dageforde). We are grateful for technical guidance from James Gosling,
Graham Hamilton, and Jim Mitchell.

We received numerous suggestions from our corporate partners and
licensees, whom we could not fully list here.

</div>
</div>
<div class="sect2">
[]{#GUID-EAB41908-8991-4660-8F77-511B470A82E1}

Appendix C: References {#JSSEC-GUID-EAB41908-8991-4660-8F77-511B470A82E1 .sect2}
----------------------

<div>
M. Gasser. Building a Secure Computer System. Van Nostrand Reinhold Co.,
New York, 1988.

L. Gong, \"Java Security: Present and Near Future\". IEEE Micro,
17(3):14\--19, May/June 1997.

L. Gong, T.M.A. Lomas, R.M. Needham, and J.H. Saltzer, \"Protecting
Poorly Chosen Secrets from Guessing Attacks\". IEEE Journal on Selected
Areas in Communications, 11(5):648\--656, June, 1993.

J. Gosling, Bill Joy, and Guy Steele. The Java Language Specification.
Addison-Wesley, Menlo Park, California, August 1996.

A.K. Jones. Protection in Programmed Systems. Ph.D. dissertation,
Carnegie-Mellon University, Pittsburgh, PA 15213, June 1973.

B.W. Lampson. Protection. In Proceedings of the 5th Princeton Symposium
on Information Sciences and Systems, Princeton University, March 1971.
Reprinted in ACM Operating Systems Review, 8(1):18\--24, January, 1974.

T. Lindholm and F. Yellin. The Java Virtual Machine Specification.
Addison-Wesley, Menlo Park, California, 1997.

P.G. Neumann. Computer-Related Risks. Addison-Wesley, Menlo Park,
California, 1995.

U.S. General Accounting Office. Information Security: Computer Attacks
at Department of Defense Pose Increasing Risks. Technical Report
GAO/AIMD-96-84, Washington, D.C. 20548, May 1996.

J.H. Saltzer. Protection and the Control of Information Sharing in
Multics. Communications of the ACM, 17(7):388\--402, July 1974.

J.H. Saltzer and M.D. Schroeder. The Protection of Information in
Computer Systems}. Proceedings of the IEEE, 63(9):1278\--1308, September
1975.

M.D. Schroeder. Cooperation of Mutually Suspicious Subsystems in a
Computer Utility. Ph.D. dissertation, Massachusetts Institute of
Technology, Cambridge, MA 02139, September 1972.

W.A. Wulf, R. Levin, and S.P. Harbison. HYDRA/C.mmp \-- An Experimental
Computer System. McGraw-Hill, 1981.

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
| -------- ----------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ------ --            | e | )\                   |
|             [![Previ | L |             <span cl |
| ous](../../dcommon/g | o | ass="icon">Contents< |
| ifs/leftnav.gif)\    | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|       [![Next](../.. | ] | -------------------- |
| /dcommon/gifs/rightn | ( | -------------------- |
| av.gif)\             | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](j | . |                      |
| ava-security-overvie | . |                      |
| w1.htm)   <span clas | / |                      |
| s="icon">Next</span> | d |                      |
| ](java-security-stan | c |                      |
| dard-algorithm-names | o |                      |
| .htm)                | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| -------- ----------- | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ------ --            | s |                      |
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
