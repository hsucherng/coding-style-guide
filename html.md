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
6. Always arrange them consistently when using on multiple elements.

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

When setting multiple classes on a single tag, follow these rules:

1. Component classes should come first, and should be limited to one only. They can be accompanied by as many modifier classes as needed.
2. Page-specific classes should come next, and should also be limited to one only. They can also be accompanied by as many modifier classes as needed.
3. Utility classes should come last. Use as many as needed.
4. Use one space character to separate classes within the same group.
5. Use *three* space characters to separate the three *groups* of classes mentioned above.
6. Always arrange them consistently when using on multiple elements.

For more details in regards to component classes vs. page-specific classes vs utility classes vs modifier classes, do check out the [CSS](css.md) guide.

:question: **Why** limit component classes to one only? The main purpose of component classes is to be able to use them throughout the site and have predictable outcomes. Mixing multiple component classes goes against this purpose, and I feel that the trade-off isn't worth going through just for the sake of reducing the element count by one.

:question: **Why** then do I allow page-specific classes to be used together with component classes? Because the main purpose of a page-specific class is to actually add to, complement, or maybe even override the style of the component class.

```html
<!-- Don't: -->
<div class="pd:1 Popup Panel _Register-popup _MNP-popup --compact _--super">
    ...
</div>

<!-- Do: -->
<div class="Popup --compact   _Register-popup _--super   pd:1">
    ...
</div>
```

## Comments

HTML comments are quite uncommon for me. I usually use comments to explain things, and that requirement doesn't come up often in HTML.

I do not use them to mark closing tags, as I believe good formatting and indentation will allow me to easily collapse sections of code in my text editors.

## ID

I currently camelCase my IDs — no particular reason for it, and I haven't stumbled upon anything that would strongly convince to stick to a specific case convention.

For the sake of this coding guide, though, I personally see two patterns for it in my own usage:

1. If the ID is mainly used for JavaScript purposes, I will camelCase it.
2. If the ID has some style associated it (*gasp!*), I will hyphenate it.

```html
<div id="mainHeader"></div> <!-- For JavaScript purposes -->
<div id="media-query"></div> <!-- Has styles associated with it -->
```

:question: **What** is this about setting styles on IDs!? Well, it's not so much styling, but more like a way to pass in data from CSS, to be consumed in JS. My most common use for this is media query detection, as media queries are a very CSS-thing that I don't want to decouple from the JS side.

:exclamation: When it comes to integration with **back-end** (especially .NET and `<input>`), there is typically a decent chance of the ID being replaced by a server-generated ID of some sort, so I generally try not to rely on using IDs if possible. For example, rather than using IDs to link a `<label>` with an `<input>`, just wrap the `<label>` around the target `<input>`.

## Line formatting

When using elements with both an opening and closing tag, always format it into muliple lines with proper indentation, *unless*:

1. The element has *zero* attributes, and
2. The element only has text contents; it does not have any child elements.

If the element satisfies the above two conditions, then I will format it into a single line.

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
- `<img>` for images that are significant in terms of content, and `background-image` for images that are decorative in nature