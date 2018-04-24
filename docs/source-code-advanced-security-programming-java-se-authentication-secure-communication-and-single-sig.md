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

  ----------------------------------------------------------------------------- ------------------------------------------------------------------------- --
                  [![Previous](../../dcommon/gifs/leftnav.gif)\                                [![Next](../../dcommon/gifs/rightnav.gif)\                 
   <span class="icon">Previous</span>](part-vi-http-spnego-authentication.htm)   <span class="icon">Next</span>](appendix-setting-kerberos-accounts.htm)  
  ----------------------------------------------------------------------------- ------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E}<!-- End Header -->

Source Code for Advanced Security Programming in Java SE Authentication, Secure Communication and Single Sign-On {#JSSEC-GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E .sect1}
================================================================================================================

<div>
<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JASS.JAVA-338B5916">
Jass.java

``` {.oac_no_warn dir="ltr"}
import javax.security.auth.Subject;
import javax.security.auth.login.*;
import javax.security.auth.callback.CallbackHandler;
import java.security.*;
import com.sun.security.auth.callback.TextCallbackHandler;
import java.io.File;

public class Jaas {
    private static String name;
    private static final boolean verbose = false;

    public static void main(String[] args) throws Exception {
        if (args.length > 0) {
            name = args[0];
        } else {
            name = "client";
        }

        // Create action to perform
        PrivilegedExceptionAction action = new MyAction();

        loginAndAction(name, action);
    }

    static void loginAndAction(String name, PrivilegedExceptionAction action)
        throws LoginException, PrivilegedActionException {

        // Create a callback handler
        CallbackHandler callbackHandler = new TextCallbackHandler();

        LoginContext context = null;

        try {
            // Create a LoginContext with a callback handler
            context = new LoginContext(name, callbackHandler);

            // Perform authentication
            context.login();
        } catch (LoginException e) {
            System.err.println("Login failed");
            e.printStackTrace();
            System.exit(-1);
        }

        // Perform action as authenticated user
        Subject subject = context.getSubject();
        if (verbose) {
            System.out.println(subject.toString());
        } else {
            System.out.println("Authenticated principal: " +
                subject.getPrincipals());
        }

        Subject.doAs(subject, action);

        context.logout();
    }

    // Action to perform
    static class MyAction implements PrivilegedExceptionAction {
        MyAction() {
        }

        public Object run() throws Exception {
            // Replace the following with an action to be performed
            // by authenticated user
            System.out.println("Performing secure action ...");
            return null;
        }
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JASS-KRB5.CONF-338B5E8A">
jass-krb5.conf

``` {.oac_no_warn dir="ltr"}
client {
    com.sun.security.auth.module.Krb5LoginModule required
    principal="test";
};

server {
    com.sun.security.auth.module.Krb5LoginModule required
    useKeyTab=true
    storeKey=true
    keyTab=sample.keytab
    principal="host/machineName";
};
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__APPCONNECTION.JAVA-338B5FD0">
AppConnection.java

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.net.Socket;

class AppConnection {
    public static final int AUTH_CMD = 100;
    public static final int DATA_CMD = 200;

    public static final int SUCCESS = 0;
    public static final int AUTH_INPROGRESS = 1;
    public static final int FAILURE = 2;

    private DataInputStream inStream;
    private DataOutputStream outStream;
    private Socket socket;

    // Client application
    AppConnection(String hostName, int port) throws IOException {
        socket = new Socket(hostName, port);

        inStream = new DataInputStream(socket.getInputStream());
        outStream = new DataOutputStream(socket.getOutputStream());

        System.out.println("Connected to address " +
            socket.getInetAddress());
    }

    // Server side application
    AppConnection(Socket socket) throws IOException {
        this.socket = socket;
        inStream = new DataInputStream(socket.getInputStream());
        outStream = new DataOutputStream(socket.getOutputStream());

        System.out.println("Got connection from client " +
            socket.getInetAddress());
    }

    byte[] receive(int expected) throws IOException {
        if (expected != -1) {
            int cmd = inStream.readInt();
            if (expected != cmd) {
                throw new IOException("Received unexpected code: " + cmd);
            }
            //System.out.println("Read cmd: " + cmd);
        }

        byte[] reply = null;
        int len;
        try {
            len = inStream.readInt();
            //System.out.println("Read length: " + len);

        } catch (IOException e) {
            len = 0;
        }
        if (len > 0) {
            reply = new byte[len];
            inStream.readFully(reply);
        } else {
            reply = new byte[0];
        }
        return reply;
    }

    AppReply send(int cmd, byte[] bytes) throws IOException {
        //System.out.println("Write cmd: " + cmd);
        outStream.writeInt(cmd);
        if (bytes != null) {
            //System.out.println("Write length: " + bytes.length);
            outStream.writeInt(bytes.length);
            if (bytes.length > 0) {
                outStream.write(bytes);
            }
        } else {
            //System.out.println("Write length: " + 0);
            outStream.writeInt(0);
        }

        outStream.flush();

        if (cmd == SUCCESS || cmd == FAILURE) {
            return null;   // Done
        }

        int returnCode = inStream.readInt();
        //System.out.println("Read cmd: " + returnCode);

        byte[] reply = null;
        if (returnCode != FAILURE) {
            reply = receive(-1);
        }
        return new AppReply(returnCode, reply);
    }

    static class AppReply {
        private int code;
        private byte[] bytes;

        AppReply(int code, byte[] bytes) {
            this.bytes = bytes;
            this.code = code;
        }

        int getStatus() {
            return code;
        }

        byte[] getBytes() {
            return bytes;
        }
    }

    void close() {
        try {
            socket.close();
        } catch (IOException e) {
        }
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__GSSSERVER.JAVA-338B6349">
GssServer.java

``` {.oac_no_warn dir="ltr"}
import org.ietf.jgss.*;
import java.io.*;
import java.net.Socket;
import java.net.ServerSocket;
import java.security.*;
import java.util.Date;

/**
 * A sample server application that uses JGSS to do mutual authentication
 * with a client using Kerberos as the underlying mechanism. It then
 * exchanges data securely with the client.
 *
 * Every message exchanged with the client includes a 4-byte application-
 * level header that contains the big-endian integer value for the number
 * of bytes that will follow as part of the JGSS token.
 *
 * The protocol is:
 *    1.  Context establishment loop:
 *         a. client sends init sec context token to server
 *         b. server sends accept sec context token to client
 *         ....
 *    2. client sends a wrap token to the server.
 *    3. server sends a wrap token back to the client.
 *
 * Start GssServer first before starting GssClient.
 *
 * Usage:  java <options> GssServer
 *
 * Example: java -Djava.security.auth.login.config=jaas-krb5.conf \
 *               GssServer
 *
 * Add -Djava.security.krb5.conf=krb5.conf to specify application-specific
 * Kerberos configuration (different from operating system's Kerberos
 * configuration).
 */

public class GssServer  {
    private static final int PORT = 4567;
    private static final boolean verbose = false;
    private static final int LOOP_LIMIT = 1;
    private static int loopCount = 0;

    public static void main(String[] args) throws Exception {

        PrivilegedExceptionAction action = new GssServerAction(PORT);

        Jaas.loginAndAction("server", action);
    }

    static class GssServerAction implements PrivilegedExceptionAction {
        private int localPort;

        GssServerAction(int port) {
            this.localPort = port;
        }

        public Object run() throws Exception {

            ServerSocket ss = new ServerSocket(localPort);

            // Get own Kerberos credentials for accepting connection
            GSSManager manager = GSSManager.getInstance();
            Oid krb5Mechanism = new Oid("1.2.840.113554.1.2.2");
            GSSCredential serverCreds = manager.createCredential(null,
                                             GSSCredential.DEFAULT_LIFETIME,
                                             krb5Mechanism,
                                             GSSCredential.ACCEPT_ONLY);
            while (loopCount++ < LOOP_LIMIT) {

                System.out.println("Waiting for incoming connection...");

                Socket socket = ss.accept();
                DataInputStream inStream =
                    new DataInputStream(socket.getInputStream());

                DataOutputStream outStream =
                    new DataOutputStream(socket.getOutputStream());

                System.out.println("Got connection from client " +
                    socket.getInetAddress());

                /*
                 * Create a GSSContext to receive the incoming request
                 * from the client. Use null for the server credentials
                 * passed in. This tells the underlying mechanism
                 * to use whatever credentials it has available that
                 * can be used to accept this connection.
                 */

                GSSContext context = manager.createContext(
                    (GSSCredential)serverCreds);

                // Do the context establishment loop

                byte[] token = null;

                while (!context.isEstablished()) {

                    if (verbose) {
                        System.out.println("Reading ...");
                    }
                    token = new byte[inStream.readInt()];

                    if (verbose) {
                        System.out.println("Will read input token of size " +
                            token.length + " for processing by acceptSecContext");
                    }
                    inStream.readFully(token);

                    if (token.length == 0) {
                        if (verbose) {
                            System.out.println("skipping zero length token");
                        }
                        continue;
                    }
                    if (verbose) {
                        System.out.println("Token = " + getHexBytes(token));
                        System.out.println("acceptSecContext..");
                    }
                    token = context.acceptSecContext(token, 0, token.length);

                    // Send a token to the peer if one was generated by
                    // acceptSecContext
                    if (token != null) {
                        if (verbose) {
                            System.out.println("Will send token of size " +
                                token.length + " from acceptSecContext.");
                        }

                        outStream.writeInt(token.length);
                        outStream.write(token);
                        outStream.flush();
                    }
                }

                System.out.println("Context Established! ");
                System.out.println("Client principal is " + context.getSrcName());
                System.out.println("Server principal is " + context.getTargName());

                /*
                 * If mutual authentication did not take place, then
                 * only the client was authenticated to the
                 * server. Otherwise, both client and server were
                 * authenticated to each other.
                 */
                if (context.getMutualAuthState())
                    System.out.println("Mutual authentication took place!");

                /*
                 * Create a MessageProp which unwrap will use to return
                 * information such as the Quality-of-Protection that was
                 * applied to the wrapped token, whether or not it was
                 * encrypted, etc. Since the initial MessageProp values
                 * are ignored, just set them to the defaults of 0 and false.
                 */
                MessageProp prop = new MessageProp(0, false);

                /*
                 * Read the token. This uses the same token byte array
                 * as that used during context establishment.
                 */
                token = new byte[inStream.readInt()];
                if (verbose) {
                    System.out.println("Will read token of size " + token.length);
                }
                inStream.readFully(token);

                byte[] input = context.unwrap(token, 0, token.length, prop);
                String str = new String(input, "UTF-8");

                System.out.println("Received data \"" +
                    str + "\" of length " + str.length());

                System.out.println("Confidentiality applied: " +
                    prop.getPrivacy());

                /*
                 * Now generate reply that is the concatenation of the
                 * incoming string with the current time.
                 */

                /*
                 * First reset the QOP of the MessageProp to 0
                 * to ensure the default Quality-of-Protection
                 * is applied.
                 */
                prop.setQOP(0);

                String now = new Date().toString();
                byte[] nowBytes = now.getBytes("UTF-8");
                int len = input.length + 1 + nowBytes.length;
                byte[] reply = new byte[len];
                System.arraycopy(input, 0, reply, 0, input.length);
                reply[input.length] = ' ';
                System.arraycopy(nowBytes, 0, reply, input.length+1,
                    nowBytes.length);

                System.out.println("Sending: " + new String(reply, "UTF-8"));
                token = context.wrap(reply, 0, reply.length, prop);

                outStream.writeInt(token.length);
                outStream.write(token);
                outStream.flush();

                System.out.println("Closing connection with client " +
                    socket.getInetAddress());
                context.dispose();
                socket.close();
            }
            return null;
        }
    }

    private static final String getHexBytes(byte[] bytes, int pos, int len) {

        StringBuffer sb = new StringBuffer();
        for (int i = pos; i < (pos+len); i++) {

            int b1 = (bytes[i]>>4) & 0x0f;
            int b2 = bytes[i] & 0x0f;

            sb.append(Integer.toHexString(b1));
            sb.append(Integer.toHexString(b2));
            sb.append(' ');
        }
        return sb.toString();
    }

    private static final String getHexBytes(byte[] bytes) {
        return getHexBytes(bytes, 0, bytes.length);
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__GSSCLIENT.JAVA-338B6631">
GssClient.java

``` {.oac_no_warn dir="ltr"}
import org.ietf.jgss.*;
import java.net.Socket;
import java.io.IOException;
import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.security.*;
import javax.security.auth.login.LoginException;

/**
 * A sample client application that uses JGSS to do mutual authentication
 * with a server using Kerberos as the underlying mechanism. It then
 * exchanges data securely with the server.
 *
 * Every message sent to the server includes a 4-byte application-level
 * header that contains the big-endian integer value for the number
 * of bytes that will follow as part of the JGSS token.
 *
 * The protocol is:
 *    1.  Context establishment loop:
 *         a. client sends init sec context token to server
 *         b. server sends accept sec context token to client
 *         ....
 *    2. client sends a wrapped token to the server.
 *    3. server sends a wrapped token back to the client for the application
 *
 * Start GssServer first before starting GssClient.
 *
 * Usage:  java <options> GssClient <service> <serverName>
 *
 * Example: java -Djava.security.auth.login.config=jaas-krb5.conf \
 *               GssClient host machine.imc.org
 *
 * Add -Djava.security.krb5.conf=krb5.conf to specify application-specific
 * Kerberos configuration (different from operating system's Kerberos
 * configuration).
 */

public class GssClient {
    private static final int PORT = 4567;
    private static final boolean verbose = false;

    public static void main(String[] args) throws Exception {

        // Obtain the command-line arguments and parse the server's principal

        if (args.length < 2) {
            System.err.println(
                "Usage: java <options> GssClient <service> <serverName>");
            System.exit(-1);
        }

        String serverPrinc = args[0] + "@" + args[1];

        PrivilegedExceptionAction action =
            new GssClientAction(serverPrinc, args[1], PORT);

        Jaas.loginAndAction("client", action);
    }

    static class GssClientAction implements PrivilegedExceptionAction {
        private String serverPrinc;
        private String hostName;
        private int port;

        GssClientAction(String serverPrinc, String hostName, int port) {
            this.serverPrinc = serverPrinc;
            this.hostName = hostName;
            this.port = port;
        }

        public Object run() throws Exception {
            Socket socket = new Socket(hostName, port);
            DataInputStream inStream =
                new DataInputStream(socket.getInputStream());
            DataOutputStream outStream =
                new DataOutputStream(socket.getOutputStream());

            System.out.println("Connected to address " +
                socket.getInetAddress());

            /*
             * This Oid is used to represent the Kerberos version 5 GSS-API
             * mechanism. It is defined in RFC 1964. We will use this Oid
             * whenever we need to indicate to the GSS-API that it must
             * use Kerberos for some purpose.
             */
            Oid krb5Oid = new Oid("1.2.840.113554.1.2.2");

            GSSManager manager = GSSManager.getInstance();

            /*
             * Create a GSSName out of the server's name.
             */
            GSSName serverName = manager.createName(serverPrinc,
                GSSName.NT_HOSTBASED_SERVICE);

            /*
             * Create a GSSContext for mutual authentication with the
             * server.
             *    - serverName is the GSSName that represents the server.
             *    - krb5Oid is the Oid that represents the mechanism to
             *      use. The client chooses the mechanism to use.
             *    - null is passed in for client credentials
             *    - DEFAULT_LIFETIME lets the mechanism decide how long the
             *      context can remain valid.
             * Note: Passing in null for the credentials asks GSS-API to
             * use the default credentials. This means that the mechanism
             * will look among the credentials stored in the current Subject
             * to find the right kind of credentials that it needs.
             */
            GSSContext context = manager.createContext(serverName,
                krb5Oid,
                null,
                GSSContext.DEFAULT_LIFETIME);

            // Set the desired optional features on the context. The client
            // chooses these options.

            context.requestMutualAuth(true);  // Mutual authentication
            context.requestConf(true);  // Will use confidentiality later
            context.requestInteg(true); // Will use integrity later

            // Do the context eastablishment loop

            byte[] token = new byte[0];

            while (!context.isEstablished()) {

                // token is ignored on the first call
                token = context.initSecContext(token, 0, token.length);

                // Send a token to the server if one was generated by
                // initSecContext
                if (token != null) {
                    if (verbose) {
                        System.out.println("Will send token of size " +
                            token.length + " from initSecContext.");
                        System.out.println("writing token = " +
                            getHexBytes(token));
                    }

                    outStream.writeInt(token.length);
                    outStream.write(token);
                    outStream.flush();
                }

                // If the client is done with context establishment
                // then there will be no more tokens to read in this loop
                if (!context.isEstablished()) {
                    token = new byte[inStream.readInt()];
                    if (verbose) {
                        System.out.println("reading token = " +
                            getHexBytes(token));
                        System.out.println("Will read input token of size " +
                            token.length + " for processing by initSecContext");
                    }
                    inStream.readFully(token);
                }
            }

            System.out.println("Context Established! ");
            System.out.println("Client principal is " + context.getSrcName());
            System.out.println("Server principal is " + context.getTargName());

            /*
             * If mutual authentication did not take place, then only the
             * client was authenticated to the server. Otherwise, both
             * client and server were authenticated to each other.
             */
            if (context.getMutualAuthState())
                System.out.println("Mutual authentication took place!");

            byte[] messageBytes = "Hello There!".getBytes("UTF-8");

            /*
             * The first MessageProp argument is 0 to request
             * the default Quality-of-Protection.
             * The second argument is true to request
             * privacy (encryption of the message).
             */
            MessageProp prop =  new MessageProp(0, true);

            /*
             * Encrypt the data and send it across. Integrity protection
             * is always applied, irrespective of confidentiality
             * (i.e., encryption).
             * You can use the same token (byte array) as that used when
             * establishing the context.
             */

            System.out.println("Sending message: " +
                new String(messageBytes, "UTF-8"));
            token = context.wrap(messageBytes, 0, messageBytes.length, prop);
            outStream.writeInt(token.length);
            outStream.write(token);
            outStream.flush();

            /*
             * Now we will allow the server to decrypt the message,
             * append a time/date on it, and send then it back.
             */

            token = new byte[inStream.readInt()];
            System.out.println("Will read token of size " + token.length);
            inStream.readFully(token);
            byte[] replyBytes = context.unwrap(token, 0, token.length, prop);

            System.out.println("Received message: " +
                new String(replyBytes, "UTF-8"));

            System.out.println("Done.");
            context.dispose();
            socket.close();

            return null;
        }
    }

    private static final String getHexBytes(byte[] bytes, int pos, int len) {

        StringBuffer sb = new StringBuffer();
        for (int i = pos; i < (pos+len); i++) {

            int b1 = (bytes[i]>>4) & 0x0f;
            int b2 = bytes[i] & 0x0f;

            sb.append(Integer.toHexString(b1));
            sb.append(Integer.toHexString(b2));
            sb.append(' ');
        }
        return sb.toString();
    }

    private static final String getHexBytes(byte[] bytes) {
        return getHexBytes(bytes, 0, bytes.length);
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__SASLTESTSERVER.JAVA-338B69BC">
SaslTestServer.java

``` {.oac_no_warn dir="ltr"}
import javax.security.sasl.*;
import javax.security.auth.callback.*;
import java.security.*;
import java.util.HashMap;
import java.net.*;
import java.util.Date;

/**
 * A sample server application that uses SASL to authenticate clients
 * using Kerberos as the underlying mechanism. It then
 * exchanges data securely with the client.
 *
 * This sample program uses a ficticious application-level protocol.
 * Every message exchanged between the client and server an 8-byte
 * header that consists of two integers: the first integer represesents
 * the application-level command or status code while the second integer
 * indicates the length of the SASL buffer. This header is followed by
 * the SASL buffer.
 *
 * The protocol is:
 *    1.  Authentication
 *         a. client sends initial response to server containing authentication
 *            information
 *         b. server accepts and evaluates response to generate challenge; it
 *            sends the challenge to the server.
 *         c. client evaluates challenge to generate response; it sends the
 *            response;
 *         d. Steps b and c are repeated until authentication succeeds or fails.
 *    2. client sends an encrypted message to the server.
 *    3. server decryptes the message and sends an encrypted one back
 *       that contains the original message plus the current time.
 *
 * Start SaslTestServer first before starting SaslTestClient.
 *
 * Usage:  java <options> SaslTestServer service serverName
 *
 * Example: java -Djava.security.auth.login.config=jaas-krb5.conf \
 *               SaslTestServer host machine.imc.org
 *
 * Add -Djava.security.krb5.conf=krb5.conf to specify application-specific
 * Kerberos configuration (different from operating system's Kerberos
 * configuration).
 */


public class SaslTestServer {
    private static final String MECH = "GSSAPI"; // SASL name for GSS-API/Kerberos
    private static final int PORT = 4568;
    private static final int LOOP_LIMIT = 1;
    private static int loopCount = 0;

    public static void main(String[] args) throws Exception {
        // Obtain the command-line arguments and parse the server's principal

        if (args.length < 2) {
            System.err.println(
                "Usage: java <options> SaslTestServer <service> <host>");
            System.exit(-1);
        }

        PrivilegedExceptionAction action =
            new SaslServerAction(args[0], args[1], PORT);

        Jaas.loginAndAction("server", action);
    }

    static class SaslServerAction implements PrivilegedExceptionAction {
        private String service;      // used for SASL authentication
        private String serverName;   // named used for SASL authentication
        private int localPort;
        private CallbackHandler cbh = new TestCallbackHandler();

        SaslServerAction(String service, String serverName, int port) {
            this.service = service;
            this.serverName = serverName;
            this.localPort = port;
        }

        public Object run() throws Exception {
            ServerSocket ss = new ServerSocket(localPort);

            HashMap<String,Object> props = new HashMap<String,Object>();
            props.put(Sasl.QOP, "auth-conf,auth-int,auth");

            // Loop, accepting requests from any client
            while (loopCount++ < LOOP_LIMIT) {
                System.out.println("Waiting for incoming connection...");
                Socket socket = ss.accept();

                // Create application-level connection to handle request
                AppConnection conn = new AppConnection(socket);

                // Normally, the application protocol will negotiate which
                // SASL mechanism to use. In this simplified example, we
                // will always use "GSSAPI", the name of the mechanism that does
                // Kerberos via GSS-API

                // Create SaslServer to perform authentication
                SaslServer srv = Sasl.createSaslServer(MECH,
                    service, serverName, props, cbh);

                if (srv == null) {
                    throw new Exception(
                        "Unable to find server implementation for " + MECH);
                }

                boolean auth = false;

                // Read initial response from client
                byte[] response = conn.receive(AppConnection.AUTH_CMD);
                AppConnection.AppReply clientMsg;

                while (!srv.isComplete()) {
                    try {
                        // Generate challenge based on response
                        byte[] challenge = srv.evaluateResponse(response);

                        if (srv.isComplete()) {
                            conn.send(AppConnection.SUCCESS, challenge);
                            auth = true;
                        } else {
                            clientMsg = conn.send(AppConnection.AUTH_INPROGRESS,
                                challenge);
                            response = clientMsg.getBytes();
                        }
                    } catch (SaslException e) {
                        // e.printStackTrace();
                        // Send failure notification to client
                        conn.send(AppConnection.FAILURE, null);
                        break;
                    }
                }

                // Check status of authentication
                if (srv.isComplete() && auth) {
                    System.out.print("Client authenticated; ");
                    System.out.println("authorized client is: " +
                        srv.getAuthorizationID());
                } else {
                    // Go get another client
                    System.out.println("Authentication failed. ");
                    continue;
                }

                String qop = (String) srv.getNegotiatedProperty(Sasl.QOP);
                System.out.println("Negotiated QOP: " + qop);

                // Now try to use security layer
                boolean sl = (qop.equals("auth-conf") || qop.equals("auth-int"));

                byte[] msg = conn.receive(AppConnection.DATA_CMD);
                byte[] realMsg = (sl ? srv.unwrap(msg, 0, msg.length) : msg);

                System.out.println("Received: " + new String(realMsg, "UTF-8"));

                // Construct reply to send to client
                String now = new Date().toString();
                byte[] nowBytes = now.getBytes("UTF-8");
                int len = realMsg.length + 1 + nowBytes.length;
                byte[] reply = new byte[len];
                System.arraycopy(realMsg, 0, reply, 0, realMsg.length);
                reply[realMsg.length] = ' ';
                System.arraycopy(nowBytes, 0, reply, realMsg.length+1,
                    nowBytes.length);

                System.out.println("Sending: " + new String(reply, "UTF-8"));

                byte[] realReply = (sl ? srv.wrap(reply, 0, reply.length) : reply);

                conn.send(AppConnection.SUCCESS, realReply);
            }
            return null;
        }
    }

    static class TestCallbackHandler implements CallbackHandler {

        public void handle(Callback[] callbacks)
            throws UnsupportedCallbackException {

            AuthorizeCallback acb = null;

            for (int i = 0; i < callbacks.length; i++) {
                if (callbacks[i] instanceof AuthorizeCallback) {
                    acb = (AuthorizeCallback) callbacks[i];
                } else {
                    throw new UnsupportedCallbackException(callbacks[i]);
                }
            }

            if (acb != null) {
                String authid = acb.getAuthenticationID();
                String authzid = acb.getAuthorizationID();
                if (authid.equals(authzid)) {
                    // Self is always authorized
                    acb.setAuthorized(true);

                } else {
                    // Should check some database for mapping and decide.
                    // Current simplified policy is to reject authzids that
                    // don't match authid

                    acb.setAuthorized(false);
                }

                if (acb.isAuthorized()) {
                    // Set canonicalized name.
                    // Should look up database for canonical names

                    acb.setAuthorizedID(authzid);
                }
            }
        }
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__SASLTESTCLIENT.JAVA-338B6D11">
SaslTestClient.java

``` {.oac_no_warn dir="ltr"}
import javax.security.sasl.*;
import javax.security.auth.callback.*;
import java.security.*;
import javax.security.auth.Subject;
import javax.security.auth.login.*;
import com.sun.security.auth.callback.*;
import java.util.HashMap;

/**
 * A sample client application that uses SASL to authenticate to
 * a server using Kerberos as the underlying mechanism. It then
 * exchanges data securely with the server.
 *
 * This sample program uses a ficticious application-level protocol.
 * Every message exchanged between the client and server an 8-byte
 * header that consists of two integers: the first integer represesents
 * the application-level command or status code while the second integer
 * indicates the length of the SASL buffer. This header is followed by
 * the SASL buffer.
 *
 * The protocol is:
 *    1.  Authentication
 *         a. client sends initial response to server containing authentication
 *            information
 *         b. server accepts and evaluates response to generate challenge; it
 *            sends the challenge to the server.
 *         c. client evaluates challenge to generate response; it sends the
 *            response;
 *         d. Steps b and c are repeated until authentication succeeds or fails.
 *    2. client sends an encrypted message to the server.
 *    3. server decryptes the message and sends an encrypted one back
 *       that contains the original message plus the current time.
 *
 * Start SaslTestServer first before starting SaslTestClient.
 *
 * Usage:  java <options> SaslTestClient service serverName
 *
 * Example: java -Djava.security.auth.login.config=jaas-krb5.conf \
 *               SaslTestClient host machine.imc.org
 *
 * Add -Djava.security.krb5.conf=krb5.conf to specify application-specific
 * Kerberos configuration (different from operating system's Kerberos
 * configuration).
 */

public class SaslTestClient {
    private static final String MECH = "GSSAPI"; // SASL name for GSS-API/Kerberos
    private static final int PORT = 4568;

    private static final byte[] EMPTY = new byte[0];

    public static void main(String[] args) throws Exception {
        // Obtain the command-line arguments and parse the server's principal

        if (args.length < 2) {
            System.err.println(
                "Usage: java <options> SaslTestClient <service> <serverName>");
            System.exit(-1);
        }

        PrivilegedExceptionAction action =
            new SaslClientAction(args[0], args[1], PORT);

        Jaas.loginAndAction("client", action);
    }

    static class SaslClientAction implements PrivilegedExceptionAction {
        private String service;      // used for SASL authentication
        private String serverName;   // name used for SASL authentication
        private int port;
        private CallbackHandler cbh = null; // Don't need handler for GSSAPI

        SaslClientAction(String service, String serverName, int port) {
            this.service = service;
            this.serverName = serverName;
            this.port = port;
        }

        public Object run() throws Exception {
            // Create application-level connection
            AppConnection conn = new AppConnection(serverName, port);

            HashMap<String,Object> props = new HashMap<String,Object>();
            // Request confidentiality
            props.put(Sasl.QOP, "auth-conf");

            // Create SaslClient to perform authentication
            SaslClient clnt = Sasl.createSaslClient(
                new String[]{MECH}, null, service, serverName, props, cbh);

            if (clnt == null) {
                throw new Exception(
                    "Unable to find client implementation for " + MECH);
            }

            byte[] response;
            byte[] challenge;

            // Get initial response for authentication
            response = clnt.hasInitialResponse() ?
                clnt.evaluateChallenge(EMPTY) : EMPTY;

            // Send initial response to server
            AppConnection.AppReply reply =
                conn.send(AppConnection.AUTH_CMD, response);

            // Repeat until authentication terminates
            while (!clnt.isComplete() &&
                (reply.getStatus() == AppConnection.AUTH_INPROGRESS ||
                 reply.getStatus() == AppConnection.SUCCESS)) {

                // Evaluate challenge to generate response
                challenge = reply.getBytes();
                response = clnt.evaluateChallenge(challenge);

                if (reply.getStatus() == AppConnection.SUCCESS) {
                    if (response != null) {
                        throw new Exception("Protocol error interacting with SASL");
                    }
                    break;
                }

                // Send response to server and read server's next challenge
                reply = conn.send(AppConnection.AUTH_CMD, response);
            }

            // Check status of authentication
            if (clnt.isComplete() && reply.getStatus() == AppConnection.SUCCESS) {
                System.out.println("Client authenticated.");
            } else {
                throw new Exception("Authentication failed: " +
                    " connection status? " + reply.getStatus());
            }

            String qop = (String) clnt.getNegotiatedProperty(Sasl.QOP);
            System.out.println("Negotiated QOP: " + qop);

            // Try out security layer
            boolean sl = (qop.equals("auth-conf") || qop.equals("auth-int"));

            byte[] msg = "Hello There!".getBytes("UTF-8");
            System.out.println("Sending: " + new String(msg, "UTF-8"));

            byte[] encrypted = (sl ? clnt.wrap(msg, 0, msg.length) : msg);

            reply = conn.send(AppConnection.DATA_CMD, encrypted);

            if (reply.getStatus() == AppConnection.SUCCESS) {
                byte[] encryptedReply = reply.getBytes();

                byte[] clearReply = (sl ? clnt.unwrap(encryptedReply,
                    0, encryptedReply.length) : encryptedReply);

                System.out.println("Received: " + new String(clearReply, "UTF-8"));
            } else {
                System.out.println("Failed exchange: " + reply.getStatus());
            }

            conn.close();

            return null;
        }
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JSSESERVER.JAVA-338B733A">
JsseServer.java

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.net.*;
import javax.net.ssl.*;
import java.util.Date;
import java.security.PrivilegedExceptionAction;
import java.security.Principal;

/*
 * Tests support for RFC 2712. Specify use of only a KRB5 cipher for both
 * client and server, by first doing a JAAS login for the server
 * without first doing a JAAS login for the client.
 */

public class JsseServer {

    private static final String KRB5_CIPHER = "TLS_KRB5_WITH_3DES_EDE_CBC_SHA";


    private static final int PORT = 4569;
    private static final boolean verbose = false;
    private static final int LOOP_LIMIT = 1;
    private static int loopCount = 0;

    public static void main(String[] args) throws Exception {

        PrivilegedExceptionAction action = new JsseServerAction(PORT);

        Jaas.loginAndAction("server", action);
    }

    static class JsseServerAction implements PrivilegedExceptionAction {
        private int localPort;

        JsseServerAction(int port) {
            this.localPort = port;
        }

        public Object run() throws Exception {

            SSLServerSocketFactory sslssf =
                (SSLServerSocketFactory) SSLServerSocketFactory.getDefault();
            SSLServerSocket sslServerSocket =
                (SSLServerSocket) sslssf.createServerSocket(localPort);

            // Enable only a KRB5 cipher suite.
            String enabledSuites[] = { KRB5_CIPHER };
            sslServerSocket.setEnabledCipherSuites(enabledSuites);
            // Should check for exception if enabledSuites is not supported

            while (loopCount++ < LOOP_LIMIT) {
                System.out.println("Waiting for incoming connection...");

                SSLSocket sslSocket = (SSLSocket) sslServerSocket.accept();

                System.out.println("Got connection from client " +
                    sslSocket.getInetAddress());

                BufferedReader in = new BufferedReader(new InputStreamReader(
                    sslSocket.getInputStream()));
                BufferedWriter out = new BufferedWriter(new OutputStreamWriter(
                    sslSocket.getOutputStream()));

                String inStr = in.readLine();
                System.out.println("Received " + inStr);

                String outStr = inStr + " " + new Date().toString() + "\n";
                out.write(outStr);
                System.out.println("Sending " + outStr);
                out.flush();

                String cipherSuiteChosen = sslSocket.getSession().getCipherSuite();
                System.out.println("Cipher suite in use: " + cipherSuiteChosen);
                Principal self = sslSocket.getSession().getLocalPrincipal();
                System.out.println("I am: " + self.toString());
                Principal peer = sslSocket.getSession().getPeerPrincipal();
                System.out.println("Client is: " + peer.toString());

                sslSocket.close();
            }
            return null;
        }
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__JSSECLIENT.JAVA-338B7667">
JsseClient.java

``` {.oac_no_warn dir="ltr"}
import java.io.*;
import java.net.*;
import javax.net.ssl.*;
import java.security.PrivilegedExceptionAction;
import java.security.Principal;

public class JsseClient {

    private static final String KRB5_CIPHER = "TLS_KRB5_WITH_3DES_EDE_CBC_SHA";

    private static final int PORT = 4569;
    private static final boolean verbose = false;

    public static void main(String[] args) throws Exception {
        // Obtain the command-line arguments and parse the server's name

        if (args.length < 1) {
            System.err.println(
                "Usage: java <options> JsseClient <serverName>");
            System.exit(-1);
        }

        PrivilegedExceptionAction action = new JsseClientAction(args[0], PORT);

        Jaas.loginAndAction("client", action);
    }

    static class JsseClientAction implements PrivilegedExceptionAction {
        private String server;
        private int port;

        JsseClientAction(String server, int port) {
            this.port = port;
            this.server = server;
        }

        public Object run() throws Exception {
            SSLSocketFactory sslsf =
                (SSLSocketFactory) SSLSocketFactory.getDefault();
            SSLSocket sslSocket = (SSLSocket) sslsf.createSocket(server, port);

            // Enable only a KRB5 cipher suite.
            String enabledSuites[] = { KRB5_CIPHER };
            sslSocket.setEnabledCipherSuites(enabledSuites);
            // Should check for exception if enabledSuites is not supported

            BufferedReader in = new BufferedReader(new InputStreamReader(
                sslSocket.getInputStream()));
            BufferedWriter out = new BufferedWriter(new OutputStreamWriter(
                sslSocket.getOutputStream()));

            String outStr = "Hello There!\n";
            out.write(outStr);
            out.flush();
            System.out.print("Sending " + outStr);

            String inStr = in.readLine();
            System.out.println("Received " + inStr);

            String cipherSuiteChosen = sslSocket.getSession().getCipherSuite();
            System.out.println("Cipher suite in use: " + cipherSuiteChosen);
            Principal self = sslSocket.getSession().getLocalPrincipal();
            System.out.println("I am: " + self.toString());
            Principal peer = sslSocket.getSession().getPeerPrincipal();
            System.out.println("Server is: " + peer.toString());

            sslSocket.close();
            return null;
        }
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__KRB5.CONF-338B7967">
krb5.conf

``` {.oac_no_warn dir="ltr"}
# krb5.conf template
# In order to complete this configuration file
# you will need to replace the __<name>__ placeholders
# with appropriate values for your network.
#
[libdefaults]
        default_realm = J1LABS.EXAMPLE.COM
    forwardable = true

default_tkt_enctypes = aes128-cts rc4-hmac des3-cbc-sha1
default_tgs_enctypes = aes128-cts rc4-hmac des3-cbc-sha1
permitted_enctypes   = aes128-cts rc4-hmac des3-cbc-sha1

[realms]
        J1LABS.EXAMPLE.COM = {
        kdc = j1hol-1280
                kdc = j1hol-004
                admin_server = j1hol-1280
        }

[domain_realm]
    .example.com = J1LABS.EXAMPLE.COM

[logging]
        default = FILE:/var/krb5/kdc.log
        kdc = FILE:/var/krb5/kdc.log
    kdc_rotate = {

# How often to rotate kdc.log. Logs will get rotated no more
# often than the period, and less often if the KDC is not used
# frequently.

        period = 1d

# how many versions of kdc.log to keep around (kdc.log.0, kdc.log.1, ...)

        versions = 10
    }

[appdefaults]
    gkadmin = {
                help_url = http://localhost:8888/ab2/coll.384.1/SEAM
        }

    kinit = {
        renewable = true
        forwardable= true
    }

        rlogin = {
                forwardable= true
        }
        rsh = {
                forwardable= true
        }
        telnet = {
                autologin = true
                forwardable= true
        }
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__GSSSPNEGOCLIENT.JAVA-338B7C31">
GssSpNegoClient.java

``` {.oac_no_warn dir="ltr"}
import org.ietf.jgss.*;
import java.net.Socket;
import java.io.IOException;
import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.security.*;
import javax.security.auth.login.LoginException;

/**
 * A sample client application that uses JGSS to do mutual authentication
 * with a server using Kerberos as the underlying mechanism. It then
 * exchanges data securely with the server.
 *
 * Every message sent to the server includes a 4-byte application-level
 * header that contains the big-endian integer value for the number
 * of bytes that will follow as part of the JGSS token.
 *
 * The protocol is:
 *    1.  Context establishment loop:
 *         a. client sends init sec context token to server
 *         b. server sends accept sec context token to client
 *         ....
 *    2. client sends a wrapped token to the server.
 *    3. server sends a wrapped token back to the client for the application
 *
 * Start GssServer first before starting GssClient.
 *
 * Usage:  java <options> GssSpNegoClient <service> <serverName>
 *
 * Example: java -Djava.security.auth.login.config=jaas-krb5.conf \
 *               GssSpNegoClient host machine.imc.org
 *
 * Add -Djava.security.krb5.conf=krb5.conf to specify application-specific
 * Kerberos configuration (different from operating system's Kerberos
 * configuration).
 */

public class GssSpNegoClient {
    private static final int PORT = 4567;
    private static final boolean verbose = false;

    public static void main(String[] args) throws Exception {

        // Obtain the command-line arguments and parse the server's principal

        if (args.length < 2) {
            System.err.println(
                "Usage: java <options> GssSpNegoClient <service> <serverName>");
            System.exit(-1);
        }

        String serverPrinc = args[0] + "@" + args[1];

        PrivilegedExceptionAction action =
            new GssClientAction(serverPrinc, args[1], PORT);

        Jaas.loginAndAction("client", action);
    }

    static class GssClientAction implements PrivilegedExceptionAction {
        private String serverPrinc;
        private String hostName;
        private int port;

        GssClientAction(String serverPrinc, String hostName, int port) {
            this.serverPrinc = serverPrinc;
            this.hostName = hostName;
            this.port = port;
        }

        public Object run() throws Exception {
            Socket socket = new Socket(hostName, port);
            DataInputStream inStream =
                new DataInputStream(socket.getInputStream());
            DataOutputStream outStream =
                new DataOutputStream(socket.getOutputStream());

            System.out.println("Connected to address " +
                socket.getInetAddress());

            /*
             * This Oid is used to represent the SPNEGO GSS-API
             * mechanism. It is defined in RFC 2478. We will use this Oid
             * whenever we need to indicate to the GSS-API that it must
             * use SPNEGO for some purpose.
             */
            Oid spnegoOid = new Oid("1.3.6.1.5.5.2");

            GSSManager manager = GSSManager.getInstance();

            /*
             * Create a GSSName out of the server's name.
             */
            GSSName serverName = manager.createName(serverPrinc,
                GSSName.NT_HOSTBASED_SERVICE, spnegoOid);

            /*
             * Create a GSSContext for mutual authentication with the
             * server.
             *    - serverName is the GSSName that represents the server.
             *    - krb5Oid is the Oid that represents the mechanism to
             *      use. The client chooses the mechanism to use.
             *    - null is passed in for client credentials
             *    - DEFAULT_LIFETIME lets the mechanism decide how long the
             *      context can remain valid.
             * Note: Passing in null for the credentials asks GSS-API to
             * use the default credentials. This means that the mechanism
             * will look among the credentials stored in the current Subject
             * to find the right kind of credentials that it needs.
             */
            GSSContext context = manager.createContext(serverName,
                spnegoOid,
                null,
                GSSContext.DEFAULT_LIFETIME);

            // Set the desired optional features on the context. The client
            // chooses these options.

            context.requestMutualAuth(true);  // Mutual authentication
            context.requestConf(true);  // Will use confidentiality later
            context.requestInteg(true); // Will use integrity later

            // Do the context eastablishment loop

            byte[] token = new byte[0];

            while (!context.isEstablished()) {

                // token is ignored on the first call
                token = context.initSecContext(token, 0, token.length);

                // Send a token to the server if one was generated by
                // initSecContext
                if (token != null) {
                    if (verbose) {
                        System.out.println("Will send token of size " +
                            token.length + " from initSecContext.");
                        System.out.println("writing token = " +
                            getHexBytes(token));
                    }

                    outStream.writeInt(token.length);
                    outStream.write(token);
                    outStream.flush();
                }

                // If the client is done with context establishment
                // then there will be no more tokens to read in this loop
                if (!context.isEstablished()) {
                    token = new byte[inStream.readInt()];
                    if (verbose) {
                        System.out.println("reading token = " +
                            getHexBytes(token));
                        System.out.println("Will read input token of size " +
                            token.length + " for processing by initSecContext");
                    }
                    inStream.readFully(token);
                }
            }

            System.out.println("Context Established! ");
            System.out.println("Client principal is " + context.getSrcName());
            System.out.println("Server principal is " + context.getTargName());

            /*
             * If mutual authentication did not take place, then only the
             * client was authenticated to the server. Otherwise, both
             * client and server were authenticated to each other.
             */
            if (context.getMutualAuthState())
                System.out.println("Mutual authentication took place!");

            byte[] messageBytes = "Hello There!".getBytes("UTF-8");

            /*
             * The first MessageProp argument is 0 to request
             * the default Quality-of-Protection.
             * The second argument is true to request
             * privacy (encryption of the message).
             */
            MessageProp prop =  new MessageProp(0, true);

            /*
             * Encrypt the data and send it across. Integrity protection
             * is always applied, irrespective of confidentiality
             * (i.e., encryption).
             * You can use the same token (byte array) as that used when
             * establishing the context.
             */

            System.out.println("Sending message: " +
                new String(messageBytes, "UTF-8"));
            token = context.wrap(messageBytes, 0, messageBytes.length, prop);
            outStream.writeInt(token.length);
            outStream.write(token);
            outStream.flush();

            /*
             * Now we will allow the server to decrypt the message,
             * append a time/date on it, and send then it back.
             */

            token = new byte[inStream.readInt()];
            System.out.println("Will read token of size " + token.length);
            inStream.readFully(token);
            byte[] replyBytes = context.unwrap(token, 0, token.length, prop);

            System.out.println("Received message: " +
                new String(replyBytes, "UTF-8"));

            System.out.println("Done.");
            context.dispose();
            socket.close();

            return null;
        }
    }

    private static final String getHexBytes(byte[] bytes, int pos, int len) {

        StringBuffer sb = new StringBuffer();
        for (int i = pos; i < (pos+len); i++) {

            int b1 = (bytes[i]>>4) & 0x0f;
            int b2 = bytes[i] & 0x0f;

            sb.append(Integer.toHexString(b1));
            sb.append(Integer.toHexString(b2));
            sb.append(' ');
        }
        return sb.toString();
    }

    private static final String getHexBytes(byte[] bytes) {
        return getHexBytes(bytes, 0, bytes.length);
    }
}
```

</div>
<!-- class="section" -->

<div class="section" id="GUID-40AF52E5-ECEA-4E5F-B0C1-35C150C7BB6E__GSSSPNEGOSERVER.JAVA-338B7F93">
GssSpNegoServer.java

``` {.oac_no_warn dir="ltr"}
import org.ietf.jgss.*;
import java.io.*;
import java.net.Socket;
import java.net.ServerSocket;
import java.security.*;
import java.util.Date;

/**
 * A sample server application that uses JGSS to do mutual authentication
 * with a client using Kerberos as the underlying mechanism. It then
 * exchanges data securely with the client.
 *
 * Every message exchanged with the client includes a 4-byte application-
 * level header that contains the big-endian integer value for the number
 * of bytes that will follow as part of the JGSS token.
 *
 * The protocol is:
 *    1.  Context establishment loop:
 *         a. client sends init sec context token to server
 *         b. server sends accept sec context token to client
 *         ....
 *    2. client sends a wrap token to the server.
 *    3. server sends a wrap token back to the client.
 *
 * Start GssSpNegoServer first before starting GssClient.
 *
 * Usage:  java <options> GssSpNegoServer
 *
 * Example: java -Djava.security.auth.login.config=jaas-krb5.conf \
 *               GssSpNegoServer
 *
 * Add -Djava.security.krb5.conf=krb5.conf to specify application-specific
 * Kerberos configuration (different from operating system's Kerberos
 * configuration).
 */

public class GssSpNegoServer  {
    private static final int PORT = 4567;
    private static final boolean verbose = false;
    private static final int LOOP_LIMIT = 1;
    private static int loopCount = 0;

    public static void main(String[] args) throws Exception {

        PrivilegedExceptionAction action = new GssServerAction(PORT);

        Jaas.loginAndAction("server", action);
    }

    static class GssServerAction implements PrivilegedExceptionAction {
        private int localPort;

        GssServerAction(int port) {
            this.localPort = port;
        }

        public Object run() throws Exception {

            ServerSocket ss = new ServerSocket(localPort);

            // Get own Kerberos credentials for accepting connection
            GSSManager manager = GSSManager.getInstance();
            Oid spnegoOid = new Oid("1.3.6.1.5.5.2");
            GSSCredential serverCreds = manager.createCredential(null,
                                             GSSCredential.DEFAULT_LIFETIME,
                                             spnegoOid,
                                             GSSCredential.ACCEPT_ONLY);
            while (loopCount++ < LOOP_LIMIT) {

                System.out.println("Waiting for incoming connection...");

                Socket socket = ss.accept();
                DataInputStream inStream =
                    new DataInputStream(socket.getInputStream());

                DataOutputStream outStream =
                    new DataOutputStream(socket.getOutputStream());

                System.out.println("Got connection from client " +
                    socket.getInetAddress());

                /*
                 * Create a GSSContext to receive the incoming request
                 * from the client. Use null for the server credentials
                 * passed in. This tells the underlying mechanism
                 * to use whatever credentials it has available that
                 * can be used to accept this connection.
                 */

                GSSContext context = manager.createContext(
                    (GSSCredential)serverCreds);

                // Do the context establishment loop

                byte[] token = null;

                while (!context.isEstablished()) {

                    if (verbose) {
                        System.out.println("Reading ...");
                    }
                    token = new byte[inStream.readInt()];

                    if (verbose) {
                        System.out.println("Will read input token of size " +
                            token.length + " for processing by acceptSecContext");
                    }
                    inStream.readFully(token);

                    if (token.length == 0) {
                        if (verbose) {
                            System.out.println("skipping zero length token");
                        }
                        continue;
                    }
                    if (verbose) {
                        System.out.println("Token = " + getHexBytes(token));
                        System.out.println("acceptSecContext..");
                    }
                    token = context.acceptSecContext(token, 0, token.length);

                    // Send a token to the peer if one was generated by
                    // acceptSecContext
                    if (token != null) {
                        if (verbose) {
                            System.out.println("Will send token of size " +
                                token.length + " from acceptSecContext.");
                        }

                        outStream.writeInt(token.length);
                        outStream.write(token);
                        outStream.flush();
                    }
                }

                System.out.println("Context Established! ");
                System.out.println("Client principal is " + context.getSrcName());
                System.out.println("Server principal is " + context.getTargName());

                /*
                 * If mutual authentication did not take place, then
                 * only the client was authenticated to the
                 * server. Otherwise, both client and server were
                 * authenticated to each other.
                 */
                if (context.getMutualAuthState())
                    System.out.println("Mutual authentication took place!");

                /*
                 * Create a MessageProp which unwrap will use to return
                 * information such as the Quality-of-Protection that was
                 * applied to the wrapped token, whether or not it was
                 * encrypted, etc. Since the initial MessageProp values
                 * are ignored, just set them to the defaults of 0 and false.
                 */
                MessageProp prop = new MessageProp(0, false);

                /*
                 * Read the token. This uses the same token byte array
                 * as that used during context establishment.
                 */
                token = new byte[inStream.readInt()];
                if (verbose) {
                    System.out.println("Will read token of size " + token.length);
                }
                inStream.readFully(token);

                byte[] input = context.unwrap(token, 0, token.length, prop);
                String str = new String(input, "UTF-8");

                System.out.println("Received data \"" +
                    str + "\" of length " + str.length());

                System.out.println("Confidentiality applied: " +
                    prop.getPrivacy());

                /*
                 * Now generate reply that is the concatenation of the
                 * incoming string with the current time.
                 */

                /*
                 * First reset the QOP of the MessageProp to 0
                 * to ensure the default Quality-of-Protection
                 * is applied.
                 */
                prop.setQOP(0);

                String now = new Date().toString();
                byte[] nowBytes = now.getBytes("UTF-8");
                int len = input.length + 1 + nowBytes.length;
                byte[] reply = new byte[len];
                System.arraycopy(input, 0, reply, 0, input.length);
                reply[input.length] = ' ';
                System.arraycopy(nowBytes, 0, reply, input.length+1,
                    nowBytes.length);

                System.out.println("Sending: " + new String(reply, "UTF-8"));
                token = context.wrap(reply, 0, reply.length, prop);

                outStream.writeInt(token.length);
                outStream.write(token);
                outStream.flush();

                System.out.println("Closing connection with client " +
                    socket.getInetAddress());
                context.dispose();
                socket.close();
            }
            return null;
        }
    }

    private static final String getHexBytes(byte[] bytes, int pos, int len) {

        StringBuffer sb = new StringBuffer();
        for (int i = pos; i < (pos+len); i++) {

            int b1 = (bytes[i]>>4) & 0x0f;
            int b2 = bytes[i] & 0x0f;

            sb.append(Integer.toHexString(b1));
            sb.append(Integer.toHexString(b2));
            sb.append(' ');
        }
        return sb.toString();
    }

    private static final String getHexBytes(byte[] bytes) {
        return getHexBytes(bytes, 0, bytes.length);
    }
}
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
| -------------------  | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| ------------- --     | e | )\                   |
|                   [! | L |             <span cl |
| [Previous](../../dco | o | ass="icon">Contents< |
| mmon/gifs/leftnav.gi | g | /span>](toc.htm)     |
| f)\                  | o |   -- --------------- |
|                [![Ne | ] | -------------------- |
| xt](../../dcommon/gi | ( | -------------------- |
| fs/rightnav.gif)\    | . | ---                  |
|                      | . |                      |
|    <span class="icon | / |                      |
| ">Previous</span>](p | . |                      |
| art-vi-http-spnego-a | . |                      |
| uthentication.htm)   | / |                      |
|  <span class="icon"> | d |                      |
| Next</span>](appendi | c |                      |
| x-setting-kerberos-a | o |                      |
| ccounts.htm)         | m |                      |
|   ------------------ | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| -------------------  | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------------------- | f |                      |
| ------------- --     | s |                      |
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
