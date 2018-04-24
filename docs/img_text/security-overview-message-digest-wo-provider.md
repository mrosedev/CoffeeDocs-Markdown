<div>
This image consists of five cylinders that represent the following:

-   Application

-   Provider Framework

-   `ProviderA`{.codeph}: Message digest implementations SHA384 and
    SHA512

-   `ProviderB`{.codeph}: Message digest implementations SHA256 and
    SHA384

-   `ProviderC`{.codeph}: Message digest implementations SHA256 and
    SHA512

An arrow representing a call to
`MessageDigest.getInstance("SHA-256")`{.codeph} starts from the
Application cylinder and passes through the following cylinders in the
indicated order:

1.  Provider Framework

2.  `ProviderA`{.codeph}

3.  `ProviderB`{.codeph}

4.  Provider Framework

The arrow ends at the Application cylinder. The call to
`MessageDigest.getInstance("SHA-256")`{.codeph} has returned a SHA-256
message digest implementation from `ProviderB`{.codeph}.

</div>
<div class="footer">
![Oracle Logo](../../../dcommon/gifs/oracle.gif){.copyrightlogo} [\
<span class="copyrightlogo">Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.</span>](../../../dcommon/html/cpyr.htm)

</div>
