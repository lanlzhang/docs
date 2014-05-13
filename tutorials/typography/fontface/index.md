{{Page_Title}}
{{Flags
|High-level issues=Needs Review
|Checked_Out=No
}}
{{Byline
|Name=Dave Gash
|Published=14 May 2014
}}
{{Summary_Section|An introduction to the JavaScript FontFace object and font loading.

}}
{{Tutorial
|Content====Introduction===

The CSS ''@font-face'' property is a powerful and flexible feature that allows you to use custom fonts in your web pages. (If you aren't familiar with @font-face, please read Paul Irish's excellent [[wiki/tutorials/typography/font-face|@font-face tutorial]] first and then come back. It's okay, we'll wait.)

But while @font-face works fine for pre-coded pages, many of us would also like to use custom fonts on the fly via scripting. This has historically been difficult to accomplish, but has now become much more straightforward with the introduction of the Javascript '''FontFace''' object.

At its core, FontFace is a new interface used for dynamically accessing font resources through scripting. With FontFace, you can load, add, and use custom fonts at any time by manipulating the object in script.

'''Note:''' As of this writing the FontFace object is only available in Google Chrome Canary, which you can get [https://www.google.com/intl/en/chrome/browser/canary.html here].

===Background===

Interestingly, a manually created CSS @font-face rule actually defines a Javascript FontFace object, with its properties set to the same values as the @font-face. The FontFace object is said to be ''CSS-connected''. Thus you can manipulate a manual @font-face with script, but that isn't exactly what we're after.

Of course, you can also create @font-face rule from scratch and "shoehorn" it into the page's stylesheet using the ''.insertRule()'' method, but that's also not the goal here.

While your script can certainly interact with manual @font-face rules, or create and manipulate CSS rules directly, in this tutorial we'll be focusing on independently creating and using FontFace objects.

===Preparing the Fonts===

Before we can begin using a custom font, we have to ''have'' a custom font. As covered in the 
[[wiki/tutorials/typography/font-face|@font-face tutorial]],
in order to ensure cross-browser compatibility you should have these versions of your font available: 
*Embedded Open Type (.eot), specifically for Internet Explorer
*True Type Font (.ttf), for Safari, Opera, Firefox, and Chrome
*Web Open Font Format (.woff), for Firefox, Chrome, Opera, and IE9
*Scalable Vector Graphics (.svg), for iPhones, iPads, and other devices that run Mobile Safari

The easiest way to convert an existing font in any of these formats to all the others is at the excellent
[http://www.fontsquirrel.com/tools/webfont-generator Font Squirrel] webfonts generator. 
Font Squirrel is a free online tool that uploads your original font, creates the required variants, and zips it up into a downloadable package.

Naturally, the font variants must all be available on the server to the pages that use them, either in the same folder or a defined path. And -- this should go without saying, but let's say it anyway -- you '''must''' be sure that the font you want to use is licensed for web use. For this article we're using an absolutely free and web-licensed font called [http://www.fontsquirrel.com/fonts/finger-paint FingerPaint], available (along with many others) at Font Squirrel.

===Creating the FontFace Object===

This is pretty straightforward; you create a FontFace with the JavaScript '''new''' keyword as you would any other object.

<pre>
var f = new FontFace("fingerpaint", "url(fingerpaint-regular-webfont.ttf)", {});
</pre>

The first parameter is the user-defined name. Call it whatever you like, but use common sense; later, you'll need to refer to the font by that name.

The second parameter is the URL of the font file. As you can see, we're using the True Type version for this example.

The third parameter is the attribute list, such as ''family'', ''style'', ''weight'', etc. As this is obviously optional, just include the empty braces and don't worry about it for now.

That defines the JavaScript FontFace object and requests that the browser locate it and associate it with the object. But the page doesn't know it's there yet.

===Adding the Font to the Page===

The next step is to add the FontFace to the document; a font cannot be used until it exists in the document's '''FontFaceSet''' object. The FontFaceSet is implicitly referenced through the document's '''fonts''' property. Thus, this

<pre>
var f = new FontFace("fingerpaint", "url(fingerpaint-regular-webfont.ttf)", {});
document.fonts.add(f);
</pre>

should add the FontFace to the page's font list. And it would, 
''if the FontFace were loaded''... but it isn't. Font families are automatically loaded only when they are used, and this one has been identified but not yet used. So we need to explictly force the font to be loaded with the (what else?) '''load()''' method.

To determine when the load is accomplished, 
we'll combine the load call with the (also new) JavaScript '''Promise''' feature. If you want to read up on promises, see 
[http://www.html5rocks.com/en/tutorials/es6/promises/ this excellent HTML5Rocks article]. 
But briefly, a JavaScript promise is a pattern for handling asynchronous operations. It operates a bit like an event listener, and lets you call a '''then()''' method that contains a callback function to be executed when the calling method is complete ("the promise is fulfilled"). So this

<pre>
var f = new FontFace("fingerpaint", "url(fingerpaint-regular-webfont.ttf)", {});
f.load().then(function (loadedFace) {
  . . .
});
</pre>

will invoke the load and then execute the anonymous function when the load is done.

What should the function do? At the very least, it should add the now loaded font to the FontFaceSet via the fonts list.

<pre>
var f = new FontFace("fingerpaint", "url(fingerpaint-regular-webfont.ttf)", {});
f.load().then(function (loadedFace) {
  document.fonts.add(loadedFace);
});
</pre>

So far, so good. The font is identified and loaded, but we still haven't actually seen it anywhere on the page.

===Using the FontFace===

There are any number of ways to assign the font to one or more HTML elements, and any number of places to put the assignment. Perhaps the most straightforward is within the anonymous function itself; that keeps all the font usage code localized, so that when the FontFace load is complete, the font is added to the document.fonts property and then applied immediately. For example, this

<pre>
var f = new FontFace("fingerpaint", "url(fingerpaint-regular-webfont.ttf)", {});
f.load().then(function (loadedFace) {
  document.fonts.add(loadedFace);
  document.body.style.fontFamily = "fingerpaint, serif";
});
</pre>

sets the entire document body to the new font, and falls back to ''serif'' if there's a problem. (As with any font assignment, always include one or more fallbacks.)

But that's a pretty broad application, especially for a whimsical font like Finger Paint. It would make more sense to only apply the font to a specific set of tags, such as just those with a class of "fp". So this

<pre>
var f = new FontFace("fingerpaint", "url(fingerpaint-regular-webfont.ttf)", {});
f.load().then(function (loadedFace) {
  document.fonts.add(loadedFace);
  var fptags = document.getElementsByClassName("fp");
  for (var i = 0; i < fptags.length; i++) {
    fptags[i].style.fontFamily = "fingerpaint, serif"; 
  }
});
</pre>

would do the trick, selecting any tags with the independent class of "fp" and applying the Finger Paint font to them.

Or, if you'd rather not rely on pre-assigned classes, you might opt to set all the H2s in the document to display in Finger Paint. If so, this

<pre>
var f = new FontFace("fingerpaint", "url(fingerpaint-regular-webfont.ttf)", {});
f.load().then(function (loadedFace) {
  document.fonts.add(loadedFace);
  var h2s = document.getElementsByTagName("h2");
  for (var i = 0; i < h2s.length; i++) {
    h2s[i].style.fontFamily = "fingerpaint, serif"; 
  }
});
</pre>

is what you need. Again, applying the font in the same place, code-wise, where it is loaded and added keeps the font code together and aids in debugging and maintenance.

===Summary===

Although the CS @font-face rule has been around for a long time and is the go-to guy for pre-written pages using static web fonts, it doesn't satisfy the scripter's need to identify, load, and use custom fonts on the fly. The JavaScript FontFace object does just that, cleanly and without hassle. 

Now it's your turn. Have a go!

}}
{{Notes_Section}}
{{Compatibility_Section
|Not_required=No
|Imported_tables=
|Desktop_rows=
|Mobile_rows=
|Notes_rows=
}}
{{See_Also_Section}}
{{Topics}}
{{External_Attribution
|Is_CC-BY-SA=No
|MDN_link=
|MSDN_link=
|HTML5Rocks_link=
}}