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

  -------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------- --
                                  [![Previous](../../dcommon/gifs/leftnav.gif)\                                                       [![Next](../../dcommon/gifs/rightnav.gif)\                       
   <span class="icon">Previous</span>](sample-code-illustrating-secure-socket-connection-client-and-server.htm)   <span class="icon">Next</span>](sample-code-illustrating-secure-rmi-connection.htm)  
  -------------------------------------------------------------------------------------------------------------- ------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-54F1F19F-0F93-4877-A4A1-46ACD03FD7CB}<!-- End Header -->

Sample Code Illustrating HTTPS Connections {#JSSEC-GUID-54F1F19F-0F93-4877-A4A1-46ACD03FD7CB .sect1}
==========================================

<div>
There are two primary APIs for accessing secure communications through
JSSE. One way is through a socket-level API that can be used for
arbitrary secure communications, as illustrated by the
[`SSLSocketClient.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-AA1C27A1-2CA8-4309-B281-D6199F60E666__SSLSOCKETCLIENT.JAVA-32CFECE1),
[`SSLSocketClientWithTunneling.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-B9103D0C-3E6A-4301-B558-461E4CB23DC9__SSLSOCKETCLIENTWITHTUNNELING.JAVA-32D03DB5),
and
[`SSLSocketClientWithClientAuth.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-756AE510-E1BF-42FE-92FC-B9BE3EC31C7B__SSLSOCKETCLIENTWITHCLIENTAUTH.JAVA-32D0CA6C)
examples (with and without the examples described in [Running
ClassFileServer](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C)).

A second, and often simpler, way is through the standard Java URL API.
You can communicate securely with an SSL-enabled web server by using the
HTTPS URL protocol or scheme using the
[<span class="apiname">java.net.URL</span>](https://docs.oracle.com/javase/10/docs/api/java/net/URL.html)
class.

Support for HTTPS URL schemes is implemented in many of the common
browsers, which allows access to secured communications without
requiring the socket-level API provided with JSSE. An example URL is
`https://www.verisign.com`{.codeph}.

The trust and key management for the HTTPS URL implementation is
environment-specific. The JSSE implementation provides an HTTPS URL
implementation. To use a different HTTPS protocol implementation, set
the `java.protocol.handler.pkgs`{.codeph} system property; see [How to
Specify a java.lang.System
Property](java-secure-socket-extension-jsse-reference-guide.htm#GUID-460C3E5A-A373-4742-9E84-EB42A7A3C363).

</div>
<div class="sect2">
[]{#GUID-BC38D378-DF50-4B41-8489-67B6AB621FAB}

Running URLReader {#JSSEC-GUID-BC38D378-DF50-4B41-8489-67B6AB621FAB .sect2}
-----------------

<div>
The example
[`URLReader.java`](sample-code-illustrating-https-connections.htm#GUID-BC38D378-DF50-4B41-8489-67B6AB621FAB__URLREADER.JAVA-33086510)
illustrates using a URL to access resources on a secure site. By
default, this example connects to `www.verisign.com`{.codeph}, but it
can be adapted to connect to
[`ClassFileServer.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C__CLASSFILESERVER.JAVA-3314B74B).
To do so, the URL will need to be modified to point to the correct
address. You may also need to update the server\'s certificate or
provide a custom <span class="apiname">HostNameVerifier</span> (see
[<span class="apiname">HttpsURLConnection</span>](https://docs.oracle.com/javase/10/docs/api/javax/net/ssl/HttpsURLConnection.html))
if the hostname in the server\'s certificate doesn\'t match the URL\'s
hostname.

<div class="infoboxnote" id="GUID-BC38D378-DF50-4B41-8489-67B6AB621FAB__GUID-19BA7A7B-2800-429C-A1F8-9536E5D75382">
Note:

If you are behind a firewall, you may need to set the
`https.proxyHost`{.codeph} and `https.proxyPort`{.codeph} system
properties to correctly specify the proxy.

</div>
<div class="section">
Usage

``` {.oac_no_warn dir="ltr"}
java URLReader
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-BC38D378-DF50-4B41-8489-67B6AB621FAB__URLREADER.JAVA-33086510">
URLReader.java

``` {.oac_no_warn dir="ltr"}
import java.net.*;
import java.io.*;

/*
 * This example illustrates using a URL to access resources
 * on a secure site.
 *
 * If you are running inside a firewall, please also set the following
 * Java system properties to the appropriate value:
 *
 *   https.proxyHost = <secure proxy server hostname>
 *   https.proxyPort = <secure proxy server port>
 *
 */

public class URLReader {
    public static void main(String[] args) throws Exception {
        URL verisign = new URL("https://www.verisign.com/");
        BufferedReader in = new BufferedReader(
                                new InputStreamReader(
                                verisign.openStream()));

        String inputLine;

        while ((inputLine = in.readLine()) != null)
            System.out.println(inputLine);

        in.close();
    }
}
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-20E68036-A8A2-4297-8074-44D076845E00}

Running URLReaderWithOptions {#JSSEC-GUID-20E68036-A8A2-4297-8074-44D076845E00 .sect2}
----------------------------

<div>
The example is very similar to
[`URLReaader.java`](sample-code-illustrating-https-connections.htm#GUID-BC38D378-DF50-4B41-8489-67B6AB621FAB__URLREADER.JAVA-33086510),
but it enables you to set the system properties through main method
arguments rather than as `-D`{.codeph} options to the Java runtime
environment.

<div class="section">
Usage

`java URLReaderWithOptions [-h proxyhost] [-p proxyport] [-k protocolhandlerpkgs] [-c ciphersarray]`{.codeph}

-   `proxyHost`{.codeph}: secure proxy server hostname
    (`https.proxyHost`{.codeph})
-   `proxyPort`{.codeph}: secure proxy server port
    (`https.proxyPort`{.codeph})
-   `protocolhandlerpkgs`{.codeph}: a pipe-separated (`|`{.codeph}) list
    of protocol handlers (`java.protocol.handler.pkgs`{.codeph})
-   `ciphersarray`{.codeph}: enabled cipher suites as a comma-separated
    list (`https.cipherSuites`{.codeph})

<div class="infoboxnote" id="GUID-20E68036-A8A2-4297-8074-44D076845E00__GUID-91B04C04-7256-438A-8976-CFF5EC570A16">
Note:

Multiple protocol handlers can be included in the
`protocolhandlerpkgs`{.codeph} argument as a list with items separated
by vertical bars. Multiple SSL cipher suite names can be included in the
`ciphersarray`{.codeph} argument as a list with items separated by
commas. The possible cipher suite names are the same as those returned
by the `SSLSocket.getSupportedCipherSuites()`{.codeph} method. The suite
names are taken from the SSL and TLS protocol specifications.

</div>
You need a `protocolhandlerpkgs`{.codeph} argument only if you want to
use an HTTPS protocol handler implementation other than the default one
provided by Oracle.

If you are running the sample code behind a firewall, then you must
include arguments for the proxy host and the proxy port. Additionally,
you can include a list of cipher suites to enable.

Here is an example of running `URLReaderWithOptions`{.codeph} and
specifying the proxy host \"webproxy\" on port 8080:

``` {.codeblock dir="ltr"}
java URLReaderWithOptions -h webproxy -p 8080
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-20E68036-A8A2-4297-8074-44D076845E00__URLREADERWITHOPTIONS.JAVA-3315CF43">
URLReaderWithOptions.java

``` {.oac_no_warn dir="ltr"}
import java.net.*;
import java.io.*;

/*
 * Using a URL to access resources on a secure site.
 *
 * You can optionally set the following command line options:
 *
 *     -h <secure proxy server hostname>
 *     -p <secure proxy server port>
 *     -k <| separated list of protocol handlers>
 *     -c <enabled cipher suites as a comma separated list>
 *
 */

public class URLReaderWithOptions {
    public static void main(String[] args) throws Exception {

        System.out.println("USAGE: java URLReaderWithOptions " +
            "[-h proxyhost] [-p proxyport] [-k protocolhandlerpkgs] " +
            "[-c ciphersarray]");

        // initialize system properties
        char option = 'd';
        for (int i = 0; i < args.length; i++) {
            System.out.println(option+": "+args[i]);
            switch(option) {
            case 'h':
                System.setProperty("https.proxyHost", args[i]);
                option = 'd';
                break;
            case 'p':
                System.setProperty("https.proxyPort", args[i]);
                option = 'd';
                break;
            case 'k':
                System.setProperty("java.protocol.handler.pkgs", args[i]);
                option = 'd';
                break;
            case 'c':
                System.setProperty("https.cipherSuites", args[i]);
                option = 'd';
                break;
            default:
                // get the next option
                if (args[i].startsWith("-")) {
                    option = args[i].charAt(1);
                }
            }
        }

        URL verisign = new URL("https://www.verisign.com/");
        BufferedReader in = new BufferedReader(
                                new InputStreamReader(
                                verisign.openStream()));

        String inputLine;

        while ((inputLine = in.readLine()) != null)
            System.out.println(inputLine);

        in.close();
    }
}
```

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
| -------------------- | a |       [![Go To Table |
| ------------ ------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------------- | L |             <span cl |
| ------------------ - | o | ass="icon">Contents< |
| -                    | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|               [![Pre | ] | -------------------- |
| vious](../../dcommon | ( | -------------------- |
| /gifs/leftnav.gif)\  | . | ---                  |
|                      | . |                      |
|                      | / |                      |
|               [![Nex | . |                      |
| t](../../dcommon/gif | . |                      |
| s/rightnav.gif)\     | / |                      |
|                      | d |                      |
|    <span class="icon | c |                      |
| ">Previous</span>](s | o |                      |
| ample-code-illustrat | m |                      |
| ing-secure-socket-co | m |                      |
| nnection-client-and- | o |                      |
| server.htm)   <span  | n |                      |
| class="icon">Next</s | / |                      |
| pan>](sample-code-il | g |                      |
| lustrating-secure-rm | i |                      |
| i-connection.htm)    | f |                      |
|   ------------------ | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| -------------------- | a |                      |
| ------------ ------- | c |                      |
| -------------------- | l |                      |
| -------------------- | e |                      |
| -------------------- | . |                      |
| ------------------ - | g |                      |
| -                    | i |                      |
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
