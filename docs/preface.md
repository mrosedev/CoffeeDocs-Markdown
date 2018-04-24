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

  ------------------------------------------------ -------------------------------------------------------- --
   [![Previous](../../dcommon/gifs/leftnav.gif)\          [![Next](../../dcommon/gifs/rightnav.gif)\        
   <span class="icon">Previous</span>](title.htm)   <span class="icon">Next</span>](general-security1.htm)  
  ------------------------------------------------ -------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-C49D47BA-EA16-4F4F-90CE-DAD9B984D823}<!-- End Header -->
[]{#JSDPG649}

Preface {#JSSEC-GUID-C49D47BA-EA16-4F4F-90CE-DAD9B984D823 .sect1}
=======

<div>
This guide provides information about the Java security technology,
tools, and implementations of commonly used security algorithms,
mechanisms, and protocols on the Java Platform, Standard Edition (Java
SE).

</div>
[]{#JSDPG650}

<div class="sect2">
[]{#GUID-4E10EE4D-C026-4A83-9270-B63AEB3E96F5}

Audience {#JSSEC-GUID-4E10EE4D-C026-4A83-9270-B63AEB3E96F5 .sect2}
--------

<div>
This document is intended for experienced developers who build
applications using the comprehensive Java security framework. It is also
intended for the user or administrator with a a set of tools to securely
manage applications.

</div>
</div>
[]{#JSDPG651}

<div class="sect2">
[]{#GUID-E409CC44-9A8F-4043-82C8-6B95CD939296}

Documentation Accessibility {#JSSEC-GUID-E409CC44-9A8F-4043-82C8-6B95CD939296 .sect2}
---------------------------

<div>
For information about Oracle\'s commitment to accessibility, visit the
Oracle Accessibility Program website at
<http://www.oracle.com/pls/topic/lookup?ctx=acc&id=docacc>.

<div class="section" id="GUID-E409CC44-9A8F-4043-82C8-6B95CD939296__GUID-D88DC1A6-B2C8-4B61-85D2-23B0215F1664">
Access to Oracle Support

Oracle customers that have purchased support have access to electronic
support through My Oracle Support. For information, visit
<http://www.oracle.com/pls/topic/lookup?ctx=acc&id=info> or visit
<http://www.oracle.com/pls/topic/lookup?ctx=acc&id=trs> if you are
hearing impaired.

</div>
<!-- class="section" -->

</div>
</div>
[]{#JSDPG653}

<div class="sect2">
[]{#GUID-7242A5DD-3D31-416A-BD79-5B49A9CF7583}

Related Documents {#JSSEC-GUID-7242A5DD-3D31-416A-BD79-5B49A9CF7583 .sect2}
-----------------

<div>
See <span>[JDK 10
Documentation](https://www.oracle.com/pls/topic/lookup?ctx=javase10&id=homepage)</span>.

</div>
</div>
[]{#JSDPG654}

<div class="sect2">
[]{#GUID-75D45AA0-5C30-4EB1-8954-FB75E303F2DC}

Conventions {#JSSEC-GUID-75D45AA0-5C30-4EB1-8954-FB75E303F2DC .sect2}
-----------

<div>
The following text conventions are used in this document:

<div class="tblformal" id="GUID-75D45AA0-5C30-4EB1-8954-FB75E303F2DC__GUID-35003CE2-9DC5-4A67-8808-256725DFFD46">
+-----------------------------------+-----------------------------------+
| Convention                        | Meaning                           |
+:==================================+:==================================+
| <span class="bold">boldface</span | Boldface type indicates graphical |
| >                                 | user interface elements           |
|                                   | associated with an action, or     |
|                                   | terms defined in text or the      |
|                                   | glossary.                         |
+-----------------------------------+-----------------------------------+
| <span class="italic">italic</span | Italic type indicates book        |
| >                                 | titles, emphasis, or placeholder  |
|                                   | variables for which you supply    |
|                                   | particular values.                |
+-----------------------------------+-----------------------------------+
| `monospace`{.codeph}              | Monospace type indicates commands |
|                                   | within a paragraph, URLs, code in |
|                                   | examples, text that appears on    |
|                                   | the screen, or text that you      |
|                                   | enter.                            |
+-----------------------------------+-----------------------------------+

</div>
<!-- class="inftblhruleinformal" -->

</div>
</div>
</div>
<!-- class="ind" --><!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   -- --------------- |
| -------------------- | [ | -------------------- |
| ---------- --------- | O | -------------------- |
| -------------------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| ------- --           | c |  Of Contents](../../ |
|    [![Previous](../. | l | dcommon/gifs/toc.gif |
| ./dcommon/gifs/leftn | e | )\                   |
| av.gif)\          [! | L |             <span cl |
| [Next](../../dcommon | o | ass="icon">Contents< |
| /gifs/rightnav.gif)\ | g | /span>](toc.htm)     |
|                      | o |   -- --------------- |
|    <span class="icon | ] | -------------------- |
| ">Previous</span>](t | ( | -------------------- |
| itle.htm)   <span cl | . | ---                  |
| ass="icon">Next</spa | . |                      |
| n>](general-security | / |                      |
| 1.htm)               | . |                      |
|   ------------------ | . |                      |
| -------------------- | / |                      |
| ---------- --------- | d |                      |
| -------------------- | c |                      |
| -------------------- | o |                      |
| ------- --           | m |                      |
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
