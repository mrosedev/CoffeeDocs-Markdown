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

  ------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------- --
            [![Previous](../../dcommon/gifs/leftnav.gif)\                                           [![Next](../../dcommon/gifs/rightnav.gif)\                                 
   <span class="icon">Previous</span>](pkcs11-reference-guide1.htm)   <span class="icon">Next</span>](java-authentication-and-authorization-service-jaas-reference-guide.htm)  
  ------------------------------------------------------------------ --------------------------------------------------------------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-76141D9C-03F1-40D8-93D8-DFFC2143A2CA}<!-- End Header -->

<span class="enumeration_chapter">6 </span>Java Authentication and Authorization Service (JAAS) {#JSSEC-GUID-76141D9C-03F1-40D8-93D8-DFFC2143A2CA .sect1}
===============================================================================================

<div>
[Java Authentication and Authorization Service (JAAS) Reference
Guide](java-authentication-and-authorization-service-jaas-reference-guide.htm#GUID-2A935F5E-0803-411D-B6BC-F8C64D01A25C)
describes Java Authentication and Authorization Service (JAAS), which
enables you to authenticate users and securely determine who is
currently executing Java code, and authorize users to ensure that they
have the access control rights, or permissions, required to do the
actions performed.

[JAAS
Tutorials](jaas-tutorials.htm#GUID-272DB20A-B590-4B2E-BD60-7EF9EB54AB5A)
provides tutorials about Java Authentication and Authorization Service
(JAAS) authentication and authorization.

[Java Authentication and Authorization Service (JAAS): LoginModule
Developer\'s
Guide](java-authentication-and-authorization-service-jaas-loginmodule-developers-guide1.htm#GUID-CB46C30D-FFF1-466F-B2F5-6DE0BD5DA43A)
shows you how to implement the <span class="apiname">LoginModule</span>
interface, which you plug into an application to provide a particular
type of authentication.

</div>
</div>
<!-- class="ind" --><!-- Start Footer -->

<div class="footer">

------------------------------------------------------------------------

+----------------------+---+---------------------:+
|   ------------------ | ! |   -- --------------- |
| -------------------- | [ | -------------------- |
| -------------------- | O | -------------------- |
| -------- ----------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| -------------------- | l | dcommon/gifs/toc.gif |
| -------------------- | e | )\                   |
| -------------- --    | L |             <span cl |
|             [![Previ | o | ass="icon">Contents< |
| ous](../../dcommon/g | g | /span>](toc.htm)     |
| ifs/leftnav.gif)\    | o |   -- --------------- |
|                      | ] | -------------------- |
|                      | ( | -------------------- |
| [![Next](../../dcomm | . | ---                  |
| on/gifs/rightnav.gif | . |                      |
| )\                   | / |                      |
|                      | . |                      |
|    <span class="icon | . |                      |
| ">Previous</span>](p | / |                      |
| kcs11-reference-guid | d |                      |
| e1.htm)   <span clas | c |                      |
| s="icon">Next</span> | o |                      |
| ](java-authenticatio | m |                      |
| n-and-authorization- | m |                      |
| service-jaas-referen | o |                      |
| ce-guide.htm)        | n |                      |
|   ------------------ | / |                      |
| -------------------- | g |                      |
| -------------------- | i |                      |
| -------- ----------- | f |                      |
| -------------------- | s |                      |
| -------------------- | / |                      |
| -------------------- | o |                      |
| -------------------- | r |                      |
| -------------- --    | a |                      |
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
