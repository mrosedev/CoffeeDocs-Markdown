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

  ---------------------------------------------------------------------- ----------------------------------------------------- --
              [![Previous](../../dcommon/gifs/leftnav.gif)\                   [![Next](../../dcommon/gifs/rightnav.gif)\       
   <span class="icon">Previous</span>](security-api-specification1.htm)   <span class="icon">Next</span>](security-tools.htm)  
  ---------------------------------------------------------------------- ----------------------------------------------------- --

[]{#BEGIN}

</div>
<!-- class="header" -->

<div class="ind">
[]{#GUID-E1A1E8ED-B39F-404B-8036-637F697B45A2}<!-- End Header -->

<span class="enumeration_chapter">14 </span>Deprecated Security APIs Marked for Removal {#JSSEC-GUID-E1A1E8ED-B39F-404B-8036-637F697B45A2 .sect1}
=======================================================================================

<div>
The following APIs are deprecated and eligible to be removed in a future
release.

<div class="section">
You can check the API dependencies using the `jdeprscan`{.codeph} tool.
See [jdeprscan](olink:JSWOR-GUID-2B7588B0-92DB-4A88-88D4-24D183660A62)
in <span><cite>Java Platform, Standard Edition Tools
Reference</cite></span>.

The following classes are deprecated and marked for removal:

-   <span class="apiname">com.sun.security.auth.PolicyFile</span>
-   <span class="apiname">com.sun.security.auth.SolarisNumericGroupPrincipal</span>
-   <span class="apiname">com.sun.security.auth.SolarisNumericUserPrincipal</span>
-   <span class="apiname">com.sun.security.auth.SolarisPrincipal</span>
-   <span class="apiname">com.sun.security.auth.X500Principal</span>
-   <span class="apiname">com.sun.security.auth.module.SolarisLoginModule</span>
-   <span class="apiname">com.sun.security.auth.module.SolarisSystem</span>

The following methods are deprecated and marked for removal:

-   <span class="apiname">java.lang.SecurityManager.getInCheck</span>
-   <span class="apiname">java.lang.SecurityManager.checkMemberAccess</span>
-   <span class="apiname">java.lang.SecurityManager.classDepth</span>
-   <span class="apiname">java.lang.SecurityManager.currentClassLoader</span>
-   <span class="apiname">java.lang.SecurityManager.currentLoadedClass</span>
-   <span class="apiname">java.lang.SecurityManager.inClass</span>
-   <span class="apiname">java.lang.SecurityManager.inClassLoader</span>
-   <span class="apiname">java.lang.SecurityManager.checkAwtEventQueueAccess</span>
-   <span class="apiname">java.lang.SecurityManager.checkTopLevelWindow</span>
-   <span class="apiname">java.lang.SecurityManager.checkSystemClipboardAccess</span>

The following field is deprecated and marked for removal:

-   <span class="apiname">java.lang.SecurityManager.incheck</span>

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
| ------------ ------- | r | ---                  |
| -------------------- | a |       [![Go To Table |
| -------------------- | c |  Of Contents](../../ |
| ------ --            | l | dcommon/gifs/toc.gif |
|               [![Pre | e | )\                   |
| vious](../../dcommon | L |             <span cl |
| /gifs/leftnav.gif)\  | o | ass="icon">Contents< |
|                   [! | g | /span>](toc.htm)     |
| [Next](../../dcommon | o |   -- --------------- |
| /gifs/rightnav.gif)\ | ] | -------------------- |
|                      | ( | -------------------- |
|    <span class="icon | . | ---                  |
| ">Previous</span>](s | . |                      |
| ecurity-api-specific | / |                      |
| ation1.htm)   <span  | . |                      |
| class="icon">Next</s | . |                      |
| pan>](security-tools | / |                      |
| .htm)                | d |                      |
|   ------------------ | c |                      |
| -------------------- | o |                      |
| -------------------- | m |                      |
| ------------ ------- | m |                      |
| -------------------- | o |                      |
| -------------------- | n |                      |
| ------ --            | / |                      |
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
