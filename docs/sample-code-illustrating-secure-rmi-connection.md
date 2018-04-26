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

  ------------------------------------------------------------------------------------- ----------------------------------------------------------------------------- --
                      [![Previous](../../dcommon/gifs/leftnav.gif)\                                      [![Next](../../dcommon/gifs/rightnav.gif)\                   
   <span class="icon">Previous</span>](sample-code-illustrating-https-connections.htm)   <span class="icon">Next</span>](sample-code-illustrating-use-sslengine.htm)  
  ------------------------------------------------------------------------------------- ----------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87}<!-- End Header -->

Sample Code Illustrating a Secure RMI Connection {#JSSEC-GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87 .sect1}
================================================

<div>
The example
[`HelloClient.java`](sample-code-illustrating-secure-rmi-connection.html#GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__HELLOCLIENT.JAVA-3316D03B)
illustrates how to create a secure Java Remote Method Invocation (RMI)
connection. The sample code is basically a \"Hello World\" example
modified to install and use a custom RMI socket factory. It uses RMI
over an SSL transport layer using JSSE. The server runs
[`HelloImpl.java`](sample-code-illustrating-secure-rmi-connection.html#GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__HELLOIMPL.JAVA-3316C983),
which sets up an internal RMI registry (rather than using the
`rmiregistry`{.codeph} command). The client runs `HelloClient`{.codeph}
and communicates over a secured connection.

<div class="section">
Usage

Setting up this sample can be a little tricky; here are the necessary
steps:

`% javac *.java `{.codeph}

`% rmic HelloImpl`{.codeph}

`% java -Djava.security.policy=policy HelloImpl`{.codeph} (run in
another window)

`% java HelloClient`{.codeph} (run in another window)

For the server, the RMI security manager will be installed, and the
supplied policy file grants permission to accept connections from any
host. Obviously, giving all permissions should not be done in a
production environment. You will need to give it the appropriate
restrictive network privileges, such as:

``` {.oac_no_warn dir="ltr"}
permission java.net.SocketPermission "hostname:1024-", "accept,resolve";
```

In addition, this example can be easily updated to run with the standard
SSL/TLS-based RMI socket factories. To do this, modify the
`HelloImpl.java` file to use:

``` {.oac_no_warn dir="ltr"}
javax.rmi.ssl.SslRMIClientSocketFactory
javax.rmi.ssl.SslRMIServerSocketFactory
```

instead of:

``` {.oac_no_warn dir="ltr"}
RMISSLClientSocketFactory
RMISSLServerSocketFactory
```

These classes use
<span class="apiname">SSLSocketFactory.getDefault()</span> and
<span class="apiname">SSLServerSocketFactory.getDefault()</span>, so you
will need to configure the system properly to locate your key and trust
material.

<div class="infoboxnote" id="GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__GUID-8BB8F4A8-5DA0-4A0B-91B4-46AD32F2DC8C">
Note:

If you use the standard SSL/TLS-based RMI socket factories, then you can
specify the key stores with system properties:

``` {.oac_no_warn dir="ltr"}
-Djavax.net.ssl.keyStore=testkeys
-Djavax.net.ssl.keyStorePassword=passphrase
```

</div>
</div>
<!-- class="section" -->

<div class="section" id="GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__HELLOCLIENT.JAVA-3316D03B">
HelloClient.java

``` {.oac_no_warn dir="ltr"}
import java.net.InetAddress;
import java.rmi.RemoteException;
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class HelloClient {

    private static final int PORT = 2019;

    public static void main(String args[]) {
        try {
            // Make reference to SSL-based registry
            Registry registry = LocateRegistry.getRegistry(
                InetAddress.getLocalHost().getHostName(), PORT,
                new RMISSLClientSocketFactory());

            // "obj" is the identifier that we'll use to refer
            // to the remote object that implements the "Hello"
            // interface
            Hello obj = (Hello) registry.lookup("HelloServer");

            String message = "blank";
            message = obj.sayHello();
            System.out.println(message+"\n");
        } catch (Exception e) {
            System.out.println("HelloClient exception: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__HELLO.JAVA-3316C72C">
Hello.java

</div>
<!-- class="section" -->

``` {.oac_no_warn dir="ltr"}
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface Hello extends Remote {
    String sayHello() throws RemoteException;
}
```

<div class="section" id="GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__HELLOIMPL.JAVA-3316C983">
HelloImpl.java

</div>
<!-- class="section" -->

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.net.InetAddress;
import java.rmi.RemoteException;
import java.rmi.RMISecurityManager;
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;
import java.rmi.server.UnicastRemoteObject;

public class HelloImpl extends UnicastRemoteObject implements Hello {

    private static final int PORT = 2019;

    public HelloImpl() throws Exception {
        super(PORT,
              new RMISSLClientSocketFactory(),
              new RMISSLServerSocketFactory());
    }

    public String sayHello() {
        return "Hello World!";
    }

    public static void main(String args[]) {

        // Create and install a security manager
        if (System.getSecurityManager() == null) {
            System.setSecurityManager(new RMISecurityManager());
        }

        try {
            // Create SSL-based registry
            Registry registry = LocateRegistry.createRegistry(PORT,
                new RMISSLClientSocketFactory(),
                new RMISSLServerSocketFactory());

            HelloImpl obj = new HelloImpl();

            // Bind this object instance to the name "HelloServer"
            registry.bind("HelloServer", obj);

            System.out.println("HelloServer bound in registry");
        } catch (Exception e) {
            System.out.println("HelloImpl err: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

<div class="section" id="GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__RMISSLCLIENTSOCKETFACTORY.JAVA-3316CC13">
RMISSLClientSocketFactory.java

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.net.*;
import java.rmi.server.*;
import javax.net.ssl.*;

public class RMISSLClientSocketFactory
        implements RMIClientSocketFactory, Serializable {

    public Socket createSocket(String host, int port) throws IOException {
            SSLSocketFactory factory =
                (SSLSocketFactory)SSLSocketFactory.getDefault();
            SSLSocket socket = (SSLSocket)factory.createSocket(host, port);
            return socket;
    }

    public int hashCode() {
        return getClass().hashCode();
    }

    public boolean equals(Object obj) {
        if (obj == this) {
            return true;
        } else if (obj == null || getClass() != obj.getClass()) {
            return false;
        }
        return true;
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__RMISSLSERVERSOCKETFACTORY.JAVA-3316CE59">
RMISSLServerSocketFactory.java

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.net.*;
import java.rmi.server.*;
import javax.net.ssl.*;
import java.security.KeyStore;
import javax.net.ssl.*;

public class RMISSLServerSocketFactory implements RMIServerSocketFactory {

    /*
     * Create one SSLServerSocketFactory, so we can reuse sessions
     * created by previous sessions of this SSLContext.
     */
    private SSLServerSocketFactory ssf = null;

    public RMISSLServerSocketFactory() throws Exception {
        try {
            // set up key manager to do server authentication
            SSLContext ctx;
            KeyManagerFactory kmf;
            KeyStore ks;

            char[] passphrase = "passphrase".toCharArray();
            ks = KeyStore.getInstance("JKS");
            ks.load(new FileInputStream("testkeys"), passphrase);

            kmf = KeyManagerFactory.getInstance("SunX509");
            kmf.init(ks, passphrase);

            ctx = SSLContext.getInstance("TLS");
            ctx.init(kmf.getKeyManagers(), null, null);

            ssf = ctx.getServerSocketFactory();
        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }

    public ServerSocket createServerSocket(int port) throws IOException {
            return ssf.createServerSocket(port);
    }

    public int hashCode() {
        return getClass().hashCode();
    }

    public boolean equals(Object obj) {
        if (obj == this) {
            return true;
        } else if (obj == null || getClass() != obj.getClass()) {
            return false;
        }
        return true;
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-2F82CCFD-22E6-4E6E-A2E1-88CF2BB19E87__POLICY-3316D1F1">
policy

``` {.oac_no_warn dir="ltr"}
// In this example, for simplicity, we will use a policy file that
// gives global permission to anyone from anywhere. Do not use this
// policy file in a production environment.

grant {
    permission java.net.SocketPermission "*", "accept,resolve";
};
```

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
| -------------------- | r | ---                  |
| ------- ------------ | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| ----- --             | L |             <span cl |
|                      | o | ass="icon">Contents< |
|   [![Previous](../.. | g | /span>](toc.htm)     |
| /dcommon/gifs/leftna | o |   -- --------------- |
| v.gif)\              | ] | -------------------- |
|                      | ( | -------------------- |
|      [![Next](../../ | . | ---                  |
| dcommon/gifs/rightna | . |                      |
| v.gif)\              | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](s | / |                      |
| ample-code-illustrat | d |                      |
| ing-https-connection | c |                      |
| s.htm)   <span class | o |                      |
| ="icon">Next</span>] | m |                      |
| (sample-code-illustr | m |                      |
| ating-use-sslengine. | o |                      |
| htm)                 | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ------- ------------ | s |                      |
| -------------------- | / |                      |
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
