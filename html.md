# HTML





- [Attributes](#attributes)
- [Class](#class)
- [Comments](#comments)
- [ID](#id)
- [Line formatting](#line-formatting)
- [Semantics](#semantics)





## Attributes

When setting attributes on tags, follow these rules:

1. The tag's closely associated attributes should come first, e.g. for `<a>`, their `href` attribute should comes first; for `<input>`, their `type` attribute should come first.
2. CSS-related attributes should come next, and should be sorted in order of specificity, which is `class`, then `style`.
3. JS-related attributes should come last.
4. Use one space character to separate each individual attribute.
5. Use *three* space characters to separate the three *groups* of attributes mentioned above.
6. Arrange them consistently when using on multiple elements.

```html
<!-- Don't: -->
<button class="Button" id="Reset" type="button">
    Reset
</button>

<button type="button" id="Submit" data-ga-track="reset" class="Button" style="margin-left: 5px;">
    Submit
</button>

<!-- Do: -->
<button type="button"   class="Button"   id="Reset">
    Reset
</button>

<button type="button"   class="Button" style="margin-left: 5px;"   data-ga-track="reset" id="Submit">
    Submit
</button>
```





## Class

When setting multiple classes on a single tag:

1. Arrange the classes in this order:
    1. Component Classes first.
    2. Local Classes second.
    3. Utility Classes last.
2. Separate Component and Local Classes using three space characters.
3. When using Modifier Classes, place them *after* their associated base class, separated with one space character.
4. Utility Classes should be individually spaced with one space character. When using responsive Utility Classes, group them up baseed on their media query, arranged from smallest to largest, and separate each group with three space characters.
5. Arrange them consistently when using on multiple elements.

:exclamation: Be sure to check out the [CSS](css.md) guide for more details on [Component Classes](css.md#component-classes), [Local Classes](css.md#local-classes), [Modifier Classes](css.md#modifier-classes), and [Utility Classes](css.md#utility-classes).

```html
<!-- Don't: -->
<div class="p:1 popup panel Register-Popup MNP-Popup --compact --Super p:3@md p:2@sm m:2@md m:1@sm">
    ...
</div>

<!-- Do: -->
<div class="popup --compact   Register-Popup --Super   p:1   p:2@sm m:1@sm   p:3@md m:2@md">
    ...
</div>
```





## Comments

HTML comments are quite uncommon for me. I usually use comments to explain things, and that requirement doesn't come up often in HTML.

I do not use them to mark closing tags, as I believe good formatting and indentation will allow me to easily collapse sections of code in my text editors.





## ID

I currently camelCase my IDs — no particular reason for it, and I haven't stumbled upon anything that would strongly convince me to stick to a specific case convention.

For the sake of this coding guide, though, I personally see two patterns for it in my own usage:

1. If the ID is mainly used for JavaScript purposes, I will camelCase it.
2. If the ID has some style associated it (*gasp!*), I will hyphenate it.

```html
<div id="mainHeader"></div> <!-- For JavaScript purposes -->
<div id="media-query"></div> <!-- Has styles associated with it -->
```

:question: **What is this about setting styles on IDs!?** Well, it's not so much styling, but more like a way to pass in data from CSS, to be consumed in JS. My most common use for this is media query detection, as media queries are a very CSS-thing that I don't want to decouple from the JS side.

:exclamation: **When it comes to integration with back-end** (especially .NET and `<input>`), there is typically a decent chance of the ID being replaced by a server-generated ID of some sort, so I generally try not to rely on using IDs if possible. For example, rather than using IDs to link a `<label>` with an `<input>`, just wrap the `<label>` around the target `<input>`.





## Line formatting

When using elements with both an opening and closing tag, always format it into multiple lines with proper indentation, *unless*:

1. The element has *zero* attributes, and
2. The element only has text contents; it does not have any child elements.

If the element satisfies the above two conditions, format it into a single line.

```html
<!-- Don't: -->
<div class="class-name">Lorem ipsum dolor sit amet, consectetur adipisicing elit.</div>

<p><strong>Lorem ipsum dolor sit amet.</strong></p>

<p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit.
</p>

<!-- Do: -->
<div class="class-name">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit.
</div>

<p>
    <strong>Lorem ipsum dolor sit amet.</strong>
</p>

<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.</p>
```





## Semantics

Proper usage of headings, lists, paragraphs, etc. is a good idea in general, but I need a much more concrete way to figure out what's right and what's wrong, and a much more obvious way to outline the tangible differences.

At my current experience, my rule of thumb is:

1. Use the relevant tag only if I'm fairly confident on its semantics, e.g. I've read up about it on a site like HTML5 Doctor, and have used it multiple times already;
2. If I'm not very sure, or if it's a tag that I've barely used, then I will refrain from using it unless I have some spare time to properly read up about it;
3. Everything else will fall into good ol' `<div>` and `<span>`, because semantic mistakes seem to be the worser option compared to zero semantics.

Low hanging fruits that I've stuck with are:

- Typography:
    - Blockquotes, `<blockquote>`
    - Definition lists, `<dl>` and its child elements, `<dt>` and `<dd>`
    - Headings: `<h1>` down to `<h6>`
    - Inline formatting: `<strong>` vs `<b>`; `<em>` vs `<i>`; `<strike>`
    - Lists: `<ul>` and `<ol>`
    - Paragraphs: `<p>`
- Forms: `<form>`, `<input>`, `<button>`, `<label>`
- Sectioning: `<section>`, `<aside>`, `<main>`, `<header>`, `<footer>`, `<nav>`
- Using anchors `<a>` for links that primarily take us to a different page; using `<button>` for clickable elements that primarily run JavaScript
- `<img>` for images that are are part of the content, and `background-image` for images that are decorative in nature