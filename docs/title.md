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

  ----------------------------------------------- ---------------------------------------------- --
   [![Previous](../../dcommon/gifs/leftnav.gif)\    [![Next](../../dcommon/gifs/rightnav.gif)\   
   <span class="icon">Previous</span>](toc.htm)    <span class="icon">Next</span>](preface.htm)  
  ----------------------------------------------- ---------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
<!-- End Header -->

Java Platform, Standard Edition {#java-platform-standard-edition .docinfo}
===============================

Security Developer's Guide

<span class="revnumber">Release 11</span>

E94828-01

September 2018

<div>
This guide helps you to understand the Java security technology, tools,
and implementations of commonly used security algorithms, mechanisms,
and protocols on the Java Platform, Standard Edition (Java SE).

</div>
[]{#sthref1}

------------------------------------------------------------------------

Java Platform, Standard Edition Security Developer's Guide,
<span>Release 11</span>

E94828-01

Copyright © 1993, 2018,
Oracle and/or its affiliates. All rights reserved.

<div>
This software and related documentation are provided under a license
agreement containing restrictions on use and disclosure and are
protected by intellectual property laws. Except as expressly permitted
in your license agreement or allowed by law, you may not use, copy,
reproduce, translate, broadcast, modify, license, transmit, distribute,
exhibit, perform, publish, or display any part, in any form, or by any
means. Reverse engineering, disassembly, or decompilation of this
software, unless required by law for interoperability, is prohibited.

The information contained herein is subject to change without notice and
is not warranted to be error-free. If you find any errors, please report
them to us in writing.

</div>
<div>
If this is software or related documentation that is delivered to the
U.S. Government or anyone licensing it on behalf of the U.S. Government,
then the following notice is applicable:

U.S. GOVERNMENT END USERS: Oracle programs, including any operating
system, integrated software, any programs installed on the hardware,
and/or documentation, delivered to U.S. Government end users are
\"commercial computer software\" pursuant to the applicable Federal
Acquisition Regulation and agency-specific supplemental regulations. As
such, use, duplication, disclosure, modification, and adaptation of the
programs, including any operating system, integrated software, any
programs installed on the hardware, and/or documentation, shall be
subject to license terms and license restrictions applicable to the
programs. No other rights are granted to the U.S. Government.

</div>
<div>
This software or hardware is developed for general use in a variety of
information management applications. It is not developed or intended for
use in any inherently dangerous applications, including applications
that may create a risk of personal injury. If you use this software or
hardware in dangerous applications, then you shall be responsible to
take all appropriate fail-safe, backup, redundancy, and other measures
to ensure its safe use. Oracle Corporation and its affiliates disclaim
any liability for any damages caused by use of this software or hardware
in dangerous applications.

</div>
<div>
Oracle and Java are registered trademarks of Oracle and/or its
affiliates. Other names may be trademarks of their respective owners.

Intel and Intel Xeon are trademarks or registered trademarks of Intel
Corporation. All SPARC trademarks are used under license and are
trademarks or registered trademarks of SPARC International, Inc. AMD,
Opteron, the AMD logo, and the AMD Opteron logo are trademarks or
registered trademarks of Advanced Micro Devices. UNIX is a registered
trademark of The Open Group.

</div>
<div>
This software or hardware and documentation may provide access to or
information about content, products, and services from third parties.
Oracle Corporation and its affiliates are not responsible for and
expressly disclaim all warranties of any kind with respect to
third-party content, products, and services unless otherwise set forth
in an applicable agreement between you and Oracle. Oracle Corporation
and its affiliates will not be responsible for any loss, costs, or
damages incurred due to your access to or use of third-party content,
products, or services, except as set forth in an applicable agreement
between you and Oracle.

</div>
</div>
<!-- class="ind" --> <!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   -- --------------- |
| -------------------- | [ | -------------------- |
| --------- ---------- | O | -------------------- |
| -------------------- | r | ---                  |
| ---------------- --  | a |       [![Go To Table |
|    [![Previous](../. | c |  Of Contents](../../ |
| ./dcommon/gifs/leftn | l | dcommon/gifs/toc.gif |
| av.gif)\    [![Next] | e | )\                   |
| (../../dcommon/gifs/ | L |             <span cl |
| rightnav.gif)\       | o | ass="icon">Contents< |
|    <span class="icon | g | /span>](toc.htm)     |
| ">Previous</span>](t | o |   -- --------------- |
| oc.htm)    <span cla | ] | -------------------- |
| ss="icon">Next</span | ( | -------------------- |
| >](preface.htm)      | . | ---                  |
|   ------------------ | . |                      |
| -------------------- | / |                      |
| --------- ---------- | . |                      |
| -------------------- | . |                      |
| ---------------- --  | / |                      |
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