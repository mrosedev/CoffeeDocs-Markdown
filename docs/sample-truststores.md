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

  -------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------- --
             [![Previous](../../dcommon/gifs/leftnav.gif)\                                             [![Next](../../dcommon/gifs/rightnav.gif)\                                 
   <span class="icon">Previous</span>](running-jsse-sample-code1.htm)   <span class="icon">Next</span>](sample-code-illustrating-secure-socket-connection-client-and-server.htm)  
  -------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-51A0A134-F222-4B69-ACCA-C5542AA7D9C8}<!-- End Header -->

Sample Truststores {#JSSEC-GUID-51A0A134-F222-4B69-ACCA-C5542AA7D9C8 .sect1}
==================

<div>
This bundle includes sample keystore files that are used with the sample
code. They are stored in the \"JKS\" keystore format, which is the
default format used by Oracle\' JDK implementation. (If another keystore
format is desired, the JDK will need to be configured to recognize the
new default format.)

JSSE uses the following certificate keystore files to authenticate the
clients and servers.

-   `*/testkeys`

    These files are used by the code samples as the source of
    public/private key and certificate material. In the client program
    directories, the `testkeys` files contains the certificate entry for
    the Java mascot `Duke`{.codeph}. In the server program directories
    (`./sockets/server` and `rmi`), the file contains a certificate
    entry for the server `localhost`{.codeph}.

    The sample code expects the `testkeys` file to be in the current
    working directory.

    <div class="infoboxnote" id="GUID-51A0A134-F222-4B69-ACCA-C5542AA7D9C8__GUID-690DA2D7-55E0-4BC4-90FF-28477E283A1A">
    Note:

    These are very simple certificates and are not appropriate for a
    production environment, but they should be sufficient for running
    the samples here.

    The password for these keystores is: `passphrase`{.codeph}

    </div>
-   `samplecacerts`

    This truststore file is very similar to the stock JDK `cacerts`
    file, in that it contains trust certificates from several vendors.
    It also contains the trusted certificates from
    <span class="apiname">Duke</span> and
    <span class="apiname">localhost</span> above.

    The password for this keystore is the same as the JDK `cacert`\'s
    initial password: `changeit`{.codeph}

    Please see your provider\'s documentation for how to configure the
    location of your trusted certificate file.

    <div class="infoboxnote" id="GUID-51A0A134-F222-4B69-ACCA-C5542AA7D9C8__GUID-7609AE78-4064-408A-AE25-DEACF27E7B1A">
    Note:

    Users of the JDK can specify the location of the truststore by using
    one of the following methods:

    </div>
    1.  System properties:

        ``` {.oac_no_warn dir="ltr"}
        java -Djavax.net.ssl.trustStore=samplecacerts \
             -Djavax.net.ssl.trustStorePassword=changeit Application
        ```

    2.  Install the file into:

        ``` {.oac_no_warn dir="ltr"}
        <java-home>/lib/security/jssecacerts
        ```

    3.  Install the file into:

        ``` {.oac_no_warn dir="ltr"}
        <java-home>/lib/security/cacerts
        ```

    If you choose (2) or (3), be sure to replace this file with a
    production `cacerts` file before deployment.

The utility `keytool`{.codeph} can be used to generate alternate
certificates and keystore files.

<div class="infoboxnote" id="GUID-51A0A134-F222-4B69-ACCA-C5542AA7D9C8__GUID-CBA42D99-0211-4BB8-9854-EC0115A00153">
Note:

Ensure that you verify your `cacerts` file. Since you trust the CAs in
the `cacerts` file as entities for signing and issuing certificates to
other entities, you must manage the `cacerts` file carefully. The
`cacerts` file should contain only certificates of the entities and CAs
you trust. It is your responsibility to verify the trusted root CA
certificates bundled in the `cacerts` file and make your own trust
decisions. To remove an untrusted CA certificate from the `cacerts`
file, use the delete option of the `keytool`{.codeph} command. You can
find the `cacerts` file in the jre installation directory. Contact your
system administrator if you do not have permission to edit this file.

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
| ---------- --------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| ----------------- -- | L |             <span cl |
|              [![Prev | o | ass="icon">Contents< |
| ious](../../dcommon/ | g | /span>](toc.htm)     |
| gifs/leftnav.gif)\   | o |   -- --------------- |
|                      | ] | -------------------- |
|                      | ( | -------------------- |
|    [![Next](../../dc | . | ---                  |
| ommon/gifs/rightnav. | . |                      |
| gif)\                | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](r | / |                      |
| unning-jsse-sample-c | d |                      |
| ode1.htm)   <span cl | c |                      |
| ass="icon">Next</spa | o |                      |
| n>](sample-code-illu | m |                      |
| strating-secure-sock | m |                      |
| et-connection-client | o |                      |
| -and-server.htm)     | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| ---------- --------- | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| ----------------- -- | a |                      |
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
