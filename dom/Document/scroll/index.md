---
title: 'scroll'
attributions:
  - 'Microsoft Developer Network: [[Windows Internet Explorer API reference](http://msdn.microsoft.com/en-us/library/ie/hh828809%28v=vs.85%29.aspx) Article]'
notes:
  - 'Needs summary, examples, spec, compat'
readiness: 'Not Ready'
tags:
  - Events
  - Needs_Summary
  - Needs_Examples
uri: dom/Document/scroll

---
## Overview Table

<table class="wikitable">
<tr>
<th>
Synchronous

</th>
<td>
No

</td>
</tr>
<tr>
<th>
Bubbles

</th>
<td>
No

</td>
</tr>
<tr>
<th>
Target

</th>
<td>
dom/Element

</td>
</tr>
<tr>
<th>
Cancelable

</th>
<td>
No

</td>
</tr>
<tr>
<th>
Default action

</th>
<td>
 ?

</td>
</tr>
</table>
## Notes

### Remarks

Use the [**componentFromPoint**](/dom/HTMLElement/componentFromPoint) and [**doScroll**](/dom/HTMLElement/doScroll) methods to control the scroll bar components. Cascading style sheets (CSS) enable scrolling on all objects through the [**overflow**](/css/properties/overflow) property. These objects are not listed in the Applies To list for this event. Scrolls the contents of an object until new portions of the object become visible. To invoke this event, do one of the following:

-   Click and drag the scroll box with the mouse.
-   Click the scroll arrow.
-   Click the scroll bar.
-   Invoke the [**doScroll**](/dom/HTMLElement/doScroll) method.
-   Press the HOME or END key
-   Press the SPACEBAR key.
-   Press the PAGE UP or PAGE DOWN key.
-   Press the ARROW UP or ARROW DOWN key until scrolling occurs.

The *pEvtObj* parameter is required for the following interfaces:

-   **HTMLAnchorEvents2**
-   **HTMLAreaEvents2**
-   **HTMLButtonElementEvents2**
-   **HTMLControlElementEvents2**
-   **HTMLDocumentEvents2**
-   **HTMLElementEvents2**
-   **HTMLFormElementEvents2**
-   **HTMLImgEvents2**
-   **HTMLFrameSiteEvents2**
-   **HTMLInputFileElementEvents2**
-   **HTMLInputImageEvents2**
-   **HTMLInputTextElementEvents2**
-   **HTMLLabelEvents2**
-   **HTMLLinkElementEvents2**
-   **HTMLMapEvents2**
-   **HTMLMarqueeElementEvents2**
-   **HTMLObjectElementEvents2**
-   **HTMLOptionButtonElementEvents2**
-   **HTMLScriptEvents2**
-   **HTMLSelectElementEvents2**
-   **HTMLStyleElementEvents2**
-   **HTMLTableEvents2**
-   **HTMLTextContainerEvents2**
-   **HTMLWindowEvents2**
-   **HTMLDocumentEvents4**

### Syntax

### Standards information

There are no standards that apply here.

### Event handler parameters

*pEvtObj* [in]
:   Type: ****IHTMLEventObj****

