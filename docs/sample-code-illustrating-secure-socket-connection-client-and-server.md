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

  ------------------------------------------------------------- --------------------------------------------------------------------------------- --
          [![Previous](../../dcommon/gifs/leftnav.gif)\                            [![Next](../../dcommon/gifs/rightnav.gif)\                     
   <span class="icon">Previous</span>](sample-truststores.htm)   <span class="icon">Next</span>](sample-code-illustrating-https-connections.htm)  
  ------------------------------------------------------------- --------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-A4D59ABB-62AF-4FC0-900E-A795FDC84E41}<!-- End Header -->

Sample Code Illustrating a Secure Socket Connection Between a Client and a Server {#JSSEC-GUID-A4D59ABB-62AF-4FC0-900E-A795FDC84E41 .sect1}
=================================================================================

<div>
These samples illustrate how to set up a secure socket connection
between a client and a server.

When running the sample client programs, you can communicate with an
existing server, such as a web server, or you can communicate with the
sample server program, `ClassFileServer`{.codeph}. You can run the
sample client and the sample server programs on different machines
connected to the same network, or you can run them both on one machine
but from different terminal windows.

All the sample `SSLSocketClient*`{.codeph} programs in the
samples/sockets/client directory (and `URLReader*`{.codeph} programs
described in [Sample Code Illustrating HTTPS
Connections](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__SAMPLECODEILLUSTRATINGHTTPSCONNECTI-7D238310))
can be run with the `ClassFileServer`{.codeph} sample server program. An
example of how to do this is shown in [Running
SSLSocketClientWithClientAuth with
ClassFileServer](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGSSLSOCKETCLIENTWITHCLIENTAUT-7D23BC0C).
You can make similar changes to run `URLReader`{.codeph},
`SSLSocketClient`{.codeph}, or `SSLSocketClientWithTunneling`{.codeph}
with `ClassFileServer`{.codeph}.

If an authentication error occurs during communication between the
client and the server (whether using a web server or
`ClassFileServer`{.codeph}), it is most likely because the necessary
keys are not in the truststore (trust key database). See [Terms and
Definitions](java-secure-socket-extension-jsse-reference-guide.htm#GUID-C7BB21C7-E19E-4DE4-8494-CB43F957C329 "The following are commonly used cryptography terms and their definitions.").
For example, the `ClassFileServer`{.codeph} uses a keystore called
`testkeys`{.codeph} containing the private key for `localhost`{.codeph}
as needed during the SSL handshake. The `testkeys`{.codeph} keystore is
included in the same samples/sockets/server directory as the
`ClassFileServer`{.codeph} source. If the client cannot find a
certificate for the corresponding public key of `localhost`{.codeph} in
the truststore it consults, then an authentication error will occur. Be
sure to use the `samplecacerts`{.codeph} truststore (which contains the
public key and certificate of the `localhost`{.codeph}), as described in
[Configuration Requirements for SSL Socket
Samples](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-B1060A74-9BAE-40F1-AB2B-C8D83812A4C7).

</div>
<div class="sect2">
[]{#GUID-B1060A74-9BAE-40F1-AB2B-C8D83812A4C7}

Configuration Requirements for SSL Socket Samples {#JSSEC-GUID-B1060A74-9BAE-40F1-AB2B-C8D83812A4C7 .sect2}
-------------------------------------------------

<div>
When running the sample programs that create a secure socket connection
between a client and a server, you will need to make the appropriate
certificates file (truststore) available. For both the client and the
server programs, you should use the certificates file
`samplecacerts`{.codeph} from the `samples`{.codeph} directory. Using
this certificates file will allow the client to authenticate the server.
The file contains all the common Certificate Authority (CA) certificates
shipped with the JDK (in the cacerts file), plus a certificate for
`localhost`{.codeph} needed by the client to authenticate
`localhost`{.codeph} when communicating with the sample server
`ClassFileServer`{.codeph}. The `ClassFileServer`{.codeph} uses a
keystore containing the private key for `localhost`{.codeph} that
corresponds to the public key in `samplecacerts`{.codeph}.

To make the `samplecacerts`{.codeph} file available to both the client
and the server, you can either copy it to the file
`java-home/lib/security/jssecacerts`, rename it to `cacerts`, and use it
to replace the `java-home/lib/security/cacerts` file, or add the
following option to the command line when running the `java`{.codeph}
command for both the client and the server:

``` {.codeblock dir="ltr"}
-Djavax.net.ssl.trustStore=path_to_samplecacerts_file
```

The password for the `samplecacerts`{.codeph} truststore is
`changeit`{.codeph}. You can substitute your own certificates in the
samples by using the `keytool`{.codeph} utility.

If you use a browser to access the sample SSL server provided in the
`ClassFileServer`{.codeph} example, then a dialog box may pop up with
the message that it does not recognize the certificate. This is normal
because the certificate used with the sample programs is self-signed and
is for testing only. You can accept the certificate for the current
session. After testing the SSL server, you should exit the browser,
which deletes the test certificate from the browser\'s namespace.

For client authentication, a separate `duke`{.codeph} certificate is
available in the appropriate directories. The public key and certificate
is also stored in the `samplecacerts`{.codeph} file.

</div>
</div>
<div class="sect2">
[]{#GUID-AA1C27A1-2CA8-4309-B281-D6199F60E666}

Running SSLSocketClient {#JSSEC-GUID-AA1C27A1-2CA8-4309-B281-D6199F60E666 .sect2}
-----------------------

<div>
The example
[`SSLSocketClient.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-AA1C27A1-2CA8-4309-B281-D6199F60E666__SSLSOCKETCLIENT.JAVA-32CFECE1)
demonstrates how to create a client that uses an `SSLSocket`{.codeph} to
send an HTTP request and to get a response from an HTTPS server. By
default, this example connects to `www.verisign.com`{.codeph}, but it
can easily be adapted to connect to `ClassFileServer` (see [Running
ClassFileServer](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C)).
The output of this program is the HTML source for
`https://www.verisign.com/index.html`{.codeph}.

You must not be behind a firewall to run this program as provided. If
you run it from behind a firewall, you will get an
`UnknownHostException`{.codeph} because JSSE cannot find a path through
your firewall to `www.verisign.com`{.codeph}. To create an equivalent
client that can run from behind a firewall, set up proxy tunneling as
illustrated in the sample program `SSLSocketClientWithTunneling`.

<div class="infoboxnote" id="GUID-AA1C27A1-2CA8-4309-B281-D6199F60E666__GUID-50A25A9C-8F31-43ED-A0A4-04AE3227AB3E">
Note:

The GET request must be slightly modified so that a file is specified.

</div>
<div class="section">
Usage

``` {.oac_no_warn dir="ltr"}
java SSLSocketClient
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-AA1C27A1-2CA8-4309-B281-D6199F60E666__SSLSOCKETCLIENT.JAVA-32CFECE1">
SSLSocketClient.java

``` {.oac_no_warn dir="ltr"}
import java.net.*;
import java.io.*;
import javax.net.ssl.*;

/*
 * This example demostrates how to use a SSLSocket as client to
 * send a HTTP request and get response from an HTTPS server.
 * It assumes that the client is not behind a firewall
 */

public class SSLSocketClient {

    public static void main(String[] args) throws Exception {
        try {
            SSLSocketFactory factory =
                (SSLSocketFactory)SSLSocketFactory.getDefault();
            SSLSocket socket =
                (SSLSocket)factory.createSocket("www.verisign.com", 443);

            /*
             * send http request
             *
             * Before any application data is sent or received, the
             * SSL socket will do SSL handshaking first to set up
             * the security attributes.
             *
             * SSL handshaking can be initiated by either flushing data
             * down the pipe, or by starting the handshaking by hand.
             *
             * Handshaking is started manually in this example because
             * PrintWriter catches all IOExceptions (including
             * SSLExceptions), sets an internal error flag, and then
             * returns without rethrowing the exception.
             *
             * Unfortunately, this means any error messages are lost,
             * which caused lots of confusion for others using this
             * code.  The only way to tell there was an error is to call
             * PrintWriter.checkError().
             */
            socket.startHandshake();

            PrintWriter out = new PrintWriter(
                                  new BufferedWriter(
                                  new OutputStreamWriter(
                                  socket.getOutputStream())));

            out.println("GET / HTTP/1.0");
            out.println();
            out.flush();

            /*
             * Make sure there were no surprises
             */
            if (out.checkError())
                System.out.println(
                    "SSLSocketClient:  java.io.PrintWriter error");

            /* read response */
            BufferedReader in = new BufferedReader(
                                    new InputStreamReader(
                                    socket.getInputStream()));

            String inputLine;
            while ((inputLine = in.readLine()) != null)
                System.out.println(inputLine);

            in.close();
            out.close();
            socket.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-B9103D0C-3E6A-4301-B558-461E4CB23DC9}

Running SSLSocketClientWithTunnelling {#JSSEC-GUID-B9103D0C-3E6A-4301-B558-461E4CB23DC9 .sect2}
-------------------------------------

<div>
The example
[`SSLSocketClientWithTunneling.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-B9103D0C-3E6A-4301-B558-461E4CB23DC9__SSLSOCKETCLIENTWITHTUNNELING.JAVA-32D03DB5)
illustrates how to do proxy tunneling to access a secure web server from
behind a firewall.

The program will return the HTML source file from
`https://www.verisign.com/index.html`{.codeph}.

<div class="section">
Usage

`java -Dhttps.proxyHost=webproxy -Dhttps.proxyPort=ProxyPortNumber SSLSocketClientWithTunneling`{.codeph}

Replace `webproxy`{.codeph} with the name of your proxy host and
`ProxyPortNumber`{.codeph} with the appropriate port number.

The system properties `https.proxyHost`{.codeph} and
`https.proxyPort`{.codeph} are used to make a socket connection to the
proxy host, and then the <span class="apiname">SSLSocket</span> is
layered on top of that <span class="apiname">Socket</span>.

``` {.oac_no_warn dir="ltr"}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-B9103D0C-3E6A-4301-B558-461E4CB23DC9__SSLSOCKETCLIENTWITHTUNNELING.JAVA-32D03DB5">
SSLSocketClientWithTunneling.java

</div>
<!-- class="section" -->

``` {.oac_no_warn dir="ltr"}
import java.net.*;
import java.io.*;
import javax.net.ssl.*;

/*
 * This example illustrates how to do proxy Tunneling to access a
 * secure web server from behind a firewall.
 *
 * Please set the following Java system properties
 * to the appropriate values:
 *
 *   https.proxyHost = <secure proxy server hostname>
 *   https.proxyPort = <secure proxy server port>
 */

public class SSLSocketClientWithTunneling {

    public static void main(String[] args) throws Exception {
        new SSLSocketClientWithTunneling().doIt("www.verisign.com", 443);
    }

    String tunnelHost;
    int tunnelPort;

    public void doIt(String host, int port) {
        try {

            /*
             * Let's setup the SSLContext first, as there's a lot of
             * computations to be done.  If the socket were created
             * before the SSLContext, the server/proxy might timeout
             * waiting for the client to actually send something.
             */
            SSLSocketFactory factory =
                (SSLSocketFactory)SSLSocketFactory.getDefault();

            /*
             * Set up a socket to do tunneling through the proxy.
             * Start it off as a regular socket, then layer SSL
             * over the top of it.
             */
            tunnelHost = System.getProperty("https.proxyHost");
            tunnelPort = Integer.getInteger("https.proxyPort").intValue();

            Socket tunnel = new Socket(tunnelHost, tunnelPort);
            doTunnelHandshake(tunnel, host, port);

            /*
             * Ok, let's overlay the tunnel socket with SSL.
             */
            SSLSocket socket =
                (SSLSocket)factory.createSocket(tunnel, host, port, true);

            /*
             * register a callback for handshaking completion event
             */
            socket.addHandshakeCompletedListener(
                new HandshakeCompletedListener() {
                    public void handshakeCompleted(
                            HandshakeCompletedEvent event) {
                        System.out.println("Handshake finished!");
                        System.out.println(
                            "\t CipherSuite:" + event.getCipherSuite());
                        System.out.println(
                            "\t SessionId " + event.getSession());
                        System.out.println(
                            "\t PeerHost " + event.getSession().getPeerHost());
                    }
                }
            );

            /*
             * send http request
             *
             * See SSLSocketClient.java for more information about why
             * there is a forced handshake here when using PrintWriters.
             */
            socket.startHandshake();

            PrintWriter out = new PrintWriter(
                                  new BufferedWriter(
                                  new OutputStreamWriter(
                                  socket.getOutputStream())));

            out.println("GET / HTTP/1.0");
            out.println();
            out.flush();

            /*
             * Make sure there were no surprises
             */
            if (out.checkError())
                System.out.println(
                    "SSLSocketClient:  java.io.PrintWriter error");

            /* read response */
            BufferedReader in = new BufferedReader(
                                    new InputStreamReader(
                                    socket.getInputStream()));

            String inputLine;

            while ((inputLine = in.readLine()) != null)
                System.out.println(inputLine);

            in.close();
            out.close();
            socket.close();
            tunnel.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /*
     * Tell our tunnel where we want to CONNECT, and look for the
     * right reply.  Throw IOException if anything goes wrong.
     */
    private void doTunnelHandshake(Socket tunnel, String host, int port)
    throws IOException
    {
        OutputStream out = tunnel.getOutputStream();
        String msg = "CONNECT " + host + ":" + port + " HTTP/1.0\n"
                     + "User-Agent: "
                     + sun.net.www.protocol.http.HttpURLConnection.userAgent
                     + "\r\n\r\n";
        byte b[];
        try {
            /*
             * We really do want ASCII7 -- the http protocol doesn't change
             * with locale.
             */
            b = msg.getBytes("ASCII7");
        } catch (UnsupportedEncodingException ignored) {
            /*
             * If ASCII7 isn't there, something serious is wrong, but
             * Paranoia Is Good (tm)
             */
            b = msg.getBytes();
        }
        out.write(b);
        out.flush();

        /*
         * We need to store the reply so we can create a detailed
         * error message to the user.
         */
        byte            reply[] = new byte[200];
        int             replyLen = 0;
        int             newlinesSeen = 0;
        boolean         headerDone = false;     /* Done on first newline */

        InputStream     in = tunnel.getInputStream();
        boolean         error = false;

        while (newlinesSeen < 2) {
            int i = in.read();
            if (i < 0) {
                throw new IOException("Unexpected EOF from proxy");
            }
            if (i == '\n') {
                headerDone = true;
                ++newlinesSeen;
            } else if (i != '\r') {
                newlinesSeen = 0;
                if (!headerDone && replyLen < reply.length) {
                    reply[replyLen++] = (byte) i;
                }
            }
        }

        /*
         * Converting the byte array to a string is slightly wasteful
         * in the case where the connection was successful, but it's
         * insignificant compared to the network overhead.
         */
        String replyStr;
        try {
            replyStr = new String(reply, 0, replyLen, "ASCII7");
        } catch (UnsupportedEncodingException ignored) {
            replyStr = new String(reply, 0, replyLen);
        }

        /* We asked for HTTP/1.0, so we should get that back */
        if (!replyStr.startsWith("HTTP/1.0 200")) {
            throw new IOException("Unable to tunnel through "
                    + tunnelHost + ":" + tunnelPort
                    + ".  Proxy returns \"" + replyStr + "\"");
        }

        /* tunneling Handshake was successful! */
    }
}
```

</div>
</div>
<div class="sect2">
[]{#GUID-756AE510-E1BF-42FE-92FC-B9BE3EC31C7B}

Running SSLSocketClientWithClientAuth {#JSSEC-GUID-756AE510-E1BF-42FE-92FC-B9BE3EC31C7B .sect2}
-------------------------------------

<div>
The example
[`SSLSocketClientWithClientAuth.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-756AE510-E1BF-42FE-92FC-B9BE3EC31C7B__SSLSOCKETCLIENTWITHCLIENTAUTH.JAVA-32D0CA6C)
is similar to [Running
SSLSocketClient](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-AA1C27A1-2CA8-4309-B281-D6199F60E666),
but this shows how to set up a key manager to do client authentication
if required by a server. This program also assumes that the client is
not outside a firewall. You can modify the program to connect from
inside a firewall by following the example in [Running
SSLSocketClientWithTunnelling](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-B9103D0C-3E6A-4301-B558-461E4CB23DC9).

To run this program, you must specify three parameters: host, port, and
requested file path. To mirror the previous examples, you can run this
program without client authentication by setting the host to
`www.verisign.com`{.codeph}, the port to `443`{.codeph}, and the
requested file path to `https://www.verisign.com/`{.codeph}. The output
when using these parameters is the HTML for the website
`https://www.verisign.com/`{.codeph}.

To run `SSLSocketClientWithClientAuth`{.codeph} to do client
authentication, you must access a server that requests client
authentication. You can use the sample program
`ClassFileServer`{.codeph} as this server. See [Running
SSLSocketClientWithClientAuth with
ClassFileServer](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-1B7038DC-7564-4EE6-A1DF-6B1445077E2E).

<div class="section">
Usage

``` {.oac_no_warn dir="ltr"}
java SSLSocketClientWithClientAuth host port requestedfilepath
```

<div class="infoboxnote" id="GUID-756AE510-E1BF-42FE-92FC-B9BE3EC31C7B__IFYOUARECONNECTINGTOTHECLASSFILESER-32D0BDD3">
Note:

If you are connecting to the
<span class="apiname">ClassFileServer</span> application above, be sure
that it can find the credentials for the `duke`{.codeph} user. See
[Sample Truststores](sample-truststores.htm).

</div>
</div>
<!-- class="section" -->

<div class="section" id="GUID-756AE510-E1BF-42FE-92FC-B9BE3EC31C7B__SSLSOCKETCLIENTWITHCLIENTAUTH.JAVA-32D0CA6C">
SSLSocketClientWithClientAuth.java

</div>
<!-- class="section" -->

``` {.oac_no_warn dir="ltr"}
import java.net.*;
import java.io.*;
import javax.net.ssl.*;
import javax.security.cert.X509Certificate;
import java.security.KeyStore;

/*
 * This example shows how to set up a key manager to do client
 * authentication if required by server.
 *
 * This program assumes that the client is not inside a firewall.
 * The application can be modified to connect to a server outside
 * the firewall by following SSLSocketClientWithTunneling.java.
 */
public class SSLSocketClientWithClientAuth {

    public static void main(String[] args) throws Exception {
        String host = null;
        int port = -1;
        String path = null;
        for (int i = 0; i < args.length; i++)
            System.out.println(args[i]);

        if (args.length < 3) {
            System.out.println(
                "USAGE: java SSLSocketClientWithClientAuth " +
                "host port requestedfilepath");
            System.exit(-1);
        }

        try {
            host = args[0];
            port = Integer.parseInt(args[1]);
            path = args[2];
        } catch (IllegalArgumentException e) {
             System.out.println("USAGE: java SSLSocketClientWithClientAuth " +
                 "host port requestedfilepath");
             System.exit(-1);
        }

        try {

            /*
             * Set up a key manager for client authentication
             * if asked by the server.  Use the implementation's
             * default TrustStore and secureRandom routines.
             */
            SSLSocketFactory factory = null;
            try {
                SSLContext ctx;
                KeyManagerFactory kmf;
                KeyStore ks;
                char[] passphrase = "passphrase".toCharArray();

                ctx = SSLContext.getInstance("TLS");
                kmf = KeyManagerFactory.getInstance("SunX509");
                ks = KeyStore.getInstance("JKS");

                ks.load(new FileInputStream("testkeys"), passphrase);

                kmf.init(ks, passphrase);
                ctx.init(kmf.getKeyManagers(), null, null);

                factory = ctx.getSocketFactory();
            } catch (Exception e) {
                throw new IOException(e.getMessage());
            }

            SSLSocket socket = (SSLSocket)factory.createSocket(host, port);

            /*
             * send http request
             *
             * See SSLSocketClient.java for more information about why
             * there is a forced handshake here when using PrintWriters.
             */
            socket.startHandshake();

            PrintWriter out = new PrintWriter(
                                  new BufferedWriter(
                                  new OutputStreamWriter(
                                  socket.getOutputStream())));
            out.println("GET " + path + " HTTP/1.0");
            out.println();
            out.flush();

            /*
             * Make sure there were no surprises
             */
            if (out.checkError())
                System.out.println(
                    "SSLSocketClient: java.io.PrintWriter error");

            /* read response */
            BufferedReader in = new BufferedReader(
                                    new InputStreamReader(
                                    socket.getInputStream()));

            String inputLine;

            while ((inputLine = in.readLine()) != null)
                System.out.println(inputLine);

            in.close();
            out.close();
            socket.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

</div>
</div>
<div class="sect2">
[]{#GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C}

Running ClassFileServer {#JSSEC-GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C .sect2}
-----------------------

<div>
This example, which consists of
[`ClassFileServer.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C__CLASSFILESERVER.JAVA-3314B74B)
and
[`ClassServer.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C__CLASSSERVER.JAVA-3314BE5B),
demonstrates the implementation of a mini-webserver, which can service
simple HTTP or HTTPS requests (only the GET method is supported). By
default, the server does not use SSL/TLS. However, a command-line option
enables SSL/TLS. Requests must be of the form:

``` {.oac_no_warn dir="ltr"}
GET /<filename>
```

<div class="section">
Usage

``` {.oac_no_warn dir="ltr"}
java ClassFileServer port docroot [TLS [true]]
```

-   `port`{.codeph}: The port on which the server resides. It can be any
    available unused port number, for example, you can use the number
    `2001`{.codeph}.
-   `docroot`{.codeph}: The root of the local directory hierarchy. It
    indicates the directory on the server that contains the file you
    want to retrieve. For example, on Linux, you can use `/home/userid/`
    (where `userid` refers to your particular UID), whereas on Windows
    systems, you can use `C:\`.
-   `TLS`{.codeph}: An optional flag which enables SSL/TLS services. If
    you omit the `TLS`{.codeph} and `true`{.codeph} parameters, which
    indicates that an ordinary (not TLS) file server should be used,
    without authentication, then nothing happens. This is because one
    side (the client) is trying to negotiate with TLS, while the other
    (the server) is not, so they cannot communicate.
-   `true`{.codeph}: An optional flag which requires that clients
    authenticate themselves. This option requires that SSL/TLS support
    be enabled.

The secure server comes preinstalled with a certificate for
`localhost`{.codeph}. If the server is on the same host as the client,
URLs of the form `https://localhost:port/file`{.codeph} should pass
hostname verification. If you choose to run on separate hosts, you
should create a new host certificate for the https hostname being used,
otherwise there will be hostname mismatch problems. (Note: in Java, this
can be corrected in the <span class="apiname">HttpsURLConnection</span>
class by providing a custom
<span class="apiname">HostnameVerifier</span> implementation, or in a
browser by accepting the dialog box that describes the hostname
mismatch.)

If you are using the TLS variant (HTTPS), remember to specify the https
protocol:

``` {.oac_no_warn dir="ltr"}
https://hostname:2001/dir1/file1
```

<div class="infoboxnote" id="GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C__GUID-9BE85FD2-AF32-451A-855F-132DF2E35267">
Note:

If you use a browser, you will see a dialog popup with the message that
the application doesn\'t recognize the `localhost`{.codeph} certificate.
This is normal because the self-signed certificate being presented to
the browser is not initially trusted. If desired, you could import the
`localhost`{.codeph} certificate into the browser\'s truststore.

</div>
</div>
<!-- class="section" -->

<div class="section" id="GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C__CLASSFILESERVER.JAVA-3314B74B">
ClassFileServer.java

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.net.*;
import java.security.KeyStore;
import javax.net.*;
import javax.net.ssl.*;
import javax.security.cert.X509Certificate;

/* ClassFileServer.java -- a simple file server that can server
 * Http get request in both clear and secure channel
 *
 * The ClassFileServer implements a ClassServer that
 * reads files from the file system. See the
 * doc for the "Main" method for how to run this
 * server.
 */

public class ClassFileServer extends ClassServer {

    private String docroot;

    private static int DefaultServerPort = 2001;

    /**
     * Constructs a ClassFileServer.
     *
     * @param path the path where the server locates files
     */
    public ClassFileServer(ServerSocket ss, String docroot) throws IOException
    {
        super(ss);
        this.docroot = docroot;
    }

    /**
     * Returns an array of bytes containing the bytes for
     * the file represented by the argument <b>path</b>.
     *
     * @return the bytes for the file
     * @exception FileNotFoundException if the file corresponding
     * to <b>path</b> could not be loaded.
     */
    public byte[] getBytes(String path)
        throws IOException
    {
        System.out.println("reading: " + path);
        File f = new File(docroot + File.separator + path);
        int length = (int)(f.length());
        if (length == 0) {
            throw new IOException("File length is zero: " + path);
        } else {
            FileInputStream fin = new FileInputStream(f);
            DataInputStream in = new DataInputStream(fin);

            byte[] bytecodes = new byte[length];
            in.readFully(bytecodes);
            return bytecodes;
        }
    }

    /**
     * Main method to create the class server that reads
     * files. This takes two command line arguments, the
     * port on which the server accepts requests and the
     * root of the path. To start up the server: <br><br>
     *
     * <code>   java ClassFileServer <port> <path>
     * </code><br><br>
     *
     * <code>   new ClassFileServer(port, docroot);
     * </code>
     */
    public static void main(String args[])
    {
        System.out.println(
            "USAGE: java ClassFileServer port docroot [TLS [true]]");
        System.out.println("");
        System.out.println(
            "If the third argument is TLS, it will start as\n" +
            "a TLS/SSL file server, otherwise, it will be\n" +
            "an ordinary file server. \n" +
            "If the fourth argument is true,it will require\n" +
            "client authentication as well.");

        int port = DefaultServerPort;
        String docroot = "";

        if (args.length >= 1) {
            port = Integer.parseInt(args[0]);
        }

        if (args.length >= 2) {
            docroot = args[1];
        }
        String type = "PlainSocket";
        if (args.length >= 3) {
            type = args[2];
        }
        try {
            ServerSocketFactory ssf =
                ClassFileServer.getServerSocketFactory(type);
            ServerSocket ss = ssf.createServerSocket(port);
            if (args.length >= 4 && args[3].equals("true")) {
                ((SSLServerSocket)ss).setNeedClientAuth(true);
            }
            new ClassFileServer(ss, docroot);
        } catch (IOException e) {
            System.out.println("Unable to start ClassServer: " +
                               e.getMessage());
            e.printStackTrace();
        }
    }

    private static ServerSocketFactory getServerSocketFactory(String type) {
        if (type.equals("TLS")) {
            SSLServerSocketFactory ssf = null;
            try {
                // set up key manager to do server authentication
                SSLContext ctx;
                KeyManagerFactory kmf;
                KeyStore ks;
                char[] passphrase = "passphrase".toCharArray();

                ctx = SSLContext.getInstance("TLS");
                kmf = KeyManagerFactory.getInstance("SunX509");
                ks = KeyStore.getInstance("JKS");

                ks.load(new FileInputStream("testkeys"), passphrase);
                kmf.init(ks, passphrase);
                ctx.init(kmf.getKeyManagers(), null, null);

                ssf = ctx.getServerSocketFactory();
                return ssf;
            } catch (Exception e) {
                e.printStackTrace();
            }
        } else {
            return ServerSocketFactory.getDefault();
        }
        return null;
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C__CLASSSERVER.JAVA-3314BE5B">
ClassServer.java

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.net.*;
import javax.net.*;

/*
 * ClassServer.java -- a simple file server that can serve
 * Http get request in both clear and secure channel
 */

public abstract class ClassServer implements Runnable {

    private ServerSocket server = null;
    /**
     * Constructs a ClassServer based on <b>ss</b> and
     * obtains a file's bytecodes using the method <b>getBytes</b>.
     *
     */
    protected ClassServer(ServerSocket ss)
    {
        server = ss;
        newListener();
    }

    /**
     * Returns an array of bytes containing the bytes for
     * the file represented by the argument <b>path</b>.
     *
     * @return the bytes for the file
     * @exception FileNotFoundException if the file corresponding
     * to <b>path</b> could not be loaded.
     * @exception IOException if error occurs reading the class
     */
    public abstract byte[] getBytes(String path)
        throws IOException, FileNotFoundException;

    /**
     * The "listen" thread that accepts a connection to the
     * server, parses the header to obtain the file name
     * and sends back the bytes for the file (or error
     * if the file is not found or the response was malformed).
     */
    public void run()
    {
        Socket socket;

        // accept a connection
        try {
            socket = server.accept();
        } catch (IOException e) {
            System.out.println("Class Server died: " + e.getMessage());
            e.printStackTrace();
            return;
        }

        // create a new thread to accept the next connection
        newListener();

        try {
            OutputStream rawOut = socket.getOutputStream();

            PrintWriter out = new PrintWriter(
                                new BufferedWriter(
                                new OutputStreamWriter(
                                rawOut)));
            try {
                // get path to class file from header
                BufferedReader in =
                    new BufferedReader(
                        new InputStreamReader(socket.getInputStream()));
                String path = getPath(in);
                // retrieve bytecodes
                byte[] bytecodes = getBytes(path);
                // send bytecodes in response (assumes HTTP/1.0 or later)
                try {
                    out.print("HTTP/1.0 200 OK\r\n");
                    out.print("Content-Length: " + bytecodes.length +
                                   "\r\n");
                    out.print("Content-Type: text/html\r\n\r\n");
                    out.flush();
                    rawOut.write(bytecodes);
                    rawOut.flush();
                } catch (IOException ie) {
                    ie.printStackTrace();
                    return;
                }

            } catch (Exception e) {
                e.printStackTrace();
                // write out error response
                out.println("HTTP/1.0 400 " + e.getMessage() + "\r\n");
                out.println("Content-Type: text/html\r\n\r\n");
                out.flush();
            }

        } catch (IOException ex) {
            // eat exception (could log error to log file, but
            // write out to stdout for now).
            System.out.println("error writing response: " + ex.getMessage());
            ex.printStackTrace();

        } finally {
            try {
                socket.close();
            } catch (IOException e) {
            }
        }
    }

    /**
     * Create a new thread to listen.
     */
    private void newListener()
    {
        (new Thread(this)).start();
    }

    /**
     * Returns the path to the file obtained from
     * parsing the HTML header.
     */
    private static String getPath(BufferedReader in)
        throws IOException
    {
        String line = in.readLine();
        String path = "";
        // extract class from GET line
        if (line.startsWith("GET /")) {
            line = line.substring(5, line.length()-1).trim();
            int index = line.indexOf(' ');
            if (index != -1) {
                path = line.substring(0, index);
            }
        }

        // eat the rest of header
        do {
            line = in.readLine();
        } while ((line.length() != 0) &&
                 (line.charAt(0) != '\r') && (line.charAt(0) != '\n'));

        if (path.length() != 0) {
            return path;
        } else {
            throw new IOException("Malformed Header");
        }
    }
}
```

</div>
<!-- class="section" -->

</div>
</div>
<div class="sect2">
[]{#GUID-1B7038DC-7564-4EE6-A1DF-6B1445077E2E}

Running SSLSocketClientWithClientAuth with ClassFileServer {#JSSEC-GUID-1B7038DC-7564-4EE6-A1DF-6B1445077E2E .sect2}
----------------------------------------------------------

<div>
You can use the sample programs
[`SSLSocketClientWithClientAuth.java`](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-756AE510-E1BF-42FE-92FC-B9BE3EC31C7B__SSLSOCKETCLIENTWITHCLIENTAUTH.JAVA-32D0CA6C)
and
[`ClassFileServer.;ava`{.codeph}](sample-code-illustrating-secure-socket-connection-client-and-server.htm#GUID-3561ED02-174C-4E65-8BB1-5995E9B7282C__CLASSFILESERVER.JAVA-3314B74B)
to set up authenticated communication, where the client and server are
authenticated to each other. You can run both sample programs on
different machines connected to the same network, or you can run them
both on one machine but from different terminal windows or command
prompt windows. To set up both the client and the server, do the
following:

1.  Run the program `ClassFileServer`{.codeph} from one machine or
    terminal window. See [Running
    ClassFileServer](java-secure-socket-extension-jsse-reference-guide.htm#GUID-1E8A0301-BD82-4E6A-BEB7-B76FE8F554BA__RUNNINGCLASSFILESERVER-7D23BEFC).
2.  Run the program `SSLSocketClientWithClientAuth`{.codeph} on another
    machine or terminal window. `SSLSocketClientWithClientAuth`{.codeph}
    requires the following parameters:
    -   `host`{.codeph} is the host name of the machine that you are
        using to run `ClassFileServer`{.codeph}.
    -   `port`{.codeph} is the same port that you specified for
        `ClassFileServer`{.codeph}.
    -   `requestedfilepath`{.codeph} indicates the path to the file that
        you want to retrieve from the server. You must give this
        parameter as `/filepath`{.codeph}. Forward slashes are required
        in the file path because it is used as part of a GET statement,
        which requires forward slashes regardless of what type of
        operating system you are running. The statement is formed as
        follows:

        ``` {.codeblock dir="ltr"}
        "GET " + requestedfilepath + " HTTP/1.0"
        ```

<div class="infoboxnote" id="GUID-1B7038DC-7564-4EE6-A1DF-6B1445077E2E__GUID-80571B4D-FD52-412D-80AF-BB6FF98147C3">
Note:

You can modify the other `SSLClient*`{.codeph} applications\'
`GET`{.codeph} commands to connect to a local machine running
`ClassFileServer`{.codeph}.

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
| --- ---------------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ----- --             | e | )\                   |
|           [![Previou | L |             <span cl |
| s](../../dcommon/gif | o | ass="icon">Contents< |
| s/leftnav.gif)\      | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|    [![Next](../../dc | ] | -------------------- |
| ommon/gifs/rightnav. | ( | -------------------- |
| gif)\                | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](s | . |                      |
| ample-truststores.ht | . |                      |
| m)   <span class="ic | / |                      |
| on">Next</span>](sam | d |                      |
| ple-code-illustratin | c |                      |
| g-https-connections. | o |                      |
| htm)                 | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| --- ---------------- | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ----- --             | s |                      |
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
