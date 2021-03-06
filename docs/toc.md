<div class="header">
[]{#top}

<div class="zz-skip-header">
[Go to primary content](#BEGIN)

</div>
+-----------------------------------+----------------------------------:+
| **Java Platform, Standard Edition |   --                              |
| Security Developer's Guide**\     |   --                              |
| **<span>Release 11</span>**\      |                                   |
| E94828-01                         |                                   |
+-----------------------------------+-----------------------------------+

------------------------------------------------------------------------

  -------------------------------------------- --
   [![Next](../../dcommon/gifs/rightnav.gif)\  
   <span class="icon">Next</span>](title.htm)  
  -------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
<!-- End Header -->

Contents {#contents .toc}
========

[Title and Copyright Information](title.htm) {#title-and-copyright-information .tocheader}
--------------------------------------------

[Preface](preface.html#GUID-C49D47BA-EA16-4F4F-90CE-DAD9B984D823) {#preface .tocheader}
----------------------------------------------------------------

-   [Audience](preface.html#GUID-4E10EE4D-C026-4A83-9270-B63AEB3E96F5)
-   [Documentation
    Accessibility](preface.html#GUID-E409CC44-9A8F-4043-82C8-6B95CD939296)
-   [Related
    Documents](preface.html#GUID-7242A5DD-3D31-416A-BD79-5B49A9CF7583)
-   [Conventions](preface.html#GUID-75D45AA0-5C30-4EB1-8954-FB75E303F2DC)

[<span class="secnum">1</span> General Security](general-security1.htm) {#general-security .tocheader}
-----------------------------------------------------------------------

-   [Java Security
    Overview](java-security-overview1.html#GUID-2EF91196-D468-4D0F-8FDC-DA2BEA165D10)
    -   [Introduction to Java
        Security](java-security-overview1.html#GUID-69EE84E6-E0BD-48B2-B3F2-200D9A5FCF93)
    -   [Java Language Security and Bytecode
        Verification](java-security-overview1.html#GUID-65C96219-B2AB-4205-808E-5B41CB2AD694)
    -   [Basic Security
        Architecture](java-security-overview1.html#GUID-0C458D46-BA4F-4091-817B-9902B6E18240)
        -   [Security
            Providers](java-security-overview1.html#GUID-74E1EFEA-F1DD-466C-B61A-CB5E89FA50DE)
        -   [File
            Locations](java-security-overview1.html#GUID-25BF3893-E577-4C96-9A4A-BEA39555CA72)
    -   [Java
        Cryptography](java-security-overview1.html#GUID-C6D250FC-F147-4284-A6BF-8384DFD39DA6)
    -   [Public Key
        Infrastructure](java-security-overview1.html#GUID-054AD71D-D449-47FF-B6F7-F416DA821D46)
        -   [Key and Certificate
            Storage](java-security-overview1.html#GUID-EB29B931-D1DE-420B-849C-D731A8DF9CDC)
        -   [Public Key Infrastructure
            Tools](java-security-overview1.html#GUID-BC9A5E59-953A-4EBC-9F03-BEF099B64F5B)
    -   [Authentication](java-security-overview1.html#GUID-F8BE6C49-3506-4D1A-8E4E-053CA439D1E2)
    -   [Secure
        Communication](java-security-overview1.html#GUID-4E5FEEF5-A541-4222-AD18-31AE184F38E4)
        -   [SSL, TLS, and DTLS
            Protocols](java-security-overview1.html#GUID-FCF419A7-B856-46DD-A36F-C6F88F9AF37F)
        -   [Simple Authentication and Security Layer
            (SASL)](java-security-overview1.html#GUID-7C74ECA4-3645-4756-B8FB-63D84480F4AD)
        -   [Generic Security Service API and
            Kerberos](java-security-overview1.html#GUID-40739A87-4E28-4195-A156-AFA008CF3B2A)
    -   [Access
        Control](java-security-overview1.html#GUID-BBEC2DC8-BA00-42B1-B52A-A49488FCF8FE)
        -   [Permissions](java-security-overview1.html#GUID-7A49C00B-BEA6-4050-9E32-6168211585F7)
        -   [Security
            Policy](java-security-overview1.html#GUID-5FB6B917-DDFE-42F5-9233-8E6250C1EA93)
        -   [Access Control
            Enforcement](java-security-overview1.html#GUID-2779612B-8DE1-49D3-8EC3-C678C3A9FC35)
    -   [XML
        Signature](java-security-overview1.html#GUID-BFC0C7D7-72B5-4DEC-ACF4-5DF4F7925303)
    -   [Additional Information about Java
        Security](java-security-overview1.html#GUID-49933D9B-83AF-4A3D-94A3-00061A9A212F)
    -   [Java Security Classes
        Summary](java-security-overview1.html#GUID-CF323502-F719-4618-91FE-4D37CB57FF24)
    -   [Deprecated Security APIs Marked for
        Removal](java-security-overview1.html#GUID-E1A1E8ED-B39F-404B-8036-637F697B45A2)
    -   [Security Tools
        Summary](java-security-overview1.html#GUID-86FA42B9-E18B-4E2B-9F2D-7567320B53AA)
    -   [Built-In
        Providers](java-security-overview1.html#GUID-2EF0B3B8-9F3A-41CF-A7DA-63DB52180084)
-   [Java SE Platform Security
    Architecture](java-se-platform-security-architecture.html#GUID-D6C53B30-01F9-49F1-9F61-35815558422B)
    -   [Introduction](java-se-platform-security-architecture.html#GUID-C203D80F-C730-45C3-AB95-D4E61FD6D89C)
        -   [The Original Sandbox
            Model](java-se-platform-security-architecture.html#GUID-CF079719-BCCD-44B5-B637-288D0D28D4F0)
        -   [Evolving the Sandbox
            Model](java-se-platform-security-architecture.html#GUID-C574845A-4D55-4EB1-8D73-326C8B755C2D)
    -   [Protection Mechanisms -- Overview of Basic
        Concepts](java-se-platform-security-architecture.html#GUID-2C2D6A1A-01CA-4C51-9BD4-33E5B1578E00)
    -   [Permissions and Security
        Policy](java-se-platform-security-architecture.html#GUID-EDCA17D5-A2FD-472B-A156-32DD6AE87C42)
        -   [The Permission
            Classes](java-se-platform-security-architecture.html#GUID-DEA8EAB1-CF00-4658-AA6D-D2C9754C8B37)
            -   [java.security.Permission](java-se-platform-security-architecture.html#GUID-1805A836-1DC0-4DBE-88CF-83BEAFD65C76)
            -   [java.security.PermissionCollection](java-se-platform-security-architecture.html#GUID-9EC8B31D-35F4-4414-AE50-64037057D62A)
            -   [java.security.Permissions](java-se-platform-security-architecture.html#GUID-F7F4DA3B-79E5-4306-88AC-791B64DCD350)
            -   [java.security.UnresolvedPermission](java-se-platform-security-architecture.html#GUID-05F504BC-6075-4CC2-A573-67F4B6AC96AC)
            -   [java.io.FilePermission](java-se-platform-security-architecture.html#GUID-FDEB3FEC-9DA9-4524-8B3D-E3D559F5C504)
            -   [java.net.SocketPermission](java-se-platform-security-architecture.html#GUID-1C00ACB3-88F6-4A8E-85D8-9AF7CB46D812)
            -   [java.security.BasicPermission](java-se-platform-security-architecture.html#GUID-BCC9A9CD-AB9C-42C5-9294-E0A593770F4C)
            -   [java.util.PropertyPermission](java-se-platform-security-architecture.html#GUID-D10A4043-110B-4E92-BAC0-4654E20E01D0)
            -   [java.lang.RuntimePermission](java-se-platform-security-architecture.html#GUID-744ACFDF-6ED1-473D-9D3A-5F34541A4377)
            -   [java.awt.AWTPermission](java-se-platform-security-architecture.html#GUID-D5BF900D-436B-4DB0-A855-FBAAF20D89FA)
            -   [java.net.NetPermission](java-se-platform-security-architecture.html#GUID-0DBB6926-DA1E-491F-8E23-D0712AC13CCB)
            -   [java.lang.reflect.ReflectPermission](java-se-platform-security-architecture.html#GUID-B5B444DD-0DED-4023-A0CB-BE2988CBA2DB)
            -   [java.io.SerializablePermission](java-se-platform-security-architecture.html#GUID-372E6279-A298-4399-BD86-CF094FCD7FC3)
            -   [java.security.SecurityPermission](java-se-platform-security-architecture.html#GUID-5F524238-B23D-4A58-8733-330EE6946AC4)
            -   [java.security.AllPermission](java-se-platform-security-architecture.html#GUID-51FC4F94-2A29-4B3A-88CB-7AF4C9A5BA59)
            -   [javax.security.auth.AuthPermission](java-se-platform-security-architecture.html#GUID-07D4DF51-7CFB-4DDA-BFC8-DF3B06BC5011)
            -   [Discussion of Permission
                Implications](java-se-platform-security-architecture.html#GUID-693DDD12-F742-4C65-8578-04B4F4CB26A1)
            -   [How To Create New Types of
                Permissions](java-se-platform-security-architecture.html#GUID-F9498F7F-365E-46D5-8B39-2FDCEB7D9E8C)
        -   [java.security.CodeSource](java-se-platform-security-architecture.html#GUID-B1EE1A73-CF14-40CB-A524-F76600BC9DF0)
        -   [java.security.Policy](java-se-platform-security-architecture.html#GUID-93B94FD3-599F-4C9F-9479-7EDC34B05D65)
            -   [Policy File
                Format](java-se-platform-security-architecture.html#GUID-F5270083-CCAC-49E0-ACAC-50176FBFDD97)
            -   [Property Expansion in Policy
                Files](java-se-platform-security-architecture.html#GUID-D21747DB-EA50-420E-9D8F-C72F34F5FCA5)
            -   [General Expansion in Policy
                Files](java-se-platform-security-architecture.html#GUID-17F2CE51-A2C7-48DF-98B9-3C7F4970A084)
            -   [Assigning
                Permissions](java-se-platform-security-architecture.html#GUID-938D6987-F1B0-4894-8348-EED3AD4B55FE)
            -   [Default System and User Policy
                Files](java-se-platform-security-architecture.html#GUID-6A3C0484-51D2-4818-8488-AF7CA523EA4A)
            -   [Customizing Policy
                Evaluation](java-se-platform-security-architecture.html#GUID-DD5954DB-DE02-4121-971A-2AAF56D90F2B)
        -   [java.security.GeneralSecurityException](java-se-platform-security-architecture.html#GUID-6F218913-E967-40AA-A756-3D41FE0D12A2)
    -   [Access Control Mechanisms and
        Algorithms](java-se-platform-security-architecture.html#GUID-3067791D-ABC6-480E-8E6F-6578F9FFC25D)
        -   [java.security.ProtectionDomain](java-se-platform-security-architecture.html#GUID-650F5B1E-287D-4DAD-B111-D26E012147C1)
        -   [java.security.AccessController](java-se-platform-security-architecture.html#GUID-C3873E27-A5E4-4F6A-BB56-A0AB3EC5684F)
            -   [Algorithm for Checking
                Permissions](java-se-platform-security-architecture.html#GUID-9C3AC8FE-C4E6-41EC-A96C-827C5A23D51A)
            -   [Handling
                Privileges](java-se-platform-security-architecture.html#GUID-E8898CB5-65BB-4D1A-A574-8F7112FC353F)
        -   [Inheritance of Access Control
            Context](java-se-platform-security-architecture.html#GUID-734D48E4-81FB-4EFF-9459-AEAD30DA3408)
        -   [java.security.AccessControlContext](java-se-platform-security-architecture.html#GUID-046F1EA2-133F-4D9B-9EF2-EB21FBB3C5E9)
    -   [Secure Class
        Loading](java-se-platform-security-architecture.html#GUID-C4FA75FE-B65C-4D8E-B608-D21A8D769A7D)
        -   [Class Loader Class
            Hierarchies](java-se-platform-security-architecture.html#GUID-221C1C24-AC48-45D4-B6BF-B31F8ACAFA04)
        -   [The Primordial Class
            Loader](java-se-platform-security-architecture.html#GUID-24372B10-3942-4084-803F-8E5CD7F1B72C)
        -   [Class Loader
            Delegation](java-se-platform-security-architecture.html#GUID-AEABE469-63AF-4041-B0F4-A283971DCFD6)
        -   [Class Resolution
            Algorithm](java-se-platform-security-architecture.html#GUID-044B4753-FEC7-4B9F-AD73-EE8EBAC66D21)
    -   [Security
        Management](java-se-platform-security-architecture.html#GUID-36A4FAF4-B31B-4BF1-A030-51E9555FE349)
        -   [Managing Applets and
            Applications](java-se-platform-security-architecture.html#GUID-DE9A9E41-E735-4624-A015-A22D6C7E75DA)
        -   [SecurityManager versus
            AccessController](java-se-platform-security-architecture.html#GUID-B83ECC0C-02AB-497A-B07D-D74AB9572DC7)
        -   [Auxiliary
            Tools](java-se-platform-security-architecture.html#GUID-1EE99075-F7E3-4EF6-988F-C7C0817508B9)
            -   [The Key and Certificate Management
                Tool](java-se-platform-security-architecture.html#GUID-491B4412-CD5A-4D06-AB51-88AF8E30D42B)
            -   [The JAR Signing and Verification
                Tool](java-se-platform-security-architecture.html#GUID-7D6D44B5-8BC7-48DB-B0D3-A9E824522AC6)
    -   [GuardedObject and
        SignedObject](java-se-platform-security-architecture.html#GUID-032A4F7C-C654-45A7-8931-9E7385BEFCB1)
        -   [java.security.GuardedObject and
            java.security.Guard](java-se-platform-security-architecture.html#GUID-2D31C55D-F676-4993-B159-CE27A336509C)
        -   [java.security.SignedObject](java-se-platform-security-architecture.html#GUID-1BE94E77-1A54-4A0E-BCD1-6E395A576A78)
    -   [Discussion and Future
        Directions](java-se-platform-security-architecture.html#GUID-2AB14B2B-AEDD-413D-B3AF-22F58BE10F34)
        -   [Resource Consumption
            Management](java-se-platform-security-architecture.html#GUID-9B24696B-B2A9-428E-8017-BE4A1952DFBF)
        -   [Arbitrary Grouping of
            Permissions](java-se-platform-security-architecture.html#GUID-489C2508-06FA-420D-B7AF-5E993C263AE8)
        -   [Object-Level
            Protection](java-se-platform-security-architecture.html#GUID-9F0CA451-E717-400C-BC46-7CACD6640F97)
        -   [Subdividing Protection
            Domains](java-se-platform-security-architecture.html#GUID-212090BE-D62C-4E0E-8D61-5F4A05EDFE82)
        -   [Running Applets with Signed
            Content](java-se-platform-security-architecture.html#GUID-4D698AAC-212D-40F6-A1EF-343598D550BB)
    -   [Appendix A: API for Privileged
        Blocks](java-se-platform-security-architecture.html#GUID-BB3C8FB3-1A1A-47F3-8536-3952B84F46F2)
        -   [Using the doPrivileged
            API](java-se-platform-security-architecture.html#GUID-3747895F-0C78-45D7-9CA9-AEE9A1FDC217)
            -   [No Return Value, No Exception
                Thrown](java-se-platform-security-architecture.html#GUID-A8827156-5B0C-4CBD-85C5-4A73B10194B1)
            -   [Returning
                Values](java-se-platform-security-architecture.html#GUID-CDC779A5-567B-4A79-9AD9-6887CD66BA3A)
            -   [Accessing Local
                Variables](java-se-platform-security-architecture.html#GUID-8661C7DE-C5EE-4D9A-B4C4-257F3EDEFD61)
            -   [Handling
                Exceptions](java-se-platform-security-architecture.html#GUID-FE22FB75-A320-40F3-94D4-87B7E6A0784A)
            -   [Asserting a Subset of
                Privileges](java-se-platform-security-architecture.html#GUID-35DBFA01-FEF4-4382-A5D1-4AD2CA441CDA)
            -   [Least
                Privilege](java-se-platform-security-architecture.html#GUID-522F4040-3CDD-4063-8380-94A3B477AD21)
            -   [More
                Privilege](java-se-platform-security-architecture.html#GUID-05B5503A-E24A-4E27-A3DE-BFFF73D65D9B)
        -   [What It Means to Have Privileged
            Code](java-se-platform-security-architecture.html#GUID-73F600BE-8098-4613-AD4B-E2DEFB9118D8)
        -   [Reflection](java-se-platform-security-architecture.html#GUID-0E000DED-C900-48BF-BBD0-8FD3599600E1)
    -   [Appendix B:
        Acknowledgments](java-se-platform-security-architecture.html#GUID-426CFCAD-6B98-4190-ADE5-E5A14C135CA2)
    -   [Appendix C:
        References](java-se-platform-security-architecture.html#GUID-EAB41908-8991-4660-8F77-511B470A82E1)
-   [Standard Algorithm
    Names](java-security-standard-algorithm-names.htm)
-   [Permissions in the
    JDK](permissions-jdk1.html#GUID-1E8E213A-D7F2-49F1-A2F0-EFB3397A8C95)
    -   [Permission Descriptions and
        Risks](permissions-jdk1.html#GUID-8D0E8306-0DD8-4802-A71E-CFEE9BF8A287)
        -   [Methods and the Permissions They
            Require](permissions-jdk1.html#GUID-8B521D4F-1502-42EA-BA70-8E3322A163B5)
        -   [java.lang.SecurityManager Method Permission
            Checks](permissions-jdk1.html#GUID-7423481B-527F-4F15-AF01-992D63521D2E)
    -   [Default Policy Implementation and Policy File
        Syntax](permissions-jdk1.html#GUID-789089CA-8557-4017-B8B0-6899AD3BA18D)
        -   [Default Policy
            Implementation](permissions-jdk1.html#GUID-233A73E2-33C6-4DD0-9EA9-8921ADF40358)
        -   [Default Policy File
            Locations](permissions-jdk1.html#GUID-BFF84712-05CF-4C1E-926F-411FDF83AE32)
        -   [Modifying the Policy
            Implementation](permissions-jdk1.html#GUID-75C71299-8B56-4AC9-A83F-41BC14535545)
        -   [Policy File
            Syntax](permissions-jdk1.html#GUID-7942E6F8-8AAB-4404-9FE9-E08DD6FFCFFA)
            -   [Keystore
                Entry](permissions-jdk1.html#GUID-97EFF17D-2BD7-45E5-AA80-AF1F000B6B83)
            -   [Grant
                Entries](permissions-jdk1.html#GUID-6E1C0535-58D9-443E-9361-6C9BABB0DCD0)
            -   [The SignedBy, Principal, and CodeBase
                Fields](permissions-jdk1.html#GUID-7450CEFD-8EDC-495E-A7A3-6C2561FA4999)
            -   [KeyStore Alias
                Replacement](permissions-jdk1.html#GUID-2636C14A-A783-447A-BE7F-3BF031076117)
            -   [The Permission
                Entries](permissions-jdk1.html#GUID-696D4901-33DD-434E-9C25-09EC5AB4D3AB)
            -   [File Path Specifications on Windows
                Systems](permissions-jdk1.html#GUID-9A8CEB0F-E717-4DAB-91B6-726A79BE4EEB)
        -   [Policy File
            Examples](permissions-jdk1.html#GUID-CE19E4A6-897A-47E1-B6AB-3E49327F7364)
        -   [Property Expansion in Policy
            Files](permissions-jdk1.html#GUID-B614FBFF-0C3C-42F3-B766-DE709CA4D73A)
        -   [Windows Systems, File Paths, and Property
            Expansion](permissions-jdk1.html#GUID-6DB03078-DAD5-4A2C-9DF9-58A8F2FA802C)
        -   [General Expansion in Policy
            Files](permissions-jdk1.html#GUID-6ACBD24A-F4B8-4B32-BAA4-949199273BE5)
    -   [Appendix A: FilePermission Path Name Canonicalization Disabled
        By
        Default](permissions-jdk1.html#GUID-83063225-0ACB-4909-9BAB-7F7D4E3749E2)
-   [Troubleshooting Security](troubleshooting-security.htm)

[<span class="secnum">2</span> Java Cryptography Architecture (JCA) Reference Guide](java-cryptography-architecture-jca-reference-guide.html#GUID-2BCFDD85-D533-4E6C-8CE9-29990DEB0190) {#java-cryptography-architecture-jca-reference-guide .tocheader}
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   [Introduction to Java Cryptography
    Architecture](java-cryptography-architecture-jca-reference-guide.html#GUID-815542FE-CF3D-407A-9673-CAE9840F6231)
    -   [JCA Design
        Principles](java-cryptography-architecture-jca-reference-guide.html#GUID-71693272-7F57-4155-99F9-A2139271FD6D)
    -   [Provider
        Architecture](java-cryptography-architecture-jca-reference-guide.html#GUID-EAB9FF73-4C69-4FD5-8A0C-5CF48211A859)
        -   [Cryptographic Service
            Providers](java-cryptography-architecture-jca-reference-guide.html#GUID-3E0744CE-6AC7-4A6D-A1F6-6C01199E6920)
        -   [How Providers Are Actually
            Implemented](java-cryptography-architecture-jca-reference-guide.html#GUID-FD5163BD-E113-4B9D-A230-11184A668616)
        -   [Keystores](java-cryptography-architecture-jca-reference-guide.html#GUID-C730728A-DB4B-488F-8171-34FC04BD0FF1)
    -   [Engine Classes and
        Algorithms](java-cryptography-architecture-jca-reference-guide.html#GUID-A7EEDE25-C4C0-4C28-94EA-262858AE9212)
-   [Core Classes and
    Interfaces](java-cryptography-architecture-jca-reference-guide.html#GUID-5C9A28FC-8B6B-45BA-8A71-6BEEA34EC27F)
    -   [The Provider
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-D8E30FE5-66B4-4F6A-88B7-280789E68307)
        -   [How Provider Implementations Are Requested and
            Supplied](java-cryptography-architecture-jca-reference-guide.html#GUID-2DCBD20D-2D5E-4ECA-81A8-1FCE9E961741)
        -   [Installing
            Providers](java-cryptography-architecture-jca-reference-guide.html#GUID-E28AC9F2-CBD7-49FC-85B8-5011A94D9007)
        -   [Provider Class
            Methods](java-cryptography-architecture-jca-reference-guide.html#GUID-F8089178-4CDC-4947-A118-7D02ED3EDFD8)
    -   [The Security
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-DE597505-1B42-4AE3-AE2D-45F9123138FA)
        -   [Managing
            Providers](java-cryptography-architecture-jca-reference-guide.html#GUID-F6337AB7-D5A0-4AEC-B026-20E885D41E90)
        -   [Security
            Properties](java-cryptography-architecture-jca-reference-guide.html#GUID-BC5C75FC-DCF7-4E57-874C-42F7EDA8FF1E)
    -   [The SecureRandom
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-AEB77CD8-D28F-4BBE-B9E5-160B5DC35D36)
        -   [Creating a SecureRandom
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-5E53C490-C1B5-4862-A32F-EAD6ADC0AE35)
        -   [Seeding or Re-Seeding the SecureRandom
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-4E42B9E7-FF0B-4FD6-B67A-44F28F943BA8)
        -   [Using a SecureRandom
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-2FCAEC55-8FB5-4FCD-9826-38ABA0AF26DD)
        -   [Generating Seed
            Bytes](java-cryptography-architecture-jca-reference-guide.html#GUID-B85818A1-2AAD-449C-BFB9-EC9146C1B340)
    -   [The MessageDigest
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-FB0090CA-2BCC-4D2C-BD2F-6F0A97197BD7)
        -   [Creating a MessageDigest
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-2F162F9E-8A5F-4586-8E3A-CEF37ECD5E2A)
        -   [Updating a Message Digest
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-72106C04-D90A-4CB8-B320-1F4F864221DC)
        -   [Computing the
            Digest](java-cryptography-architecture-jca-reference-guide.html#GUID-616B5D4B-F334-46B4-9969-6CB4ADF29789)
    -   [The Signature
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-9CF09CE2-9443-4F4E-8095-5CBFC7B697CF)
        -   [Signature Object
            States](java-cryptography-architecture-jca-reference-guide.html#GUID-3586E054-8F23-4D2B-BEA4-47635DAB4EEE)
        -   [Creating a Signature
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-1240FDC5-818E-4067-9C3C-D9635DF7D8A6)
        -   [Initializing a Signature
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-B3C371AB-A447-4F28-9C6E-1349FAC889E6)
        -   [Signing with a Signature
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-93D13151-06F6-4BEA-8F83-074CDB5809DA)
        -   [Verifying with a Signature
            Object](java-cryptography-architecture-jca-reference-guide.html#GUID-1B8AD667-3717-4D9E-B92E-322CFF8C832A)
    -   [The Cipher
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-94225C88-F2F1-44D1-A781-1DD9D5094566)
    -   [Other Cipher-based
        Classes](java-cryptography-architecture-jca-reference-guide.html#GUID-F64C7E9B-12B4-4BFA-A4E7-B2877400C836)
        -   [The Cipher Stream
            Classes](java-cryptography-architecture-jca-reference-guide.html#GUID-C0283BC0-8B88-480D-82B1-7B01EAC3D8DF)
        -   [The SealedObject
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-33BA4D9F-5253-4A53-81C1-38569E8FFCA8)
    -   [The Mac
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-8E014689-EBBB-4DE1-B6E0-24CE59AD8B9A)
    -   [Key
        Interfaces](java-cryptography-architecture-jca-reference-guide.html#GUID-BD91C9BC-CFC6-4125-B46F-772C638FA5DC)
    -   [The KeyPair
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-9A793484-AE6A-4513-A603-BFEAE887DD8B)
    -   [Key Specification Interfaces and
        Classes](java-cryptography-architecture-jca-reference-guide.html#GUID-D1EA35A1-710A-4EBC-8ABB-10875411EBB0)
        -   [The KeySpec
            Interface](java-cryptography-architecture-jca-reference-guide.html#GUID-CFF50556-89F9-4AB0-9EDE-D5763B900BFF)
        -   [The KeySpec
            Subinterfaces](java-cryptography-architecture-jca-reference-guide.html#GUID-5DE3B786-8E76-4679-B66B-6B3EC098075E)
        -   [The EncodedKeySpec
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-8EAA36B1-5CD8-40FC-944E-099C71E716B4)
            -   [The PKCS8EncodedKeySpec
                Class](java-cryptography-architecture-jca-reference-guide.html#GUID-7E6373D0-273A-4C5C-B3EB-14ABBE6B759E)
            -   [The X509EncodedKeySpec
                Class](java-cryptography-architecture-jca-reference-guide.html#GUID-F41053CD-D1F3-4BAE-B97D-72C53A9892DC)
    -   [Generators and
        Factories](java-cryptography-architecture-jca-reference-guide.html#GUID-D4A4B706-6C4F-436D-B5ED-A29C98260578)
        -   [The KeyFactory
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-09C8DF67-7C78-453C-95B4-E7E7DEAD446A)
        -   [The SecretKeyFactory
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-5E8F4099-779F-4484-9A95-F1CEA167601A)
        -   [The KeyPairGenerator
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-7EA29AC2-28B5-405D-BD2F-7055EC9E1EDD)
        -   [The KeyGenerator
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-F178CBC3-D25F-48B6-9F2F-ABB586E713A1)
    -   [The KeyAgreement
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-C4D8A5D0-ECA7-4686-A8F0-636115500C31)
    -   [Key
        Management](java-cryptography-architecture-jca-reference-guide.html#GUID-AB51DEFD-5238-4F96-967F-082F6D34FBEA)
        -   [The KeyStore
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-09050137-31F1-468A-A552-B051A4E35876)
    -   [Algorithm Parameters
        Classes](java-cryptography-architecture-jca-reference-guide.html#GUID-33407B4E-D819-4294-94AB-C6FABF96A93D)
        -   [The AlgorithmParameterSpec
            Interface](java-cryptography-architecture-jca-reference-guide.html#GUID-190C91B4-991D-416E-A932-C0E37B33A86D)
        -   [The AlgorithmParameters
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-EF3A257D-5489-472A-8297-7E9952A5AAB0)
        -   [The AlgorithmParameterGenerator
            Class](java-cryptography-architecture-jca-reference-guide.html#GUID-921D1B8C-5A16-403E-B3A6-D9C6EC684D1C)
    -   [The CertificateFactory
        Class](java-cryptography-architecture-jca-reference-guide.html#GUID-9A581FBA-EDF7-4BCA-8244-4CE2C75E4CEA)
-   [How the JCA Might Be Used in a SSL/TLS
    Implementation](java-cryptography-architecture-jca-reference-guide.html#GUID-C9C9DD6C-3A6B-4759-B41E-AAAC502C0229)
-   [Cryptographic Strength
    Configuration](java-cryptography-architecture-jca-reference-guide.html#GUID-EFA5AC2D-644E-4CD9-8523-C6D3936D5FB1)
-   [Jurisdiction Policy File
    Format](java-cryptography-architecture-jca-reference-guide.html#GUID-F2CF205E-744E-4C16-B504-B6F79781E762)
-   [How to Make Applications Exempt from Cryptographic
    Restrictions](java-cryptography-architecture-jca-reference-guide.html#GUID-B74786B8-A0AD-4DC3-8A2D-2EF41084CE3D)
-   [Standard
    Names](java-cryptography-architecture-jca-reference-guide.html#GUID-6EA080B2-D6B3-4FAD-8369-2170756E0469)
-   [Packaging Your
    Application](java-cryptography-architecture-jca-reference-guide.html#GUID-4FE9F3DF-5D49-44F6-8F28-7541114D520C)
-   [Additional JCA Code
    Samples](java-cryptography-architecture-jca-reference-guide.html#GUID-871FA938-5110-409E-A4EC-16F2A898093A)
    -   [Computing a MessageDigest
        Object](java-cryptography-architecture-jca-reference-guide.html#GUID-6E9FB890-F011-450E-9EC5-EBB358E1D8A1)
    -   [Generating a Pair of
        Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-ED6EDA78-8D20-4059-92E1-FBDDE4D3DFE6)
    -   [Generating and Verifying a Signature Using Generated
        Keys](java-cryptography-architecture-jca-reference-guide.html#GUID-7389E94B-A595-4020-A4D2-73FB0DD5A05A)
    -   [Generating/Verifying Signatures Using Key Specifications and
        KeyFactory](java-cryptography-architecture-jca-reference-guide.html#GUID-5514BAFF-5F0F-403C-9943-56A632D6E406)
    -   [Generating Random
        Numbers](java-cryptography-architecture-jca-reference-guide.html#GUID-36893ED5-E3CA-496B-BC78-B13EE971C736)
    -   [Determining If Two Keys Are
        Equal](java-cryptography-architecture-jca-reference-guide.html#GUID-F7F401C9-63E6-4BE4-9F32-A28B3568EBCC)
    -   [Reading Base64-Encoded
        Certificates](java-cryptography-architecture-jca-reference-guide.html#GUID-CD24C31B-45FA-480C-AFCA-C108C01689D8)
    -   [Parsing a Certificate
        Reply](java-cryptography-architecture-jca-reference-guide.html#GUID-8001F1B9-7DBF-4135-A5F3-0042F803E58A)
    -   [Using
        Encryption](java-cryptography-architecture-jca-reference-guide.html#GUID-AA678E6B-7EAB-44F3-A8CD-F59BEA201BBF)
    -   [Using Password-Based
        Encryption](java-cryptography-architecture-jca-reference-guide.html#GUID-C9F76AFB-6B20-45A7-B84F-96756C8A94B4)
-   [Sample Programs for Diffie-Hellman Key Exchange, AES/GCM, and
    HMAC-SHA256](java-cryptography-architecture-jca-reference-guide.html#GUID-725B837C-9DB3-4B9F-A8D8-1E1C72B558E0)
    -   [Diffie-Hellman Key Exchange between 2
        Parties](java-cryptography-architecture-jca-reference-guide.html#GUID-98B5A57E-E5BA-46F2-BE35-2056F43C58A4)
    -   [Diffie-Hellman Key Exchange between 3
        Parties](java-cryptography-architecture-jca-reference-guide.html#GUID-3DADAE4E-EBC1-46CE-A47B-A09AD9E2A01E)
    -   [AES/GCM
        Example](java-cryptography-architecture-jca-reference-guide.html#GUID-BCF9A664-EA76-49C9-AB0C-662FD7542B85)
    -   [HMAC-SHA256
        Example](java-cryptography-architecture-jca-reference-guide.html#GUID-1B141C6A-7BB3-4DA2-A112-ADEBCE7F4B4A)

[<span class="secnum">3</span> How to Implement a Provider in the Java Cryptography Architecture](howtoimplaprovider.html#GUID-C485394F-08C9-4D35-A245-1B82CDDBC031) {#how-to-implement-a-provider-in-the-java-cryptography-architecture .tocheader}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   [Who Should Read This
    Document](howtoimplaprovider.html#GUID-75AFEAAB-BDEE-4857-9637-9D72D6C42DED)
-   [Notes on
    Terminology](howtoimplaprovider.html#GUID-2D03228D-7B79-44F8-9D24-A3DCF71B12E4)
-   [Introduction to Implementing
    Providers](howtoimplaprovider.html#GUID-42A646A7-E42A-4DA4-A84E-F4862510E3E8)
-   [Engine Classes and Corresponding Service Provider Interface
    Classes](howtoimplaprovider.html#GUID-B35E3749-0A12-42C3-BA0B-C444D7E140BB)
-   [Steps to Implement and Integrate a
    Provider](howtoimplaprovider.html#GUID-CC161921-EBD2-48C6-B543-A956658B68B6)
    -   [Step 1: Write your Service Implementation
        Code](howtoimplaprovider.html#GUID-1D2FDA77-743C-47CB-9CCB-2585FEC0607A)
        -   [Step 1.1: Consider Additional JCA Provider Requirements and
            Recommendations for Encryption
            Implementations](howtoimplaprovider.html#GUID-AEE5234F-24F1-4899-B490-C79F0C2D8D59)
    -   [Step 2: Give your Provider a
        Name](howtoimplaprovider.html#GUID-7241AB0C-71DC-408C-8726-B8E0225DDBCE)
    -   [Step 3: Write Your Master Class, a Subclass of
        Provider](howtoimplaprovider.html#GUID-1C82EDB9-96CA-44AB-8590-E299814D6A46)
        -   [Step 3.1: Create a Provider That Uses String Objects to
            Register Its
            Services](howtoimplaprovider.html#GUID-AB9C2460-0CF2-48BA-B9FE-7059071344CE)
        -   [Step 3.2: Create a Provider That Uses
            Provider.Service](howtoimplaprovider.html#GUID-CB446B7A-CEA2-4F4A-A4AF-4D492CB58733)
        -   [Step 3.3: Specify Additional Information for Cipher
            Implementations](howtoimplaprovider.html#GUID-E1800256-2F1C-471D-96B5-A39ABA751461)
    -   [Step 4: Create a Module Declaration for Your
        Provider](howtoimplaprovider.html#GUID-7C304A79-6D0B-438B-A02E-51648C909876)
    -   [Step 5: Compile Your
        Code](howtoimplaprovider.html#GUID-83742677-6E39-4A8D-BF0F-BC743E3AE43C)
    -   [Step 6: Place Your Provider in a JAR
        File](howtoimplaprovider.html#GUID-B30F5AA2-6517-4107-9FFF-F6BBE57A7A5F)
    -   [Step 7: Sign Your JAR File, If
        Necessary](howtoimplaprovider.html#GUID-2D4432F9-1C3C-4A91-8612-2B2840188B36)
        -   [Step 7.1: Get a Code-Signing
            Certificate](howtoimplaprovider.html#GUID-434AACF7-0D2C-494A-B32A-508A6B605F62)
        -   [Step 7.2: Sign Your
            Provider](howtoimplaprovider.html#GUID-CF5F0E7D-BA0E-494C-8A5A-B228FF839AEF)
    -   [Step 8: Prepare for
        Testing](howtoimplaprovider.html#GUID-FB9C6DB2-DE9A-4EFE-89B4-C2C168C5982D)
        -   [Step 8.1: Configure the
            Provider](howtoimplaprovider.html#GUID-831AA25F-F702-442D-A2E4-8DA6DEA16F33)
        -   [Step 8.2: Set Provider
            Permissions](howtoimplaprovider.html#GUID-6E267101-15F4-4E7B-A6EB-64E36AAD1285)
    -   [Step 9: Write and Compile Your Test
        Programs](howtoimplaprovider.html#GUID-C6054169-FE6E-4837-B2BD-382DFEB955C0)
    -   [Step 10: Run Your Test
        Programs](howtoimplaprovider.html#GUID-3FD26072-6982-4DCE-932C-DE152C463992)
    -   [Step 11: Apply for U.S. Government Export Approval If
        Required](howtoimplaprovider.html#GUID-A62916EE-BE09-4229-9D05-3D6AF303CA4E)
    -   [Step 12: Document Your Provider and Its Supported
        Services](howtoimplaprovider.html#GUID-912FAB1D-628A-47EA-A1DD-A216F2DD4245)
        -   [Step 12.1: Indicate Whether Your Implementation is
            Cloneable for Message Digests and
            MACs](howtoimplaprovider.html#GUID-CC2277C4-14EA-45A8-BC81-8A0715FDC8E9)
    -   [Step 13: Make Your Class Files and Documentation Available to
        Clients](howtoimplaprovider.html#GUID-3521E2A8-93B5-4D0F-AE2D-DC1B5E6857B7)
-   [Further Implementation Details and
    Requirements](howtoimplaprovider.html#GUID-C8B79D46-6EA9-4E27-8083-7CB967732BB3)
    -   [Alias
        Names](howtoimplaprovider.html#GUID-735A3CD6-0EE5-423C-B5BA-61500BA20854)
    -   [Service
        Interdependencies](howtoimplaprovider.html#GUID-8ED3CE1A-B25A-4E16-B45D-4EB36C9A7406)
    -   [Default
        Initialization](howtoimplaprovider.html#GUID-A46F72E3-DFF4-4864-8BBC-30684ADF78BA)
    -   [Default Key Pair Generator Parameter
        Requirements](howtoimplaprovider.html#GUID-A80C8BAC-AD25-4328-AE62-987F805B6BAF)
    -   [The Provider.Service
        Class](howtoimplaprovider.html#GUID-B1428B09-5542-4D36-9C0D-D78A8B2B3C00)
    -   [Signature
        Formats](howtoimplaprovider.html#GUID-604DD293-1F38-487D-A2F9-F9E95F5D727C)
    -   [DSA Interfaces and their Required
        Implementations](howtoimplaprovider.html#GUID-C618C5AF-737E-41AB-8FD3-6F5BB8A319A9)
    -   [RSA Interfaces and their Required
        Implementations](howtoimplaprovider.html#GUID-353BF021-CABC-4CB4-A019-927D423B4627)
    -   [Diffie-Hellman Interfaces and their Required
        Implementations](howtoimplaprovider.html#GUID-E63F9312-ED15-41D5-8F62-93C6137D5F06)
    -   [Interfaces for Other Algorithm
        Types](howtoimplaprovider.html#GUID-6F87545B-E4EF-4EA7-8EAF-0FEA9DB2495E)
    -   [Algorithm Parameter Specification Interfaces and
        Classes](howtoimplaprovider.html#GUID-4EC9F5A8-8427-40DC-A480-38482B05C8A9)
    -   [Key Specification Interfaces and Classes Required by Key
        Factories](howtoimplaprovider.html#GUID-97E2DE2A-5DFD-4A87-AFA7-CDECC3F77FA6)
    -   [Secret-Key
        Generation](howtoimplaprovider.html#GUID-63A770A3-398A-41C4-B2C9-894D76567F5C)
    -   [Adding New Object
        Identifiers](howtoimplaprovider.html#GUID-5A41A05A-B8F0-4E24-A61B-347721809A8B)
    -   [Ensuring
        Exportability](howtoimplaprovider.html#GUID-ECCC1170-B552-4CF9-BD00-64A70DEC2AC6)
-   [Sample Code for
    MyProvider](howtoimplaprovider.html#GUID-0BB9FD94-C66E-44BC-BE8A-AF7CB376F137)

[<span class="secnum">4</span> JDK Providers Documentation](oracle-providers.html#GUID-FE2D2E28-C991-4EF9-9DBE-2A4982726313) {#jdk-providers-documentation .tocheader}
---------------------------------------------------------------------------------------------------------------------------

-   [Introduction to JDK
    Providers](oracle-providers.html#GUID-F41EE1C9-DD6A-4BAB-8979-EB7654094029)
-   [Import Limits on Cryptographic
    Algorithms](oracle-providers.html#GUID-9224B90B-7B2F-41F9-BB96-C0A1B6A0FEAA)
-   [Cipher
    Transformations](oracle-providers.html#GUID-BC92B7F1-D15C-432A-B725-9BBA9FEF61DB)
-   [SecureRandom
    Implementations](oracle-providers.html#GUID-9DC4ADD5-6D01-4B2E-9E85-B88E3BEE7453)
-   [The SunPKCS11
    Provider](oracle-providers.html#GUID-C4706FFE-D08F-4E29-B0BE-CCE8C93DD940)
-   [The SUN
    Provider](oracle-providers.html#GUID-3A80CC46-91E1-4E47-AC51-CB7B782CEA7D)
-   [The SunRsaSign
    Provider](oracle-providers.html#GUID-17E3589E-E4BA-4881-9B12-9880DD2D128D)
-   [The SunJSSE
    Provider](oracle-providers.html#GUID-7093246A-31A3-4304-AC5F-5FB6400405E2)
-   [The SunJCE
    Provider](oracle-providers.html#GUID-A47B1249-593C-4C38-A0D0-68FA7681E0A7)
-   [The SunJGSS
    Provider](oracle-providers.html#GUID-9CAAC18D-CFF0-4602-A1B7-53C9FAA98C9F)
-   [The SunSASL
    Provider](oracle-providers.html#GUID-EB759F08-B8D8-424A-9357-10F9002AE177)
-   [The XMLDSig
    Provider](oracle-providers.html#GUID-D09DE3FE-237F-4B7B-A323-0A370137E0F3)
-   [The SunPCSC
    Provider](oracle-providers.html#GUID-DEAD6543-FB59-46F3-B4E7-EE1AFE246EA0)
-   [The SunMSCAPI
    Provider](oracle-providers.html#GUID-4F1737D6-1569-4340-B140-678C70E63CD5)
-   [The SunEC
    Provider](oracle-providers.html#GUID-091BF58C-82AB-4C9C-850F-1660824D5254)
-   [The OracleUcrypto
    Provider](oracle-providers.html#GUID-B1F2B3F3-F2A4-4FF5-8887-3B3335343B2A)
-   [The Apple
    Provider](oracle-providers.html#GUID-3185649A-C316-45F2-A70E-2B3FF6BDC34F)
-   [The JdkLDAP
    Provider](oracle-providers.html#GUID-67D4652C-2551-4BBE-9941-50A9348AEA84)
-   [The JdkSASL
    Provider](oracle-providers.html#GUID-D08B5350-6653-4FC6-B350-2B009A9E7FD6)

[<span class="secnum">5</span> PKCS\#11 Reference Guide](pkcs11-reference-guide1.html#GUID-30E98B63-4910-40A1-A6DD-663EAF466991) {#pkcs11-reference-guide .tocheader}
-------------------------------------------------------------------------------------------------------------------------------

-   [SunPKCS11
    Provider](pkcs11-reference-guide1.html#GUID-6DA72F34-6C6A-4F7D-ADBA-5811576A9331)
-   [SunPKCS11
    Requirements](pkcs11-reference-guide1.html#GUID-97F1E537-CB59-4C7F-AB6B-05D4DBD69AC0)
-   [SunPKCS11
    Configuration](pkcs11-reference-guide1.html#GUID-C4ABFACB-B2C9-4E71-A313-79F881488BB9)
-   [Accessing Network Security Services
    (NSS)](pkcs11-reference-guide1.html#GUID-85EA1017-E59C-49B9-9207-65B7B2BF171E)
-   [Troubleshooting
    PKCS\#11](pkcs11-reference-guide1.html#GUID-7989F8B4-7260-4908-8203-99056B2D060E)
-   [Disabling PKCS\#11 Providers and/or Individual PKCS\#11
    Mechanisms](pkcs11-reference-guide1.html#GUID-F068B4E6-8FAD-4443-9269-7DF13573C8DF)
-   [Application
    Developers](pkcs11-reference-guide1.html#GUID-4C366313-33B9-458C-A845-33D0C8A9C367)
    -   [Token
        Login](pkcs11-reference-guide1.html#GUID-6E8B2F3C-792F-4512-9BB3-234C440ADC46)
    -   [Token
        Keys](pkcs11-reference-guide1.html#GUID-508B5E3B-BF39-4E02-A1BD-523352D3AA12)
    -   [Delayed Provider
        Selection](pkcs11-reference-guide1.html#GUID-99785B51-50D8-458E-AA2C-755749F1E39E)
    -   [JAAS
        KeyStoreLoginModule](pkcs11-reference-guide1.html#GUID-60672551-8FF7-4BE1-AF28-CA0C81706B1C)
    -   [Tokens as JSSE Keystore and Trust
        Stores](pkcs11-reference-guide1.html#GUID-CE29BCBA-4C87-4DA0-B170-328E579200BD)
-   [Using keytool and jarsigner with PKCS\#11
    Tokens](pkcs11-reference-guide1.html#GUID-05DE5039-C62A-42B9-8F8E-DB6DB1B0CD44)
-   [Policy
    Tool](pkcs11-reference-guide1.html#GUID-F8D31D74-8D4D-4981-BC63-05ABED100AB8)
-   [Provider
    Developers](pkcs11-reference-guide1.html#GUID-2216C9EC-5F64-424C-BA35-E7DDEDC61C53)
    -   [Provider
        Services](pkcs11-reference-guide1.html#GUID-BDF21F95-43FA-462F-A89C-5DF20760440E)
    -   [Parameter
        Support](pkcs11-reference-guide1.html#GUID-AD009675-E028-4A86-BE87-8DBD03B538DC)
-   [SunPKCS11 Provider Supported
    Algorithms](pkcs11-reference-guide1.html#GUID-D3EF9023-7DDC-435D-9186-D2FD05674777)
-   [SunPKCS11 Provider KeyStore
    Requirements](pkcs11-reference-guide1.html#GUID-F068390B-EB41-48A0-A713-B4CBCC72285D)
-   [Example
    Provider](pkcs11-reference-guide1.html#GUID-50C137F1-F23B-434D-AA90-5A744ABA2F5B)

[<span class="secnum">6</span> Java Authentication and Authorization Service (JAAS)](java-authentication-and-authorization-service-jaas1.htm) {#java-authentication-and-authorization-service-jaas .tocheader}
---------------------------------------------------------------------------------------------------------------------------------------------

-   [Java Authentication and Authorization Service (JAAS) Reference
    Guide](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-2A935F5E-0803-411D-B6BC-F8C64D01A25C)
    -   [Who Should Read This
        Document](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-31AC2288-E4E8-42D9-821E-85385F1F2FE8)
    -   [Related
        Documentation](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-11885DA7-0D17-4756-B193-3CC9376B1225)
    -   [Core Classes and
        Interfaces](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-D679A98F-C706-4FE2-9027-39A520BA0FCB)
        -   [Common
            Classes](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-2CDC988F-D462-4CEA-9243-CC74B000327F)
            -   [Subject](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-804BDE80-9E66-421C-BF0A-A96FBE7DE4E3)
            -   [Principals](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-8FAF9739-CD62-4A47-9582-884DBF3081F0)
            -   [Credentials](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-9381520E-7A13-4087-BA26-C6CB8BE4A437)
        -   [Authentication Classes and
            Interfaces](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-6A19B0FB-39F9-4917-A3B1-72E4387BA021)
            -   [LoginContext](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-164692CF-6790-488C-BF86-39F7C5CF0F5A)
            -   [LoginModule](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-0FDBE77C-01C3-4A98-9925-4F8D2E260118)
            -   [CallbackHandler](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-1018AB86-8912-4C00-8717-2FA2B54A4866)
            -   [Callback](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-A6E64966-EDDC-4519-9E42-1114E5E3DEFC)
        -   [Authorization
            Classes](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-B8891FFA-ACD2-4E42-9488-0551B28F31C8)
            -   [Policy](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-66990EE6-1213-4BF7-AC43-A4C75AE6746D)
            -   [AuthPermission](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-B7D676A5-E9E6-4FDA-B0F3-8A51B3747138)
            -   [PrivateCredentialPermission](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-D7D015EE-54C6-4D85-83C2-05742314847D)
    -   [JAAS Tutorials and Sample
        Programs](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-7B9C6511-A221-414A-8A4B-6BCF08172065)
    -   [Appendix A: JAAS Settings in the java.security Security
        Properties
        File](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-106F4B32-B9A3-4B75-BDBF-29B252BB3F53)
        -   [Login Configuration
            Provider](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-75C5BF67-1530-4383-8A0D-6C2C6B378096)
        -   [Login Configuration
            URLs](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-F26A634E-7D9F-41FD-822A-59A2D33E79BB)
        -   [Policy
            Provider](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-6396FFE2-3877-405C-B40C-8B838A2B69D5)
        -   [Policy File
            URLs](java-authentication-and-authorization-service-jaas-reference-guide.html#GUID-D6502328-3C68-4E79-816B-599CC503DF73)
    -   [Appendix B: JAAS Login Configuration
        File](appendix-b-jaas-login-configuration-file.html#GUID-7EB80FA5-3C16-4016-AED6-0FC619F86F8E)
        -   [Login Configuration File Structure and
            Contents](appendix-b-jaas-login-configuration-file.html#GUID-9713B697-EFED-49A1-9E15-8039AD04458B)
        -   [Where to Specify Which Login Configuration File Should Be
            Used](appendix-b-jaas-login-configuration-file.html#GUID-1D5D78E1-4771-43B7-AEED-1D427A7044F0)
-   [JAAS
    Tutorials](jaas-tutorials.html#GUID-272DB20A-B590-4B2E-BD60-7EF9EB54AB5A)
    -   [JAAS Authentication
        Tutorial](jaas-authentication-tutorial.html#GUID-BFEBDB00-9826-499C-A20F-E9463883DED4)
        -   [The Authentication Tutorial
            Code](jaas-authentication-tutorial.html#GUID-EF77AA97-CB87-4D1D-A3BF-8541FF41BA4A)
            -   [SampleAcn.java](jaas-authentication-tutorial.html#GUID-01DE56D2-3A45-4C38-83EB-257783975372)
            -   [SampleLoginModule.java and
                SamplePrincipal.java](jaas-authentication-tutorial.html#GUID-03476CCA-11C6-4D51-B170-C8DD7C0D9075)
        -   [The Login
            Configuration](jaas-authentication-tutorial.html#GUID-987700C5-AE03-4EB1-B16A-66A1404B9604)
            -   [The Login Configuration File for the JAAS
                Authentication
                Tutorial](jaas-authentication-tutorial.html#GUID-A7E0803F-DA0B-42BF-8E25-DA5889BE847F)
        -   [Running the
            Code](jaas-authentication-tutorial.html#GUID-743703A2-7EC1-4391-A816-4A883FB6A017)
        -   [Running the Code with a Security
            Manager](jaas-authentication-tutorial.html#GUID-44F2BF3A-F51D-4F21-8F40-96CB1120396D)
    -   [JAAS Authorization
        Tutorial](jaas-authorization-tutorial.html#GUID-D43CF965-8A5F-4A23-A2AF-F41DD5F8B411)
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
            -   [SampleAzn.java](jaas-authorization-tutorial.html#GUID-07EAB926-63EA-48F4-8DF0-4CC4526FA545)
            -   [SampleAction.java](jaas-authorization-tutorial.html#GUID-6ECF7E31-E49D-4DF7-B9C9-1EB62EA32510)
        -   [The Login Configuration File for the JAAS Authorization
            Tutorial](jaas-authorization-tutorial.html#GUID-247D6204-446B-4B48-B376-5CD76CAFE3E7)
        -   [The Policy
            File](jaas-authorization-tutorial.html#GUID-8462E46D-FF67-4630-9A87-D24EE60D100C)
            -   [Permissions Required by
                SampleAzn](jaas-authorization-tutorial.html#GUID-B048635B-ACC3-4049-BFAA-16F047ABA415)
            -   [Permissions Required by
                SampleAction](jaas-authorization-tutorial.html#GUID-1C4609F2-96F3-4B8B-BFF4-1496301EA4B0)
            -   [Permissions Required by
                SampleLoginModule](jaas-authorization-tutorial.html#GUID-C7890B53-2A4B-4024-8A67-23CAFC81C496)
            -   [The Full Policy
                File](jaas-authorization-tutorial.html#GUID-3A2FF6CF-3124-4402-B550-D0F4E76B3D4D)
            -   [Running the Authorization Tutorial
                Code](jaas-authorization-tutorial.html#GUID-04A78ED2-B68C-4C89-849D-F9BF4F17BBD1)
-   [Java Authentication and Authorization Service (JAAS): LoginModule
    Developer\'s
    Guide](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A)
    -   [Introduction to
        LoginModule](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-3F7CF22D-A207-49EE-B1CC-575FBF3789DE)
    -   [Steps to Implement a
        LoginModule](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-EE1C4BBE-289F-4419-A233-43F2D897765B)
        -   [Step 1: Understand the Authentication
            Technology](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-A4140569-4124-4AE7-81CC-145537BE0F42)
        -   [Step 2: Name the LoginModule
            Implementation](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-A6BAE987-54F4-4634-9D03-7EB986C7F484)
        -   [Step 3: Implement the Abstract LoginModule
            Methods](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-E9C5810B-ADB6-4454-869D-B269ECA8145F)
        -   [Step 4: Choose or Write a Sample
            Application](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-4A0BD9DC-B45F-4606-A6BD-8BAC22952C52)
        -   [Step 5: Compile the LoginModule and
            Application](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-6DEAB2A4-2ADE-4CC8-B188-F0A58A38F61C)
        -   [Step 6: Prepare for
            Testing](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-800F2CC8-C4BC-4AE7-B29A-1BFBE01D9979)
        -   [Step 7: Test Use of the
            LoginModule](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-D8079E42-9E73-4378-9D34-E528BE727857)
        -   [Step 8: Document Your LoginModule
            Implementation](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-F799DF94-AD31-47CC-8760-863492F506EF)
        -   [Step 9: Make LoginModule JAR File and Documents
            Available](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.html#GUID-0A07484F-050E-4162-AE90-3A975AB26055)

[<span class="secnum">7</span> Java Generic Security Services (Java GSS-API)](java-generic-security-services-java-gss-api1.htm) {#java-generic-security-services-java-gss-api .tocheader}
-------------------------------------------------------------------------------------------------------------------------------

-   [Introduction to JAAS and Java GSS-API
    Tutorials](introduction-jaas-and-java-gss-api-tutorials1.htm)
    -   [When to Use Java GSS-API Versus
        JSSE](when-use-java-gss-api-vs-jsse.html#GUID-51EAFD1C-7203-40C7-A295-61062D322E8C)
    -   [Use of Java GSS-API for Secure Message Exchanges Without JAAS
        Programming](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-42A2B80C-90CD-4C7A-8EED-8BFFE83CAF56)
        -   [Overview of the Client and Server
            Applications](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-BEDCBE80-87A3-4124-B891-DF15C55301A5)
        -   [The SampleClient and SampleServer
            Code](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-0DDC8ACE-7398-41C6-B061-CF3DEAB7AC86)
            -   [Obtaining the Command-Line
                Arguments](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-50F25F90-A350-4A21-A06E-44E33209D542)
            -   [Establishing a Socket Connection for Message
                Exchanges](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-04BC81DE-98D3-42CA-9AC0-45CB4ECEC0BB)
            -   [Establishing a Security
                Context](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-3619B5FA-76CA-4445-8770-8D56CEBA967B)
            -   [Exchanging Messages
                Securely](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-39585A77-5CF3-4122-B4EC-3D778392370D)
            -   [Clean
                Up](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-DA54B317-30B2-4666-86B6-B1AD4D627002)
        -   [Kerberos User and Service Principal
            Names](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-6D82A7D2-C406-40F4-838A-42ED61194182)
            -   [When the Realm Is Required in Principal
                Names](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-B2F0BDD6-C35F-4B99-8AC3-60F0FCD351DF)
        -   [The Login Configuration
            File](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-2ED6C724-87F1-49EB-9015-32E6E74E3C6A)
        -   [The useSubjectCredsOnly System
            Property](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-841EB74E-3B52-4421-BC10-FE3C8511E007)
        -   [Running the SampleClient and SampleServer
            Programs](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-DC1FCD2D-101C-4EF2-8034-387CBE66FA3E)
            -   [Prepare SampleServer for
                Execution](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-758C5F29-2F6A-420B-9BFA-FA741149F3B6)
            -   [Prepare SampleClient for
                Execution](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-2D1E8C81-221C-44CC-9B86-7A41C7DCA44B)
            -   [Execute
                SampleServer](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-9D61C2A9-1E0D-4701-8FBF-F5D31AA4BB2C)
            -   [Execute
                SampleClient](use-java-gss-api-secure-message-exchanges-jaas-programming.html#GUID-9AF3C84A-CB43-4F4B-A09D-445D8741FE59)
    -   [JAAS
        Authentication](jaas-authentication.html#GUID-0C6EB04B-D203-4688-A3E2-A7D442334623)
        -   [The Authentication Tutorial
            Code](jaas-authentication.html#GUID-F12A6645-5A3E-41F7-94E6-57694DFFF2D3)
            -   [Instantiating a
                LoginContext](jaas-authentication.html#GUID-080F384C-0FF3-4443-B4A7-21B6F03371F0)
            -   [Calling the LoginContext\'s login
                Method](jaas-authentication.html#GUID-98A3DD32-C417-449B-9C55-1C9509364612)
        -   [The Login
            Configuration](jaas-authentication.html#GUID-C595253D-3817-4CA6-9336-D7D5159C9680)
            -   [The Login Configuration File for This
                Tutorial](jaas-authentication.html#GUID-D6F986DD-2046-4025-A65F-AC8855C85984)
        -   [Running the
            Code](jaas-authentication.html#GUID-A76E9155-E82F-48C0-9382-C365C157EEBF)
        -   [Running the Code with a Security
            Manager](jaas-authentication.html#GUID-EF86E769-AFAF-4341-B9B0-4E122A0BFCEC)
    -   [JAAS
        Authorization](jaas-authorization.html#GUID-69241059-CCD0-49F6-838F-DDC752F9F19F)
        -   [What is JAAS
            Authorization?](jaas-authorization.html#GUID-95EBDFAE-D531-45ED-BF48-4CC122E483E1)
        -   [How Is JAAS Authorization
            Performed?](jaas-authorization.html#GUID-9B40B33D-3618-4F98-9DDE-9A639F751CA4)
            -   [How Do You Make Principal-Based Policy File
                Statements?](jaas-authorization.html#GUID-80F0B546-1E95-457B-8EF7-5BB1519E20A4)
            -   [How Do You Associate a Subject with an Access Control
                Context?](jaas-authorization.html#GUID-86CC2E0C-58B9-4E35-91E1-EC130EE2E4FC)
        -   [The Authorization Tutorial
            Code](jaas-authorization.html#GUID-6C7F947A-E2F3-4C1A-BF58-8198E4E9B6D3)
            -   [JaasAzn.java](jaas-authorization.html#GUID-EEBB584B-80FA-4EDD-B57A-BED4CCFE4EB4)
            -   [SampleAction.java](jaas-authorization.html#GUID-994AEA05-292D-418A-8C2D-A32E3A9AC7D3)
        -   [The Login Configuration
            File](jaas-authorization.html#GUID-C7E4B4C5-1541-4482-BA11-98A1D489CA76)
        -   [The Policy
            File](jaas-authorization.html#GUID-19567566-CC1A-4440-AE33-D7C6AB305D3F)
            -   [Permissions Required by
                JaasAzn](jaas-authorization.html#GUID-90DA29A4-6980-49EB-B4F0-21E6678AB7A2)
            -   [Permissions Required by
                SampleAction](jaas-authorization.html#GUID-9ADEB874-E415-4ABC-BB20-70FBBFF87F84)
        -   [Running the Authorization Tutorial
            Code](jaas-authorization.html#GUID-F22DFBEC-7DF0-4CFB-B882-B5A58C2C76B1)
    -   [Use of JAAS Login
        Utility](use-jaas-login-utility.html#GUID-F41E74DF-EE54-4EB1-8609-49C6D324ADF5)
        -   [What You Need to Know About the Login
            Utility](use-jaas-login-utility.html#GUID-F92EBF93-2E18-4006-86CC-3D4C0DC6174E)
        -   [Application and Other File
            Requirements](use-jaas-login-utility.html#GUID-A988A760-1F2E-4665-AC8B-BACDEBAED5B5)
            -   [Application
                Requirements](use-jaas-login-utility.html#GUID-2DA66897-B872-4DB3-B580-2A884321B52E)
            -   [Login Configuration File
                Requirements](use-jaas-login-utility.html#GUID-1475ADA8-4B71-4022-8295-209AFCEB89D9)
            -   [Policy File
                Requirements](use-jaas-login-utility.html#GUID-6F2F1165-FF1F-46BB-B18B-1D13E1A51BAF)
        -   [The Sample Application
            Program](use-jaas-login-utility.html#GUID-78D65FB0-34DC-4DEE-95A4-0C0BD1AE6330)
        -   [The Login Configuration
            File](use-jaas-login-utility.html#GUID-DFC52892-6206-4D1F-96B3-B8F11C2536E1)
        -   [The Policy
            File](use-jaas-login-utility.html#GUID-FF7EBCB2-F3B9-4483-86A1-7EDA7ECA1689)
            -   [Permissions Required by the Login and MyAction
                Classes](use-jaas-login-utility.html#GUID-9E9CAD3D-5F80-424E-AE19-B102064054E4)
            -   [Permissions Required by
                Sample](use-jaas-login-utility.html#GUID-25C2E3C5-F329-40F3-A701-878526AFEEB2)
        -   [Running the Sample Program with the Login
            Utility](use-jaas-login-utility.html#GUID-B3F1D0B9-D58A-469B-AF56-9636FE86FF0F)
    -   [Use of JAAS Login Utility and Java GSS-API for Secure Message
        Exchanges](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-C1DFED9D-D3A1-4C11-95D8-3543935E87C8)
        -   [Before You Start: Recommended
            Reading](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-A742F77E-9D77-42E1-BFB8-2DE9C6FB3051)
        -   [Overview of the Client and Server
            Applications](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-1C2B6E45-2E2F-421C-B0D3-F034156DDAE7)
        -   [Kerberos User and Service Principal
            Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-832A32FD-3D99-4624-86A4-7AFBF8924C80)
            -   [When the Realm is Required in Principal
                Names](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-E863F99A-77AC-4BE8-BAC1-A7B2E77FE775)
        -   [The Login Configuration
            File](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-3B582CD5-135F-4516-843E-1831DB25CCC4)
        -   [The Policy
            Files](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-2BA7F0B7-D3E3-4B81-8E98-0A39F9763B59)
            -   [The Client Policy
                File](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-6C3F477A-6245-48F1-B83F-3CCE8581197C)
            -   [The Server Policy
                File](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-9126BE63-55A5-45C0-8EDC-89A65A83271D)
        -   [Running the SampleClient and SampleServer
            Programs](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-07D0C8CC-0922-4B0F-B14D-9A644CB13783)
            -   [Prepare SampleServer for
                Execution](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-901B5429-D25C-4DAA-90BB-7665E3682D52)
            -   [Prepare SampleClient for
                Execution](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-F72FA916-2507-479C-A2E3-89FCB25D0FE8)
            -   [Execute
                SampleServer](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-70ADB0E1-E036-4E40-8289-66545AD90C2F)
            -   [Execute
                SampleClient](use-jaas-login-utility-and-java-gss-api-secure-message-exchanges.html#GUID-19CC950B-FFCA-471A-918E-92559F556356)
    -   [More Things You Can Do with Java GSS-API and
        JAAS](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-B69758E7-D7B9-4860-BFA2-0429618374E8)
        -   [Executing Code on Behalf of the Client
            User](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-7836E843-A8F1-4C59-A5FD-BFEE3B307508)
            -   [Basic
                Approach](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-08F32421-A49E-4DB8-9FD9-CC25D398CF2D)
            -   [Sample Code and Policy
                File](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-B04626E5-C67D-4116-A7D4-4D58270BE4CB)
            -   [Running the Sample
                Code](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-4CD5A92F-DDD9-4464-9F42-4105B583A08B)
        -   [Using Credentials Delegated from the
            Client](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-23E84B31-CEAD-4FAC-A3EB-AD807587A502)
        -   [Permission Required In Order to Delegate
            Credentials](more-things-you-can-do-java-gss-api-and-jaas.html#GUID-46E411CE-A04B-4489-AEC6-9AF4D569B371)
    -   [Kerberos
        Requirements](kerberos-requirements1.html#GUID-EAA2758B-3071-4CDA-AEF1-D76F5271E998)
        -   [Setting Properties to Indicate the Default Realm and
            KDC](kerberos-requirements1.html#GUID-8B30CD5C-64B6-48DE-9CD5-0E44D3A434A7)
        -   [Locating the krb5.conf Configuration
            File](kerberos-requirements1.html#GUID-0C6413BA-417B-493D-BC89-F9FB90D5E641)
        -   [Naming Conventions for Realm Names and
            Hostnames](kerberos-requirements1.html#GUID-E73CCEA1-E94F-4E8D-9C42-403AF825658A)
        -   [Cross-Realm
            Authentication](kerberos-requirements1.html#GUID-9D76C533-8EF4-4417-884A-37C60FA233FC)
    -   [Troubleshooting](troubleshooting.html#GUID-2087ADBA-6C36-43D5-8841-C79FCB4F5FBE)
    -   [Source Code for JAAS and Java GSS-API
        Tutorials](source-code-jaas-and-java-gss-api-tutorials.htm)
    -   [Related Documentation](related-documentation1.htm)
-   [Single Sign-on Using Kerberos in
    Java](single-sign-using-kerberos-java1.html#GUID-D4230975-A28B-4532-B1DD-3C7219A4867F)
    -   [Abstract](single-sign-using-kerberos-java1.html#GUID-E8171823-258A-45DF-A420-661EAC84CCDD)
    -   [Introduction](single-sign-using-kerberos-java1.html#GUID-7147244C-E7D5-4D70-92C6-069EB7C651A3)
    -   [Kerberos
        V5](single-sign-using-kerberos-java1.html#GUID-6F8CAB6F-7DA8-4DED-8369-92BBB95C8A9E)
    -   [Java Authentication and Authorization Service
        (JAAS)](single-sign-using-kerberos-java1.html#GUID-38C14739-0A86-46EA-B0E9-44A7CD6AA9E4)
        -   [Pluggable and Stackable
            Framework](single-sign-using-kerberos-java1.html#GUID-B4D7E22E-459E-4909-ABF7-647733847E75)
        -   [Authentication and
            Authorization](single-sign-using-kerberos-java1.html#GUID-2FFC7B8E-C8FC-492B-8D57-0BC14EA4D033)
        -   [Subject](single-sign-using-kerberos-java1.html#GUID-AA7F81DA-583A-4275-8D2E-0C1FD2919ED2)
        -   [doAs and
            doAsPrivileged](single-sign-using-kerberos-java1.html#GUID-6F5671ED-C6FC-4842-A1FA-DB08E61C369A)
        -   [LoginContext](single-sign-using-kerberos-java1.html#GUID-DBF4F859-01ED-4E47-B842-EE128B146E8D)
        -   [Callbacks](single-sign-using-kerberos-java1.html#GUID-20572EC0-B790-4C69-B168-6129F9B42C26)
        -   [LoginModules](single-sign-using-kerberos-java1.html#GUID-8AFBA819-AE63-4879-B83F-0E64FB880939)
        -   [The Kerberos Login
            Module](single-sign-using-kerberos-java1.html#GUID-45DD4879-CD1B-4E02-8B20-572C95C8386E)
        -   [Kerberos
            Classes](single-sign-using-kerberos-java1.html#GUID-A82CE65B-0730-42EC-973B-51D1CDA7D382)
        -   [Authorization](single-sign-using-kerberos-java1.html#GUID-BB48DD97-7BC5-487D-AE9C-E469917DFE73)
    -   [Java Generic Security Service Application Program Interface
        (Java
        GSS-API)](single-sign-using-kerberos-java1.html#GUID-3336BC5D-90CA-4646-B96A-FE79EA2D1AD6)
        -   [Generic Security Service API
            (GSS-API)](single-sign-using-kerberos-java1.html#GUID-A92F4222-4C58-49AA-AF94-E7BB12D3C3C5)
        -   [Java
            GSS-API](single-sign-using-kerberos-java1.html#GUID-D73F1DE2-D003-429F-B918-2CDC6897E9C7)
        -   [The GSSName
            Interface](single-sign-using-kerberos-java1.html#GUID-AB5BB523-052A-4ACA-B0D5-BF5A3C220093)
        -   [The GSSCredential
            Interface](single-sign-using-kerberos-java1.html#GUID-01637F56-125B-469E-8C4A-D642417DE870)
        -   [The GSSContext
            Interface](single-sign-using-kerberos-java1.html#GUID-D552C782-1820-444B-85EA-A4AED3DE3757)
        -   [Message
            Protection](single-sign-using-kerberos-java1.html#GUID-627867F1-0787-4D20-A971-01F2B5EA3FF3)
        -   [Credential
            Delegation](single-sign-using-kerberos-java1.html#GUID-363496FF-1E54-4A63-8B3B-89D7D23C2C4B)
    -   [Default Credential Acquisition
        Model](single-sign-using-kerberos-java1.html#GUID-B54B88B4-087F-4B0D-A28B-C0980D762D5C)
    -   [Exceptions to the
        Model](single-sign-using-kerberos-java1.html#GUID-7F63948A-0FF3-4818-89E8-B39A1CF4DBB3)
    -   [Web Browser
        Integration](single-sign-using-kerberos-java1.html#GUID-E478197F-C0D8-4D35-82D8-E52E2B307B9B)
    -   [Security
        Risks](single-sign-using-kerberos-java1.html#GUID-1793ADE8-8B78-4680-A871-063ED761CFF5)
        -   [Credential
            Acquisition](single-sign-using-kerberos-java1.html#GUID-23E25BFC-E77A-495C-8406-897E9D124395)
        -   [Context
            Establishment](single-sign-using-kerberos-java1.html#GUID-5BB1D535-B4A3-403A-91CF-8A5B98B6DB0E)
        -   [Credential
            Delegation](single-sign-using-kerberos-java1.html#GUID-3D1AFF31-323B-4DD6-829A-B7205FA11161)
    -   [Conclusions](single-sign-using-kerberos-java1.html#GUID-4A2151A0-B23A-4B2E-BFEE-A17545262B48)
    -   [Acknowledgements](single-sign-using-kerberos-java1.html#GUID-D65B3B0F-2689-4B4E-BAAD-A9E0D3571A84)
    -   [References](single-sign-using-kerberos-java1.html#GUID-67712665-922E-4947-8103-0AAE9C2AAC2B)
-   [Advanced Security Programming in Java SE Authentication, Secure
    Communication and Single
    Sign-On](advanced-security-programming-java-se-authentication-secure-communication-and-single-sign1.htm)
    -   [Part I : Secure Authentication using the Java Authentication
        and Authorization Service
        (JAAS)](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.html#GUID-42416198-9AEE-428C-80EF-2A56488B5890)
        -   [Exercise 1: Using the JAAS
            API](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.html#GUID-1446370E-5019-4BD1-860A-22BAC1F13CF8)
        -   [Exercise 2: Configuring JAAS for Kerberos
            Authentication](part-i-secure-authentication-using-java-authentication-and-authorization-service-jaas.html#GUID-2079DC72-5A2E-46FE-978F-42D113FFA41A)
    -   [Part II : Secure Communications using the Java SE Security
        API](part-ii-secure-communications-using-java-se-security-api.html#GUID-98B02DB0-13DB-4175-9485-3449E1A241B5)
        -   [Exercise 3: Using the Java Generic Security Service (GSS)
            API](part-ii-secure-communications-using-java-se-security-api.html#GUID-1E4E43BA-EC38-435E-A426-7A88E52F34DF)
        -   [Exercise 4: Using the Java SASL
            API](part-ii-secure-communications-using-java-se-security-api.html#GUID-727C5CDB-8701-40B3-8355-00C8314590A3)
        -   [Exercise 5: Using the Java Secure Socket Extension with
            Kerberos](part-ii-secure-communications-using-java-se-security-api.html#GUID-9AAFC7BB-8562-4E3E-B5EF-E33F30E779D1)
    -   [Part III : Deploying for Single Sign-On in a Kerberos
        Environment](part-iii-deploying-single-sign-kerberos-environment.html#GUID-549EA363-62DD-4819-BC92-4C8B23D01A1F)
        -   [Exercise 6: Deploying for Single
            Sign-On](part-iii-deploying-single-sign-kerberos-environment.html#GUID-5D0B8FD9-FF12-44E7-B7E9-7620E95E784C)
    -   [Part IV : Secure Communications Using Stronger Encryption
        Algorithms](part-iv-secure-communications-using-stronger-encryption-algorithms.html#GUID-49820DF7-0DED-4C63-8DB8-89718501ADB1)
        -   [Exercise 7: Configuring to Use Stronger Encryption
            Algorithms in a Kerberos Environment, to Secure the
            Communication](part-iv-secure-communications-using-stronger-encryption-algorithms.html#GUID-29FBA28F-5E45-47FF-AB3A-CEB60871D212)
    -   [Part V : Secure Authentication Using SPNEGO Java GSS
        Mechanism](part-v-secure-authentication-using-spnego-java-gss-mechanism.html#GUID-B51B4169-BD5D-4A19-BC2B-7F6B3ABB9B7A)
        -   [Exercise 8: Using the Java Generic Security Services (GSS)
            API with
            SPNEGO](part-v-secure-authentication-using-spnego-java-gss-mechanism.html#GUID-47C377A7-68D9-4B16-86AF-5AE89BCB2845)
    -   [Part VI: HTTP/SPNEGO
        Authentication](part-vi-http-spnego-authentication.html#GUID-996F729E-5FEA-4E29-A32A-78FB510B2D80)
        -   [Exercise 9: Using HTTP/SPNEGO
            Authentication](part-vi-http-spnego-authentication.html#GUID-2978DB58-6217-4E29-95EF-2C1F25F7C37F)
            -   [What is HTTP
                SPNEGO](part-vi-http-spnego-authentication.html#GUID-89457AC9-89FE-4934-A6F3-B03D72D95AA7)
            -   [How to use HTTP/SPNEGO
                Authentication](part-vi-http-spnego-authentication.html#GUID-1101592C-854C-4CB2-B46C-CE3EE8652FB0)
            -   [HTTP/SPNEGO Authentication
                Example](part-vi-http-spnego-authentication.html#GUID-05B34286-D0B6-4C35-B0BF-C98CD9F7E1D2)
    -   [Source Code for Advanced Security Programming in Java SE
        Authentication, Secure Communication and Single
        Sign-On](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm)
    -   [Appendix A: Setting up Kerberos
        Accounts](appendix-setting-kerberos-accounts.html#GUID-D1F41B0A-E756-49CB-828A-422DC23E572B)
-   [The Kerberos 5 GSS-API Mechanism](kerberos-5-gss-api-mechanism.htm)

[<span class="secnum">8</span> Java Secure Socket Extension (JSSE) Reference Guide](java-secure-socket-extension-jsse-reference-guide.html#GUID-93DEEE16-0B70-40E5-BBE7-55C3FD432345) {#java-secure-socket-extension-jsse-reference-guide .tocheader}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   [Introduction to
    JSSE](java-secure-socket-extension-jsse-reference-guide.html#GUID-0EF5DA4E-856C-4AD2-A9FD-0837C5881DDA)
    -   [JSSE Features and
        Benefits](java-secure-socket-extension-jsse-reference-guide.html#GUID-F069F4ED-DF2C-4B3B-90FB-F89E700CF21A)
    -   [JSSE Standard
        API](java-secure-socket-extension-jsse-reference-guide.html#GUID-2DF22C2B-C32E-4665-BB4B-E9510865FDC0)
    -   [SunJSSE
        Provider](java-secure-socket-extension-jsse-reference-guide.html#GUID-59EC25A8-4CE4-4D94-896B-8E6FB23C2838)
    -   [JSSE Related
        Documentation](java-secure-socket-extension-jsse-reference-guide.html#GUID-DF5DA7C2-7B13-4341-B8F2-E4A64F8C0FFA)
-   [Terms and
    Definitions](java-secure-socket-extension-jsse-reference-guide.html#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329)
-   [Secure Sockets Layer (SSL) Protocol
    Overview](java-secure-socket-extension-jsse-reference-guide.html#GUID-69ECD56C-3B20-47F4-AEF0-A06EFA13A61D)
    -   [Why Use
        SSL?](java-secure-socket-extension-jsse-reference-guide.html#GUID-4F882170-B4A9-4E61-8411-6D7194B32FED)
    -   [How SSL
        Works](java-secure-socket-extension-jsse-reference-guide.html#GUID-83C9697A-35B7-4962-972F-06795E705BE9)
    -   [Cryptographic
        Processes](java-secure-socket-extension-jsse-reference-guide.html#GUID-AE5F865E-126F-4EF2-8333-DBEB879E06EC)
        -   [Secret-Key
            Cryptography](java-secure-socket-extension-jsse-reference-guide.html#GUID-D2F6DDC1-9689-4BC2-B6D5-4EA13596AEB0)
        -   [Public-Key
            Cryptography](java-secure-socket-extension-jsse-reference-guide.html#GUID-0B0D23FF-1AE8-42FC-95F2-3767833D5E86)
        -   [Comparison Between Secret-Key and Public-Key
            Cryptography](java-secure-socket-extension-jsse-reference-guide.html#GUID-694CE95C-6E3C-4F0E-9ABB-E8DCA655EAA7)
        -   [Public Key
            Certificates](java-secure-socket-extension-jsse-reference-guide.html#GUID-2EEF5310-2407-45E2-A3A5-81532D247CD1)
        -   [Cryptographic Hash
            Functions](java-secure-socket-extension-jsse-reference-guide.html#GUID-86CD4C06-0B0F-4B0F-9C41-3EDC5658F491)
        -   [Message Authentication
            Code](java-secure-socket-extension-jsse-reference-guide.html#GUID-0EB1B09A-0B04-43EA-873D-1E7EE325010D)
        -   [Digital
            Signatures](java-secure-socket-extension-jsse-reference-guide.html#GUID-ECC35863-046D-40D4-8B74-5F0150D4342A)
    -   [The SSL
        Handshake](java-secure-socket-extension-jsse-reference-guide.html#GUID-7FCC21CB-158B-440C-B5E4-E4E5A2D7352B)
    -   [The SSL
        Protocol](java-secure-socket-extension-jsse-reference-guide.html#GUID-D04EF7C1-B1D4-4611-9896-A7B5573CBEED)
        -   [Handshaking Again
            (Renegotiation)](java-secure-socket-extension-jsse-reference-guide.html#GUID-FCA1CA1F-9FF1-4C9F-8FE8-EBFDE84F735F)
        -   [Cipher Suite Choice and Remote Entity
            Verification](java-secure-socket-extension-jsse-reference-guide.html#GUID-D6A538A2-8CEF-4C6D-9C44-295758E64E38)
-   [Client-Driven OCSP and OCSP
    Stapling](java-secure-socket-extension-jsse-reference-guide.html#GUID-E1A3A7C3-309A-4415-903B-B31C96F68C86)
    -   [Client-Driven OCSP and Certificate
        Revocation](java-secure-socket-extension-jsse-reference-guide.html#GUID-5B5A093F-FE4E-4D57-B66C-93CD6F78B1D1)
        -   [Setting up a Java Client to use Client-Driven
            OCSP](java-secure-socket-extension-jsse-reference-guide.html#GUID-4E3834C7-E741-499E-9646-3557670FD88A)
    -   [OCSP Stapling and Certificate
        Revocation](java-secure-socket-extension-jsse-reference-guide.html#GUID-489366D5-635A-4204-8980-3FB126047C45)
        -   [Setting Up a Java Client to Use OCSP
            Stapling](java-secure-socket-extension-jsse-reference-guide.html#GUID-F15D190D-85A1-4012-8FE3-060DBD90E579)
        -   [Setting Up a Java Server to Use OCSP
            Stapling](java-secure-socket-extension-jsse-reference-guide.html#GUID-423716FB-DA34-4C73-B3A1-EB4CE120BB62)
    -   [OCSP Stapling Configuration
        Properties](java-secure-socket-extension-jsse-reference-guide.html#GUID-3A540C8F-5EB7-4E96-9051-92A1E2D8AF37)
-   [JSSE Classes and
    Interfaces](java-secure-socket-extension-jsse-reference-guide.html#GUID-B7AB25FA-7F0C-4EFA-A827-813B2CE7FBDC)
    -   [JSSE Core Classes and
        Interfaces](java-secure-socket-extension-jsse-reference-guide.html#GUID-4A6ABFE4-6B0E-4DF2-A9E8-EEEB71935293)
    -   [SocketFactory and ServerSocketFactory
        Classes](java-secure-socket-extension-jsse-reference-guide.html#GUID-6AF71CD9-4E87-49E1-B175-89810D54139E)
    -   [SSLSocketFactory and SSLServerSocketFactory
        Classes](java-secure-socket-extension-jsse-reference-guide.html#GUID-F0917FCC-FBB0-4E36-8D79-37F14F8A274B)
        -   [Obtaining an
            SSLSocketFactory](java-secure-socket-extension-jsse-reference-guide.html#GUID-86684173-0E06-4EA9-AF89-B80E0D7B602E)
    -   [SSLSocket and SSLServerSocket
        Classes](java-secure-socket-extension-jsse-reference-guide.html#GUID-8EF3AA86-6559-482D-82C7-4F6F6951A1AB)
        -   [Obtaining an
            SSLSocket](java-secure-socket-extension-jsse-reference-guide.html#GUID-BA88D2CC-EC63-4A74-A696-E1A56BD68BF0)
    -   [SSLEngine
        Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-8796681D-06C8-4884-ADE4-782394F6F6FB)
        -   [Creating an SSLEngine
            Object](java-secure-socket-extension-jsse-reference-guide.html#GUID-16B697CD-77EB-468F-94A1-04254BA75FD7)
        -   [Generating and Processing SSL/TLS
            Data](java-secure-socket-extension-jsse-reference-guide.html#GUID-6DB10B60-4FE0-4C29-8E6D-DC661522A2B4)
        -   [Datagram Transport Layer Security (DTLS)
            Protocol](java-secure-socket-extension-jsse-reference-guide.html#GUID-D0F8B9C3-721B-43A4-B2CE-7512B175F76D)
            -   [The DTLS
                Handshake](java-secure-socket-extension-jsse-reference-guide.html#GUID-B62245D1-5337-4B51-B1F3-CA89099157C1)
            -   [Handling Retransmissions in DTLS
                Connections](java-secure-socket-extension-jsse-reference-guide.html#GUID-6C8AA45B-EB45-4767-BBB4-B7C5A64A60B7)
        -   [Creating an SSLEngine Object for
            DTLS](java-secure-socket-extension-jsse-reference-guide.html#GUID-4D854666-433A-4672-B902-565CC7AEE0BF)
        -   [Generating and Processing DTLS
            Data](java-secure-socket-extension-jsse-reference-guide.html#GUID-80EBB1BB-8A36-4B6F-BC35-AF235F30EF45)
        -   [Understanding SSLEngine Operation
            Statuses](java-secure-socket-extension-jsse-reference-guide.html#GUID-AC6700ED-ADC4-41EA-B111-2AEF2CBF7744)
        -   [Dealing With Blocking
            Tasks](java-secure-socket-extension-jsse-reference-guide.html#GUID-7ED13982-53B2-455B-9198-3289F19905B6)
        -   [Shutting Down a SSL/TLS/DTLS
            Connection](java-secure-socket-extension-jsse-reference-guide.html#GUID-2B54A68F-75AF-4FEA-9339-F7082FE5DA33)
    -   [SSLSession and
        ExtendedSSLSession](java-secure-socket-extension-jsse-reference-guide.html#GUID-AB362290-033A-4D3B-AAF3-1BFEB1CD472B)
    -   [HttpsURLConnection
        Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-A14E129D-4D9D-4F38-A9F0-ED6F97B18863)
        -   [Setting the Assigned
            SSLSocketFactory](java-secure-socket-extension-jsse-reference-guide.html#GUID-8BE4AE6F-21EF-4DF0-91D4-B2D36EF625CA)
        -   [Setting the Assigned
            HostnameVerifier](java-secure-socket-extension-jsse-reference-guide.html#GUID-ABE2057C-0F36-48E1-8E76-4FC8D72A6573)
    -   [Support Classes and
        Interfaces](java-secure-socket-extension-jsse-reference-guide.html#GUID-AD2529FD-8778-4A02-B544-5F58E083774B)
        -   [The SSLContext
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-C281CAF3-275F-4DE4-8B47-4A84363CF39F)
            -   [Obtaining and Initializing the SSLContext
                Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-1F3F9B1E-143A-4C05-922E-152EA1DFAE90)
            -   [Creating an SSLContext
                Object](java-secure-socket-extension-jsse-reference-guide.html#GUID-9BAC1902-A203-4422-8163-61D64ADD2FF7)
        -   [The TrustManager
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-42CA1099-42AD-4772-BC4A-29C2A78E3EC9)
        -   [The TrustManagerFactory
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-AB5DA59B-B070-4AC5-A9C1-C3C30BF9209F)
            -   [Creating a
                TrustManagerFactory](java-secure-socket-extension-jsse-reference-guide.html#GUID-CF1771C6-D881-48E3-BB0D-49DC3E7C893B)
            -   [PKIX TrustManager
                Support](java-secure-socket-extension-jsse-reference-guide.html#GUID-ED23411A-B4AA-4E46-A5E9-619A0CF30151)
        -   [The X509TrustManager
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-7932AB21-2FED-402E-A806-3088402BAEA6)
            -   [Creating an
                X509TrustManager](java-secure-socket-extension-jsse-reference-guide.html#GUID-32CF3420-56E8-4BC5-8D3B-1F6B4692A290)
            -   [Creating Your Own
                X509TrustManager](java-secure-socket-extension-jsse-reference-guide.html#GUID-E1205974-3249-4E40-83C0-5F89C7375CF4)
            -   [Updating the Keystore
                Dynamically](java-secure-socket-extension-jsse-reference-guide.html#GUID-43F18232-8DDE-4F0C-B2AB-0EE4B472B15F)
        -   [X509ExtendedTrustManager
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-BAAC4A6F-2705-4A16-874A-1CDF0E48B8E3)
            -   [Creating an
                X509ExtendedTrustManager](java-secure-socket-extension-jsse-reference-guide.html#GUID-A6B7B05A-3696-4F86-A05C-9500EEC91C2D)
            -   [Creating Your Own
                X509ExtendedTrustManager](java-secure-socket-extension-jsse-reference-guide.html#GUID-AC443CF8-4CBD-4B77-8733-46D8DA2E3248)
        -   [The KeyManager
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-997AB098-DDD7-40E2-9FD0-5AA3C83E1702)
        -   [The KeyManagerFactory
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-616A7E77-587C-44E0-9F69-92BEDF631D5F)
            -   [Creating a
                KeyManagerFactory](java-secure-socket-extension-jsse-reference-guide.html#GUID-65A7A023-AE02-4A95-8210-386AE6F18EB5)
        -   [The X509KeyManager
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-9C8442E4-279D-4E60-B4D0-3B1558C99F4F)
            -   [Creating an
                X509KeyManager](java-secure-socket-extension-jsse-reference-guide.html#GUID-FEA439FF-8110-4F2D-82AF-54815002805E)
            -   [Creating Your Own
                X509KeyManager](java-secure-socket-extension-jsse-reference-guide.html#GUID-E0A44B4B-A888-4997-AB5E-5E0580FF87DE)
        -   [The X509ExtendedKeyManager
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-5C4AC46A-DE04-4D72-B94A-35C1F1B94A41)
        -   [Relationship Between a TrustManager and a
            KeyManager](java-secure-socket-extension-jsse-reference-guide.html#GUID-9D7375F9-D688-436D-A214-02653F50ED32)
    -   [Secondary Support Classes and
        Interfaces](java-secure-socket-extension-jsse-reference-guide.html#GUID-1B0C19BB-0F27-4757-9CA5-D03037C4E658)
        -   [The SSLParameters
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-BC9AD59B-05B6-4ACA-9CDD-D18ACEA3840D)
            -   [Cipher Suite
                Preference](java-secure-socket-extension-jsse-reference-guide.html#GUID-EFC2FACC-680C-42CE-A3A9-E9A6673EA813)
        -   [The SSLSessionContext
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-4E20A067-B139-4754-B4B3-AAF372F76D02)
        -   [The SSLSessionBindingListener
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-F2F8AC17-849A-40EE-A385-FD15328999B6)
        -   [The SSLSessionBindingEvent
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-C32994C1-0F5E-42D0-9CB6-EF4422024730)
        -   [The HandShakeCompletedListener
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-DFBAA9D1-C08B-48C9-88FE-F88003A6A6C7)
        -   [The HandShakeCompletedEvent
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-F242B876-6932-4B17-A755-1D9AFA25E54B)
        -   [The HostnameVerifier
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-9E46E5AA-FE3E-48D7-B616-98A143F74587)
        -   [The X509Certificate
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-1B4C6B3B-CDB3-433D-8F24-41EF5DE2FA5F)
        -   [The AlgorithmConstraints
            Interface](java-secure-socket-extension-jsse-reference-guide.html#GUID-54BC5FB3-3841-4005-A876-9FA2F49B2D0F)
        -   [The StandardConstants
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-651B5070-F586-4504-A6CD-8BEB2D928D47)
        -   [The SNIServerName
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-ADD484B7-244A-4FBC-AEF0-96873890CD6B)
        -   [The SNIMatcher
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-073F0493-3DB8-4388-818B-83E92021EF45)
        -   [The SNIHostName
            Class](java-secure-socket-extension-jsse-reference-guide.html#GUID-E10158C4-E808-41B7-9958-A119927743D8)
-   [Customizing
    JSSE](java-secure-socket-extension-jsse-reference-guide.html#GUID-A41282C3-19A3-400A-A40F-86F4DA22ABA9)
    -   [How to Specify a java.lang.System
        Property](java-secure-socket-extension-jsse-reference-guide.html#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363)
    -   [How to Specify a java.security.Security
        Property](java-secure-socket-extension-jsse-reference-guide.html#GUID-38CC6235-823B-49D7-A566-4BEA1B64C9C6)
    -   [Customizing the X509Certificate
        Implementation](java-secure-socket-extension-jsse-reference-guide.html#GUID-F196CEDD-DC14-40EA-852A-133DB9BA798B)
    -   [Specifying Default Enabled Cipher
        Suites](java-secure-socket-extension-jsse-reference-guide.html#GUID-D61663E8-2405-4B2D-A1F1-B8C7EA2688DB)
    -   [Specifying an Alternative HTTPS Protocol
        Implementation](java-secure-socket-extension-jsse-reference-guide.html#GUID-7EBD6A94-9ADE-4321-8915-17B3763F8E77)
    -   [Customizing the Provider
        Implementation](java-secure-socket-extension-jsse-reference-guide.html#GUID-8BC473B2-CD64-4E8B-8136-80BB286091B1)
    -   [Registering the Cryptographic Provider
        Statically](java-secure-socket-extension-jsse-reference-guide.html#GUID-59723547-D466-44C9-B066-EC5098B508E6)
    -   [Registering the Cryptographic Service Provider
        Dynamically](java-secure-socket-extension-jsse-reference-guide.html#GUID-D5D3557F-069E-48CE-8586-94BCC2B0203A)
    -   [Provider
        Configuration](java-secure-socket-extension-jsse-reference-guide.html#GUID-9F841002-E08F-48A6-BC57-7D15DE6575DA)
    -   [Configuring the Preferred Provider for Specific
        Algorithms](java-secure-socket-extension-jsse-reference-guide.html#GUID-C3441400-9D82-4545-ADAE-0C332EA4AC58)
    -   [Customizing the Default Keystores and Truststores, Store Types,
        and Store
        Passwords](java-secure-socket-extension-jsse-reference-guide.html#GUID-7D9F43B8-AABF-4C5B-93E6-3AFB18B66150)
    -   [Customizing the Default Key Managers and Trust
        Managers](java-secure-socket-extension-jsse-reference-guide.html#GUID-0ACD9274-607C-49BE-AED9-BEE2B4F2BEF2)
    -   [Disabled and Restricted Cryptographic
        Algorithms](java-secure-socket-extension-jsse-reference-guide.html#GUID-0A438179-32A7-4900-A81C-29E3073E1E90)
    -   [Customizing the Encryption Algorithm
        Providers](java-secure-socket-extension-jsse-reference-guide.html#GUID-316FB978-7588-442E-B829-B4973DB3B584)
    -   [Customizing Size of Ephemeral Diffie-Hellman
        Keys](java-secure-socket-extension-jsse-reference-guide.html#GUID-D9B216E8-3EFC-4882-B76E-17A87D8F2F9D)
    -   [Customizing Maximum Fragment Length Negotiation (MFLN)
        Extension](java-secure-socket-extension-jsse-reference-guide.html#GUID-41D5F11E-81BD-4C03-A315-48016D9B9B36)
    -   [Configuring the Maximum and Minimum Packet
        Size](java-secure-socket-extension-jsse-reference-guide.html#GUID-3C9ADC85-E82C-421E-808D-F06028838F47)
-   [Transport Layer Security (TLS) Renegotiation
    Issue](java-secure-socket-extension-jsse-reference-guide.html#GUID-9C767872-3A6C-4AD1-9805-49F112A0FA28)
    -   [Phased Approach to Fixing This
        Issue](java-secure-socket-extension-jsse-reference-guide.html#GUID-E41EDAB4-D1D7-4224-B3A4-E08D74E9CE04)
    -   [Description of the Phase 2
        Fix](java-secure-socket-extension-jsse-reference-guide.html#GUID-475E6316-283A-4A59-9B11-2479348C4629)
    -   [Workarounds and Alternatives to SSL/TLS
        Renegotiation](java-secure-socket-extension-jsse-reference-guide.html#GUID-D2B6262D-B052-4757-9087-3CBD61B3CE8A)
    -   [TLS Implementation
        Details](java-secure-socket-extension-jsse-reference-guide.html#GUID-7CC1B0FD-BDCB-4F56-847D-D4FDDC7F8747)
    -   [Description of the Phase 1
        Fix](java-secure-socket-extension-jsse-reference-guide.html#GUID-67842028-3E8F-49E0-A0C1-63F480408412)
    -   [Allow Unsafe Server Certificate Change in SSL/TLS
        Renegotiations](java-secure-socket-extension-jsse-reference-guide.html#GUID-9A577D22-9DED-407E-9F16-5C006E3F3BF3)
-   [Hardware Acceleration and Smartcard
    Support](java-secure-socket-extension-jsse-reference-guide.html#GUID-3151D7C3-7CE3-41B6-BF65-295B259C63A6)
    -   [Configuring JSSE to Use Smartcards as Keystores and
        Truststores](java-secure-socket-extension-jsse-reference-guide.html#GUID-3412BD4D-9B6F-4FF0-A11C-ABA5945B40AE)
    -   [Multiple and Dynamic
        Keystores](java-secure-socket-extension-jsse-reference-guide.html#GUID-C236C41B-54CA-4095-986B-7C62BBC419FB)
-   [Kerberos Cipher
    Suites](java-secure-socket-extension-jsse-reference-guide.html#GUID-67227445-EE66-4F33-BEED-535C548BCC73)
    -   [Kerberos
        Requirements](java-secure-socket-extension-jsse-reference-guide.html#GUID-2CEBB012-B3E0-44FB-B935-8A95E184AF84)
    -   [Peer Identity
        Information](java-secure-socket-extension-jsse-reference-guide.html#GUID-3D49787E-4D31-4D65-8FFE-CE19B6CAD3E2)
    -   [Security
        Manager](java-secure-socket-extension-jsse-reference-guide.html#GUID-B583D760-8D38-4B3F-94FA-66E63AFCE1D1)
-   [Additional Keystore Formats
    (PKCS12)](java-secure-socket-extension-jsse-reference-guide.html#GUID-93EBE6F4-1460-450A-8D9C-AF086C233BDF)
-   [Server Name Indication (SNI)
    Extension](java-secure-socket-extension-jsse-reference-guide.html#GUID-82B884DF-AA3D-4FE1-8991-9C3F14044C4F)
-   [TLS Application Layer Protocol
    Negotiation](java-secure-socket-extension-jsse-reference-guide.html#GUID-DC583ED6-06AD-435C-BC9C-763F4642B2B3)
    -   [Setting up ALPN on the
        Client](java-secure-socket-extension-jsse-reference-guide.html#GUID-CBFA212F-C726-4D58-A520-A4BE147D1290)
    -   [Setting up Default ALPN on the
        Server](java-secure-socket-extension-jsse-reference-guide.html#GUID-59618539-24AD-431E-84E3-585C4C4BF4E5)
    -   [Setting up Custom ALPN on the
        Server](java-secure-socket-extension-jsse-reference-guide.html#GUID-B17DF013-83BD-4A00-BF91-D9E1E0BE70D8)
    -   [Determining Negotiated ALPN Value during
        Handshaking](java-secure-socket-extension-jsse-reference-guide.html#GUID-BB4A54B3-FBC2-4B32-91CA-A16F91467ED9)
    -   [ALPN Related Classes and
        Methods](java-secure-socket-extension-jsse-reference-guide.html#GUID-6D774DB6-FD5C-4066-B144-C1F10E2DD742)
-   [Troubleshooting
    JSSE](java-secure-socket-extension-jsse-reference-guide.html#GUID-D8F6E432-12F2-47B8-9FD0-CE57A4A4F2E1)
    -   [Configuration
        Problems](java-secure-socket-extension-jsse-reference-guide.html#GUID-E8E3C6C4-5B7E-466F-B11C-35BF3B9F454D)
        -   [CertificateException While
            Handshaking](java-secure-socket-extension-jsse-reference-guide.html#GUID-E87F514E-A7E8-4E79-90DE-D375FF64A908)
        -   [Runtime Exception: SSL Service Not
            Available](java-secure-socket-extension-jsse-reference-guide.html#GUID-48170215-4EF1-4653-B58F-81572E9FE23F)
        -   [Runtime Exception: \"No available certificate corresponding
            to the SSL cipher suites which are
            enabled\"](java-secure-socket-extension-jsse-reference-guide.html#GUID-92715704-80F4-431A-BF99-D583EE61C4AB)
        -   [Runtime Exception: No Cipher Suites in
            Common](java-secure-socket-extension-jsse-reference-guide.html#GUID-1409C7FD-0E15-4367-93F5-EB327099D8B5)
        -   [Socket Disconnected After Sending ClientHello
            Message](java-secure-socket-extension-jsse-reference-guide.html#GUID-B20D551B-9558-43C5-94D8-BF5464C8F2B7)
        -   [SunJSSE Cannot Find a JCA Provider That Supports a Required
            Algorithm and Causes a
            NoSuchAlgorithmException](java-secure-socket-extension-jsse-reference-guide.html#GUID-85667451-803E-4E07-B366-00E19790595B)
        -   [FailedDownloadException Thrown When Trying to Obtain
            Application Resources from Web Server over
            SSL](java-secure-socket-extension-jsse-reference-guide.html#GUID-BEA0A351-848D-4E0E-9B96-48B27FDED1BA)
        -   [IllegalArgumentException When RC4 Cipher Suites are
            Configured for
            DTLS](java-secure-socket-extension-jsse-reference-guide.html#GUID-001B7524-87A4-4085-B8EF-929E0503DBEC)
    -   [Debugging
        Utilities](java-secure-socket-extension-jsse-reference-guide.html#GUID-31B7E142-B874-46E9-8DD0-4E18EC0EB2CF)
        -   [Debugging SSL/TLS
            Connections](java-secure-socket-extension-jsse-reference-guide.html#GUID-4D421910-C36D-40A2-8BA2-7D42CCBED3C6)
-   [Code
    Examples](java-secure-socket-extension-jsse-reference-guide.html#GUID-0573BCE4-05C4-429C-8ECC-3D3D8CA807F4)
    -   [Converting an Unsecure Socket to a Secure
        Socket](java-secure-socket-extension-jsse-reference-guide.html#GUID-AB802E5F-07CE-468D-AC7C-7EBCAAE119AD)
    -   [Running the JSSE Sample
        Code](java-secure-socket-extension-jsse-reference-guide.html#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA)
    -   [Creating a Keystore to Use with
        JSSE](java-secure-socket-extension-jsse-reference-guide.html#GUID-3D26386B-BC7A-41BB-AC70-80E6CD147D6F)
    -   [Using the Server Name Indication (SNI)
        Extension](java-secure-socket-extension-jsse-reference-guide.html#GUID-63945B45-E909-483F-B3A9-E26586737383)
        -   [Typical Client-Side Usage
            Examples](java-secure-socket-extension-jsse-reference-guide.html#GUID-BCCE0D1F-08D8-4608-8A5A-5BFA54FED2C0)
        -   [Typical Server-Side Usage
            Examples](java-secure-socket-extension-jsse-reference-guide.html#GUID-FA9C8332-B6D9-48E6-AF66-700E00B829D2)
        -   [Working with Virtual
            Infrastructures](java-secure-socket-extension-jsse-reference-guide.html#GUID-0D1E93B9-F63F-46E6-B8A9-0E3AF3207445)
-   [Standard
    Names](java-secure-socket-extension-jsse-reference-guide.html#GUID-847CA40C-F439-4A31-A7FA-C37B4DEC2190)
-   [Provider
    Pluggability](java-secure-socket-extension-jsse-reference-guide.html#GUID-08173142-567C-495C-A48F-32D0FCED466B)
-   [JSSE Cipher Suite
    Parameters](java-secure-socket-extension-jsse-reference-guide.html#GUID-09C3A453-AAAB-4D8B-830A-558B3F30BDF3)

[<span class="secnum">9</span> Running the JSSE Sample Code](running-jsse-sample-code1.htm) {#running-the-jsse-sample-code .tocheader}
-------------------------------------------------------------------------------------------

-   [Sample Truststores](sample-truststores.htm)
-   [Sample Code Illustrating a Secure Socket Connection Between a
    Client and a
    Server](sample-code-illustrating-secure-socket-connection-client-and-server.html#GUID-A4D59ABB-62AF-4FC0-900E-A795FDC84E41)
    -   [Configuration Requirements for SSL Socket
        Samples](sample-code-illustrating-secure-socket-connection-client-and-server.html#GUID-B1060A74-9BAE-40F1-AB2B-C8D83812A4C7)
    -   [Running
        SSLSocketClient](sample-code-illustrating-secure-socket-connection-client-and-server.html#GUID-AA1C27A1-2CA8-4309-B281-D6199F60E666)
    -   [Running
        SSLSocketClientWithTunnelling](sample-code-illustrating-secure-socket-connection-client-and-server.html#GUID-B9103D0C-3E6A-4301-B558-461E4CB23DC9)
    -   [Running
        SSLSocketClientWithClientAuth](sample-code-illustrating-secure-socket-connection-client-and-server.html#GUID-756AE510-E1BF-42FE-92FC-B9BE3EC31C7B)
    -   [Running
        ClassFileServer](sample-code-illustrating-secure-socket-connection-client-and-server.html#GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C)
    -   [Running SSLSocketClientWithClientAuth with
        ClassFileServer](sample-code-illustrating-secure-socket-connection-client-and-server.html#GUID-1B7038DC-7564-4EE6-A1DF-6B1445077E2E)
-   [Sample Code Illustrating HTTPS
    Connections](sample-code-illustrating-https-connections.html#GUID-54F1F19F-0F93-4877-A4A1-46ACD03FD7CB)
    -   [Running
        URLReader](sample-code-illustrating-https-connections.html#GUID-BC38D378-DF50-4B41-8489-67B6AB621FAB)
    -   [Running
        URLReaderWithOptions](sample-code-illustrating-https-connections.html#GUID-20E68036-A8A2-4297-8074-44D076845E00)
-   [Sample Code Illustrating a Secure RMI
    Connection](sample-code-illustrating-secure-rmi-connection.html#GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87)
-   [Sample Code Illustrating the Use of an
    SSLEngine](sample-code-illustrating-use-sslengine.html#GUID-EDE915F0-427B-48C7-918F-23C44384B862)
    -   [Running
        SSLEngineSimpleDemo](sample-code-illustrating-use-sslengine.html#GUID-3DB6AE99-C0BA-49D1-9ABD-DEF439A965E6)
-   [Troubleshooting JSSE Sample
    Code](troubleshooting-jsse-sample-code.htm)

[<span class="secnum">10</span> Java PKI Programmers Guide](java-pki-programmers-guide.html#GUID-650D0D53-B617-4055-AFD3-AF5C2629CBBF) {#java-pki-programmers-guide .tocheader}
-------------------------------------------------------------------------------------------------------------------------------------

-   [PKI Programmers Guide
    Overview](java-pki-programmers-guide.html#GUID-D6A18B1E-A2A8-4CA2-BD18-514CD807810E)
    -   [Introduction to Public Key
        Certificates](java-pki-programmers-guide.html#GUID-2EFB901C-9ED1-4823-9311-B05B49E34AEA)
    -   [X.509 Certificates and Certificate Revocation Lists
        (CRLs)](java-pki-programmers-guide.html#GUID-8DEBED06-13C6-4608-8C74-7C8144EF0D23)
-   [Core Classes and
    Interfaces](java-pki-programmers-guide.html#GUID-271526C4-6095-4233-9F7F-0CD0C62BDA93)
    -   [Basic Certification Path
        Classes](java-pki-programmers-guide.html#GUID-2D30176C-EE5A-41F8-896B-1A16E7F786B8)
        -   [The CertPath
            Class](java-pki-programmers-guide.html#GUID-E47B8A0E-6B3A-4B49-994D-CF185BF441EC)
        -   [The CertificateFactory
            Class](java-pki-programmers-guide.html#GUID-BCABADD4-C0DC-4987-B187-F086B4BCE195)
        -   [The CertPathParameters
            Interface](java-pki-programmers-guide.html#GUID-2AF52C1B-8EE2-4D65-9273-F7AC523AB42F)
    -   [Certification Path Validation
        Classes](java-pki-programmers-guide.html#GUID-C825028D-5F30-4041-ACC4-466657F59F02)
        -   [The CertPathValidator
            Class](java-pki-programmers-guide.html#GUID-808C1A6D-6A67-4026-A9DE-223A428EC80A)
        -   [The CertPathValidatorResult
            Interface](java-pki-programmers-guide.html#GUID-29AC2D33-7518-4DEA-A4CC-544CB174B915)
    -   [Certification Path Building
        Classes](java-pki-programmers-guide.html#GUID-CBABC770-E714-4E6C-AD40-EA680BE91C20)
        -   [The CertPathBuilder
            Class](java-pki-programmers-guide.html#GUID-BEFCC824-21C1-4AD3-B670-D0CA01F08D95)
        -   [The CertPathBuilderResult
            Interface](java-pki-programmers-guide.html#GUID-47B1564D-DFC3-4F0F-A006-CB7303EDD919)
    -   [Certificate/CRL Storage
        Classes](java-pki-programmers-guide.html#GUID-AB96FD45-6F8A-4785-B6C5-082BEB6CDA5E)
        -   [The CertStore
            Class](java-pki-programmers-guide.html#GUID-5404B79C-3D49-4668-974C-1BACD1A98B73)
        -   [The CertStoreParameters
            Interface](java-pki-programmers-guide.html#GUID-BC87018F-F888-4905-8ED4-AE574C646AF2)
        -   [The CertSelector and CRLSelector
            Interfaces](java-pki-programmers-guide.html#GUID-263AAFB6-DC37-4B64-95E7-60D59D7728B5)
            -   [The X509CertSelector
                Class](java-pki-programmers-guide.html#GUID-2229C26E-1196-4E4F-8F23-731CE5CA254E)
            -   [The X509CRLSelector
                Class](java-pki-programmers-guide.html#GUID-08C0B832-6934-4A28-8932-8CEB87259BA8)
    -   [PKIX
        Classes](java-pki-programmers-guide.html#GUID-5BBEF087-CA8A-4287-97FB-BD88DCD12FE5)
        -   [The TrustAnchor
            Class](java-pki-programmers-guide.html#GUID-772D31A0-FF9B-4A1E-985B-2100177C74F9)
        -   [The PKIXParameters
            Class](java-pki-programmers-guide.html#GUID-3D95A3BE-74CB-4357-BB85-9A8DEA36A457)
        -   [The PKIXCertPathValidatorResult
            Class](java-pki-programmers-guide.html#GUID-DF6CA960-B37A-4EE1-9E43-76561F711A7D)
        -   [The PolicyNode Interface and PolicyQualifierInfo
            Class](java-pki-programmers-guide.html#GUID-3AD41382-E729-469B-83EE-CB2FE66D71D8)
        -   [The PKIXBuilderParameters
            Class](java-pki-programmers-guide.html#GUID-BB092D65-80CA-457E-A7B4-F1B41A1A674A)
        -   [The PKIXCertPathBuilderResult
            Class](java-pki-programmers-guide.html#GUID-BF0E3B2B-1DA5-4A95-A8DD-C03C04EA70E7)
        -   [The PKIXCertPathChecker
            Class](java-pki-programmers-guide.html#GUID-D46630F6-939D-4054-A451-3D8206ED4E62)
        -   [Using PKIXCertPathChecker in Certificate Path
            Validation](java-pki-programmers-guide.html#GUID-F727578E-71D0-4BC5-9B06-47EE13F9CBCF)
            -   [Check Revocation Status of Certificates with
                PKIXRevocationChecker
                Class](java-pki-programmers-guide.html#GUID-43A3A247-E165-408C-AD74-88A75BFB4750)
-   [Implementing a Service
    Provider](java-pki-programmers-guide.html#GUID-266DD62E-39A7-435B-90DF-7EB1425D56E1)
    -   [Steps to Implement and Integrate a
        Provider](java-pki-programmers-guide.html#GUID-BFF21E4E-30F9-4D92-BD1E-C530DD33609F)
        -   [Service
            Interdependencies](java-pki-programmers-guide.html#GUID-255CC70E-E05E-4109-AA6E-51B83C5A3618)
        -   [Certification Path Parameter Specification
            Interfaces](java-pki-programmers-guide.html#GUID-5C8A1966-6636-475F-B533-3D080DB0653A)
        -   [Certification Path Result Specification
            Interfaces](java-pki-programmers-guide.html#GUID-67EDE244-431F-4382-9384-B5CBD8163C05)
        -   [Certification Path Exception
            Classes](java-pki-programmers-guide.html#GUID-C6FC73C4-E9CA-45A2-A135-5E81FA345F5F)
-   [Appendix A: Standard
    Names](java-pki-programmers-guide.html#GUID-EF1585DC-20BF-4140-B71E-0A8528D4A57D)
-   [Appendix B: CertPath Implementation in SUN
    Provider](java-pki-programmers-guide.html#GUID-EB250086-0AC1-4D60-AE2A-FC7461374746)
-   [Appendix C: OCSP
    Support](java-pki-programmers-guide.html#GUID-E6E737DB-4000-4005-969E-BCD0238B1566)
-   [Appendix D: CertPath Implementation in JdkLDAP
    Provider](java-pki-programmers-guide.html#GUID-FF62B0E3-E57A-4F40-970A-0481AF750CCD)
-   [Appendix E: Disabling Cryptographic
    Algorithms](java-pki-programmers-guide.html#GUID-D2A99DE3-62CF-4E4B-BF91-814C4A5C4DD3)

[<span class="secnum">11</span> Java SASL API Programming and Deployment Guide](java-sasl-api-programming-and-deployment-guide1.html#GUID-6D78EE33-62E6-4D85-9695-322EED493F72) {#java-sasl-api-programming-and-deployment-guide .tocheader}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   [Java SASL API
    Overview](java-sasl-api-programming-and-deployment-guide1.html#GUID-6F735DD5-1648-4BB7-A4BC-D001DC3B82AC)
    -   [Creating the
        Mechanisms](java-sasl-api-programming-and-deployment-guide1.html#GUID-7CFF731F-8330-40D6-8841-C1FB07C73655)
    -   [Passing Input to the
        Mechanisms](java-sasl-api-programming-and-deployment-guide1.html#GUID-90092190-14A7-48F9-923A-A37FDCC28D6B)
    -   [Using the
        Mechanisms](java-sasl-api-programming-and-deployment-guide1.html#GUID-F3774782-A395-48C9-A9BD-10C9F25FFE50)
    -   [Using the Negotiated Security
        Layer](java-sasl-api-programming-and-deployment-guide1.html#GUID-762BDD49-6EE8-419C-A45E-540462CB192B)
-   [How SASL Mechanisms are Installed and
    Selected](java-sasl-api-programming-and-deployment-guide1.html#GUID-93982F1C-AFFE-47B9-B4BA-41551ECCE2D2)
-   [The SunSASL
    Provider](java-sasl-api-programming-and-deployment-guide1.html#GUID-2F50B103-FE9F-459F-9EC5-B708358A7B59)
    -   [The SunSASL Provider Client
        Mechanisms](java-sasl-api-programming-and-deployment-guide1.html#GUID-681CD78D-D2E4-43DE-9225-249AA83FF177)
    -   [The SunSASL Provider Server
        Mechanisms](java-sasl-api-programming-and-deployment-guide1.html#GUID-0D61D8E5-31E8-4F26-9BD2-9AF92F5318F9)
-   [The JdkSASL
    Provider](java-sasl-api-programming-and-deployment-guide1.html#GUID-B6A1E089-0C59-413F-ABF6-E73F44F89E6A)
    -   [The JdkSASL Provider Client
        Mechanism](java-sasl-api-programming-and-deployment-guide1.html#GUID-6B2412AB-D5BC-4C8A-9DA7-515E32DDE971)
    -   [The JdkSASL Provider Server
        Mechanism](java-sasl-api-programming-and-deployment-guide1.html#GUID-F815A77D-744E-4914-9963-886A1B10FC3C)
-   [Debugging and
    Monitoring](java-sasl-api-programming-and-deployment-guide1.html#GUID-10BCFA2D-E33C-4A11-BDD4-012B5713F430)
-   [Implementing a SASL Security
    Provider](java-sasl-api-programming-and-deployment-guide1.html#GUID-A21D50AD-3730-4FE6-A13B-75529607E068)

[<span class="secnum">12</span> XML Digital Signature API Overview and Tutorial](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-DB46A001-6DBD-4571-BDBC-1BBC394BF61E) {#xml-digital-signature-api-overview-and-tutorial .tocheader}
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-   [Package
    Hierarchy](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-BBFA7B90-3EA2-49DE-964B-8A60D4134343)
-   [Service
    Providers](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-A32C5AC5-08F9-4316-9D63-0CDEAC3A5405)
-   [Introduction to XML
    Signatures](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-E11E6051-5F30-4DDA-A4EE-5F9C1AB1F7B8)
    -   [Example of an XML
        Signature](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-E5A89234-A67A-4999-8E31-6D6C26B9BAAF)
-   [XML Signature Secure Validation
    Mode](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-8618C294-3BFE-45C3-9A1E-C4629E337E68)
-   [XML Digital Signature API
    Examples](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-E7E9239F-C973-4D05-AC3F-53F714C259DB)
    -   [Validate
        Example](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-22AB40C4-45EC-4714-91A2-CFB59EC05AA0)
        -   [Validating an XML
            Signature](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-28D86779-8D2A-4741-8D78-49830EFF9473)
        -   [Instantiating the Document that Contains the
            Signature](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-B2651FD1-F5CD-49D1-8541-466ABAB7ECA8)
        -   [Specifying the Signature Element to be
            Validated](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-66D2F1B6-2D1E-4721-B70B-4BA32103A79E)
        -   [Creating a Validation
            Context](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-FCBFE214-3F87-412D-BC0F-EC4CE1519529)
        -   [Unmarshalling the XML
            Signature](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-B5297B69-8989-4D40-994D-C40ED0C71C94)
        -   [Validating the XML
            Signature](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-CF8C37C4-7360-4833-83FB-6A2948C26818)
            -   [What If the XML Signature Fails to
                Validate?](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-20CF389E-3F3F-4156-B8A3-CFB411E75274)
        -   [Using
            KeySelectors](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-26946ED1-1BBE-4AFD-B1CA-5A6A46FD7354)
    -   [GenEnveloped
        Example](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-1152D2A5-ECBB-4727-9B0F-1941E4171108)
        -   [Generating an XML
            Signature](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-177088CC-2CFD-477D-BB05-E8B9C48AE270)
        -   [Instantiating the Document to be
            Signed](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-37E2785A-6ACD-4E09-9A72-4F6AE9A641D9)
        -   [Creating a Public Key
            Pair](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-A0C0D616-CD13-441C-A1A2-122431692B9F)
        -   [Creating a Signing
            Context](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-2FA5FBA6-8DB7-460D-BDEA-2BF38B14BC19)
        -   [Assembling the XML
            Signature](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-3DEB54D1-220A-4140-832D-DD42976057B6)
        -   [Generating the XML
            Signature](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-3B6E8DE8-AC10-46B2-BC89-9E0B2CE8634C)
        -   [Printing or Displaying the Resulting
            Document](java-xml-digital-signature-api-overview-and-tutorial.html#GUID-1D6C3745-9E04-400A-ADD1-65E5FD3ADB5C)

[<span class="secnum">13</span> Security API Specification](security-api-specification1.htm) {#security-api-specification .tocheader}
--------------------------------------------------------------------------------------------

[<span class="secnum">14</span> Deprecated Security APIs Marked for Removal](deprecated-security-apis-marked-removal.htm) {#deprecated-security-apis-marked-for-removal .tocheader}
-------------------------------------------------------------------------------------------------------------------------

[<span class="secnum">15</span> Security Tools](security-tools.htm) {#security-tools .tocheader}
-------------------------------------------------------------------

[<span class="secnum">16</span> Related Security Topics](security-tutorials.htm) {#related-security-topics .tocheader}
--------------------------------------------------------------------------------

</div>
<!-- class="ind" --> <!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   --                 |
| -------------------- | [ |   --                 |
| ------ --            | O |                      |
|    [![Next](../../dc | r |                      |
| ommon/gifs/rightnav. | a |                      |
| gif)\                | c |                      |
|    <span class="icon | l |                      |
| ">Next</span>](title | e |                      |
| .htm)                | L |                      |
|   ------------------ | o |                      |
| -------------------- | g |                      |
| ------ --            | o |                      |
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
