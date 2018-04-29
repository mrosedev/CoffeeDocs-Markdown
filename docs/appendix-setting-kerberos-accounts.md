<div class="header">
[]{#top}

<div class="zz-skip-header">
[Go to primary content](#BEGIN)

</div>


  ----------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------- --
                                                   [![Previous](../../dcommon/gifs/leftnav.gif)\                                                              [![Next](../../dcommon/gifs/rightnav.gif)\              
   <span class="icon">Previous</span>](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.htm)   <span class="icon">Next</span>](kerberos-5-gss-api-mechanism.htm)  
  ----------------------------------------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-D1F41B0A-E756-49CB-828A-422DC23E572B}<!-- End Header -->

Appendix A: Setting up Kerberos Accounts {#JSSEC-GUID-D1F41B0A-E756-49CB-828A-422DC23E572B .sect1}
========================================

<div>
Kerberos accounts are set up on the Key Distribution Center (KDC). Each
entry in the Kerberos database contains a Kerberos principal. You should
create a host-based principal for the machine that you will be running
the servers (e.g., \"host/j1hol-001\") and a client principal (e.g.,
\"test\") for accessing the servers.

For Solaris, please refer to following documentation on how to setup
Kerberos principals.

-   [Administering Kerberos
    Principals](https://docs.oracle.com/cd/E19963-01/html/821-1456/aadmin-1.html)

-   [System Administration Guide: Security
    Services](https://docs.oracle.com/cd/E19253-01/816-4557/)

For Windows, please refer to Microsoft documentation. Here are some
pointers.

-   [How To Create an Active Directory Server in Windows Server
    2003](http://support.microsoft.com/kb/324753)

-   [Microsoft
    Kerberos](http://msdn.microsoft.com/en-us/library/windows/desktop/aa378747%28v=vs.85%29.aspx)

-   [Interoperability with Microsoft Windows 2000 Active Directory and
    Kerberos
    Services](http://msdn.microsoft.com/en-us/library/windows/desktop/ms808911.aspx)

The exercises assume that the operating system has been configured to
use the correct Kerberos server. This configuration typically requires
administration privileges. If you cannot configure the operating system,
then you can use a Kerberos configuration file with your `java`{.codeph}
command by using the `-Djava.security.krb5.conf`{.codeph} option. Here
is an example of how to invoke one of the commands from the exercises to
use the
[`krb5.conf`](source-code-advanced-security-programming-java-se-authentication-secure-communication-and-single-sig.html#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__KRB5.CONF-338B7967)
configuration file.

``` {.oac_no_warn dir="ltr"}
% java -Djava.security.auth.login.config=jaas-krb5.conf\
  -Djava.security.krb5.conf=krb5.conf Jaas client
```

</div>
</div>
<!-- class="ind" --><!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------


</div>
<!-- class="footer" -->
