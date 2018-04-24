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

  ----------------------------------------------------------- ----------------------------------------------------------------------------------------- --
         [![Previous](../../dcommon/gifs/leftnav.gif)\                               [![Next](../../dcommon/gifs/rightnav.gif)\                         
   <span class="icon">Previous</span>](permissions-jdk1.htm)   <span class="icon">Next</span>](java-cryptography-architecture-jca-reference-guide.htm)  
  ----------------------------------------------------------- ----------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-4F9F7BB5-5C9E-4888-9E28-3017EF746FA0}<!-- End Header -->

Troubleshooting Security {#JSSEC-GUID-4F9F7BB5-5C9E-4888-9E28-3017EF746FA0 .sect1}
========================

<div>
To monitor security access, you can set the
`java.security.debug`{.codeph} system property, which determines what
trace messages are printed during execution.

<div class="section">
To see a list of all debugging options, use the `help`{.codeph} setting:

``` {.oac_no_warn dir="ltr"}
java -Djava.security.debug=help
```

<div class="p">
<div class="infoboxnote" id="GUID-4F9F7BB5-5C9E-4888-9E28-3017EF746FA0__GUID-61F5D702-AA50-493C-B813-C0A0B595D39A">
Note:

To use more than one option, separate options with a comma.

JSSE also provides dynamic debug tracing support for SSL/TLS/DTLS
troubleshooting. See [Debugging
Utilities](java-secure-socket-extension-jsse-reference-guide.htm#GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF).

</div>
</div>
The following table lists `java.security.debug`{.codeph} options and
links to further information about each option:

<div class="tblformal" id="GUID-4F9F7BB5-5C9E-4888-9E28-3017EF746FA0__GUID-90D4A85A-D027-4E85-929F-5A36BB96FA8D">
Table 1-10 `java.security.debug`{.codeph} Options

+-----------------------+-----------------------+-----------------------+
| Option                | Description           | Further Information   |
+:======================+:======================+:======================+
| `all`{.codeph}        | Turn on all the       |  None                 |
|                       | debugging options     |                       |
+-----------------------+-----------------------+-----------------------+
| `access`{.codeph}     | Print all results     | [Permissions in the   |
|                       | from the              | JDK](permissions-jdk1 |
|                       | `AccessController.che | .htm#GUID-1E8E213A-D7 |
|                       | ckPermission`{.codeph | F2-49F1-A2F0-EFB3397A |
|                       | }</a></code>          | 8C95 "A permission re |
|                       | method.               | presents access to a  |
|                       |                       | system resource. In o |
|                       | You can use the       | rder for a resource a |
|                       | following options     | ccess to be allowed f |
|                       | with the              | or an applet (or an a |
|                       | `access`{.codeph}     | pplication running wi |
|                       | option:               | th a security manager |
|                       |                       | ), the corresponding  |
|                       | 1.  `stack`{.codeph}: | permission must be ex |
|                       |     Include stack     | plicitly granted to t |
|                       |     trace             | he code attempting th |
|                       | 2.  `domain`{.codeph} | e access.")           |
|                       | :                     |                       |
|                       |     Dump all domains  |                       |
|                       |     in context        |                       |
|                       | 3.  `failure`{.codeph |                       |
|                       | }:                    |                       |
|                       |     Before throwing   |                       |
|                       |     exception, dump   |                       |
|                       |     stack and domain  |                       |
|                       |     that do not have  |                       |
|                       |     permission        |                       |
|                       |                       |                       |
|                       | You can use the       |                       |
|                       | following options     |                       |
|                       | with the              |                       |
|                       | `stack`{.codeph} and  |                       |
|                       | `domain`{.codeph}     |                       |
|                       | options:              |                       |
|                       |                       |                       |
|                       | 1.  `permission=<clas |                       |
|                       | sname>`{.codeph}:     |                       |
|                       |     Only dump output  |                       |
|                       |     if specified      |                       |
|                       |     permission is     |                       |
|                       |     being checked     |                       |
|                       | 2.  `codebase=<URL>`{ |                       |
|                       | .codeph}:             |                       |
|                       |     Only dump output  |                       |
|                       |     if specified      |                       |
|                       |     codebase is being |                       |
|                       |     checked           |                       |
+-----------------------+-----------------------+-----------------------+
| `certpath`{.codeph}   | Turns on debugging    | [PKI Programmers      |
|                       | for the PKIX          | Guide                 |
|                       | `CertPathValidator`{. | Overview](java-pki-pr |
|                       | codeph}</a></code>    | ogrammers-guide.htm#G |
|                       | and                   | UID-D6A18B1E-A2A8-4CA |
|                       | `CertPathBuilder`{.co | 2-BD18-514CD807810E " |
|                       | deph}</a></code>      | The Java Certificatio |
|                       | implementations. Use  | n Path API defines in |
|                       | the `ocsp`{.codeph}   | terfaces and abstract |
|                       | option with the       |  classes for creating |
|                       | `certpath`{.codeph}   | , building, and valid |
|                       | option for OCSP       | ating certification p |
|                       | protocol tracing. A   | aths.  Implementation |
|                       | hexadecimal dump of   | s may be plugged in u |
|                       | the OCSP request and  | sing a provider-based |
|                       | response bytes is     |  interface.")         |
|                       | displayed.            |                       |
+-----------------------+-----------------------+-----------------------+
| `combiner`{.codeph}   | `SubjectDomainCombine | [Permissions in the   |
|                       | r`{.codeph}</a></code | JDK](permissions-jdk1 |
|                       | >                     | .htm#GUID-1E8E213A-D7 |
|                       | debugging             | F2-49F1-A2F0-EFB3397A |
|                       |                       | 8C95 "A permission re |
|                       |                       | presents access to a  |
|                       |                       | system resource. In o |
|                       |                       | rder for a resource a |
|                       |                       | ccess to be allowed f |
|                       |                       | or an applet (or an a |
|                       |                       | pplication running wi |
|                       |                       | th a security manager |
|                       |                       | ), the corresponding  |
|                       |                       | permission must be ex |
|                       |                       | plicitly granted to t |
|                       |                       | he code attempting th |
|                       |                       | e access.")           |
+-----------------------+-----------------------+-----------------------+
| `configfile`{.codeph} | JAAS (Java            | [Java Authentication  |
|                       | Authentication and    | and Authorization     |
|                       | Authorization         | Service (JAAS)        |
|                       | Service)              | Reference             |
|                       | configuration file    | Guide](https://docs.o |
|                       | loading               | racle.com/javase/8/do |
|                       |                       | cs/technotes/guides/s |
|                       |                       | ecurity/jaas/JAASRefG |
|                       |                       | uide.html)            |
|                       |                       |                       |
|                       |                       | [Use of JAAS Login    |
|                       |                       | Utility and Java      |
|                       |                       | GSS-API for Secure    |
|                       |                       | Message               |
|                       |                       | Exchanges](https://do |
|                       |                       | cs.oracle.com/javase/ |
|                       |                       | 8/docs/technotes/guid |
|                       |                       | es/security/jgss/tuto |
|                       |                       | rials/ClientServer.ht |
|                       |                       | ml)                   |
+-----------------------+-----------------------+-----------------------+
| `configparser`{.codep | JAAS configuration    | [Java Authentication  |
| h}                    | file parsing          | and Authorization     |
|                       |                       | Service (JAAS)        |
|                       |                       | Reference             |
|                       |                       | Guide](https://docs.o |
|                       |                       | racle.com/javase/8/do |
|                       |                       | cs/technotes/guides/s |
|                       |                       | ecurity/jaas/JAASRefG |
|                       |                       | uide.html)            |
|                       |                       |                       |
|                       |                       | [Use of JAAS Login    |
|                       |                       | Utility and Java      |
|                       |                       | GSS-API for Secure    |
|                       |                       | Message               |
|                       |                       | Exchanges](https://do |
|                       |                       | cs.oracle.com/javase/ |
|                       |                       | 8/docs/technotes/guid |
|                       |                       | es/security/jgss/tuto |
|                       |                       | rials/ClientServer.ht |
|                       |                       | ml)                   |
+-----------------------+-----------------------+-----------------------+
| `gssloginconfig`{.cod | Java GSS (Generic     | [Java Generic         |
| eph}                  | Security Services)    | Security Services:    |
|                       | login configuration   | (Java GSS) and        |
|                       | file debugging        | Kerberos](https://doc |
|                       |                       | s.oracle.com/javase/8 |
|                       |                       | /docs/technotes/guide |
|                       |                       | s/security/jgss/jgss- |
|                       |                       | features.html)        |
|                       |                       |                       |
|                       |                       | [JAAS and Java        |
|                       |                       | GSS-API               |
|                       |                       | Tutorial](https://doc |
|                       |                       | s.oracle.com/javase/8 |
|                       |                       | /docs/technotes/guide |
|                       |                       | s/security/jgss/tutor |
|                       |                       | ials/BasicClientServe |
|                       |                       | r.html)               |
|                       |                       |                       |
|                       |                       | `javax.security.auth. |
|                       |                       | login.Configuration`{ |
|                       |                       | .codeph}</a></code>:  |
|                       |                       | A Configuration       |
|                       |                       | object is responsible |
|                       |                       | for specifying which  |
|                       |                       | `javax.net.ssl.SSLEng |
|                       |                       | ine`{.codeph}</a></co |
|                       |                       | de>                   |
|                       |                       | should be used for a  |
|                       |                       | particular            |
|                       |                       | application, and in   |
|                       |                       | what order the        |
|                       |                       | `LoginModules`{.codep |
|                       |                       | h}                    |
|                       |                       | should be invoked.    |
|                       |                       |                       |
|                       |                       | [JAAS Login           |
|                       |                       | Configuration         |
|                       |                       | File](https://docs.or |
|                       |                       | acle.com/javase/8/doc |
|                       |                       | s/technotes/guides/se |
|                       |                       | curity/jgss/tutorials |
|                       |                       | /LoginConfigFile.html |
|                       |                       | )                     |
|                       |                       |                       |
|                       |                       | [Advanced Security    |
|                       |                       | Programming in Java   |
|                       |                       | SE Authentication,    |
|                       |                       | Secure Communication  |
|                       |                       | and Single            |
|                       |                       | Sign-On](https://docs |
|                       |                       | .oracle.com/javase/8/ |
|                       |                       | docs/technotes/guides |
|                       |                       | /security/jgss/lab/)  |
+-----------------------+-----------------------+-----------------------+
| `jar`{.codeph}        | JAR file verification | [Verifying Signed JAR |
|                       |                       | Files](https://docs.o |
|                       |                       | racle.com/javase/tuto |
|                       |                       | rial/deployment/jar/v |
|                       |                       | erify.html)           |
|                       |                       | from The Java         |
|                       |                       | Tutorials             |
+-----------------------+-----------------------+-----------------------+
| `jca`{.codeph}        | JCA engine class      | [Engine Classes and   |
|                       | debugging             | Algorithms](java-cryp |
|                       |                       | tography-architecture |
|                       |                       | -jca-reference-guide. |
|                       |                       | htm#GUID-A7EEDE25-C4C |
|                       |                       | 0-4C28-94EA-262858AE9 |
|                       |                       | 212 "An engine class  |
|                       |                       | provides the interfac |
|                       |                       | e to a specific type  |
|                       |                       | of cryptographic serv |
|                       |                       | ice, independent of a |
|                       |                       |  particular cryptogra |
|                       |                       | phic algorithm or pro |
|                       |                       | vider.")              |
+-----------------------+-----------------------+-----------------------+
| `keystore`{.codeph}   | Keystore debugging    | [Keystores](java-cryp |
|                       |                       | tography-architecture |
|                       |                       | -jca-reference-guide. |
|                       |                       | htm#GUID-C730728A-DB4 |
|                       |                       | B-488F-8171-34FC04BD0 |
|                       |                       | FF1 "A database calle |
|                       |                       | d a "keystore" can be |
|                       |                       |  used to manage a rep |
|                       |                       | ository of keys and c |
|                       |                       | ertificates. Keystore |
|                       |                       | s are available to ap |
|                       |                       | plications that need  |
|                       |                       | data for authenticati |
|                       |                       | on, encryption, or si |
|                       |                       | gning purposes.")     |
|                       |                       |                       |
|                       |                       | [`KeyStore`{.codeph}] |
|                       |                       | (https://docs.oracle. |
|                       |                       | com/javase/10/docs/ap |
|                       |                       | i/java/security/KeySt |
|                       |                       | ore.html)             |
+-----------------------+-----------------------+-----------------------+
| `logincontext`{.codep | `LoginContext`{.codep | [Java Authentication  |
| h}                    | h}</a></code>         | and Authorization     |
|                       | results               | Service (JAAS)        |
|                       |                       | Reference             |
|                       |                       | Guide](https://docs.o |
|                       |                       | racle.com/javase/8/do |
|                       |                       | cs/technotes/guides/s |
|                       |                       | ecurity/jaas/JAASRefG |
|                       |                       | uide.html)            |
|                       |                       |                       |
|                       |                       | [Use of JAAS Login    |
|                       |                       | Utility and Java      |
|                       |                       | GSS-API for Secure    |
|                       |                       | Message               |
|                       |                       | Exchanges](https://do |
|                       |                       | cs.oracle.com/javase/ |
|                       |                       | 8/docs/technotes/guid |
|                       |                       | es/security/jgss/tuto |
|                       |                       | rials/ClientServer.ht |
|                       |                       | ml)                   |
+-----------------------+-----------------------+-----------------------+
| `pkcs11`{.codeph}     | PKCS11 session        | [PKCS\#11 Reference   |
|                       | manager debugging     | Guide](pkcs11-referen |
|                       |                       | ce-guide1.htm#GUID-30 |
|                       |                       | E98B63-4910-40A1-A6DD |
|                       |                       | -663EAF466991)        |
+-----------------------+-----------------------+-----------------------+
| `pkcs11keystore`{.cod | PKCS11 KeyStore       | [PKCS\#11 Reference   |
| eph}                  | debugging             | Guide](pkcs11-referen |
|                       |                       | ce-guide1.htm#GUID-30 |
|                       |                       | E98B63-4910-40A1-A6DD |
|                       |                       | -663EAF466991)        |
+-----------------------+-----------------------+-----------------------+
| `pkcs12`{.codeph}     | PKCS12 KeyStore       | None                  |
|                       | debugging             |                       |
+-----------------------+-----------------------+-----------------------+
| `policy`{.codeph}     | Loading and granting  | [Set up the Policy    |
|                       | permissions with      | File to Grant the     |
|                       | policy file           | Required Permissions  |
|                       |                       | (Controlling          |
|                       |                       | Applications)](https: |
|                       |                       | //docs.oracle.com/jav |
|                       |                       | ase/tutorial/security |
|                       |                       | /tour2/step3.html)    |
|                       |                       | from The Java         |
|                       |                       | Tutorials             |
|                       |                       |                       |
|                       |                       | [Default Policy       |
|                       |                       | Implementation and    |
|                       |                       | Policy File           |
|                       |                       | Syntax](permissions-j |
|                       |                       | dk1.htm#GUID-789089CA |
|                       |                       | -8557-4017-B8B0-6899A |
|                       |                       | D3BA18D)              |
+-----------------------+-----------------------+-----------------------+
| `provider`{.codeph}   | Security provider     | [Java Cryptography    |
|                       | debugging             | Architecture (JCA)    |
|                       |                       | Reference             |
|                       | The following options | Guide](java-cryptogra |
|                       | can be used with the  | phy-architecture-jca- |
|                       | provider option:      | reference-guide.htm#G |
|                       |                       | UID-2BCFDD85-D533-4E6 |
|                       | `engine=<engines>`{.c | C-8CE9-29990DEB0190 " |
|                       | odeph}                | The Java Cryptography |
|                       | : The output is       |  Architecture (JCA) i |
|                       | displayed only for a  | s a major piece of th |
|                       | specified list of JCA | e platform, and conta |
|                       | engines.              | ins a "provider" arch |
|                       |                       | itecture and a set of |
|                       | <div class="p">       |  APIs for digital sig |
|                       | The supported values  | natures, message dige |
|                       | for                   | sts (hashes), certifi |
|                       | <span class="variable | cates and certificate |
|                       | ">\<engines\></span>  |  validation, encrypti |
|                       | are:                  | on (symmetric/asymmet |
|                       |                       | ric block/stream ciph |
|                       | -   Cipher            | ers), key generation  |
|                       |                       | and management, and s |
|                       | -   KeyAgreement      | ecure random number g |
|                       |                       | eneration, to name a  |
|                       | -   KeyGenerator      | few.")                |
|                       |                       |                       |
|                       | -   KeyPairGenerator  |                       |
|                       |                       |                       |
|                       | -   KeyStore          |                       |
|                       |                       |                       |
|                       | -   Mac               |                       |
|                       |                       |                       |
|                       | -   MessageDigest     |                       |
|                       |                       |                       |
|                       | -   SecureRandom      |                       |
|                       |                       |                       |
|                       | -   Signature         |                       |
|                       |                       |                       |
|                       | </div>                |                       |
+-----------------------+-----------------------+-----------------------+
| `scl`{.codeph}        | Permissions that      | [Permissions in the   |
|                       | [`SecureClassLoader`{ | JDK](permissions-jdk1 |
|                       | .codeph}](https://doc | .htm#GUID-1E8E213A-D7 |
|                       | s.oracle.com/javase/1 | F2-49F1-A2F0-EFB3397A |
|                       | 0/docs/api/java/secur | 8C95 "A permission re |
|                       | ity/SecureClassLoader | presents access to a  |
|                       | .html)                | system resource. In o |
|                       | assigns               | rder for a resource a |
|                       |                       | ccess to be allowed f |
|                       |                       | or an applet (or an a |
|                       |                       | pplication running wi |
|                       |                       | th a security manager |
|                       |                       | ), the corresponding  |
|                       |                       | permission must be ex |
|                       |                       | plicitly granted to t |
|                       |                       | he code attempting th |
|                       |                       | e access.")           |
+-----------------------+-----------------------+-----------------------+
| `securerandom`{.codep | SecureRandom          | [The SecureRandom     |
| h}                    | debugging             | Class](java-cryptogra |
|                       |                       | phy-architecture-jca- |
|                       |                       | reference-guide.htm#G |
|                       |                       | UID-AEB77CD8-D28F-4BB |
|                       |                       | E-B9E5-160B5DC35D36)  |
+-----------------------+-----------------------+-----------------------+
| `sunpkcs11`{.codeph}  | SunPKCS11 provider    | [PKCS\#11 Reference   |
|                       | debugging             | Guide](pkcs11-referen |
|                       |                       | ce-guide1.htm#GUID-30 |
|                       |                       | E98B63-4910-40A1-A6DD |
|                       |                       | -663EAF466991)        |
+-----------------------+-----------------------+-----------------------+
| `ts`{.codeph}         | Timestamping          | None                  |
|                       | debugging             |                       |
+-----------------------+-----------------------+-----------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
<!-- class="section" -->

</div>
</div>
<!-- class="ind" --><!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   -- --------------- |
| -------------------- | [ | -------------------- |
| -------------------- | O | -------------------- |
| - ------------------ | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ----------- --       | e | )\                   |
|          [![Previous | L |             <span cl |
| ](../../dcommon/gifs | o | ass="icon">Contents< |
| /leftnav.gif)\       | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|      [![Next](../../ | ] | -------------------- |
| dcommon/gifs/rightna | ( | -------------------- |
| v.gif)\              | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](p | . |                      |
| ermissions-jdk1.htm) | . |                      |
|    <span class="icon | / |                      |
| ">Next</span>](java- | d |                      |
| cryptography-archite | c |                      |
| cture-jca-reference- | o |                      |
| guide.htm)           | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| - ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ----------- --       | s |                      |
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
